
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>IYSO Premium Dashboard</title>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
body { background:#05080c; color:#fff; font-family:sans-serif; }
.sidebar { width:240px; position:fixed; height:100vh; background:#000; padding:20px; }
.main { margin-left:260px; padding:20px; }
.glass { background:#111; padding:20px; border-radius:15px; }
.nav-link { color:#aaa; cursor:pointer; margin-bottom:10px; }
.nav-link.active { color:#fff; background:#006837; padding:8px; border-radius:8px; }
.stat { font-size:24px; color:#c6a34f; }
</style>
</head>

<body>

<div class="sidebar">
<h3>IYSO</h3>
<div class="nav-link active" data-page="dash">Dashboard</div>
<div class="nav-link" data-page="members">Members</div>
<div class="nav-link" data-page="donations">Donations</div>
<div class="nav-link" data-page="events">Events</div>
</div>

<div class="main">

<!-- DASHBOARD -->
<div id="dash" class="page">
<h3>Dashboard</h3>

<div class="row">
<div class="col-md-4"><div class="glass">Total Fund<div id="totalFund" class="stat">0</div></div></div>
<div class="col-md-4"><div class="glass">Monthly Fund<div id="monthlyFund" class="stat">0</div></div></div>
<div class="col-md-4"><div class="glass">Real Balance<div id="balanceFund" class="stat">0</div></div></div>
</div>

<div class="row mt-4">
<div class="col-md-6"><div class="glass"><canvas id="donationChart"></canvas></div></div>
<div class="col-md-6"><div class="glass"><canvas id="eventChart"></canvas></div></div>
</div>

<div class="row mt-4">
<div class="col-md-6"><div class="glass"><canvas id="monthlyTrendChart"></canvas></div></div>
<div class="col-md-6"><div class="glass"><div id="topDonors"></div></div></div>
</div>

</div>

<div id="members" class="page" style="display:none;"><div id="memberList"></div></div>
<div id="donations" class="page" style="display:none;"><div id="donationList"></div></div>
<div id="events" class="page" style="display:none;"><div id="executeList"></div></div>

</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getFirestore, collection, onSnapshot } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

const firebaseConfig = {
    apiKey: "YOUR_KEY",
    projectId: "iyso-web"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

// NAV
document.querySelectorAll('.nav-link').forEach(link=>{
    link.onclick=()=>{
        document.querySelectorAll('.nav-link').forEach(l=>l.classList.remove('active'));
        link.classList.add('active');
        document.querySelectorAll('.page').forEach(p=>p.style.display='none');
        document.getElementById(link.dataset.page).style.display='block';
    }
});

let donationChart, eventChart, monthlyTrendChart;

// ================= DONATIONS =================
onSnapshot(collection(db,"donations"),snap=>{

let total=0, monthly=0, event=0;
let monthlyMap={}, donorMap={};

snap.forEach(d=>{
    const x=d.data();
    total+=x.amount||0;

    if(x.type==="monthly") monthly+=x.amount;
    else event+=x.amount;

    // monthly trend
    if(x.date){
        const m=x.date.slice(0,7);
        monthlyMap[m]=(monthlyMap[m]||0)+x.amount;
    }

    // top donor
    if(x.uid){
        donorMap[x.uid]=donorMap[x.uid]||{name:x.name,total:0};
        donorMap[x.uid].total+=x.amount;
    }
});

document.getElementById("totalFund").innerText=`$${total}`;
document.getElementById("monthlyFund").innerText=`$${monthly}`;

// pie chart
if(donationChart) donationChart.destroy();
donationChart=new Chart(document.getElementById('donationChart'),{
type:'doughnut',
data:{labels:['Monthly','Event'],datasets:[{data:[monthly,event]}]}
});

// monthly trend
const months=Object.keys(monthlyMap).sort();
const values=months.map(m=>monthlyMap[m]);

if(monthlyTrendChart) monthlyTrendChart.destroy();
monthlyTrendChart=new Chart(document.getElementById('monthlyTrendChart'),{
type:'line',
data:{labels:months,datasets:[{data:values}]}
});

// top donors
const top=Object.values(donorMap).sort((a,b)=>b.total-a.total).slice(0,5);
let html="<ul>";
top.forEach(d=>{
html+=`<li>${d.name} - $${d.total}</li>`;
});
html+="</ul>";
document.getElementById("topDonors").innerHTML=html;

});

// ================= EVENTS =================
onSnapshot(collection(db,"events"),snap=>{

let totalEventFund=0;
let totalEventCost=0;
let extraCost=0;

snap.forEach(d=>{
    const e=d.data();

    if(e.status==="Executed"){

        let fund=Number(e.fund)||0;
        let cost=Number(e.cost)||0;

        totalEventFund+=fund;
        totalEventCost+=cost;

        if(cost>fund){
            extraCost+=(cost-fund);
        }
    }
});

// REAL BALANCE
const mainFund = Number(document.getElementById("totalFund").innerText.replace('$','')) || 0;
const realBalance = mainFund - extraCost;

document.getElementById("balanceFund").innerText = `$${realBalance}`;

// chart
if(eventChart) eventChart.destroy();
eventChart=new Chart(document.getElementById('eventChart'),{
type:'bar',
data:{labels:['Fund','Cost'],datasets:[{data:[totalEventFund,totalEventCost]}]}
});

});

</script>

</body>
</html>
