
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>IYSO প্রিমিয়াম ড্যাশবোর্ড | আইডিয়াল যুব সেবা সংস্থা</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        :root {
            --green: #006837;
            --gold: #c6a34f;
            --dark-green: #004d2e;
            --dark-red: #8b0000;
            --bg: #0a0f14;
            --card: rgba(18, 25, 32, 0.95);
            --pink: #e2136e;
            --orange: #f7941d;
            --success-green: #2ecc71;
            --danger-red: #e74c3c;
            --warning-yellow: #f39c12;
            --table-bg: rgba(0, 0, 0, 0.6);
            --table-hover: rgba(255, 255, 255, 0.08);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #0a1a0f 0%, #0a0f14 100%);
            color: #fff;
            font-family: 'Hind Siliguri', 'Inter', sans-serif;
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
        }

        /* Background Watermark */
        body::before {
            content: "";
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('image_0.png') center/contain no-repeat;
            opacity: 0.04;
            pointer-events: none;
            z-index: 0;
        }

        /* Premium Sidebar - Responsive */
        .sidebar {
            width: 280px;
            height: 100vh;
            position: fixed;
            background: rgba(0, 0, 0, 0.75);
            backdrop-filter: blur(20px);
            padding: 25px 15px;
            border-right: 1px solid rgba(255,255,255,0.08);
            z-index: 100;
            transition: all 0.3s ease;
            overflow-y: auto;
        }

        @media (max-width: 768px) {
            .sidebar {
                transform: translateX(-100%);
                width: 260px;
                z-index: 1000;
                transition: transform 0.3s ease;
            }
            .sidebar.open {
                transform: translateX(0);
            }
            .main {
                margin-left: 0 !important;
                padding: 15px !important;
            }
            .menu-toggle {
                display: block !important;
                position: fixed;
                top: 15px;
                left: 15px;
                z-index: 1001;
                background: var(--green);
                border: none;
                color: white;
                padding: 10px 15px;
                border-radius: 8px;
                cursor: pointer;
            }
            .net-balance-amount {
                font-size: 40px !important;
            }
            .small-card-amount {
                font-size: 22px !important;
            }
            .stat {
                font-size: 24px;
            }
        }

        @media (min-width: 769px) {
            .menu-toggle {
                display: none;
            }
        }

        @media (max-width: 480px) {
            .main {
                padding: 10px !important;
            }
            .glass-card {
                padding: 15px !important;
            }
            .net-balance-card {
                padding: 20px !important;
            }
            .net-balance-amount {
                font-size: 32px !important;
            }
            .small-card-amount {
                font-size: 18px !important;
            }
            .data-table {
                font-size: 12px;
            }
            .data-table th, .data-table td {
                padding: 8px !important;
            }
            .money-numbers {
                margin-top: 15px;
            }
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
            position: relative;
            font-family: 'Hind Siliguri', sans-serif;
        }

        .logo::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 50px;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--gold), transparent);
        }

        .nav-item {
            padding: 12px 16px;
            margin: 6px 0;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            color: rgba(255,255,255,0.8);
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 12px;
            position: relative;
            overflow: hidden;
            font-family: 'Hind Siliguri', sans-serif;
            font-size: 16px;
        }

        .nav-item i {
            width: 24px;
            font-size: 18px;
        }

        .nav-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
            transition: left 0.5s;
        }

        .nav-item:hover::before {
            left: 100%;
        }

        .nav-item:hover {
            background: rgba(0, 104, 55, 0.3);
            color: white;
            transform: translateX(5px);
        }

        .nav-item.active {
            background: linear-gradient(135deg, var(--green), var(--dark-green));
            color: white;
            box-shadow: 0 4px 15px rgba(0,104,55,0.4);
        }

        /* Main Content */
        .main {
            margin-left: 280px;
            padding: 25px 30px;
            position: relative;
            z-index: 1;
            transition: margin-left 0.3s ease;
        }

        /* Glass Card Effect */
        .glass-card {
            background: var(--card);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 20px;
            border: 1px solid rgba(255,255,255,0.08);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            height: 100%;
        }

        .glass-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
        }

        /* Net Balance */
        .net-balance-card {
            background: linear-gradient(135deg, rgba(0,104,55,0.25) 0%, rgba(0,77,46,0.5) 100%);
            backdrop-filter: blur(10px);
            border-radius: 28px;
            padding: 30px;
            border: 2px solid rgba(198,163,79,0.3);
            text-align: center;
            box-shadow: 0 20px 40px rgba(0,0,0,0.4);
            animation: glow 2s ease-in-out infinite;
        }

        @keyframes glow {
            0%, 100% { box-shadow: 0 20px 40px rgba(0,0,0,0.4); }
            50% { box-shadow: 0 20px 60px rgba(198,163,79,0.2); }
        }

        .net-balance-label {
            font-size: 16px;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: var(--gold);
            margin-bottom: 15px;
            font-family: 'Hind Siliguri', sans-serif;
        }

        .net-balance-amount {
            font-size: 64px;
            font-weight: 800;
            background: linear-gradient(135deg, var(--gold) 0%, #ffd700 100%);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            line-height: 1.2;
        }

        /* Small Cards */
        .small-card {
            padding: 18px;
        }

        .small-card-title {
            font-size: 12px;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            color: rgba(255,255,255,0.5);
            margin-bottom: 10px;
            font-family: 'Hind Siliguri', sans-serif;
        }

        .small-card-amount {
            font-size: 26px;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .month-name {
            font-size: 11px;
            color: var(--gold);
            margin-top: 5px;
            font-family: 'Hind Siliguri', sans-serif;
        }

        /* Money Numbers */
        .money-numbers {
            background: rgba(0,0,0,0.5);
            border-radius: 16px;
            padding: 12px;
            border: 1px solid rgba(255,255,255,0.1);
        }

        .bkash-box {
            background: linear-gradient(135deg, var(--pink), #c40e5e);
            border-radius: 12px;
            padding: 10px 14px;
            margin-bottom: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            animation: slideIn 0.5s ease;
        }

        .nagad-box {
            background: linear-gradient(135deg, var(--orange), #e67e00);
            border-radius: 12px;
            padding: 10px 14px;
            cursor: pointer;
            transition: all 0.3s ease;
            animation: slideIn 0.5s ease 0.1s;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateX(20px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .bkash-box:hover, .nagad-box:hover {
            transform: scale(1.02);
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .send-number {
            font-size: 16px;
            font-weight: 700;
            letter-spacing: 1px;
            direction: ltr;
        }

        /* Tables - Enhanced Visibility */
        .data-table {
            background: var(--table-bg);
            border-radius: 16px;
            overflow-x: auto;
            backdrop-filter: blur(5px);
        }

        .data-table table {
            width: 100%;
            min-width: 500px;
        }

        .data-table th {
            padding: 14px 12px;
            border-bottom: 1px solid rgba(255,255,255,0.2);
            color: var(--gold) !important;
            font-weight: 700;
            background: rgba(0, 0, 0, 0.5);
            font-size: 14px;
            font-family: 'Hind Siliguri', sans-serif;
        }

        .data-table td {
            padding: 12px;
            border-bottom: 1px solid rgba(255,255,255,0.08);
            color: #f0f0f0 !important;
            font-size: 14px;
            background: transparent;
        }

        .data-table tr {
            transition: background 0.2s ease;
        }

        .data-table tr:hover {
            background: var(--table-hover) !important;
        }

        /* Badges */
        .badge-add {
            background: var(--dark-green);
            color: #a8e6cf;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
        }

        .badge-subtract {
            background: var(--dark-red);
            color: #ffb3b3;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
        }

        /* Event Status Badges */
        .status-success {
            background: var(--success-green);
            color: white;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
        }

        .status-failed {
            background: var(--danger-red);
            color: white;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
        }

        .status-pending {
            background: var(--warning-yellow);
            color: #333;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
        }

        /* Modal */
        .modal-content {
            background: linear-gradient(135deg, #1a1f24, #0f1419);
            border: 1px solid var(--green);
            border-radius: 20px;
        }

        .form-control, .form-select {
            background: #2a2f35;
            border: 1px solid #3a3f45;
            color: white;
            font-family: 'Hind Siliguri', sans-serif;
        }

        .form-control:focus, .form-select:focus {
            background: #2a2f35;
            color: white;
            border-color: var(--green);
            box-shadow: 0 0 0 0.2rem rgba(0,104,55,0.25);
        }

        .btn-success {
            background: var(--green);
            border: none;
        }

        .btn-success:hover {
            background: var(--dark-green);
            transform: translateY(-2px);
        }

        /* Footer Glowing Texts */
        .footer-text {
            text-align: center;
            padding: 20px 0 10px;
            margin-top: 30px;
            border-top: 1px solid rgba(255,255,255,0.1);
        }

        .glowing-text {
            font-size: 12px;
            color: var(--gold);
            text-align: center;
            animation: textGlow 1.5s ease-in-out infinite;
            font-family: 'Hind Siliguri', sans-serif;
            letter-spacing: 1px;
        }

        .creator-text {
            font-size: 11px;
            color: rgba(198, 163, 79, 0.8);
            text-align: right;
            margin-top: 10px;
            animation: textGlow 2s ease-in-out infinite;
            font-family: 'Hind Siliguri', sans-serif;
        }

        @keyframes textGlow {
            0%, 100% {
                text-shadow: 0 0 5px rgba(198, 163, 79, 0.3);
                opacity: 0.8;
            }
            50% {
                text-shadow: 0 0 15px rgba(198, 163, 79, 0.6);
                opacity: 1;
            }
        }

        /* Tabs */
        .nav-tabs {
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .nav-tabs .nav-link {
            color: rgba(255,255,255,0.6);
            border: none;
            font-weight: 600;
            font-family: 'Hind Siliguri', sans-serif;
        }

        .nav-tabs .nav-link.active {
            color: var(--gold);
            background: transparent;
            border-bottom: 2px solid var(--gold);
        }

        /* Utility */
        .text-gold { color: var(--gold); }
        .text-dark-green { color: #a8e6cf; }
        .text-dark-red { color: #ffb3b3; }

        /* Animations */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .page {
            animation: fadeInUp 0.4s ease;
        }

        button {
            transition: all 0.3s ease;
        }

        button:active {
            transform: scale(0.95);
        }

        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        ::-webkit-scrollbar-track {
            background: rgba(0,0,0,0.3);
            border-radius: 10px;
        }

        ::-webkit-scrollbar-thumb {
            background: var(--green);
            border-radius: 10px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--gold);
        }

        .row {
            margin-right: 0;
            margin-left: 0;
        }
    </style>
</head>
<body>

<button class="menu-toggle" onclick="toggleSidebar()">
    <i class="fas fa-bars"></i>
</button>

<div class="sidebar" id="sidebar">
    <div class="logo">IYSO</div>
    <div class="nav-item active" data-page="dash">
        <i class="fas fa-chart-line"></i>
        <span>ড্যাশবোর্ড</span>
    </div>
    <div class="nav-item" data-page="members">
        <i class="fas fa-users"></i>
        <span>সদস্যবৃন্দ</span>
    </div>
    <div class="nav-item" data-page="donations">
        <i class="fas fa-hand-holding-usd"></i>
        <span>দান-অনুদান</span>
    </div>
    <div class="nav-item" data-page="expenses">
        <i class="fas fa-chart-line"></i>
        <span>খরচের তালিকা</span>
    </div>
    <div class="nav-item" data-page="events">
        <i class="fas fa-calendar-alt"></i>
        <span>ইভেন্ট সমূহ</span>
    </div>
</div>

<div class="main">
    <!-- Dashboard Page -->
    <div id="dash" class="page">
        <div class="row mb-4">
            <div class="col-lg-9 col-md-8 col-12">
                <div class="net-balance-card">
                    <div class="net-balance-label">নেট ব্যালেন্স</div>
                    <div class="net-balance-amount" id="netBalance">৳0</div>
                </div>
            </div>
            <div class="col-lg-3 col-md-4 col-12">
                <div class="money-numbers">
                    <div class="bkash-box" onclick="editSendNumber('bkash')">
                        <div style="font-size: 11px; opacity: 0.9;"><i class="fas fa-mobile-alt"></i> বিকাশ (সেন্ড মানি)</div>
                        <div class="send-number" id="bkashNumber">017XXXXXXXX</div>
                    </div>
                    <div class="nagad-box" onclick="editSendNumber('nagad')">
                        <div style="font-size: 11px; opacity: 0.9;"><i class="fas fa-mobile-alt"></i> নগদ (সেন্ড মানি)</div>
                        <div class="send-number" id="nagadNumber">017XXXXXXXX</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="row g-3 mb-4">
            <div class="col-md-4 col-sm-6 col-12">
                <div class="glass-card small-card">
                    <div class="small-card-title"><i class="fas fa-donate"></i> মোট সংগ্রহ</div>
                    <div class="small-card-amount" id="totalFund">৳0</div>
                    <div class="month-name">সর্বমোট সংগ্রহ</div>
                </div>
            </div>
            <div class="col-md-4 col-sm-6 col-12">
                <div class="glass-card small-card">
                    <div class="small-card-title"><i class="fas fa-calendar-week"></i> চলতি মাসের সংগ্রহ</div>
                    <div class="small-card-amount" id="monthlyCollection">৳0</div>
                    <div class="month-name" id="currentMonthName">জানুয়ারি ২০২৪</div>
                </div>
            </div>
            <div class="col-md-4 col-sm-6 col-12">
                <div class="glass-card small-card">
                    <div class="small-card-title"><i class="fas fa-trophy"></i> ইভেন্ট ফান্ড</div>
                    <div class="small-card-amount" id="eventFundCollection">৳0</div>
                    <div class="month-name" id="eventMonthName">ইভেন্ট সংগ্রহ</div>
                </div>
            </div>
        </div>

        <div class="row g-3">
            <div class="col-md-6 col-12">
                <div class="glass-card small-card">
                    <div class="small-card-title"><i class="fas fa-arrow-down"></i> চলতি মাসের খরচ</div>
                    <div class="small-card-amount" id="monthlyExpenses">৳0</div>
                    <div class="month-name" id="expenseMonthName">চলতি মাসের খরচ</div>
                </div>
            </div>
            <div class="col-md-6 col-12">
                <div class="glass-card small-card">
                    <div class="small-card-title"><i class="fas fa-chart-pie"></i> মোট খরচ</div>
                    <div class="small-card-amount" id="totalExpenses">৳0</div>
                    <div class="month-name">সর্বমোট খরচ</div>
                </div>
            </div>
        </div>
    </div>

    <!-- Members Page -->
    <div id="members" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-2">
            <h3><i class="fas fa-users text-gold"></i> সদস্যবৃন্দ</h3>
            <button onclick="openMemberForm()" class="btn btn-success px-4"><i class="fas fa-plus"></i> নতুন সদস্য</button>
        </div>
        <div class="data-table" id="memberList">লোড হচ্ছে...</div>
    </div>

    <!-- Donations Page -->
    <div id="donations" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-2">
            <h3><i class="fas fa-hand-holding-usd text-gold"></i> দান-অনুদানের তালিকা</h3>
            <button onclick="openDonationForm()" class="btn btn-success px-4"><i class="fas fa-plus"></i> নতুন দান</button>
        </div>
        <div class="data-table" id="donationList">লোড হচ্ছে...</div>
    </div>

    <!-- Expenses Page -->
    <div id="expenses" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-2">
            <h3><i class="fas fa-chart-line text-gold"></i> খরচের তালিকা</h3>
            <button onclick="openExpenseForm()" class="btn btn-danger px-4"><i class="fas fa-plus"></i> নতুন খরচ</button>
        </div>
        <div class="data-table" id="expenseList">লোড হচ্ছে...</div>
    </div>

    <!-- Events Page -->
    <div id="events" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-2">
            <h3><i class="fas fa-calendar-alt text-gold"></i> ইভেন্ট প্ল্যানিং</h3>
            <button onclick="openEventForm()" class="btn btn-success px-4"><i class="fas fa-plus"></i> নতুন ইভেন্ট</button>
        </div>
        <div class="data-table" id="planningList">লোড হচ্ছে...</div>
    </div>

    <!-- Footer -->
    <div class="footer-text">
        <div class="glowing-text">আইডিয়াল যুব সেবা সংস্থা</div>
        <div class="creator-text">Created by Nahidul Islam</div>
    </div>
</div>

<!-- Modal -->
<div class="modal fade" id="dataModal" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
        <div class="modal-content">
            <div class="modal-header border-0">
                <h5 class="modal-title" id="modalTitle">ফর্ম</h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body" id="modalBody"></div>
            <div class="modal-footer border-0">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">বাতিল</button>
                <button type="button" class="btn btn-success" id="saveBtn">সংরক্ষণ</button>
            </div>
        </div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, deleteDoc, doc, updateDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "YOUR_KEY",
        projectId: "iyso-web"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    const bsModal = new bootstrap.Modal(document.getElementById('dataModal'));

    // Sidebar Toggle for Mobile
    window.toggleSidebar = () => {
        document.getElementById('sidebar').classList.toggle('open');
    };

    // Close sidebar when clicking outside on mobile
    document.addEventListener('click', (e) => {
        const sidebar = document.getElementById('sidebar');
        const toggleBtn = document.querySelector('.menu-toggle');
        if (window.innerWidth <= 768 && sidebar.classList.contains('open')) {
            if (!sidebar.contains(e.target) && !toggleBtn.contains(e.target)) {
                sidebar.classList.remove('open');
            }
        }
    });

    // Navigation
    document.querySelectorAll('.nav-item').forEach(item => {
        item.onclick = () => {
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            item.classList.add('active');
            document.querySelectorAll('.page').forEach(p => p.style.display = 'none');
            const pageId = document.getElementById(item.dataset.page);
            pageId.style.display = 'block';
            pageId.style.animation = 'none';
            setTimeout(() => pageId.style.animation = 'fadeInUp 0.4s ease', 10);
            if (window.innerWidth <= 768) {
                document.getElementById('sidebar').classList.remove('open');
            }
        };
    });

    // Get current month in Bangla
    function getCurrentMonthBangla() {
        const months = ['জানুয়ারি', 'ফেব্রুয়ারি', 'মার্চ', 'এপ্রিল', 'মে', 'জুন', 'জুলাই', 'আগস্ট', 'সেপ্টেম্বর', 'অক্টোবর', 'নভেম্বর', 'ডিসেম্বর'];
        const now = new Date();
        return `${months[now.getMonth()]} ${now.getFullYear()}`;
    }

    // Send numbers
    let bkashNumber = localStorage.getItem('bkashNumber') || '017XXXXXXXX';
    let nagadNumber = localStorage.getItem('nagadNumber') || '017XXXXXXXX';
    document.getElementById('bkashNumber').innerText = bkashNumber;
    document.getElementById('nagadNumber').innerText = nagadNumber;
    document.getElementById('currentMonthName').innerText = getCurrentMonthBangla();
    document.getElementById('expenseMonthName').innerText = getCurrentMonthBangla();
    document.getElementById('eventMonthName').innerText = 'ইভেন্ট সংগ্রহ';

    window.editSendNumber = (type) => {
        const newNumber = prompt(`${type.toUpperCase()} সেন্ড মানি নম্বর দিন:`, type === 'bkash' ? bkashNumber : nagadNumber);
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

    // Member Form
    window.openMemberForm = (data = null) => {
        document.getElementById('modalTitle').innerHTML = data ? '<i class="fas fa-edit"></i> সদস্য সম্পাদনা' : '<i class="fas fa-user-plus"></i> নতুন সদস্য';
        document.getElementById('modalBody').innerHTML = `
            <input type="text" id="mUID" class="form-control mb-3" placeholder="সদস্য আইডি" value="${data?.uid || ''}">
            <input type="text" id="mName" class="form-control mb-3" placeholder="পুরো নাম" value="${data?.name || ''}">
            <input type="text" id="mDesignation" class="form-control mb-3" placeholder="পদবি" value="${data?.designation || ''}">
            <select id="mBlood" class="form-select mb-3">
                <option value="">ব্লাড গ্রুপ</option>
                ${['A+','A-','B+','B-','O+','O-','AB+','AB-'].map(b => `<option value="${b}" ${data?.blood === b ? 'selected' : ''}>${b}</option>`).join('')}
            </select>
            <input type="text" id="mPhone" class="form-control mb-3" placeholder="ফোন নম্বর" value="${data?.phone || ''}">
            <input type="email" id="mEmail" class="form-control" placeholder="ইমেইল" value="${data?.email || ''}">
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

    // Donation Form
    window.openDonationForm = (data = null) => {
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('modalTitle').innerHTML = data ? '<i class="fas fa-edit"></i> দান সম্পাদনা' : '<i class="fas fa-plus"></i> নতুন দান';
        document.getElementById('modalBody').innerHTML = `
            <input type="text" id="dUID" class="form-control mb-3" placeholder="সদস্য আইডি" value="${data?.uid || ''}">
            <input type="text" id="dName" class="form-control mb-3" placeholder="সদস্যের নাম" value="${data?.name || ''}" readonly style="background:#1a1f24">
            <input type="number" id="dAmount" class="form-control mb-3" placeholder="পরিমাণ (টাকা)" value="${data?.amount || ''}">
            <select id="dType" class="form-select mb-3">
                <option value="monthly" ${data?.type === 'monthly' ? 'selected' : ''}>মাসিক চাঁদা</option>
                <option value="event" ${data?.type === 'event' ? 'selected' : ''}>ইভেন্ট দান</option>
            </select>
            <select id="dSystem" class="form-select mb-3">
                <option value="">পেমেন্ট পদ্ধতি</option>
                <option value="Bkash" ${data?.system === 'Bkash' ? 'selected' : ''}>বিকাশ</option>
                <option value="Nagad" ${data?.system === 'Nagad' ? 'selected' : ''}>নগদ</option>
                <option value="Cash" ${data?.system === 'Cash' ? 'selected' : ''}>নগদ</option>
            </select>
            <input type="date" id="dDate" class="form-control" value="${data?.date || today}">
            <input type="text" id="dEventName" class="form-control mt-3" placeholder="ইভেন্টের নাম (যদি ইভেন্ট দান হয়)" value="${data?.eventName || ''}">
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

    // Expense Form
    window.openExpenseForm = (data = null) => {
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('modalTitle').innerHTML = data ? '<i class="fas fa-edit"></i> খরচ সম্পাদনা' : '<i class="fas fa-plus"></i> নতুন খরচ';
        document.getElementById('modalBody').innerHTML = `
            <input type="text" id="eDesc" class="form-control mb-3" placeholder="খরচের বিবরণ" value="${data?.description || ''}">
            <input type="number" id="eAmount" class="form-control mb-3" placeholder="পরিমাণ (টাকা)" value="${data?.amount || ''}">
            <select id="eType" class="form-select mb-3">
                <option value="monthly" ${data?.type === 'monthly' ? 'selected' : ''}>মাসিক খরচ</option>
                <option value="event" ${data?.type === 'event' ? 'selected' : ''}>ইভেন্ট খরচ</option>
            </select>
            <input type="date" id="eDate" class="form-control" value="${data?.date || today}">
            <input type="text" id="eEventName" class="form-control mt-3" placeholder="ইভেন্টের নাম (যদি ইভেন্ট খরচ হয়)" value="${data?.eventName || ''}">
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

    // Event Form
    window.openEventForm = (data = null) => {
        document.getElementById('modalTitle').innerHTML = data ? '<i class="fas fa-edit"></i> ইভেন্ট সম্পাদনা' : '<i class="fas fa-calendar-plus"></i> নতুন ইভেন্ট';
        document.getElementById('modalBody').innerHTML = `
            <input type="text" id="evName" class="form-control mb-3" placeholder="ইভেন্টের নাম" value="${data?.name || ''}">
            <input type="date" id="evDate" class="form-control mb-3" value="${data?.date || ''}">
            <input type="number" id="evBudget" class="form-control mb-3" placeholder="বাজেট (টাকা)" value="${data?.budget || ''}">
            <select id="evStatus" class="form-select mb-3">
                <option value="pending" ${data?.status === 'pending' || !data?.status ? 'selected' : ''}>🟡 পেন্ডিং</option>
                <option value="successful" ${data?.status === 'successful' ? 'selected' : ''}>🟢 সফল</option>
                <option value="failed" ${data?.status === 'failed' ? 'selected' : ''}>🔴 ব্যর্থ</option>
            </select>
            <textarea id="evDetails" class="form-control" rows="3" placeholder="ইভেন্টের বিবরণ">${data?.details || ''}</textarea>
            ${data?.status === 'successful' ? `
                <div class="mt-3 p-3 border border-success rounded">
                    <label>সংগৃহীত তহবিল (টাকা)</label>
                    <input type="number" id="evFund" class="form-control mt-1" value="${data?.fund || 0}">
                    <label class="mt-2">আসল খরচ (টাকা)</label>
                    <input type="number" id="evCost" class="form-control mt-1" value="${data?.cost || 0}">
                </div>
            ` : ''}
        `;
        
        const statusSelect = document.getElementById('evStatus');
        if (statusSelect) {
            statusSelect.onchange = () => {
                const body = document.getElementById('modalBody');
                const existingFund = data?.fund || 0;
                const existingCost = data?.cost || 0;
                if (statusSelect.value === 'successful') {
                    if (!document.getElementById('evFund')) {
                        const div = document.createElement('div');
                        div.className = 'mt-3 p-3 border border-success rounded';
                        div.innerHTML = `
                            <label>সংগৃহীত তহবিল (টাকা)</label>
                            <input type="number" id="evFund" class="form-control mt-1" value="${existingFund}">
                            <label class="mt-2">আসল খরচ (টাকা)</label>
                            <input type="number" id="evCost" class="form-control mt-1" value="${existingCost}">
                        `;
                        body.appendChild(div);
                    }
                } else {
                    const fundDiv = document.getElementById('evFund')?.parentElement;
                    if (fundDiv && fundDiv.parentElement === body) fundDiv.remove();
                }
            };
        }
        
        document.getElementById('saveBtn').onclick = async () => {
            const eventData = {
                name: document.getElementById('evName').value,
                date: document.getElementById('evDate').value,
                budget: Number(document.getElementById('evBudget').value),
                status: document.getElementById('evStatus').value,
                details: document.getElementById('evDetails').value,
                fund: document.getElementById('evFund') ? Number(document.getElementById('evFund').value) : (data?.fund || 0),
                cost: document.getElementById('evCost') ? Number(document.getElementById('evCost').value) : (data?.cost || 0)
            };
            if (data) await updateDoc(doc(db, "events", data.id), eventData);
            else await addDoc(collection(db, "events"), eventData);
            bsModal.hide();
        };
        bsModal.show();
    };

    window.deleteItem = async (collectionName, id) => {
        if (confirm("এই এন্ট্রি ডিলিট করবেন?")) {
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
        
        let html = `<table class="table"><thead><tr><th>তারিখ</th><th>সদস্য</th><th>পরিমাণ</th><th>ধরন</th><th>পদ্ধতি</th><th>অ্যাকশন</th></tr></thead><tbody>`;
        
        snap.forEach(doc => {
            const d = doc.data();
            totalFunds += d.amount;
            if (d.type === 'monthly') {
                if (isCurrentMonth(d.date)) monthlyFunds += d.amount;
            } else if (d.type === 'event') {
                eventFunds += d.amount;
            }
            
            const typeBadge = d.type === 'monthly' ? '<span class="badge-add">মাসিক</span>' : '<span class="badge-add">ইভেন্ট</span>';
            html += `<tr>
                <td style="color:#ddd">${d.date || '-'}</td>
                <td style="color:#fff"><strong>${d.uid || 'অতিথি'}</strong><br><small>${d.name || ''}</small></td>
                <td style="color:#a8e6cf; font-weight:bold">৳${d.amount}</td>
                <td>${typeBadge}${d.eventName ? `<br><small>${d.eventName}</small>` : ''}</td>
                <td style="color:#ddd">${d.system || '-'}</td>
                <td><button class="btn btn-sm btn-outline-warning me-1" onclick='openDonationForm(${JSON.stringify({id:doc.id,...d})})'><i class="fas fa-edit"></i></button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('donations','${doc.id}')"><i class="fas fa-trash"></i></button></td>
            </tr>`;
        });
        
        html += `</tbody></table>`;
        document.getElementById('donationList').innerHTML = html || '<p class="text-muted p-3">কোন দান নেই</p>';
        document.getElementById('totalFund').innerHTML = `৳${totalFunds}`;
        document.getElementById('monthlyCollection').innerHTML = `৳${monthlyFunds}`;
        document.getElementById('eventFundCollection').innerHTML = `৳${eventFunds}`;
        document.getElementById('netBalance').innerHTML = `৳${totalFunds - totalExpensesAmount}`;
    });

    // Expenses Listener
    onSnapshot(collection(db, "expenses"), (snap) => {
        totalExpensesAmount = 0;
        monthlyExpensesAmount = 0;
        
        let html = `<table class="table"><thead><tr><th>তারিখ</th><th>বিবরণ</th><th>পরিমাণ</th><th>ধরন</th><th>অ্যাকশন</th></tr></thead><tbody>`;
        
        snap.forEach(doc => {
            const e = doc.data();
            totalExpensesAmount += e.amount;
            if (e.type === 'monthly' && isCurrentMonth(e.date)) {
                monthlyExpensesAmount += e.amount;
            }
            
            const typeBadge = e.type === 'monthly' ? '<span class="badge-subtract">মাসিক</span>' : '<span class="badge-subtract">ইভেন্ট</span>';
            html += `<tr>
                <td style="color:#ddd">${e.date || '-'}</td>
                <td style="color:#fff">${e.description}${e.eventName ? `<br><small>${e.eventName}</small>` : ''}</td>
                <td style="color:#ffb3b3; font-weight:bold">৳${e.amount}</td>
                <td>${typeBadge}</td>
                <td><button class="btn btn-sm btn-outline-warning me-1" onclick='openExpenseForm(${JSON.stringify({id:doc.id,...e})})'><i class="fas fa-edit"></i></button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('expenses','${doc.id}')"><i class="fas fa-trash"></i></button></td>
            </tr>`;
        });
        
        html += `</tbody></table>`;
        document.getElementById('expenseList').innerHTML = html || '<p class="text-muted p-3">কোন খরচ নেই</p>';
        document.getElementById('monthlyExpenses').innerHTML = `৳${monthlyExpensesAmount}`;
        document.getElementById('totalExpenses').innerHTML = `৳${totalExpensesAmount}`;
        document.getElementById('netBalance').innerHTML = `৳${totalFunds - totalExpensesAmount}`;
    });

    // Members Listener
    onSnapshot(collection(db, "members"), (snap) => {
        let html = `<table class="table"><thead><tr><th>আইডি</th><th>নাম</th><th>পদবি</th><th>ব্লাড</th><th>যোগাযোগ</th><th>অ্যাকশন</th></tr></thead><tbody>`;
        snap.forEach(doc => {
            const m = doc.data();
            html += `<tr>
                <td style="color:#c6a34f; font-weight:bold">${m.uid || '-'}</td>
                <td style="color:#fff">${m.name}</td>
                <td style="color:#fff">${m.designation || '-'}</td>
                <td><span class="badge bg-danger">${m.blood || '-'}</span></td>
                <td style="color:#fff">${m.phone}<br><small>${m.email}</small></td>
                <td><button class="btn btn-sm btn-outline-warning me-1" onclick='openMemberForm(${JSON.stringify({id:doc.id,...m})})'><i class="fas fa-edit"></i></button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('members','${doc.id}')"><i class="fas fa-trash"></i></button></td>
            </tr>`;
        });
        html += `</tbody></table>`;
        document.getElementById('memberList').innerHTML = html || '<p class="text-muted p-3">কোন সদস্য নেই</p>';
    });

    // Events Listener
    onSnapshot(collection(db, "events"), (snap) => {
        let planningHtml = `<table class="table"><thead><tr><th>ইভেন্ট</th><th>তারিখ</th><th>বাজেট</th><th>স্ট্যাটাস</th><th>সংগৃহীত</th><th>খরচ</th><th>অ্যাকশন</th></tr></thead><tbody>`;
        
        snap.forEach(doc => {
            const e = doc.data();
            let statusBadge = '';
            let rowColor = '';
            
            if (e.status === 'successful') {
                statusBadge = '<span class="status-success"><i class="fas fa-check-circle"></i> সফল</span>';
                rowColor = 'style="border-left: 3px solid #2ecc71"';
            } else if (e.status === 'failed') {
                statusBadge = '<span class="status-failed"><i class="fas fa-times-circle"></i> ব্যর্থ</span>';
                rowColor = 'style="border-left: 3px solid #e74c3c"';
            } else {
                statusBadge = '<span class="status-pending"><i class="fas fa-clock"></i> পেন্ডিং</span>';
                rowColor = 'style="border-left: 3px solid #f39c12"';
            }
            
            planningHtml += `<tr ${rowColor}>
                <td style="color:#fff"><strong>${e.name}</strong><br><small>${e.details || ''}</small></td>
                <td style="color:#ddd">${e.date || '-'}</td>
                <td style="color:#c6a34f">৳${e.budget || 0}</td>
                <td>${statusBadge}</td>
                <td style="color:#a8e6cf">৳${e.fund || 0}</td>
                <td style="color:#ffb3b3">৳${e.cost || 0}</td>
                <td><button class="btn btn-sm btn-outline-warning me-1" onclick='openEventForm(${JSON.stringify({id:doc.id,...e})})'><i class="fas fa-edit"></i></button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('events','${doc.id}")'><i class="fas fa-trash"></i></button></td>
            </tr>`;
        });
        
        planningHtml += `</tbody></table>`;
        document.getElementById('planningList').innerHTML = planningHtml || '<p class="text-muted p-3">কোন ইভেন্ট নেই</p>';
    });
</script>

</body>
</html>
