<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Мой распорядок</title>
  <style>
    :root {
      --bg: #f4f7fb;
      --card: rgba(255, 255, 255, 0.82);
      --card-solid: #ffffff;
      --text: #152238;
      --muted: #7b8798;
      --line: #e7edf5;
      --primary: #5b67f1;
      --primary-dark: #4652d6;
      --accent: #e8eaff;
      --success: #2bb673;
      --danger: #ef6672;
      --shadow: 0 18px 50px rgba(46, 63, 96, 0.11);
      --radius: 24px;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      color: var(--text);
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont,
        "Segoe UI", sans-serif;
      background:
        radial-gradient(circle at top left, rgba(116, 127, 255, 0.2), transparent 30%),
        radial-gradient(circle at bottom right, rgba(126, 224, 196, 0.18), transparent 28%),
        var(--bg);
    }

    button,
    input,
    textarea {
      font: inherit;
    }

    button {
      border: 0;
      cursor: pointer;
    }

    .app {
      width: min(1440px, 100%);
      margin: 0 auto;
      padding: 28px;
    }

    .topbar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 20px;
      margin-bottom: 26px;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 13px;
    }

    .brand-icon {
      display: grid;
      place-items: center;
      width: 48px;
      height: 48px;
      color: white;
      font-size: 22px;
      border-radius: 16px;
      background: linear-gradient(145deg, #707cff, #4c58dd);
      box-shadow: 0 10px 22px rgba(91, 103, 241, 0.28);
    }

    .brand h1 {
      margin: 0;
      font-size: clamp(22px, 3vw, 32px);
      letter-spacing: -0.8px;
    }

    .brand p {
      margin: 3px 0 0;
      color: var(--muted);
      font-size: 14px;
    }

    .top-actions {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .icon-button,
    .outline-button,
    .primary-button {
      min-height: 44px;
      border-radius: 14px;
      transition: 0.2s ease;
    }

    .icon-button {
      width: 44px;
      color: var(--muted);
      background: var(--card);
      border: 1px solid rgba(255, 255, 255, 0.9);
    }

    .icon-button:hover,
    .outline-button:hover {
      color: var(--primary);
      transform: translateY(-1px);
    }

    .outline-button {
      padding: 0 17px;
      color: var(--text);
      background: rgba(255, 255, 255, 0.62);
      border: 1px solid var(--line);
      font-weight: 700;
    }

    .primary-button {
      padding: 0 19px;
      color: white;
      background: linear-gradient(135deg, var(--primary), #747eff);
      box-shadow: 0 10px 24px rgba(91, 103, 241, 0.23);
      font-weight: 800;
    }

    .primary-button:hover {
      background: linear-gradient(135deg, var(--primary-dark), #6872ef);
      transform: translateY(-1px);
    }

    .dashboard {
      display: grid;
      grid-template-columns: 270px minmax(0, 1fr);
      gap: 24px;
      align-items: start;
    }

    .sidebar,
    .calendar-panel {
      background: var(--card);
      border: 1px solid rgba(255, 255, 255, 0.85);
      box-shadow: var(--shadow);
      backdrop-filter: blur(18px);
    }

    .sidebar {
      padding: 20px;
      border-radius: var(--radius);
    }

    .mini-calendar {
      padding-bottom: 21px;
      margin-bottom: 20px;
      border-bottom: 1px solid var(--line);
    }

    .mini-calendar-header,
    .calendar-heading,
    .progress-top,
    .task-form-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
    }

    .mini-calendar-header strong {
      font-size: 15px;
    }

    .mini-calendar-header button {
      width: 30px;
      height: 30px;
      color: var(--muted);
      background: transparent;
      border-radius: 9px;
    }

    .mini-calendar-header button:hover {
      color: var(--primary);
      background: var(--accent);
    }

    .weekdays,
    .mini-days {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      gap: 4px;
      margin-top: 14px;
      text-align: center;
    }

    .weekdays {
      color: var(--muted);
      font-size: 10px;
      font-weight: 800;
      text-transform: uppercase;
    }

    .mini-days button {
      position: relative;
      width: 28px;
      height: 28px;
      margin: auto;
      color: var(--text);
      background: transparent;
      border-radius: 9px;
      font-size: 11px;
    }

    .mini-days button:hover,
    .mini-days button.active {
      color: white;
      background: var(--primary);
    }

    .mini-days button.muted {
      color: #c5cbd6;
    }

    .mini-days button.has-tasks::after {
      position: absolute;
      bottom: 3px;
      left: 50%;
      width: 4px;
      height: 4px;
      content: "";
      background: var(--success);
      border-radius: 50%;
      transform: translateX(-50%);
    }

    .mini-days button.active.has-tasks::after {
      background: white;
    }

    .side-section-title {
      margin: 0 0 12px;
      color: var(--muted);
      font-size: 11px;
      font-weight: 800;
      letter-spacing: 1px;
      text-transform: uppercase;
    }

    .nav-list {
      display: grid;
      gap: 7px;
      margin-bottom: 23px;
    }

    .nav-item {
      display: flex;
      align-items: center;
      gap: 11px;
      width: 100%;
      padding: 11px 12px;
      color: #596579;
      background: transparent;
      border-radius: 13px;
      text-align: left;
      font-size: 14px;
      font-weight: 700;
    }

    .nav-item:hover,
    .nav-item.active {
      color: var(--primary);
      background: var(--accent);
    }

    .nav-item span:first-child {
      width: 20px;
      text-align: center;
      font-size: 17px;
    }

    .progress-card {
      padding: 16px;
      color: white;
      background: linear-gradient(145deg, #26345b, #4d5b9c);
      border-radius: 18px;
      box-shadow: 0 12px 25px rgba(45, 58, 103, 0.2);
    }

    .progress-card p {
      margin: 0 0 13px;
      color: rgba(255, 255, 255, 0.72);
      font-size: 12px;
    }

    .progress-top {
      margin-bottom: 9px;
    }

    .progress-top strong {
      font-size: 22px;
    }

    .progress-top span {
      color: rgba(255, 255, 255, 0.72);
      font-size: 12px;
    }

    .progress-track {
      height: 7px;
      overflow: hidden;
      background: rgba(255, 255, 255, 0.2);
      border-radius: 99px;
    }

    .progress-fill {
      width: 0;
      height: 100%;
      background: #79e0bb;
      border-radius: inherit;
      transition: width 0.3s ease;
    }

    .calendar-panel {
      min-width: 0;
      padding: 28px;
      border-radius: var(--radius);
    }

    .calendar-heading {
      align-items: flex-end;
      margin-bottom: 24px;
    }

    .calendar-heading h2 {
      margin: 0;
      font-size: clamp(24px, 3vw, 34px);
      letter-spacing: -1px;
    }

    .calendar-heading p {
      margin: 6px 0 0;
      color: var(--muted);
      font-size: 14px;
    }

    .view-switcher {
      display: flex;
      padding: 4px;
      background: #f0f3f9;
      border-radius: 12px;
    }

    .view-switcher button {
      padding: 8px 13px;
      color: var(--muted);
      background: transparent;
      border-radius: 9px;
      font-size: 12px;
      font-weight: 700;
    }

    .view-switcher button.active {
      color: var(--text);
      background: white;
      box-shadow: 0 3px 10px rgba(36, 50, 77, 0.08);
    }

    .week-grid {
      display: grid;
      grid-template-columns: repeat(7, minmax(150px, 1fr));
      gap: 13px;
      overflow-x: auto;
      padding: 2px 2px 10px;
    }

    .day-column {
      min-width: 150px;
      min-height: 445px;
      padding: 14px;
      background: rgba(248, 250, 253, 0.82);
      border: 1px solid var(--line);
      border-radius: 19px;
      transition: 0.2s ease;
    }

    .day-column.today {
      border-color: rgba(91, 103, 241, 0.38);
      box-shadow: inset 0 3px 0 var(--primary);
    }

    .day-column.selected {
      background: #f4f4ff;
      border-color: rgba(91, 103, 241, 0.5);
    }

    .day-header {
      padding-bottom: 13px;
      margin-bottom: 12px;
      border-bottom: 1px solid var(--line);
    }

    .day-name {
      color: var(--muted);
      font-size: 11px;
      font-weight: 800;
      letter-spacing: 0.5px;
      text-transform: uppercase;
    }

    .day-number {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-top: 4px;
      font-size: 24px;
      font-weight: 850;
    }

    .today-badge {
      padding: 4px 7px;
      color: var(--primary);
      background: var(--accent);
      border-radius: 7px;
      font-size: 9px;
      letter-spacing: 0.4px;
      text-transform: uppercase;
    }

    .tasks {
      display: grid;
      gap: 9px;
    }

    .task {
      position: relative;
      display: flex;
      gap: 9px;
      padding: 10px 9px;
      background: white;
      border: 1px solid #edf0f6;
      border-radius: 12px;
      box-shadow: 0 5px 14px rgba(51, 70, 106, 0.05);
    }

    .task.done {
      opacity: 0.58;
    }

    .task.done .task-title {
      text-decoration: line-through;
    }

    .task-check {
      flex: 0 0 auto;
      width: 17px;
      height: 17px;
      margin-top: 1px;
      accent-color: var(--success);
      cursor: pointer;
    }

    .task-content {
      min-width: 0;
      padding-right: 5px;
    }

    .task-title {
      margin: 0;
      overflow-wrap: anywhere;
      font-size: 12px;
      font-weight: 750;
      line-height: 1.35;
    }

    .task-time {
      display: block;
      margin-top: 5px;
      color: var(--muted);
      font-size: 10px;
    }

    .task-delete {
      position: absolute;
      top: 7px;
      right: 7px;
      display: grid;
      place-items: center;
      width: 20px;
      height: 20px;
      color: #b7bfcc;
      background: transparent;
      border-radius: 6px;
      opacity: 0;
      transition: 0.2s ease;
    }

    .task:hover .task-delete {
      opacity: 1;
    }

    .task-delete:hover {
      color: var(--danger);
      background: #fff0f1;
    }

    .empty-day {
      padding: 25px 3px;
      color: #aeb7c7;
      font-size: 11px;
      line-height: 1.45;
      text-align: center;
    }

    .add-task {
      width: 100%;
      padding: 9px;
      margin-top: 13px;
      color: var(--primary);
      background: transparent;
      border: 1px dashed #c9d0ed;
      border-radius: 10px;
      font-size: 11px;
      font-weight: 800;
    }

    .add-task:hover {
      background: var(--accent);
      border-color: var(--primary);
    }

    .footer-note {
      margin-top: 18px;
      color: var(--muted);
      font-size: 12px;
      text-align: center;
    }

    .modal-backdrop {
      position: fixed;
      z-index: 10;
      inset: 0;
      display: none;
      place-items: center;
      padding: 20px;
      background: rgba(18, 29, 52, 0.38);
      backdrop-filter: blur(7px);
    }

    .modal-backdrop.open {
      display: grid;
    }

    .modal {
      width: min(460px, 100%);
      padding: 25px;
      background: white;
      border-radius: 22px;
      box-shadow: 0 25px 80px rgba(24, 39, 71, 0.28);
      animation: modal-in 0.2s ease;
    }

    @keyframes modal-in {
      from {
        opacity: 0;
        transform: translateY(8px) scale(0.98);
      }
      to {
        opacity: 1;
        transform: translateY(0) scale(1);
      }
    }

    .modal h3 {
      margin: 0;
      font-size: 22px;
    }

    .modal-subtitle {
      margin: 6px 0 20px;
      color: var(--muted);
      font-size: 13px;
    }

    .form-field {
      display: grid;
      gap: 7px;
      margin-bottom: 14px;
    }

    .form-field label {
      color: #657188;
      font-size: 12px;
      font-weight: 800;
    }

    .form-field input,
    .form-field textarea {
      width: 100%;
      padding: 12px 13px;
      color: var(--text);
      background: #f8faff;
      border: 1px solid var(--line);
      border-radius: 12px;
      outline: none;
      resize: vertical;
    }

    .form-field input:focus,
    .form-field textarea:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(91, 103, 241, 0.12);
    }

    .modal-actions {
      display: flex;
      justify-content: flex-end;
      gap: 9px;
      margin-top: 20px;
    }

    @media (max-width: 1050px) {
      .dashboard {
        grid-template-columns: 1fr;
      }

      .sidebar {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        gap: 20px;
      }

      .mini-calendar,
      .nav-list {
        margin: 0;
      }

      .mini-calendar {
        padding: 0;
        border: 0;
      }

      .progress-card {
        align-self: start;
      }
    }

    @media (max-width: 700px) {
      .app {
        padding: 16px;
      }

      .topbar,
      .calendar-heading {
        align-items: flex-start;
        flex-direction: column;
      }

      .top-actions {
        width: 100%;
      }

      .top-actions .primary-button {
        flex: 1;
      }

      .sidebar {
        display: block;
      }

      .mini-calendar {
        padding-bottom: 20px;
        margin-bottom: 20px;
        border-bottom: 1px solid var(--line);
      }

      .nav-list {
        margin-bottom: 20px;
      }

      .calendar-panel {
        padding: 18px 13px;
      }

      .calendar-heading {
        gap: 15px;
      }

      .view-switcher {
        align-self: stretch;
      }

      .view-switcher button {
        flex: 1;
      }
    }
  </style>
</head>
<body>
  <main class="app">
    <header class="topbar">
      <div class="brand">
        <div class="brand-icon">✓</div>
        <div>
          <h1>Мой распорядок</h1>
          <p>Планируй неделю спокойно и уверенно</p>
        </div>
      </div>

      <div class="top-actions">
        <button class="icon-button" id="todayButton" title="Перейти к текущей неделе">⌖</button>
        <button class="outline-button" id="clearButton">Очистить неделю</button>
        <button class="primary-button" id="openModalButton">＋ Новая задача</button>
      </div>
    </header>

    <section class="dashboard">
      <aside class="sidebar">
        <div class="mini-calendar">
          <div class="mini-calendar-header">
            <button id="previousMonth" aria-label="Предыдущий месяц">‹</button>
            <strong id="miniMonth"></strong>
            <button id="nextMonth" aria-label="Следующий месяц">›</button>
          </div>
          <div class="weekdays">
            <span>Пн</span>
            <span>Вт</span>
            <span>Ср</span>
            <span>Чт</span>
            <span>Пт</span>
            <span>Сб</span>
            <span>Вс</span>
          </div>
          <div class="mini-days" id="miniDays"></div>
        </div>

        <div class="nav-list">
          <p class="side-section-title">Навигация</p>
          <button class="nav-item active" data-view="week">
            <span>▦</span>
            <span>Моя неделя</span>
          </button>
          <button class="nav-item" id="allTasksButton">
            <span>✓</span>
            <span>Все задачи</span>
          </button>
        </div>

        <div class="progress-card">
          <p>Прогресс недели</p>
          <div class="progress-top">
            <strong id="progressPercent">0%</strong>
            <span id="progressCount">0 из 0</span>
          </div>
          <div class="progress-track">
            <div class="progress-fill" id="progressFill"></div>
          </div>
        </div>
      </aside>

      <section class="calendar-panel">
        <div class="calendar-heading">
          <div>
            <h2 id="weekTitle"></h2>
            <p id="weekSubtitle"></p>
          </div>

          <div class="view-switcher">
            <button class="active">Неделя</button>
            <button id="compactButton">Компактно</button>
          </div>
        </div>

        <div class="week-grid" id="weekGrid"></div>
        <div class="footer-note">Данные сохраняются автоматически в этом браузере</div>
      </section>
    </section>
  </main>

  <div class="modal-backdrop" id="modalBackdrop">
    <form class="modal" id="taskForm">
      <h3>Новая задача</h3>
      <p class="modal-subtitle" id="modalSubtitle">Добавь план в свой распорядок</p>

      <div class="form-field">
        <label for="taskTitle">Название задачи</label>
        <input id="taskTitle" type="text" placeholder="Например: тренировка или чтение" maxlength="100" required />
      </div>

      <div class="form-field">
        <label for="taskTime">Время</label>
        <input id="taskTime" type="time" />
      </div>

      <div class="form-field">
        <label for="taskNote">Заметка</label>
        <textarea id="taskNote" rows="3" placeholder="Дополнительные детали"></textarea>
      </div>

      <div class="modal-actions">
        <button type="button" class="outline-button" id="closeModalButton">Отмена</button>
        <button type="submit" class="primary-button">Добавить задачу</button>
      </div>
    </form>
  </div>

  <script>
    (() => {
      "use strict";

      const STORAGE_KEY = "personal-week-planner-v1";
      const weekdayNames = ["Пн", "Вт", "Ср", "Чт", "Пт", "Сб", "Вс"];
      const monthNames = [
        "январь", "февраль", "март", "апрель", "май", "июнь",
        "июль", "август", "сентябрь", "октябрь", "ноябрь", "декабрь"
      ];
      const monthNamesGenitive = [
        "января", "февраля", "марта", "апреля", "мая", "июня",
        "июля", "августа", "сентября", "октября", "ноября", "декабря"
      ];

      const state = {
        selectedDate: startOfDay(new Date()),
        weekStart: getMonday(new Date()),
        miniMonth: new Date(new Date().getFullYear(), new Date().getMonth(), 1),
        tasks: loadTasks(),
        compact: false
      };

      const elements = {
        weekGrid: document.getElementById("weekGrid"),
        weekTitle: document.getElementById("weekTitle"),
        weekSubtitle: document.getElementById("weekSubtitle"),
        miniMonth: document.getElementById("miniMonth"),
        miniDays: document.getElementById("miniDays"),
        progressPercent: document.getElementById("progressPercent"),
        progressCount: document.getElementById("progressCount"),
        progressFill: document.getElementById("progressFill"),
        modalBackdrop: document.getElementById("modalBackdrop"),
        taskForm: document.getElementById("taskForm"),
        taskTitle: document.getElementById("taskTitle"),
        taskTime: document.getElementById("taskTime"),
        taskNote: document.getElementById("taskNote"),
        modalSubtitle: document.getElementById("modalSubtitle")
      };

      function startOfDay(date) {
        return new Date(date.getFullYear(), date.getMonth(), date.getDate());
      }

      function getMonday(date) {
        const result = startOfDay(date);
        const day = result.getDay();
        const diff = day === 0 ? -6 : 1 - day;
        result.setDate(result.getDate() + diff);
        return result;
      }

      function addDays(date, amount) {
        const result = new Date(date);
        result.setDate(result.getDate() + amount);
        return result;
      }

      function dateKey(date) {
        const year = date.getFullYear();
        const month = String(date.getMonth() + 1).padStart(2, "0");
        const day = String(date.getDate()).padStart(2, "0");
        return `${year}-${month}-${day}`;
      }

      function sameDate(first, second) {
        return dateKey(first) === dateKey(second);
      }

      function formatRange(start, end) {
        if (start.getMonth() === end.getMonth()) {
          return `${start.getDate()}–${end.getDate()} ${monthNamesGenitive[end.getMonth()]}`;
        }

        return `${start.getDate()} ${monthNamesGenitive[start.getMonth()]} – ${end.getDate()} ${monthNamesGenitive[end.getMonth()]}`;
      }

      function escapeHtml(value) {
        return String(value)
          .replaceAll("&", "&amp;")
          .replaceAll("<", "&lt;")
          .replaceAll(">", "&gt;")
          .replaceAll('"', "&quot;")
          .replaceAll("'", "&#039;");
      }

      function loadTasks() {
        try {
          const saved = localStorage.getItem(STORAGE_KEY);
          const parsed = saved ? JSON.parse(saved) : {};
          return parsed && typeof parsed === "object" ? parsed : {};
        } catch (error) {
          console.warn("Не удалось загрузить задачи:", error);
          return {};
        }
      }

      function saveTasks() {
        try {
          localStorage.setItem(STORAGE_KEY, JSON.stringify(state.tasks));
        } catch (error) {
          alert("Не удалось сохранить данные. Проверь доступ браузера к localStorage.");
          console.error(error);
        }
      }

      function getTasks(date) {
        return Array.isArray(state.tasks[dateKey(date)]) ? state.tasks[dateKey(date)] : [];
      }

      function render() {
        renderHeader();
        renderWeek();
        renderMiniCalendar();
        renderProgress();
      }

      function renderHeader() {
        const weekEnd = addDays(state.weekStart, 6);
        elements.weekTitle.textContent = "Моя неделя";
        elements.weekSubtitle.textContent = `${formatRange(state.weekStart, weekEnd)} · ${state.tasksCount || ""}`.replace(" · ", " · ");
      }

      function renderWeek() {
        elements.weekGrid.classList.toggle("compact", state.compact);
        elements.weekGrid.innerHTML = "";

        for (let index = 0; index < 7; index += 1) {
          const date = addDays(state.weekStart, index);
          const tasks = getTasks(date);
          const column = document.createElement("article");

          column.className = "day-column";
          if (sameDate(date, new Date())) column.classList.add("today");
          if (sameDate(date, state.selectedDate)) column.classList.add("selected");

          const taskMarkup = tasks.length
            ? tasks.map((task, taskIndex) => `
                <div class="task ${task.done ? "done" : ""}">
                  <input
                    class="task-check"
                    type="checkbox"
                    ${task.done ? "checked" : ""}
                    data-action="toggle"
                    data-date="${dateKey(date)}"
                    data-index="${taskIndex}"
                    aria-label="Отметить задачу выполненной"
                  />
                  <div class="task-content">
                    <p class="task-title">${escapeHtml(task.title)}</p>
                    ${task.time ? `<span class="task-time">◷ ${escapeHtml(task.time)}</span>` : ""}
                    ${task.note ? `<span class="task-time">${escapeHtml(task.note)}</span>` : ""}
                  </div>
                  <button
                    class="task-delete"
                    data-action="delete"
                    data-date="${dateKey(date)}"
                    data-index="${taskIndex}"
                    aria-label="Удалить задачу"
                  >×</button>
                </div>
              `).join("")
            : `<div class="empty-day">Пока свободно.<br />Добавь свой план</div>`;

          column.innerHTML = `
            <div class="day-header">
              <div class="day-name">${weekdayNames[index]}</div>
              <div class="day-number">
                <span>${date.getDate()}</span>
                ${sameDate(date, new Date()) ? '<span class="today-badge">Сегодня</span>' : ""}
              </div>
            </div>
            <div class="tasks">${taskMarkup}</div>
            <button class="add-task" data-action="add" data-date="${dateKey(date)}">＋ Добавить</button>
          `;

          elements.weekGrid.appendChild(column);
        }
      }

      function renderMiniCalendar() {
        const year = state.miniMonth.getFullYear();
        const month = state.miniMonth.getMonth();

        elements.miniMonth.textContent = `${monthNames[month]} ${year}`;
        elements.miniDays.innerHTML = "";

        const firstDay = new Date(year, month, 1);
        const offset = firstDay.getDay() === 0 ? 6 : firstDay.getDay() - 1;
        const daysInMonth = new Date(year, month + 1, 0).getDate();
        const previousMonthDays = new Date(year, month, 0).getDate();

        for (let cell = 0; cell < 42; cell += 1) {
          let dayNumber;
          let cellDate;
          let muted = false;

          if (cell < offset) {
            dayNumber = previousMonthDays - offset + cell + 1;
            cellDate = new Date(year, month - 1, dayNumber);
            muted = true;
          } else if (cell >= offset + daysInMonth) {
            dayNumber = cell - offset - daysInMonth + 1;
            cellDate = new Date(year, month + 1, dayNumber);
            muted = true;
          } else {
            dayNumber = cell - offset + 1;
            cellDate = new Date(year, month, dayNumber);
          }

          const button = document.createElement("button");
          button.textContent = dayNumber;
          button.dataset.date = dateKey(cellDate);

          if (muted) button.classList.add("muted");
          if (sameDate(cellDate, state.selectedDate)) button.classList.add("active");
          if (getTasks(cellDate).length > 0) button.classList.add("has-tasks");

          button.addEventListener("click", () => {
            state.selectedDate = cellDate;
            state.weekStart = getMonday(cellDate);
            state.miniMonth = new Date(cellDate.getFullYear(), cellDate.getMonth(), 1);
            render();
          });

          elements.miniDays.appendChild(button);
        }
      }

      function renderProgress() {
        const weekDates = Array.from({ length: 7 }, (_, index) => addDays(state.weekStart, index));
        const allTasks = weekDates.flatMap(getTasks);
        const completed = allTasks.filter((task) => task.done).length;
        const total = allTasks.length;
        const percent = total ? Math.round((completed / total) * 100) : 0;

        elements.progressPercent.textContent = `${percent}%`;
        elements.progressCount.textContent = `${completed} из ${total}`;
        elements.progressFill.style.width = `${percent}%`;
      }

      function openModal(date = state.selectedDate) {
        state.selectedDate = startOfDay(date);
        elements.modalSubtitle.textContent =
          `Задача на ${weekdayNames[(date.getDay() + 6) % 7]}, ${date.getDate()} ${monthNamesGenitive[date.getMonth()]}`;
        elements.taskForm.reset();
        elements.modalBackdrop.classList.add("open");
        setTimeout(() => elements.taskTitle.focus(), 0);
      }

      function closeModal() {
        elements.modalBackdrop.classList.remove("open");
      }

      function addTask(event) {
        event.preventDefault();

        const title = elements.taskTitle.value.trim();
        if (!title) {
          elements.taskTitle.focus();
          return;
        }

        const key = dateKey(state.selectedDate);
        if (!Array.isArray(state.tasks[key])) state.tasks[key] = [];

        state.tasks[key].push({
          id: `${Date.now()}-${Math.random().toString(16).slice(2)}`,
          title,
          time: elements.taskTime.value,
          note: elements.taskNote.value.trim(),
          done: false
        });

        saveTasks();
        closeModal();
        render();
      }

      function clearWeek() {
        const weekDates = Array.from({ length: 7 }, (_, index) => dateKey(addDays(state.weekStart, index)));
        const hasTasks = weekDates.some((key) => Array.isArray(state.tasks[key]) && state.tasks[key].length);

        if (!hasTasks) {
          alert("В этой неделе пока нет задач.");
          return;
        }

        if (!confirm("Удалить все задачи текущей недели?")) return;

        weekDates.forEach((key) => delete state.tasks[key]);
        saveTasks();
        render();
      }

      elements.weekGrid.addEventListener("click", (event) => {
        const target = event.target.closest("[data-action]");
        if (!target) return;

        const action = target.dataset.action;
        const date = new Date(`${target.dataset.date}T00:00:00`);
        const index = Number(target.dataset.index);

        if (action === "add") {
          openModal(date);
          return;
        }

        if (action === "delete") {
          const tasks = getTasks(date);
          if (!tasks[index]) return;
          tasks.splice(index, 1);
          if (!tasks.length) delete state.tasks[dateKey(date)];
          saveTasks();
          render();
        }
      });

      elements.weekGrid.addEventListener("change", (event) => {
        const target = event.target.closest('[data-action="toggle"]');
        if (!target) return;

        const date = new Date(`${target.dataset.date}T00:00:00`);
        const index = Number(target.dataset.index);
        const tasks = getTasks(date);

        if (!tasks[index]) return;
        tasks[index].done = target.checked;
        saveTasks();
        render();
      });

      document.getElementById("openModalButton").addEventListener("click", () => openModal());
      document.getElementById("closeModalButton").addEventListener("click", closeModal);
      document.getElementById("clearButton").addEventListener("click", clearWeek);

      document.getElementById("todayButton").addEventListener("click", () => {
        const today = startOfDay(new Date());
        state.selectedDate = today;
        state.weekStart = getMonday(today);
        state.miniMonth = new Date(today.getFullYear(), today.getMonth(), 1);
        render();
      });

      document.getElementById("previousMonth").addEventListener("click", () => {
        state.miniMonth = new Date(
          state.miniMonth.getFullYear(),
          state.miniMonth.getMonth() - 1,
          1
        );
        renderMiniCalendar();
      });

      document.getElementById("nextMonth").addEventListener("click", () => {
        state.miniMonth = new Date(
          state.miniMonth.getFullYear(),
          state.miniMonth.getMonth() + 1,
          1
        );
        renderMiniCalendar();
      });

      document.getElementById("allTasksButton").addEventListener("click", () => {
        const total = Object.values(state.tasks).reduce(
          (sum, tasks) => sum + (Array.isArray(tasks) ? tasks.length : 0),
          0
        );
        alert(`Всего задач в расписании: ${total}`);
      });

      document.getElementById("compactButton").addEventListener("click", (event) => {
        state.compact = !state.compact;
        event.currentTarget.classList.toggle("active", state.compact);
        elements.weekGrid.style.gridTemplateColumns = state.compact
          ? "repeat(7, minmax(120px, 1fr))"
          : "";
      });

      elements.taskForm.addEventListener("submit", addTask);

      elements.modalBackdrop.addEventListener("click", (event) => {
        if (event.target === elements.modalBackdrop) closeModal();
      });

      document.addEventListener("keydown", (event) => {
        if (event.key === "Escape") closeModal();
      });

      render();
    })();
  </script>
</body>
</html>
