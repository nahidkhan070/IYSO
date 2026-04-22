
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>IYSO প্রিমিয়াম ড্যাশবোর্ড | আইডিয়াল যুব সেবা সংস্থা</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdn.sheetjs.com/xlsx-0.20.2/package/dist/xlsx.full.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.31/jspdf.plugin.autotable.min.js"></script>

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
            --handcash: #888;
            --purple: #9b59b6;
            --aqua: #1abc9c;
            --light-grey: #bdc3c7;
            --success-green: #2ecc71;
            --danger-red: #e74c3c;
            --warning-yellow: #f39c12;
            --table-bg: rgba(0, 0, 0, 0.6);
            --table-hover: rgba(0, 104, 55, 0.15);
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

        body::before {
            content: "";
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('image_0.png') center/contain no-repeat;
            opacity: 0.03;
            pointer-events: none;
            z-index: 0;
        }

        .sidebar {
            width: 280px;
            height: 100vh;
            position: fixed;
            background: linear-gradient(135deg, rgba(0, 0, 0, 0.95) 0%, rgba(0, 50, 25, 0.95) 100%);
            backdrop-filter: blur(20px);
            padding: 30px 20px;
            border-right: 1px solid rgba(198, 163, 79, 0.2);
            z-index: 1000;
            transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            overflow-y: auto;
            transform: translateX(0);
            box-shadow: 5px 0 30px rgba(0, 0, 0, 0.3);
        }

        @media (max-width: 768px) {
            .sidebar {
                transform: translateX(-100%);
                width: 280px;
            }
            .sidebar.open {
                transform: translateX(0);
            }
            .main {
                margin-left: 0 !important;
                padding: 70px 12px 20px !important;
            }
            .menu-toggle {
                display: flex !important;
                position: fixed;
                top: 12px;
                left: 12px;
                z-index: 1001;
                background: linear-gradient(135deg, var(--green), var(--dark-green));
                border: none;
                color: white;
                padding: 12px 16px;
                border-radius: 12px;
                cursor: pointer;
                align-items: center;
                gap: 10px;
                font-size: 14px;
                font-weight: 600;
                box-shadow: 0 4px 15px rgba(0,104,55,0.3);
            }
            .net-balance-amount {
                font-size: 36px !important;
            }
            .small-card-amount {
                font-size: 20px !important;
            }
            .glass-card {
                padding: 15px !important;
            }
            .net-balance-card {
                padding: 20px !important;
                margin-bottom: 15px;
            }
            .money-numbers {
                margin-top: 10px;
            }
            .chrome-tabs {
                flex-wrap: wrap;
                gap: 8px;
            }
            .chrome-tab {
                flex: 1;
                min-width: 100px;
                text-align: center;
                padding: 10px 12px !important;
                font-size: 12px !important;
            }
            .export-buttons {
                flex-wrap: wrap;
            }
        }

        @media (max-width: 480px) {
            .main {
                padding: 65px 10px 15px !important;
            }
            .net-balance-amount {
                font-size: 28px !important;
            }
            .small-card-amount {
                font-size: 18px !important;
            }
            .small-card-title {
                font-size: 10px !important;
            }
            .data-table {
                font-size: 11px;
            }
            .data-table th, .data-table td {
                padding: 8px 6px !important;
            }
            .btn {
                padding: 6px 12px !important;
                font-size: 12px !important;
            }
            h3 {
                font-size: 18px !important;
            }
            .chrome-tab {
                font-size: 10px !important;
                padding: 8px 10px !important;
            }
        }

        @media (min-width: 769px) {
            .menu-toggle {
                display: none;
            }
        }

        .logo {
            font-size: 32px;
            font-weight: 800;
            background: linear-gradient(135deg, var(--gold) 0%, #ffd700 50%, var(--gold) 100%);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 50px;
            text-align: center;
            letter-spacing: 3px;
            position: relative;
            font-family: 'Hind Siliguri', sans-serif;
            animation: logoGlow 3s ease-in-out infinite;
        }

        @keyframes logoGlow {
            0%, 100% { filter: drop-shadow(0 0 5px rgba(198,163,79,0.3)); }
            50% { filter: drop-shadow(0 0 20px rgba(198,163,79,0.6)); }
        }

        .logo::after {
            content: '';
            position: absolute;
            bottom: -12px;
            left: 50%;
            transform: translateX(-50%);
            width: 60px;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--gold), transparent);
        }

        .nav-item {
            padding: 14px 18px;
            margin: 8px 0;
            border-radius: 14px;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            color: rgba(255,255,255,0.8);
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 14px;
            position: relative;
            overflow: hidden;
            font-family: 'Hind Siliguri', sans-serif;
            font-size: 16px;
        }

        .nav-item i {
            width: 24px;
            font-size: 18px;
            transition: transform 0.3s ease;
        }

        .nav-item:hover i {
            transform: scale(1.1);
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
            transform: translateX(8px);
        }

        .nav-item.active {
            background: linear-gradient(135deg, var(--green), var(--dark-green));
            color: white;
            box-shadow: 0 6px 20px rgba(0,104,55,0.4);
        }

        .nav-item.active i {
            transform: scale(1.05);
        }

        .main {
            margin-left: 280px;
            padding: 25px 30px;
            position: relative;
            z-index: 1;
            transition: margin-left 0.3s ease;
            min-height: 100vh;
        }

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

        .money-numbers {
            background: rgba(0,0,0,0.5);
            border-radius: 16px;
            padding: 12px;
            border: 1px solid rgba(255,255,255,0.1);
            height: 100%;
        }

        .bkash-box {
            background: linear-gradient(135deg, var(--pink), #c40e5e);
            border-radius: 12px;
            padding: 10px 14px;
            margin-bottom: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .nagad-box {
            background: linear-gradient(135deg, var(--orange), #e67e00);
            border-radius: 12px;
            padding: 10px 14px;
            cursor: pointer;
            transition: all 0.3s ease;
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
            background: transparent;
        }

        .data-table tr {
            transition: background 0.2s ease;
        }

        .data-table tr:hover {
            background: var(--table-hover) !important;
        }

        .uid-text { color: var(--purple) !important; font-weight: 600; }
        .name-text { color: var(--aqua) !important; font-weight: 600; }
        .blood-text { color: var(--light-grey) !important; font-weight: 500; }
        .bkash-text { color: var(--pink) !important; font-weight: 600; }
        .nagad-text { color: var(--orange) !important; font-weight: 600; }
        .handcash-text { color: var(--handcash) !important; font-weight: 600; }

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

        .chrome-tabs {
            display: flex;
            gap: 8px;
            background: rgba(0, 0, 0, 0.3);
            padding: 8px;
            border-radius: 16px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .chrome-tab {
            padding: 12px 24px;
            background: rgba(255, 255, 255, 0.05);
            border: none;
            color: rgba(255, 255, 255, 0.7);
            font-weight: 600;
            border-radius: 12px;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            cursor: pointer;
            position: relative;
            overflow: hidden;
            font-family: 'Hind Siliguri', sans-serif;
            font-size: 14px;
            backdrop-filter: blur(10px);
        }

        .chrome-tab::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
            transition: left 0.5s;
        }

        .chrome-tab:hover::before {
            left: 100%;
        }

        .chrome-tab:hover {
            background: rgba(0, 104, 55, 0.3);
            color: white;
            transform: translateY(-2px);
        }

        .chrome-tab.active {
            background: linear-gradient(135deg, var(--green), var(--dark-green));
            color: white;
            box-shadow: 0 4px 15px rgba(0, 104, 55, 0.4);
        }

        .chrome-tab.active::after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 20%;
            width: 60%;
            height: 3px;
            background: var(--gold);
            border-radius: 3px;
        }

        .summary-card {
            background: linear-gradient(135deg, rgba(0,104,55,0.2), rgba(198,163,79,0.1));
            border-radius: 12px;
            padding: 12px 20px;
            border: 1px solid rgba(198,163,79,0.3);
            backdrop-filter: blur(10px);
        }

        .summary-label {
            font-size: 12px;
            color: var(--gold);
            letter-spacing: 1px;
        }

        .summary-amount {
            font-size: 24px;
            font-weight: 700;
            color: var(--gold);
        }

        .search-container {
            position: relative;
            flex: 1;
            max-width: 350px;
        }

        .search-container input {
            background: rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 12px;
            padding: 10px 40px 10px 15px;
            color: white;
            width: 100%;
            transition: all 0.3s ease;
        }

        .search-container input:focus {
            outline: none;
            border-color: var(--green);
            background: rgba(0, 0, 0, 0.7);
        }

        .search-container i {
            position: absolute;
            right: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--gold);
        }

        .export-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            align-items: center;
        }

        .btn-export-excel {
            background: linear-gradient(135deg, #1e8449, #145a32);
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 10px;
            font-size: 13px;
            font-weight: 600;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .btn-import-excel {
            background: linear-gradient(135deg, #2980b9, #1a5276);
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 10px;
            font-size: 13px;
            font-weight: 600;
            transition: all 0.3s ease;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-export-pdf {
            background: linear-gradient(135deg, #c0392b, #922b21);
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 10px;
            font-size: 13px;
            font-weight: 600;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .btn-export-excel:hover, .btn-export-pdf:hover, .btn-import-excel:hover {
            transform: translateY(-2px);
            filter: brightness(1.1);
        }

        .file-input-wrapper {
            position: relative;
            display: inline-block;
        }
        
        .file-input-wrapper input {
            position: absolute;
            opacity: 0;
            width: 100%;
            height: 100%;
            cursor: pointer;
            left: 0;
            top: 0;
        }
        
        .import-progress {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(0,0,0,0.95);
            padding: 20px 30px;
            border-radius: 12px;
            z-index: 2000;
            text-align: center;
            border: 1px solid var(--gold);
            box-shadow: 0 0 30px rgba(0,0,0,0.5);
            font-weight: 600;
        }

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

        .password-modal .modal-content {
            background: linear-gradient(135deg, #1a1f24, #0f1419);
            border: 2px solid var(--gold);
        }

        .password-input {
            font-size: 18px;
            letter-spacing: 2px;
            text-align: center;
        }

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
            0%, 100% { text-shadow: 0 0 5px rgba(198, 163, 79, 0.3); opacity: 0.8; }
            50% { text-shadow: 0 0 15px rgba(198, 163, 79, 0.6); opacity: 1; }
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .page { animation: fadeInUp 0.4s ease; }

        button { transition: all 0.3s ease; }
        button:active { transform: scale(0.95); }

        ::-webkit-scrollbar { width: 8px; height: 8px; }
        ::-webkit-scrollbar-track { background: rgba(0,0,0,0.3); border-radius: 10px; }
        ::-webkit-scrollbar-thumb { background: var(--green); border-radius: 10px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--gold); }

        .phone-numbers-container {
            max-height: 200px;
            overflow-y: auto;
            border: 1px solid #3a3f45;
            border-radius: 8px;
            padding: 10px;
            background: #1a1f24;
        }

        .phone-number-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px;
            margin-bottom: 5px;
            background: #2a2f35;
            border-radius: 6px;
        }

        .remove-phone-btn {
            background: none;
            border: none;
            color: var(--danger-red);
            cursor: pointer;
            padding: 0 5px;
        }
        .remove-phone-btn:hover { color: #ff6b6b; }
        .add-phone-btn { margin-top: 10px; width: 100%; }
    </style>
</head>
<body>

<button class="menu-toggle" onclick="toggleSidebar()">
    <i class="fas fa-bars"></i> মেনু
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

    <div id="members" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-3">
            <h3><i class="fas fa-users text-gold"></i> সদস্যবৃন্দ</h3>
            <div class="d-flex gap-2 flex-wrap export-buttons">
                <div class="search-container">
                    <input type="text" id="memberSearchInput" placeholder="আইডি, নাম, ফোন, ইমেইল দিয়ে খুঁজুন..." onkeyup="searchMembers()">
                    <i class="fas fa-search"></i>
                </div>
                <button onclick="exportToExcel('members')" class="btn-export-excel"><i class="fas fa-file-excel"></i> Excel Export</button>
                <div class="file-input-wrapper">
                    <button class="btn-import-excel" onclick="document.getElementById('importExcelFile').click()"><i class="fas fa-upload"></i> Excel Import</button>
                    <input type="file" id="importExcelFile" accept=".xlsx, .xls" style="display:none;" onchange="importMembersFromExcel(this)">
                </div>
                <button onclick="exportToPDF('members')" class="btn-export-pdf"><i class="fas fa-file-pdf"></i> PDF</button>
                <button onclick="openMemberForm()" class="btn btn-success px-4"><i class="fas fa-plus"></i> নতুন সদস্য</button>
            </div>
        </div>
        <div class="data-table" id="memberList">লোড হচ্ছে...</div>
    </div>

    <div id="donations" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-2">
            <h3><i class="fas fa-hand-holding-usd text-gold"></i> দান-অনুদানের তালিকা</h3>
            <div class="d-flex gap-2 export-buttons">
                <button onclick="exportToExcel('donations')" class="btn-export-excel"><i class="fas fa-file-excel"></i> Excel</button>
                <button onclick="exportToPDF('donations')" class="btn-export-pdf"><i class="fas fa-file-pdf"></i> PDF</button>
                <button onclick="openDonationForm()" class="btn btn-success px-4"><i class="fas fa-plus"></i> নতুন দান</button>
            </div>
        </div>
        
        <div class="chrome-tabs">
            <button class="chrome-tab active" data-tab="lifetime"><i class="fas fa-globe"></i> সর্বমোট দান</button>
            <button class="chrome-tab" data-tab="current"><i class="fas fa-calendar-week"></i> চলতি মাসের দান</button>
            <button class="chrome-tab" data-tab="previous"><i class="fas fa-history"></i> পূর্ববর্তী মাসের দান</button>
        </div>
        
        <div id="lifetimeTab" class="tab-content-active">
            <div class="summary-card mb-3"><div class="summary-label">সর্বমোট সংগ্রহ</div><div class="summary-amount" id="lifetimeSummary">৳0</div></div>
            <div class="data-table" id="lifetimeDonationList">লোড হচ্ছে...</div>
        </div>
        <div id="currentTab" class="tab-content-hidden" style="display:none;">
            <div class="summary-card mb-3"><div class="summary-label">চলতি মাসের মোট সংগ্রহ</div><div class="summary-amount" id="currentSummary">৳0</div></div>
            <div class="data-table" id="currentDonationList">লোড হচ্ছে...</div>
        </div>
        <div id="previousTab" class="tab-content-hidden" style="display:none;">
            <div class="summary-card mb-3"><div class="summary-label">পূর্ববর্তী মাসের মোট সংগ্রহ</div><div class="summary-amount" id="previousSummary">৳0</div></div>
            <div class="data-table" id="previousDonationList">লোড হচ্ছে...</div>
        </div>
    </div>

    <div id="expenses" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-2">
            <h3><i class="fas fa-chart-line text-gold"></i> খরচের তালিকা</h3>
            <div class="d-flex gap-2 export-buttons">
                <button onclick="exportToExcel('expenses')" class="btn-export-excel"><i class="fas fa-file-excel"></i> Excel</button>
                <button onclick="exportToPDF('expenses')" class="btn-export-pdf"><i class="fas fa-file-pdf"></i> PDF</button>
                <button onclick="openExpenseForm()" class="btn btn-danger px-4"><i class="fas fa-plus"></i> নতুন খরচ</button>
            </div>
        </div>
        
        <div class="chrome-tabs">
            <button class="chrome-tab expense-tab active" data-expense-tab="lifetime"><i class="fas fa-globe"></i> সর্বমোট খরচ</button>
            <button class="chrome-tab expense-tab" data-expense-tab="current"><i class="fas fa-calendar-week"></i> চলতি মাসের খরচ</button>
            <button class="chrome-tab expense-tab" data-expense-tab="previous"><i class="fas fa-history"></i> পূর্ববর্তী মাসের খরচ</button>
        </div>
        
        <div id="expenseLifetimeTab" class="expense-tab-content">
            <div class="summary-card mb-3"><div class="summary-label">সর্বমোট খরচ</div><div class="summary-amount" id="expenseLifetimeSummary">৳0</div></div>
            <div class="data-table" id="expenseLifetimeList">লোড হচ্ছে...</div>
        </div>
        <div id="expenseCurrentTab" class="expense-tab-content" style="display:none;">
            <div class="summary-card mb-3"><div class="summary-label">চলতি মাসের মোট খরচ</div><div class="summary-amount" id="expenseCurrentSummary">৳0</div></div>
            <div class="data-table" id="expenseCurrentList">লোড হচ্ছে...</div>
        </div>
        <div id="expensePreviousTab" class="expense-tab-content" style="display:none;">
            <div class="summary-card mb-3"><div class="summary-label">পূর্ববর্তী মাসের মোট খরচ</div><div class="summary-amount" id="expensePreviousSummary">৳0</div></div>
            <div class="data-table" id="expensePreviousList">লোড হচ্ছে...</div>
        </div>
    </div>

    <div id="events" class="page" style="display:none;">
        <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-2">
            <h3><i class="fas fa-calendar-alt text-gold"></i> ইভেন্ট প্ল্যানিং</h3>
            <div class="d-flex gap-2 export-buttons">
                <button onclick="exportToExcel('events')" class="btn-export-excel"><i class="fas fa-file-excel"></i> Excel</button>
                <button onclick="exportToPDF('events')" class="btn-export-pdf"><i class="fas fa-file-pdf"></i> PDF</button>
                <button onclick="openEventForm()" class="btn btn-success px-4"><i class="fas fa-plus"></i> নতুন ইভেন্ট</button>
            </div>
        </div>
        <div class="data-table" id="planningList">লোড হচ্ছে...</div>
    </div>

    <div class="footer-text">
        <div class="glowing-text">আইডিয়াল যুব সেবা সংস্থা</div>
        <div class="creator-text">Created by Nahidul Islam</div>
    </div>
</div>

<div class="modal fade" id="passwordModal" tabindex="-1" data-bs-backdrop="static">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
            <div class="modal-header border-0">
                <h5 class="modal-title"><i class="fas fa-lock"></i> পাসওয়ার্ড প্রয়োজন</h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body">
                <p>এই অপারেশন করতে পাসওয়ার্ড দিন:</p>
                <input type="password" id="passwordInput" class="form-control password-input" placeholder="পাসওয়ার্ড">
                <div id="passwordError" class="text-danger mt-2" style="display:none;">ভুল পাসওয়ার্ড! আবার চেষ্টা করুন।</div>
            </div>
            <div class="modal-footer border-0">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">বাতিল</button>
                <button type="button" class="btn btn-success" id="confirmPasswordBtn">নিশ্চিত করুন</button>
            </div>
        </div>
    </div>
</div>

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
    import { getFirestore, collection, addDoc, onSnapshot, deleteDoc, doc, updateDoc, query, where, getDocs, writeBatch } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "YOUR_KEY",
        projectId: "iyso-web"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    const bsModal = new bootstrap.Modal(document.getElementById('dataModal'));
    const passwordModal = new bootstrap.Modal(document.getElementById('passwordModal'));

    // Changed password to iyso2020
    const ADMIN_PASSWORD = "iyso2020";
    let currentMembersData = [];

    function verifyPassword(callback, actionData = null) {
        document.getElementById('passwordInput').value = '';
        document.getElementById('passwordError').style.display = 'none';
        const confirmBtn = document.getElementById('confirmPasswordBtn');
        const newConfirmBtn = confirmBtn.cloneNode(true);
        confirmBtn.parentNode.replaceChild(newConfirmBtn, confirmBtn);
        newConfirmBtn.onclick = () => {
            if (document.getElementById('passwordInput').value === ADMIN_PASSWORD) {
                passwordModal.hide();
                if (callback) callback(actionData);
            } else {
                document.getElementById('passwordError').style.display = 'block';
            }
        };
        passwordModal.show();
    }

    window.toggleSidebar = () => document.getElementById('sidebar').classList.toggle('open');

    document.addEventListener('click', (e) => {
        const sidebar = document.getElementById('sidebar');
        const toggleBtn = document.querySelector('.menu-toggle');
        if (window.innerWidth <= 768 && sidebar.classList.contains('open')) {
            if (!sidebar.contains(e.target) && !toggleBtn.contains(e.target)) {
                sidebar.classList.remove('open');
            }
        }
    });

    document.querySelectorAll('.nav-item').forEach(item => {
        item.onclick = () => {
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            item.classList.add('active');
            document.querySelectorAll('.page').forEach(p => p.style.display = 'none');
            const pageId = document.getElementById(item.dataset.page);
            pageId.style.display = 'block';
            pageId.style.animation = 'none';
            setTimeout(() => pageId.style.animation = 'fadeInUp 0.4s ease', 10);
            if (window.innerWidth <= 768) document.getElementById('sidebar').classList.remove('open');
        };
    });

    function getCurrentMonthBangla() {
        const months = ['জানুয়ারি', 'ফেব্রুয়ারি', 'মার্চ', 'এপ্রিল', 'মে', 'জুন', 'জুলাই', 'আগস্ট', 'সেপ্টেম্বর', 'অক্টোবর', 'নভেম্বর', 'ডিসেম্বর'];
        const now = new Date();
        return `${months[now.getMonth()]} ${now.getFullYear()}`;
    }

    let bkashNumber = localStorage.getItem('bkashNumber') || '017XXXXXXXX';
    let nagadNumber = localStorage.getItem('nagadNumber') || '017XXXXXXXX';
    document.getElementById('bkashNumber').innerText = bkashNumber;
    document.getElementById('nagadNumber').innerText = nagadNumber;
    document.getElementById('currentMonthName').innerText = getCurrentMonthBangla();
    document.getElementById('expenseMonthName').innerText = getCurrentMonthBangla();
    document.getElementById('eventMonthName').innerText = 'ইভেন্ট সংগ্রহ';

    window.editSendNumber = (type) => {
        verifyPassword(() => {
            const newNumber = prompt(`${type.toUpperCase()} সেন্ড মানি নম্বর দিন:`, type === 'bkash' ? bkashNumber : nagadNumber);
            if (newNumber && newNumber.trim()) {
                if (type === 'bkash') { bkashNumber = newNumber; document.getElementById('bkashNumber').innerText = bkashNumber; localStorage.setItem('bkashNumber', bkashNumber); }
                else { nagadNumber = newNumber; document.getElementById('nagadNumber').innerText = nagadNumber; localStorage.setItem('nagadNumber', nagadNumber); }
            }
        });
    };

    window.openMemberForm = (data = null) => {
        const action = () => {
            let phoneNumbers = data?.phoneNumbers || (data?.phone ? [data.phone] : ['']);
            document.getElementById('modalTitle').innerHTML = data ? '<i class="fas fa-edit"></i> সদস্য সম্পাদনা' : '<i class="fas fa-user-plus"></i> নতুন সদস্য';
            document.getElementById('modalBody').innerHTML = `
                <input type="text" id="mUID" class="form-control mb-3" placeholder="সদস্য আইডি" value="${data?.uid || ''}">
                <input type="text" id="mName" class="form-control mb-3" placeholder="পুরো নাম" value="${data?.name || ''}">
                <input type="text" id="mDesignation" class="form-control mb-3" placeholder="পদবি" value="${data?.designation || ''}">
                <select id="mBlood" class="form-select mb-3">
                    <option value="">ব্লাড গ্রুপ</option>
                    ${['A+','A-','B+','B-','O+','O-','AB+','AB-'].map(b => `<option value="${b}" ${data?.blood === b ? 'selected' : ''}>${b}</option>`).join('')}
                </select>
                <label class="small text-muted mb-2">ফোন নম্বরসমূহ (একাধিক)</label>
                <div id="phoneNumbersContainer" class="phone-numbers-container mb-3"></div>
                <button type="button" class="btn btn-sm btn-outline-success add-phone-btn" onclick="addPhoneField()"><i class="fas fa-plus"></i> আরও ফোন নম্বর যোগ করুন</button>
                <input type="email" id="mEmail" class="form-control mt-3" placeholder="ইমেইল" value="${data?.email || ''}">
            `;
            window.renderPhoneNumbers = () => {
                const container = document.getElementById('phoneNumbersContainer');
                if (!container) return;
                container.innerHTML = '';
                phoneNumbers.forEach((phone, index) => {
                    const div = document.createElement('div');
                    div.className = 'phone-number-item';
                    div.innerHTML = `<input type="tel" class="form-control phone-input" style="flex:1; margin-right:10px;" placeholder="017XXXXXXXX" value="${phone}" data-index="${index}"><button type="button" class="remove-phone-btn" onclick="removePhoneField(${index})"><i class="fas fa-trash"></i></button>`;
                    container.appendChild(div);
                });
                document.querySelectorAll('.phone-input').forEach(input => {
                    input.onchange = (e) => { phoneNumbers[parseInt(e.target.dataset.index)] = e.target.value; };
                });
            };
            window.addPhoneField = () => { phoneNumbers.push(''); renderPhoneNumbers(); };
            window.removePhoneField = (index) => { phoneNumbers.splice(index, 1); renderPhoneNumbers(); };
            renderPhoneNumbers();
            const saveBtn = document.getElementById('saveBtn');
            const newSaveBtn = saveBtn.cloneNode(true);
            saveBtn.parentNode.replaceChild(newSaveBtn, saveBtn);
            newSaveBtn.onclick = async () => {
                const validPhoneNumbers = phoneNumbers.filter(p => p && p.trim().length >= 8);
                const memberData = {
                    uid: document.getElementById('mUID').value,
                    name: document.getElementById('mName').value,
                    designation: document.getElementById('mDesignation').value,
                    blood: document.getElementById('mBlood').value,
                    phoneNumbers: validPhoneNumbers,
                    phone: validPhoneNumbers[0] || '',
                    email: document.getElementById('mEmail').value
                };
                if (data) await updateDoc(doc(db, "members", data.id), memberData);
                else await addDoc(collection(db, "members"), memberData);
                bsModal.hide();
            };
            bsModal.show();
        };
        verifyPassword(action, data);
    };

    window.getMemberByPhone = async (phone) => {
        if (!phone || phone.length < 8) return null;
        const membersRef = collection(db, "members");
        const q = query(membersRef, where("phoneNumbers", "array-contains", phone));
        const snapshot = await getDocs(q);
        if (!snapshot.empty) return { id: snapshot.docs[0].id, ...snapshot.docs[0].data() };
        return null;
    };

    window.importMembersFromExcel = async (input) => {
        const file = input.files[0];
        if (!file) return;
        
        verifyPassword(async () => {
            const progressDiv = document.createElement('div');
            progressDiv.className = 'import-progress';
            progressDiv.innerHTML = '<i class="fas fa-spinner fa-spin"></i> ডাটা ইম্পোর্ট হচ্ছে... দয়া করে অপেক্ষা করুন';
            document.body.appendChild(progressDiv);
            
            try {
                const data = await file.arrayBuffer();
                const workbook = XLSX.read(data);
                const worksheet = workbook.Sheets[workbook.SheetNames[0]];
                const jsonData = XLSX.utils.sheet_to_json(worksheet);
                
                const batch = writeBatch(db);
                let count = 0;
                
                for (const row of jsonData) {
                    const uid = row['আইডি'] || row['ID'] || row['uid'] || '';
                    if (!uid) continue;
                    
                    const phoneNumbers = [];
                    const phoneField = row['যোগাযোগ'] || row['ফোন'] || row['phone'] || '';
                    if (phoneField) {
                        const phones = phoneField.toString().split(',').map(p => p.trim());
                        phoneNumbers.push(...phones);
                    }
                    
                    const memberData = {
                        uid: uid,
                        name: row['নাম'] || row['Name'] || row['name'] || '',
                        designation: row['পদবি'] || row['Designation'] || row['designation'] || '',
                        blood: row['ব্লাড'] || row['Blood'] || row['blood'] || '',
                        phoneNumbers: phoneNumbers,
                        phone: phoneNumbers[0] || '',
                        email: row['ইমেইল'] || row['Email'] || row['email'] || ''
                    };
                    
                    const existingMember = currentMembersData.find(m => m.uid === uid);
                    if (existingMember) {
                        const memberRef = doc(db, "members", existingMember.id);
                        batch.update(memberRef, memberData);
                    } else {
                        const memberRef = doc(collection(db, "members"));
                        batch.set(memberRef, memberData);
                    }
                    count++;
                }
                
                await batch.commit();
                progressDiv.innerHTML = `<i class="fas fa-check-circle"></i> সফলভাবে ${count} টি সদস্য ইম্পোর্ট হয়েছে!`;
                setTimeout(() => progressDiv.remove(), 3000);
                
            } catch (error) {
                progressDiv.innerHTML = `<i class="fas fa-exclamation-triangle"></i> ইম্পোর্ট ব্যর্থ হয়েছে: ${error.message}`;
                setTimeout(() => progressDiv.remove(), 3000);
                console.error("Import error:", error);
            }
            
            input.value = '';
        });
    };

    window.openDonationForm = (data = null) => {
        const action = () => {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('modalTitle').innerHTML = data ? '<i class="fas fa-edit"></i> দান সম্পাদনা' : '<i class="fas fa-plus"></i> নতুন দান';
            document.getElementById('modalBody').innerHTML = `
                <div class="mb-3"><label class="small text-muted">ফোন নম্বর (সদস্য খুঁজতে)</label><input type="tel" id="dPhone" class="form-control mb-2" placeholder="017XXXXXXXX" value="${data?.phone || ''}"><div id="phoneSearchStatus" class="small" style="display:none;"></div></div>
                <input type="text" id="dUID" class="form-control mb-3" placeholder="সদস্য আইডি" value="${data?.uid || ''}" readonly style="background:#1a1f24">
                <input type="text" id="dName" class="form-control mb-3" placeholder="সদস্যের নাম" value="${data?.name || ''}" readonly style="background:#1a1f24">
                <input type="number" id="dAmount" class="form-control mb-3" placeholder="পরিমাণ (টাকা)" value="${data?.amount || ''}">
                <select id="dType" class="form-select mb-3"><option value="monthly" ${data?.type === 'monthly' ? 'selected' : ''}>মাসিক চাঁদা</option><option value="event" ${data?.type === 'event' ? 'selected' : ''}>ইভেন্ট দান</option></select>
                <select id="dSystem" class="form-select mb-3"><option value="">পেমেন্ট পদ্ধতি</option><option value="Bkash" ${data?.system === 'Bkash' ? 'selected' : ''}>বিকাশ</option><option value="Nagad" ${data?.system === 'Nagad' ? 'selected' : ''}>নগদ</option><option value="HandCash" ${data?.system === 'HandCash' ? 'selected' : ''}>হ্যান্ড ক্যাশ</option></select>
                <input type="date" id="dDate" class="form-control mb-3" value="${data?.date || today}">
                <input type="text" id="dEventName" class="form-control" placeholder="ইভেন্টের নাম (যদি ইভেন্ট দান হয়)" value="${data?.eventName || ''}">
            `;
            const phoneInput = document.getElementById('dPhone');
            const statusDiv = document.getElementById('phoneSearchStatus');
            let debounceTimer;
            phoneInput.oninput = async () => {
                clearTimeout(debounceTimer);
                const phone = phoneInput.value.trim();
                if (phone.length >= 8) {
                    statusDiv.style.display = 'block';
                    statusDiv.innerHTML = '<i class="fas fa-spinner fa-spin"></i> খুঁজছি...';
                    statusDiv.style.color = '#c6a34f';
                    debounceTimer = setTimeout(async () => {
                        const member = await getMemberByPhone(phone);
                        if (member) {
                            document.getElementById('dUID').value = member.uid || '';
                            document.getElementById('dName').value = member.name || '';
                            statusDiv.innerHTML = '<i class="fas fa-check-circle"></i> সদস্য পাওয়া গেছে!';
                            statusDiv.style.color = '#2ecc71';
                            setTimeout(() => statusDiv.style.display = 'none', 2000);
                        } else {
                            document.getElementById('dUID').value = '';
                            document.getElementById('dName').value = '';
                            statusDiv.innerHTML = '<i class="fas fa-exclamation-triangle"></i> সদস্য পাওয়া যায়নি';
                            statusDiv.style.color = '#e74c3c';
                            setTimeout(() => statusDiv.style.display = 'none', 2000);
                        }
                    }, 500);
                } else { statusDiv.style.display = 'none'; document.getElementById('dUID').value = ''; document.getElementById('dName').value = ''; }
            };
            const saveBtn = document.getElementById('saveBtn');
            const newSaveBtn = saveBtn.cloneNode(true);
            saveBtn.parentNode.replaceChild(newSaveBtn, saveBtn);
            newSaveBtn.onclick = async () => {
                const donationData = {
                    uid: document.getElementById('dUID').value, name: document.getElementById('dName').value, phone: document.getElementById('dPhone').value,
                    amount: Number(document.getElementById('dAmount').value), type: document.getElementById('dType').value,
                    system: document.getElementById('dSystem').value, date: document.getElementById('dDate').value,
                    eventName: document.getElementById('dEventName').value || '', timestamp: new Date().toISOString()
                };
                if (data) await updateDoc(doc(db, "donations", data.id), donationData);
                else await addDoc(collection(db, "donations"), donationData);
                bsModal.hide();
            };
            bsModal.show();
        };
        verifyPassword(action, data);
    };

    window.openExpenseForm = (data = null) => {
        const action = () => {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('modalTitle').innerHTML = data ? '<i class="fas fa-edit"></i> খরচ সম্পাদনা' : '<i class="fas fa-plus"></i> নতুন খরচ';
            document.getElementById('modalBody').innerHTML = `
                <input type="text" id="eDesc" class="form-control mb-3" placeholder="খরচের বিবরণ" value="${data?.description || ''}">
                <input type="number" id="eAmount" class="form-control mb-3" placeholder="পরিমাণ (টাকা)" value="${data?.amount || ''}">
                <select id="eType" class="form-select mb-3"><option value="monthly" ${data?.type === 'monthly' ? 'selected' : ''}>মাসিক খরচ</option><option value="event" ${data?.type === 'event' ? 'selected' : ''}>ইভেন্ট খরচ</option></select>
                <input type="date" id="eDate" class="form-control mb-3" value="${data?.date || today}">
                <input type="text" id="eEventName" class="form-control" placeholder="ইভেন্টের নাম (যদি ইভেন্ট খরচ হয়)" value="${data?.eventName || ''}">
            `;
            const saveBtn = document.getElementById('saveBtn');
            const newSaveBtn = saveBtn.cloneNode(true);
            saveBtn.parentNode.replaceChild(newSaveBtn, saveBtn);
            newSaveBtn.onclick = async () => {
                const expenseData = {
                    description: document.getElementById('eDesc').value, amount: Number(document.getElementById('eAmount').value),
                    type: document.getElementById('eType').value, date: document.getElementById('eDate').value,
                    eventName: document.getElementById('eEventName').value || '', timestamp: new Date().toISOString()
                };
                if (data) await updateDoc(doc(db, "expenses", data.id), expenseData);
                else await addDoc(collection(db, "expenses"), expenseData);
                bsModal.hide();
            };
            bsModal.show();
        };
        verifyPassword(action, data);
    };

    window.openEventForm = (data = null) => {
        const action = () => {
            document.getElementById('modalTitle').innerHTML = data ? '<i class="fas fa-edit"></i> ইভেন্ট সম্পাদনা' : '<i class="fas fa-calendar-plus"></i> নতুন ইভেন্ট';
            document.getElementById('modalBody').innerHTML = `
                <input type="text" id="evName" class="form-control mb-3" placeholder="ইভেন্টের নাম" value="${data?.name || ''}">
                <input type="date" id="evDate" class="form-control mb-3" value="${data?.date || ''}">
                <input type="number" id="evBudget" class="form-control mb-3" placeholder="বাজেট (টাকা)" value="${data?.budget || ''}">
                <select id="evStatus" class="form-select mb-3"><option value="pending" ${data?.status === 'pending' || !data?.status ? 'selected' : ''}>🟡 পেন্ডিং</option><option value="successful" ${data?.status === 'successful' ? 'selected' : ''}>🟢 সফল</option><option value="failed" ${data?.status === 'failed' ? 'selected' : ''}>🔴 ব্যর্থ</option></select>
                <textarea id="evDetails" class="form-control" rows="3" placeholder="ইভেন্টের বিবরণ">${data?.details || ''}</textarea>
                ${data?.status === 'successful' ? `<div class="mt-3 p-3 border border-success rounded"><label>সংগৃহীত তহবিল (টাকা)</label><input type="number" id="evFund" class="form-control mt-1" value="${data?.fund || 0}"><label class="mt-2">আসল খরচ (টাকা)</label><input type="number" id="evCost" class="form-control mt-1" value="${data?.cost || 0}"></div>` : ''}
            `;
            const statusSelect = document.getElementById('evStatus');
            if (statusSelect) {
                statusSelect.onchange = () => {
                    const body = document.getElementById('modalBody');
                    const existingFund = data?.fund || 0;
                    const existingCost = data?.cost || 0;
                    if (statusSelect.value === 'successful' && !document.getElementById('evFund')) {
                        const div = document.createElement('div');
                        div.className = 'mt-3 p-3 border border-success rounded';
                        div.innerHTML = `<label>সংগৃহীত তহবিল (টাকা)</label><input type="number" id="evFund" class="form-control mt-1" value="${existingFund}"><label class="mt-2">আসল খরচ (টাকা)</label><input type="number" id="evCost" class="form-control mt-1" value="${existingCost}">`;
                        body.appendChild(div);
                    } else if (statusSelect.value !== 'successful') {
                        const fundDiv = document.getElementById('evFund')?.parentElement;
                        if (fundDiv && fundDiv.parentElement === body) fundDiv.remove();
                    }
                };
            }
            const saveBtn = document.getElementById('saveBtn');
            const newSaveBtn = saveBtn.cloneNode(true);
            saveBtn.parentNode.replaceChild(newSaveBtn, saveBtn);
            newSaveBtn.onclick = async () => {
                const eventData = {
                    name: document.getElementById('evName').value, date: document.getElementById('evDate').value,
                    budget: Number(document.getElementById('evBudget').value), status: document.getElementById('evStatus').value,
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
        verifyPassword(action, data);
    };

    window.deleteItem = async (collectionName, id) => {
        verifyPassword(async () => {
            if (confirm("এই এন্ট্রি ডিলিট করবেন?")) await deleteDoc(doc(db, collectionName, id));
        });
    };

    // Fixed PDF Export Function
    window.exportToPDF = async (type) => {
        verifyPassword(async () => {
            try {
                const { jsPDF } = window.jspdf;
                const doc = new jsPDF({ orientation: 'landscape', unit: 'mm', format: 'a4' });
                let columns = [];
                let rows = [];
                let title = '';
                
                if (type === 'members') {
                    title = 'IYSO - সদস্য তালিকা';
                    columns = [['আইডি', 'নাম', 'পদবি', 'ব্লাড গ্রুপ', 'যোগাযোগ']];
                    const memberRows = document.querySelectorAll('#membersTableBody tr');
                    for (const row of memberRows) {
                        if (row.style.display !== 'none') {
                            const cells = row.querySelectorAll('td');
                            if (cells.length > 0) {
                                rows.push([
                                    cells[0]?.innerText || '',
                                    cells[1]?.innerText || '',
                                    cells[2]?.innerText || '',
                                    cells[3]?.innerText.replace('ব্লাড', '').trim() || '',
                                    cells[4]?.innerText || ''
                                ]);
                            }
                        }
                    }
                } else if (type === 'donations') {
                    const activeTab = document.querySelector('.chrome-tab.active')?.getAttribute('data-tab') || 'lifetime';
                    title = activeTab === 'lifetime' ? 'IYSO - সর্বমোট দান তালিকা' : (activeTab === 'current' ? 'IYSO - চলতি মাসের দান তালিকা' : 'IYSO - পূর্ববর্তী মাসের দান তালিকা');
                    columns = [['তারিখ', 'সদস্য আইডি', 'নাম', 'পরিমাণ', 'ধরন', 'পদ্ধতি']];
                    let tableId = activeTab === 'lifetime' ? 'lifetimeTableBody' : (activeTab === 'current' ? 'currentTableBody' : 'previousTableBody');
                    const rowsData = document.querySelectorAll(`#${tableId} tr`);
                    for (const row of rowsData) {
                        const cells = row.querySelectorAll('td');
                        if (cells.length > 0) {
                            rows.push([
                                cells[0]?.innerText || '',
                                cells[1]?.innerText.split('\n')[0] || '',
                                cells[1]?.innerText.split('\n')[1] || '',
                                cells[2]?.innerText || '',
                                cells[3]?.innerText || '',
                                cells[4]?.innerText || ''
                            ]);
                        }
                    }
                } else if (type === 'expenses') {
                    const activeTab = document.querySelector('.expense-tab.active')?.getAttribute('data-expense-tab') || 'lifetime';
                    title = activeTab === 'lifetime' ? 'IYSO - সর্বমোট খরচ তালিকা' : (activeTab === 'current' ? 'IYSO - চলতি মাসের খরচ তালিকা' : 'IYSO - পূর্ববর্তী মাসের খরচ তালিকা');
                    columns = [['তারিখ', 'বিবরণ', 'পরিমাণ', 'ধরন']];
                    let tableId = activeTab === 'lifetime' ? 'expenseLifetimeTableBody' : (activeTab === 'current' ? 'expenseCurrentTableBody' : 'expensePreviousTableBody');
                    const rowsData = document.querySelectorAll(`#${tableId} tr`);
                    for (const row of rowsData) {
                        const cells = row.querySelectorAll('td');
                        if (cells.length > 0) {
                            rows.push([
                                cells[0]?.innerText || '',
                                cells[1]?.innerText || '',
                                cells[2]?.innerText || '',
                                cells[3]?.innerText || ''
                            ]);
                        }
                    }
                } else if (type === 'events') {
                    title = 'IYSO - ইভেন্ট তালিকা';
                    columns = [['ইভেন্ট', 'তারিখ', 'বাজেট', 'স্ট্যাটাস', 'সংগৃহীত', 'খরচ']];
                    const rowsData = document.querySelectorAll('#eventsTableBody tr');
                    for (const row of rowsData) {
                        const cells = row.querySelectorAll('td');
                        if (cells.length > 0) {
                            rows.push([
                                cells[0]?.innerText || '',
                                cells[1]?.innerText || '',
                                cells[2]?.innerText || '',
                                cells[3]?.innerText || '',
                                cells[4]?.innerText || '',
                                cells[5]?.innerText || ''
                            ]);
                        }
                    }
                }
                
                if (rows.length === 0) {
                    alert("কোন ডাটা নেই!");
                    return;
                }
                
                doc.setFontSize(16);
                doc.setTextColor(198, 163, 79);
                doc.text(title, 14, 15);
                doc.setTextColor(255, 255, 255);
                
                doc.autoTable({
                    head: columns,
                    body: rows,
                    startY: 25,
                    theme: 'striped',
                    styles: { 
                        fontSize: 9, 
                        cellPadding: 3, 
                        textColor: [255, 255, 255],
                        fillColor: [20, 25, 30],
                        lineColor: [198, 163, 79],
                        lineWidth: 0.1
                    },
                    headStyles: { 
                        fillColor: [0, 104, 55], 
                        textColor: [255, 255, 255], 
                        fontStyle: 'bold', 
                        halign: 'center',
                        valign: 'middle'
                    },
                    alternateRowStyles: { 
                        fillColor: [30, 35, 40] 
                    },
                    margin: { top: 25, left: 10, right: 10 }
                });
                
                const fileName = `${title.replace(/ /g, '_')}.pdf`;
                doc.save(fileName);
                
            } catch (error) {
                console.error("PDF Export Error:", error);
                alert("PDF export failed: " + error.message);
            }
        });
    };

    window.exportToExcel = (type) => {
        verifyPassword(() => {
            let data = [];
            let filename = '';
            if (type === 'members') {
                const rows = document.querySelectorAll('#membersTableBody tr');
                rows.forEach(row => {
                    const cells = row.querySelectorAll('td');
                    if (cells.length > 0 && row.style.display !== 'none') {
                        data.push({
                            'আইডি': cells[0]?.innerText || '',
                            'নাম': cells[1]?.innerText || '',
                            'পদবি': cells[2]?.innerText || '',
                            'ব্লাড': cells[3]?.innerText.replace('ব্লাড', '').trim() || '',
                            'যোগাযোগ': cells[4]?.innerText || ''
                        });
                    }
                });
                filename = 'members_data';
            } else if (type === 'donations') {
                const activeTab = document.querySelector('.chrome-tab.active')?.getAttribute('data-tab') || 'lifetime';
                let tableId = '';
                if (activeTab === 'lifetime') tableId = 'lifetimeTableBody';
                else if (activeTab === 'current') tableId = 'currentTableBody';
                else tableId = 'previousTableBody';
                const rows = document.querySelectorAll(`#${tableId} tr`);
                rows.forEach(row => {
                    const cells = row.querySelectorAll('td');
                    if (cells.length > 0) {
                        data.push({
                            'তারিখ': cells[0]?.innerText || '',
                            'সদস্য আইডি': cells[1]?.innerText.split('\n')[0] || '',
                            'নাম': cells[1]?.innerText.split('\n')[1] || '',
                            'পরিমাণ': cells[2]?.innerText || '',
                            'ধরন': cells[3]?.innerText || '',
                            'পদ্ধতি': cells[4]?.innerText || ''
                        });
                    }
                });
                filename = `donations_${activeTab}_data`;
            } else if (type === 'expenses') {
                const activeTab = document.querySelector('.expense-tab.active')?.getAttribute('data-expense-tab') || 'lifetime';
                let tableId = '';
                if (activeTab === 'lifetime') tableId = 'expenseLifetimeTableBody';
                else if (activeTab === 'current') tableId = 'expenseCurrentTableBody';
                else tableId = 'expensePreviousTableBody';
                const rows = document.querySelectorAll(`#${tableId} tr`);
                rows.forEach(row => {
                    const cells = row.querySelectorAll('td');
                    if (cells.length > 0) {
                        data.push({
                            'তারিখ': cells[0]?.innerText || '',
                            'বিবরণ': cells[1]?.innerText || '',
                            'পরিমাণ': cells[2]?.innerText || '',
                            'ধরন': cells[3]?.innerText || ''
                        });
                    }
                });
                filename = `expenses_${activeTab}_data`;
            } else if (type === 'events') {
                const rows = document.querySelectorAll('#eventsTableBody tr');
                rows.forEach(row => {
                    const cells = row.querySelectorAll('td');
                    if (cells.length > 0) {
                        data.push({
                            'ইভেন্ট': cells[0]?.innerText || '',
                            'তারিখ': cells[1]?.innerText || '',
                            'বাজেট': cells[2]?.innerText || '',
                            'স্ট্যাটাস': cells[3]?.innerText || '',
                            'সংগৃহীত': cells[4]?.innerText || '',
                            'খরচ': cells[5]?.innerText || ''
                        });
                    }
                });
                filename = 'events_data';
            }
            const ws = XLSX.utils.json_to_sheet(data);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, 'Sheet1');
            XLSX.writeFile(wb, `${filename}.xlsx`);
        });
    };

    window.searchMembers = () => {
        const searchTerm = document.getElementById('memberSearchInput').value.toLowerCase();
        const rows = document.querySelectorAll('#membersTableBody tr');
        let hasResults = false;
        rows.forEach(row => {
            const text = row.innerText.toLowerCase();
            if (text.includes(searchTerm)) { row.style.display = ''; hasResults = true; }
            else { row.style.display = 'none'; }
        });
        if (!hasResults && rows.length > 0 && !document.querySelector('.no-results-row')) {
            const noResultRow = document.createElement('tr');
            noResultRow.innerHTML = `<td colspan="6" class="no-results">কোন সদস্য পাওয়া যায়নি</td>`;
            document.getElementById('membersTableBody').appendChild(noResultRow);
            noResultRow.classList.add('no-results-row');
        } else if (hasResults) {
            const noResultRow = document.querySelector('.no-results-row');
            if (noResultRow) noResultRow.remove();
        }
    };

    // Global variables for calculations
    let totalFunds = 0;
    let totalExpensesAmount = 0;

    // Donations Listener - Updates totalFunds
    onSnapshot(collection(db, "donations"), (snap) => {
        totalFunds = 0;
        let monthlyFunds = 0;
        let eventFunds = 0;
        let currentMonthTotal = 0;
        let previousMonthTotal = 0;
        
        let lifetimeHtml = `<table class="table"><thead><tr><th>তারিখ</th><th>সদস্য</th><th>পরিমাণ</th><th>ধরন</th><th>পদ্ধতি</th><th>অ্যাকশন</th></tr></thead><tbody id="lifetimeTableBody">`;
        let currentHtml = `<table class="table"><thead><tr><th>তারিখ</th><th>সদস্য</th><th>পরিমাণ</th><th>ধরন</th><th>পদ্ধতি</th><th>অ্যাকশন</th></tr></thead><tbody id="currentTableBody">`;
        let previousHtml = `<table class="table"><thead><tr><th>তারিখ</th><th>সদস্য</th><th>পরিমাণ</th><th>ধরন</th><th>পদ্ধতি</th><th>অ্যাকশন</th></tr></thead><tbody id="previousTableBody">`;
        
        const currentMonthNum = new Date().getMonth();
        const currentYearNum = new Date().getFullYear();
        const previousMonthNum = currentMonthNum === 0 ? 11 : currentMonthNum - 1;
        const previousYearNum = currentMonthNum === 0 ? currentYearNum - 1 : currentYearNum;
        
        function isCurrentMonth(dateStr) { 
            if (!dateStr) return false; 
            const date = new Date(dateStr); 
            return !isNaN(date.getTime()) && date.getMonth() === currentMonthNum && date.getFullYear() === currentYearNum; 
        }
        
        function isPreviousMonth(dateStr) { 
            if (!dateStr) return false; 
            const date = new Date(dateStr); 
            return !isNaN(date.getTime()) && date.getMonth() === previousMonthNum && date.getFullYear() === previousYearNum; 
        }
        
        snap.forEach(doc => {
            const d = doc.data();
            const amount = Number(d.amount) || 0;
            totalFunds += amount;
            
            if (d.type === 'monthly') { 
                if (isCurrentMonth(d.date)) { 
                    monthlyFunds += amount; 
                    currentMonthTotal += amount; 
                } 
                if (isPreviousMonth(d.date)) { 
                    previousMonthTotal += amount; 
                } 
            } else if (d.type === 'event') { 
                eventFunds += amount; 
            }
            
            const typeBadge = d.type === 'monthly' ? '<span class="badge-add">মাসিক</span>' : '<span class="badge-add">ইভেন্ট</span>';
            let methodClass = '', methodText = d.system || '-';
            if (d.system === 'Bkash') { methodClass = 'bkash-text'; methodText = 'বিকাশ'; }
            else if (d.system === 'Nagad') { methodClass = 'nagad-text'; methodText = 'নগদ'; }
            else if (d.system === 'HandCash') { methodClass = 'handcash-text'; methodText = 'হ্যান্ড ক্যাশ'; }
            
            const row = `<tr><td>${d.date || '-'}</td><td><strong class="uid-text">${d.uid || 'অতিথি'}</strong><br><span class="name-text">${d.name || ''}</span><br><small class="text-muted">${d.phone || ''}</small></td><td style="font-weight:bold">৳${amount}</td><td>${typeBadge}${d.eventName ? `<br><small>${d.eventName}</small>` : ''}</td><td class="${methodClass}">${methodText}</td><td><button class="btn btn-sm btn-outline-warning me-1" onclick='openDonationForm(${JSON.stringify({id:doc.id,...d})})'><i class="fas fa-edit"></i></button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('donations','${doc.id}')"><i class="fas fa-trash"></i></button></td></tr>`;
            lifetimeHtml += row;
            if (isCurrentMonth(d.date)) currentHtml += row;
            if (isPreviousMonth(d.date)) previousHtml += row;
        });
        
        lifetimeHtml += `</tbody></table>`; 
        currentHtml += `</tbody></table>`; 
        previousHtml += `</tbody></table>`;
        
        document.getElementById('lifetimeDonationList').innerHTML = lifetimeHtml; 
        document.getElementById('currentDonationList').innerHTML = currentHtml; 
        document.getElementById('previousDonationList').innerHTML = previousHtml;
        document.getElementById('lifetimeSummary').innerHTML = `৳${totalFunds}`; 
        document.getElementById('currentSummary').innerHTML = `৳${currentMonthTotal}`; 
        document.getElementById('previousSummary').innerHTML = `৳${previousMonthTotal}`;
        document.getElementById('totalFund').innerHTML = `৳${totalFunds}`; 
        document.getElementById('monthlyCollection').innerHTML = `৳${monthlyFunds}`; 
        document.getElementById('eventFundCollection').innerHTML = `৳${eventFunds}`;
        
        // Update net balance with latest expenses
        document.getElementById('netBalance').innerHTML = `৳${totalFunds - totalExpensesAmount}`;
    });

    // Expenses Listener - Updates totalExpensesAmount
    onSnapshot(collection(db, "expenses"), (snap) => {
        totalExpensesAmount = 0;
        let expenseCurrentMonthTotal = 0;
        let expensePreviousMonthTotal = 0;
        
        let lifetimeHtml = `<table class="table"><thead><tr><th>তারিখ</th><th>বিবরণ</th><th>পরিমাণ</th><th>ধরন</th><th>অ্যাকশন</th></tr></thead><tbody id="expenseLifetimeTableBody">`;
        let currentHtml = `<table class="table"><thead><tr><th>তারিখ</th><th>বিবরণ</th><th>পরিমাণ</th><th>ধরন</th><th>অ্যাকশন</th></tr></thead><tbody id="expenseCurrentTableBody">`;
        let previousHtml = `<table class="table"><thead><tr><th>তারিখ</th><th>বিবরণ</th><th>পরিমাণ</th><th>ধরন</th><th>অ্যাকশন</th></tr></thead><tbody id="expensePreviousTableBody">`;
        
        const currentMonthNum = new Date().getMonth();
        const currentYearNum = new Date().getFullYear();
        const previousMonthNum = currentMonthNum === 0 ? 11 : currentMonthNum - 1;
        const previousYearNum = currentMonthNum === 0 ? currentYearNum - 1 : currentYearNum;
        
        function isCurrentMonth(dateStr) { 
            if (!dateStr) return false; 
            const date = new Date(dateStr); 
            return !isNaN(date.getTime()) && date.getMonth() === currentMonthNum && date.getFullYear() === currentYearNum; 
        }
        
        function isPreviousMonth(dateStr) { 
            if (!dateStr) return false; 
            const date = new Date(dateStr); 
            return !isNaN(date.getTime()) && date.getMonth() === previousMonthNum && date.getFullYear() === previousYearNum; 
        }
        
        snap.forEach(doc => {
            const e = doc.data();
            const amount = Number(e.amount) || 0;
            totalExpensesAmount += amount;
            if (isCurrentMonth(e.date)) expenseCurrentMonthTotal += amount;
            if (isPreviousMonth(e.date)) expensePreviousMonthTotal += amount;
            
            const typeBadge = e.type === 'monthly' ? '<span class="badge-subtract">মাসিক</span>' : '<span class="badge-subtract">ইভেন্ট</span>';
            const row = `<tr><td>${e.date || '-'}</td><td>${e.description}${e.eventName ? `<br><small>${e.eventName}</small>` : ''}</td><td style="font-weight:bold">৳${amount}</td><td>${typeBadge}</td><td><button class="btn btn-sm btn-outline-warning me-1" onclick='openExpenseForm(${JSON.stringify({id:doc.id,...e})})'><i class="fas fa-edit"></i></button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('expenses','${doc.id}')"><i class="fas fa-trash"></i></button></td></tr>`;
            lifetimeHtml += row;
            if (isCurrentMonth(e.date)) currentHtml += row;
            if (isPreviousMonth(e.date)) previousHtml += row;
        });
        
        lifetimeHtml += `</tbody></table>`; 
        currentHtml += `</tbody></table>`; 
        previousHtml += `</tbody></table>`;
        
        document.getElementById('expenseLifetimeList').innerHTML = lifetimeHtml; 
        document.getElementById('expenseCurrentList').innerHTML = currentHtml; 
        document.getElementById('expensePreviousList').innerHTML = previousHtml;
        document.getElementById('expenseLifetimeSummary').innerHTML = `৳${totalExpensesAmount}`; 
        document.getElementById('expenseCurrentSummary').innerHTML = `৳${expenseCurrentMonthTotal}`; 
        document.getElementById('expensePreviousSummary').innerHTML = `৳${expensePreviousMonthTotal}`;
        document.getElementById('monthlyExpenses').innerHTML = `৳${expenseCurrentMonthTotal}`; 
        document.getElementById('totalExpenses').innerHTML = `৳${totalExpensesAmount}`;
        
        // Update net balance with latest donations
        document.getElementById('netBalance').innerHTML = `৳${totalFunds - totalExpensesAmount}`;
    });

    // Members Listener
    onSnapshot(collection(db, "members"), (snap) => {
        currentMembersData = [];
        let html = `<table class="table"><thead><tr><th>আইডি</th><th>নাম</th><th>পদবি</th><th>ব্লাড</th><th>যোগাযোগ</th><th>অ্যাকশন</th></tr></thead><tbody id="membersTableBody">`;
        snap.forEach(doc => {
            const m = doc.data();
            currentMembersData.push({ id: doc.id, ...m });
            const phoneDisplay = m.phoneNumbers ? m.phoneNumbers.join(', ') : (m.phone || '-');
            html += `<tr><td class="uid-text" style="font-weight:bold">${m.uid || '-'}</td><td class="name-text">${m.name}</td><td>${m.designation || '-'}</td><td class="blood-text"><span class="badge bg-danger">${m.blood || '-'}</span></td><td>${phoneDisplay}<br><small>${m.email || ''}</small></td><td><button class="btn btn-sm btn-outline-warning me-1" onclick='openMemberForm(${JSON.stringify({id:doc.id,...m})})'><i class="fas fa-edit"></i></button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('members','${doc.id}')"><i class="fas fa-trash"></i></button></td></tr>`;
        });
        html += `</tbody></table>`;
        document.getElementById('memberList').innerHTML = html;
    });

    // Events Listener
    onSnapshot(collection(db, "events"), (snap) => {
        let planningHtml = `<table class="table"><thead><tr><th>ইভেন্ট</th><th>তারিখ</th><th>বাজেট</th><th>স্ট্যাটাস</th><th>সংগৃহীত</th><th>খরচ</th><th>অ্যাকশন</th></tr></thead><tbody id="eventsTableBody">`;
        snap.forEach(doc => {
            const e = doc.data();
            let statusBadge = '';
            if (e.status === 'successful') statusBadge = '<span class="status-success"><i class="fas fa-check-circle"></i> সফল</span>';
            else if (e.status === 'failed') statusBadge = '<span class="status-failed"><i class="fas fa-times-circle"></i> ব্যর্থ</span>';
            else statusBadge = '<span class="status-pending"><i class="fas fa-clock"></i> পেন্ডিং</span>';
            planningHtml += `<tr><td><strong>${e.name}</strong><br><small>${e.details || ''}</small></td><td>${e.date || '-'}</td><td style="font-weight:bold">৳${e.budget || 0}</td><td>${statusBadge}</td><td style="font-weight:bold">৳${e.fund || 0}</td><td style="font-weight:bold">৳${e.cost || 0}</td><td><button class="btn btn-sm btn-outline-warning me-1" onclick='openEventForm(${JSON.stringify({id:doc.id,...e})})'><i class="fas fa-edit"></i></button><button class="btn btn-sm btn-outline-danger" onclick="deleteItem('events','${doc.id}')"><i class="fas fa-trash"></i></button></td></tr>`;
        });
        planningHtml += `</tbody></table>`;
        document.getElementById('planningList').innerHTML = planningHtml;
    });

    function initDonationTabs() {
        const tabs = document.querySelectorAll('.chrome-tab:not(.expense-tab)');
        tabs.forEach(tab => {
            tab.addEventListener('click', () => {
                tabs.forEach(t => t.classList.remove('active'));
                tab.classList.add('active');
                document.getElementById('lifetimeTab').style.display = 'none';
                document.getElementById('currentTab').style.display = 'none';
                document.getElementById('previousTab').style.display = 'none';
                const tabName = tab.getAttribute('data-tab');
                if (tabName === 'lifetime') document.getElementById('lifetimeTab').style.display = 'block';
                else if (tabName === 'current') document.getElementById('currentTab').style.display = 'block';
                else if (tabName === 'previous') document.getElementById('previousTab').style.display = 'block';
            });
        });
    }

    function initExpenseTabs() {
        const tabs = document.querySelectorAll('.expense-tab');
        tabs.forEach(tab => {
            tab.addEventListener('click', () => {
                tabs.forEach(t => t.classList.remove('active'));
                tab.classList.add('active');
                document.getElementById('expenseLifetimeTab').style.display = 'none';
                document.getElementById('expenseCurrentTab').style.display = 'none';
                document.getElementById('expensePreviousTab').style.display = 'none';
                const tabName = tab.getAttribute('data-expense-tab');
                if (tabName === 'lifetime') document.getElementById('expenseLifetimeTab').style.display = 'block';
                else if (tabName === 'current') document.getElementById('expenseCurrentTab').style.display = 'block';
                else if (tabName === 'previous') document.getElementById('expensePreviousTab').style.display = 'block';
            });
        });
    }

    setTimeout(() => { initDonationTabs(); initExpenseTabs(); }, 500);
</script>

</body>
</html>
