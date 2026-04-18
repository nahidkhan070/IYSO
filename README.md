<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IYSO Premium Dashboard</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
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
            font-family: 'Plus Jakarta Sans', sans-serif;
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
        }

        .main {
            margin-left: 260px;
            padding: 25px;
        }

        .nav-link {
            color: #aaa;
            margin-bottom: 10px;
            cursor: pointer;
            padding: 10px;
            transition: 0.3s;
            border-radius: 8px;
        }

        .nav-link.active, .nav-link:hover {
            color: #fff !important;
            background: var(--green);
        }

        .glass {
            background: var(--card);
            border-radius: 20px;
            padding: 20px;
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255,255,255,0.05);
            height: 100%;
        }

        .stat {
            font-size: 28px;
            font-weight: 700;
            color: var(--gold);
        }

        /* Modal Customization */
        .modal-content {
            background: #121417;
            border: 1px solid var(--green);
            border-radius: 20px;
        }
        .form-control, .form-select {
            background: #1a1d21;
            border: 1px solid #333;
            color: white;
        }
        .form-control:focus {
            background: #1a1d21;
            color: white;
            border-color: var(--green);
            box-shadow: none;
        }
        .table { color: white; }
        /* Custom Payment Method Colors */
.bg-pink {
    background-color: #e2136e !important; /* bKash Pink */
}

.bg-orange {
    background-color: #f7941d !important; /* Nagad Orange */
}

.badge {
    font-weight: 600;
    letter-spacing: 0.5px;
    text-transform: uppercase;
    font-size: 0.75rem;
}
    </style>
</head>

<body>

<div class="sidebar">
    <h2 class="fw-800 mb-4 text-center" style="color: var(--gold);">IYSO</h2>
    <div class="nav-link active" data-page="dash">Dashboard</div>
    <div class="nav-link" data-page="members">Members</div>
    <div class="nav-link" data-page="donations">Donations</div>
    <div class="nav-link" data-page="events">Events</div>
</div>

<div class="main">
    <div id="dash" class="page">
        <h3 class="mb-4">Executive Overview</h3>
        <div class="row g-3">
            <div class="col-md-4">
                <div class="glass">
                    <h6>Total Fund Collected</h6>
                    <div class="stat" id="totalFund">0</div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="glass">
                    <h6>Monthly Subscription Total</h6>
                    <div class="stat" id="monthlyFund">0</div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="glass">
                    <h6>Net Event Balance</h6>
                    <div class="stat" id="balanceFund">0</div>
                </div>
            </div>
        </div>

        <div class="row mt-4">
            <div class="col-md-6">
                <div class="glass">
                    <h6 class="mb-3">Donation Distribution</h6>
                    <canvas id="donationChart"></canvas>
                </div>
            </div>
            <div class="col-md-6">
                <div class="glass">
                    <h6 class="mb-3">Fund vs Expenditure</h6>
                    <canvas id="eventChart"></canvas>
                </div>
            </div>
        </div>
    </div>

    <div id="members" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3>Organization Members</h3>
            <button onclick="openForm('members')" class="btn btn-success px-4">Add Member</button>
        </div>
        <div class="glass">
            <div id="memberList">Loading members...</div>
        </div>
    </div>

    <div id="donations" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3>Donation Logs</h3>
            <button onclick="openForm('donations')" class="btn btn-success px-4">New Donation</button>
        </div>
        <div class="glass">
            <div id="donationList">Loading logs...</div>
        </div>
    </div>

    <div id="events" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3>Event Management</h3>
            <button onclick="openForm('events')" class="btn btn-success px-4">Create Event</button>
        </div>
        <div class="glass">
            <div id="eventList">Loading events...</div>
        </div>
    </div>
</div>

