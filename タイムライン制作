<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Simple Timeline Mobile - Header UI</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        :root {
            --bg-color: #f2f2f7;
            --card-bg: #ffffff;
            --accent: #007aff;
            --text: #1c1c1e;
            --border: #d1d1d6;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            background-color: var(--bg-color);
            color: var(--text);
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            -webkit-tap-highlight-color: transparent;
        }

        .container {
            width: 100%;
            max-width: 500px;
            padding: 16px;
            box-sizing: border-box;
            padding-bottom: 60px;
        }

        /* --- Header Section with Theme Switcher --- */
        header {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            margin: 20px 0;
            position: relative;
        }

        h1 {
            font-size: 1.4rem;
            margin: 0;
            font-weight: 700;
        }

        .theme-container {
            position: relative;
            display: flex;
            align-items: center;
        }

        .theme-trigger {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background: var(--accent);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            border: none;
            transition: transform 0.3s ease;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .theme-container.open .theme-trigger {
            transform: rotate(45deg);
        }

        .color-options {
            position: absolute;
            left: 48px;
            display: flex;
            gap: 8px;
            background: var(--card-bg);
            padding: 6px;
            border-radius: 20px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            opacity: 0;
            transform: translateX(-10px);
            pointer-events: none;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            border: 1px solid var(--border);
        }

        .theme-container.open .color-options {
            opacity: 1;
            transform: translateX(0);
            pointer-events: auto;
        }

        .color-dot {
            width: 28px;
            height: 28px;
            border-radius: 50%;
            cursor: pointer;
            border: 2px solid white;
            box-shadow: 0 1px 4px rgba(0,0,0,0.1);
            transition: transform 0.2s;
        }

        .color-dot:active {
            transform: scale(0.85);
        }

        /* --- Input section --- */
        .input-group {
            background: var(--card-bg);
            padding: 16px;
            border-radius: 20px;
            box-shadow: 0 4px 16px rgba(0,0,0,0.04);
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 20px;
        }

        .input-row {
            display: flex;
            gap: 8px;
        }

        input[id="timeInput"] {
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 12px;
            font-size: 16px; 
            font-family: inherit;
            background: #fff;
            width: 80px;
            text-align: center;
        }

        input[id="taskInput"] {
            flex: 1;
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 12px;
            font-size: 16px;
            background: #fff;
        }

        .add-btn {
            background: var(--accent);
            color: white;
            border: none;
            border-radius: 10px;
            padding: 14px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
        }

        .save-btn {
            width: 100%;
            background: transparent;
            color: var(--accent);
            border: 2px solid var(--accent);
            border-radius: 12px;
            padding: 12px;
            margin-bottom: 24px;
            cursor: pointer;
            font-size: 15px;
            font-weight: 600;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        /* --- Timeline area --- */
        #capture-area {
            background-color: var(--bg-color);
            padding: 10px 5px;
        }

        .timeline {
            position: relative;
            padding-left: 24px;
            margin-left: 10px;
        }

        .timeline::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            bottom: 0;
            width: 2px;
            background: var(--border);
        }

        .item {
            background: var(--card-bg);
            margin-bottom: 12px;
            padding: 16px;
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            position: relative;
            box-shadow: 0 2px 8px rgba(0,0,0,0.03);
        }

        .item::before {
            content: '';
            position: absolute;
            left: -30px;
            top: 50%;
            transform: translateY(-50%);
            width: 12px;
            height: 12px;
            background: var(--accent);
            border-radius: 50%;
            border: 3px solid var(--bg-color);
        }

        .time {
            font-weight: 700;
            font-size: 15px;
            min-width: 50px;
        }

        .task {
            font-size: 15px;
            line-height: 1.4;
            color: #3a3a3c;
        }

        .delete-btn {
            background: none;
            color: #ff3b30;
            opacity: 0.3;
            border: none;
            padding: 8px;
            font-size: 12px;
            cursor: pointer;
        }

        .no-capture {
            display: none !important;
        }

        @media (max-width: 350px) {
            .input-row { flex-direction: column; }
            input[id="timeInput"] { width: 100%; }
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>Timeline</h1>
        <div class="theme-container" id="themeContainer">
            <button class="theme-trigger" onclick="toggleMenu()">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="13.5" cy="6.5" r=".5"/><circle cx="17.5" cy="10.5" r=".5"/><circle cx="8.5" cy="7.5" r=".5"/><circle cx="6.5" cy="12.5" r=".5"/><path d="M12 2C6.5 2 2 6.5 2 12s4.5 10 10 10c.92 0 1.7-.39 2.3-1.03a1.73 1.73 0 0 0 .4-1.3c-.15-1 .57-1.67 1.3-1.67H18c2.2 0 4-1.8 4-4a8 8 0 0 0-10-8Z"/></svg>
            </button>
            <div class="color-options">
                <div class="color-dot" style="background-color: #007aff;" onclick="setTheme('#007aff')"></div>
                <div class="color-dot" style="background-color: #34c759;" onclick="setTheme('#34c759')"></div>
                <div class="color-dot" style="background-color: #ff9500;" onclick="setTheme('#ff9500')"></div>
                <div class="color-dot" style="background-color: #ff3b30;" onclick="setTheme('#ff3b30')"></div>
                <div class="color-dot" style="background-color: #5856d6;" onclick="setTheme('#5856d6')"></div>
                <div class="color-dot" style="background-color: #1c1c1e;" onclick="setTheme('#1c1c1e')"></div>
            </div>
        </div>
    </header>

    <div class="input-group">
        <div class="input-row">
            <input type="text" id="timeInput" placeholder="00:00" inputmode="numeric" maxlength="5">
            <input type="text" id="taskInput" placeholder="予定を入力" onkeypress="handleKey(event)">
        </div>
        <button class="add-btn" id="addBtn" onclick="addSchedule()">追加</button>
    </div>

    <button class="save-btn" id="saveBtn" onclick="saveAsImage()">
        <span>📸</span> 画像として保存
    </button>

    <div id="capture-area">
        <div id="timeline" class="timeline"></div>
    </div>
</div>

<script>
    let schedules = JSON.parse(localStorage.getItem('mySchedules')) || [];
    let currentTheme = localStorage.getItem('myThemeColor') || '#007aff';

    function initTheme() {
        document.documentElement.style.setProperty('--accent', currentTheme);
    }

    function toggleMenu() {
        document.getElementById('themeContainer').classList.toggle('open');
    }

    function setTheme(color) {
        currentTheme = color;
        document.documentElement.style.setProperty('--accent', color);
        localStorage.setItem('myThemeColor', color);
        toggleMenu();
    }

    const timeInput = document.getElementById('timeInput');
    timeInput.addEventListener('input', (e) => {
        let val = e.target.value.replace(/\D/g, ''); 
        if (val.length > 2) {
            val = val.slice(0, 2) + ':' + val.slice(2, 4);
        }
        e.target.value = val;
    });

    function render() {
        const timeline = document.getElementById('timeline');
        timeline.innerHTML = '';
        schedules.sort((a, b) => a.time.localeCompare(b.time));

        if (schedules.length === 0) {
            timeline.innerHTML = '<p style="text-align:center; color:#8e8e93; font-size:14px; margin-top:20px;">予定を追加してください</p>';
        }

        schedules.forEach((item, index) => {
            const div = document.createElement('div');
            div.className = 'item';
            div.innerHTML = `
                <div class="item-content">
                    <span class="time">${item.time}</span>
                    <span class="task">${item.task}</span>
                </div>
                <button class="delete-btn" onclick="deleteItem(${index})">✕</button>
            `;
            timeline.appendChild(div);
        });
        localStorage.setItem('mySchedules', JSON.stringify(schedules));
    }

    function addSchedule() {
        const taskInput = document.getElementById('taskInput');
        if (!timeInput.value || !taskInput.value || !timeInput.value.includes(':')) return;
        schedules.push({ time: timeInput.value, task: taskInput.value });
        timeInput.value = '';
        taskInput.value = '';
        render();
        taskInput.blur();
    }

    function deleteItem(index) {
        schedules.splice(index, 1);
        render();
    }

    function handleKey(e) { if (e.key === 'Enter') addSchedule(); }

    async function saveAsImage() {
        const area = document.getElementById('capture-area');
        const deleteButtons = document.querySelectorAll('.delete-btn');
        const saveBtn = document.getElementById('saveBtn');
        const themeContainer = document.getElementById('themeContainer');
        
        saveBtn.innerText = "作成中...";
        saveBtn.disabled = true;
        deleteButtons.forEach(btn => btn.classList.add('no-capture'));
        themeContainer.classList.add('no-capture');

        try {
            const canvas = await html2canvas(area, {
                backgroundColor: '#f2f2f7',
                scale: 3,
                useCORS: true
            });
            const link = document.createElement('a');
            link.download = `timeline_${Date.now()}.png`;
            link.href = canvas.toDataURL('image/png');
            link.click();
        } catch (error) {
            console.error('Save failed:', error);
        } finally {
            deleteButtons.forEach(btn => btn.classList.remove('no-capture'));
            themeContainer.classList.remove('no-capture');
            saveBtn.innerHTML = "<span>📸</span> 画像として保存";
            saveBtn.disabled = false;
        }
    }

    initTheme();
    render();
</script>
</body>
</html>
