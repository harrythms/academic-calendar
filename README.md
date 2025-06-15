<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Academic Calendar</title>
  <style>
    :root {
      --primary: #4caf50;
      --bg: #f7f9fb;
      --card: #ffffff;
      --text: #333;
      --accent: #2e3b55;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body, html {
      font-family: 'Segoe UI', sans-serif;
      height: 100%;
      background-color: var(--bg);
      color: var(--text);
    }

    /* HOME PAGE STYLING */
    #home {
      height: 100vh;
      background: linear-gradient(to bottom right, #4caf50, #81c784);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      color: white;
      text-align: center;
      padding: 2rem;
    }

    #home h1 {
      font-size: 3rem;
      margin-bottom: 1rem;
    }

    #home p {
      font-size: 1.2rem;
      margin-bottom: 2rem;
      max-width: 600px;
    }

    #home button {
      padding: 0.75rem 2rem;
      font-size: 1.1rem;
      background: white;
      color: #4caf50;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
      transition: background 0.3s ease;
    }

    #home button:hover {
      background: #e0f2f1;
    }

    /* DASHBOARD STYLING — same as before */
    #dashboard {
      display: none;
      height: 100vh;
    }

    .sidebar {
      width: 240px;
      background: var(--accent);
      color: white;
      padding: 2rem 1rem;
      display: flex;
      flex-direction: column;
    }

    .sidebar h1 {
      font-size: 1.8rem;
      text-align: center;
      margin-bottom: 2rem;
    }

    .sidebar a {
      text-decoration: none;
      color: white;
      padding: 0.75rem 1rem;
      margin: 0.4rem 0;
      border-radius: 10px;
      font-size: 1rem;
      transition: background 0.2s;
    }

    .sidebar a:hover,
    .sidebar a.active {
      background-color: var(--primary);
    }

    .main {
      flex: 1;
      padding: 2rem;
      overflow-y: auto;
    }

    .section {
      display: none;
    }

    .section.active {
      display: block;
    }

    h2 {
      font-size: 1.5rem;
      margin-bottom: 1rem;
    }

    .subject-card {
      background: var(--card);
      padding: 1rem;
      margin-bottom: 1rem;
      border-radius: 12px;
      box-shadow: 0 3px 8px rgba(0, 0, 0, 0.05);
    }

    .progress {
      background: #ddd;
      height: 12px;
      border-radius: 6px;
      overflow: hidden;
      margin-top: 5px;
    }

    .progress-bar {
      height: 12px;
      background: var(--primary);
      width: 0%;
    }

    .todo input, .todo select, .todo button {
      padding: 0.5rem;
      margin: 0.4rem 0.4rem 0.4rem 0;
      border-radius: 8px;
      border: 1px solid #ccc;
    }

    .todo button {
      background: var(--primary);
      color: white;
      border: none;
      cursor: pointer;
    }

    .todo ul {
      list-style: none;
      margin-top: 1rem;
    }

    .todo li {
      background: var(--card);
      margin-bottom: 0.5rem;
      padding: 0.6rem;
      border-radius: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .weekdays {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      text-align: center;
      font-weight: bold;
      margin-bottom: 0.5rem;
    }

    .calendar-container {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      gap: 0.5rem;
    }

    .calendar-day {
      background: var(--card);
      padding: 0.5rem;
      border-radius: 8px;
      min-height: 100px;
      cursor: pointer;
      display: flex;
      flex-direction: column;
      border: 1px solid #e0e0e0;
      transition: background 0.2s;
    }

    .calendar-day:hover {
      background: #e8f5e9;
    }

    .date {
      font-weight: bold;
      margin-bottom: 4px;
    }

    .event {
      font-size: 0.9rem;
      background: #dff0d8;
      padding: 2px 5px;
      border-radius: 4px;
      margin: 2px 0;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .event button {
      background: none;
      border: none;
      color: red;
      font-weight: bold;
      cursor: pointer;
    }

    #timer-display {
      font-size: 3rem;
      margin: 1.5rem 0;
    }

    .timer-buttons button {
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 8px;
      background: var(--primary);
      color: white;
      margin-right: 0.5rem;
      cursor: pointer;
    }

    @media (max-width: 768px) {
      .sidebar {
        flex-direction: row;
        width: 100%;
        padding: 1rem;
        overflow-x: auto;
        justify-content: space-around;
      }

      .sidebar a {
        font-size: 0.9rem;
        padding: 0.6rem;
        white-space: nowrap;
      }

      #dashboard {
        flex-direction: column;
      }
    }

    #dashboard-wrapper {
      display: flex;
      height: 100vh;
    }
  </style>
</head>
<body>

  <!-- HOME PAGE -->
  <div id="home">
    <h1>🎓 Academic Calendar</h1>
    <p>Welcome to your smart academic assistant — track subjects, stay productive, and manage your time effectively.</p>
    <button onclick="enterDashboard()">Enter Dashboard</button>
  </div>

  <!-- DASHBOARD PAGE -->
  <div id="dashboard">
    <div id="dashboard-wrapper">
      <div class="sidebar">
        <h1>📚 StudyFlow</h1>
        <a href="#" data-page="subjects" class="active">Subjects</a>
        <a href="#" data-page="todo">To-Do</a>
        <a href="#" data-page="calendar">Calendar</a>
        <a href="#" data-page="timer">Timer</a>
      </div>

      <div class="main">
       <!-- Replace your existing #subjects section with this -->
