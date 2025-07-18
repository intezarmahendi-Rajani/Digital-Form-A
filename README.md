# Digital-Form-A
For Utkal C Coal Mine of Jindal Steel and Power Ltd digital Form A for Mining employees as per 12th safety conference of DGMS.
<br>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Digital Form-A Dashboard</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" />
  <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-database-compat.js"></script>
</head>
<body class="bg-gray-100 text-gray-900">
  <div class="p-6 max-w-xl mx-auto">
    <div id="login" class="block">
      <h1 class="text-xl font-bold mb-4">Login</h1>
      <label class="block mb-2">Username</label>
      <input id="username" class="border p-2 w-full mb-2" type="text" />
      <label class="block mb-2">Password</label>
      <input id="password" class="border p-2 w-full mb-4" type="password" />
      <button onclick="login()" class="bg-blue-600 text-white px-4 py-2 w-full">Login</button>
    </div>

    <div id="dashboard" class="hidden">
      <h1 class="text-2xl font-bold mb-4">Digital Form-A Dashboard</h1>
      <div class="bg-white p-4 rounded shadow-md space-y-4">
        <div>
          <label>Employee ID</label>
          <input id="employeeId" class="border p-2 w-full" type="text" />
        </div>
        <div>
          <label>Name</label>
          <input id="name" class="border p-2 w-full" type="text" />
        </div>
        <div>
          <label>Designation</label>
          <input id="designation" class="border p-2 w-full" type="text" />
        </div>
        <div>
          <label>Department</label>
          <input id="department" class="border p-2 w-full" type="text" />
        </div>
        <div>
          <label>VT/PME Date</label>
          <input id="vtDate" class="border p-2 w-full" type="date" />
        </div>
        <div>
          <label>Expiry Date</label>
          <input id="expiryDate" class="border p-2 w-full" type="date" />
        </div>
        <div>
          <label>Upload Medical/VT Report</label>
          <input id="upload" class="border p-2 w-full" type="file" />
        </div>
        <div>
          <label>Remarks</label>
          <textarea id="remarks" class="border p-2 w-full" placeholder="Add any notes or observations..."></textarea>
        </div>
        <button onclick="submitForm()" class="bg-green-600 text-white px-4 py-2 w-full">Submit</button>
      </div>
    </div>
  </div>

  <script>
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_AUTH_DOMAIN",
      databaseURL: "YOUR_DATABASE_URL",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_STORAGE_BUCKET",
      messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
      appId: "YOUR_APP_ID"
    };

    firebase.initializeApp(firebaseConfig);
    const database = firebase.database();

    function login() {
      const user = document.getElementById('username').value;
      const pass = document.getElementById('password').value;
      if (user === 'admin' && pass === 'admin') {
        document.getElementById('login').style.display = 'none';
        document.getElementById('dashboard').style.display = 'block';
      } else {
        alert('Invalid credentials');
      }
    }

    function submitForm() {
      const formData = {
        employeeId: document.getElementById('employeeId').value,
        name: document.getElementById('name').value,
        designation: document.getElementById('designation').value,
        department: document.getElementById('department').value,
        vtDate: document.getElementById('vtDate').value,
        expiryDate: document.getElementById('expiryDate').value,
        remarks: document.getElementById('remarks').value,
        uploadedFileName: document.getElementById('upload').files[0]?.name || ""
      };

      database.ref('digital-form-a-submissions').push(formData)
        .then(() => {
          alert('Form submitted successfully!');
        })
        .catch(error => {
          console.error('Error submitting form:', error);
          alert('Error submitting form.');
        });
    }
  </script>
</body>
</html>
