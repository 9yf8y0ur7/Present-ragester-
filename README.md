# Present-ragester-
 Student present ragester 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Student List App with Sign Up</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: #e0f7fa;
    margin: 20px;
  }
  h2 {
    text-align: center;
  }
  #authContainer, #appContainer {
    max-width: 350px;
    margin: 0 auto;
    padding: 20px;
    background: #fff;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
  }
  input[type="text"], input[type="password"] {
    width: 100%;
    padding: 10px;
    margin-top: 8px;
    margin-bottom: 16px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  button {
    width: 100%;
    padding: 10px;
    background-color: #00796b;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  button:hover {
    background-color: #004d40;
  }
  #message {
    text-align: center;
    color: red;
    margin-top: 10px;
  }
  #toggleAuth {
    background: none;
    border: none;
    color: #00796b;
    cursor: pointer;
    text-decoration: underline;
    padding: 0;
    margin-top: 10px;
  }
</style>
</head>
<body>

<h2 id="formTitle">Sign Up</h2>

<div id="authContainer">
  <div id="signUpForm">
    <h3>Register</h3>
    <label for="newUsername">Username:</label>
    <input type="text" id="newUsername" placeholder="Create username" />
    <label for="newPassword">Password:</label>
    <input type="password" id="newPassword" placeholder="Create password" />
    <button onclick="signUp()">Sign Up</button>
    <p style="text-align:center;">Already have an account? <button id="toggleBtn" onclick="toggleAuth()">Login here</button></p>
  </div>

  <div id="loginForm" style="display:none;">
    <h3>Login</h3>
    <label for="username">Username:</label>
    <input type="text" id="username" placeholder="Enter username" />
    <label for="password">Password:</label>
    <input type="password" id="password" placeholder="Enter password" />
    <button onclick="login()">Login</button>
    <p style="text-align:center;">Don't have an account? <button id="toggleBtn" onclick="toggleAuth()">Sign Up here</button></p>
  </div>
  <div id="message"></div>
</div>

<!-- Student List App, initially hidden -->
<div id="appContainer" style="display:none;">
  <h1>Student List App</h1>
  <div style="text-align: center;">
    <button onclick="addRow()">Add New Student</button>
    <button onclick="logout()" style="margin-left:10px;">Logout</button>
  </div>

  <div id="tableContainer" style="margin-top:20px;">
    <table id="studentTable" border="1" style="width:100%; border-collapse:collapse;">
      <thead>
        <tr>
          <th>List No.</th>
          <th>Name</th>
          <th>Class</th>
          <th>Fees</th>
          <th>Registration Date</th>
          <th>Aane Ka Din</th>
          <th>Jane Ka Din</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </div>
</div>

<script>
  const messageDiv = document.getElementById('message');
  const authContainer = document.getElementById('authContainer');
  const signUpForm = document.getElementById('signUpForm');
  const loginForm = document.getElementById('loginForm');
  const formTitle = document.getElementById('formTitle');
  const toggleBtn = document.getElementById('toggleBtn');

  const appContainer = document.getElementById('appContainer');

  // Function to toggle between Sign Up and Login forms
  function toggleAuth() {
    if(signUpForm.style.display === 'none') {
      signUpForm.style.display = 'block';
      loginForm.style.display = 'none';
      formTitle.innerText = 'Sign Up';
      messageDiv.innerText = '';
    } else {
      signUpForm.style.display = 'none';
      loginForm.style.display = 'block';
      formTitle.innerText = 'Login';
      messageDiv.innerText = '';
    }
  }

  // Sign Up function
  function signUp() {
    const username = document.getElementById('newUsername').value.trim();
    const password = document.getElementById('newPassword').value.trim();

    if(!username || !password) {
      messageDiv.innerText = 'Please fill all fields!';
      return;
    }

    // Save credentials in localStorage
    localStorage.setItem('user', JSON.stringify({username, password}));
    messageDiv.innerText = 'Registration successful! Please login.';
    toggleAuth(); // switch to login form
  }

  // Login function
  function login() {
    const username = document.getElementById('username').value.trim();
    const password = document.getElementById('password').value.trim();

    const storedUser = JSON.parse(localStorage.getItem('user'));

    if(storedUser && username === storedUser.username && password === storedUser.password) {
      messageDiv.innerText = '';
      authContainer.style.display = 'none';
      showApp();
    } else {
      messageDiv.innerText = 'Invalid username or password!';
    }
  }

  function showApp() {
    document.getElementById('authContainer').style.display = 'none';
    document.getElementById('appContainer').style.display = 'block';
    initializeList();
  }

  function logout() {
    // Hide app and show auth
    document.getElementById('appContainer').style.display = 'none';
    document.getElementById('authContainer').style.display = 'block';
    // Clear login fields
    document.getElementById('username').value = '';
    document.getElementById('password').value = '';
  }

  // Student list functions
  const tbody = document.querySelector('#studentTable tbody');
  let rowCount = 0;

  function addRow() {
    rowCount++;
    const tr = document.createElement('tr');

    tr.innerHTML = `
      <td>${rowCount}</td>
      <td contenteditable="true"></td>
      <td contenteditable="true"></td>
      <td contenteditable="true"></td>
      <td contenteditable="true"></td>
      <td contenteditable="true"></td>
      <td contenteditable="true"></td>
      <td><button onclick="deleteRow(this)">Delete</button></td>
    `;
    tbody.appendChild(tr);
  }

  function deleteRow(btn) {
    const row = btn.closest('tr');
    row.remove();
    updateSerialNumbers();
  }

  function updateSerialNumbers() {
    const row
     
   
   s = tbody.querySelectorAll('tr');
    rowCount = 0;
    rows.forEach((row, index) => {
      row.querySelector('td').innerText = index + 1;
    });
  }

  // Optional: Load initial list
  function initializeList() {
    for(let i=0; i<50; i++) {
      addRow();
    }
  }

  // Initialize with Sign Up view
  toggleAuth();
</script>

</body>
</html>
