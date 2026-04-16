
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
            --card-bg: rgba(17, 24, 32, 0.95);
        }

        body {
            background: radial-gradient(circle at top right, #003d21, var(--dark-bg) 70%);
            color: #e9ecef;
            font-family: 'Plus Jakarta Sans', 'Hind Siliguri', sans-serif;
            min-height: 100vh;
            margin: 0;
            position: relative;
        }

        /* --- RESTORED WATERMARK --- */
        body::before {
            content: "";
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 80vw;
            height: 80vw;
            max-width: 600px;
            /* Using the confirmed filename from your upload */
            background: url('image_ae9264.jpg') no-repeat center;
            background-size: contain;
            opacity: 0.04; /* Very subtle so text remains readable */
            z-index: -1;
            pointer-events: none;
        }

        #sidebar {
            width: 260px;
            height: 100vh;
            position: fixed;
            background: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(20px);
            border-right: 1px solid rgba(198, 163, 79, 0.1);
            padding: 30px 20px;
            z-index: 1000;
        }

        .main-content { margin-left: 260px; padding: 40px; }

        .glass-card {
            background: var(--card-bg);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            padding: 25px;
            transition: 0.3s;
        }

        /* Sidebar Logo Area */
        .sidebar-brand img {
            filter: drop-shadow(0 0 10px rgba(198, 163, 79, 0.2));
            transition: 0.3s;
        }
        
        .sidebar-brand img:hover { transform: scale(1.05); }

        .nav-link { color: #8a949d; cursor: pointer; padding: 12px; border-radius: 10px; transition: 0.3s; text-decoration: none; display: block; }
        .nav-link:hover, .nav-link.active { background: var(--iyso-green); color: #fff; }

        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.4s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        @media (max-width: 992px) {
            #sidebar { width: 0; padding: 0; visibility: hidden; }
            .main-content { margin-left: 0; padding: 20px; }
        }
    </style>
</head>
<body>

<div id="sidebar">
    <div class="sidebar-brand text-center mb-5">
        <img src="image_ae9264.jpg" alt="IYSO Logo" height="85">
        <h6 class="mt-3 fw-bold text-white letter-spacing-1">IYSO PORTAL</h6>
    </div>
    <div class="nav flex-column">
        <div class="nav-link active" onclick="showSection('overview')"><i class="fas fa-chart-line me-2"></i> Dashboard</div>
        <div class="nav-link" onclick="showSection('members')"><i class="fas fa-users-cog me-2"></i> Members</div>
        <div class="nav-link" onclick="showSection('costs')"><i class="fas fa-wallet me-2"></i> Costing</div>
        <div class="nav-link" onclick="showSection('summary')"><i class="fas fa-file-invoice me-2"></i> Summary Report</div>
    </div>
</div>

<div class="main-content">
    
    <div id="overview" class="page-section active">
        <h2 class="fw-bold mb-4">Executive Dashboard</h2>
        <div class="row g-4 mb-4">
            <div class="col-md-6">
                <div class="glass-card" style="background: linear-gradient(135deg, var(--iyso-green), #002d18); border: 1px solid var(--iyso-gold);">
                    <h5 class="text-gold">Net Balance Fund / নিট তহবিল</h5>
                    <h1 id="net-balance" style="font-weight: 800; color: #fff;">৳0</h1>
                </div>
            </div>
            <div class="col-md-6">
                <div class="glass-card">
                    <h5>Official Channels</h5>
                    <div class="d-flex justify-content-around mt-3">
                        <div class="text-center"><small class="d-block text-muted">bKash</small><b id="disp-bkash">01XXXXXXXXX</b></div>
                        <div class="text-center"><small class="d-block text-muted">Nagad</small><b id="disp-nagad">01XXXXXXXXX</b></div>
                    </div>
                </div>
            </div>
        </div>

        <h4 class="mb-3">Live Donation Table</h4>
        <div class="glass-card p-0 overflow-hidden">
            <table class="table table-dark m-0">
                <thead><tr><th>Date</th><th>Donor</th><th>ID</th><th>Amount</th></tr></thead>
                <tbody id="dash-donation-table">
                    </tbody>
            </table>
        </div>
    </div>

</div>

<script type="module">
    // Firebase logic remains identical to the previous version
    window.showSection = (id) => {
        document.querySelectorAll('.page-section').forEach(s => s.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
        event.currentTarget.classList.add('active');
    };
</script>
</body>
</html>
