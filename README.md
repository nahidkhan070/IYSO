
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IYSO | Admin ERP</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        body { background-color: #f8f9fa; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        #wrapper { display: flex; align-items: stretch; }
        
        /* Sidebar Styling */
        #sidebar { min-width: 250px; max-width: 250px; background: #212529; color: #fff; min-height: 100vh; transition: all 0.3s; }
        #sidebar .sidebar-header { padding: 25px 20px; background: #1a1d20; text-align: center; }
        
        /* Sidebar Logo (PNG) */
        #sidebar .sidebar-header img { 
            max-width: 130px; 
            height: auto; 
            /* Optional: subtle drop shadow to help logo pop on dark background */
            filter: drop-shadow(0px 4px 4px rgba(0,0,0,0.5));
        }

        #sidebar ul.components { padding: 20px 0; }
        #sidebar ul li a { padding: 12px 20px; display: block; color: #adb5bd; text-decoration: none; font-weight: 500; }
        #sidebar ul li a:hover { color: #fff; background: #343a40; border-left: 4px solid #198754; }
        
        /* Navbar Styling */
        .navbar { box-shadow: 0 2px 10px rgba(0,0,0,0.05); }
        .navbar-brand img { max-height: 45px; width: auto; margin-right: 12px; }

        /* User Profile Image from Unsplash */
        .user-profile-img {
            width: 42px;
            height: 42px;
            object-fit: cover;
            border-radius: 50%;
            border: 2px solid #e9ecef;
        }

        /* Card Styling */
        .card { border: none; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.08); transition: all 0.3s ease; }
        .card:hover { transform: translateY(-5px); box-shadow: 0 8px 15px rgba(0,0,0,0.1); }
        .stat-icon { font-size: 2.2rem; opacity: 0.2; }
    </style>
</head>
<body>

<div id="wrapper">
    <nav id="sidebar">
        <div class="sidebar-header border-bottom border-secondary">
            <img src="image_0.png" alt="IYSO Logo">
            <h6 class="mt-3 text-uppercase tracking-wider">Control Center</h6>
        </div>
        <ul class="list-unstyled components">
            <li><a href="#"><i class="fas fa-th-large me-2"></i> Dashboard</a></li>
            <li><a href="#"><i class="fas fa-users me-2"></i> Member Directory</a></li>
            <li><a href="#"><i class="fas fa-clock me-2"></i> Schedules</a></li>
            <li><a href="#"><i class="fas fa-box-open me-2"></i> Inventory</a></li>
            <li><a href="#"><i class="fas fa-file-invoice-dollar me-2"></i> Finance</a></li>
            <li class="mt-4 px-3 text-muted small text-uppercase">Admin</li>
            <li><a href="#"><i class="fas fa-cog me-2"></i> Settings</a></li>
        </ul>
    </nav>

    <div id="content" class="w-100">
        <nav class="navbar navbar-expand-lg navbar-light bg-white p-3">
            <div class="container-fluid">
                <a class="navbar-brand d-flex align-items-center fw-bold" href="#">
                    <img src="image_0.png" alt="IYSO Logo">
                    <span>IYSO <span class="text-success">ERP</span></span>
                </a>
                <div class="ms-auto d-flex align-items-center">
                    <div class="me-3 text-end d-none d-md-block">
                        <div class="fw-bold small">Nahid Khan</div>
                        <div class="text-muted" style="font-size: 0.75rem;">Super Admin</div>
                    </div>
                    <img src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?q=80&w=100&auto=format&fit=crop" 
                         class="user-profile-img" alt="Profile">
                </div>
            </div>
        </nav>

        <div class="container-fluid p-4">
            <div class="row g-4 mb-4">
                <div class="col-md-4">
                    <div class="card p-4 border-start border-primary border-5">
                        <div class="d-flex justify-content-between align-items-center">
                            <div><p class="text-muted mb-0">Total Members</p><h2 class="fw-bold">1,240</h2></div>
                            <i class="fas fa-users stat-icon text-primary"></i>
                        </div>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="card p-4 border-start border-success border-5">
                        <div class="d-flex justify-content-between align-items-center">
                            <div><p class="text-muted mb-0">Active Events</p><h2 class="fw-bold">12</h2></div>
                            <i class="fas fa-calendar-check stat-icon text-success"></i>
                        </div>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="card p-4 border-start border-warning border-5">
                        <div class="d-flex justify-content-between align-items-center">
                            <div><p class="text-muted mb-0">New Requests</p><h2 class="fw-bold">45</h2></div>
                            <i class="fas fa-bell stat-icon text-warning"></i>
                        </div>
                    </div>
                </div>
            </div>

            <div class="card border-0 shadow-sm p-4">
                <div class="d-flex justify-content-between align-items-center mb-4">
                    <h5 class="fw-bold">Organization Logs</h5>
                    <button class="btn btn-sm btn-outline-primary">View All</button>
                </div>
                <div class="table-responsive">
                    <table class="table table-hover align-middle">
                        <thead class="bg-light">
                            <tr>
                                <th class="border-0">User</th>
                                <th class="border-0">Activity</th>
                                <th class="border-0">Status</th>
                                <th class="border-0">Time</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td><strong>Nahid Khan</strong></td>
                                <td>Published Monthly Schedule</td>
                                <td><span class="badge rounded-pill bg-success-subtle text-success border border-success">Live</span></td>
                                <td class="text-muted">2 mins ago</td>
                            </tr>
                            <tr>
                                <td><strong>System</strong></td>
                                <td>Database Backup</td>
                                <td><span class="badge rounded-pill bg-info-subtle text-info border border-info">Auto</span></td>
                                <td class="text-muted">1 hour ago</td>
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
