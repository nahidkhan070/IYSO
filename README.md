
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IYSO | Executive Portal</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --iyso-green: #006837;
            --iyso-gold: #c6a34f;
            --dark-bg: #04070a;
            --card-bg: rgba(17, 24, 32, 0.85);
            --emerald-gradient: linear-gradient(135deg, #006837 0%, #002d18 100%);
        }

        body {
            background: radial-gradient(circle at top right, #003d21, var(--dark-bg) 70%);
            color: #e9ecef;
            font-family: 'Plus Jakarta Sans', sans-serif;
            min-height: 100vh;
            margin: 0;
            overflow-x: hidden;
        }

        /* Background Watermark */
        body::before {
            content: "";
            position: fixed;
            top: 50%;
            left: 60%; /* Centered relative to the main content */
            transform: translate(-50%, -50%);
            width: 600px;
            height: 600px;
            background: url('image_0.png') no-repeat center;
            background-size: contain;
            opacity: 0.04; /* Very subtle watermark */
            z-index: -1;
            pointer-events: none;
        }

        /* Sidebar Navigation */
        #sidebar {
            width: 260px; height: 100vh; position: fixed;
            background: rgba(0, 0, 0, 0.6); backdrop-filter: blur(25px);
            border-right: 1px solid rgba(198, 163, 79, 0.15);
            padding: 40px 20px;
            z-index: 100;
        }

        .main-content { margin-left: 260px; padding: 50px; position: relative; }

        /* Animated Navigation Tabs */
        .nav-link {
            color: #8a949d; padding: 14px 18px; border-radius: 12px;
            margin-bottom: 10px; transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); 
            cursor: pointer; display: flex; align-items: center;
            border: 1px solid transparent;
        }

        .nav-link i { transition: transform 0.3s ease; }

        .nav-link:hover {
            background: rgba(255, 255, 255, 0.05);
            color: var(--iyso-gold);
            transform: translateX(8px); /* Shifts right on hover */
            border-color: rgba(198, 163, 79, 0.2);
        }

        .nav-link:hover i { transform: scale(1.2); color: var(--iyso-gold); }

        .nav-link.active { 
            background: var(--iyso-green); 
            color: #fff; 
            box-shadow: 0 10px 20px rgba(0, 104, 55, 0.4);
            transform: translateX(5px);
        }

        /* Premium Animated Cards */
        .glass-card {
            background: var(--card-bg);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 24px; padding: 30px;
            backdrop-filter: blur(15px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.4);
            margin-bottom: 30px;
            transition: all 0.3s ease;
        }

        .glass-card:hover {
            transform: translateY(-10px); /* Lifts up */
            border-color: rgba(198, 163, 79, 0.3);
            background: rgba(17, 24, 32, 0.95);
            box-shadow: 0 30px 60px rgba(0,0,0,0.6);
        }

        /* Button Pulse Animation */
        .btn-gold {
            background: linear-gradient(135deg, var(--iyso-gold), #947a3a);
            color: #000; font-weight: 800; border: none; border-radius: 12px;
            padding: 12px 25px; transition: 0.3s;
        }

        .btn-gold:hover {
            transform: scale(1.05);
            box-shadow: 0 0 20px rgba(198, 163, 79, 0.5);
        }

        .page-section { display: none; }
        .page-section.active { display: block; animation: slideIn 0.6s ease-out; }

        @keyframes slideIn { 
            from { opacity: 0; transform: translateY(30px); filter: blur(10px); } 
            to { opacity: 1; transform: translateY(0); filter: blur(0); } 
        }

        .status-pill { cursor: pointer; transition: 0.3s; }
        .status-pill:hover { filter: brightness(1.3); transform: scale(1.1); }
    </style>
</head>
<body>

<div id="sidebar">
    <div class="text-center mb-5">
        <img src="image_0.png" alt="IYSO Logo" height="85">
        <h5 class="mt-3 fw-bold text-white">IYSO PORTAL</h5>
    </div>
    <div class="nav flex-column">
        <div class="nav-link active" onclick="showSection('overview')"><i class="fas fa-th-large me-3"></i> Dashboard</div>
        <div class="nav-link" onclick="showSection('members')"><i class="fas fa-id-card me-3"></i> Members</div>
        <div class="nav-link" onclick="showSection('events')"><i class="fas fa-project-diagram me-3"></i> Events</div>
    </div>
</div>

<div class="main-content">
    <div id="overview" class="page-section active">
        <h2 class="mb-4 fw-bold">Executive Overview</h2>
        <div class="row g-4 mb-5">
            <div class="col-md-4"><div class="glass-card"><small class="text-muted">Total Collections</small><h2 id="yearly-stat">৳0</h2></div></div>
            <div class="col-md-4"><div class="glass-card"><small class="text-muted">Monthly Revenue</small><h2 id="monthly-stat" class="text-success">৳0</h2></div></div>
        </div>
        <h4 class="mb-4">Live Donation Ledger</h4>
        <div class="glass-card p-0 overflow-hidden">
            <table class="table table-dark table-hover m-0">
                <thead><tr><th>Date</th><th>Name</th><th>ID</th><th>Amount</th></tr></thead>
                <tbody id="report-table"></tbody>
            </table>
        </div>
    </div>

    <div id="events" class="page-section">
        <div class="d-flex justify-content-between align-items-center mb-5">
            <h2>Organization Events</h2>
            <button class="btn btn-gold" onclick="addEvent()">Create Event</button>
        </div>
        <div id="event-grid" class="row g-4"></div>
    </div>

    <div id="members" class="page-section">
        <div class="d-flex justify-content-between align-items-center mb-5">
            <h2>Member Directory</h2>
            <button class="btn btn-gold" onclick="addMember()">Register Member</button>
        </div>
        <div id="member-grid" class="row g-4"></div>
    </div>
</div>

<script type="module">
    // (Existing Firebase logic remains exactly the same as the previous step)
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, updateDoc, doc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

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
        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        event.currentTarget.classList.add('active');
    };

    // Firebase Listeners & Functions (Code from previous step here)
    onSnapshot(collection(db, "events"), (snap) => {
        let html = '';
        snap.forEach(d => {
            const e = d.data();
            const statusClass = `status-${e.status || 'planned'}`;
            html += `
            <div class="col-md-6">
                <div class="glass-card">
                    <div class="d-flex justify-content-between align-items-start mb-3">
                        <h5 class="fw-bold mb-0">${e.title}</h5>
                        <span class="status-pill status-${e.status || 'planned'}" onclick="toggleStatus('${d.id}', '${e.status || 'planned'}')">${(e.status || 'planned').toUpperCase()}</span>
                    </div>
                    <div class="row text-center mt-4">
                        <div class="col-4 border-end small">Budget<div class="text-white fw-bold">৳${e.budget}</div></div>
                        <div class="col-4 border-end small">Actual Cost<div class="text-danger fw-bold">৳${e.cost || 0}</div></div>
                        <div class="col-4 small">Collected<div class="text-success fw-bold">৳${e.fund || 0}</div></div>
                    </div>
                </div>
            </div>`;
        });
        document.getElementById('event-grid').innerHTML = html;
    });

    onSnapshot(collection(db, "members"), (snap) => {
        let html = '';
        snap.forEach(d => {
            const m = d.data();
            html += `
            <div class="col-md-6"><div class="glass-card d-flex align-items-center">
                <div class="me-3" style="width:50px; height:50px; background:var(--iyso-green); border-radius:50%; display:flex; align-items:center; justify-content:center;"><i class="fas fa-user"></i></div>
                <div><h6 class="mb-0 text-white">${m.name}</h6><small class="text-muted">${m.memberId} | ${m.phone || 'No Phone'}</small></div>
            </div></div>`;
        });
        document.getElementById('member-grid').innerHTML = html;
    });
</script>
</body>
</html>
