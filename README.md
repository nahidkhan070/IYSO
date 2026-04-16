
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>IYSO Portal</title>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

<style>
body{background:#0b0f14;color:#fff;font-family:sans-serif}
#loginPage{display:flex;height:100vh;align-items:center;justify-content:center}
#app{display:none}
.sidebar{width:250px;position:fixed;height:100%;background:#000;padding:20px}
.main{margin-left:260px;padding:20px}
</style>
</head>
<body>

<!-- LOGIN PAGE -->
<div id="loginPage">
  <div class="card p-4" style="width:320px">
    <img src="image_0.png" style="width:80px;margin:auto">
    <h4 class="text-center mt-2">Admin Login</h4>
    <input id="email" class="form-control my-2" placeholder="Email">
    <input id="password" type="password" class="form-control my-2" placeholder="Password">
    <button onclick="login()" class="btn btn-success w-100">Login</button>
  </div>
</div>

<!-- MAIN APP -->
<div id="app">
  <div class="sidebar">
    <img src="image_0.png" width="80">
    <h5>IYSO</h5>
    <button onclick="logout()" class="btn btn-danger btn-sm">Logout</button>
  </div>

  <div class="main">
    <h2>Dashboard</h2>

    <button class="btn btn-success" onclick="addDonation()">+ Add Donation</button>
    <button class="btn btn-primary" onclick="exportExcel()">Export Excel</button>
    <button class="btn btn-warning" onclick="exportPDF()">Export PDF</button>

    <table class="table table-dark mt-3">
      <thead><tr><th>Name</th><th>Amount</th></tr></thead>
      <tbody id="donTable"></tbody>
    </table>
  </div>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getAuth, signInWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
import { getFirestore, collection, addDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

const firebaseConfig = {
 apiKey: "YOUR_KEY",
 authDomain: "YOUR_DOMAIN",
 projectId: "YOUR_PROJECT"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

// LOGIN
window.login = async () => {
 const email = document.getElementById('email').value;
 const password = document.getElementById('password').value;
 await signInWithEmailAndPassword(auth,email,password);
};

window.logout = () => signOut(auth);

onAuthStateChanged(auth, user => {
 if(user){
  document.getElementById('loginPage').style.display='none';
  document.getElementById('app').style.display='block';
 } else {
  document.getElementById('loginPage').style.display='flex';
  document.getElementById('app').style.display='none';
 }
});

// ADD DONATION
window.addDonation = async () => {
 const name = prompt("Donor Name");
 const amount = prompt("Amount");
 if(name && amount){
  await addDoc(collection(db,"donations"),{name,amount:parseFloat(amount)});
 }
};

// LIVE DATA
onSnapshot(collection(db,"donations"), snap=>{
 let html='';
 snap.forEach(d=>{
  const data=d.data();
  html+=`<tr><td>${data.name}</td><td>${data.amount}</td></tr>`;
 });
 document.getElementById('donTable').innerHTML=html;
});

// EXPORT EXCEL
window.exportExcel = () => {
 const table = document.getElementById('donTable');
 let data=[['Name','Amount']];
 [...table.rows].forEach(r=>{
  data.push([r.cells[0].innerText,r.cells[1].innerText]);
 });
 const ws = XLSX.utils.aoa_to_sheet(data);
 const wb = XLSX.utils.book_new();
 XLSX.utils.book_append_sheet(wb,ws,"Donations");
 XLSX.writeFile(wb,"donations.xlsx");
};

// EXPORT PDF
window.exportPDF = () => {
 const { jsPDF } = window.jspdf;
 const doc = new jsPDF();
 doc.text("Donation Report",10,10);
 let y=20;
 document.querySelectorAll('#donTable tr').forEach(r=>{
  doc.text(r.innerText,10,y);
  y+=10;
 });
 doc.save("report.pdf");
};

</script>
</body>
</html>
