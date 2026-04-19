
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IYSO Premium Financial Dashboard</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        :root {
            --green: #006837;
            --gold: #c6a34f;
            --dark-green: #004d2e;
            --dark-red: #8b0000;
            --bg: #0a0f14;
            --card: rgba(18, 25, 32, 0.92);
            --pink: #e2136e;
            --orange: #f7941d;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #0a1a0f 0%, #0a0f14 100%);
            color: #fff;
            font-family: 'Inter', sans-serif;
            min-height: 100vh;
        }

        /* Premium Sidebar */
        .sidebar {
            width: 280px;
            height: 100vh;
            position: fixed;
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(20px);
            padding: 30px 20px;
            border-right: 1px solid rgba(255,255,255,0.08);
            z-index: 100;
        }

        .logo {
            font-size: 28px;
            font-weight: 800;
            background: linear-gradient(135deg, var(--gold) 0%, #ffd700 100%);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 40px;
            text-align: center;
            letter-spacing: 2px;
        }

        .nav-item {
            padding: 12px 20px;
            margin: 8px 0;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            color: rgba(255,255,255,0.7);
            font-weight: 500;
        }

        .nav-item:hover {
            background: rgba(0, 104, 55, 0.3);
            color: white;
            transform: translateX(5px);
        }

        .nav-item.active {
            background: linear-gradient(135deg, var(--green), var(--dark-green));
            color: white;
            box-shadow: 0 4px 15px rgba(0,104,55,0.3);
        }

        /* Main Content */
        .main {
            margin-left: 280px;
            padding: 30px 40px;
        }

        /* Glass Card Effect */
        .glass-card {
            background: var(--card);
            backdrop-filter: blur(10px);
            border-radius: 24px;
            padding: 24px;
            border: 1px solid rgba(255,255,255,0.05);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            height: 100%;
        }

        .glass-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        /* Net Balance - Big and Centered */
        .net-balance-card {
            background: linear-gradient(135deg, rgba(0,104,55,0.2) 0%, rgba(0,77,46,0.4) 100%);
            backdrop-filter: blur(10px);
            border-radius: 32px;
            padding: 40px;
            border: 2px solid rgba(198,163,79,0.3);
            text-align: center;
            box-shadow: 0 20px 40px rgba(0,0,0,0.4);
        }

        .net-balance-label {
            font-size: 18px;
            text-transform: uppercase;
            letter-spacing: 3px;
            color: var(--gold);
            margin-bottom: 20px;
        }

        .net-balance-amount {
            font-size: 72px;
            font-weight: 800;
            background: linear-gradient(135deg, var(--gold) 0%, #ffd700 100%);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            line-height: 1.2;
        }

        /* Small Cards */
        .small-card {
            padding: 20px;
        }

        .small-card-title {
            font-size: 13px;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: rgba(255,255,255,0.5);
            margin-bottom: 12px;
        }

        .small-card-amount {
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 8px;
        }

        .month-name {
            font-size: 12px;
            color: var(--gold);
            margin-top: 8px;
        }

        /* Money Receive Numbers */
        .money-numbers {
            background: rgba(0,0,0,0.5);
            border-radius: 16px;
            padding: 15px;
            border: 1px solid rgba(255,255,255,0.1);
        }

        .bkash-box {
            background: linear-gradient(135deg, var(--pink), #c40e5e);
            border-radius: 12px;
            padding: 12px 16px;
            margin-bottom: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .nagad-box {
            background: linear-gradient(135deg, var(--orange), #e67e00);
            border-radius: 12px;
            padding: 12px 16px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .bkash-box:hover, .nagad-box:hover {
            transform: scale(1.02);
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .send-number {
            font-size: 18px;
            font-weight: 700;
            letter-spacing: 1px;
        }

        /* Tables */
        .data-table {
            background: rgba(0,0,0,0.3);
            border-radius: 16px;
            overflow-x: auto;
        }

        .data-table table {
            width: 100%;
            color: white;
        }

        .data-table th {
            padding: 15px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            color: var(--gold);
            font-weight: 600;
        }

        .data-table td {
            padding: 12px 15px;
            border-bottom: 1px solid rgba(255,255,255,0.05);
        }

        .badge-add {
            background: var(--dark-green);
            color: #90ee90;
        }

        .badge-subtract {
            background: var(--dark-red);
            color: #ff9999;
        }

        /* Modal */
        .modal-content {
            background: #1a1f24;
            border: 1px solid var(--green);
            border-radius: 20px;
        }

        .form-control, .form-select {
            background: #2a2f35;
            border: 1px solid #3a3f45;
            color: white;
        }

        .form-control:focus, .form-select:focus {
            background: #2a2f35;
            color: white;
            border-color: var(--green);
            box-shadow: none;
        }

        .btn-success {
            background: var(--green);
            border: none;
        }

        .btn-success:hover {
            background: var(--dark-green);
        }

        /* Tabs */
        .nav-tabs {
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .nav-tabs .nav-link {
            color: rgba(255,255,255,0.6);
            border: none;
            font-weight: 600;
        }

        .nav-tabs .nav-link.active {
            color: var(--gold);
            background: transparent;
            border-bottom: 2px solid var(--gold);
        }

        /* Utility */
        .text-gold { color: var(--gold); }
        .text-dark-green { color: #90ee90; }
        .text-dark-red { color: #ff9999; }
    </style>
</head>
<body>

<div class="sidebar">
    <div class="logo">IYSO</div>
    <div class="nav-item active" data-page="dash">📊 Dashboard</div>
    <div class="nav-item" data-page="members">👥 Members</div>
    <div class="nav-item" data-page="donations">💰 Donations</div>
    <div class="nav-item" data-page="expenses">📉 Expenses</div>
    <div class="nav-item" data-page="events">🎪 Events</div>
</div>

<div class="main">
    <!-- Dashboard Page -->
    <div id="dash" class="page">
        <!-- Net Balance Row -->
        <div class="row mb-4">
            <div class="col-md-9">
                <div class="net-balance-card">
                    <div class="net-balance-label">NET BALANCE</div>
                    <div class="net-balance-amount" id="netBalance">$0</div>
                </div>
            </div>
            <div class="col-md-3">
                <div class="money-numbers">
                    <div class="bkash-box" onclick="editSendNumber('bkash')">
                        <div style="font-size: 12px; opacity: 0.8;">bKash (Send Money)</div>
                        <div class="send-number" id="bkashNumber">017XXXXXXXX</div>
                    </div>
                    <div class="nagad-box" onclick="editSendNumber('nagad')">
                        <div style="font-size: 12px; opacity: 0.8;">Nagad (Send Money)</div>
                        <div class="send-number" id="nagadNumber">017XXXXXXXX</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Top Row: Total Fund, Monthly Collection, Event Fund -->
        <div class="row g-4 mb-4">
            <div class="col-md-4">
                <div class="glass-card small-card">
                    <div class="small-card-title">TOTAL FUND COLLECTION</div>
                    <div class="small-card-amount" id="totalFund">$0</div>
                    <div class="month-name">Lifetime Collection</div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="glass-card small-card">
                    <div class="small-card-title">MONTHLY COLLECTION</div>
                    <div class="small-card-amount" id="monthlyCollection">$0</div>
                    <div class="month-name" id="currentMonthName">January 2024</div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="glass-card small-card">
                    <div class="small-card-title">EVENT FUND COLLECTION</div>
                    <div class="small-card-amount" id="eventFundCollection">$0</div>
                    <div class="month-name" id="eventMonthName">Event Donations</div>
                </div>
            </div>
        </div>

        <!-- Bottom Row: Monthly Expenses, Total Expenses -->
        <div class="row g-4">
            <div class="col-md-6">
                <div class="glass-card small-card">
                    <div class="small-card-title">MONTHLY EXPENSES</div>
                    <div class="small-card-amount" id="monthlyExpenses">$0</div>
                    <div class="month-name" id="expenseMonthName">Current Month Costs</div>
                </div>
            </div>
            <div class="col-md-6">
                <div class="glass-card small-card">
                    <div class="small-card-title">TOTAL EXPENSES</div>
                    <div class="small-card-amount" id="totalExpenses">$0</div>
                    <div class="month-name">Lifetime Expenses</div>
                </div>
            </div>
        </div>
    </div>

    <!-- Members Page -->
    <div id="members" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3>Organization Members</h3>
            <button onclick="openMemberForm()" class="btn btn-success px-4">+ Add Member</button>
        </div>
        <div class="data-table" id="memberList">Loading members...</div>
    </div>

    <!-- Donations Page -->
    <div id="donations" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3>Donation Logs</h3>
            <button onclick="openDonationForm()" class="btn btn-success px-4">+ New Donation</button>
        </div>
        <div class="data-table" id="donationList">Loading donations...</div>
    </div>

    <!-- Expenses Page -->
    <div id="expenses" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3>Expense Logs</h3>
            <button onclick="openExpenseForm()" class="btn btn-danger px-4">+ Add Expense</button>
        </div>
        <div class="data-table" id="expenseList">Loading expenses...</div>
    </div>

    <!-- Events Page -->
    <div id="events" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3>Event Management</h3>
            <button onclick="openEventForm()" class="btn btn-success px-4">+ Plan Event</button>
        </div>
        <ul class="nav nav-tabs mb-4">
            <li class="nav-item">
                <button class="nav-link active" data-bs-toggle="tab" data-bs-target="#planning">Planning</button>
            </li>
            <li class="nav-item">
                <button class="nav-link" data-bs-toggle="tab" data-bs-target="#executed">Executed</button>
            </li>
        </ul>
        <div class="tab-content">
            <div class="tab-pane fade show active" id="planning">
                <div class="data-table" id="planningList">Loading...</div>
            </div>
            <div class="tab-pane fade" id="executed">
                <div class="data-table" id="executedList">Loading...</div>
            </div>
        </div>
    </div>
</div>

<!-- Modal -->
<div class="modal fade" id="dataModal" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
            <div class="modal-header border-0">
                <h5 class="modal-title" id="modalTitle">Form</h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body" id="modalBody"></div>
            <div class="modal-footer border-0">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                <button type="button" class="btn btn-success" id="saveBtn">Save</button>
            </div>
        </div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, deleteDoc, doc, updateDoc, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "YOUR_KEY",
        projectId: "iyso-web"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    const bsModal = new bootstrap.Modal(document.getElementById('dataModal'));

    // Navigation
    document.querySelectorAll('.nav-item').forEach(item => {
        item.onclick = () => {
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            item.classList.add('active');
            document.querySelectorAll('.page').forEach(p => p.style.display = 'none');
            document.getElementById(item.dataset.page).style.display = 'block';
        };
    });

    // Get current month name
    function getCurrentMonth() {
        const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
        const now = new Date();
        return `${months[now.getMonth()]} ${now.getFullYear()}`;
    }

    // Initialize send numbers from localStorage
    let bkashNumber = localStorage.getItem('bkashNumber') || '017XXXXXXXX';
    let nagadNumber = localStorage.getItem('nagadNumber') || '017XXXXXXXX';
    document.getElementById('bkashNumber').innerText = bkashNumber;
    document.getElementById('nagadNumber').innerText = nagadNumber;
    document.getElementById('currentMonthName').innerText = getCurrentMonth();
    document.getElementById('expenseMonthName').innerText = getCurrentMonth();
    document.getElementById('eventMonthName').innerText = 'Event Donations';

    window.editSendNumber = (type) => {
        const newNumber = prompt(`Enter ${type.toUpperCase()} send money number:`, type === 'bkash' ? bkashNumber : nagadNumber);
        if (newNumber && newNumber.trim()) {
            if (type === 'bkash') {
                bkashNumber = newNumber;
                document.getElementById('bkashNumber').innerText = bkashNumber;
                localStorage.setItem('bkashNumber', bkashNumber);
            } else {
                nagadNumber = newNumber;
                document.getElementById('nagadNumber').innerText = nagadNumber;
                localStorage.setItem('nagadNumber', nagadNumber);
            }
        }
    };

    // Open Forms
    window.openMemberForm = (data = null) => {
        document.getElementById('modalTitle').innerText = data ? 'Edit Member' : 'Add Member';
        document.getElementById('modalBody').innerHTML = `
            <input type="text" id="mUID" class="form-control mb-3" placeholder="Member ID" value="${data?.uid || ''}">
            <input type="text" id="mName" class="form-control mb-3" placeholder="Full Name" value="${data?.name || ''}">
            <input type="text" id="mDesignation" class="form-control mb-3" placeholder="Designation" value="${data?.designation || ''}">
            <select id="mBlood" class="form-select mb-3">
                <option value="">Blood Group</option>
                ${['A+','A-','B+','B-','O+','O-','AB+','AB-'].map(b => `<option value="${b}" ${data?.blood === b ? 'selected' : ''}>${b}</option>`).join('')}
            </select>
            <input type="text" id="mPhone" class="form-control mb-3" placeholder="Phone" value="${data?.phone || ''}">
            <input type="email" id="mEmail" class="form-control" placeholder="Email" value="${data?.email || ''}">
        `;
        document.getElementById('saveBtn').onclick = async () => {
            const memberData = {
                uid: document.getElementById('mUID').value,
                name: document.getElementById('mName').value,
                designation: document.getElementById('mDesignation').value,
                blood: document.getElementById('mBlood').value,
                phone: document.getElementById('mPhone').value,
                email: document.getElementById('mEmail').value
            };
            if (data) await updateDoc(doc(db, "members", data.id), memberData);
            else await addDoc(collection(db, "members"), memberData);
            bsModal.hide();
        };
        bsModal.show();
    };

    window.openDonationForm = (data = null) => {
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('modalTitle').innerText = data ? 'Edit Donation' : 'New Donation';
        document.getElementById('modalBody').innerHTML = `
            <input type="text" id="dUID" class="form-control mb-3" placeholder="Member ID" value="${data?.uid || ''}">
            <input type="text" id="dName" class="form-control mb-3" placeholder="Member Name" value="${data?.name || ''}" readonly style="background:#1a1f24">
            <input type="number" id="dAmount" class="form-control mb-3" placeholder="Amount ($)" value="${data?.amount || ''}">
            <select id="dType" class="form-select mb-3">
                <option value="monthly" ${data?.type === 'monthly' ? 'selected' : ''}>Monthly Donation</option>
                <option value="event" ${data?.type === 'event' ? 'selected' : ''}>Event Donation</option>
            </select>
            <select id="dSystem" class="form-select mb-3">
                <option value="">Payment Method</option>
                <option value="Bkash" ${data?.system === 'Bkash' ? 'selected' : ''}>bKash</option>
                <option value="Nagad" ${data?.system === 'Nagad' ? 'selected' : ''}>Nagad</option>
                <option value="Cash" ${data?.system === 'Cash' ? 'selected' : ''}>Cash</option>
            </select>
            <input type="date" id="dDate" class="form-control" value="${data?.date || today}">
            <small class="text-muted mt-2">Event Name (if event donation):</small>
            <input type="text" id="dEventName" class="form-control mt-1" placeholder="Event name" value="${data?.eventName || ''}">
        `;
        const uidInput = document.getElementById('dUID');
        uidInput.oninput = async () => {
            const uid = uidInput.value.trim();
            if (uid) {
                const membersRef = collection(db, "members");
                const q = await import("https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js").then(m => m.query(membersRef, m.where("uid", "==", uid)));
                const snapshot = await import("https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js").then(m => m.getDocs(q));
                snapshot.forEach(doc => {
                    document.getElementById('dName').value = doc.data().name;
                });
            }
        };
        document.getElementById('saveBtn').onclick = async () => {
            const donationData = {
                uid: document.getElementById('dUID').value,
                name: document.getElementById('dName').value,
                amount: Number(document.getElementById('dAmount').value),
                type: document.getElementById('dType').value,
                system: document.getElementById('dSystem').value,
                date: document.getElementById('dDate').value,
                eventName: document.getElementById('dEventName').value || '',
                timestamp: new Date().toISOString()
            };
            if (data) await updateDoc(doc(db, "donations", data.id), donationData);
            else await addDoc(collection(db, "donations"), donationData);
            bsModal.hide();
        };
        bsModal.show();
    };

    window.openExpenseForm = (data = null) => {
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('modalTitle').innerText = data ? 'Edit Expense' : 'Add Expense';
        document.getElementById('modalBody').innerHTML = `
            <input type="text" id="eDesc" class="form-control mb-3" placeholder="Expense Description" value="${data?.description || ''}">
            <input type="number" id="eAmount" class="form-control mb-3" placeholder="Amount ($)" value="${data?.amount || ''}">
            <select id="eType" class="form-select mb-3">
                <option value="monthly" ${data?.type === 'monthly' ? 'selected' : ''}>Monthly Expense</option>
                <option value="event" ${data?.type === 'event' ? 'selected' : ''}>Event Expense</option>
            </select>
            <input type="date" id="eDate" class="form-control" value="${data?.date || today}">
            <small class="text-muted mt-2">Event Name (if event expense):</small>
            <input type="text" id="eEventName" class="form-control mt-1" placeholder="Event name" value="${data?.eventName || ''}">
        `;
        document.getElementById('saveBtn').onclick = async () => {
            const expenseData = {
                description: document.getElementById('eDesc').value,
                amount: Number(document.getElementById('eAmount').value),
                type: document.getElementById('eType').value,
                date: document.getElementById('eDate').value,
                eventName: document.getElementById('eEventName').value || '',
                timestamp: new Date().toISOString()
            };
            if (data) await updateDoc(doc(db, "expenses", data.id), expenseData);
            else await addDoc(collection(db, "expenses"), expenseData);
            bsModal.hide();
        };
        bsModal.show();
    };

    window.openEventForm = (data = null) => {
        document.getElementById('modalTitle').innerText = data ? 'Edit Event' : 'Plan Event';
        document.getElementById('modalBody').innerHTML = `
            <input type="text" id="evName" class="form-control mb-3" placeholder="Event Name" value="${data?.name || ''}">
            <input type="date" id="evDate" class="form-control mb-3" value="${data?.date || ''}">
            <input type="number" id="evBudget" class="form-control mb-3" placeholder="Budget ($)" value="${data?.budget || ''}">
            <textarea id="evDetails" class="form-control" rows="3" placeholder="Event Details">${data?.details || ''}</textarea>
        `;
        document.getElementById('saveBtn').onclick = async () => {
            const eventData = {
                name: document.getElementById('evName').value,
                date: document.getElementById('evDate').value,
                budget: Number(document.getElementById('evBudget').value),
                details: document.getElementById('evDetails').value,
                status: data?.status || 'Planned',
                fund: data?.fund || 0,
                cost: data?.cost || 0
            };
            if (data) await updateDoc(doc(db, "events", data.id), eventData);
            else await addDoc(collection(db, "events"), eventData);
            bsModal.hide();
        };
        bsModal.show();
    };

    window.executeEvent = async (eventData) => {
        const fund = prompt("Enter fund raised for this event ($):", eventData.fund || "0");
        const cost = prompt("Enter actual expenses for this event ($):", eventData.cost || "0");
        if (fund !== null && cost !== null) {
            await updateDoc(doc(db, "events", eventData.id), {
                status: "Executed",
                fund: Number(fund),
                cost: Number(cost)
            });
        }
    };

    window.deleteItem = async (collectionName, id) => {
        if (confirm("Delete this entry?")) {
            await deleteDoc(doc(db, collectionName, id));
        }
    };

    // Real-time data listeners
    let totalFunds = 0, monthlyFunds = 0, eventFunds = 0;
    let totalExpensesAmount = 0, monthlyExpensesAmount = 0;

    const currentMonth = new Date().getMonth();
    const currentYear = new Date().getFullYear();

    function isCurrentMonth(dateStr) {
        if (!dateStr) return false;
        const date = new Date(dateStr);
        return date.getMonth() === currentMonth && date.getFullYear() === currentYear;
    }

    // Donations Listener
    onSnapshot(collection(db, "donations"), (snap) => {
        totalFunds = 0;
        monthlyFunds = 0;
        eventFunds = 0;
        
        let html = `<table><thead><tr><th>Date</th><th>Member</th><th>Amount</th><th>Type</th><th>Method</th><th>Action</th></tr></thead><tbody>`;
        
        snap.forEach(doc => {
            const d = doc.data();
            totalFunds += d.amount;
            if (d.type === 'monthly') {
                monthlyFunds += d.amount;
                if (isCurrentMonth(d.date)) monthlyFunds += d.amount;
            } else if (d.type === 'event') {
                eventFunds += d.amount;
            }
            
            const typeBadge = d.type === 'monthly' ? '<span class="badge-add badge">Monthly</span>' : '<span class="badge-add badge">Event</span>';
            html += `<tr>
                <td>${d.date || '-'}</td>
                <td>${d.uid || 'Guest'}<br><small>${d.name || ''}</small></td>
                <td class="text-success">$${d.amount}</td>
                <td>${typeBadge}${d.eventName ? `<br><small>${d.eventName}</small>` : ''}</td>
                <td>${d.system || '-'}</td>
                <td><button class="btn btn-sm btn-outline-warning me-1" onclick='openDonationForm(${JSON.stringify({id:doc.id,...d})})'>Edit</button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('donations','${doc.id}')">Del</button></td>
            </tr>`;
        });
        
        html += `</tbody></table>`;
        document.getElementById('donationList').innerHTML = html || '<p>No donations yet</p>';
        document.getElementById('totalFund').innerHTML = `$${totalFunds}`;
        document.getElementById('monthlyCollection').innerHTML = `$${monthlyFunds}`;
        document.getElementById('eventFundCollection').innerHTML = `$${eventFunds}`;
        
        document.getElementById('netBalance').innerHTML = `$${totalFunds - totalExpensesAmount}`;
    });

    // Expenses Listener
    onSnapshot(collection(db, "expenses"), (snap) => {
        totalExpensesAmount = 0;
        monthlyExpensesAmount = 0;
        
        let html = `<table><thead><tr><th>Date</th><th>Description</th><th>Amount</th><th>Type</th><th>Action</th></tr></thead><tbody>`;
        
        snap.forEach(doc => {
            const e = doc.data();
            totalExpensesAmount += e.amount;
            if (e.type === 'monthly' && isCurrentMonth(e.date)) {
                monthlyExpensesAmount += e.amount;
            }
            if (e.type === 'event') {
                // Event expenses count towards total
            }
            
            const typeBadge = e.type === 'monthly' ? '<span class="badge-subtract badge">Monthly</span>' : '<span class="badge-subtract badge">Event</span>';
            html += `<tr>
                <td>${e.date || '-'}</td>
                <td>${e.description}${e.eventName ? `<br><small>${e.eventName}</small>` : ''}</td>
                <td class="text-danger">$${e.amount}</td>
                <td>${typeBadge}</td>
                <td><button class="btn btn-sm btn-outline-warning me-1" onclick='openExpenseForm(${JSON.stringify({id:doc.id,...e})})'>Edit</button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('expenses','${doc.id}')">Del</button></td>
            </tr>`;
        });
        
        html += `</tbody></table>`;
        document.getElementById('expenseList').innerHTML = html || '<p>No expenses yet</p>';
        document.getElementById('monthlyExpenses').innerHTML = `$${monthlyExpensesAmount}`;
        document.getElementById('totalExpenses').innerHTML = `$${totalExpensesAmount}`;
        document.getElementById('netBalance').innerHTML = `$${totalFunds - totalExpensesAmount}`;
    });

    // Members Listener
    onSnapshot(collection(db, "members"), (snap) => {
        let html = `<table><thead><tr><th>ID</th><th>Name</th><th>Designation</th><th>Blood</th><th>Contact</th><th>Action</th></tr></thead><tbody>`;
        snap.forEach(doc => {
            const m = doc.data();
            html += `<tr>
                <td class="text-gold">${m.uid || '-'}</td>
                <td>${m.name}</td>
                <td>${m.designation || '-'}</td>
                <td><span class="badge bg-danger">${m.blood || '-'}</span></td>
                <td>${m.phone}<br><small>${m.email}</small></td>
                <td><button class="btn btn-sm btn-outline-warning me-1" onclick='openMemberForm(${JSON.stringify({id:doc.id,...m})})'>Edit</button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('members','${doc.id}')">Del</button></td>
            </tr>`;
        });
        html += `</tbody></table>`;
        document.getElementById('memberList').innerHTML = html || '<p>No members yet</p>';
    });

    // Events Listener
    onSnapshot(collection(db, "events"), (snap) => {
        let planningHtml = `<table><thead><tr><th>Event</th><th>Date</th><th>Budget</th><th>Action</th></tr></thead><tbody>`;
        let executedHtml = `<table><thead><tr><th>Event</th><th>Budget</th><th>Raised</th><th>Cost</th><th>Result</th><th>Action</th></tr></thead><tbody>`;
        
        snap.forEach(doc => {
            const e = doc.data();
            if (e.status === 'Planned' || !e.status) {
                planningHtml += `<tr>
                    <td><strong>${e.name}</strong><br><small>${e.details || ''}</small></td>
                    <td>${e.date || '-'}</td>
                    <td>$${e.budget || 0}</td>
                    <td><button class="btn btn-sm btn-success me-1" onclick='executeEvent(${JSON.stringify({id:doc.id,...e})})'>Execute</button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('events','${doc.id}')">Del</button></td>
                </tr>`;
            } else if (e.status === 'Executed') {
                const profit = (e.fund || 0) - (e.cost || 0);
                executedHtml += `<tr>
                    <td><strong>${e.name}</strong></td>
                    <td>$${e.budget || 0}</td>
                    <td class="text-success">$${e.fund || 0}</td>
                    <td class="text-danger">$${e.cost || 0}</td>
                    <td><span class="${profit >= 0 ? 'text-success' : 'text-danger'}">$${profit}</span></td>
                    <td><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('events','${doc.id}')">Del</button></td>
                </tr>`;
            }
        });
        
        planningHtml += `</tbody></table>`;
        executedHtml += `</tbody></table>`;
        document.getElementById('planningList').innerHTML = planningHtml || '<p>No planned events</p>';
        document.getElementById('executedList').innerHTML = executedHtml || '<p>No executed events</p>';
    });
</script>

</body>
</html>
