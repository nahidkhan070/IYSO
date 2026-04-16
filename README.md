
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IYSO | Executive Portal</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=Hind+Siliguri:wght@400;600&display=swap" rel="stylesheet">
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
            font-family: 'Plus Jakarta Sans', 'Hind Siliguri', sans-serif;
            min-height: 100vh;
        }

        /* Subtle Logo Watermark */
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
        }

        .main-content { margin-left: 260px; padding: 40px; }

        .glass-card {
            background: var(--card-bg); border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 20px; padding: 25px; transition: 0.3s;
        }

        .method-icon { width: 30px; height: 30px; object-fit: contain; margin-right: 10px; }
        
        .nav-link { color: #8a949d; cursor: pointer; padding: 12px; border-radius: 10px; transition: 0.3s; }
        .nav-link:hover, .nav-link.active { background: var(--iyso-green); color: #fff; }

        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        @media (max-width: 992px) {
            #sidebar { display: none; }
            .main-content { margin-left: 0; }
        }
    </style>
</head>
<body>

<div id="sidebar">
    <div class="text-center mb-4">
        <img src="0-02-03-d309263e56130046c80157bf1f139cae99883115fd22a5526673d00fb3c476e4_52a78bf800e32839.jpg" height="60">
        <h6 class="mt-2 fw-bold text-white">IYSO PORTAL</h6>
    </div>
    <div class="nav flex-column">
        <div class="nav-link active" onclick="showSection('overview')"><i class="fas fa-home me-2"></i> Dashboard</div>
        <div class="nav-link" onclick="showSection('members')"><i class="fas fa-users me-2"></i> Members</div>
        <div class="nav-link" onclick="showSection('events')"><i class="fas fa-calendar-star me-2"></i> Events</div>
        <div class="nav-link" onclick="showSection('settings')"><i class="fas fa-cog me-2"></i> Settings</div>
    </div>
</div>

<div class="main-content">
    
    <div id="overview" class="page-section active">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h2 class="fw-bold">Executive Overview / নির্বাহী সংক্ষিপ্ত বিবরণ</h2>
            <button class="btn btn-outline-warning btn-sm" onclick="addDonation()">+ Record Donation / অনুদান যোগ করুন</button>
        </div>
        
        <div class="row g-4 mb-5">
            <div class="col-md-4"><div class="glass-card"><h6>Monthly / মাসিক</h6><h2 id="m-stat">৳0</h2></div></div>
            <div class="col-md-4"><div class="glass-card"><h6>Yearly / বার্ষিক</h6><h2 id="y-stat">৳0</h2></div></div>
            <div class="col-md-4">
                <div class="glass-card py-2">
                    <div class="small text-muted">Payment Channels</div>
                    <div id="channel-stats" style="font-size: 0.8rem;"></div>
                </div>
            </div>
        </div>

        <div class="glass-card p-0 overflow-hidden">
            <table class="table table-dark m-0">
                <thead><tr><th>Date</th><th>Name</th><th>Method</th><th>Amount</th></tr></thead>
                <tbody id="donation-table"></tbody>
            </table>
        </div>
    </div>

    <div id="events" class="page-section">
        <div class="d-flex justify-content-between mb-4">
            <h2>Events / ইভেন্টসমূহ</h2>
            <button class="btn btn-success" onclick="addEvent()">+ Add Event / ইভেন্ট যোগ করুন</button>
        </div>
        <div id="event-grid" class="row g-3"></div>
    </div>

    <div id="settings" class="page-section">
        <h2 class="mb-4">Portal Settings</h2>
        <div class="glass-card col-md-6">
            <label class="form-label">bKash Number</label>
            <input type="text" id="bkash-num" class="form-control mb-3 bg-dark text-white border-secondary" placeholder="017xxxxxxxx">
            <label class="form-label">Nagad Number</label>
            <input type="text" id="nagad-num" class="form-control mb-3 bg-dark text-white border-secondary" placeholder="018xxxxxxxx">
            <button class="btn btn-gold w-100" onclick="saveSettings()">Update Numbers</button>
        </div>
    </div>

</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, query, orderBy, doc, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

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

    // Nav Logic
    window.showSection = (id) => {
        document.querySelectorAll('.page-section').forEach(s => s.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
        event.currentTarget.classList.add('active');
    };

    // --- DONATION LOGIC ---
    window.addDonation = async () => {
        const name = prompt("Donor Name:");
        const amt = prompt("Amount (৳):");
        const method = prompt("Method (bkash / nagad / cash):").toLowerCase();
        
        if(name && amt) {
            await addDoc(collection(db, "donations"), {
                name, 
                amount: parseFloat(amt), 
                method, 
                date: new Date(),
                month: new Date().getMonth(),
                year: new Date().getFullYear()
            });
        }
    };

    onSnapshot(collection(db, "donations"), (snap) => {
        let html = ''; let mTotal = 0; let yTotal = 0;
        let methods = { bkash: 0, nagad: 0, cash: 0 };
        const now = new Date();

        snap.forEach(doc => {
            const d = doc.data();
            yTotal += d.amount;
            if(d.month === now.getMonth()) {
                mTotal += d.amount;
                if(methods[d.method] !== undefined) methods[d.method] += d.amount;
            }
            html += `<tr>
                <td>${d.date.toDate().toLocaleDateString()}</td>
                <td>${d.name}</td>
                <td><span class="badge bg-secondary">${d.method.toUpperCase()}</span></td>
                <td class="text-success">৳${d.amount}</td>
            </tr>`;
        });

        document.getElementById('donation-table').innerHTML = html;
        document.getElementById('m-stat').innerText = `৳${mTotal}`;
        document.getElementById('y-stat').innerText = `৳${yTotal}`;
        document.getElementById('channel-stats').innerHTML = `
            bKash: ৳${methods.bkash} | Nagad: ৳${methods.nagad} | Cash: ৳${methods.cash}
        `;
    });

    // --- EVENT LOGIC ---
    window.addEvent = async () => {
        const title = prompt("Event Name / ইভেন্টের নাম:");
        const budget = prompt("Budget / বাজেট:");
        if(title) {
            await addDoc(collection(db, "events"), { title, budget, date: new Date() });
        }
    };

    onSnapshot(collection(db, "events"), (snap) => {
        let html = '';
        snap.forEach(d => {
            const e = d.data();
            html += `<div class="col-md-6"><div class="glass-card">
                <h5 class="text-success">${e.title}</h5>
                <p class="mb-0 small">Budget: ৳${e.budget}</p>
            </div></div>`;
        });
        document.getElementById('event-grid').innerHTML = html;
    });

    // --- SETTINGS LOGIC ---
    window.saveSettings = async () => {
        const bkash = document.getElementById('bkash-num').value;
        const nagad = document.getElementById('nagad-num').value;
        await setDoc(doc(db, "config", "numbers"), { bkash, nagad });
        alert("Numbers Updated!");
    };

    // Load Settings
    const loadSettings = async () => {
        const res = await getDoc(doc(db, "config", "numbers"));
        if(res.exists()) {
            document.getElementById('bkash-num').value = res.data().bkash;
            document.getElementById('nagad-num').value = res.data().nagad;
        }
    };
    loadSettings();

</script>
</body>
</html>
