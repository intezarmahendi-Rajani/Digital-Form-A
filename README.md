# Digital-Form-A
For Utkal C Coal Mine of Jindal Steel and Power Ltd digital Form A for Mining employees as per 12th safety conference of DGMS.
<br>
<br>
<br>
<br>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Utkal C Coal Mine - Contractual Workers Login</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background-color: #f2f2f2;
      background-image: url('background-mine.jpg'); /* Replace with actual mine image */
      background-size: cover;
      background-position: center;
    }
    .container {
      display: flex;
      height: 100vh;
      align-items: center;
      justify-content: center;
    }
    .login-box {
      background: #fff;
      border-radius: 10px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
      padding: 30px;
      width: 350px;
    }
    .login-box h1 {
      font-size: 20px;
      text-align: center;
      color: #003366;
      margin-bottom: 10px;
    }
    .form-group {
      margin-bottom: 15px;
    }
    .form-group label {
      display: block;
      margin-bottom: 5px;
      font-size: 14px;
    }
    .form-group input,
    .form-group select {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    .login-btn {
      width: 100%;
      padding: 10px;
      background-color: #0055a5;
      color: #fff;
      border: none;
      border-radius: 5px;
      font-weight: bold;
      cursor: pointer;
    }
    .login-btn:hover {
      background-color: #003d7a;
    }
    .extra-links {
      text-align: center;
      margin-top: 10px;
    }
    .extra-links a {
      color: #0055a5;
      font-size: 13px;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="login-box">
      <img src="jspl-logo.png" alt="JSPL Logo" style="width: 60px; display: block; margin: 0 auto;">
      <h1>UTKAL C COAL MINE<br>Jindal Steel and Power Ltd</h1>
      <div class="form-group">
        <label for="area">Area Name</label>
        <select id="area">
          <option>Choose Area Name</option>
          <option>Angul</option>
          <option>Tensa</option>
          <option>Kasia</option>
        </select>
      </div>
      <div class="form-group">
        <label for="mine">Mine Name</label>
        <select id="mine">
          <option>Choose Mine Name</option>
          <option>Utkal C</option>
          <option>Utkal B1</option>
          <option>Utkal B2</option>
          <option>Tensa Mine</option>
          <option>Kasia Mine</option>
        </select>
      </div>
      <div class="form-group">
        <label for="username">Username</label>
        <input type="text" id="username" placeholder="Enter username" />
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" id="password" placeholder="Enter password" />
      </div>
      <button class="login-btn">Login</button>
      <div class="extra-links">
        <a href="#">Admin Login</a> | <a href="#">Forgot Password?</a>
        <br/>
        <label><input type="checkbox" /> Remember Me</label>
      </div>
    </div>
  </div>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Contractual Workers Information System</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #0d4e96;
            --secondary: #e9ecef;
            --accent: #ff6b00;
            --dark: #343a40;
            --light: #f8f9fa;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f5f7fa;
            color: #333;
        }
        
        .login-container {
            background: linear-gradient(135deg, #0d4e96 0%, #1a6bc4 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .login-card {
            background: white;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 450px;
            overflow: hidden;
        }
        
        .login-header {
            background: var(--primary);
            color: white;
            padding: 25px 20px;
            text-align: center;
        }
        
        .login-body {
            padding: 30px;
        }
        
        .form-control:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 0.2rem rgba(13, 78, 150, 0.25);
        }
        
        .btn-login {
            background: var(--primary);
            color: white;
            font-weight: 600;
            padding: 10px;
            transition: all 0.3s;
        }
        
        .btn-login:hover {
            background: #0a3d75;
            transform: translateY(-2px);
        }
        
        /* Dashboard Styles */
        .dashboard-container {
            display: flex;
            min-height: 100vh;
        }
        
        .sidebar {
            width: 250px;
            background: var(--primary);
            color: white;
            min-height: 100vh;
            box-shadow: 3px 0 10px rgba(0, 0, 0, 0.1);
            transition: all 0.3s;
            z-index: 100;
        }
        
        .sidebar-header {
            padding: 20px 15px;
            background: rgba(0, 0, 0, 0.15);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .nav-link {
            color: rgba(255, 255, 255, 0.8);
            padding: 12px 20px;
            border-left: 3px solid transparent;
            transition: all 0.2s;
        }
        
        .nav-link:hover, .nav-link.active {
            background: rgba(255, 255, 255, 0.1);
            color: white;
            border-left: 3px solid var(--accent);
        }
        
        .nav-link i {
            margin-right: 10px;
            width: 20px;
            text-align: center;
        }
        
        .main-content {
            flex: 1;
            overflow-x: hidden;
        }
        
        .topbar {
            background: white;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
            padding: 15px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 99;
        }
        
        .breadcrumb {
            background: transparent;
            margin-bottom: 0;
            padding: 0;
            font-size: 0.9rem;
        }
        
        .breadcrumb-item a {
            color: var(--primary);
            text-decoration: none;
        }
        
        .user-info {
            display: flex;
            align-items: center;
        }
        
        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--secondary);
            display: flex;
            align-items: center;
            justify-content: center;
            margin-left: 15px;
            font-weight: bold;
            color: var(--primary);
        }
        
        .content-area {
            padding: 25px;
        }
        
        .section-title {
            color: var(--primary);
            border-bottom: 2px solid var(--primary);
            padding-bottom: 10px;
            margin-bottom: 25px;
            font-weight: 600;
        }
        
        .card {
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            border: none;
            margin-bottom: 25px;
        }
        
        .card-header {
            background: white;
            border-bottom: 1px solid #eaeaea;
            font-weight: 600;
            padding: 15px 20px;
            border-radius: 10px 10px 0 0 !important;
        }
        
        .form-section {
            margin-bottom: 30px;
        }
        
        .form-label {
            font-weight: 500;
            color: #555;
        }
        
        .btn-primary {
            background: var(--primary);
            border: none;
            padding: 8px 20px;
        }
        
        .btn-primary:hover {
            background: #0a3d75;
        }
        
        .status-indicator {
            display: inline-block;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: #28a745;
            margin-right: 5px;
        }
        
        .mobile-toggle {
            display: none;
            background: transparent;
            border: none;
            color: white;
            font-size: 1.5rem;
        }
        
        @media (max-width: 992px) {
            .sidebar {
                position: fixed;
                left: -250px;
            }
            
            .sidebar.active {
                left: 0;
            }
            
            .mobile-toggle {
                display: block;
            }
            
            .main-content {
                margin-left: 0;
            }
        }
    </style>
