
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>IYSO | Management Portal</title>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<style>
:root {
    --iyso-green: #006837;
    --iyso-gold: #c6a34f;
    --dark-bg: #04070a;
    --card-bg: rgba(17, 24, 32, 0.9);
}

body {
    background: radial-gradient(circle at top right, #003d21, var(--dark-bg) 70%);
    color: #e9ecef;
    font-family: 'Plus Jakarta Sans', sans-serif;
}

/* WATERMARK */
body::before {
    content: "";
    position: fixed;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    width: 70vw;
    background: url('image_0.png') no-repeat center;
    background-size: contain;
    opacity: 0.03;
    z-index: -1;
}

/* SIDEBAR */
#sidebar {
    width: 260px;
    height: 100vh;
    position: fixed;
    background: rgba(0,0,0,0.6);
    backdrop-filter: blur(25px);
    padding: 30px 20px;
}

.main-content {
    margin-left: 260px;
    padding: 25px;
}

/* NAV */
.nav-link {
    color: #8a949d;
    padding: 12px;
    border-radius: 10px;
    margin-bottom: 5px;
    cursor: pointer;
}

.nav-link.active,
.nav-link:hover {
    background: var(--iyso-green);
    color: white;
}

/* TOPBAR */
.topbar {
    background: rgba(0,0,0,0.5);
    padding: 15px;
    border-radius: 15px;
    margin-bottom: 20px;
}

/* CARDS */
.stat-card {
    background: var(--card-bg);
    border-radius: 20px;
    padding: 20px;
    display: flex;
    justify-content: space-between;
}

.stat-card:hover {
    border: 1px solid var(--iyso-gold);
}

.member-card {
    background: var(--card-bg);
    padding: 15px;
    border-radius: 15px;
}

.page-section { display: none; }
.page-section.active { display: block; }

</style>
</head>

<body>

<div id="sidebar">
    <div class="text-center mb-4">
        <img src="image_0.png" height="60">
        <h5>IYSO PORTAL</h5>
    </div>

    <div class="nav flex-column">
        <div class="nav-link active" data-section="overview">Dashboard</div>
        <div class="nav-link" data-section="members">Members</div>
    </div>
</div>

<div class="main-content">

<div class="topbar d-flex justify-content-between">
    <h5>Dashboard</h5>
    <button class="btn btn-success" onclick="openModal()">+ Add Member</button>
</div>

<!-- DASHBOARD -->
<div id="overview" class="page-section active">
    <div class="row g-3">
        <div class="col-md-6">
            <div class="stat-card">
                <div>
                    <h6>Monthly</h6>
                    <h2 id="monthly-stat">৳0</h2>
                </div>
                <i class="fas fa-coins"></i>
            </div>
        </div>

        <div class="col-md-6">
            <div class="stat-card">
                <div>
                    <h6>Yearly</h6>
                    <h2 id="yearly-stat">৳0</h2>
                </div>
                <i class="fas fa-chart-line"></i>
            </div>
        </div>
    </div>
</div>

<!-- MEMBERS -->
<div id="members" class="page-section">
    <div class="d-flex justify-content-between mb-3">
        <h4>Members (<span id="member-count">0</span>)</h4>

        <input id="searchInput" class="form-control" placeholder="Search..." style="width:200px;">
    </div>

    <div id="member-grid" class="row g-3"></div>
</div>

</div>

<!-- MODAL -->
<div class="modal fade" id="memberModal">
  <div class="modal-dialog">
    <div class="modal-content bg-dark text-white">
      <div class="modal-header">
        <h5 id="modalTitle">Add Member</h5>
      </div>
      <div class="modal-body">
        <input id="name" class="form-control mb-2" placeholder="Name">
        <input id="mid" class="form-control" placeholder="Member ID">
      </div>
      <div class="modal-footer">
        <button class="btn btn-success" onclick="saveMember()">Save</button>
      </div>
    </div>
  </div>
</div>

<!-- DELETE MODAL -->
<div class="modal fade" id="deleteModal">
  <div class="modal-dialog modal-sm">
    <div class="modal-content bg-dark text-white text-center p-3">
        <h6>Delete this member?</h6>
        <div class="mt-3">
            <button class="btn btn-danger" onclick="confirmDelete()">Yes</button>
            <button class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
        </div>
    </div>
  </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getFirestore, collection, addDoc, onSnapshot, updateDoc, deleteDoc, doc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

const firebaseConfig = {
    apiKey: "YOUR_KEY",
    authDomain: "iyso-web.firebaseapp.com",
    projectId: "iyso-web"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

// NAV
document.querySelectorAll('.nav-link').forEach(link => {
    link.onclick = () => {
        document.querySelectorAll('.page-section, .nav-link').forEach(el => el.classList.remove('active'));
        document.getElementById(link.dataset.section).classList.add('active');
        link.classList.add('active');
    };
});

// MODALS
const modal = new bootstrap.Modal(document.getElementById('memberModal'));
const deleteModal = new bootstrap.Modal(document.getElementById('deleteModal'));

let editId = null;
let deleteId = null;
let allMembers = [];

// OPEN
window.openModal = () => {
    editId = null;
    document.getElementById('name').value = '';
    document.getElementById('mid').value = '';
    modal.show();
};

// EDIT
window.editMember = (id, name, mid) => {
    editId = id;
    document.getElementById('name').value = name;
    document.getElementById('mid').value = mid;
    modal.show();
};

// SAVE
window.saveMember = async () => {
    const name = document.getElementById('name').value;
    const mid = document.getElementById('mid').value;

    if(!name || !mid) return alert("Fill all fields");

    if(editId) {
        await updateDoc(doc(db, "members", editId), { name, memberId: mid });
    } else {
        await addDoc(collection(db, "members"), { name, memberId: mid });
    }

    modal.hide();
};

// DELETE
window.deleteMember = (id) => {
    deleteId = id;
    deleteModal.show();
};

window.confirmDelete = async () => {
    await deleteDoc(doc(db, "members", deleteId));
    deleteModal.hide();
};

// LOAD
onSnapshot(collection(db, "members"), (snap) => {
    allMembers = [];
    snap.forEach(d => {
        allMembers.push({ id: d.id, ...d.data() });
    });

    renderMembers(allMembers);
});

// RENDER
function renderMembers(data) {
    let html = '';

    data.forEach(m => {
        html += `
        <div class="col-md-4">
            <div class="member-card d-flex justify-content-between">
                <div>
                    <h6>${m.name}</h6>
                    <small>${m.memberId}</small>
                </div>

                <div>
                    <button class="btn btn-sm btn-warning" onclick="editMember('${m.id}','${m.name}','${m.memberId}')">
                        <i class="fas fa-edit"></i>
                    </button>
                    <button class="btn btn-sm btn-danger" onclick="deleteMember('${m.id}')">
                        <i class="fas fa-trash"></i>
                    </button>
                </div>
            </div>
        </div>`;
    });

    document.getElementById('member-grid').innerHTML = html;
    document.getElementById('member-count').innerText = data.length;
}

// SEARCH
document.getElementById('searchInput').addEventListener('input', (e) => {
    const val = e.target.value.toLowerCase();

    const filtered = allMembers.filter(m =>
        m.name.toLowerCase().includes(val) ||
        m.memberId.toLowerCase().includes(val)
    );

    renderMembers(filtered);
});

</script>

</body>
</html>
