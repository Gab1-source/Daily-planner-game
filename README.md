# Daily-planner-game
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Daily Planner | Plan Your Day</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
        }

        header h1 {
            font-size: 2.5em;
            font-weight: 700;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        }

        header p {
            font-size: 1.1em;
            opacity: 0.9;
        }

        .date-display {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            color: white;
            text-align: center;
            margin-bottom: 30px;
            font-size: 1.1em;
            backdrop-filter: blur(10px);
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin-bottom: 30px;
        }

        .card {
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 50px rgba(0, 0, 0, 0.2);
        }

        .card h2 {
            color: #667eea;
            margin-bottom: 20px;
            font-size: 1.5em;
            border-bottom: 3px solid #667eea;
            padding-bottom: 10px;
        }

        .input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        input[type="text"],
        input[type="time"],
        select {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1em;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            transition: border-color 0.3s ease;
        }

        input[type="text"]:focus,
        input[type="time"]:focus,
        select:focus {
            outline: none;
            border-color: #667eea;
        }

        button {
            padding: 12px 25px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1em;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }

        button:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        button:active {
            transform: scale(0.98);
        }

        .tasks-list {
            max-height: 400px;
            overflow-y: auto;
        }

        .task-item {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-left: 4px solid #667eea;
            transition: all 0.3s ease;
        }

        .task-item:hover {
            background: #e8eaf6;
        }

        .task-item.completed {
            opacity: 0.6;
            text-decoration: line-through;
        }

        .task-content {
            flex: 1;
        }

        .task-text {
            font-weight: 600;
            margin-bottom: 5px;
            color: #333;
        }

        .task-time {
            font-size: 0.9em;
            color: #999;
        }

        .task-priority {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.85em;
            font-weight: 600;
            margin-top: 8px;
        }

        .priority-high {
            background: #ffebee;
            color: #c62828;
        }

        .priority-medium {
            background: #fff3e0;
            color: #e65100;
        }

        .priority-low {
            background: #e8f5e9;
            color: #2e7d32;
        }

        .task-actions {
            display: flex;
            gap: 8px;
        }

        .btn-small {
            padding: 8px 12px;
            font-size: 0.9em;
            border-radius: 6px;
            cursor: pointer;
            border: none;
            font-weight: 600;
            transition: all 0.2s ease;
        }

        .btn-complete {
            background: #4caf50;
            color: white;
        }

        .btn-complete:hover {
            background: #45a049;
        }

        .btn-delete {
            background: #f44336;
            color: white;
        }

        .btn-delete:hover {
            background: #da190b;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-top: 20px;
        }

        .stat-box {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-number {
            font-size: 2em;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 0.95em;
            opacity: 0.9;
        }

        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: #999;
        }

        .empty-state-icon {
            font-size: 3em;
            margin-bottom: 10px;
        }

        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }

            header h1 {
                font-size: 2em;
            }

            .stats {
                grid-template-columns: 1fr;
            }
        }

        /* Scrollbar styling */
        .tasks-list::-webkit-scrollbar {
            width: 8px;
        }

        .tasks-list::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }

        .tasks-list::-webkit-scrollbar-thumb {
            background: #667eea;
            border-radius: 10px;
        }

        .tasks-list::-webkit-scrollbar-thumb:hover {
            background: #764ba2;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>📅 Daily Planner</h1>
            <p>Organize your day and boost productivity</p>
        </header>

        <div class="date-display" id="dateDisplay"></div>

        <div class="main-content">
            <!-- Add Task Section -->
            <div class="card">
                <h2>➕ Add Task</h2>
                <div class="input-group">
                    <input type="text" id="taskInput" placeholder="What do you need to do?" maxlength="100">
                </div>
                <div class="input-group">
                    <input type="time" id="taskTime">
                </div>
                <div class="input-group">
                    <select id="priorityInput">
                        <option value="low">Low Priority</option>
                        <option value="medium" selected>Medium Priority</option>
                        <option value="high">High Priority</option>
                    </select>
                </div>
                <button onclick="addTask()">Add Task</button>

                <div class="stats" id="stats">
                    <div class="stat-box">
                        <div class="stat-number" id="totalTasks">0</div>
                        <div class="stat-label">Total Tasks</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-number" id="completedTasks">0</div>
                        <div class="stat-label">Completed</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-number" id="remainingTasks">0</div>
                        <div class="stat-label">Remaining</div>
                    </div>
                </div>
            </div>

            <!-- Tasks List Section -->
            <div class="card">
                <h2>📋 Today's Tasks</h2>
                <div class="tasks-list" id="tasksList">
                    <div class="empty-state">
                        <div class="empty-state-icon">✨</div>
                        <p>No tasks yet. Add one to get started!</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        let tasks = JSON.parse(localStorage.getItem('tasks')) || [];

        function displayDate() {
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const today = new Date().toLocaleDateString('en-US', options);
            document.getElementById('dateDisplay').textContent = today;
        }

        function addTask() {
            const taskInput = document.getElementById('taskInput');
            const taskTime = document.getElementById('taskTime');
            const priorityInput = document.getElementById('priorityInput');

            if (taskInput.value.trim() === '') {
                alert('Please enter a task!');
                return;
            }

            const task = {
                id: Date.now(),
                text: taskInput.value.trim(),
                time: taskTime.value || 'No time set',
                priority: priorityInput.value,
                completed: false
            };

            tasks.push(task);
            saveTasks();
            renderTasks();

            taskInput.value = '';
            taskTime.value = '';
            priorityInput.value = 'medium';
            taskInput.focus();
        }

        function deleteTask(id) {
            tasks = tasks.filter(task => task.id !== id);
            saveTasks();
            renderTasks();
        }

        function toggleComplete(id) {
            const task = tasks.find(t => t.id === id);
            if (task) {
                task.completed = !task.completed;
                saveTasks();
                renderTasks();
            }
        }

        function renderTasks() {
            const tasksList = document.getElementById('tasksList');

            if (tasks.length === 0) {
                tasksList.innerHTML = `
                    <div class="empty-state">
                        <div class="empty-state-icon">✨</div>
                        <p>No tasks yet. Add one to get started!</p>
                    </div>
                `;
                updateStats();
                return;
            }

            const sortedTasks = [...tasks].sort((a, b) => {
                if (a.time === 'No time set') return 1;
                if (b.time === 'No time set') return -1;
                return a.time.localeCompare(b.time);
            });

            tasksList.innerHTML = sortedTasks.map(task => `
                <div class="task-item ${task.completed ? 'completed' : ''}">
                    <div class="task-content">
                        <div class="task-text">${escapeHtml(task.text)}</div>
                        <div class="task-time">⏰ ${task.time}</div>
                        <span class="task-priority priority-${task.priority}">${task.priority.toUpperCase()}</span>
                    </div>
                    <div class="task-actions">
                        <button class="btn-small btn-complete" onclick="toggleComplete(${task.id})">
                            ${task.completed ? '↩️ Undo' : '✓ Done'}
                        </button>
                        <button class="btn-small btn-delete" onclick="deleteTask(${task.id})">Delete</button>
                    </div>
                </div>
            `).join('');

            updateStats();
        }

        function updateStats() {
            const total = tasks.length;
            const completed = tasks.filter(t => t.completed).length;
            const remaining = total - completed;

            document.getElementById('totalTasks').textContent = total;
            document.getElementById('completedTasks').textContent = completed;
            document.getElementById('remainingTasks').textContent = remaining;
        }

        function saveTasks() {
            localStorage.setItem('tasks', JSON.stringify(tasks));
        }

        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        // Allow Enter key to add task
        document.getElementById('taskInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                addTask();
            }
        });

        // Initialize
        displayDate();
        renderTasks();
    </script>
</body>
</html>
