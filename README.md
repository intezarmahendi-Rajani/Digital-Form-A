# Digital-Form-A
For Utkal C Coal Mine of Jindal Steel and Power Ltd digital Form A for Mining employees as per 12th safety conference of DGMS.
<br>
<br>

<!DOCTYPE html>
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
          <option>Tamnar</option>
          option>Kasia</option>
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
