<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>To-Do List</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #f0f8ff;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      height: 100vh;
      margin: 0;
      padding-top: 50px;
    }

    .container {
      background: #fff;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.2);
      width: 100%;
      max-width: 400px;
    }

    h1 {
      text-align: center;
      color: #333;
    }

    .input-section {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
    }

    #taskInput {
      flex: 1;
      padding: 10px;
      font-size: 16px;
    }

    button {
      padding: 10px 15px;
      background-color: #2e8b57;
      color: white;
      border: none;
      cursor: pointer;
      border-radius: 6px;
    }

    button:hover {
      background-color: #256f47;
    }

    ul {
      list-style-type: none;
      padding: 0;
    }

    li {
      background: #e0f7fa;
      padding: 10px;
      margin-bottom: 10px;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    li span {
      flex: 1;
    }

    .delete-btn {
      background-color: crimson;
      color: white;
      border: none;
      padding: 6px 10px;
      border-radius: 4px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>📝 My To-Do List</h1>
    <div class="input-section">
      <input type="text" id="taskInput" placeholder="Add a new task..." />
      <button onclick="addTask()">Add</button>
    </div>
    <ul id="taskList"></ul>
  </div>

  <script>
    // Load tasks on page load
    window.onload = function() {
      loadTasks();
    };

    function addTask() {
      const taskInput = document.getElementById("taskInput");
      const task = taskInput.value.trim();

      if (task === "") {
        alert("Please enter a task.");
        return;
      }

      let tasks = getTasks();
      tasks.push(task);
      localStorage.setItem("tasks", JSON.stringify(tasks));
      taskInput.value = "";

      loadTasks();
    }

    function deleteTask(index) {
      let tasks = getTasks();
      tasks.splice(index, 1);
      localStorage.setItem("tasks", JSON.stringify(tasks));
      loadTasks();
    }

    function loadTasks() {
      const taskList = document.getElementById("taskList");
      taskList.innerHTML = "";

      let tasks = getTasks();
      tasks.forEach((task, index) => {
        const li = document.createElement("li");
        li.innerHTML = `<span>${task}</span>
                        <button class="delete-btn" onclick="deleteTask(${index})">Delete</button>`;
        taskList.appendChild(li);
      });
    }

    function getTasks() {
      let tasks = localStorage.getItem("tasks");
      return tasks ? JSON.parse(tasks) : [];
    }
  </script>
</body>
</html>
