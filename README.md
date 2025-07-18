<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JSPL Employee Management System</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --jspl-blue: #0055a4;
            --jspl-red: #c8102e;
            --jspl-accent: #ffc72c;
            --dark: #1a2e4a;
            --light: #f5f7fa;
            --success: #28a745;
            --danger: #dc3545;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f0f2f5;
            color: #333;
            height: 100vh;
            overflow: hidden;
        }
        
        .login-container {
            background: linear-gradient(135deg, var(--jspl-blue) 0%, #003a75 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        
        .login-card {
            background: white;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 450px;
            overflow: hidden;
            animation: fadeIn 0.5s ease-in-out;
        }
        
        .login-header {
            background: var(--jspl-blue);
            color: white;
            padding: 25px 20px;
            text-align: center;
            position: relative;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .jspl-logo {
            width: 120px;
            height: 120px;
            background: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }
        
        .jspl-logo-inner {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background: var(--jspl-red);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 1.5rem;
            text-align: center;
            line-height: 1.2;
        }
        
        .login-body {
            padding: 30px;
            position: relative;
            z-index: 2;
        }
        
        .form-control:focus {
            border-color: var(--jspl-blue);
            box-shadow: 0 0 0 0.2rem rgba(0, 85, 164, 0.25);
        }
        
        .btn-login {
            background: var(--jspl-blue);
            color: white;
            font-weight: 600;
            padding: 10px;
            transition: all 0.3s;
            border: none;
        }
        
        .btn-login:hover {
            background: #004080;
            transform: translateY(-2px);
        }
        
        /* Dashboard Styles */
        .dashboard-container {
            display: flex;
            min-height: 100vh;
        }
        
        .sidebar {
            width: 250px;
            background: var(--dark);
            color: white;
            min-height: 100vh;
            box-shadow: 3px 0 10px rgba(0, 0, 0, 0.1);
            transition: all 0.3s;
            z-index: 100;
            position: fixed;
            left: 0;
            top: 0;
            bottom: 0;
        }
        
        .sidebar-header {
            padding: 20px 15px;
            background: rgba(0, 0, 0, 0.2);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            align-items: center;
        }
        
        .sidebar-logo {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: white;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 10px;
            flex-shrink: 0;
        }
        
        .sidebar-logo-inner {
            width: 32px;
            height: 32px;
            border-radius: 50%;
            background: var(--jspl-red);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 0.8rem;
            text-align: center;
            line-height: 1;
        }
        
        .nav-link {
            color: rgba(255, 255, 255, 0.8);
            padding: 12px 20px;
            border-left: 3px solid transparent;
            transition: all 0.2s;
            display: flex;
            align-items: center;
        }
        
        .nav-link:hover, .nav-link.active {
            background: rgba(255, 255, 255, 0.1);
            color: white;
            border-left: 3px solid var(--jspl-accent);
        }
        
        .nav-link i {
            margin-right: 10px;
            width: 20px;
            text-align: center;
            font-size: 18px;
        }
        
        .main-content {
            flex: 1;
            overflow-x: hidden;
            margin-left: 250px;
            background: var(--light);
            min-height: 100vh;
        }
        
        .topbar {
            background: white;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
            padding: 15px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 99;
            position: sticky;
            top: 0;
            border-bottom: 3px solid var(--jspl-blue);
        }
        
        .breadcrumb {
            background: transparent;
            margin-bottom: 0;
            padding: 0;
            font-size: 0.9rem;
        }
        
        .breadcrumb-item a {
            color: var(--jspl-blue);
            text-decoration: none;
            font-weight: 500;
        }
        
        .user-info {
            display: flex;
            align-items: center;
        }
        
        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--jspl-blue) 0%, var(--jspl-red) 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            margin-left: 15px;
            font-weight: bold;
            color: white;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        
        .content-area {
            padding: 25px;
            height: calc(100vh - 70px);
            overflow-y: auto;
        }
        
        .section-title {
            color: var(--jspl-blue);
            border-bottom: 2px solid var(--jspl-blue);
            padding-bottom: 10px;
            margin-bottom: 25px;
            font-weight: 600;
            position: relative;
        }
        
        .section-title::after {
            content: "";
            position: absolute;
            left: 0;
            bottom: -2px;
            width: 80px;
            height: 2px;
            background: var(--jspl-accent);
        }
        
        .card {
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
            border: none;
            margin-bottom: 25px;
            transition: transform 0.3s;
            border-top: 3px solid var(--jspl-blue);
        }
        
        .card:hover {
            transform: translateY(-5px);
        }
        
        .card-header {
            background: white;
            border-bottom: 1px solid #eaeaea;
            font-weight: 600;
            padding: 15px 20px;
            border-radius: 10px 10px 0 0 !important;
            color: var(--jspl-blue);
            display: flex;
            align-items: center;
        }
        
        .card-header i {
            margin-right: 10px;
            color: var(--jspl-accent);
        }
        
        .form-section {
            margin-bottom: 30px;
        }
        
        .form-label {
            font-weight: 500;
            color: #555;
            margin-bottom: 5px;
        }
        
        .btn-primary {
            background: var(--jspl-blue);
            border: none;
            padding: 10px 25px;
            font-weight: 600;
            transition: all 0.3s;
        }
        
        .btn-primary:hover {
            background: #004080;
            transform: translateY(-2px);
        }
        
        .btn-outline-primary {
            border-color: var(--jspl-blue);
            color: var(--jspl-blue);
        }
        
        .btn-outline-primary:hover {
            background: var(--jspl-blue);
            color: white;
        }
        
        .status-indicator {
            display: inline-block;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: var(--success);
            margin-right: 5px;
            box-shadow: 0 0 8px rgba(40, 167, 69, 0.5);
            animation: pulse 1.5s infinite;
        }
        
        .mobile-toggle {
            display: none;
            background: transparent;
            border: none;
            color: white;
            font-size: 1.5rem;
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 25px;
            border-radius: 8px;
            color: white;
            font-weight: 500;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.15);
            z-index: 1000;
            transform: translateX(200%);
            transition: transform 0.3s ease-in-out;
        }
        
        .notification.show {
            transform: translateX(0);
        }
        
        .notification.success {
            background: var(--success);
        }
        
        .notification.error {
            background: var(--danger);
        }
        
        .form-control, .form-select {
            border-radius: 8px;
            padding: 10px 15px;
            border: 1px solid #ddd;
        }
        
        .employee-table {
            width: 100%;
            border-collapse: collapse;
        }
        
        .employee-table th {
            background: var(--jspl-blue);
            color: white;
            padding: 12px 15px;
            text-align: left;
        }
        
        .employee-table td {
            padding: 12px 15px;
            border-bottom: 1px solid #eee;
        }
        
        .employee-table tr:hover {
            background-color: #f9f9f9;
        }
        
        .employee-table .action-btn {
            padding: 5px 10px;
            margin-right: 5px;
        }
        
        .photo-upload {
            border: 2px dashed #ddd;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            background: #f9f9f9;
        }
        
        .photo-upload:hover {
            border-color: var(--jspl-blue);
            background: #f0f8ff;
        }
        
        .photo-preview {
            width: 150px;
            height: 180px;
            object-fit: cover;
            border: 1px solid #ddd;
            border-radius: 5px;
            display: block;
            margin: 0 auto 15px;
        }
        
        .photo-placeholder {
            width: 150px;
            height: 180px;
            background: #f5f5f5;
            border: 1px dashed #ccc;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 15px;
            color: #777;
            font-size: 14px;
        }
        
        .qr-code-container {
            width: 120px;
            height: 120px;
            margin: 10px auto;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid #eee;
            padding: 5px;
        }
        
        @media (max-width: 992px) {
            .sidebar {
                transform: translateX(-100%);
            }
            
            .sidebar.active {
                transform: translateX(0);
            }
            
            .mobile-toggle {
                display: block;
            }
            
            .main-content {
                margin-left: 0;
            }
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes pulse {
            0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(40, 167, 69, 0.7); }
            70% { transform: scale(1); box-shadow: 0 0 0 10px rgba(40, 167, 69, 0); }
            100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(40, 167, 69, 0); }
        }
        
        .data-storage-info {
            background: #e8f4ff;
            border-radius: 8px;
            padding: 15px;
            margin-top: 20px;
            border-left: 4px solid var(--jspl-blue);
        }
        
        .storage-status {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .storage-bar {
            height: 8px;
            background: #e0e0e0;
            border-radius: 4px;
            overflow: hidden;
            margin-top: 5px;
        }
        
        .storage-fill {
            height: 100%;
            background: var(--jspl-blue);
            border-radius: 4px;
            width: 45%;
        }
        
        .storage-count {
            font-weight: 600;
            color: var(--jspl-blue);
            font-size: 1.2rem;
        }
        
        .jspl-badge {
            background: var(--jspl-red);
            color: white;
            padding: 3px 8px;
            border-radius: 4px;
            font-size: 0.8rem;
            font-weight: 600;
            margin-left: 5px;
        }
        
        /* ID Card Styles */
        .id-card {
            max-width: 600px;
            margin: 20px auto;
            border: 1px solid #ddd;
            border-radius: 10px;
            overflow: hidden;
            background: white;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
        }
        
        .id-header {
            background: var(--jspl-blue);
            color: white;
            padding: 15px;
            text-align: center;
            position: relative;
        }
        
        .id-header h2 {
            margin: 0;
            font-size: 1.6rem;
            font-weight: 700;
        }
        
        .id-header h3 {
            margin: 5px 0 0;
            font-size: 1.1rem;
            font-weight: 400;
        }
        
        .id-body {
            padding: 20px;
        }
        
        .employee-photo {
            width: 150px;
            height: 180px;
            background: #f5f5f5;
            border: 1px solid #ddd;
            margin: 0 auto 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            color: #777;
        }
        
        .employee-info {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        
        .info-item {
            margin-bottom: 12px;
        }
        
        .info-label {
            font-weight: 600;
            color: #444;
            display: block;
            margin-bottom: 3px;
            font-size: 0.9rem;
        }
        
        .info-value {
            font-size: 1.05rem;
            color: #333;
            padding: 5px 10px;
            background: #f9f9f9;
            border-radius: 5px;
            border: 1px solid #eee;
        }
        
        .id-footer {
            padding: 15px;
            background: #f5f5f5;
            border-top: 1px solid #ddd;
            display: flex;
            justify-content: space-between;
        }
        
        .signature-area {
            text-align: center;
            width: 45%;
        }
        
        .signature-line {
            border-top: 1px solid #333;
            width: 80%;
            margin: 0 auto 5px;
            padding-top: 20px;
        }
        
        .qr-code {
            width: 100px;
            height: 100px;
            background: #f9f9f9;
            border: 1px solid #ddd;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto;
        }
        
        .pdf-view {
            background: white;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            margin-top: 20px;
            height: 600px;
            overflow-y: auto;
        }
        
        .employee-card {
            background: white;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
        }
        
        .employee-card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid var(--jspl-blue);
            padding-bottom: 10px;
            margin-bottom: 15px;
        }
        
        .employee-id {
            background: var(--jspl-blue);
            color: white;
            padding: 3px 10px;
            border-radius: 4px;
            font-weight: 600;
        }
        
        .employee-name {
            font-size: 1.4rem;
            font-weight: 600;
            color: #333;
        }
        
        .employee-position {
            font-size: 1.1rem;
            color: var(--jspl-red);
        }
        
        .search-container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            margin-bottom: 20px;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
    </style>
</head>
<body>
    <!-- Login Page -->
    <div id="loginPage" class="login-container">
        <div class="login-card">
            <div class="login-header">
                <div class="jspl-logo">
                    <div class="jspl-logo-inner">
                        JSPL
                    </div>
                </div>
                <h2 class="mb-1">Contractual Workers Information System</h2>
                <h5 class="mb-0">Jindal Steel & Power (JSPL)</h5>
            </div>
            <div class="login-body">
                <form id="loginForm">
                    <div class="mb-3">
                        <label class="form-label">Area Name</label>
                        <select class="form-select">
                            <option selected disabled>Choose Area Name</option>
                            <option>Angul</option>
                            <option>Barbil</option>
                            <option>Raigarh</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Mine Name</label>
                        <select class="form-select">
                            <option selected disabled>Choose Mine Name</option>
                            <option>Utkal C Coal Mine</option>
                            <option>Utkal B1 Mine</option>
                            <option>Utkal B2 Mine</option>
                            <option>Tensa Mine</option>
                            <option>Kesia Mine</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Username</label>
                        <input type="text" class="form-control" value="admin" id="username">
                    </div>
                    <div class="mb-4">
                        <label class="form-label">Password</label>
                        <input type="password" class="form-control" placeholder="●●●●●●●●" value="admin123" id="password">
                    </div>
                    <div class="mb-3 form-check">
                        <input type="checkbox" class="form-check-input" id="rememberMe">
                        <label class="form-check-label" for="rememberMe">Remember Me</label>
                    </div>
                    <div class="d-grid mb-3">
                        <button type="button" id="loginBtn" class="btn btn-login btn-lg">Login</button>
                    </div>
                    <div class="d-flex justify-content-between">
                        <a href="#" class="text-decoration-none">Forget Password?</a>
                        <a href="#" class="text-decoration-none">Admin Login</a>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Dashboard (Initially Hidden) -->
    <div id="dashboardPage" class="d-none">
        <div class="dashboard-container">
            <div class="sidebar">
                <div class="sidebar-header">
                    <button class="mobile-toggle">
                        <i class="fas fa-bars"></i>
                    </button>
                    <div class="sidebar-logo">
                        <div class="sidebar-logo-inner">
                            JSPL
                        </div>
                    </div>
                    <div class="ms-2">
                        <h5 class="mb-0">Jindal Steel & Power</h5>
                        <small class="opacity-75">Contractual Workers System</small>
                    </div>
                </div>
                <div class="nav flex-column">
                    <a class="nav-link active" data-section="dashboard">
                        <i class="fas fa-tachometer-alt"></i> Dashboard
                    </a>
                    <a class="nav-link" data-section="manageEmployee">
                        <i class="fas fa-users"></i> Manage Employee
                    </a>
                    <a class="nav-link" data-section="addEmployee">
                        <i class="fas fa-user-plus"></i> Add Employee Details
                    </a>
                    <a class="nav-link" data-section="viewEmployee">
                        <i class="fas fa-list"></i> View all Employee
                    </a>
                    <a class="nav-link" data-section="uploadBulk">
                        <i class="fas fa-file-upload"></i> Upload Bulk Data
                    </a>
                    <a class="nav-link" data-section="deepEstablish">
                        <i class="fas fa-id-card"></i> Deep And Establish ID
                    </a>
                    <a class="nav-link" data-section="manageDoc">
                        <i class="fas fa-file"></i> Manage Document
                    </a>
                    <a class="nav-link" data-section="manageGallery">
                        <i class="fas fa-images"></i> Manage Gallery
                    </a>
                    <a class="nav-link" data-section="manageExam">
                        <i class="fas fa-book"></i> Manage Exam
                    </a>
                    <a class="nav-link" data-section="manageReport">
                        <i class="fas fa-chart-bar"></i> Manage Report
                    </a>
                </div>
            </div>
            
            <div class="main-content">
                <div class="topbar">
                    <div>
                        <nav aria-label="breadcrumb">
                            <ol class="breadcrumb" id="breadcrumb">
                                <li class="breadcrumb-item"><a href="#" data-section="dashboard">Mine Dashboard</a></li>
                                <li class="breadcrumb-item active">Dashboard</li>
                            </ol>
                        </nav>
                    </div>
                    <div class="user-info">
                        <div>
                            <span class="status-indicator"></span>
                            <span>Online</span>
                        </div>
                        <div class="user-avatar">JS</div>
                    </div>
                </div>
                
                <div class="content-area">
                    <!-- Dashboard Section -->
                    <div id="dashboardSection">
                        <h3 class="section-title">Mine Dashboard <span class="jspl-badge">JSPL</span></h3>
                        
                        <div class="row">
                            <div class="col-md-3 mb-4">
                                <div class="card text-center">
                                    <div class="card-body">
                                        <h5 class="card-title">Total Employees</h5>
                                        <h2 class="card-text text-primary">247</h2>
                                        <p class="text-muted">Active: 235</p>
                                    </div>
                                </div>
                            </div>
                            <div class="col-md-3 mb-4">
                                <div class="card text-center">
                                    <div class="card-body">
                                        <h5 class="card-title">New This Month</h5>
                                        <h2 class="card-text text-success">18</h2>
                                        <p class="text-muted">Contract Workers</p>
                                    </div>
                                </div>
                            </div>
                            <div class="col-md-3 mb-4">
                                <div class="card text-center">
                                    <div class="card-body">
                                        <h5 class="card-title">Pending Documents</h5>
                                        <h2 class="card-text text-danger">32</h2>
                                        <p class="text-muted">Require Attention</p>
                                    </div>
                                </div>
                            </div>
                            <div class="col-md-3 mb-4">
                                <div class="card text-center">
                                    <div class="card-body">
                                        <h5 class="card-title">Safety Compliance</h5>
                                        <h2 class="card-text text-warning">92%</h2>
                                        <p class="text-muted">Above Target</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="card">
                            <div class="card-header">
                                <i class="fas fa-chart-line"></i> Employee Statistics
                            </div>
                            <div class="card-body">
                                <div class="row">
                                    <div class="col-md-8">
                                        <canvas id="employeeChart" height="250"></canvas>
                                    </div>
                                    <div class="col-md-4">
                                        <canvas id="departmentChart" height="250"></canvas>
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="card">
                            <div class="card-header">
                                <i class="fas fa-list"></i> Recent Employees
                            </div>
                            <div class="card-body">
                                <div class="employee-card">
                                    <div class="employee-card-header">
                                        <div>
                                            <span class="employee-id">EMP-2023-056</span>
                                            <h4 class="employee-name">Suraj Pandey</h4>
                                        </div>
                                        <span class="employee-position">Dumper Operator</span>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-8">
                                            <div class="info-item">
                                                <span class="info-label">Employee ID:</span>
                                                <span class="info-value">EMP-2023-056</span>
                                            </div>
                                            <div class="info-item">
                                                <span class="info-label">A Form:</span>
                                                <span class="info-value">ALPL131</span>
                                            </div>
                                            <div class="info-item">
                                                <span class="info-label">Mobile:</span>
                                                <span class="info-value">8932856726</span>
                                            </div>
                                            <div class="info-item">
                                                <span class="info-label">Mine:</span>
                                                <span class="info-value">Utkal C Coal Mine</span>
                                            </div>
                                        </div>
                                        <div class="col-md-4 text-center">
                                            <div class="qr-code-container" id="qrPreview1"></div>
                                            <button class="btn btn-sm btn-primary mt-2">Generate ID Card</button>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="employee-card">
                                    <div class="employee-card-header">
                                        <div>
                                            <span class="employee-id">EMP-2023-042</span>
                                            <h4 class="employee-name">Rajesh Kumar</h4>
                                        </div>
                                        <span class="employee-position">Safety Officer</span>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-8">
                                            <div class="info-item">
                                                <span class="info-label">Employee ID:</span>
                                                <span class="info-value">EMP-2023-042</span>
                                            </div>
                                            <div class="info-item">
                                                <span class="info-label">A Form:</span>
                                                <span class="info-value">ALPL129</span>
                                            </div>
                                            <div class="info-item">
                                                <span class="info-label">Mobile:</span>
                                                <span class="info-value">7890123456</span>
                                            </div>
                                            <div class="info-item">
                                                <span class="info-label">Mine:</span>
                                                <span class="info-value">Utkal B1 Mine</span>
                                            </div>
                                        </div>
                                        <div class="col-md-4 text-center">
                                            <div class="qr-code-container" id="qrPreview2"></div>
                                            <button class="btn btn-sm btn-primary mt-2">Generate ID Card</button>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Add Employee Section -->
                    <div id="addEmployeeSection" class="d-none">
                        <h3 class="section-title">Add Employee Details <span class="jspl-badge">JSPL</span></h3>
                        
                        <form id="employeeForm">
                            <div class="card">
                                <div class="card-header">
                                    <i class="fas fa-user"></i> Personal Information
                                </div>
                                <div class="card-body">
                                    <div class="row">
                                        <div class="col-md-4 mb-4">
                                            <div class="photo-upload" id="photoUpload">
                                                <div class="photo-placeholder" id="photoPlaceholder">
                                                    <i class="fas fa-camera fa-3x mb-2"></i>
                                                    <div>Click to upload employee photo</div>
                                                </div>
                                                <img id="photoPreview" class="photo-preview d-none">
                                                <input type="file" id="employeePhoto" accept="image/*" class="d-none">
                                                <div class="text-muted mt-2">Max file size: 2MB</div>
                                            </div>
                                        </div>
                                        <div class="col-md-8">
                                            <div class="row">
                                                <div class="col-md-6">
                                                    <div class="mb-3">
                                                        <label class="form-label">Form A Number</label>
                                                        <input type="text" class="form-control" name="formA_number" required>
                                                    </div>
                                                    <div class="mb-3">
                                                        <label class="form-label">SL NO</label>
                                                        <input type="text" class="form-control" name="sl_no" required>
                                                    </div>
                                                    <div class="mb-3">
                                                        <label class="form-label">Gender</label>
                                                        <select class="form-select" name="gender" required>
                                                            <option selected disabled>Choose Gender</option>
                                                            <option>Male</option>
                                                            <option>Female</option>
                                                            <option>Other</option>
                                                        </select>
                                                    </div>
                                                    <div class="mb-3">
                                                        <label class="form-label">Date of Joining</label>
                                                        <input type="date" class="form-control" name="date_of_joining" required>
                                                    </div>
                                                </div>
                                                <div class="col-md-6">
                                                    <div class="mb-3">
                                                        <label class="form-label">Name of the Establishment</label>
                                                        <select class="form-select" name="establishment_name" required>
                                                            <option selected disabled>Choose Establishment</option>
                                                            <option>Utkal C Coal Mine</option>
                                                            <option>Utkal B1 Mine</option>
                                                            <option>Utkal B2 Mine</option>
                                                            <option>Tensa Mine</option>
                                                            <option>Kesia Mine</option>
                                                        </select>
                                                    </div>
                                                    <div class="mb-3">
                                                        <label class="form-label">Employee Register</label>
                                                        <input type="text" class="form-control" name="employee_register" required>
                                                    </div>
                                                    <div class="mb-3">
                                                        <label class="form-label">Father / Spouse Name</label>
                                                        <input type="text" class="form-control" name="father_spouse_name" required>
                                                    </div>
                                                    <div class="mb-3">
                                                        <label class="form-label">Education</label>
                                                        <input type="text" class="form-control" name="education" required>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-6">
                                            <div class="mb-3">
                                                <label class="form-label">Employment Type</label>
                                                <input type="text" class="form-control" name="employment_type" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">ESIC IP</label>
                                                <input type="text" class="form-control" name="esic_ip" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Bank Name</label>
                                                <input type="text" class="form-control" name="bank_name" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Permanent Address</label>
                                                <textarea class="form-control" rows="2" name="permanent_address" required></textarea>
                                            </div>
                                        </div>
                                        <div class="col-md-6">
                                            <div class="mb-3">
                                                <label class="form-label">Mobile</label>
                                                <input type="tel" class="form-control" name="mobile" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">LWF</label>
                                                <input type="text" class="form-control" name="lwf" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Bank Account No</label>
                                                <input type="text" class="form-control" name="bank_account_no" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Date of Exit</label>
                                                <input type="date" class="form-control" name="date_of_exit">
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <h3 class="section-title mt-5">Project Details <span class="jspl-badge">JSPL</span></h3>
                            
                            <div class="card">
                                <div class="card-header">
                                    <i class="fas fa-project-diagram"></i> Project Information
                                </div>
                                <div class="card-body">
                                    <div class="row">
                                        <div class="col-md-6">
                                            <div class="mb-3">
                                                <label class="form-label">First Name</label>
                                                <input type="text" class="form-control" name="first_name" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Nationality</label>
                                                <input type="text" class="form-control" name="nationality" value="Indian" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Designation</label>
                                                <select class="form-select" name="designation" required>
                                                    <option selected disabled>Choose Designation</option>
                                                    <option>Mine Supervisor</option>
                                                    <option>Heavy Equipment Operator</option>
                                                    <option>Blasting Technician</option>
                                                    <option>Safety Officer</option>
                                                    <option>Geologist</option>
                                                    <option>Maintenance Engineer</option>
                                                </select>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">UAN</label>
                                                <input type="text" class="form-control" name="uan" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Aadhar Number</label>
                                                <input type="text" class="form-control" name="aadhar_number" required>
                                            </div>
                                        </div>
                                        <div class="col-md-6">
                                            <div class="mb-3">
                                                <label class="form-label">Last Name</label>
                                                <input type="text" class="form-control" name="last_name" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Date of Birth</label>
                                                <input type="date" class="form-control" name="date_of_birth" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Category Address</label>
                                                <input type="text" class="form-control" name="category_address" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">PAN Number</label>
                                                <input type="text" class="form-control" name="pan_number" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">IFSC Code</label>
                                                <input type="text" class="form-control" name="ifsc_code" required>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-6">
                                            <div class="mb-3">
                                                <label class="form-label">Service Book</label>
                                                <input type="text" class="form-control" name="service_book" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Reason of Exit</label>
                                                <input type="text" class="form-control" name="reason_of_exit">
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">IMZ/PME DATE</label>
                                                <input type="date" class="form-control" name="imz_pme_date" required>
                                            </div>
                                        </div>
                                        <div class="col-md-6">
                                            <div class="mb-3">
                                                <label class="form-label">Present Address</label>
                                                <textarea class="form-control" rows="2" name="present_address" required></textarea>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Identification Mark</label>
                                                <input type="text" class="form-control" name="identification_mark" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Place of Employment</label>
                                                <select class="form-select" name="place_of_employment" required>
                                                    <option selected disabled>Choose Mine</option>
                                                    <option>Utkal C Coal Mine</option>
                                                    <option>Utkal B1 Mine</option>
                                                    <option>Utkal B2 Mine</option>
                                                    <option>Tensa Mine</option>
                                                    <option>Kesia Mine</option>
                                                </select>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <h3 class="section-title mt-5">Nominee Details <span class="jspl-badge">JSPL</span></h3>
                            
                            <div class="card">
                                <div class="card-header">
                                    <i class="fas fa-users"></i> Nominee Information
                                </div>
                                <div class="card-body">
                                    <div class="row">
                                        <div class="col-md-6">
                                            <div class="mb-3">
                                                <label class="form-label">Nominee Name</label>
                                                <input type="text" class="form-control" name="nominee_name" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Nominee Mobile</label>
                                                <input type="tel" class="form-control" name="nominee_mobile" required>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Relationship</label>
                                                <input type="text" class="form-control" name="relationship" required>
                                            </div>
                                        </div>
                                        <div class="col-md-6">
                                            <div class="mb-3">
                                                <label class="form-label">Nominee Address</label>
                                                <textarea class="form-control" rows="3" name="nominee_address" required></textarea>
                                            </div>
                                            <div class="mb-3">
                                                <label class="form-label">Blood Group</label>
                                                <input type="text" class="form-control" name="blood_group" required>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-6">
                                            <div class="mb-3">
                                                <label class="form-label">Date of First Appointment</label>
                                                <input type="date" class="form-control" name="date_of_first_appointment" required>
                                            </div>
                                        </div>
                                        <div class="col-md-6">
                                            <div class="mb-3">
                                                <label class="form-label">YT Certificate Date</label>
                                                <input type="date" class="form-control" name="yt_certificate_date" required>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="card">
                                <div class="card-header">
                                    <i class="fas fa-save"></i> Save Employee Details
                                </div>
                                <div class="card-body">
                                    <div class="text-center">
                                        <button type="submit" class="btn btn-primary btn-lg me-3">
                                            <i class="fas fa-save me-1"></i> Save Employee Details
                                        </button>
                                        <button type="reset" class="btn btn-outline-primary btn-lg">
                                            <i class="fas fa-times me-1"></i> Reset Form
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </form>
                    </div>
                    
                    <!-- View Employee Section -->
                    <div id="viewEmployeeSection" class="d-none">
                        <h3 class="section-title">Employee Records <span class="jspl-badge">JSPL</span></h3>
                        
                        <div class="card">
                            <div class="card-header">
                                <i class="fas fa-search"></i> Search Employees
                            </div>
                            <div class="card-body">
                                <div class="row">
                                    <div class="col-md-4 mb-3">
                                        <div class="form-group">
                                            <label class="form-label">Employee Name</label>
                                            <input type="text" class="form-control" id="searchName" placeholder="Enter employee name">
                                        </div>
                                    </div>
                                    <div class="col-md-4 mb-3">
                                        <div class="form-group">
                                            <label class="form-label">Employee ID</label>
                                            <input type="text" class="form-control" id="searchId" placeholder="Enter employee ID">
                                        </div>
                                    </div>
                                    <div class="col-md-4 mb-3">
                                        <div class="form-group">
                                            <label class="form-label">Designation</label>
                                            <select class="form-select" id="searchDesignation">
                                                <option value="">All Designations</option>
                                                <option>Mine Supervisor</option>
                                                <option>Heavy Equipment Operator</option>
                                                <option>Blasting Technician</option>
                                                <option>Safety Officer</option>
                                                <option>Geologist</option>
                                                <option>Maintenance Engineer</option>
                                            </select>
                                        </div>
                                    </div>
                                </div>
                                <div class="row">
                                    <div class="col-md-4 mb-3">
                                        <div class="form-group">
                                            <label class="form-label">Mine Location</label>
                                            <select class="form-select" id="searchMine">
                                                <option value="">All Mines</option>
                                                <option>Utkal C Coal Mine</option>
                                                <option>Utkal B1 Mine</option>
                                                <option>Utkal B2 Mine</option>
                                                <option>Tensa Mine</option>
                                                <option>Kesia Mine</option>
                                            </select>
                                        </div>
                                    </div>
                                    <div class="col-md-4 mb-3">
                                        <div class="form-group">
                                            <label class="form-label">Status</label>
                                            <select class="form-select" id="searchStatus">
                                                <option value="">All Status</option>
                                                <option>Active</option>
                                                <option>Inactive</option>
                                            </select>
                                        </div>
                                    </div>
                                    <div class="col-md-4 mb-3">
                                        <div class="form-group">
                                            <label class="form-label">&nbsp;</label>
                                            <button class="btn btn-primary w-100" id="searchBtn">
                                                <i class="fas fa-search me-1"></i> Search Employees
                                            </button>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="card">
                            <div class="card-header d-flex justify-content-between align-items-center">
                                <div>
                                    <i class="fas fa-list"></i> Employee Records
                                </div>
                                <div>
                                    <span id="resultCount">Showing 0 results</span>
                                </div>
                            </div>
                            <div class="card-body">
                                <div class="table-responsive">
                                    <table class="employee-table">
                                        <thead>
                                            <tr>
                                                <th>Employee ID</th>
                                                <th>Full Name</th>
                                                <th>Designation</th>
                                                <th>Mine Location</th>
                                                <th>Status</th>
                                                <th>Actions</th>
                                            </tr>
                                        </thead>
                                        <tbody id="employeeTableBody">
                                            <tr>
                                                <td colspan="6" class="text-center py-5">
                                                    <i class="fas fa-search fa-2x mb-3"></i>
                                                    <p>Use the search form to find employees</p>
                                                </td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Generate PDF Section -->
                    <div id="generatePdfSection" class="d-none">
                        <h3 class="section-title">Employee ID Card <span class="jspl-badge">JSPL</span></h3>
                        
                        <div class="card">
                            <div class="card-header">
                                <i class="fas fa-id-card"></i> Employee Registration Form
                            </div>
                            <div class="card-body">
                                <div class="id-card">
                                    <div class="id-header">
                                        <h2>Utkal C Coal Mine of JSPL</h2>
                                        <h3>EMPLOYEE REGISTER FORM A</h3>
                                        <h4>(See Rule 2(1) Part A and Part B)</h4>
                                    </div>
                                    <div class="id-body">
                                        <div class="row">
                                            <div class="col-md-4 text-center">
                                                <div class="photo-placeholder" id="pdfPhotoPlaceholder">
                                                    <i class="fas fa-user fa-3x"></i>
                                                </div>
                                                <div class="qr-code-container mt-3" id="pdfQrCode"></div>
                                            </div>
                                            <div class="col-md-8">
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="info-item">
                                                            <span class="info-label">Employee ID</span>
                                                            <span class="info-value" id="pdfId">-</span>
                                                        </div>
                                                        <div class="info-item">
                                                            <span class="info-label">Full Name</span>
                                                            <span class="info-value" id="pdfName">-</span>
                                                        </div>
                                                        <div class="info-item">
                                                            <span class="info-label">Designation</span>
                                                            <span class="info-value" id="pdfDesignation">-</span>
                                                        </div>
                                                        <div class="info-item">
                                                            <span class="info-label">S/W/D</span>
                                                            <span class="info-value" id="pdfFather">-</span>
                                                        </div>
                                                        <div class="info-item">
                                                            <span class="info-label">A Form</span>
                                                            <span class="info-value" id="pdfFormA">-</span>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="info-item">
                                                            <span class="info-label">Blood Group</span>
                                                            <span class="info-value" id="pdfBlood">-</span>
                                                        </div>
                                                        <div class="info-item">
                                                            <span class="info-label">Mobile</span>
                                                            <span class="info-value" id="pdfMobile">-</span>
                                                        </div>
                                                        <div class="info-item">
                                                            <span class="info-label">Date of Joining</span>
                                                            <span class="info-value" id="pdfDoj">-</span>
                                                        </div>
                                                        <div class="info-item">
                                                            <span class="info-label">Mine Location</span>
                                                            <span class="info-value" id="pdfMine">-</span>
                                                        </div>
                                                        <div class="info-item">
                                                            <span class="info-label">Status</span>
                                                            <span class="info-value" id="pdfStatus">-</span>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div class="info-item mt-3">
                                                    <span class="info-label">Address</span>
                                                    <span class="info-value" id="pdfAddress">-</span>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="id-footer">
                                        <div class="signature-area">
                                            <div>Signature of Contractor</div>
                                            <div class="signature-line"></div>
                                        </div>
                                        <div class="signature-area">
                                            <div>Signature of Employee</div>
                                            <div class="signature-line"></div>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="text-center mt-4">
                                    <button id="generatePdfBtn" class="btn btn-primary btn-lg">
                                        <i class="fas fa-file-pdf me-2"></i> Generate PDF with QR Code
                                    </button>
                                    <button id="backToSearch" class="btn btn-outline-primary btn-lg ms-3">
                                        <i class="fas fa-arrow-left me-2"></i> Back to Search
                                    </button>
                                </div>
                                
                                <div class="pdf-view mt-4">
                                    <div class="text-center">
                                        <h4>PDF Preview</h4>
                                        <p class="text-muted">Generated PDF will appear here</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Notification -->
    <div class="notification" id="notification"></div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Initialize libraries
        const { jsPDF } = window.jspdf;
        
        // Employee Data Management using localStorage
        const EMPLOYEE_STORAGE_KEY = 'jspl_employees';
        
        // Initialize sample data if empty
        function initializeEmployeeData() {
            if (!localStorage.getItem(EMPLOYEE_STORAGE_KEY)) {
                const sampleData = [
                    {
                        id: 'EMP-2023-056',
                        formA_number: 'ALPL131',
                        establishment_name: 'Utkal C Coal Mine',
                        sl_no: '001',
                        employee_register: 'EMP-001',
                        gender: 'Male',
                        father_spouse_name: 'Paramananda Pandey',
                        education: 'High School',
                        date_of_joining: '2023-01-01',
                        employment_type: 'Contractual',
                        mobile: '8932856726',
                        lwf: 'LWF-001',
                        esic_ip: 'ESIC-001',
                        bank_account_no: '123456789012',
                        bank_name: 'State Bank of India',
                        date_of_exit: '',
                        permanent_address: 'AT/PO-HALDI,BALLIA,UTTARPRADESH',
                        date_of_first_appointment: '2023-01-01',
                        token_number: 'TKN-001',
                        yt_certificate_date: '2023-01-10',
                        first_name: 'Suraj',
                        last_name: 'Pandey',
                        nationality: 'Indian',
                        date_of_birth: '1990-05-15',
                        designation: 'Dumper Operator',
                        category_address: 'Category C',
                        uan: 'UAN001',
                        pan_number: 'ABCDE1234F',
                        aadhar_number: '123412341234',
                        ifsc_code: 'SBIN0001234',
                        service_book: 'SB-001',
                        present_address: 'Central Colony, Utkal C Coal Mine',
                        reason_of_exit: '',
                        identification_mark: 'Mole on left cheek',
                        imz_pme_date: '2023-02-01',
                        place_of_employment: 'Utkal C Coal Mine',
                        nominee_name: 'Radha Devi',
                        nominee_address: 'AT/PO-HALDI,BALLIA,UTTARPRADESH',
                        blood_group: 'A+',
                        nit_number: 'NIT-001',
                        status: 'Active',
                        photo: ''
                    },
                    {
                        id: 'EMP-2023-042',
                        formA_number: 'ALPL129',
                        establishment_name: 'Utkal B1 Mine',
                        sl_no: '002',
                        employee_register: 'EMP-002',
                        gender: 'Male',
                        father_spouse_name: 'Rajesh Kumar',
                        education: 'Diploma in Mining',
                        date_of_joining: '2023-02-15',
                        employment_type: 'Contractual',
                        mobile: '7890123456',
                        lwf: 'LWF-002',
                        esic_ip: 'ESIC-002',
                        bank_account_no: '234567890123',
                        bank_name: 'Punjab National Bank',
                        date_of_exit: '',
                        permanent_address: 'AT/PO-Barbil, Odisha',
                        date_of_first_appointment: '2023-02-15',
                        token_number: 'TKN-002',
                        yt_certificate_date: '2023-02-20',
                        first_name: 'Rajesh',
                        last_name: 'Kumar',
                        nationality: 'Indian',
                        date_of_birth: '1988-11-22',
                        designation: 'Safety Officer',
                        category_address: 'Category B',
                        uan: 'UAN002',
                        pan_number: 'BCDEF2345G',
                        aadhar_number: '234523452345',
                        ifsc_code: 'PNB0001234',
                        service_book: 'SB-002',
                        present_address: 'Staff Quarters, Utkal B1 Mine',
                        reason_of_exit: '',
                        identification_mark: 'Scar on right hand',
                        imz_pme_date: '2023-03-10',
                        place_of_employment: 'Utkal B1 Mine',
                        nominee_name: 'Sunita Devi',
                        nominee_address: 'AT/PO-Barbil, Odisha',
                        blood_group: 'B+',
                        nit_number: 'NIT-002',
                        status: 'Active',
                        photo: ''
                    }
                ];
                localStorage.setItem(EMPLOYEE_STORAGE_KEY, JSON.stringify(sampleData));
            }
        }
        
        // Get all employees
        function getAllEmployees() {
            const employees = localStorage.getItem(EMPLOYEE_STORAGE_KEY);
            return employees ? JSON.parse(employees) : [];
        }
        
        // Search employees
        function searchEmployees(filters) {
            const employees = getAllEmployees();
            return employees.filter(emp => {
                // Check name
                if (filters.name) {
                    const fullName = `${emp.first_name} ${emp.last_name}`.toLowerCase();
                    if (!fullName.includes(filters.name.toLowerCase())) return false;
                }
                
                // Check ID
                if (filters.id && !emp.id.toLowerCase().includes(filters.id.toLowerCase())) return false;
                
                // Check designation
                if (filters.designation && emp.designation !== filters.designation) return false;
                
                // Check mine
                if (filters.mine && emp.place_of_employment !== filters.mine) return false;
                
                // Check status
                if (filters.status && emp.status !== filters.status) return false;
                
                return true;
            });
        }
        
        // Render employee table
        function renderEmployeeTable(employees) {
            const tableBody = document.getElementById('employeeTableBody');
            const resultCount = document.getElementById('resultCount');
            
            if (employees.length === 0) {
                tableBody.innerHTML = `
                    <tr>
                        <td colspan="6" class="text-center py-5">
                            <i class="fas fa-exclamation-circle fa-2x mb-3"></i>
                            <p>No employees found matching your criteria</p>
                        </td>
                    </tr>
                `;
                resultCount.textContent = 'Showing 0 results';
                return;
            }
            
            let tableHtml = '';
            employees.forEach(emp => {
                tableHtml += `
                    <tr>
                        <td>${emp.id}</td>
                        <td>${emp.first_name} ${emp.last_name}</td>
                        <td>${emp.designation}</td>
                        <td>${emp.place_of_employment}</td>
                        <td><span class="badge ${emp.status === 'Active' ? 'bg-success' : 'bg-danger'}">${emp.status}</span></td>
                        <td>
                            <button class="btn btn-sm btn-primary action-btn view-btn" data-id="${emp.id}">
                                <i class="fas fa-eye"></i>
                            </button>
                            <button class="btn btn-sm btn-success action-btn pdf-btn" data-id="${emp.id}">
                                <i class="fas fa-file-pdf"></i>
                            </button>
                        </td>
                    </tr>
                `;
            });
            
            tableBody.innerHTML = tableHtml;
            resultCount.textContent = `Showing ${employees.length} results`;
            
            // Add event listeners to buttons
            document.querySelectorAll('.view-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const id = this.dataset.id;
                    // In a real app, this would navigate to a detailed view
                    alert(`View details for employee: ${id}`);
                });
            });
            
            document.querySelectorAll('.pdf-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const id = this.dataset.id;
                    const employee = getAllEmployees().find(emp => emp.id === id);
                    if (employee) {
                        showPdfView(employee);
                    }
                });
            });
        }
        
        // Show PDF view
        function showPdfView(employee) {
            // Update the PDF view with employee data
            document.getElementById('pdfId').textContent = employee.id;
            document.getElementById('pdfName').textContent = `${employee.first_name} ${employee.last_name}`;
            document.getElementById('pdfDesignation').textContent = employee.designation;
            document.getElementById('pdfFather').textContent = employee.father_spouse_name;
            document.getElementById('pdfFormA').textContent = employee.formA_number;
            document.getElementById('pdfBlood').textContent = employee.blood_group;
            document.getElementById('pdfMobile').textContent = employee.mobile;
            document.getElementById('pdfDoj').textContent = new Date(employee.date_of_joining).toLocaleDateString();
            document.getElementById('pdfMine').textContent = employee.place_of_employment;
            document.getElementById('pdfStatus').textContent = employee.status;
            document.getElementById('pdfAddress').textContent = employee.permanent_address;
            
            // Generate QR code
            const qrContainer = document.getElementById('pdfQrCode');
            qrContainer.innerHTML = '';
            new QRCode(qrContainer, {
                text: `JSPL Employee ID: ${employee.id}\nName: ${employee.first_name} ${employee.last_name}\nMine: ${employee.place_of_employment}`,
                width: 100,
                height: 100,
                colorDark: "#000000",
                colorLight: "#ffffff",
                correctLevel: QRCode.CorrectLevel.H
            });
            
            // Show the PDF section
            showSection('generatePdfSection');
        }
        
        // Generate PDF
        function generatePDF() {
            const pdf = new jsPDF('p', 'mm', 'a4');
            
            // Add header
            pdf.setFontSize(16);
            pdf.setFont("helvetica", "bold");
            pdf.setTextColor(0, 85, 164); // JSPL Blue
            pdf.text("Utkal C Coal Mine of JSPL", 105, 20, null, null, 'center');
            pdf.setFontSize(14);
            pdf.text("EMPLOYEE REGISTER FORM A", 105, 28, null, null, 'center');
            pdf.setFontSize(12);
            pdf.setTextColor(0, 0, 0);
            pdf.text("(See Rule 2(1) Part A and Part B)", 105, 34, null, null, 'center');
            
            // Add employee details
            pdf.setFontSize(12);
            pdf.setFont("helvetica", "normal");
            
            // Draw photo placeholder
            pdf.setDrawColor(200, 200, 200);
            pdf.setFillColor(245, 245, 245);
            pdf.rect(20, 45, 40, 50, 'F');
            pdf.text("Employee Photo", 40, 75, null, null, 'center');
            
            // Employee details
            const employee = {
                id: document.getElementById('pdfId').textContent,
                name: document.getElementById('pdfName').textContent,
                designation: document.getElementById('pdfDesignation').textContent,
                father: document.getElementById('pdfFather').textContent,
                formA: document.getElementById('pdfFormA').textContent,
                blood: document.getElementById('pdfBlood').textContent,
                mobile: document.getElementById('pdfMobile').textContent,
                doj: document.getElementById('pdfDoj').textContent,
                mine: document.getElementById('pdfMine').textContent,
                status: document.getElementById('pdfStatus').textContent,
                address: document.getElementById('pdfAddress').textContent
            };
            
            pdf.text(`Employee ID: ${employee.id}`, 70, 50);
            pdf.text(`Full Name: ${employee.name}`, 70, 58);
            pdf.text(`Designation: ${employee.designation}`, 70, 66);
            pdf.text(`S/W/D: ${employee.father}`, 70, 74);
            pdf.text(`A Form: ${employee.formA}`, 70, 82);
            pdf.text(`Blood Group: ${employee.blood}`, 70, 90);
            pdf.text(`Mobile: ${employee.mobile}`, 70, 98);
            pdf.text(`Date of Joining: ${employee.doj}`, 70, 106);
            pdf.text(`Mine Location: ${employee.mine}`, 70, 114);
            pdf.text(`Status: ${employee.status}`, 70, 122);
            
            // Address
            pdf.text(`Address: ${employee.address}`, 20, 130);
            
            // Add QR code
            const qrSize = 50;
            const qrX = 160;
            const qrY = 45;
            const qrData = `JSPL Employee ID: ${employee.id}\nName: ${employee.name}\nDesignation: ${employee.designation}\nMine: ${employee.mine}`;
            
            // Draw QR code background
            pdf.setFillColor(255, 255, 255);
            pdf.rect(qrX - 5, qrY - 5, qrSize + 10, qrSize + 20, 'F');
            
            // Generate QR code
            const qrCanvas = document.createElement('canvas');
            new QRCode(qrCanvas, {
                text: qrData,
                width: qrSize,
                height: qrSize,
                colorDark: "#000000",
                colorLight: "#ffffff",
                correctLevel: QRCode.CorrectLevel.H
            });
            
            // Convert canvas to image
            const qrImage = qrCanvas.toDataURL('image/png');
            pdf.addImage(qrImage, 'PNG', qrX, qrY, qrSize, qrSize);
            
            pdf.text('Scan to verify', qrX + qrSize/2, qrY + qrSize + 10, null, null, 'center');
            
            // Add footer
            pdf.setLineWidth(0.5);
            pdf.line(30, 180, 80, 180);
            pdf.line(130, 180, 180, 180);
            pdf.text("Signature of Contractor", 55, 185, null, null, 'center');
            pdf.text("Signature of Employee", 155, 185, null, null, 'center');
            
            // Add page number
            pdf.setFontSize(10);
            pdf.text("Page 1 of 1", 105, 290, null, null, 'center');
            
            // Show in preview
            const pdfData = pdf.output('datauristring');
            document.querySelector('.pdf-view').innerHTML = `<iframe src="${pdfData}" style="width:100%; height:100%; border:none"></iframe>`;
            
            showNotification('PDF generated successfully!');
        }
        
        // Show notification
        function showNotification(message, type = 'success') {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.className = `notification ${type} show`;
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }
        
        // Navigation
        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('#dashboardSection, #addEmployeeSection, #viewEmployeeSection, #generatePdfSection').forEach(el => {
                el.classList.add('d-none');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.remove('d-none');
            
            // Update breadcrumb
            const breadcrumb = document.getElementById('breadcrumb');
            let sectionName = '';
            
            switch(sectionId) {
                case 'dashboardSection':
                    sectionName = 'Dashboard';
                    break;
                case 'addEmployeeSection':
                    sectionName = 'Add Employee Details';
                    break;
                case 'viewEmployeeSection':
                    sectionName = 'View Employees';
                    break;
                case 'generatePdfSection':
                    sectionName = 'Generate ID Card';
                    break;
            }
            
            breadcrumb.innerHTML = `
                <li class="breadcrumb-item"><a href="#" data-section="dashboard">Mine Dashboard</a></li>
                <li class="breadcrumb-item active">${sectionName}</li>
            `;
        }
        
        // Initialize
        function init() {
            // Initialize charts
            // Employee chart
            const employeeCtx = document.getElementById('employeeChart').getContext('2d');
            new Chart(employeeCtx, {
                type: 'bar',
                data: {
                    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul'],
                    datasets: [{
                        label: 'Employees Added',
                        data: [12, 19, 15, 8, 14, 18, 22],
                        backgroundColor: 'rgba(0, 85, 164, 0.7)',
                        borderColor: 'rgba(0, 85, 164, 1)',
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        title: {
                            display: true,
                            text: 'Monthly Employee Additions'
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });
            
            // Department chart
            const deptCtx = document.getElementById('departmentChart').getContext('2d');
            new Chart(deptCtx, {
                type: 'doughnut',
                data: {
                    labels: ['Operations', 'Maintenance', 'Safety', 'Administration', 'Logistics'],
                    datasets: [{
                        label: 'Employees by Department',
                        data: [85, 42, 28, 36, 56],
                        backgroundColor: [
                            'rgba(0, 85, 164, 0.7)',
                            'rgba(200, 16, 46, 0.7)',
                            'rgba(255, 199, 44, 0.7)',
                            'rgba(40, 167, 69, 0.7)',
                            'rgba(108, 117, 125, 0.7)'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'bottom'
                        },
                        title: {
                            display: true,
                            text: 'Department Distribution'
                        }
                    }
                }
            });
            
            // Generate QR codes for preview
            const qr1 = document.getElementById('qrPreview1');
            new QRCode(qr1, {
                text: 'EMP-2023-056|Suraj Pandey|Dumper Operator|Utkal C Coal Mine',
                width: 100,
                height: 100,
                colorDark: "#000000",
                colorLight: "#ffffff",
                correctLevel: QRCode.CorrectLevel.H
            });
            
            const qr2 = document.getElementById('qrPreview2');
            new QRCode(qr2, {
                text: 'EMP-2023-042|Rajesh Kumar|Safety Officer|Utkal B1 Mine',
                width: 100,
                height: 100,
                colorDark: "#000000",
                colorLight: "#ffffff",
                correctLevel: QRCode.CorrectLevel.H
            });
            
            // Navigation event listeners
            document.querySelectorAll('.nav-link').forEach(link => {
                link.addEventListener('click', function() {
                    // Remove active from all
                    document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
                    
                    // Add active to clicked
                    this.classList.add('active');
                    
                    // Show corresponding section
                    const section = this.dataset.section;
                    if (section === 'dashboard') showSection('dashboardSection');
                    if (section === 'addEmployee') showSection('addEmployeeSection');
                    if (section === 'viewEmployee') showSection('viewEmployeeSection');
                });
            });
            
            // Breadcrumb navigation
            document.getElementById('breadcrumb').addEventListener('click', function(e) {
                if (e.target.tagName === 'A') {
                    e.preventDefault();
                    showSection('dashboardSection');
                    document.querySelector('.nav-link.active').classList.remove('active');
                    document.querySelector('.nav-link[data-section="dashboard"]').classList.add('active');
                }
            });
            
            // Generate PDF button
            document.getElementById('generatePdfBtn').addEventListener('click', generatePDF);
            
            // Back to search button
            document.getElementById('backToSearch').addEventListener('click', function() {
                showSection('viewEmployeeSection');
            });
            
            // Search button
            document.getElementById('searchBtn').addEventListener('click', function() {
                const filters = {
                    name: document.getElementById('searchName').value,
                    id: document.getElementById('searchId').value,
                    designation: document.getElementById('searchDesignation').value,
                    mine: document.getElementById('searchMine').value,
                    status: document.getElementById('searchStatus').value
                };
                
                const results = searchEmployees(filters);
                renderEmployeeTable(results);
            });
            
            // Photo upload
            document.getElementById('photoUpload').addEventListener('click', function() {
                document.getElementById('employeePhoto').click();
            });
            
            document.getElementById('employeePhoto').addEventListener('change', function(e) {
                const file = e.target.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onload = function(event) {
                        const preview = document.getElementById('photoPreview');
                        const placeholder = document.getElementById('photoPlaceholder');
                        
                        placeholder.classList.add('d-none');
                        preview.src = event.target.result;
                        preview.classList.remove('d-none');
                    };
                    reader.readAsDataURL(file);
                }
            });
        }
        
        // Login functionality
        document.getElementById('loginBtn').addEventListener('click', function() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            if (username === 'admin' && password === 'admin123') {
                document.getElementById('loginPage').classList.add('d-none');
                document.getElementById('dashboardPage').classList.remove('d-none');
                initializeEmployeeData();
                init();
            } else {
                showNotification('Invalid username or password', 'error');
            }
        });
        
        // Mobile sidebar toggle
        document.querySelector('.mobile-toggle').addEventListener('click', function() {
            document.querySelector('.sidebar').classList.toggle('active');
        });
        
        // Initialize form with today's date
        window.addEventListener('DOMContentLoaded', function() {
            const today = new Date().toISOString().split('T')[0];
            document.querySelector('input[name="date_of_joining"]').value = today;
            document.querySelector('input[name="imz_pme_date"]').value = today;
            document.querySelector('input[name="yt_certificate_date"]').value = today;
            document.querySelector('input[name="date_of_first_appointment"]').value = today;
        });
    </script>
</body>
</html>
