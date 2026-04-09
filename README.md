
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
        #sidebar { min-width: 250px; max-width: 250px; background: #212529; color: #fff; min-height: 100vh; transition: all 0.3s; }
        #sidebar .sidebar-header { padding: 20px; background: #1a1d20; }
        #sidebar ul.components { padding: 20px 0; border-bottom: 1px solid #47748b; }
        #sidebar ul li a { padding: 10px 20px; display: block; color: #adb5bd; text-decoration: none; }
        #sidebar ul li a:hover { color: #fff; background: #343a40; }
        .card { border: none; border-radius: 10px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); transition: transform 0.2s; }
        .card:hover { transform: translateY(-5px); }
        .stat-icon { font-size: 2rem; opacity: 0.3; }
    </style>
</head>
<body>

<div id="wrapper">
    <nav id="sidebar">
        <div class="sidebar-header">
            <h3>IYSO ERP</h3>
        </div>
        <ul class="list-unstyled components">
            <li><a href="#"><i class="fas fa-home me-2"></i> Dashboard</a></li>
            <li><a href="#"><i class="fas fa-users me-2"></i> Members</a></li>
            <li><a href="#"><i class="fas fa-calendar-alt me-2"></i> Schedules</a></li>
            <li><a href="#"><i class="fas fa-tshirt me-2"></i> Inventory (Jerseys)</a></li>
            <li><a href="#"><i class="fas fa-chart-line me-2"></i> Reports</a></li>
            <li><a href="#"><i class="fas fa-cog me-2"></i> Settings</a></li>
        </ul>
    </nav>

    <div id="content" class="w-100">
        <nav class="navbar navbar-expand-lg navbar-light bg-white border-bottom p-3">
            <div class="container-fluid">
                <span class="navbar-brand">Organization Overview</span>
                <div class="ms-auto">
                    <i class="fas fa-bell me-3"></i>
                    <img src="https://via.placeholder.com/35" class="rounded-circle" alt="User">
                </div>
            </div>
        </nav>

        <div class="container-fluid p-4">
            <div class="row mb-4">
                <div class="col-md-3">
                    <div class="card p-3 bg-primary text-white">
                        <div class="d-flex justify-content-between">
                            <div><h5>Members</h5><h3>124</h3></div>
                            <i class="fas fa-user-friends stat-icon"></i>
                        </div>
                    </div>
                </div>
                <div class="col-md-3">
                    <div class="card p-3 bg-success text-white">
                        <div class="d-flex justify-content-between">
                            <div><h5>Active Projects</h5><h3>8</h3></div>
                            <i class="fas fa-tasks stat-icon"></i>
                        </div>
                    </div>
                </div>
            </div>

            <div class="card p-4">
                <h5 class="mb-3">Recent Activities</h5>
                <table class="table table-hover">
                    <thead class="table-light">
                        <tr>
                            <th>Date</th>
                            <th>Member</th>
                            <th>Action</th>
                            <th>Status</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>2026-04-09</td>
                            <td>Nahid Khan</td>
                            <td>Updated Jersey Design</td>
                            <td><span class="badge bg-info">Completed</span></td>
                        </tr>
                        <tr>
                            <td>2026-04-08</td>
                            <td>Admin</td>
                            <td>New Schedule Uploaded</td>
                            <td><span class="badge bg-warning">Pending</span></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
