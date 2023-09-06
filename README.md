<!DOCTYPE html>
<html>
<head>
    <title>Task Management App</title>
    <style>
        /* Add your CSS styles for layout and cards here */
    </style>
</head>
<body>
    <div id="app">
        <h1>Task Management App</h1>
        
        <!-- Add Task Form -->
        <form id="taskForm">
            <input type="text" id="taskTitle" placeholder="Task Title" required>
            <textarea id="taskDescription" placeholder="Task Description" required></textarea>
            <button type="submit">Add Task</button>
        </form>

        <!-- Task Lists (To Do, Doing, Done) -->
        <div class="task-list" id="todo">
            <h2>To Do</h2>
        </div>
        <div class="task-list" id="doing">
            <h2>Doing</h2>
        </div>
        <div class="task-list" id="done">
            <h2>Done</h2>
        </div>
    </div>

    <!-- JavaScript for functionality -->
    <script>
        // Sample tasks data (for demonstration)
        const tasks = [
            { id: 1, title: "Task 1", description: "Description 1", status: "todo" },
            { id: 2, title: "Task 2", description: "Description 2", status: "doing" },
            { id: 3, title: "Task 3", description: "Description 3", status: "done" }
        ];

        // Function to render tasks
        function renderTasks() {
            const todoList = document.getElementById('todo');
            const doingList = document.getElementById('doing');
            const doneList = document.getElementById('done');

            todoList.innerHTML = '';
            doingList.innerHTML = '';
            doneList.innerHTML = '';

            tasks.forEach(task => {
                const taskCard = document.createElement('div');
                taskCard.className = 'task-card';
                taskCard.innerHTML = `
                    <h3>${task.title}</h3>
                    <p>${task.description}</p>
                    <button class="edit-btn">Edit</button>
                    <button class="delete-btn">Delete</button>
                `;

                // Add event listeners for edit and delete buttons
                const editButton = taskCard.querySelector('.edit-btn');
                const deleteButton = taskCard.querySelector('.delete-btn');

                editButton.addEventListener('click', () => editTask(task.id));
                deleteButton.addEventListener('click', () => deleteTask(task.id));

                if (task.status === 'todo') {
                    todoList.appendChild(taskCard);
                } else if (task.status === 'doing') {
                    doingList.appendChild(taskCard);
                } else if (task.status === 'done') {
                    doneList.appendChild(taskCard);
                }
            });
        }

        // Function to add a new task
        function addTask(title, description) {
            const newTask = {
                id: tasks.length + 1,
                title,
                description,
                status: 'todo'
            };
            tasks.push(newTask);
            renderTasks();
        }

        // Function to edit an existing task
        function editTask(id) {
            // Implement edit functionality here
            // You can create a form/modal for editing
        }

        // Function to delete a task
        function deleteTask(id) {
            const taskIndex = tasks.findIndex(task => task.id === id);
            if (taskIndex !== -1) {
                tasks.splice(taskIndex, 1);
                renderTasks();
            }
        }

        // Handle form submission
        const taskForm = document.getElementById('taskForm');
        taskForm.addEventListener('submit', function (e) {
            e.preventDefault();
            const title = document.getElementById('taskTitle').value;
            const description = document.getElementById('taskDescription').value;
            addTask(title, description);
            taskForm.reset();
        });

        // Initial rendering of tasks
        renderTasks();
    </script>
</body>
</html>