<div id="subjects" class="section active">
  <h2>Your Subjects</h2>

  <div class="subject-card" style="border-left: 6px solid #4caf50;">
    <strong>Mathematics</strong>
    <div>Marks: <span>45</span></div>
    <div class="progress"><div class="progress-bar" style="width: 90%"></div></div>
  </div>

  <div class="subject-card" style="border-left: 6px solid #4caf50;">
    <strong>C Programming</strong>
    <div>Marks: <span style="color: red; font-weight: bold;">18</span></div>
    <div class="progress"><div class="progress-bar" style="width: 36%"></div></div>
  </div>

  <div class="subject-card" style="border-left: 6px solid #4caf50;">
    <strong>Economics</strong>
    <div>Marks: <span>32</span></div>
    <div class="progress"><div class="progress-bar" style="width: 64%"></div></div>
  </div>

  <div class="subject-card" style="border-left: 6px solid #4caf50;">
    <strong>Computer Hardware</strong>
    <div>Marks: <span>25</span></div>
    <div class="progress"><div class="progress-bar" style="width: 50%"></div></div>
  </div>

  <div class="subject-card" style="border-left: 6px solid #4caf50;">
    <strong>Digital Logic</strong>
    <div>Marks: <span style="color: red; font-weight: bold;">15</span></div>
    <div class="progress"><div class="progress-bar" style="width: 30%"></div></div>
  </div>
</div>



        <div id="todo" class="section">
          <h2>To-Do List</h2>
          <div class="todo">
            <input type="text" id="taskInput" placeholder="New Task" />
            <select id="priority"><option>Normal</option><option>High</option></select>
            <button onclick="addTask()">Add</button>
            <ul id="taskList"></ul>
          </div>
        </div>

        <div id="calendar" class="section">
          <h2>Monthly Calendar</h2>
          <div class="weekdays"><div>Sun</div><div>Mon</div><div>Tue</div><div>Wed</div><div>Thu</div><div>Fri</div><div>Sat</div></div>
          <div class="calendar-container" id="calendar-grid"></div>
        </div>

        <div id="timer" class="section">
          <h2>Focus Timer</h2>
          <div id="timer-display">25:00</div>
          <div class="timer-buttons">
            <button onclick="startTimer()">Start</button>
            <button onclick="resetTimer()">Reset</button>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- JS -->
  <script>
    function enterDashboard() {
      document.getElementById("home").style.display = "none";
      document.getElementById("dashboard").style.display = "block";
    }

    // Navigation
    const links = document.querySelectorAll(".sidebar a");
    const sections = document.querySelectorAll(".section");
    links.forEach(link => {
      link.addEventListener("click", e => {
        e.preventDefault();
        const page = link.dataset.page;
        sections.forEach(sec => sec.classList.remove("active"));
        document.getElementById(page).classList.add("active");
        links.forEach(l => l.classList.remove("active"));
        link.classList.add("active");
      });
    });

    // To-Do
    function addTask() {
      const taskInput = document.getElementById("taskInput");
      const priority = document.getElementById("priority").value;
      const taskList = document.getElementById("taskList");
      const li = document.createElement("li");
      li.textContent = `${taskInput.value} (${priority})`;
      const btn = document.createElement("button");
      btn.textContent = "❌";
      btn.onclick = () => li.remove();
      li.appendChild(btn);
      taskList.appendChild(li);
      taskInput.value = "";
    }

    // Timer
    let time = 25 * 60;
    let interval;
    function startTimer() {
      if (interval) return;
      interval = setInterval(() => {
        if (time <= 0) {
          clearInterval(interval);
          interval = null;
          alert("Time's up!");
          return;
        }
        time--;
        updateTimer();
      }, 1000);
    }

    function resetTimer() {
      clearInterval(interval);
      interval = null;
      time = 25 * 60;
      updateTimer();
    }

    function updateTimer() {
      const minutes = Math.floor(time / 60);
      const seconds = time % 60;
      document.getElementById("timer-display").textContent =
        `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
    }

    updateTimer();

    // Calendar
    const calendarGrid = document.getElementById("calendar-grid");
    const events = {};

    function generateCalendar(year, month) {
      calendarGrid.innerHTML = "";
      const firstDay = new Date(year, month, 1);
      const lastDate = new Date(year, month + 1, 0).getDate();
      const startDay = firstDay.getDay();

      for (let i = 0; i < startDay; i++) {
        const empty = document.createElement("div");
        calendarGrid.appendChild(empty);
      }

      for (let date = 1; date <= lastDate; date++) {
        const fullDate = `${year}-${String(month + 1).padStart(2, '0')}-${String(date).padStart(2, '0')}`;
        const cell = document.createElement("div");
        cell.className = "calendar-day";

        const dateEl = document.createElement("div");
        dateEl.className = "date";
        dateEl.textContent = date;
        cell.appendChild(dateEl);

        if (events[fullDate]) {
          events[fullDate].forEach((event, i) => {
            const p = document.createElement("div");
            p.className = "event";
            p.innerHTML = `${event} <button onclick="deleteEvent('${fullDate}', ${i})">×</button>`;
            cell.appendChild(p);
          });
        }

        cell.addEventListener("click", e => {
          if (e.target.tagName === "BUTTON") return;
          const eventText = prompt(`Add event on ${fullDate}:`);
          if (eventText) {
            if (!events[fullDate]) events[fullDate] = [];
            events[fullDate].push(eventText);
            generateCalendar(year, month);
          }
        });

        calendarGrid.appendChild(cell);
      }
    }

    function deleteEvent(date, index) {
      events[date].splice(index, 1);
      if (events[date].length === 0) delete events[date];
      const now = new Date();
      generateCalendar(now.getFullYear(), now.getMonth());
    }

    const today = new Date();
    generateCalendar(today.getFullYear(), today.getMonth());
  </script>
</body>
</html>
