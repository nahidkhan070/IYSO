
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IYSO | Executive Management Portal</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --iyso-green: #006837;
            --iyso-gold: #c6a34f;
            --dark-bg: #04070a;
            --card-bg: rgba(17, 24, 32, 0.8);
            --emerald-gradient: linear-gradient(135deg, #006837 0%, #002d18 100%);
            --gold-gradient: linear-gradient(135deg, #c6a34f 0%, #947a3a 100%);
        }

        body {
            background: radial-gradient(circle at top right, #003d21, var(--dark-bg) 60%);
            color: #e9ecef;
            font-family: 'Plus Jakarta Sans', sans-serif;
            min-height: 100vh;
        }

        /* Premium Sidebar */
        #sidebar {
            width: 260px; height: 100vh; position: fixed;
            background: rgba(0, 0, 0, 0.4); backdrop-filter: blur(20px);
            border-right: 1px solid rgba(198, 163, 79, 0.2);
            padding: 30px 20px;
        }

        .main-content { margin-left: 260px; padding: 40px; }

        .glass-card {
            background: var(--card-bg);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 24px;
            padding: 25px;
            backdrop-filter: blur(10px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.5);
            margin-bottom: 25px;
        }

        .nav-link {
            color: #8a949d; padding: 12px 15px; border-radius: 12px;
            margin-bottom: 8px; transition: 0.3s; cursor: pointer;
        }

        .nav-link:hover, .nav-link.active { background: var(--iyso-green); color: #fff; }

        .btn-gold {
            background: var(--gold-gradient); color: #000; font-weight: 700;
            border: none; border-radius: 12px; padding: 12px 25px;
        }

        .member-avatar {
            width: 60px; height: 60px; border-radius: 50%;
            border: 2px solid var(--iyso-gold); object-fit: cover;
        }

        .status-badge { font-size: 0.7rem; padding: 4px 12px; border-radius: 50px; background: rgba(0, 255, 136, 0.1); color: #00ff88; border: 1px solid #00ff88; }
        
        .page-section { display: none; animation: fadeIn 0.4s ease; }
        .page-section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

<div id="sidebar">
    <div class="text-center mb-5">
        <img src="image_0.png" alt="Logo" height="70">
        <h5 class="mt-3 fw-bold text-white">IYSO PORTAL</h5>
    </div>
    <div class="nav flex-column">
        <div class="nav-link active" onclick="showSection('overview')"><i class="fas fa-home me-2"></i> Dashboard</div>
        <div class="nav-link" onclick="showSection('members')"><i class="fas fa-users me-2"></i> Members</div>
        <div class="nav-link" onclick="showSection('finance')"><i class="fas fa-file-invoice-dollar me-2"></i> Donations</div>
        <div class="nav-link" onclick="showSection('events')"><i class="fas fa-calendar-star me-2"></i> Events</div>
    </div>
</div>

<div class="main-content">
    
    <div id="overview" class="page-section active">
        <h2 class="mb-4 fw-bold">Executive Overview</h2>
        <div class="row g-4 mb-5">
            <div class="col-md-4">
                <div class="glass-card" style="border-left: 5px solid var(--iyso-gold);">
                    <h6 class="text-muted">Yearly Collections</h6>
                    <h2 id="yearly-stat">৳0</h2>
                </div>
            </div>
            <div class="col-md-4">
                <div class="glass-card" style="border-left: 5px solid var(--iyso-green);">
                    <h6 class="text-muted">Monthly Revenue</h6>
                    <h2 id="monthly-stat">৳0</h2>
                </div>
            </div>
        </div>

        <h4 class="mb-3">Monthly Donation Report</h4>
        <div class="glass-card p-0 overflow-hidden">
            <table class="table table-dark table-hover m-0">
                <thead class="bg-dark">
                    <tr><th>Date</th><th>Member Name</th><th>ID</th><th>Amount</th></tr>
                </thead>
                <tbody id="report-table"></tbody>
            </table>
        </div>
    </div>

    <div id="members" class="page-section">
        <div class="d-flex justify-content-between mb-4">
            <h2>Member Directory</h2>
            <button class="btn btn-gold" onclick="addMember()">+ Register Member</button>
        </div>
        <div id="member-grid" class="row g-4"></div>
    </div>

    <div id="events" class="page-section">
        <div class="d-flex justify-content-between mb-4">
            <h2>Event Management</h2>
            <button class="btn btn-gold" onclick="addEvent()">+ New Event</button>
        </div>
        <div id="event-grid" class="row g-4"></div>
    </div>

</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, query, orderBy } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

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

    // Navigation
    window.showSection = (id) => {
        document.querySelectorAll('.page-section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        event.currentTarget.classList.add('active');
    };

    // --- MEMBER LOGIC ---
    window.addMember = async () => {
        const name = prompt("Name:");
        const id = prompt("Unique ID (e.g. IYSO-001):");
        const desig = prompt("Designation:");
        const phone = prompt("Phone (Optional):");
        const blood = prompt("Blood Group (Optional):");
        if(name && id) {
            await addDoc(collection(db, "members"), { name, memberId: id, desig, phone, blood });
        }
    };

    onSnapshot(collection(db, "members"), (snap) => {
        let html = '';
        snap.forEach(doc => {
            const m = doc.data();
            html += `
            <div class="col-md-6">
                <div class="glass-card d-flex align-items-center">
                    <div class="me-3 text-center">
                        <div class="member-avatar d-flex align-items-center justify-content-center bg-success">
                            <i class="fas fa-user text-white"></i>
                        </div>
                    </div>
                    <div>
                        <span class="status-badge">${m.desig || 'Member'}</span>
                        <h5 class="mb-1 mt-1 text-white">${m.name} <small class="text-muted">(${m.memberId})</small></h5>
                        <p class="mb-0 small text-muted">
                            <i class="fas fa-phone-alt me-1"></i> ${m.phone || 'N/A'} | 
                            <i class="fas fa-droplet me-1 text-danger"></i> ${m.blood || 'N/A'}
                        </p>
                    </div>
                </div>
            </div>`;
        });
        document.getElementById('member-grid').innerHTML = html;
    });

    // --- EVENT LOGIC ---
    window.addEvent = async () => {
        const title = prompt("Event Title:");
        const budget = prompt("Budget (৳):");
        const cost = prompt("Actual Cost (৳):");
        const collectionAmt = prompt("Total Fund Collected (৳):");
        if(title) {
            await addDoc(collection(db, "events"), { title, budget, cost, collectionAmt, date: new Date() });
        }
    };

    onSnapshot(collection(db, "events"), (snap) => {
        let html = '';
        snap.forEach(doc => {
            const e = doc.data();
            html += `
            <div class="col-md-6">
                <div class="glass-card">
                    <h5 class="fw-bold text-success"><i class="fas fa-star me-2"></i>${e.title}</h5>
                    <div class="row mt-3 text-center">
                        <div class="col-4 border-end"><h6>Budget</h6><p class="mb-0 text-white">৳${e.budget}</p></div>
                        <div class="col-4 border-end"><h6>Cost</h6><p class="mb-0 text-danger">৳${e.cost}</p></div>
                        <div class="col-4"><h6>Fund</h6><p class="mb-0 text-success">৳${e.collectionAmt}</p></div>
                    </div>
                </div>
            </div>`;
        });
        document.getElementById('event-grid').innerHTML = html;
    });

    // --- DONATION REPORT LOGIC ---
    onSnapshot(collection(db, "donations"), (snap) => {
        let html = ''; let monthTotal = 0; let yearTotal = 0;
        const now = new Date();
        snap.forEach(doc => {
            const d = doc.data();
            yearTotal += d.amount;
            if(d.month === now.getMonth()) monthTotal += d.amount;
            html += `<tr><td>${d.date.toDate().toLocaleDateString()}</td><td>${d.name}</td><td>${d.memberId}</td><td class="text-success">৳${d.amount}</td></tr>`;
        });
        document.getElementById('report-table').innerHTML = html;
        document.getElementById('monthly-stat').innerText = `৳${monthTotal}`;
        document.getElementById('yearly-stat').innerText = `৳${yearTotal}`;
    });
</script>
</body>
</html>
