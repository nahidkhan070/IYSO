
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>IYSO Premium Dashboard</title>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
:root{
--green:#006837;
--gold:#c6a34f;
--bg:#05080c;
--card:rgba(20,25,32,0.85);
}

body{
background: radial-gradient(circle at top right,#003d21,var(--bg));
color:#fff;
font-family:'Plus Jakarta Sans',sans-serif;
}

.sidebar{
width:250px;
height:100vh;
position:fixed;
background:rgba(0,0,0,0.6);
backdrop-filter:blur(20px);
padding:20px;
}

.main{
margin-left:260px;
padding:25px;
}

.nav-link{
color:#aaa;
margin-bottom:10px;
cursor:pointer;
}

.nav-link.active,.nav-link:hover{
color:#fff;
background:var(--green);
padding:8px;
border-radius:8px;
}

.glass{
background:var(--card);
border-radius:20px;
padding:20px;
backdrop-filter:blur(15px);
}

.stat{
font-size:28px;
font-weight:700;
}

</style>
</head>

<body>

<div class="sidebar">
<h4>IYSO</h4>
<div class="nav-link active" data="dash">Dashboard</div>
<div class="nav-link" data="members">Members</div>
<div class="nav-link" data="donations">Donations</div>
<div class="nav-link" data="events">Events</div>
</div>

<div class="main">

<!-- DASHBOARD -->
<div id="dash" class="page">

<h3>Dashboard</h3>

<div class="row g-3">
<div class="col-md-4">
<div class="glass">
<h6>Total Fund</h6>
<div class="stat" id="totalFund">0</div>
</div>
</div>

<div class="col-md-4">
<div class="glass">
<h6>Monthly Fund</h6>
<div class="stat" id="monthlyFund">0</div>
</div>
</div>

<div class="col-md-4">
<div class="glass">
<h6>Balance After Events</h6>
<div class="stat" id="balanceFund">0</div>
</div>
</div>
</div>

<div class="row mt-4">
<div class="col-md-6">
<div class="glass">
<canvas id="donationChart"></canvas>
</div>
</div>

<div class="col-md-6">
<div class="glass">
<canvas id="eventChart"></canvas>
</div>
</div>
</div>

</div>

<!-- MEMBERS -->
<div id="members" class="page" style="display:none;">
<h3>Members</h3>
<button onclick="openMember()" class="btn btn-success mb-3">Add</button>
<div id="memberList"></div>
</div>

<!-- DONATIONS -->
<div id="donations" class="page" style="display:none;">
<h3>Donations</h3>
<button onclick="openDonation()" class="btn btn-success mb-3">Add</button>
</div>

<!-- EVENTS -->
<div id="events" class="page" style="display:none;">
<h3>Events</h3>
<button onclick="openEvent()" class="btn btn-success mb-3">Add</button>
</div>

</div>

<!-- MODALS (same as before but styled) -->

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getFirestore, collection, addDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

const app = initializeApp({
apiKey:"YOUR_KEY",
projectId:"iyso-web"
});
const db=getFirestore(app);

// NAV
document.querySelectorAll('.nav-link').forEach(n=>{
n.onclick=()=>{
document.querySelectorAll('.page').forEach(p=>p.style.display='none');
document.getElementById(n.dataset.data).style.display='block';
};
});

// CHARTS
let donationChart, eventChart;

onSnapshot(collection(db,"donations"),snap=>{
let total=0,monthly=0,event=0;

snap.forEach(d=>{
let x=d.data();
total+=x.amount;
if(x.type==="monthly") monthly+=x.amount;
else event+=x.amount;
});

document.getElementById("totalFund").innerText=total;
document.getElementById("monthlyFund").innerText=monthly;

if(donationChart) donationChart.destroy();

donationChart=new Chart(document.getElementById('donationChart'),{
type:'doughnut',
data:{
labels:['Monthly','Event'],
datasets:[{data:[monthly,event]}]
}
});
});

onSnapshot(collection(db,"events"),snap=>{
let cost=0,fund=0;

snap.forEach(d=>{
let e=d.data();
fund+=e.fund;
cost+=e.cost;
});

let balance=fund-cost;
document.getElementById("balanceFund").innerText=balance;

if(eventChart) eventChart.destroy();

eventChart=new Chart(document.getElementById('eventChart'),{
type:'bar',
data:{
labels:['Fund Raised','Actual Cost'],
datasets:[{data:[fund,cost]}]
}
});
});

</script>

</body>
</html>
