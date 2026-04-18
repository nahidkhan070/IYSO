
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>IYSO | Full Management System</title>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<style>
body { background:#0b0f14; color:#fff; font-family:sans-serif; }
#sidebar { width:240px; position:fixed; height:100vh; background:#111; padding:20px; }
.main { margin-left:240px; padding:20px; }
.nav-link { color:#aaa; cursor:pointer; margin-bottom:10px; }
.nav-link.active, .nav-link:hover { color:#fff; }
.card { background:#1a1f26; border:none; }
</style>
</head>

<body>

<div id="sidebar">
    <h4>IYSO</h4>
    <div class="nav-link active" data="dashboard">Dashboard</div>
    <div class="nav-link" data="members">Members</div>
    <div class="nav-link" data="donations">Donations</div>
    <div class="nav-link" data="events">Events</div>
</div>

<div class="main">

<!-- DASHBOARD -->
<div id="dashboard" class="page">
    <h3>Dashboard</h3>
    <div class="row">
        <div class="col-md-4"><div class="card p-3"><h6>Total Fund</h6><h2 id="totalFund">0</h2></div></div>
        <div class="col-md-4"><div class="card p-3"><h6>Monthly Donations</h6><h2 id="monthlyFund">0</h2></div></div>
        <div class="col-md-4"><div class="card p-3"><h6>Event Balance Used</h6><h2 id="eventCost">0</h2></div></div>
    </div>
</div>

<!-- MEMBERS -->
<div id="members" class="page" style="display:none;">
    <h3>Members</h3>
    <button onclick="openMember()">Add Member</button>
    <div id="memberList"></div>
</div>

<!-- DONATIONS -->
<div id="donations" class="page" style="display:none;">
    <h3>Donations</h3>
    <button onclick="openDonation()">Add Donation</button>
    <div id="donationList"></div>
</div>

<!-- EVENTS -->
<div id="events" class="page" style="display:none;">
    <h3>Events</h3>
    <button onclick="openEvent()">Add Event</button>
    <div id="eventList"></div>
</div>

</div>

<!-- MODALS -->

<!-- MEMBER -->
<div class="modal" id="memberModal">
<div class="modal-dialog">
<div class="modal-content bg-dark text-white p-3">
<input id="mName" placeholder="Name" class="form-control mb-2">
<input id="mId" placeholder="Member ID" class="form-control mb-2">
<input id="mContact" placeholder="Contact" class="form-control mb-2">
<input id="mBlood" placeholder="Blood Group" class="form-control mb-2">
<button onclick="saveMember()">Save</button>
</div></div></div>

<!-- DONATION -->
<div class="modal" id="donationModal">
<div class="modal-dialog">
<div class="modal-content bg-dark text-white p-3">
<input id="dName" placeholder="Name" class="form-control mb-2">
<input id="dAmount" type="number" placeholder="Amount" class="form-control mb-2">
<select id="dType" class="form-control mb-2">
<option value="monthly">Monthly</option>
<option value="event">Event</option>
</select>
<input id="dEvent" placeholder="Event Name (if event donation)" class="form-control mb-2">
<button onclick="saveDonation()">Save</button>
</div></div></div>

<!-- EVENT -->
<div class="modal" id="eventModal">
<div class="modal-dialog">
<div class="modal-content bg-dark text-white p-3">
<input id="eName" placeholder="Event Name" class="form-control mb-2">
<input id="eDate" type="date" class="form-control mb-2">
<input id="eBudget" type="number" placeholder="Budget" class="form-control mb-2">
<input id="eFund" type="number" placeholder="Fund Raised" class="form-control mb-2">
<input id="eCost" type="number" placeholder="Actual Cost" class="form-control mb-2">
<button onclick="saveEvent()">Save</button>
</div></div></div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getFirestore, collection, addDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

const app = initializeApp({
    apiKey:"YOUR_KEY",
    projectId:"iyso-web"
});

const db = getFirestore(app);

// NAV
document.querySelectorAll('.nav-link').forEach(n=>{
    n.onclick=()=>{
        document.querySelectorAll('.page').forEach(p=>p.style.display='none');
        document.getElementById(n.dataset.data).style.display='block';
    }
});

// MEMBERS
window.openMember=()=>memberModal.style.display='block';

window.saveMember=async()=>{
await addDoc(collection(db,"members"),{
name:mName.value,
memberId:mId.value,
contact:mContact.value,
blood:mBlood.value
});
memberModal.style.display='none';
};

onSnapshot(collection(db,"members"),snap=>{
let html="";
snap.forEach(d=>{
let m=d.data();
html+=`<div>${m.name} (${m.memberId}) - ${m.contact} - ${m.blood}</div>`;
});
memberList.innerHTML=html;
});

// DONATIONS
window.openDonation=()=>donationModal.style.display='block';

window.saveDonation=async()=>{
await addDoc(collection(db,"donations"),{
name:dName.value,
amount:Number(dAmount.value),
type:dType.value,
event:dEvent.value || null
});
donationModal.style.display='none';
};

// EVENTS
window.openEvent=()=>eventModal.style.display='block';

window.saveEvent=async()=>{
await addDoc(collection(db,"events"),{
name:eName.value,
date:eDate.value,
budget:Number(eBudget.value),
fund:Number(eFund.value),
cost:Number(eCost.value)
});
eventModal.style.display='none';
};

// DASHBOARD CALCULATION
onSnapshot(collection(db,"donations"),snap=>{
let total=0, monthly=0;
snap.forEach(d=>{
let x=d.data();
total+=x.amount;
if(x.type==="monthly") monthly+=x.amount;
});
document.getElementById("totalFund").innerText=total;
document.getElementById("monthlyFund").innerText=monthly;
});

onSnapshot(collection(db,"events"),snap=>{
let cost=0;
snap.forEach(d=>{
let e=d.data();
if(e.cost>e.fund){
cost += (e.cost - e.fund);
}
});
document.getElementById("eventCost").innerText=cost;
});
</script>

</body>
</html>
