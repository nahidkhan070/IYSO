
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
            --light-gradient: linear-gradient(135deg, #ffffff 0%, #f0f7f3 100%);
            --emerald-gradient: linear-gradient(135deg, #006837 0%, #004d29 100%);
        }

        body {
            background: var(--light-gradient);
            color: #2d3436;
            font-family: 'Plus Jakarta Sans', sans-serif;
            min-height: 100vh;
        }

        /* Premium Gold Gradient Border */
        .premium-border {
            border: 2px solid;
            border-image: linear-gradient(to right, var(--iyso-gold), #fffce0) 1;
        }

        .navbar {
            background: var(--emerald-gradient);
            box-shadow: 0 4px 20px rgba(0, 104, 55, 0.2);
            padding: 15px 0;
        }

        .glass-card {
            background: rgba(255, 255, 255, 0.9);
            border: 1px solid rgba(0, 104, 55, 0.1);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.05);
            padding: 25px;
            transition: 0.3s;
        }

        .btn-gold {
            background: linear-gradient(135deg, var(--iyso-gold) 0%, #e5c06d 100%);
            color: #fff; font-weight: 700; border: none; border-radius: 10px;
            padding: 10px 20px; box-shadow: 0 4px 15px rgba(198, 163, 79, 0.3);
        }

        .member-id-tag {
            background: var(--iyso-green);
            color: white;
            padding: 2px 10px;
            border-radius: 5px;
            font-size: 0.75rem;
            font-weight: bold;
        }

        .stat-card {
            background: var(--emerald-gradient);
            color: white;
            border-radius: 20px;
            padding: 20px;
        }

        .nav-tabs .nav-link { color: var(--iyso-green); font-weight: 600; border: none; }
        .nav-tabs .nav-link.active { color: var(--iyso-gold); border-bottom: 3px solid var(--iyso-gold); background: none; }
    </style>
</head>
<body>

<nav class="navbar mb-5">
    <div class="container">
        <a class="navbar-brand d-flex align-items-center text-white" href="#">
            <img src="image_0.png" alt="Logo" height="60" style="filter: drop-shadow(0 0 5px rgba(255,255,255,0.5));">
            <div class="ms-3">
                <h4 class="mb-0 fw-bold">IYSO PORTAL</h4>
                <small style="font-size: 0.6rem; letter-spacing: 1px;">IDEAL YOUTH SERVICE ORGANIZATION</small>
            </div>
        </a>
    </div>
</nav>

<div class="container">
    <div class="row g-4 mb-5">
        <div class="col-md-4">
            <div class="stat-card shadow">
                <h6>Monthly Donation Summary</h6>
                <h2 id="monthly-total">৳0</h2>
            </div>
        </div>
        <div class="col-md-4">
            <div class="stat-card shadow" style="background: var(--iyso-gold);">
                <h6>Yearly Total</h6>
                <h2 id="yearly-total">৳0</h2>
            </div>
        </div>
        <div class="col-md-4">
            <div class="glass-card d-flex align-items-center justify-content-center">
                <button class="btn btn-gold w-100 py-3" onclick="showAddMember()"><i class="fas fa-user-plus me-2"></i>Register New Member</button>
            </div>
        </div>
    </div>

    <ul class="nav nav-tabs mb-4" id="myTab" role="tablist">
        <li class="nav-item"><button class="nav-link active" onclick="showTab('members-tab')">Member Directory</button></li>
        <li class="nav-item"><button class="nav-link" onclick="showTab('history-tab')">Donation History</button></li>
    </ul>

    <div id="members-tab" class="tab-content active">
        <div class="row g-4" id="member-display">
            </div>
    </div>

    <div id="history-tab" class="tab-content d-none">
        <div class="glass-card">
            <div class="input-group mb-4">
                <input type="text" id="searchId" class="form-control" placeholder="Enter Member ID (e.g. IYSO-001)">
                <button class="btn btn-gold" onclick="searchHistory()">Search History</button>
            </div>
            <div id="history-results"></div>
        </div>
    </div>
</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, query, where, orderBy } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

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

    // --- Tab Switcher ---
    window.showTab = (tabId) => {
        document.querySelectorAll('.tab-content').forEach(t => t.classList.add('d-none'));
        document.getElementById(tabId).classList.remove('d-none');
    };

    // --- Register Member ---
    window.showAddMember = async () => {
        const name = prompt("Full Name:");
        const id = prompt("Assign Unique ID (e.g. IYSO-001):");
        if(name && id) {
            await addDoc(collection(db, "members"), { name, memberId: id, totalDonated: 0 });
        }
    };

    // --- Add Donation ---
    window.donate = async (memberId, name) => {
        const amt = prompt(`Enter Donation Amount for ${name}:`);
        if(amt) {
            await addDoc(collection(db, "donations"), {
                memberId: memberId,
                name: name,
                amount: parseFloat(amt),
                date: new Date(),
                month: new Date().getMonth(),
                year: new Date().getFullYear()
            });
            alert("Donation Recorded!");
        }
    };

    // --- Real-time Listeners ---
    onSnapshot(collection(db, "members"), (snap) => {
        let html = '';
        snap.forEach(doc => {
            const m = doc.data();
            html += `
            <div class="col-md-4">
                <div class="glass-card text-center border-top border-5 border-success">
                    <span class="member-id-tag">${m.memberId}</span>
                    <h5 class="mt-3 fw-bold">${m.name}</h5>
                    <button class="btn btn-sm btn-outline-success mt-2" onclick="donate('${m.memberId}', '${m.name}')">Add Donation</button>
                </div>
            </div>`;
        });
        document.getElementById('member-display').innerHTML = html;
    });

    // --- Summary Calculations ---
    onSnapshot(collection(db, "donations"), (snap) => {
        let monthTotal = 0; let yearTotal = 0;
        const now = new Date();
        snap.forEach(doc => {
            const d = doc.data();
            if(d.year === now.getFullYear()) {
                yearTotal += d.amount;
                if(d.month === now.getMonth()) monthTotal += d.amount;
            }
        });
        document.getElementById('monthly-total').innerText = `৳${monthTotal}`;
        document.getElementById('yearly-total').innerText = `৳${yearTotal}`;
    });

    // --- Search Member History ---
    window.searchHistory = async () => {
        const id = document.getElementById('searchId').value;
        const q = query(collection(db, "donations"), where("memberId", "==", id), orderBy("date", "desc"));
        
        onSnapshot(q, (snap) => {
            let total = 0;
            let html = `<h5 class="fw-bold mb-3 text-success">Donation History for ${id}</h5><table class="table">`;
            snap.forEach(doc => {
                const d = doc.data();
                total += d.amount;
                html += `<tr><td>${d.date.toDate().toLocaleDateString()}</td><td>৳${d.amount}</td></tr>`;
            });
            html += `<tr class="table-success"><td><strong>Total Donated</strong></td><td><strong>৳${total}</strong></td></tr></table>`;
            document.getElementById('history-results').innerHTML = html;
        });
    };

</script>
</body>
</html>
