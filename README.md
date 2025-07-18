<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JSPL Contractual Workers System</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
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
        
        .login-header::after {
            content: "";
            position: absolute;
            bottom: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 30px;
            height: 30px;
            background: var(--jspl-blue);
            transform: rotate(45deg);
            z-index: 1;
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
                    <a class="nav-link active">
                        <i class="fas fa-tachometer-alt"></i> Dashboard
                    </a>
                    <a class="nav-link">
                        <i class="fas fa-users"></i> Manage Employee
                    </a>
                    <a class="nav-link">
                        <i class="fas fa-user-plus"></i> Add Employee Details
                    </a>
                    <a class="nav-link">
                        <i class="fas fa-list"></i> View all Employee
                    </a>
                    <a class="nav-link">
                        <i class="fas fa-file-upload"></i> Upload Bulk Data
                    </a>
                    <a class="nav-link">
                        <i class="fas fa-id-card"></i> Deep And Establish ID
                    </a>
                    <a class="nav-link">
                        <i class="fas fa-file"></i> Manage Document
                    </a>
                    <a class="nav-link">
                        <i class="fas fa-images"></i> Manage Gallery
                    </a>
                    <a class="nav-link">
                        <i class="fas fa-book"></i> Manage Exam
                    </a>
                    <a class="nav-link">
                        <i class="fas fa-chart-bar"></i> Manage Report
                    </a>
                </div>
            </div>
            
            <div class="main-content">
                <div class="topbar">
                    <div>
                        <nav aria-label="breadcrumb">
                            <ol class="breadcrumb">
                                <li class="breadcrumb-item"><a href="#">Mine Dashboard</a></li>
                                <li class="breadcrumb-item active">Add Employee Details</li>
                                <li class="breadcrumb-item">/ Manage Master / Add Employee Details</li>
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
                    <h3 class="section-title">Employee Details <span class="jspl-badge">JSPL</span></h3>
                    
                    <form id="employeeForm">
                        <div class="card">
                            <div class="card-header">
                                <i class="fas fa-user"></i> Personal Information
                            </div>
                            <div class="card-body">
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
                                        <div class="mb-3">
                                            <label class="form-label">Token Number</label>
                                            <input type="text" class="form-control" name="token_number" required>
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
                                        <div class="mb-3">
                                            <label class="form-label">Date of First Appointment</label>
                                            <input type="date" class="form-control" name="date_of_first_appointment" required>
                                        </div>
                                        <div class="mb-3">
                                            <label class="form-label">YT Certificate Date</label>
                                            <input type="date" class="form-control" name="yt_certificate_date" required>
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
                                        <div class="mb-3">
                                            <label class="form-label">Nominee Name</label>
                                            <input type="text" class="form-control" name="nominee_name" required>
                                        </div>
                                        <div class="mb-3">
                                            <label class="form-label">Blood Group</label>
                                            <input type="text" class="form-control" name="blood_group" required>
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
                                        <div class="mb-3">
                                            <label class="form-label">Nominee Address</label>
                                            <textarea class="form-control" rows="2" name="nominee_address" required></textarea>
                                        </div>
                                        <div class="mb-3">
                                            <label class="form-label">NIT NUMBER</label>
                                            <input type="text" class="form-control" name="nit_number" required>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        <h3 class="section-title mt-5">Department Details <span class="jspl-badge">JSPL</span></h3>
                        
                        <div class="card">
                            <div class="card-header">
                                <i class="fas fa-building"></i> Department Information
                            </div>
                            <div class="card-body">
                                <div class="alert alert-info">
                                    <i class="fas fa-info-circle me-2"></i> Department details will be automatically populated based on project assignment.
                                </div>
                                <div class="text-center">
                                    <button type="submit" class="btn btn-primary me-2">
                                        <i class="fas fa-save me-1"></i> Save Employee Details
                                    </button>
                                    <button type="reset" class="btn btn-outline-primary">
                                        <i class="fas fa-times me-1"></i> Reset Form
                                    </button>
                                </div>
                            </div>
                        </div>
                    </form>
                    
                    <div class="data-storage-info">
                        <h5><i class="fas fa-database me-2"></i> Employee Data Storage</h5>
                        <div class="storage-status">
                            <span>Current Employees: </span>
                            <span class="storage-count ms-2" id="employeeCount">0</span>
                        </div>
                        <div>Local Storage Status:</div>
                        <div class="storage-bar">
                            <div class="storage-fill" id="storageFill"></div>
                        </div>
                        <div class="mt-2">
                            <button class="btn btn-sm btn-outline-primary me-2" id="viewEmployeesBtn">
                                <i class="fas fa-eye me-1"></i> View All Employees
                            </button>
                            <button class="btn btn-sm btn-outline-danger" id="clearStorageBtn">
                                <i class="fas fa-trash-alt me-1"></i> Clear Storage
                            </button>
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
        // Employee Data Management using localStorage
        const EMPLOYEE_STORAGE_KEY = 'jspl_employees';
        
        // Initialize sample data if empty
        function initializeEmployeeData() {
            if (!localStorage.getItem(EMPLOYEE_STORAGE_KEY)) {
                const sampleData = [
                    {
                        id: Date.now(),
                        formA_number: 'JSPL-2023-001',
                        establishment_name: 'Utkal C Coal Mine',
                        sl_no: '001',
                        employee_register: 'EMP-001',
                        gender: 'Male',
                        father_spouse_name: 'Rajesh Sharma',
                        education: 'B.Tech Mining',
                        date_of_joining: '2023-01-15',
                        employment_type: 'Permanent',
                        mobile: '9876543210',
                        lwf: 'LWF-001',
                        esic_ip: 'ESIC-001',
                        bank_account_no: '123456789012',
                        bank_name: 'State Bank of India',
                        date_of_exit: '',
                        permanent_address: '123 Main St, Barbil, Odisha',
                        date_of_first_appointment: '2023-01-15',
                        token_number: 'TKN-001',
                        yt_certificate_date: '2023-01-20',
                        first_name: 'Amit',
                        last_name: 'Sharma',
                        nationality: 'Indian',
                        date_of_birth: '1990-05-10',
                        designation: 'Mine Supervisor',
                        category_address: 'Category A',
                        uan: 'UAN001',
                        pan_number: 'ABCDE1234F',
                        aadhar_number: '123412341234',
                        ifsc_code: 'SBIN0001234',
                        service_book: 'SB-001',
                        present_address: 'Staff Quarter, Utkal C Coal Mine',
                        reason_of_exit: '',
                        identification_mark: 'Mole on left cheek',
                        imz_pme_date: '2023-02-01',
                        place_of_employment: 'Utkal C Coal Mine',
                        nominee_name: 'Rajesh Sharma',
                        nominee_address: '123 Main St, Barbil, Odisha',
                        blood_group: 'B+',
                        nit_number: 'NIT-001'
                    }
                ];
                localStorage.setItem(EMPLOYEE_STORAGE_KEY, JSON.stringify(sampleData));
            }
            updateStorageUI();
        }
        
        // Get all employees
        function getAllEmployees() {
            const employees = localStorage.getItem(EMPLOYEE_STORAGE_KEY);
            return employees ? JSON.parse(employees) : [];
        }
        
        // Save new employee
        function saveEmployee(employeeData) {
            const employees = getAllEmployees();
            employeeData.id = Date.now(); // Unique ID
            employees.push(employeeData);
            localStorage.setItem(EMPLOYEE_STORAGE_KEY, JSON.stringify(employees));
            return employeeData.id;
        }
        
        // Clear all employee data
        function clearEmployeeData() {
            localStorage.removeItem(EMPLOYEE_STORAGE_KEY);
        }
        
        // Update storage UI information
        function updateStorageUI() {
            const employees = getAllEmployees();
            document.getElementById('employeeCount').textContent = employees.length;
            
            // Calculate storage usage (for demonstration)
            const storagePercent = Math.min(45, employees.length * 5);
            document.getElementById('storageFill').style.width = `${storagePercent}%`;
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
        
        // Login functionality
        document.getElementById('loginBtn').addEventListener('click', function() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            if (username === 'admin' && password === 'admin123') {
                document.getElementById('loginPage').classList.add('d-none');
                document.getElementById('dashboardPage').classList.remove('d-none');
                initializeEmployeeData();
            } else {
                showNotification('Invalid username or password', 'error');
            }
        });
        
        // Mobile sidebar toggle
        document.querySelector('.mobile-toggle').addEventListener('click', function() {
            document.querySelector('.sidebar').classList.toggle('active');
        });
        
        // Navigation link activation
        const navLinks = document.querySelectorAll('.nav-link');
        navLinks.forEach(link => {
            link.addEventListener('click', function() {
                navLinks.forEach(l => l.classList.remove('active'));
                this.classList.add('active');
            });
        });
        
        // Handle form submission
        document.getElementById('employeeForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Collect form data
            const formData = new FormData(this);
            const employeeData = {};
            
            for (const [key, value] of formData.entries()) {
                employeeData[key] = value;
            }
            
            // Save employee
            saveEmployee(employeeData);
            showNotification('Employee details saved successfully!');
            updateStorageUI();
            
            // Reset form
            this.reset();
            
            // Set today's date for some fields
            const today = new Date().toISOString().split('T')[0];
            document.querySelector('input[name="date_of_joining"]').value = today;
            document.querySelector('input[name="imz_pme_date"]').value = today;
            document.querySelector('input[name="yt_certificate_date"]').value = today;
        });
        
        // View employees button
        document.getElementById('viewEmployeesBtn').addEventListener('click', function() {
            const employees = getAllEmployees();
            if (employees.length > 0) {
                alert(`${employees.length} employees found in storage.`);
            } else {
                alert('No employees found in storage.');
            }
        });
        
        // Clear storage button
        document.getElementById('clearStorageBtn').addEventListener('click', function() {
            if (confirm('Are you sure you want to clear all employee data?')) {
                clearEmployeeData();
                showNotification('All employee data has been cleared', 'error');
                updateStorageUI();
            }
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
