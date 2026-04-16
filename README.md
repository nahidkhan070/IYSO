
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IYSO | Official Management Portal</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --iyso-green: #006837;
            --iyso-gold: #c6a34f;
            --dark-bg: #06090c;
            --card-bg: #111820;
            --glass-border: rgba(198, 163, 79, 0.2);
        }

        body {
            background-color: var(--dark-bg);
            color: #e9ecef;
            font-family: 'Plus Jakarta Sans', sans-serif;
        }

        /* Premium Sidebar */
        #sidebar {
            width: 280px;
            height: 100vh;
            background: var(--card-bg);
            border-right: 1px solid var(--glass-border);
            position: fixed;
            padding: 30px 20px;
        }

        .main-content { margin-left: 280px; padding: 40px; }

        .nav-link {
            color: #8a949d;
            padding: 12px 15px;
            border-radius: 12px;
            margin-bottom: 8px;
            transition: 0.3s;
            cursor: pointer;
        }

        .nav-link:hover, .nav-link.active {
            background: var(--iyso-green);
            color: #fff;
        }

        /* Glassmorphism Cards */
        .premium-card {
            background: var(--card-bg);
            border: 1px solid var(--glass-border);
            border-radius: 24px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .btn-gold {
            background: var(--iyso-gold);
            color: #000;
            font-weight: 700;
            border-radius: 12px;
            border: none;
            padding: 10px 25px;
        }

        .status-badge {
            font-size: 0.7rem;
            padding: 4px 12px;
            border-radius: 50px;
            background: rgba(198, 163, 79, 0.1);
            color: var(--iyso-gold);
            border: 1px solid var(--iyso-gold);
        }

        /* Hide sections by default */
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.5s ease; }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

<div id="sidebar">
    <div class="text-center mb-5">
        <img src="image_0.png" alt="IYSO Logo" height="80">
        <h5 class="mt-3 fw-bold text-white">IYSO PORTAL</h5>
        <small class="text-muted">Super Admin Panel</small>
    </div>

    <div class="nav flex-column">
        <div class="nav-link active" onclick="showSection('overview')"><i class="fas fa-chart-line me-3"></i> Overview</div>
        <div class="nav-link" onclick="showSection('directory')"><i class="fas fa-users me-3"></i> Member Directory</div>
        <div class="nav-link" onclick="showSection('finance')"><i class="fas fa-wallet me-3"></i> Finance Section</div>
        <div class="nav-link" onclick="showSection('schedules')"><i class="fas fa-calendar-alt me-3"></i> Event Schedules</div>
    </div>
</div>

<div class="main-content">
    
    <div id="overview" class="page-section active">
        <div class="d-flex justify-content-between align-items-center mb-5">
            <h1>Organization Dashboard</h1>
            <div class="d-flex align-items-center">
                <div class="me-3 text-end"><div class="fw-bold">Nahid Khan</div><small class="text-muted">Super Admin</small></div>
                <img src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=100" class="rounded-circle border border-warning" height="45" width="45">
            </div>
        </div>

        <div class="row g-4 mb-4">
            <div class="col-md-4">
                <div class="premium-card">
                    <h6 class="text-muted">Total Members</h6>
                    <h2 id="total-members-count">0</h2>
                </div>
            </div>
            <div class="col-md-4">
                <div class="premium-card">
                    <h6 class="text-muted">Available Funds</h6>
                    <h2 id="current-fund-display" class="text-success">$0.00</h2>
                </div>
            </div>
            <div class="col-md-4">
                <div class="premium-card">
                    <h6 class="text-muted">Upcoming Events</h6>
                    <h2>03</h2>
                </div>
            </div>
        </div>
    </div>

    <div id="directory" class="page-section">
        <div class="d-flex justify-content-between mb-4">
            <h2>Member Directory</h2>
            <button class="btn btn-gold" onclick="addMember()"><i class="fas fa-plus me-2"></i>New Member</button>
        </div>
        <div id="member-list" class="row g-4"></div>
    </div>

    <div id="finance" class="page-section">
        <div class="d-flex justify-content-between mb-4">
            <h2>Finance Section</h2>
            <button class="btn btn-gold" onclick="addFinance()"><i class="fas fa-plus me-2"></i>Record Transaction</button>
        </div>
        <div class="premium-card p-0">
            <table class="table table-dark table-hover m-0">
                <thead><tr><th>Description</th><th>Category</th><th>Amount</th></tr></thead>
                <tbody id="finance-table-body"></tbody>
            </table>
        </div>
    </div>

    <div id="schedules" class="page-section">
        <h2>Event Schedules</h2>
        <div class="premium-card mt-4">
            <p class="text-muted">Your 30-day organizational schedule will appear here.</p>
            </div>
    </div>

</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "AIzaSyCDs8tMQt14l4TNlTXPloQZk0LmL_Z4oNY",
        authDomain: "iyso-web.firebaseapp.com",
        projectId: "iyso-web",
        storageBucket: "iyso-web.firebasestorage.app",
        messagingSenderId: "898053892858",
        appId: "1:898053892858:web:e81b46946d2f9e84b73743",
        measurementId: "G-C699C3CKG8"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    // Sidebar Navigation Logic
    window.showSection = (sectionId) => {
        document.querySelectorAll('.page-section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
        document.getElementById(sectionId).classList.add('active');
        event.currentTarget.classList.add('active');
    };

    // Firebase Functions: Members
    window.addMember = async () => {
        const name = prompt("Member Name:");
        const role = prompt("Designation:");
        if (name && role) await addDoc(collection(db, "members"), { name, role });
    };

    onSnapshot(collection(db, "members"), (snap) => {
        let html = '';
        document.getElementById('total-members-count').innerText = snap.size;
        snap.forEach(doc => {
            const m = doc.data();
            html += `
            <div class="col-md-6">
                <div class="premium-card d-flex align-items-center p-3">
                    <div class="me-3" style="width:50px; height:50px; background:var(--iyso-green); border-radius:12px; display:flex; align-items:center; justify-content:center;">
                        <i class="fas fa-user text-white"></i>
                    </div>
                    <div><span class="status-badge">${m.role}</span><h5 class="mb-0 mt-1 text-white">${m.name}</h5></div>
                </div>
            </div>`;
        });
        document.getElementById('member-list').innerHTML = html;
    });

    // Firebase Functions: Finance
    window.addFinance = async () => {
        const desc = prompt("Transaction Description:");
        const amt = prompt("Amount (e.g. 500 or -200):");
        if (desc && amt) await addDoc(collection(db, "finance"), { desc, amount: parseFloat(amt) });
    };

    onSnapshot(collection(db, "finance"), (snap) => {
        let html = ''; let total = 0;
        snap.forEach(doc => {
            const f = doc.data();
            total += f.amount;
            html += `<tr><td>${f.desc}</td><td>General</td><td class="${f.amount >= 0 ? 'text-success' : 'text-danger'}">${f.amount}</td></tr>`;
        });
        document.getElementById('finance-table-body').innerHTML = html;
        document.getElementById('current-fund-display').innerText = `$${total.toFixed(2)}`;
    });
</script>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
