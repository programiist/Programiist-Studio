<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Programmiist Studio — Конструктор Сайтов</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            display: flex;
            flex-direction: column;
            height: 100vh;
            background-color: #0b0f19;
            color: #f8fafc;
            overflow: hidden;
        }

        /* Кастомный скроллбар */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0b0f19;
        }
        ::-webkit-scrollbar-thumb {
            background: #334155;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #38bdf8;
        }

        /* Верхняя панель (Header) */
        .top-bar {
            height: 65px;
            background: rgba(30, 41, 59, 0.75);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 25px;
            z-index: 100;
            flex-shrink: 0;
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 14px;
            font-size: 20px;
            font-weight: 800;
            background: linear-gradient(135deg, #38bdf8, #818cf8, #c084fc);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: 0.5px;
        }

        /* АНИМИРОВАННАЯ ИКОНКА С МОЛНИЕЙ */
        .brand-icon {
            position: relative;
            width: 42px;
            height: 42px;
            background: linear-gradient(135deg, #0284c7, #6366f1, #9333ea);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 20px rgba(56, 189, 248, 0.5);
            animation: pulseGlow 3s infinite alternate;
            overflow: hidden;
            flex-shrink: 0;
        }

        @keyframes pulseGlow {
            0% { box-shadow: 0 0 15px rgba(56, 189, 248, 0.4), 0 0 30px rgba(99, 102, 241, 0.2); }
            100% { box-shadow: 0 0 25px rgba(56, 189, 248, 0.8), 0 0 45px rgba(168, 85, 247, 0.5); }
        }

        .brand-icon::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: repeating-conic-gradient(transparent 0deg 180deg, rgba(255, 255, 255, 0.15) 180deg 360deg);
            animation: rotateBg 6s linear infinite;
        }

        @keyframes rotateBg {
            100% { transform: rotate(360deg); }
        }

        .brand-icon svg {
            position: relative;
            width: 26px;
            height: 26px;
            z-index: 2;
            fill: none;
            stroke: #ffffff;
            stroke-width: 2.2;
            stroke-linecap: round;
            stroke-linejoin: round;
            filter: drop-shadow(0 0 6px #ffffff);
        }

        .brand-icon svg path {
            stroke-dasharray: 60;
            stroke-dashoffset: 60;
            animation: lightningStrike 2s ease-in-out infinite;
        }

        @keyframes lightningStrike {
            0% {
                stroke-dashoffset: 60;
                opacity: 0.3;
            }
            40% {
                stroke-dashoffset: 0;
                opacity: 1;
                filter: drop-shadow(0 0 12px #38bdf8);
            }
            60% {
                stroke-dashoffset: 0;
                opacity: 1;
                filter: drop-shadow(0 0 15px #ffffff);
            }
            100% {
                stroke-dashoffset: -60;
                opacity: 0.3;
            }
        }

        .view-toggle {
            display: flex;
            background-color: #0f172a;
            padding: 4px;
            border-radius: 10px;
            gap: 4px;
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        .toggle-btn {
            padding: 7px 18px;
            border: none;
            background: transparent;
            color: #94a3b8;
            border-radius: 7px;
            cursor: pointer;
            font-weight: 600;
            font-size: 13px;
            transition: all 0.3s ease;
        }

        .toggle-btn.active {
            background: linear-gradient(135deg, #38bdf8, #3b82f6);
            color: #0f172a;
            box-shadow: 0 0 12px rgba(56, 189, 248, 0.4);
        }

        /* Главный контейнер */
        .main-container {
            display: flex;
            flex: 1;
            overflow: hidden;
        }

        /* Боковые панели */
        .sidebar {
            width: 300px;
            background-color: #111827;
            border-right: 1px solid rgba(255, 255, 255, 0.08);
            display: flex;
            flex-direction: column;
            padding: 20px;
            gap: 12px;
            overflow-y: auto;
            flex-shrink: 0;
        }

        .sidebar-right {
            border-right: none;
            border-left: 1px solid rgba(255, 255, 255, 0.08);
        }

        .sidebar h2 {
            font-size: 12px;
            text-transform: uppercase;
            letter-spacing: 1.2px;
            color: #38bdf8;
            margin-top: 10px;
            margin-bottom: 5px;
            font-weight: 700;
        }

        .sidebar h2:first-child {
            margin-top: 0;
        }

        .btn-element {
            padding: 10px 14px;
            background: #1e293b;
            border: 1px solid #334155;
            color: #f8fafc;
            border-radius: 8px;
            cursor: pointer;
            text-align: left;
            font-weight: 500;
            font-size: 13px;
            transition: all 0.25s ease;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .btn-element:hover {
            background: linear-gradient(135deg, rgba(56, 189, 248, 0.15), rgba(99, 102, 241, 0.15));
            border-color: #38bdf8;
            color: #38bdf8;
            transform: translateX(3px);
            box-shadow: 0 0 10px rgba(56, 189, 248, 0.2);
        }

        .btn-danger {
            background: rgba(239, 68, 68, 0.1);
            color: #f87171;
            border: 1px solid rgba(239, 68, 68, 0.3);
            margin-top: 10px;
        }

        .btn-danger:hover {
            background: #ef4444;
            color: #ffffff;
            border-color: #ef4444;
            box-shadow: 0 0 12px rgba(239, 68, 68, 0.4);
            transform: none;
        }

        /* РАБОЧАЯ ОБЛАСТЬ (ИСПРАВЛЕНА ПРОКРУТКА) */
        .workspace {
            flex: 1;
            padding: 25px;
            overflow-y: scroll; /* Принудительно включаем скролл вниз */
            display: flex;
            flex-direction: column;
            align-items: center;
            background: radial-gradient(circle at center, #1e293b 0%, #0b0f19 100%);
            height: 100%;
        }

        .canvas {
            width: 100%;
            max-width: 850px;
            min-height: 550px;
            background-color: #ffffff;
            color: #1e293b;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5), 0 0 1px rgba(255, 255, 255, 0.2);
            transition: all 0.2s;
            margin-bottom: 50px; /* Отступ снизу для комфортного скролла */
        }

        /* Текстовый редактор кода */
        .code-editor-container {
            width: 100%;
            max-width: 850px;
            height: 100%;
            display: none;
            flex-direction: column;
            gap: 10px;
        }

        .code-editor {
            width: 100%;
            height: 500px;
            background-color: #0f172a;
            color: #38bdf8;
            border: 1px solid #334155;
            border-radius: 10px;
            padding: 18px;
            font-family: 'Fira Code', 'Courier New', Courier, monospace;
            font-size: 14px;
            line-height: 1.5;
            resize: vertical;
            outline: none;
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
        }

        .code-editor:focus {
            border-color: #38bdf8;
            box-shadow: 0 0 15px rgba(56, 189, 248, 0.3);
        }

        /* Элементы на холсте */
        .canvas-item {
            position: relative;
            margin-bottom: 15px;
            padding: 8px;
            border: 1px dashed transparent;
            border-radius: 6px;
            cursor: pointer;
            transition: border-color 0.2s;
        }

        .canvas-item:hover {
            border-color: #38bdf8;
        }

        .canvas-item.selected {
            border-color: #818cf8;
            outline: 2px solid #818cf8;
            box-shadow: 0 0 10px rgba(129, 140, 248, 0.3);
        }

        .canvas-item .delete-btn {
            position: absolute;
            top: -10px;
            right: -10px;
            background: linear-gradient(135deg, #f43f5e, #e11d48);
            color: white;
            border: none;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            font-size: 12px;
            cursor: pointer;
            display: none;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 8px rgba(0,0,0,0.3);
            z-index: 10;
            transition: transform 0.2s;
        }

        .canvas-item .delete-btn:hover {
            transform: scale(1.15);
        }

        .canvas-item:hover .delete-btn {
            display: flex;
        }

        /* Формы настройки */
        .control-group {
            display: flex;
            flex-direction: column;
            gap: 6px;
            margin-bottom: 12px;
        }

        .control-group label {
            font-size: 12px;
            color: #94a3b8;
        }

        .control-group input, .control-group select {
            padding: 9px 12px;
            background-color: #0f172a;
            border: 1px solid #334155;
            color: #f8fafc;
            border-radius: 6px;
            font-size: 13px;
            outline: none;
            transition: border-color 0.2s;
        }

        .control-group input:focus, .control-group select:focus {
            border-color: #38bdf8;
        }

        .control-group input[type="color"] {
            height: 38px;
            cursor: pointer;
            padding: 4px;
        }

        .action-btn {
            padding: 10px 22px;
            background: linear-gradient(135deg, #0284c7, #38bdf8);
            color: #0f172a;
            border: none;
            border-radius: 8px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 0 15px rgba(56, 189, 248, 0.3);
        }

        .action-btn:hover {
            transform: translateY(-1px);
            box-shadow: 0 0 22px rgba(56, 189, 248, 0.6);
        }
    </style>
</head>
<body>

    <!-- Шапка сайта -->
    <div class="top-bar">
        <div class="brand">
            <div class="brand-icon">
                <svg viewBox="0 0 24 24">
                    <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"></path>
                </svg>
            </div>
            Programmiist Studio
        </div>
        <div class="view-toggle">
            <button class="toggle-btn active" id="btn-view-visual" onclick="switchView('visual')">Визуальный редактор</button>
            <button class="toggle-btn" id="btn-view-code" onclick="switchView('code')">Редактор кода (HTML)</button>
        </div>
        <button class="action-btn" onclick="exportHTML()">Скачать HTML</button>
    </div>

    <!-- Основное рабочее пространство -->
    <div class="main-container">
        
        <!-- Левая панель -->
        <div class="sidebar">
            <h2>Базовые блоки</h2>
            <button class="btn-element" onclick="addElement('navbar')">Шапка (Nav) <span>+</span></button>
            <button class="btn-element" onclick="addElement('header')">Заголовок <span>+</span></button>
            <button class="btn-element" onclick="addElement('text')">Текст <span>+</span></button>
            <button class="btn-element" onclick="addElement('button')">Кнопка «Узнать больше» <span>+</span></button>
            <button class="btn-element" onclick="addElement('image')">Изображение <span>+</span></button>
            <button class="btn-element" onclick="addElement('divider')">Разделитель <span>+</span></button>
            <button class="btn-element" onclick="addElement('footer')">Подвал (Footer) <span>+</span></button>

            <h2>Сложные блоки</h2>
            <button class="btn-element" onclick="addElement('card')">Карточка <span>+</span></button>
            <button class="btn-element" onclick="addElement('grid3')">Сетка (3 карточки) <span>+</span></button>
            <button class="btn-element" onclick="addElement('gallery2')">Галерея (2 фото) <span>+</span></button>
            <button class="btn-element" onclick="addElement('form')">Форма заявки <span>+</span></button>
            <button class="btn-element" onclick="addElement('faq')">Блок FAQ <span>+</span></button>

            <h2>Настройки страницы</h2>
            <div class="control-group">
                <label>Фон холста:</label>
                <input type="color" id="page-bg-color" value="#ffffff" onchange="changeCanvasBg(this.value)">
            </div>
            <div class="control-group">
                <label>Отступы холста (px):</label>
                <input type="number" id="page-padding" value="25" min="0" max="100" onchange="changeCanvasPadding(this.value)">
            </div>
            <div class="control-group">
                <label>Шрифт страницы:</label>
                <select id="page-font" onchange="changeCanvasFont(this.value)">
                    <option value="'Segoe UI', sans-serif">Segoe UI</option>
                    <option value="Arial, sans-serif">Arial</option>
                    <option value="'Times New Roman', serif">Times New Roman</option>
                    <option value="'Courier New', monospace">Courier New</option>
                </select>
            </div>
            <button class="btn-element btn-danger" onclick="clearCanvas()">Очистить холст 🗑</button>
        </div>

        <!-- Центральная панель с рабочей областью -->
        <div class="workspace">
            <div class="canvas" id="canvas">
                <p id="empty-msg" style="color: #64748b; text-align: center; margin-top: 220px;">
                    Выберите блоки на левой панели для добавления
                </p>
            </div>

            <div class="code-editor-container" id="code-container">
                <label style="color: #94a3b8; font-size: 13px;">Прямое редактирование HTML-кода:</label>
                <textarea class="code-editor" id="code-editor" oninput="applyCodeChanges()"></textarea>
            </div>
        </div>

        <!-- Правая панель: Свойства -->
        <div class="sidebar sidebar-right">
            <h2>Свойства</h2>
            <div id="editor-controls">
                <p style="color: #64748b; font-size: 13px;">Выберите элемент на холсте для настройки</p>
            </div>
        </div>

    </div>

    <script>
        const canvas = document.getElementById('canvas');
        const emptyMsg = document.getElementById('empty-msg');
        const editorControls = document.getElementById('editor-controls');
        const codeEditor = document.getElementById('code-editor');
        const codeContainer = document.getElementById('code-container');
        
        let selectedElement = null;
        let elementCount = 0;
        let currentMode = 'visual';

        function switchView(mode) {
            currentMode = mode;
            document.getElementById('btn-view-visual').classList.toggle('active', mode === 'visual');
            document.getElementById('btn-view-code').classList.toggle('active', mode === 'code');

            if (mode === 'code') {
                updateCodeEditorFromCanvas();
                canvas.style.display = 'none';
                codeContainer.style.display = 'flex';
            } else {
                canvas.style.display = 'block';
                codeContainer.style.display = 'none';
            }
        }

        function changeCanvasBg(color) { canvas.style.backgroundColor = color; }
        function changeCanvasPadding(val) { canvas.style.padding = val + 'px'; }
        function changeCanvasFont(font) { canvas.style.fontFamily = font; }

        function clearCanvas() {
            if (confirm("Вы уверены, что хотите полностью очистить сайт?")) {
                canvas.innerHTML = '';
                if (emptyMsg) {
                    emptyMsg.style.display = 'block';
                    canvas.appendChild(emptyMsg);
                }
                editorControls.innerHTML = '<p style="color: #64748b; font-size: 13px;">Выберите элемент на холсте для настройки</p>';
            }
        }

        function addElement(type) {
            if (emptyMsg) emptyMsg.style.display = 'none';

            elementCount++;
            const wrapper = document.createElement('div');
            wrapper.className = 'canvas-item';
            wrapper.id = 'item-' + elementCount;

            let el;
            if (type === 'navbar') {
                el = document.createElement('nav');
                el.style.display = 'flex';
                el.style.justifyContent = 'space-between';
                el.style.alignItems = 'center';
                el.style.padding = '12px 15px';
                el.style.backgroundColor = '#f1f5f9';
                el.style.borderRadius = '6px';
                el.innerHTML = '<strong style="font-size:18px; color:#0f172a;">Programmiist Site</strong><div><a href="#" style="margin-left:15px; text-decoration:none; color:#334155;">Главная</a><a href="#" style="margin-left:15px; text-decoration:none; color:#334155;">Услуги</a><a href="#" style="margin-left:15px; text-decoration:none; color:#334155;">Контакты</a></div>';
            } else if (type === 'header') {
                el = document.createElement('h1');
                el.innerText = 'Заголовок страницы';
                el.style.color = '#0f172a';
            } else if (type === 'text') {
                el = document.createElement('p');
                el.innerText = 'Это пример текстового блока. Введите сюда любой ваш текст...';
                el.style.color = '#334155';
            } else if (type === 'button') {
                let targetUrl = prompt("Введите ссылку для кнопки (URL):", "https://example.com");
                if (!targetUrl) targetUrl = "#";

                el = document.createElement('a');
                el.innerText = 'Узнать больше';
                el.href = targetUrl;
                el.target = "_blank";
                el.style.display = 'inline-block';
                el.style.padding = '10px 20px';
                el.style.backgroundColor = '#38bdf8';
                el.style.color = '#0f172a';
                el.style.textDecoration = 'none';
                el.style.borderRadius = '6px';
                el.style.fontWeight = 'bold';
            } else if (type === 'image') {
                el = document.createElement('img');
                el.src = 'https://via.placeholder.com/750x250';
                el.style.width = '100%';
                el.style.borderRadius = '6px';
            } else if (type === 'card') {
                el = document.createElement('div');
                el.style.border = '1px solid #e2e8f0';
                el.style.borderRadius = '8px';
                el.style.padding = '15px';
                el.style.backgroundColor = '#f8fafc';
                el.innerHTML = '<h3 style="color:#0f172a;">Название карточки</h3><p style="margin-top:8px; font-size:14px; color:#64748b;">Описание карточки товара или услуги.</p>';
            } else if (type === 'grid3') {
                el = document.createElement('div');
                el.style.display = 'grid';
                el.style.gridTemplateColumns = 'repeat(3, 1fr)';
                el.style.gap = '15px';
                el.innerHTML = `
                    <div style="border:1px solid #e2e8f0; padding:15px; border-radius:6px; background:#f8fafc;">
                        <h4 style="color:#0f172a;">Услуга 1</h4>
                        <p style="font-size:13px; color:#64748b; margin-top:5px;">Описание первого блока услуг.</p>
                    </div>
                    <div style="border:1px solid #e2e8f0; padding:15px; border-radius:6px; background:#f8fafc;">
                        <h4 style="color:#0f172a;">Услуга 2</h4>
                        <p style="font-size:13px; color:#64748b; margin-top:5px;">Описание второго блока услуг.</p>
                    </div>
                    <div style="border:1px solid #e2e8f0; padding:15px; border-radius:6px; background:#f8fafc;">
                        <h4 style="color:#0f172a;">Услуга 3</h4>
                        <p style="font-size:13px; color:#64748b; margin-top:5px;">Описание третьего блока услуг.</p>
                    </div>
                `;
            } else if (type === 'gallery2') {
                el = document.createElement('div');
                el.style.display = 'grid';
                el.style.gridTemplateColumns = '1fr 1fr';
                el.style.gap = '15px';
                el.innerHTML = `
                    <img src="https://via.placeholder.com/350x200" style="width:100%; border-radius:6px;">
                    <img src="https://via.placeholder.com/350x200" style="width:100%; border-radius:6px;">
                `;
            } else if (type === 'form') {
                el = document.createElement('form');
                el.style.border = '1px solid #e2e8f0';
                el.style.padding = '20px';
                el.style.borderRadius = '8px';
                el.style.backgroundColor = '#f8fafc';
                el.onsubmit = (e) => e.preventDefault();
                el.innerHTML = `
                    <h3 style="margin-bottom:12px; color:#0f172a;">Оставить заявку</h3>
                    <input type="text" placeholder="Ваше имя" style="width:100%; padding:8px; margin-bottom:10px; border:1px solid #cbd5e1; border-radius:4px;">
                    <input type="email" placeholder="Ваш Email" style="width:100%; padding:8px; margin-bottom:10px; border:1px solid #cbd5e1; border-radius:4px;">
                    <textarea placeholder="Сообщение" style="width:100%; height:70px; padding:8px; margin-bottom:10px; border:1px solid #cbd5e1; border-radius:4px;"></textarea>
                    <button style="padding:10px 15px; background:#38bdf8; border:none; border-radius:4px; font-weight:bold; cursor:pointer;">Отправить</button>
                `;
            } else if (type === 'faq') {
                el = document.createElement('div');
                el.style.padding = '15px';
                el.style.borderLeft = '4px solid #38bdf8';
                el.style.backgroundColor = '#f1f5f9';
                el.innerHTML = `
                    <h4 style="color:#0f172a;">Вопрос: Как сделать заказ?</h4>
                    <p style="margin-top:5px; font-size:14px; color:#475569;">Ответ: Заполните форму заявки выше или свяжитесь с нами по контактам.</p>
                `;
            } else if (type === 'divider') {
                el = document.createElement('hr');
                el.style.border = 'none';
                el.style.borderTop = '1px solid #cbd5e1';
                el.style.margin = '15px 0';
            } else if (type === 'footer') {
                el = document.createElement('footer');
                el.style.textAlign = 'center';
                el.style.padding = '15px 0';
                el.style.color = '#94a3b8';
                el.style.fontSize = '12px';
                el.innerText = '© 2026 Все права защищены.';
            }

            wrapper.appendChild(el);

            const deleteBtn = document.createElement('button');
            deleteBtn.className = 'delete-btn';
            deleteBtn.innerText = '✕';
            deleteBtn.onclick = (e) => {
                e.stopPropagation();
                wrapper.remove();
                if (canvas.querySelectorAll('.canvas-item').length === 0 && emptyMsg) {
                    emptyMsg.style.display = 'block';
                }
                editorControls.innerHTML = '<p style="color: #64748b; font-size: 13px;">Выберите элемент на холсте для настройки</p>';
            };
            wrapper.appendChild(deleteBtn);

            wrapper.onclick = (e) => {
                e.stopPropagation();
                selectElement(wrapper, el, type);
            };

            canvas.appendChild(wrapper);
            selectElement(wrapper, el, type);

            if (currentMode === 'code') {
                updateCodeEditorFromCanvas();
            }
        }

        function selectElement(wrapper, targetEl, type) {
            document.querySelectorAll('.canvas-item').forEach(item => item.classList.remove('selected'));
            wrapper.classList.add('selected');
            selectedElement = targetEl;

            let html = '';

            if (type === 'header' || type === 'text' || type === 'button' || type === 'footer') {
                html += `
                    <div class="control-group">
                        <label>Текст блока:</label>
                        <input type="text" id="prop-text" value="${targetEl.innerText}">
                    </div>
                `;
            }

            if (type === 'button') {
                html += `
                    <div class="control-group">
                        <label>Ссылка (URL):</label>
                        <input type="text" id="prop-href" value="${targetEl.getAttribute('href')}">
                    </div>
                    <div class="control-group">
                        <label>Цвет кнопки:</label>
                        <input type="color" id="prop-bg" value="${rgbToHex(targetEl.style.backgroundColor)}">
                    </div>
                `;
            }

            if (type === 'image') {
                html += `
                    <div class="control-group">
                        <label>URL Изображения:</label>
                        <input type="text" id="prop-src" value="${targetEl.src}">
                    </div>
                `;
            }

            if (type === 'card' || type === 'navbar' || type === 'form' || type === 'faq') {
                html += `
                    <div class="control-group">
                        <label>Фон блока:</label>
                        <input type="color" id="prop-bg" value="${rgbToHex(targetEl.style.backgroundColor)}">
                    </div>
                `;
            }

            if (type === 'header' || type === 'text' || type === 'footer') {
                html += `
                    <div class="control-group">
                        <label>Цвет текста:</label>
                        <input type="color" id="prop-color" value="${rgbToHex(targetEl.style.color)}">
                    </div>
                    <div class="control-group">
                        <label>Выравнивание:</label>
                        <select id="prop-align">
                            <option value="left" ${targetEl.style.textAlign === 'left' ? 'selected' : ''}>Слева</option>
                            <option value="center" ${targetEl.style.textAlign === 'center' ? 'selected' : ''}>По центру</option>
                            <option value="right" ${targetEl.style.textAlign === 'right' ? 'selected' : ''}>Справа</option>
                        </select>
                    </div>
                `;
            }

            editorControls.innerHTML = html || '<p style="color: #64748b; font-size: 13px;">Для этого элемента нет быстрой настройки</p>';

            const propText = document.getElementById('prop-text');
            if (propText) propText.oninput = (e) => targetEl.innerText = e.target.value;

            const propHref = document.getElementById('prop-href');
            if (propHref) propHref.oninput = (e) => targetEl.setAttribute('href', e.target.value);

            const propBg = document.getElementById('prop-bg');
            if (propBg) propBg.oninput = (e) => targetEl.style.backgroundColor = e.target.value;

            const propSrc = document.getElementById('prop-src');
            if (propSrc) propSrc.oninput = (e) => targetEl.src = e.target.value;

            const propColor = document.getElementById('prop-color');
            if (propColor) propColor.oninput = (e) => targetEl.style.color = e.target.value;

            const propAlign = document.getElementById('prop-align');
            if (propAlign) propAlign.onchange = (e) => targetEl.style.textAlign = e.target.value;
        }

        function updateCodeEditorFromCanvas() {
            const cloneCanvas = canvas.cloneNode(true);
            cloneCanvas.querySelectorAll('.delete-btn').forEach(btn => btn.remove());
            cloneCanvas.querySelectorAll('#empty-msg').forEach(msg => msg.remove());
            
            let cleanHTML = '';
            cloneCanvas.querySelectorAll('.canvas-item').forEach(item => {
                cleanHTML += item.firstElementChild.outerHTML + '\n';
            });

            codeEditor.value = cleanHTML.trim();
        }

        function applyCodeChanges() {
            const newHTML = codeEditor.value;
            canvas.innerHTML = '';
            
            const tempDiv = document.createElement('div');
            tempDiv.innerHTML = newHTML;

            if (tempDiv.children.length === 0) {
                if (emptyMsg) {
                    emptyMsg.style.display = 'block';
                    canvas.appendChild(emptyMsg);
                }
                return;
            }

            Array.from(tempDiv.children).forEach(child => {
                elementCount++;
                const wrapper = document.createElement('div');
                wrapper.className = 'canvas-item';
                wrapper.id = 'item-' + elementCount;
                wrapper.appendChild(child.cloneNode(true));

                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'delete-btn';
                deleteBtn.innerText = '✕';
                deleteBtn.onclick = (e) => {
                    e.stopPropagation();
                    wrapper.remove();
                };
                wrapper.appendChild(deleteBtn);

                wrapper.onclick = (e) => {
                    e.stopPropagation();
                    selectElement(wrapper, wrapper.firstElementChild, child.tagName.toLowerCase());
                };

                canvas.appendChild(wrapper);
            });
        }

        function rgbToHex(rgb) {
            if (!rgb) return '#ffffff';
            const res = rgb.match(/\d+/g);
            if (!res) return '#ffffff';
            return "#" + ((1 << 24) + (parseInt(res[0]) << 16) + (parseInt(res[1]) << 8) + parseInt(res[2])).toString(16).slice(1);
        }

        // ЭКСПОРТ (ИСПРАВЛЕН СКРОЛЛ ДЛЯ ИТОГОВОЙ СТРАНИЦЫ)
        function exportHTML() {
            if (currentMode === 'code') {
                applyCodeChanges();
            }

            const cloneCanvas = canvas.cloneNode(true);
            cloneCanvas.querySelectorAll('.delete-btn').forEach(btn => btn.remove());
            cloneCanvas.querySelectorAll('#empty-msg').forEach(msg => msg.remove());

            let cleanContent = '';
            cloneCanvas.querySelectorAll('.canvas-item').forEach(item => {
                cleanContent += `  <div style="margin-bottom: 15px;">\n    ${item.firstElementChild.outerHTML}\n  </div>\n`;
            });

            const bgColor = canvas.style.backgroundColor || '#ffffff';
            const padding = canvas.style.padding || '25px';
            const fontFamily = canvas.style.fontFamily || "'Segoe UI', sans-serif";

            const fullPageCode = `<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Сайт созданный в Programmiist Studio</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { 
            font-family: ${fontFamily}; 
            padding: ${padding}; 
            max-width: 850px; 
            margin: 0 auto; 
            background-color: ${bgColor};
            min-height: 100vh;
            overflow-y: auto;
        }
    </style>
</head>
<body>
${cleanContent}
</body>
</html>`;

            const blob = new Blob([fullPageCode], { type: 'text/html' });
            const a = document.createElement('a');
            a.href = URL.createObjectURL(blob);
            a.download = 'index.html';
            a.click();
        }
    </script>
</body>
</html>
