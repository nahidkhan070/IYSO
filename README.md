
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
            min-height: 100vh;
            margin: 0;
        }

        body::before {
            content: "";
            position: fixed;
            top: 50%; left: 50%;
            transform: translate(-50%, -50%);
            width: 80vw; height: 80vw;
            max-width: 600px;
            background: url('image_0.png') no-repeat center;
            background-size: contain;
            opacity: 0.04;
            z-index: -1;
            pointer-events: none;
        }

        /* --- RESPONSIVE SIDEBAR --- */
        #sidebar {
            width: 260px; height: 100vh; position: fixed;
            background: rgba(0, 0, 0, 0.6); backdrop-filter: blur(25px);
            border-right: 1px solid rgba(198, 163, 79, 0.15);
            padding: 40px 20px; z-index: 1000;
            transition: transform 0.3s ease;
        }

        .main-content { margin-left: 260px; padding: 30px; transition: 0.3s; }

        @media (max-width: 992px) {
            #sidebar { transform: translateX(-100%); width: 240px; }
            #sidebar.active { transform: translateX(0); }
            .main-content { margin-left: 0; padding: 20px; padding-top: 80px; }
            .mobile-toggle { display: block !important; }
        }

        .mobile-toggle {
            display: none; position: fixed; top: 20px; left: 20px;
            z-index: 1100; background: var(--iyso-green);
            color: white; border: none; border-radius: 8px; padding: 10px 15px;
        }

        /* --- ANIMATED ELEMENTS --- */
        .nav-link {
            color: #8a949d; padding: 12px 15px; border-radius: 12px;
            margin-bottom: 8px; transition: 0.3s; cursor: pointer;
            text-decoration: none; display: flex; align-items: center;
        }

        .nav-link:hover, .nav-link.active {
            background: var(--iyso-green); color: #fff;
            transform: translateX(5px);
        }

        .glass-card {
            background: var(--card-bg);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 20px; padding: 25px;
            backdrop-filter: blur(15px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.4);
            transition: 0.3s;
        }

        .glass-card:hover { transform: translateY(-5px); border-color: var(--iyso-gold); }

        .btn-action {
            background: rgba(255,255,255,0.05); border: none;
            color: #8a949d; border-radius: 8px; width: 35px; height: 35px;
            transition: 0.3s;
        }

        .btn-action:hover { background: var(--iyso-gold); color: #000; }

        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.5s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
    </style>
</head>
<body>

<button class="mobile-toggle" onclick="toggleSidebar()"><i class="fas fa-bars"></i></button>

<div id="sidebar">
    <div class="text-center mb-5">
        <img src="image_0.png" alt="Logo" height="70">
        <h5 class="mt-3 fw-bold text-white">IYSO PORTAL</h5>
    </div>
    <div class="nav flex-column">
        <div class="nav-link active" data-section="overview"><i class="fas fa-chart-pie me-3"></i> Dashboard</div>
        <div class="nav-link" data-section="members"><i class="fas fa-user-friends me-3"></i> Members</div>
        <div class="nav-link" data-section="events"><i class="fas fa-calendar-alt me-3"></i> Events</div>
    </div>
</div>

<div class="main-content">
    <div id="overview" class="page-section active">
        <h2 class="mb-4">Dashboard</h2>
        <div class="row g-3">
            <div class="col-md-6"><div class="glass-card"><h6>Monthly Collections</h6><h2 id="monthly-stat">৳0</h2></div></div>
            <div class="col-md-6"><div class="glass-card"><h6>Total Yearly</h6><h2 id="yearly-stat">৳0</h2></div></div>
        </div>
        <div class="glass-card mt-4 p-0 overflow-hidden">
            <div class="table-responsive">
                <table class="table table-dark m-0">
                    <thead><tr><th>Date</th><th>Name</th><th>Amount</th></tr></thead>
                    <tbody id="report-table"></tbody>
                </table>
            </div>
        </div>
    </div>

    <div id="members" class="page-section">
        <div class="d-flex justify-content-between mb-4">
            <h3>Directory</h3>
            <button class="btn btn-success" onclick="manageMember()">+ Add New</button>
        </div>
        <div id="member-grid" class="row g-3"></div>
    </div>
</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, updateDoc, deleteDoc, doc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

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

    // Responsive Toggle
    window.toggleSidebar = () => document.getElementById('sidebar').classList.toggle('active');

    // Navigation Logic
    document.querySelectorAll('.nav-link').forEach(link => {
        link.onclick = () => {
            document.querySelectorAll('.page-section, .nav-link').forEach(el => el.classList.remove('active'));
            document.getElementById(link.dataset.section).classList.add('active');
            link.classList.add('active');
            if(window.innerWidth < 992) toggleSidebar();
        };
    });

    // --- MEMBER CRUD ---
    window.manageMember = async (id = null, currentData = {}) => {
        const name = prompt("Name:", currentData.name || "");
        const mid = prompt("Member ID:", currentData.memberId || "");
        if(!name || !mid) return;

        if(id) {
            await updateDoc(doc(db, "members", id), { name, memberId: mid });
        } else {
            await addDoc(collection(db, "members"), { name, memberId: mid, date: new Date() });
        }
    };

    window.removeMember = async (id) => {
        if(confirm("Permanently delete this member?")) await deleteDoc(doc(db, "members", id));
    };

    onSnapshot(collection(db, "members"), (snap) => {
        let html = '';
        snap.forEach(d => {
            const m = d.data();
            html += `
            <div class="col-sm-6 col-xl-4">
                <div class="glass-card">
                    <div class="d-flex justify-content-between align-items-start">
                        <div><h6 class="mb-0 text-white">${m.name}</h6><small>${m.memberId}</small></div>
                        <div class="d-flex gap-2">
                            <button class="btn-action" onclick="manageMember('${d.id}', {name:'${m.name}', memberId:'${m.memberId}'})"><i class="fas fa-edit"></i></button>
                            <button class="btn-action" onclick="removeMember('${d.id}')"><i class="fas fa-trash"></i></button>
                        </div>
                    </div>
                </div>
            </div>`;
        });
        document.getElementById('member-grid').innerHTML = html;
    });

    // --- FINANCE STATS ---
    onSnapshot(collection(db, "donations"), (snap) => {
        let mTotal = 0; let yTotal = 0; let rows = '';
        const now = new Date();
        snap.forEach(d => {
            const data = d.data();
            yTotal += data.amount;
            if(data.month === now.getMonth()) mTotal += data.amount;
            rows += `<tr><td>${data.date.toDate().toLocaleDateString()}</td><td>${data.name}</td><td>৳${data.amount}</td></tr>`;
        });
        document.getElementById('report-table').innerHTML = rows;
        document.getElementById('monthly-stat').innerText = `৳${mTotal}`;
        document.getElementById('yearly-stat').innerText = `৳${yTotal}`;
    });
</script>
</body>
</html>
