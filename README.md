# study-planner-pro-
for ssc students 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SSC CGL Study Planner Pro</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Theme-specific styles */
        .theme-default { background: #f7fafc; }
        .theme-default .app-container { background: #ffffff; }
        .theme-default .add-task-btn { background: #2563eb; }
        .theme-default .add-task-btn:hover { background: #1e40af; }
        .theme-default .download-btn { background: #059669; }
        .theme-default .download-btn:hover { background: #047857; }

        .theme-forest { background: url('https://images.unsplash.com/photo-1448375240586-882707db888b?auto=format&fit=crop&w=1920&q=80') no-repeat center center fixed; background-size: cover; }
        .theme-forest .app-container { background: rgba(255, 255, 255, 0.95); border: 2px solid #4b6a3b; }
        .theme-forest .add-task-btn { background: #4b6a3b; }
        .theme-forest .add-task-btn:hover { background: #3a522e; }
        .theme-forest .download-btn { background: #6b8e23; }
        .theme-forest .download-btn:hover { background: #5a7a1f; }

        .theme-ocean { background: url('https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=1920&q=80') no-repeat center center fixed; background-size: cover; }
        .theme-ocean .app-container { background: rgba(255, 255, 255, 0.95); border: 2px solid #2c5282; }
        .theme-ocean .add-task-btn { background: #2c5282; }
        .theme-ocean .add-task-btn:hover { background: #2b6cb0; }
        .theme-ocean .download-btn { background: #319795; }
        .theme-ocean .download-btn:hover { background: #2c7a7b; }

        .theme-library { background: url('https://images.unsplash.com/photo-1521587760476-6c12a4b040da?auto=format&fit=crop&w=1920&q=80') no-repeat center center fixed; background-size: cover; }
        .theme-library .app-container { background: rgba(245, 243, 235, 0.95); border: 2px solid #744210; }
        .theme-library .add-task-btn { background: #744210; }
        .theme-library .add-task-btn:hover { background: #5f370e; }
        .theme-library .download-btn { background: #975a16; }
        .theme-library .download-btn:hover { background: #7c4a12; }

        .theme-desk { background: url('https://images.unsplash.com/photo-1497032628192-86f99bcd76bc?auto=format&fit=crop&w=1920&q=80') no-repeat center center fixed; background-size: cover; }
        .theme-desk .app-container { background: rgba(255, 255, 255, 0.95); border: 2px solid #4a5568; }
        .theme-desk .add-task-btn { background: #4a5568; }
        .theme-desk .add-task-btn:hover { background: #2d3748; }
        .theme-desk .download-btn { background: #718096; }
        .theme-desk .download-btn:hover { background: #5a6b7c; }
    </style>
</head>
<body class="min-h-screen flex flex-col items-center p-4 font-sans theme-default">
    <div class="w-full max-w-4xl rounded-xl shadow-lg p-6 app-container">
        <div class="flex justify-between items-center mb-6">
            <h1 class="text-3xl font-bold text-center text-blue-700">SSC CGL Study Planner Pro</h1>
            <div>
                <label class="text-sm font-medium text-gray-700">Theme:</label>
                <select id="themeSelect" onchange="changeTheme()" class="ml-2 p-1 border rounded-md">
                    <option value="default">Default</option>
                    <option value="forest">Forest</option>
                    <option value="ocean">Ocean</option>
                    <option value="library">Library</option>
                    <option value="desk">Desk</option>
                </select>
            </div>
        </div>

        <!-- Task Input Form -->
        <div class="mb-6 bg-gray-100 p-4 rounded-lg">
            <h2 class="text-lg font-semibold mb-3">Add New Task</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700">Subject</label>
                    <select id="subjectInput" class="w-full p-2 border rounded-md focus:ring-2 focus:ring-blue-500" onchange="updateTopicSuggestions()">
                        <option value="Quant">Quantitative Aptitude</option>
                        <option value="English">English</option>
                        <option value="Reasoning">Reasoning</option>
                        <option value="GK">General Knowledge</option>
                    </select>
                </div>
                <div>
                    <label class="block text-sm font-medium text-gray-700">Topic</label>
                    <input id="topicInput" type="text" list="topicSuggestions" placeholder="e.g., Algebra" class="w-full p-2 border rounded-md focus:ring-2 focus:ring-blue-500">
                    <datalist id="topicSuggestions"></datalist>
                </div>
                <div>
                    <label class="block text-sm font-medium text-gray-700">Task Description</label>
                    <input id="taskInput" type="text" placeholder="e.g., Solve 50 Questions" class="w-full p-2 border rounded-md focus:ring-2 focus:ring-blue-500">
                </div>
                <div>
                    <label class="block text-sm font-medium text-gray-700">Time</label>
                    <input id="timeInput" type="time" class="w-full p-2 border rounded-md focus:ring-2 focus:ring-blue-500">
                </div>
                <div>
                    <label class="block text-sm font-medium text-gray-700">Date</label>
                    <input id="dateInput" type="date" class="w-full p-2 border rounded-md focus:ring-2 focus:ring-blue-500">
                </div>
                <div>
                    <label class="block text-sm font-medium text-gray-700">Duration (hours)</label>
                    <input id="durationInput" type="number" min="0.5" step="0.5" placeholder="e.g., 2" class="w-full p-2 border rounded-md focus:ring-2 focus:ring-blue-500">
                </div>
            </div>
            <button onclick="addTask()" class="mt-4 w-full text-white p-2 rounded-md add-task-btn hover:bg-blue-700 transition">Add Task</button>
        </div>

        <!-- Subject Tabs -->
        <div class="mb-6">
            <div class="flex space-x-2 border-b">
                <button onclick="showSubject('Quant')" class="px-4 py-2 font-semibold text-blue-600 border-b-2 border-blue-600">Quant</button>
                <button onclick="showSubject('English')" class="px-4 py-2 font-semibold text-green-600 hover:border-b-2 hover:border-green-600">English</button>
                <button onclick="showSubject('Reasoning')" class="px-4 py-2 font-semibold text-yellow-600 hover:border-b-2 hover:border-yellow-600">Reasoning</button>
                <button onclick="showSubject('GK')" class="px-4 py-2 font-semibold text-red-600 hover:border-b-2 hover:border-red-600">GK</button>
            </div>
        </div>

        <!-- Date Filter -->
        <div class="mb-4">
            <label class="block text-sm font-medium text-gray-700">View Tasks for:</label>
            <input id="filterDate" type="date" class="w-full md:w-1/3 p-2 border rounded-md focus:ring-2 focus:ring-blue-500" onchange="renderTimetable()">
        </div>

        <!-- Timetable Display -->
        <h2 class="text-lg font-semibold mb-2">Daily Timetable</h2>
        <div id="timetable" class="space-y-2 mb-6"></div>

        <!-- Study Records -->
        <h2 class="text-lg font-semibold mb-2">Study Records</h2>
        <div class="flex space-x-2 mb-4">
            <button onclick="showDailyRecords()" class="bg-gray-200 p-2 rounded-md hover:bg-gray-300">Daily</button>
            <button onclick="showWeeklyRecords()" class="bg-gray-200 p-2 rounded-md hover:bg-gray-300">Weekly</button>
            <button onclick="showMonthlyRecords()" class="bg-gray-200 p-2 rounded-md hover:bg-gray-300">Monthly</button>
            <button onclick="downloadRecords()" class="text-white p-2 rounded-md download-btn">Download Records</button>
        </div>
        <div id="records" class="space-y-2"></div>

        <!-- Revision Planner -->
        <h2 class="text-lg font-semibold mb-2 mt-6">Revision Suggestions</h2>
        <div id="revisionPlanner" class="space-y-2"></div>
    </div>

    <!-- Audio for Alarm -->
    <audio id="alarmSound" src="https://www.soundjay.com/buttons/beep-01a.mp3" loop></audio>

    <script>
        // Request notification permission
        if (Notification.permission !== "granted") {
            Notification.requestPermission();
        }

        // Load data from localStorage
        let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
        let studyRecords = JSON.parse(localStorage.getItem("studyRecords")) || {
            Quant: [], English: [], Reasoning: [], GK: []
        };
        let currentSubject = "Quant";
        let currentTheme = localStorage.getItem("theme") || "default";
        document.body.className = `min-h-screen flex flex-col items-center p-4 font-sans theme-${currentTheme}`;
        document.getElementById("themeSelect").value = currentTheme;

        // Topic suggestions
        const topicSuggestions = {
            Quant: ["Algebra", "Geometry", "Trigonometry", "Number System", "Data Interpretation"],
            English: ["Vocabulary", "Grammar", "Reading Comprehension", "Sentence Correction"],
            Reasoning: ["Coding-Decoding", "Analogies", "Series", "Puzzles"],
            GK: ["Current Affairs", "History", "Geography", "Polity", "Science"]
        };

        // Change theme
        function changeTheme() {
            const theme = document.getElementById("themeSelect").value;
            document.body.className = `min-h-screen flex flex-col items-center p-4 font-sans theme-${theme}`;
            localStorage.setItem("theme", theme);
        }

        // Update topic suggestions
        function updateTopicSuggestions() {
            const subject = document.getElementById("subjectInput").value;
            const datalist = document.getElementById("topicSuggestions");
            datalist.innerHTML = topicSuggestions[subject].map(t => `<option value="${t}">`).join("");
        }

        // Render timetable
        function renderTimetable() {
            const timetable = document.getElementById("timetable");
            const filterDate = document.getElementById("filterDate").value || new Date().toISOString().slice(0, 10);
            timetable.innerHTML = "";
            const filteredTasks = tasks.filter(task => task.date === filterDate && task.subject === currentSubject);
            filteredTasks.sort((a, b) => a.time.localeCompare(b.time));
            if (filteredTasks.length === 0) {
                timetable.innerHTML = `<p class="text-gray-500">No tasks for ${currentSubject} on this date.</p>`;
            }
            filteredTasks.forEach(task => {
                const taskDiv = document.createElement("div");
                taskDiv.className = `p-3 border rounded-lg flex justify-between items-center ${task.completed ? "bg-green-100" : "bg-white"} ${currentSubject === "Quant" ? "border-blue-300" : currentSubject === "English" ? "border-green-300" : currentSubject === "Reasoning" ? "border-yellow-300" : "border-red-300"} hover:shadow-md transition`;
                taskDiv.innerHTML = `
                    <div>
                        <p class="font-medium">${task.description}</p>
                        <p class="text-sm text-gray-600">${task.topic} | ${task.time} | ${task.duration} hrs</p>
                    </div>
                    <div class="flex space-x-2">
                        <input type="checkbox" ${task.completed ? "checked" : ""} onchange="toggleTask('${task.id}')">
                        <button onclick="deleteTask('${task.id}')" class="text-red-500 hover:text-red-700">Delete</button>
                    </div>
                `;
                timetable.appendChild(taskDiv);
            });
            updateRevisionPlanner();
        }

        // Generate unique ID
        function generateId() {
            return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, c => {
                const r = Math.random() * 16 | 0, v = c === 'x' ? r : (r & 0x3 | 0x8);
                return v.toString(16);
            });
        }

        // Add new task
        function addTask() {
            const taskInput = document.getElementById("taskInput");
            const subjectInput = document.getElementById("subjectInput");
            const topicInput = document.getElementById("topicInput");
            const timeInput = document.getElementById("timeInput");
            const dateInput = document.getElementById("dateInput");
            const durationInput = document.getElementById("durationInput");
            const today = new Date().toISOString().slice(0, 10);
            if (taskInput.value && subjectInput.value && topicInput.value && timeInput.value && dateInput.value && durationInput.value) {
                if (dateInput.value < today) {
                    alert("Cannot add tasks for past dates!");
                    return;
                }
                tasks.push({
                    id: generateId(),
                    description: taskInput.value,
                    subject: subjectInput.value,
                    topic: topicInput.value,
                    time: timeInput.value,
                    date: dateInput.value,
                    duration: parseFloat(durationInput.value),
                    completed: false
                });
                localStorage.setItem("tasks", JSON.stringify(tasks));
                taskInput.value = topicInput.value = timeInput.value = durationInput.value = "";
                renderTimetable();
            } else {
                alert("Please fill all fields!");
            }
        }

        // Toggle task completion
        function toggleTask(id) {
            const task = tasks.find(t => t.id === id);
            task.completed = !task.completed;
            if (task.completed) {
                studyRecords[task.subject].push({
                    date: task.date,
                    topic: task.topic,
                    duration: task.duration
                });
                localStorage.setItem("studyRecords", JSON.stringify(studyRecords));
                stopAlarm();
            }
            localStorage.setItem("tasks", JSON.stringify(tasks));
            renderTimetable();
        }

        // Delete task
        function deleteTask(id) {
            tasks = tasks.filter(t => t.id !== id);
            localStorage.setItem("tasks", JSON.stringify(tasks));
            renderTimetable();
        }

        // Play alarm
        function playAlarm() {
            const alarm = document.getElementById("alarmSound");
            alarm.play().catch(err => console.log("Audio play failed:", err));
        }

        // Stop alarm
        function stopAlarm() {
            const alarm = document.getElementById("alarmSound");
            alarm.pause();
            alarm.currentTime = 0;
        }

        // Check for missed tasks
        function checkMissedTasks() {
            const now = new Date();
            const currentDate = now.toISOString().slice(0, 10);
            const currentTime = now.toTimeString().slice(0, 5);
            tasks.forEach(task => {
                if (!task.completed && task.date === currentDate && task.time < currentTime) {
                    if (Notification.permission === "granted") {
                        new Notification(`Missed Task: ${task.description}`, {
                            body: `Scheduled for ${task.time} (${task.subject}). Mark it as done!`,
                            icon: "https://via.placeholder.com/32"
                        });
                    }
                    playAlarm();
                }
            });
        }

        // Show subject-specific content
        function showSubject(subject) {
            currentSubject = subject;
            document.querySelectorAll(".flex.space-x-2 button").forEach(btn => {
                btn.className = `px-4 py-2 font-semibold ${btn.textContent === subject ? `border-b-2 border-${subject === "Quant" ? "blue" : subject === "English" ? "green" : subject === "Reasoning" ? "yellow" : "red"}-600 text-${subject === "Quant" ? "blue" : subject === "English" ? "green" : subject === "Reasoning" ? "yellow" : "red"}-600` : "text-gray-600 hover:border-b-2 hover:border-gray-600"}`;
            });
            document.getElementById("subjectInput").value = subject;
            updateTopicSuggestions();
            renderTimetable();
            showDailyRecords();
        }

        // Show daily records
        function showDailyRecords() {
            const recordsDiv = document.getElementById("records");
            const today = new Date().toISOString().slice(0, 10);
            const records = studyRecords[currentSubject].filter(r => r.date === today);
            recordsDiv.innerHTML = `<h3 class="font-semibold">${currentSubject} Daily Records (${today})</h3>`;
            if (records.length === 0) {
                recordsDiv.innerHTML += `<p class="text-gray-500">No ${currentSubject} records for today.</p>`;
                return;
            }
            const summary = aggregateRecords(records);
            recordsDiv.innerHTML += `
                <p><strong>Total Hours</strong>: ${summary.duration} hrs</p>
                <div class="w-full bg-gray-200 h-2 rounded-full mt-2">
                    <div class="bg-${currentSubject === "Quant" ? "blue" : currentSubject === "English" ? "green" : currentSubject === "Reasoning" ? "yellow" : "red"}-500 h-2 rounded-full" style="width: ${Math.min(summary.duration / 10 * 100, 100)}%"></div>
                </div>
                <ul class="list-disc pl-5 mt-2">
                    ${summary.topics.map(t => `<li>${t.topic} (${t.duration} hrs)</li>`).join("")}
                </ul>
            `;
        }

        // Show weekly records
        function showWeeklyRecords() {
            const recordsDiv = document.getElementById("records");
            const today = new Date();
            const weekStart = new Date(today.setDate(today.getDate() - today.getDay()));
            const weekEnd = new Date(today.setDate(today.getDate() + 6));
            const records = studyRecords[currentSubject].filter(r => {
                const recordDate = new Date(r.date);
                return recordDate >= weekStart && recordDate <= weekEnd;
            });
            recordsDiv.innerHTML = `<h3 class="font-semibold">${currentSubject} Weekly Records (${weekStart.toISOString().slice(0, 10)} to ${weekEnd.toISOString().slice(0, 10)})</h3>`;
            if (records.length === 0) {
                recordsDiv.innerHTML += `<p class="text-gray-500">No ${currentSubject} records for this week.</p>`;
                return;
            }
            const summary = aggregateRecords(records);
            recordsDiv.innerHTML += `
                <p><strong>Total Hours</strong>: ${summary.duration} hrs</p>
                <div class="w-full bg-gray-200 h-2 rounded-full mt-2">
                    <div class="bg-${currentSubject === "Quant" ? "blue" : currentSubject === "English" ? "green" : currentSubject === "Reasoning" ? "yellow" : "red"}-500 h-2 rounded-full" style="width: ${Math.min(summary.duration / 70 * 100, 100)}%"></div>
                </div>
                <ul class="list-disc pl-5 mt-2">
                    ${summary.topics.map(t => `<li>${t.topic} (${t.duration} hrs)</li>`).join("")}
                </ul>
            `;
        }

        // Show monthly records
        function showMonthlyRecords() {
            const recordsDiv = document.getElementById("records");
            const today = new Date();
            const monthStart = new Date(today.getFullYear(), today.getMonth(), 1);
            const monthEnd = new Date(today.getFullYear(), today.getMonth() + 1, 0);
            const records = studyRecords[currentSubject].filter(r => {
                const recordDate = new Date(r.date);
                return recordDate >= monthStart && recordDate <= monthEnd;
            });
            recordsDiv.innerHTML = `<h3 class="font-semibold">${currentSubject} Monthly Records (${monthStart.toISOString().slice(0, 10)} to ${monthEnd.toISOString().slice(0, 10)})</h3>`;
            if (records.length === 0) {
                recordsDiv.innerHTML += `<p class="text-gray-500">No ${currentSubject} records for this month.</p>`;
                return;
            }
            const summary = aggregateRecords(records);
            recordsDiv.innerHTML += `
                <p><strong>Total Hours</strong>: ${summary.duration} hrs</p>
                <div class="w-full bg-gray-200 h-2 rounded-full mt-2">
                    <div class="bg-${currentSubject === "Quant" ? "blue" : currentSubject === "English" ? "green" : currentSubject === "Reasoning" ? "yellow" : "red"}-500 h-2 rounded-full" style="width: ${Math.min(summary.duration / 300 * 100, 100)}%"></div>
                </div>
                <ul class="list-disc pl-5 mt-2">
                    ${summary.topics.map(t => `<li>${t.topic} (${t.duration} hrs)</li>`).join("")}
                </ul>
            `;
        }

        // Aggregate records
        function aggregateRecords(records) {
            const summary = { duration: 0, topics: [] };
            records.forEach(r => {
                const topicIndex = summary.topics.findIndex(t => t.topic === r.topic);
                if (topicIndex === -1) {
                    summary.topics.push({ topic: r.topic, duration: r.duration });
                } else {
                    summary.topics[topicIndex].duration += r.duration;
                }
                summary.duration += r.duration;
            });
            return summary;
        }

        // Update revision planner
        function updateRevisionPlanner() {
            const revisionDiv = document.getElementById("revisionPlanner");
            const today = new Date();
            const isSunday = today.getDay() === 0;
            const isFirstOfMonth = today.getDate() === 1;
            if (!isSunday && !isFirstOfMonth) {
                revisionDiv.innerHTML = `<p class="text-gray-500">Revision suggestions updated every Sunday (weekly) and 1st of month (monthly).</p>`;
                return;
            }
            const records = studyRecords[currentSubject];
            const summary = aggregateRecords(records);
            const suggestions = summary.topics.sort((a, b) => a.duration - b.duration).slice(0, 2);
            revisionDiv.innerHTML = `<h3 class="font-semibold">${currentSubject} ${isSunday ? "Weekly" : "Monthly"} Revision Suggestions</h3>`;
            if (suggestions.length === 0) {
                revisionDiv.innerHTML += `<p class="text-gray-500">No ${currentSubject} records yet. Complete tasks to get suggestions.</p>`;
                return;
            }
            suggestions.forEach(s => {
                revisionDiv.innerHTML += `<p>Revise ${s.topic} (${s.duration} hrs studied)</p>`;
            });
        }

        // Download records
        function downloadRecords() {
            const content = JSON.stringify(studyRecords[currentSubject], null, 2);
            const blob = new Blob([content], { type: "text/plain" });
            const url = URL.createObjectURL(blob);
            const a = document.createElement("a");
            a.href = url;
            a.download = `${currentSubject}_study_records.txt`;
            a.click();
            URL.revokeObjectURL(url);
        }

        // Run checks and initial setup
        setInterval(checkMissedTasks, 60000);
        document.getElementById("filterDate").value = new Date().toISOString().slice(0, 10);
        updateTopicSuggestions();
        showSubject("Quant");
    </script>
</body>
</html>
