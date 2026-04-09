
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
            --dark-bg: #0b0f13;
            --glass: rgba(255, 255, 255, 0.05);
        }

        body { background-color: var(--dark-bg); color: #fff; font-family: 'Plus Jakarta Sans', sans-serif; }

        /* Premium Glass Design */
        .glass-card {
            background: var(--glass);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 20px;
            backdrop-filter: blur(15px);
            padding: 25px;
            margin-bottom: 20px;
        }

        .navbar { background: rgba(11, 15, 19, 0.9); border-bottom: 1px solid rgba(255,255,255,0.1); }
        .btn-iyso { background: var(--iyso-green); color: white; border: 1px solid var(--iyso-gold); border-radius: 10px; padding: 10px 20px; transition: 0.3s; }
        .btn-iyso:hover { background: var(--iyso-gold); color: black; }

        .profile-img-circle {
            width: 60px; height: 60px;
            border-radius: 50%;
            border: 2px solid var(--iyso-gold);
            display: flex; align-items: center; justify-content: center;
            background: var(--iyso-green); font-size: 1.5rem;
        }

        .status-badge { font-size: 0.7rem; padding: 3px 10px; border-radius: 50px; background: rgba(0, 255, 136, 0.1); color: #00ff88; border: 1px solid #00ff88; }
    </style>
</head>
<body>

<nav class="navbar sticky-top">
    <div class="container">
        <a class="navbar-brand d-flex align-items-center text-white" href="#">
            <img src="image_0.png" alt="Logo" height="50">
            <span class="ms-3 fw-bold">IYSO PORTAL</span>
        </a>
        <div class="ms-auto">
            <button class="btn btn-iyso" onclick="addNewMember()"><i class="fas fa-plus me-2"></i>Add Member</button>
            <button class="btn btn-outline-light ms-2" onclick="addFinance()"><i class="fas fa-dollar-sign me-2"></i>Record Finance</button>
        </div>
    </div>
</nav>

<div class="container mt-5">
    <div class="row">
        <div class="col-md-4">
            <div class="glass-card text-center">
                <h6 class="text-muted">Total Members</h6>
                <h2 id="member-count">0</h2>
            </div>
        </div>
        <div class="col-md-4">
            <div class="glass-card text-center text-success">
                <h6 class="text-muted">Current Fund</h6>
                <h2 id="total-fund">$0.00</h2>
            </div>
        </div>
        <div class="col-md-4">
            <div class="glass-card text-center text-warning">
                <h6 class="text-muted">Events Organized</h6>
                <h2>14</h2>
            </div>
        </div>

        <div class="col-lg-7">
            <h4 class="mb-4">Member Directory</h4>
            <div id="member-list" class="row">
                </div>
        </div>

        <div class="col-lg-5">
            <h4 class="mb-4">Finance Ledger</h4>
            <div class="glass-card p-0 overflow-hidden">
                <table class="table table-dark table-hover m-0">
                    <thead>
                        <tr>
                            <th>Description</th>
                            <th>Amount</th>
                        </tr>
                    </thead>
                    <tbody id="finance-list">
                        </tbody>
                </table>
            </div>
        </div>
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
        appId: "1:898053892858:web:e81b46946d2f9e84b73743",
        measurementId: "G-C699C3CKG8"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    // --- FUNCTION: Add Member ---
    window.addNewMember = async function() {
        const name = prompt("Enter Full Name:");
        const role = prompt("Enter Designation (e.g. Secretary):");
        if (name && role) {
            await addDoc(collection(db, "members"), { name, role, date: new Date() });
        }
    }

    // --- FUNCTION: Add Finance Record ---
    window.addFinance = async function() {
        const desc = prompt("Enter Description:");
        const amount = prompt("Enter Amount (e.g. 500 or -200 for expense):");
        if (desc && amount) {
            await addDoc(collection(db, "finance"), { desc, amount: parseFloat(amount), date: new Date() });
        }
    }

    // --- REAL-TIME LISTENERS ---
    
    // Listen for Members
    onSnapshot(collection(db, "members"), (snapshot) => {
        let html = '';
        document.getElementById('member-count').innerText = snapshot.size;
        snapshot.forEach((doc) => {
            const m = doc.data();
            html += `
            <div class="col-md-6 mb-3">
                <div class="glass-card d-flex align-items-center p-3">
                    <div class="profile-img-circle me-3"><i class="fas fa-user text-white"></i></div>
                    <div><span class="status-badge">${m.role}</span><h6 class="mb-0 mt-1">${m.name}</h6></div>
                </div>
            </div>`;
        });
        document.getElementById('member-list').innerHTML = html;
    });

    // Listen for Finance
    onSnapshot(collection(db, "finance"), (snapshot) => {
        let html = '';
        let total = 0;
        snapshot.forEach((doc) => {
            const f = doc.data();
            total += f.amount;
            html += `<tr><td>${f.desc}</td><td class="${f.amount >= 0 ? 'text-success' : 'text-danger'}">${f.amount >= 0 ? '+' : ''}${f.amount}</td></tr>`;
        });
        document.getElementById('finance-list').innerHTML = html;
        document.getElementById('total-fund').innerText = `$${total.toFixed(2)}`;
    });

</script>

</body>
</html>
