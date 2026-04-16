
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IYSO | Management Portal</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=Hind+Siliguri:wght@400;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --iyso-green: #006837;
            --iyso-gold: #c6a34f;
            --dark-bg: #04070a;
            --card-bg: rgba(17, 24, 32, 0.95);
        }

        body {
            background: radial-gradient(circle at top right, #003d21, var(--dark-bg) 70%);
            color: #e9ecef;
            font-family: 'Plus Jakarta Sans', 'Hind Siliguri', sans-serif;
            min-height: 100vh;
            margin: 0;
        }

        body::before {
            content: ""; position: fixed; top: 50%; left: 50%;
            transform: translate(-50%, -50%); width: 70vw; height: 70vw;
            background: url('0-02-03-d309263e56130046c80157bf1f139cae99883115fd22a5526673d00fb3c476e4_52a78bf800e32839.jpg') no-repeat center;
            background-size: contain; opacity: 0.03; z-index: -1; pointer-events: none;
        }

        #sidebar {
            width: 260px; height: 100vh; position: fixed;
            background: rgba(0, 0, 0, 0.6); backdrop-filter: blur(20px);
            border-right: 1px solid rgba(198, 163, 79, 0.1); padding: 30px 20px;
            z-index: 1000;
        }

        .main-content { margin-left: 260px; padding: 40px; transition: 0.3s; }

        .glass-card {
            background: var(--card-bg); border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 20px; padding: 25px; transition: 0.3s; height: 100%;
        }

        .nav-link { color: #8a949d; cursor: pointer; padding: 12px; border-radius: 10px; transition: 0.3s; display: block; text-decoration: none; margin-bottom: 5px; }
        .nav-link:hover, .nav-link.active { background: var(--iyso-green); color: #fff; }

        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.4s; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .balance-card { background: linear-gradient(135deg, var(--iyso-green), #002d18); border: 1px solid var(--iyso-gold); }
        
        @media (max-width: 992px) {
            #sidebar { width: 0; padding: 0; visibility: hidden; }
            .main-content { margin-left: 0; padding: 20px; }
        }
    </style>
</head>
<body>

<div id="sidebar">
    <div class="text-center mb-4">
        <img src="0-02-03-d309263e56130046c80157bf1f139cae99883115fd22a5526673d00fb3c476e4_52a78bf800e32839.jpg" height="70">
        <h6 class="mt-2 fw-bold text-white">IYSO PORTAL</h6>
    </div>
    <div class="nav flex-column">
        <div class="nav-link active" onclick="showSection('overview')"><i class="fas fa-chart-line me-2"></i> Dashboard</div>
        <div class="nav-link" onclick="showSection('members')"><i class="fas fa-users-cog me-2"></i> Members</div>
        <div class="nav-link" onclick="showSection('costs')"><i class="fas fa-wallet me-2"></i> Costing</div>
        <div class="nav-link" onclick="showSection('summary')"><i class="fas fa-file-invoice me-2"></i> Summary Report</div>
        <div class="nav-link" onclick="showSection('settings')"><i class="fas fa-tools me-2"></i> Settings</div>
    </div>
</div>

<div class="main-content">
    
    <div id="overview" class="page-section active">
        <h2 class="fw-bold mb-4">Dashboard</h2>
        <div class="row g-4 mb-4">
            <div class="col-md-6">
                <div class="glass-card balance-card">
                    <h5 class="text-gold">Net Balance Fund / নিট তহবিল</h5>
                    <h1 id="net-balance" style="font-weight: 800;">৳0</h1>
                </div>
            </div>
            <div class="col-md-6">
                <div class="glass-card">
                    <h5>Official Channels</h5>
                    <div class="d-flex justify-content-around mt-3">
                        <div class="text-center"><small class="d-block text-muted">bKash</small><b id="disp-bkash">-</b></div>
                        <div class="text-center"><small class="d-block text-muted">Nagad</small><b id="disp-nagad">-</b></div>
                    </div>
                </div>
            </div>
        </div>

        <h4 class="mb-3">Monthly Donation Ledger</h4>
        <div class="glass-card p-0 overflow-hidden">
            <div class="table-responsive">
                <table class="table table-dark m-0">
                    <thead><tr><th>Date</th><th>Donor</th><th>ID</th><th>Method</th><th>Amount</th></tr></thead>
                    <tbody id="dash-donation-table"></tbody>
                </table>
            </div>
        </div>
    </div>

    <div id="members" class="page-section">
        <div class="d-flex justify-content-between mb-4">
            <h3>Member Management</h3>
            <button class="btn btn-success" onclick="openMemberModal()">+ Add Member</button>
        </div>
        <div id="member-grid" class="row g-3"></div>
    </div>

    <div id="costs" class="page-section">
        <div class="d-flex justify-content-between mb-4">
            <h3>Expenditure / ব্যয় সমূহ</h3>
            <button class="btn btn-danger" onclick="addCost()">+ Add Costing</button>
        </div>
        <div class="glass-card p-0 overflow-hidden">
            <table class="table table-dark m-0">
                <thead><tr><th>Date</th><th>Description</th><th>Amount</th></tr></thead>
                <tbody id="cost-table"></tbody>
            </table>
        </div>
    </div>

    <div id="summary" class="page-section">
        <h3 class="mb-4">Financial Summary Report</h3>
        <div class="row g-4">
            <div class="col-md-4"><div class="glass-card"><h6>Monthly Donation Total</h6><h4 id="sum-m-don">৳0</h4></div></div>
            <div class="col-md-4"><div class="glass-card"><h6>Monthly Costing Total</h6><h4 id="sum-m-cost">৳0</h4></div></div>
            <div class="col-md-4"><div class="glass-card text-success"><h6>Monthly Savings</h6><h4 id="sum-m-save">৳0</h4></div></div>
            <div class="col-md-6"><div class="glass-card"><h6>Yearly Donation Collection</h6><h4 id="sum-y-don">৳0</h4></div></div>
            <div class="col-md-6"><div class="glass-card"><h6>Yearly Total Expenditure</h6><h4 id="sum-y-cost">৳0</h4></div></div>
        </div>
    </div>

</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, doc, updateDoc, deleteDoc, getDoc, setDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "AIzaSyCDs8tMQt14l4TNlTXPloQZk0LmL_Z4oNY",
        authDomain: "iyso-web.firebaseapp.com",
        projectId: "iyso-web",
        storageBucket: "iyso-web.firebasestorage.app",
        messagingSenderId: "898053892858",
        appId: "1:898053892858:web:e81b46946d2f9e84b73743"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    window.showSection = (id) => {
        document.querySelectorAll('.page-section').forEach(s => s.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
        event.currentTarget.classList.add('active');
    };

    // --- MEMBER CRUD ---
    window.openMemberModal = async (memberId = null, current = {}) => {
        const name = prompt("Name:", current.name || "");
        const mid = prompt("Unique Member ID:", current.memberId || "");
        const desig = prompt("Designation:", current.desig || "");
        const phone = prompt("Phone:", current.phone || "");
        const blood = prompt("Blood Group:", current.blood || "");
        
        if(name && mid) {
            const data = { name, memberId: mid, desig, phone, blood, updated: new Date() };
            if(memberId) await updateDoc(doc(db, "members", memberId), data);
            else await addDoc(collection(db, "members"), data);
        }
    };

    window.deleteMember = async (id) => { if(confirm("Delete Member?")) await deleteDoc(doc(db, "members", id)); };

    onSnapshot(collection(db, "members"), (snap) => {
        let html = '';
        snap.forEach(d => {
            const m = d.data();
            html += `<div class="col-md-4"><div class="glass-card">
                <div class="d-flex justify-content-between">
                    <span class="badge bg-success">${m.desig}</span>
                    <div class="dropdown">
                        <button class="btn btn-sm text-white" onclick="openMemberModal('${d.id}', ${JSON.stringify(m).replace(/"/g, '&quot;')})"><i class="fas fa-edit"></i></button>
                        <button class="btn btn-sm text-danger" onclick="deleteMember('${d.id}')"><i class="fas fa-trash"></i></button>
                    </div>
                </div>
                <h5 class="mt-2 mb-1">${m.name}</h5>
                <small class="text-muted">ID: ${m.memberId}</small><br>
                <small class="text-muted"><i class="fas fa-phone-alt me-1"></i> ${m.phone} | <i class="fas fa-tint me-1 text-danger"></i> ${m.blood}</small>
            </div></div>`;
        });
        document.getElementById('member-grid').innerHTML = html;
    });

    // --- COSTING LOGIC ---
    window.addCost = async () => {
        const desc = prompt("Cost Description:");
        const amt = prompt("Amount (৳):");
        if(desc && amt) {
            await addDoc(collection(db, "costs"), { 
                desc, amount: parseFloat(amt), date: new Date(), 
                month: new Date().getMonth(), year: new Date().getFullYear() 
            });
        }
    };

    // --- GLOBAL STATE & SUMMARIES ---
    let totalDonations = 0;
    let totalCosts = 0;

    onSnapshot(collection(db, "donations"), (snap) => {
        let mDon = 0; let yDon = 0; let dHtml = '';
        const now = new Date();
        snap.forEach(d => {
            const data = d.data();
            yDon += data.amount;
            if(data.month === now.getMonth()) mDon += data.amount;
            dHtml += `<tr><td>${data.date.toDate().toLocaleDateString()}</td><td>${data.name}</td><td>${data.memberId || 'N/A'}</td><td>${data.method}</td><td>৳${data.amount}</td></tr>`;
        });
        totalDonations = yDon;
        document.getElementById('sum-m-don').innerText = `৳${mDon}`;
        document.getElementById('sum-y-don').innerText = `৳${yDon}`;
        document.getElementById('dash-donation-table').innerHTML = dHtml;
        updateBalance();
    });

    onSnapshot(collection(db, "costs"), (snap) => {
        let mCost = 0; let yCost = 0; let cHtml = '';
        const now = new Date();
        snap.forEach(d => {
            const data = d.data();
            yCost += data.amount;
            if(data.month === now.getMonth()) mCost += data.amount;
            cHtml += `<tr><td>${data.date.toDate().toLocaleDateString()}</td><td>${data.desc}</td><td>৳${data.amount}</td></tr>`;
        });
        totalCosts = yCost;
        document.getElementById('sum-m-cost').innerText = `৳${mCost}`;
        document.getElementById('sum-y-cost').innerText = `৳${yCost}`;
        document.getElementById('cost-table').innerHTML = cHtml;
        updateBalance();
    });

    function updateBalance() {
        const bal = totalDonations - totalCosts;
        document.getElementById('net-balance').innerText = `৳${bal}`;
        const mDon = parseFloat(document.getElementById('sum-m-don').innerText.replace('৳', ''));
        const mCost = parseFloat(document.getElementById('sum-m-cost').innerText.replace('৳', ''));
        document.getElementById('sum-m-save').innerText = `৳${mDon - mCost}`;
    }
</script>
</body>
</html>
