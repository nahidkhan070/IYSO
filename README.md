
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IYSO Premium Management</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=Hind+Siliguri:wght@400;600&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        :root {
            --green: #006837;
            --gold: #c6a34f;
            --bg: #05080c;
            --card: rgba(20, 25, 32, 0.85);
        }

        body {
            background: radial-gradient(circle at top right, #003d21, var(--bg));
            color: #fff;
            font-family: 'Plus Jakarta Sans', 'Hind Siliguri', sans-serif;
            min-height: 100vh;
        }

        .sidebar {
            width: 250px;
            height: 100vh;
            position: fixed;
            background: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(20px);
            padding: 20px;
            border-right: 1px solid rgba(255,255,255,0.1);
            z-index: 1000;
        }

        .main { margin-left: 260px; padding: 25px; }

        .nav-link {
            color: #aaa; margin-bottom: 10px; cursor: pointer;
            padding: 12px; transition: 0.3s; border-radius: 8px;
        }

        .nav-link.active, .nav-link:hover {
            color: #fff !important; background: var(--green);
        }

        .glass {
            background: var(--card); border-radius: 20px; padding: 20px;
            backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.05);
        }

        .stat { font-size: 28px; font-weight: 700; color: var(--gold); }

        .lang-btn {
            position: fixed; top: 20px; right: 20px; z-index: 1001;
            background: var(--card); border: 1px solid var(--green); color: white;
            border-radius: 30px; padding: 5px 15px;
        }

        .modal-content { background: #121417; border: 1px solid var(--green); border-radius: 20px; }
        .form-control, .form-select { background: #1a1d21; border: 1px solid #333; color: white; margin-bottom: 10px; }
        .form-control:focus { background: #1a1d21; color: white; border-color: var(--green); box-shadow: none; }
        .table { color: white; vertical-align: middle; }
    </style>
</head>

<body>

<button class="lang-btn" onclick="toggleLang()" id="langSwitcher">বাংলা</button>

<div class="sidebar">
    <h2 class="fw-800 mb-4 text-center" style="color: var(--gold);">IYSO</h2>
    <div class="nav-link active" data-page="dash" id="nav-dash">Dashboard</div>
    <div class="nav-link" data-page="members" id="nav-members">Members</div>
    <div class="nav-link" data-page="donations" id="nav-donations">Donations</div>
    <div class="nav-link" data-page="events" id="nav-events">Events</div>
</div>

<div class="main">
    <div id="dash" class="page">
        <h3 id="head-dash" class="mb-4">Executive Overview</h3>
        <div class="row g-3">
            <div class="col-md-4">
                <div class="glass">
                    <h6 id="card-total">Total Fund</h6>
                    <div class="stat" id="totalFund">0</div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="glass">
                    <h6 id="card-monthly">Monthly Subscriptions</h6>
                    <div class="stat" id="monthlyFund">0</div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="glass">
                    <h6 id="card-balance">Net Balance</h6>
                    <div class="stat" id="balanceFund">0</div>
                </div>
            </div>
        </div>

        <div class="row mt-4">
            <div class="col-md-6"><div class="glass"><canvas id="donationChart"></canvas></div></div>
            <div class="col-md-6"><div class="glass"><canvas id="eventChart"></canvas></div></div>
        </div>
    </div>

    <div id="members" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3 id="head-members">Members</h3>
            <button onclick="openMemberForm()" class="btn btn-success px-4" id="btn-add-member">Add Member</button>
        </div>
        <div class="glass table-responsive">
            <div id="memberList">Loading...</div>
        </div>
    </div>

    <div id="donations" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3 id="head-donations">Donations</h3>
            <button onclick="openDonationForm()" class="btn btn-success px-4" id="btn-add-donation">Record Donation</button>
        </div>
        <div class="glass table-responsive"><div id="donationList">Loading...</div></div>
    </div>

    <div id="events" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3 id="head-events">Events</h3>
            <button onclick="openEventForm()" class="btn btn-success px-4" id="btn-add-event">Create Event</button>
        </div>
        <div class="glass table-responsive"><div id="eventList">Loading...</div></div>
    </div>
</div>

<div class="modal fade" id="dataModal" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
            <div class="modal-header border-0">
                <h5 class="modal-title" id="modalTitle">Form</h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body" id="modalBody"></div>
            <div class="modal-footer border-0">
                <button type="button" class="btn btn-success w-100" id="saveBtn">Save</button>
            </div>
        </div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, deleteDoc, doc, updateDoc, getDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

    const firebaseConfig = { apiKey: "YOUR_KEY", projectId: "iyso-web" };
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    const bsModal = new bootstrap.Modal(document.getElementById('dataModal'));

    // --- LANGUAGE SYSTEM ---
    let currentLang = 'en';
    const dict = {
        en: {
            dash: "Dashboard", members: "Members", donations: "Donations", events: "Events",
            total: "Total Fund", monthly: "Monthly Subscriptions", balance: "Net Balance",
            addMember: "Add Member", addDonation: "Add Donation", addEvent: "Create Event",
            save: "Save Changes", delete: "Delete", edit: "Edit", confirm: "Are you sure?",
            id: "ID", name: "Name", desig: "Designation", phone: "Phone", email: "Email", action: "Action"
        },
        bn: {
            dash: "ড্যাশবোর্ড", members: "সদস্যবৃন্দ", donations: "অনুদান", events: "ইভেন্ট",
            total: "মোট তহবিল", monthly: "মাসিক চাঁদা", balance: "বর্তমান ব্যালেন্স",
            addMember: "সদস্য যোগ করুন", addDonation: "অনুদান যোগ করুন", addEvent: "ইভেন্ট তৈরি করুন",
            save: "সংরক্ষণ করুন", delete: "ডিলিট", edit: "সম্পাদনা", confirm: "আপনি কি নিশ্চিত?",
            id: "আইডি", name: "নাম", desig: "পদবী", phone: "ফোন", email: "ইমেইল", action: "অ্যাকশন"
        }
    };

    window.toggleLang = () => {
        currentLang = currentLang === 'en' ? 'bn' : 'en';
        document.getElementById('langSwitcher').innerText = currentLang === 'en' ? 'বাংলা' : 'English';
        applyLang();
    };

    function applyLang() {
        const d = dict[currentLang];
        document.getElementById('nav-dash').innerText = d.dash;
        document.getElementById('nav-members').innerText = d.members;
        document.getElementById('nav-donations').innerText = d.donations;
        document.getElementById('nav-events').innerText = d.events;
        document.getElementById('head-dash').innerText = d.dash;
        document.getElementById('head-members').innerText = d.members;
        document.getElementById('head-donations').innerText = d.donations;
        document.getElementById('head-events').innerText = d.events;
        document.getElementById('card-total').innerText = d.total;
        document.getElementById('card-monthly').innerText = d.monthly;
        document.getElementById('card-balance').innerText = d.balance;
        document.getElementById('btn-add-member').innerText = d.addMember;
        document.getElementById('btn-add-donation').innerText = d.addDonation;
        document.getElementById('btn-add-event').innerText = d.addEvent;
        // Refresh tables to update headers
        refreshTables();
    }

    // --- NAVIGATION ---
    document.querySelectorAll('.nav-link').forEach(link => {
        link.onclick = () => {
            document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
            link.classList.add('active');
            document.querySelectorAll('.page').forEach(p => p.style.display = 'none');
            document.getElementById(link.dataset.page).style.display = 'block';
        };
    });

    // --- MEMBER CRUD (ADD & EDIT) ---
    window.openMemberForm = async (id = null) => {
        const body = document.getElementById('modalBody');
        const saveBtn = document.getElementById('saveBtn');
        const title = document.getElementById('modalTitle');
        let data = { uid:'', name:'', desig:'', phone:'', email:'' };

        if(id) {
            const docSnap = await getDoc(doc(db, "members", id));
            data = docSnap.data();
            title.innerText = dict[currentLang].edit;
        } else {
            title.innerText = dict[currentLang].addMember;
        }

        body.innerHTML = `
            <input type="text" id="mUid" class="form-control" placeholder="${dict[currentLang].id}" value="${data.uid}">
            <input type="text" id="mName" class="form-control" placeholder="${dict[currentLang].name}" value="${data.name}">
            <input type="text" id="mDesig" class="form-control" placeholder="${dict[currentLang].desig}" value="${data.desig}">
            <input type="text" id="mPhone" class="form-control" placeholder="${dict[currentLang].phone}" value="${data.phone}">
            <input type="email" id="mEmail" class="form-control" placeholder="${dict[currentLang].email}" value="${data.email}">
        `;

        saveBtn.onclick = async () => {
            const payload = {
                uid: document.getElementById('mUid').value,
                name: document.getElementById('mName').value,
                desig: document.getElementById('mDesig').value,
                phone: document.getElementById('mPhone').value,
                email: document.getElementById('mEmail').value
            };
            if(id) await updateDoc(doc(db, "members", id), payload);
            else await addDoc(collection(db, "members"), payload);
            bsModal.hide();
        };
        bsModal.show();
    };

    // --- SHARED ACTIONS ---
    window.deleteDocItem = async (col, id) => {
        if(confirm(dict[currentLang].confirm)) await deleteDoc(doc(db, col, id));
    };

    // --- REAL-TIME LISTENERS ---
    let donationChart, eventChart;

    function refreshTables() {
        // Handled by onSnapshot listeners automatically
    }

    onSnapshot(collection(db, "members"), snap => {
        const d = dict[currentLang];
        let html = `<table class="table table-hover"><thead><tr><th>${d.id}</th><th>${d.name}</th><th>${d.desig}</th><th>${d.phone}</th><th>${d.action}</th></tr></thead><tbody>`;
        snap.forEach(doc => {
            const m = doc.data();
            html += `<tr>
                <td>${m.uid}</td><td>${m.name}</td><td>${m.desig}</td><td>${m.phone}</td>
                <td>
                    <button class="btn btn-sm btn-outline-warning me-1" onclick="openMemberForm('${doc.id}')">${d.edit}</button>
                    <button class="btn btn-sm btn-outline-danger" onclick="deleteDocItem('members','${doc.id}')">${d.delete}</button>
                </td>
            </tr>`;
        });
        document.getElementById('memberList').innerHTML = html + `</tbody></table>`;
    });

    // Donations Listener
    onSnapshot(collection(db, "donations"), snap => {
        let total = 0, monthly = 0, event = 0;
        let html = `<table class="table"><thead><tr><th>Amount</th><th>Type</th><th>Action</th></tr></thead><tbody>`;
        snap.forEach(doc => {
            const x = doc.data();
            total += x.amount;
            if (x.type === "monthly") monthly += x.amount; else event += x.amount;
            html += `<tr><td>$${x.amount}</td><td>${x.type}</td><td><button class="btn btn-sm btn-outline-danger" onclick="deleteDocItem('donations','${doc.id}')">X</button></td></tr>`;
        });
        document.getElementById("totalFund").innerText = `$${total}`;
        document.getElementById("monthlyFund").innerText = `$${monthly}`;
        document.getElementById('donationList').innerHTML = html + `</tbody></table>`;
        if (donationChart) donationChart.destroy();
        donationChart = new Chart(document.getElementById('donationChart'), {
            type: 'doughnut', data: { labels: ['Monthly', 'Event'], datasets: [{ data: [monthly, event], backgroundColor: ['#006837', '#c6a34f'], borderWidth: 0 }] }
        });
    });

    // Events Listener
    onSnapshot(collection(db, "events"), snap => {
        let cost = 0, fund = 0;
        let html = `<table class="table"><thead><tr><th>Event</th><th>Raised</th><th>Cost</th><th>Action</th></tr></thead><tbody>`;
        snap.forEach(doc => {
            const e = doc.data();
            fund += e.fund; cost += e.cost;
            html += `<tr><td>${e.name}</td><td>$${e.fund}</td><td>$${e.cost}</td><td><button class="btn btn-sm btn-outline-danger" onclick="deleteDocItem('events','${doc.id}')">X</button></td></tr>`;
        });
        document.getElementById("balanceFund").innerText = `$${fund - cost}`;
        document.getElementById('eventList').innerHTML = html + `</tbody></table>`;
        if (eventChart) eventChart.destroy();
        eventChart = new Chart(document.getElementById('eventChart'), {
            type: 'bar', data: { labels: ['Raised', 'Expense'], datasets: [{ data: [fund, cost], backgroundColor: ['#006837', '#c6a34f'] }] }
        });
    });

    applyLang(); // Init
</script>

</body>
</html>
