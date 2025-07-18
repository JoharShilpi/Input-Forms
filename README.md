<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>My Webpage</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #f4f4f4;
      color: #333;
    }

    nav {
      background-color: #007BFF;
      color: white;
      padding: 15px 30px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
    }

    nav .logo {
      font-size: 24px;
      font-weight: bold;
    }

    nav ul {
      display: flex;
      list-style: none;
      gap: 20px;
    }

    nav ul li {
      cursor: pointer;
    }

    .main-content {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 30px;
      padding: 30px;
    }

    .section {
      background-color: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.05);
    }

    h2 {
      margin-bottom: 15px;
    }

    .form-group {
      margin-bottom: 15px;
    }

    label {
      display: block;
      margin-bottom: 5px;
    }

    input[type="text"],
    input[type="email"] {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 6px;
    }

    input[type="submit"] {
      background-color: #007BFF;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }

    .error {
      color: red;
      font-size: 13px;
      margin-top: 5px;
    }

    #taskInput {
      width: 70%;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 6px;
    }

    #addTaskBtn {
      padding: 8px 15px;
      margin-left: 10px;
      background-color: #28a745;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }

    #taskList {
      margin-top: 20px;
      list-style: none;
      padding: 0;
    }

    #taskList li {
      background: #e9ecef;
      padding: 10px;
      margin-bottom: 10px;
      display: flex;
      justify-content: space-between;
      border-radius: 5px;
    }

    #taskList li button {
      background-color: #dc3545;
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 5px;
      cursor: pointer;
    }

    @media (max-width: 768px) {
      .main-content {
        grid-template-columns: 1fr;
      }

      nav {
        flex-direction: column;
        align-items: flex-start;
      }

      nav ul {
        flex-direction: column;
        gap: 10px;
        margin-top: 10px;
      }
    }
  </style>
</head>
<body>

  <nav>
    <div class="logo">MyWebApp</div>
    <ul>
      <li>Home</li>
      <li>Form</li>
      <li>To-Do</li>
    </ul>
  </nav>

  <div class="main-content">

    <div class="section">
      <h2>Contact Form</h2>
      <form id="contactForm" novalidate>
        <div class="form-group">
          <label for="name">Name:</label>
          <input type="text" id="name" />
          <div class="error" id="nameError"></div>
        </div>

        <div class="form-group">
          <label for="email">Email:</label>
          <input type="email" id="email" />
          <div class="error" id="emailError"></div>
        </div>

        <input type="submit" value="Submit" />
      </form>
    </div>

    <div class="section">
      <h2>To-Do List</h2>
      <input type="text" id="taskInput" placeholder="Enter task" />
      <button id="addTaskBtn">Add</button>
      <ul id="taskList"></ul>
    </div>

  </div>

  <script>
    const form = document.getElementById("contactForm");
    const nameInput = document.getElementById("name");
    const emailInput = document.getElementById("email");
    const nameError = document.getElementById("nameError");
    const emailError = document.getElementById("emailError");

    form.addEventListener("submit", function (e) {
      e.preventDefault();
      let isValid = true;
      nameError.textContent = "";
      emailError.textContent = "";

      const nameValue = nameInput.value.trim();
      const emailValue = emailInput.value.trim();
      const emailPattern = /^[^ ]+@[^ ]+\.[a-z]{2,6}$/;

      if (nameValue === "") {
        nameError.textContent = "Name is required.";
        isValid = false;
      }

      if (emailValue === "") {
        emailError.textContent = "Email is required.";
        isValid = false;
      } else if (!emailPattern.test(emailValue)) {
        emailError.textContent = "Invalid email format.";
        isValid = false;
      }

      if (isValid) {
        alert("Form submitted successfully!");
        form.reset();
      }
    });

    const taskInput = document.getElementById("taskInput");
    const addTaskBtn = document.getElementById("addTaskBtn");
    const taskList = document.getElementById("taskList");

    addTaskBtn.addEventListener("click", () => {
      const taskText = taskInput.value.trim();
      if (taskText === "") return;

      const li = document.createElement("li");
      li.innerHTML = `
        ${taskText}
        <button onclick="this.parentElement.remove()">Remove</button>
      `;
      taskList.appendChild(li);
      taskInput.value = "";
    });
  </script>

</body>
</html>


