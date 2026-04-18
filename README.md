
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>IYSO Portal</title>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

<style>
:root {
    --iyso-green:#006837;
    --iyso-gold:#c6a34f;
    --dark-bg:#04070a;
}
body {
    background: radial-gradient(circle at top right, #003d21, var(--dark-bg) 70%);
    color:#fff;
}
body::before {
    content:"";
    position:fixed;
    top:50%;left:50%;
    transform:translate(-50%,-50%);
    width:60vw;height:60vw;
    background:url('image_0.png') no-repeat center;
    background-size:contain;
    opacity:0.05;
}
#sidebar {
    width:250px;height:100vh;
    position:fixed;
    background:#000;
    padding:20px;
}
.main-content { margin-left:260px; padding:30px; }
.nav-link { color:#aaa; cursor:pointer; }
.nav-link.active { color:#fff; background:var(--iyso-green); }
.glass { background:#111; padding:20px; border-radius:15px; }
</style>
</head>

<body>

<div id="sidebar">
    <div class="text-center">
        <img src="image_0.png" height="60">
        <h6>IYSO</h6>
    </div>

    <div class="nav flex-column mt-4">
        <div class="nav-link active" onclick="showSection('overview',event)">Dashboard</div>
        <div class="nav-link" onclick="showSection('members',event)">Members</div>
    </div>
</div>

<div class="main-content">

<div id="overview" class="page-section">
<h3>Dashboard</h3>
<div class="glass">
<h4 id="balance">৳0</h4>
</div>
</div>

<div id="members" class="page-section" style="display:none">
<h3>Members</h3>
<button class="btn btn-success mb-3" onclick="openMemberModal()">Add Member</button>
<div id="member-list" class="row"></div>
</div>

</div>

<!-- LOGIN MODAL -->
<div class="modal fade" id="loginModal">
<div class="modal-dialog">
<div class="modal-content bg-dark p-4">
<h4>Admin Login</h4>
<input id="email" class="form-control my-2" placeholder="Email">
<input id="pass" type="password" class="form-control my-2" placeholder="Password">
<button class="btn btn-success w-100" onclick="login()">Login</button>
</div>
</div>
</div>

<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getFirestore, collection, addDoc, onSnapshot, doc, updateDoc, deleteDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";
import { getAuth, signInWithEmailAndPassword } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

const firebaseConfig = {
    apiKey:"YOUR_KEY",
    authDomain:"YOUR_DOMAIN",
    projectId:"YOUR_ID"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
const auth = getAuth(app);

let isAdmin = false;

window.login = async () => {
    const email = document.getElementById('email').value;
    const pass = document.getElementById('pass').value;

    try {
        await signInWithEmailAndPassword(auth, email, pass);
        if(email === "iysoadmin@iyso.com") isAdmin = true;
        alert("Login Success");
        location.reload();
    } catch {
        alert("Login Failed");
    }
};

window.showSection = (id,e) => {

    if(id === 'overview' && !isAdmin){
        new bootstrap.Modal(document.getElementById('loginModal')).show();
        return;
    }

    document.querySelectorAll('.page-section').forEach(s=>s.style.display='none');
    document.getElementById(id).style.display='block';

    document.querySelectorAll('.nav-link').forEach(n=>n.classList.remove('active'));
    e.target.classList.add('active');
};

window.openMemberModal = async (id=null,data={}) => {

    if(!isAdmin) return alert("Admin only");

    const name = prompt("Name:",data.name||"");
    const mid = prompt("Member ID:",data.memberId||"");
    const desig = prompt("Designation:",data.desig||"");
    const phone = prompt("Phone:",data.phone||"");
    const blood = prompt("Blood:",data.blood||"");
    const photo = prompt("Photo URL:",data.photo||"");

    if(name && mid){
        const obj = {name,memberId:mid,desig,phone,blood,photo};

        if(id) await updateDoc(doc(db,"members",id),obj);
        else await addDoc(collection(db,"members"),obj);
    }
};

window.deleteMember = async (id)=>{
    if(!isAdmin) return;
    if(confirm("Delete?")) await deleteDoc(doc(db,"members",id));
};

onSnapshot(collection(db,"members"),snap=>{
    let html="";
    snap.forEach(d=>{
        const m=d.data();

        html+=`
        <div class="col-md-4">
        <div class="glass">
        <img src="${m.photo||'https://via.placeholder.com/80'}" width="60" class="rounded-circle">
        <h5>${m.name}</h5>
        <small>${m.memberId}</small><br>
        <small>${m.phone}</small><br>
        <small>${m.blood||''}</small>

        ${isAdmin ? `
        <div class="mt-2">
        <button onclick='openMemberModal("${d.id}",${JSON.stringify(m)})' class="btn btn-sm btn-warning">Edit</button>
        <button onclick='deleteMember("${d.id}")' class="btn btn-sm btn-danger">Delete</button>
        </div>` : ''}

        </div>
        </div>`;
    });

    document.getElementById("member-list").innerHTML = html;
});

</script>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

</body>
</html>