<div class="modal fade" id="dataModal" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
            <div class="modal-header border-0">
                <h5 class="modal-title" id="modalTitle">Entry Form</h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body" id="modalBody">
                </div>
            <div class="modal-footer border-0">
                <button type="button" class="btn btn-dark" data-bs-dismiss="modal">Close</button>
                <button type="button" class="btn btn-success" id="saveBtn">Save Entry</button>
            </div>
        </div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, deleteDoc, doc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "YOUR_KEY",
        projectId: "iyso-web"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    const bsModal = new bootstrap.Modal(document.getElementById('dataModal'));

    // NAVIGATION SYSTEM
    document.querySelectorAll('.nav-link').forEach(link => {
        link.onclick = () => {
            document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
            link.classList.add('active');
            document.querySelectorAll('.page').forEach(p => p.style.display = 'none');
            document.getElementById(link.dataset.page).style.display = 'block';
        };
    });

    // OPEN FORM LOGIC
    window.openForm = (type, existingData = null) => {
    const body = document.getElementById('modalBody');
    const saveBtn = document.getElementById('saveBtn');
    const title = document.getElementById('modalTitle');

    if (type === 'members') {
        title.innerText = existingData ? "Edit Member Details" : "Add New Member";
        body.innerHTML = `
            <input type="text" id="mUID" class="form-control mb-3" placeholder="Unique ID (e.g. IYSO-001)" value="${existingData?.uid || ''}">
            <input type="text" id="mName" class="form-control mb-3" placeholder="Full Name" value="${existingData?.name || ''}">
            <input type="text" id="mDesig" class="form-control mb-3" placeholder="Designation" value="${existingData?.designation || ''}">
            <div class="row mb-3">
                <div class="col">
                    <select id="mBlood" class="form-select">
                        <option value="">Blood Group</option>
                        ${['A+', 'A-', 'B+', 'B-', 'O+', 'O-', 'AB+', 'AB-'].map(bg => 
                            `<option value="${bg}" ${existingData?.blood === bg ? 'selected' : ''}>${bg}</option>`
                        ).join('')}
                    </select>
                </div>
                <div class="col">
                    <input type="text" id="mPhone" class="form-control" placeholder="Phone No" value="${existingData?.phone || ''}">
                </div>
            </div>
            <input type="email" id="mEmail" class="form-control" placeholder="Email Address" value="${existingData?.email || ''}">`;

        saveBtn.onclick = async () => {
            const data = {
                uid: document.getElementById('mUID').value,
                name: document.getElementById('mName').value,
                designation: document.getElementById('mDesig').value,
                blood: document.getElementById('mBlood').value,
                phone: document.getElementById('mPhone').value,
                email: document.getElementById('mEmail').value
            };

            if (existingData) {
                await updateDoc(doc(db, "members", existingData.id), data);
            } else {
                await addDoc(collection(db, "members"), data);
            }
            bsModal.hide();
            };
        } 
        
       else if (type === 'donations') {
    title.innerText = existingData ? "Edit Donation Log" : "New Donation Entry";
    
    // Get current date in YYYY-MM-DD format for the input field
    const today = new Date().toISOString().split('T')[0];
    const displayDate = existingData?.date || today;

    body.innerHTML = `
        <div class="row mb-3">
            <div class="col-md-5">
                <label class="small text-muted mb-1">Member ID</label>
                <input type="text" id="dUID" class="form-control" placeholder="e.g. IYSO-001" value="${existingData?.uid || ''}">
            </div>
            <div class="col-md-7">
                <label class="small text-muted mb-1">Member Name</label>
                <input type="text" id="dName" class="form-control" placeholder="Auto-filled" value="${existingData?.name || ''}" readonly style="background: #0d1117;">
            </div>
        </div>
        <div class="row mb-3">
            <div class="col">
                <label class="small text-muted mb-1">Amount ($)</label>
                <input type="number" id="dAmount" class="form-control" placeholder="0.00" value="${existingData?.amount || ''}">
            </div>
            <div class="col">
                <label class="small text-muted mb-1">Method</label>
                <select id="dSystem" class="form-select">
                    <option value="">Select System</option>
                    ${['Bkash', 'Nagad', 'By-Cash'].map(sys => 
                        `<option value="${sys}" ${existingData?.system === sys ? 'selected' : ''}>${sys}</option>`
                    ).join('')}
                </select>
            </div>
        </div>
        <div class="row mb-3">
            <div class="col">
                <label class="small text-muted mb-1">Date</label>
                <input type="date" id="dDate" class="form-control" value="${displayDate}">
            </div>
            <div class="col">
                <label class="small text-muted mb-1">Donation Type</label>
                <select id="dType" class="form-select">
                    <option value="monthly" ${existingData?.type === 'monthly' ? 'selected' : ''}>Monthly</option>
                    <option value="event" ${existingData?.type === 'event' ? 'selected' : ''}>Event</option>
                </select>
            </div>
        </div>`;

    // --- AUTO-FILL LOGIC ---
    const idInput = document.getElementById('dUID');
    idInput.oninput = () => {
        const val = idInput.value.trim();
        const memberRows = document.querySelectorAll('#memberList tr');
        let found = false;
        memberRows.forEach(tr => {
            const uid = tr.cells[0]?.innerText;
            const name = tr.cells[1]?.innerText;
            if(uid === val && val !== "") {
                document.getElementById('dName').value = name;
                found = true;
            }
        });
        if(!found) document.getElementById('dName').value = "";
    };

    // --- SAVE / UPDATE LOGIC ---
    saveBtn.onclick = async () => {
        const data = {
            uid: document.getElementById('dUID').value,
            name: document.getElementById('dName').value,
            amount: Number(document.getElementById('dAmount').value),
            system: document.getElementById('dSystem').value,
            type: document.getElementById('dType').value,
            date: document.getElementById('dDate').value
        };

        try {
            if (existingData && existingData.id) {
                // UPDATE existing record
                const docRef = doc(db, "donations", existingData.id);
                await updateDoc(docRef, data);
            } else {
                // ADD new record
                await addDoc(collection(db, "donations"), data);
            }
            bsModal.hide();
        } catch (error) {
            console.error("Error saving donation: ", error);
            alert("Failed to save. Check console for details.");
        }
    };
}

        else if (type === 'events') {
            title.innerText = "Add Event";
            body.innerHTML = `
                <input type="text" id="eName" class="form-control mb-3" placeholder="Event Title">
                <input type="number" id="eFund" class="form-control mb-3" placeholder="Budget Raised">
                <input type="number" id="eCost" class="form-control" placeholder="Actual Expense">`;
            saveBtn.onclick = async () => {
                await addDoc(collection(db, "events"), {
                    name: document.getElementById('eName').value,
                    fund: Number(document.getElementById('eFund').value),
                    cost: Number(document.getElementById('eCost').value)
                });
                bsModal.hide();
            };
        }
        bsModal.show();
    };

    // GLOBAL DELETE
    window.deleteDocItem = async (col, id) => {
        if(confirm("Confirm deletion?")) await deleteDoc(doc(db, col, id));
    };

    // REAL-TIME DATA LISTENERS
    let donationChart, eventChart;

    // 1. Members
  onSnapshot(collection(db, "members"), snap => {
    let html = `
    <div class="table-responsive">
        <table class="table table-hover mt-2 align-middle" style="font-size: 0.9rem;">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Designation</th>
                    <th>Blood</th>
                    <th>Contact</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>`;
    
    snap.forEach(d => {
        const m = d.data();
        // This converts the data into a string so the Edit button can read it
        const memberData = JSON.stringify({id: d.id, ...m}).replace(/"/g, '&quot;');
        
        html += `
            <tr>
                <td class="text-warning fw-bold">${m.uid || '-'}</td>
                <td>${m.name}</td>
                <td><small>${m.designation || '-'}</small></td>
                <td><span class="badge bg-danger">${m.blood || '-'}</span></td>
                <td><small>${m.phone || ''}<br><span class="text-muted">${m.email}</span></small></td>
                <td>
                    <button class="btn btn-sm btn-outline-info me-1" onclick='openForm("members", ${memberData})'>Edit</button>
                    <button class="btn btn-sm btn-outline-danger" onclick="deleteDocItem('members','${d.id}')">Delete</button>
                </td>
            </tr>`;
    });
    document.getElementById('memberList').innerHTML = html + `</tbody></table></div>`;
});

    // 2. Donations & Chart
    onSnapshot(collection(db, "donations"), snap => {
    let total = 0, monthly = 0, event = 0;
    let html = `
    <div class="table-responsive">
        <table class="table table-hover mt-2 align-middle">
            <thead>
                <tr>
                    <th>Date</th> 
                    <th>Member</th>
                    <th>Amount</th>
                    <th>Method</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>`;
    
    snap.forEach(d => {
    const x = d.data();
    const donationData = JSON.stringify({id: d.id, ...x}).replace(/"/g, '&quot;');
    
    total += x.amount;
    if (x.type === "monthly") monthly += x.amount; else event += x.amount;

    // Define color logic for payment systems
    let systemBadgeColor = "border-secondary text-light"; // Default
    if (x.system === 'Bkash') systemBadgeColor = "bg-pink text-white"; 
    if (x.system === 'Nagad') systemBadgeColor = "bg-orange text-white";
    if (x.system === 'By-Cash') systemBadgeColor = "bg-success text-white";

    html += `
        <tr>
            <td>
            <td><small class="text-muted">${x.date || '-'}</small></td> <td>
                <span class="text-warning small fw-bold">${x.uid || 'Guest'}</span><br>
                ${x.name || 'Anonymous'}
            </td>
            <td class="stat" style="font-size: 1.1rem;">$${x.amount}</td>
            <td><span class="badge ${systemBadgeColor}" style="padding: 5px 10px;">${x.system || '-'}</span></td>
            <td><small class="text-muted">${x.type}</small></td>
            <td>
                <button class="btn btn-sm btn-outline-info me-1" onclick='openForm("donations", ${donationData})'>Edit</button>
                <button class="btn btn-sm btn-outline-danger" onclick="deleteDocItem('donations','${d.id}')">Delete</button>
            </td>
        </tr>`;
});

    document.getElementById("totalFund").innerText = `$${total}`;
    document.getElementById("monthlyFund").innerText = `$${monthly}`;
    document.getElementById('donationList').innerHTML = html + `</tbody></table></div>`;

    // --- CHART UPDATE LOGIC --- (Keep your existing chart code here)
    if (donationChart) donationChart.destroy();
    donationChart = new Chart(document.getElementById('donationChart'), {
        type: 'doughnut',
        data: {
            labels: ['Monthly', 'Event'],
            datasets: [{ data: [monthly, event], backgroundColor: ['#006837', '#c6a34f'], borderWidth: 0 }]
        },
        options: { plugins: { legend: { labels: { color: '#fff' } } } }
    });
});

    // 3. Events & Chart
    onSnapshot(collection(db, "events"), snap => {
        let cost = 0, fund = 0;
        let html = `<table class="table table-hover mt-2"><thead><tr><th>Event</th><th>Raised</th><th>Cost</th><th>Action</th></tr></thead><tbody>`;
        
        snap.forEach(d => {
            const e = d.data();
            fund += e.fund; cost += e.cost;
            html += `<tr><td>${e.name}</td><td>$${e.fund}</td><td>$${e.cost}</td><td><button class="btn btn-sm btn-outline-danger" onclick="deleteDocItem('events','${d.id}')">Delete</button></td></tr>`;
        });

        document.getElementById("balanceFund").innerText = `$${fund - cost}`;
        document.getElementById('eventList').innerHTML = html + `</tbody></table>`;

        if (eventChart) eventChart.destroy();
        eventChart = new Chart(document.getElementById('eventChart'), {
            type: 'bar',
            data: {
                labels: ['Budget Raised', 'Expense'],
                datasets: [{ label: 'USD', data: [fund, cost], backgroundColor: ['#006837', '#c6a34f'] }]
            },
            options: { 
                scales: { 
                    y: { ticks: { color: '#fff' }, grid: { color: 'rgba(255,255,255,0.1)' } },
                    x: { ticks: { color: '#fff' } }
                },
                plugins: { legend: { display: false } }
            }
        });
    });
</script>

</body>
</html>