</head>
<body>
    <!-- Login Page -->
    <div id="loginPage" class="login-container">
        <div class="login-card">
            <div class="login-header">
                <h2 class="mb-1">Contractual Workers Information System</h2>
                <h5 class="mb-0">MAHANADI COALFIELDS LIMITED</h5>
            </div>
            <div class="login-body">
                <form id="loginForm">
                    <div class="mb-3">
                        <label class="form-label">Area Name</label>
                        <select class="form-select">
                            <option selected disabled>Choose Area Name</option>
                            <option>Area 1</option>
                            <option>Area 2</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Mine Name</label>
                        <select class="form-select">
                            <option selected disabled>Choose Mine Name</option>
                            <option>Mine 1</option>
                            <option>Mine 2</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Username</label>
                        <input type="text" class="form-control" value="jaganaah">
                    </div>
                    <div class="mb-4">
                        <label class="form-label">Password</label>
                        <input type="password" class="form-control" placeholder="●●●●●●●●">
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
                <div class="sidebar-header d-flex align-items-center">
                    <button class="mobile-toggle">
                        <i class="fas fa-bars"></i>
                    </button>
                    <div class="ms-3">
                        <h4 class="mb-0">JAGANNATH</h4>
                        <small class="opacity-75">Jagannath OCP</small>
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
                    <h3 class="section-title">Employee Details</h3>
                    
                    <div class="card">
                        <div class="card-header">
                            Personal Information
                        </div>
                        <div class="card-body">
                            <div class="row">
                                <div class="col-md-6">
                                    <div class="mb-3">
                                        <label class="form-label">Form A Number</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">SL NO</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Gender</label>
                                        <select class="form-select">
                                            <option selected disabled>Choose Gender</option>
                                            <option>Male</option>
                                            <option>Female</option>
                                            <option>Other</option>
                                        </select>
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Date of Joining</label>
                                        <input type="date" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Employment Type</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">ESIC IP</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Bank Name</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Permanent Address</label>
                                        <textarea class="form-control" rows="2"></textarea>
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Token Number</label>
                                        <input type="text" class="form-control">
                                    </div>
                                </div>
                                <div class="col-md-6">
                                    <div class="mb-3">
                                        <label class="form-label">Name of the Establishment</label>
                                        <select class="form-select">
                                            <option selected disabled>Choose Name of the Establishment</option>
                                            <option>Establishment 1</option>
                                            <option>Establishment 2</option>
                                        </select>
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Employee Register</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Father / Spouse Name</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Education</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Mobile</label>
                                        <input type="tel" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">LWF</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Bank Account No</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Date of Exit</label>
                                        <input type="date" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Date of First Appointment</label>
                                        <input type="date" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">YT Certificate Date</label>
                                        <input type="date" class="form-control">
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <h3 class="section-title mt-5">Project Name</h3>
                    
                    <div class="card">
                        <div class="card-header">
                            Project Details
                        </div>
                        <div class="card-body">
                            <div class="row">
                                <div class="col-md-6">
                                    <div class="mb-3">
                                        <label class="form-label">First Name</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Nationality</label>
                                        <input type="text" class="form-control" value="Indian">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Designation</label>
                                        <select class="form-select">
                                            <option selected disabled>Choose Designation</option>
                                            <option>Manager</option>
                                            <option>Supervisor</option>
                                            <option>Worker</option>
                                        </select>
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">UAN</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Aadhar Number</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Service Book</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Reason of Exit</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">IMZ/PME DATE</label>
                                        <input type="date" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Nominee Name</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Blood Group</label>
                                        <input type="text" class="form-control">
                                    </div>
                                </div>
                                <div class="col-md-6">
                                    <div class="mb-3">
                                        <label class="form-label">Last Name</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Date of Birth</label>
                                        <input type="date" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Category Address</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">PAN Number</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">IFSC Code</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Present Address</label>
                                        <textarea class="form-control" rows="2"></textarea>
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Identification Mark</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Place of Employment</label>
                                        <input type="text" class="form-control">
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">Nominee Address</label>
                                        <textarea class="form-control" rows="2"></textarea>
                                    </div>
                                    <div class="mb-3">
                                        <label class="form-label">NIT NUMBER</label>
                                        <input type="text" class="form-control">
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <h3 class="section-title mt-5">Department Details</h3>
                    
                    <div class="card">
                        <div class="card-header">
                            Department Information
                        </div>
                        <div class="card-body">
                            <div class="alert alert-info">
                                Department details will be automatically populated based on project assignment.
                            </div>
                            <div class="text-center">
                                <button class="btn btn-primary me-2">
                                    <i class="fas fa-save me-1"></i> Save Employee Details
                                </button>
                                <button class="btn btn-secondary">
                                    <i class="fas fa-times me-1"></i> Cancel
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Login functionality
        document.getElementById('loginBtn').addEventListener('click', function() {
            document.getElementById('loginPage').classList.add('d-none');
            document.getElementById('dashboardPage').classList.remove('d-none');
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
    </script>
</body>
</html>
