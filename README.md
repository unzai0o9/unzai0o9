<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DO TASK</title>
    <style>
        /* Global Reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(45deg, #ff6f61, #ffcc00); /* Bold gradient background */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            color: white;
            text-align: center;
            padding: 20px;
            font-size: 18px;
        }

        h1 {
            font-size: 3.5em;
            font-weight: 700;
            color: #fff;
            text-shadow: 4px 4px 15px rgba(0, 0, 0, 0.4);
            margin-bottom: 30px;
            letter-spacing: 5px;
            text-transform: uppercase;
            animation: pulse 1.5s ease-in-out infinite;
        }

        /* Add pulse animation to h1 */
        @keyframes pulse {
            0% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.1);
            }
            100% {
                transform: scale(1);
            }
        }

        .container {
            width: 100%;
            max-width: 600px;
            background-color: rgba(0, 0, 0, 0.7); /* Dark background for the container */
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 10px 60px rgba(0, 0, 0, 0.5);
            transition: transform 0.3s;
            animation: zoomIn 1s ease-in-out;
        }

        @keyframes zoomIn {
            0% {
                transform: scale(0);
            }
            100% {
                transform: scale(1);
            }
        }

        input[type="text"] {
            padding: 15px;
            width: 80%;
            font-size: 1.5em;
            border-radius: 25px;
            border: 2px solid #fff;
            outline: none;
            margin-bottom: 20px;
            transition: background-color 0.3s, box-shadow 0.3s;
            background-color: rgba(255, 255, 255, 0.3);
            color: white;
        }

        input[type="text"]:focus {
            background-color: #ffcc00;
            box-shadow: 0 0 15px rgba(255, 204, 0, 0.6);
        }

        button {
            padding: 20px 40px;
            background-color: #ff6f61;
            font-size: 1.5em;
            color: white;
            border-radius: 50px;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.3s;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
            margin-top: 20px;
        }

        button:hover {
            background-color: #ff4500;
            transform: scale(1.1);
        }

        .task-list {
            margin-top: 30px;
            list-style-type: none;
            padding: 0;
        }

        .task-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #2c3e50;
            margin: 10px 0;
            padding: 20px;
            border-radius: 15px;
            transition: background-color 0.3s, transform 0.3s;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }

        .task-item:hover {
            background-color: #34495e;
            transform: translateY(-5px);
        }

        .task-item span {
            font-size: 1.5em;
            color: #fff;
        }

        .task-item button {
            padding: 10px 20px;
            background-color: #27ae60;
            border-radius: 10px;
            border: none;
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .task-item button:hover {
            background-color: #2ecc71;
        }

        .delete-button {
            background-color: #e74c3c;
            padding: 10px 20px;
            font-size: 1em;
            font-weight: bold;
            color: white;
            border-radius: 10px;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .delete-button:hover {
            background-color: #c0392b;
        }

        .points {
            margin-top: 30px;
            font-size: 2em;
            font-weight: bold;
            color: #ffcc00;
            text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.5);
        }

        .reset-button {
            margin-top: 40px;
            padding: 20px 40px;
            background-color: #e74c3c;
            font-size: 1.5em;
            color: white;
            border-radius: 50px;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.3s;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }

        .reset-button:hover {
            background-color: #c0392b;
            transform: scale(1.1);
        }

        .warning-message {
            color: #ff6347;
            font-size: 1.4em;
            font-weight: bold;
            margin-top: 40px;
            text-transform: uppercase;
            letter-spacing: 3px;
        }

        /* Animation for task completion */
        .completed {
            background-color: #2ecc71 !important;
            text-decoration: line-through;
            opacity: 0.7;
        }

    </style>
</head>
<body>

    <div class="container">
        <h1>DO TASK</h1>

        <input type="text" id="taskInput" placeholder="Add a new task..." />
        <button onclick="addTask()">Add Task</button>

        <ul id="taskList" class="task-list"></ul>

        <div class="points">
            Points: <span id="score">0</span>
        </div>

        <button class="reset-button" onclick="resetPoints()">Reset Points</button>

        <div class="warning-message">
            At least you have to earn 100 points in 1 day!
        </div>
    </div>

    <script>
        let score = 0;

        // Function to add a task
        function addTask() {
            const taskInput = document.getElementById("taskInput").value;
            if (taskInput === "") {
                alert("Please enter a task!");
                return;
            }

            const taskList = document.getElementById("taskList");
            const taskItem = document.createElement("li");
            taskItem.classList.add("task-item");

            // Task content
            const taskContent = document.createElement("span");
            taskContent.innerText = taskInput;

            // Complete button
            const completeButton = document.createElement("button");
            completeButton.innerText = "Complete";
            completeButton.onclick = function() {
                completeTask(taskItem);
            };

            // Delete button
            const deleteButton = document.createElement("button");
            deleteButton.classList.add("delete-button");
            deleteButton.innerText = "Delete";
            deleteButton.onclick = function() {
                deleteTask(taskItem);
            };

            taskItem.appendChild(taskContent);
            taskItem.appendChild(completeButton);
            taskItem.appendChild(deleteButton);
            taskList.appendChild(taskItem);

            document.getElementById("taskInput").value = "";
        }

        // Function to mark a task as completed
        function completeTask(taskItem) {
            taskItem.classList.add("completed");
            score += 10; // Add points for completing a task
            document.getElementById("score").innerText = score;
        }

        // Function to delete a task
        function deleteTask(taskItem) {
            taskItem.remove();
        }

        // Function to reset points
        function resetPoints() {
            score = 0;
            document.getElementById("score").innerText = score;
        }
    </script>

</body>
</html>
``
