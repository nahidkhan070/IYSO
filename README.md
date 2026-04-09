
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IYSO | Official Portal</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --iyso-green: #006837; /* From your logo */
            --iyso-gold: #c6a34f;  /* From the star/crescent */
            --dark-bg: #0b0f13;
            --glass: rgba(255, 255, 255, 0.05);
        }

        body {
            background-color: var(--dark-bg);
            color: #ffffff;
            font-family: 'Plus Jakarta Sans', sans-serif;
            overflow-x: hidden;
        }

        /* Premium Navbar */
        .navbar {
            background: rgba(11, 15, 19, 0.8);
            backdrop-filter: blur(15px);
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .navbar-brand img { height: 50px; }

        /* Sidebar Navigation */
        .nav-link {
            color: #adb5bd;
            font-weight: 500;
            transition: 0.3s;
            border-radius: 8px;
            margin-bottom: 5px;
        }

        .nav-link:hover, .nav-link.active {
            color: #fff;
            background: var(--iyso-green);
        }

        /* Glass Cards */
        .premium-card {
            background: var(--glass);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 20px;
            backdrop-filter: blur(10px);
            padding: 25px;
            transition: 0.4s ease;
        }

        .premium-card:hover {
            border-color: var(--iyso-gold);
            transform: translateY(-5px);
        }

        /* Member Profile Styles */
        .profile-img {
            width: 80px; height: 80px;
            border-radius: 50%;
            border: 3px solid var(--iyso-gold);
            object-fit: cover;
        }

        .status-badge {
            font-size: 0.7rem;
            padding: 5px 12px;
            border-radius: 50px;
            background: rgba(0, 104, 55, 0.2);
            color: #00ff88;
            border: 1px solid #00ff88;
        }

        .finance-up { color: #00ff88; }
        .finance-down { color: #ff4d4d; }

    </style>
</head>
<body>

<nav class="navbar navbar-expand-lg sticky-top">
    <div class="container">
        <a class="navbar-brand d-flex align-items-center" href="#">
            <img src="image_0.png" alt="Logo">
            <div class="ms-3">
                <span class="d-block fw-bold mb-0" style="letter-spacing: 2px;">IYSO</span>
                <small class="text-muted" style="font-size: 0.6rem;">IDEAL YOUTH SERVICE ORGANIZATION</small>
            </div>
        </a>
        <div class="ms-auto d-flex align-items-center">
            <span class="me-3 d-none d-md-block small text-muted">Welcome, <b>Nahid Khan</b></span>
            <img src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=100" class="rounded-circle border border-secondary" height="40" width="40">
        </div>
    </div>
</nav>

<div class="container mt-5">
    <div class="row">
        <div class="col-lg-3 mb-4">
            <div class="premium-card sticky-top" style="top: 100px;">
                <nav class="nav flex-column">
                    <a class="nav-link active" href="#"><i class="fas fa-chart-pie me-2"></i> Overview</a>
                    <a class="nav-link" href="#"><i class="fas fa-user-group me-2"></i> Member Directory</a>
                    <a class="nav-link" href="#"><i class="fas fa-file-invoice-dollar me-2"></i> Finance Section</a>
                    <a class="nav-link" href="#"><i class="fas fa-calendar-days me-2"></i> Schedules</a>
                    <a class="nav-link" href="#"><i class="fas fa-trophy me-2"></i> Events</a>
                    <hr class="text-secondary">
                    <a class="nav-link" href="#"><i class="fas fa-gear me-2"></i> Admin Settings</a>
                </nav>
            </div>
        </div>

        <div class="col-lg-9">
            
            <div class="row g-4 mb-5">
                <div class="col-md-4">
                    <div class="premium-card text-center">
                        <h6 class="text-muted">Current Balance</h6>
                        <h2 class="fw-bold finance-up">$4,250.00</h2>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="premium-card text-center">
                        <h6 class="text-muted">Active Members</h6>
                        <h2 class="fw-bold" style="color: var(--iyso-gold);">128</h2>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="premium-card text-center">
                        <h6 class="text-muted">Next Event</h6>
                        <h2 class="fw-bold">14 Days</h2>
                    </div>
                </div>
            </div>

            <h4 class="mb-4 fw-bold"><i class="fas fa-user-circle me-2 text-success"></i> Leadership Profiles</h4>
            <div class="row g-4 mb-5">
                <div class="col-md-6">
                    <div class="premium-card d-flex align-items-center">
                        <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=100" class="profile-img me-3">
                        <div>
                            <span class="status-badge">Super Admin</span>
                            <h5 class="mb-0 mt-2">Nahid Khan</h5>
                            <small class="text-muted">Organization Lead</small>
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="premium-card d-flex align-items-center">
                        <img src="https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=100" class="profile-img me-3">
                        <div>
                            <span class="status-badge" style="border-color: #00d2ff; color: #00d2ff;">Secretary</span>
                            <h5 class="mb-0 mt-2">Sarah Ahmed</h5>
                            <small class="text-muted">Operations Manager</small>
                        </div>
                    </div>
                </div>
            </div>

            <div class="premium-card">
                <div class="d-flex justify-content-between mb-4">
                    <h5 class="fw-bold">Recent Finance Activity</h5>
                    <button class="btn btn-sm btn-outline-success">Export PDF</button>
                </div>
                <div class="table-responsive">
                    <table class="table table-dark table-hover border-0">
                        <thead>
                            <tr class="text-muted">
                                <th>Transaction</th>
                                <th>Category</th>
                                <th>Amount</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Jersey Production</td>
                                <td>Inventory</td>
                                <td class="finance-down">-$500.00</td>
                                <td><span class="badge bg-secondary">Paid</span></td>
                            </tr>
                            <tr>
                                <td>Monthly Donation</td>
                                <td>Revenue</td>
                                <td class="finance-up">+$1,200.00</td>
                                <td><span class="badge bg-success">Received</span></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

        </div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
