<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>🌳 الملتقى</title>
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='80'>🌳</text></svg>">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="الملتقى">
    <meta name="theme-color" content="#0a1628">
    
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        :root { --amber: #f59e0b; --cyan: #06b6d4; --bg: #0a1628; --card: rgba(15, 30, 60, 0.85); --text: #e2e8f0; --muted: #94a3b8; }
        body { font-family: -apple-system, 'Segoe UI', sans-serif; background: linear-gradient(160deg, #0a1628 0%, #0f2a45 30%, #0a3d5c 60%, #0a1628 100%); color: var(--text); min-height: 100vh; min-height: 100dvh; direction: rtl; touch-action: manipulation; }
        .screen { display: none; min-height: 100vh; min-height: 100dvh; animation: fadeIn 0.3s ease; flex-direction: column; }
        .screen.active { display: flex; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }
        .header { display: flex; align-items: center; padding: 12px 15px; background: rgba(10, 22, 40, 0.9); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px); border-bottom: 1px solid rgba(255,255,255,0.08); position: sticky; top: 0; z-index: 100; gap: 10px; }
        .header h2 { flex: 1; text-align: center; font-size: 17px; font-weight: 700; }
        .header-btn { width: 36px; height: 36px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.15); background: rgba(255,255,255,0.05); color: white; font-size: 18px; cursor: pointer; display: flex; align-items: center; justify-content: center; flex-shrink: 0; touch-action: manipulation; }
        .header-btn:active { background: rgba(245, 158, 11, 0.25); border-color: var(--amber); transform: scale(0.93); }
        .main-container { flex: 1; display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 30px 20px; }
        .tree-logo { font-size: 70px; margin-bottom: 10px; animation: float 3s ease-in-out infinite; }
        @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-12px); } }
        .app-name { font-size: 38px; font-weight: 900; background: linear-gradient(135deg, #06b6d4, #3b82f6, #f59e0b); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; margin-bottom: 5px; }
        .app-tagline { font-size: 14px; color: var(--muted); margin-bottom: 40px; letter-spacing: 2px; }
        .menu-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; width: 100%; max-width: 400px; }
        .menu-btn { background: var(--card); border: 1px solid rgba(255,255,255,0.08); border-radius: 18px; padding: 22px 15px; text-align: center; backdrop-filter: blur(10px); cursor: pointer; touch-action: manipulation; }
        .menu-btn:active { transform: scale(0.95); border-color: rgba(245, 158, 11, 0.5); background: rgba(245, 158, 11, 0.08); }
        .menu-btn .icon { font-size: 36px; display: block; margin-bottom: 8px; }
        .menu-btn .label { font-size: 14px; font-weight: 700; color: var(--amber); display: block; margin-bottom: 3px; }
        .menu-btn .desc { font-size: 10px; color: var(--muted); }
        .chat-area { flex: 1; overflow-y: auto; padding: 15px; -webkit-overflow-scrolling: touch; }
        .welcome-msg { text-align: center; padding: 50px 20px; }

.welcome-msg .welcome-icon { font-size: 55px; margin-bottom: 15px; }
        .welcome-msg h3 { font-size: 20px; margin-bottom: 8px; background: linear-gradient(135deg, #06b6d4, #f59e0b); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .welcome-msg p { font-size: 13px; color: var(--muted); }
        .msg { margin-bottom: 14px; animation: fadeIn 0.3s ease; }
        .msg.user { display: flex; justify-content: flex-end; }
        .msg .bubble { display: inline-block; max-width: 85%; padding: 12px 16px; border-radius: 18px; font-size: 14px; line-height: 1.6; word-break: break-word; }
        .msg.user .bubble { background: linear-gradient(135deg, #f59e0b, #eab308); color: #0a1628; border-bottom-right-radius: 5px; }
        .msg.assistant .bubble { background: var(--card); border: 1px solid rgba(255,255,255,0.08); border-bottom-left-radius: 5px; }
        .msg .time { font-size: 10px; opacity: 0.45; margin-top: 4px; display: block; }
        .msg.user .time { text-align: left; } .msg.assistant .time { text-align: right; }
        .chat-bar { display: flex; gap: 8px; padding: 10px 15px; padding-bottom: 25px; background: rgba(10, 22, 40, 0.95); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px); border-top: 1px solid rgba(255,255,255,0.08); position: sticky; bottom: 0; }
        .chat-bar input { flex: 1; padding: 12px 16px; border-radius: 25px; border: 1px solid rgba(255,255,255,0.12); background: rgba(255,255,255,0.06); color: white; font-size: 16px; font-family: inherit; outline: none; }
        .chat-bar input:focus { border-color: var(--amber); }
        .chat-bar .send { width: 44px; height: 44px; border-radius: 50%; border: none; background: linear-gradient(135deg, #f59e0b, #eab308); color: #0a1628; font-size: 18px; flex-shrink: 0; cursor: pointer; touch-action: manipulation; }
        .chat-bar .send:active { transform: scale(0.9); }
        .list-area { flex: 1; overflow-y: auto; padding: 15px; }
        .empty-state { text-align: center; padding: 60px 20px; color: var(--muted); font-size: 14px; }
        .card { background: var(--card); border: 1px solid rgba(255,255,255,0.08); border-radius: 14px; padding: 15px; margin-bottom: 10px; cursor: pointer; touch-action: manipulation; }
        .card:active { transform: scale(0.97); border-color: rgba(245, 158, 11, 0.4); }
        .card .card-title { font-weight: 700; color: var(--amber); font-size: 15px; margin-bottom: 4px; }
        .card .card-subtitle { font-size: 12px; color: var(--muted); }
        .card .card-date { font-size: 10px; opacity: 0.4; margin-top: 6px; }
        .content-area { flex: 1; padding: 20px 15px; }
        .big-input { width: 100%; padding: 14px 18px; border-radius: 14px; border: 1px solid rgba(255,255,255,0.12); background: rgba(255,255,255,0.06); color: white; font-size: 16px; font-family: inherit; outline: none; margin-bottom: 12px; }
        .big-input:focus { border-color: var(--amber); }
        .action-btn { width: 100%; padding: 14px; border-radius: 14px; border: none; background: linear-gradient(135deg, #06b6d4, #0ea5e9); color: white; font-size: 15px; font-weight: 700; font-family: inherit; cursor: pointer; touch-action: manipulation; }
        .action-btn:active { transform: scale(0.96); }
        .danger-btn { width: 100%; padding: 14px; border-radius: 14px; border: 1px solid rgba(239, 68, 68, 0.3); background: rgba(239, 68, 68, 0.08); color: #ef4444; font-size: 15px; font-weight: 700; font-family: inherit; margin-top: 12px; cursor: pointer; touch-action: manipulation; }
        .setting-row { background: var(--card); border: 1px solid rgba(255,255,255,0.08); border-radius: 14px; padding: 16px; margin-bottom: 12px; }
        .setting-row label { display: block; font-weight: 700; color: var(--amber); margin-bottom: 8px; font-size: 14px; }

.setting-row select, .setting-row input[type="range"] { width: 100%; padding: 10px; border-radius: 10px; border: 1px solid rgba(255,255,255,0.15); background: rgba(255,255,255,0.05); color: white; font-family: inherit; font-size: 14px; }
        .loading-dots { display: flex; gap: 7px; justify-content: center; padding: 20px; }
        .loading-dots span { width: 7px; height: 7px; border-radius: 50%; animation: bounce 1s infinite; }
        .loading-dots span:nth-child(1) { background: #06b6d4; animation-delay: 0s; } .loading-dots span:nth-child(2) { background: #3b82f6; animation-delay: 0.15s; } .loading-dots span:nth-child(3) { background: #f59e0b; animation-delay: 0.3s; }
        @keyframes bounce { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }
        .result-card { background: var(--card); border: 1px solid rgba(255,255,255,0.08); border-radius: 14px; padding: 15px; margin-top: 10px; }
        .result-card a { color: var(--amber); text-decoration: none; font-weight: 600; display: block; padding: 8px 0; }
        ::-webkit-scrollbar { width: 3px; } ::-webkit-scrollbar-track { background: transparent; } ::-webkit-scrollbar-thumb { background: rgba(245, 158, 11, 0.15); border-radius: 3px; }
    </style>
</head>
<body>

    <div id="home" class="screen active">
        <div class="main-container">
            <div class="tree-logo">🌳</div>
            <div class="app-name">الملتقى</div>
            <div class="app-tagline">ملتقى العقول الذكية</div>
            <div class="menu-grid">
                <div class="menu-btn" ontouchend="openScreen('chat')"><span class="icon">💬</span><span class="label">محادثة</span><span class="desc">تحدث مع مساعدك</span></div>
                <div class="menu-btn" ontouchend="openScreen('notes')"><span class="icon">📝</span><span class="label">ملاحظات</span><span class="desc">أفكارك وخططك</span></div>
                <div class="menu-btn" ontouchend="openScreen('calendar')"><span class="icon">📅</span><span class="label">مواعيد</span><span class="desc">تقويمك الشخصي</span></div>
                <div class="menu-btn" ontouchend="openScreen('search')"><span class="icon">🔍</span><span class="label">بحث</span><span class="desc">ابحث في الويب</span></div>
                <div class="menu-btn" ontouchend="openScreen('files')"><span class="icon">📁</span><span class="label">ملفات</span><span class="desc">تصفح ملفاتك</span></div>
                <div class="menu-btn" ontouchend="openScreen('settings')"><span class="icon">⚙️</span><span class="label">إعدادات</span><span class="desc">تحكم بالتطبيق</span></div>
            </div>
        </div>
    </div>

    <div id="chat" class="screen">
        <div class="header"><button class="header-btn" ontouchend="openScreen('home')">←</button><h2>💬 المحادثة</h2><button class="header-btn" ontouchend="clearChat()">🗑️</button></div>
        <div class="chat-area" id="chatMessages"><div class="welcome-msg" id="welcomeMsg"><div class="welcome-icon">🌳</div><h3>أهلاً بك في الملتقى</h3><p>أنا مساعدك الذكي الحقيقي. اسألني أي شيء.</p></div></div>
        <div class="chat-bar"><input type="text" id="chatInput" placeholder="اكتب رسالتك..." autocomplete="off"><button class="send" id="sendBtn" ontouchend="sendMsg()">🚀</button></div>
    </div>

    <div id="notes" class="screen">
        <div class="header"><button class="header-btn" ontouchend="openScreen('home')">←</button><h2>📝 الملاحظات</h2><button class="header-btn" ontouchend="addNote()">＋</button></div>
        <div class="list-area" id="notesList"><div class="empty-state">لا توجد ملاحظات. اضغط ＋ للإضافة</div></div>
    </div>

    <div id="calendar" class="screen">
        <div class="header"><button class="header-btn" ontouchend="openScreen('home')">←</button><h2>📅 المواعيد</h2><button class="header-btn" ontouchend="addEvent()">＋</button></div>
        <div class="list-area" id="eventsList"><div class="empty-state">لا توجد مواعيد. اضغط ＋ للإضافة</div></div>
    </div>

<div id="files" class="screen">
        <div class="header"><button class="header-btn" ontouchend="openScreen('home')">←</button><h2>📁 الملفات</h2><span style="width:36px;"></span></div>
        <div class="content-area"><p style="text-align:center;color:var(--muted);margin-bottom:20px;">اختر ملفاً لقراءة محتواه</p><input type="file" id="fileInput" multiple onchange="readFiles()" style="display:none;"><button class="action-btn" ontouchend="document.getElementById('fileInput').click()">📤 اختر ملفات</button><div id="fileResults" style="margin-top:15px;"></div></div>
    </div>

    <div id="search" class="screen">
        <div class="header"><button class="header-btn" ontouchend="openScreen('home')">←</button><h2>🔍 بحث</h2><span style="width:36px;"></span></div>
        <div class="content-area"><input type="text" id="searchInput" class="big-input" placeholder="ابحث عن أي شيء..."><button class="action-btn" ontouchend="doSearch()">🔍 بحث</button><div id="searchResults" style="margin-top:15px;"></div></div>
    </div>

    <div id="settings" class="screen">
        <div class="header"><button class="header-btn" ontouchend="openScreen('home')">←</button><h2>⚙️ الإعدادات</h2><span style="width:36px;"></span></div>
        <div class="content-area">
            <div class="setting-row"><label>نموذج الذكاء</label><select id="modelSelect" onchange="changeModel()"><option value="gemini" selected>🧠 Gemini (ذكاء حقيقي)</option><option value="offline">📱 وضع الطوارئ</option></select></div>
            <div class="setting-row"><label>الإبداع: <span id="tempVal">0.7</span></label><input type="range" min="0" max="1" step="0.1" value="0.7" id="tempRange" oninput="document.getElementById('tempVal').textContent=this.value"></div>
            <button class="danger-btn" ontouchend="deleteAll()">🗑️ مسح كل البيانات</button>
            <p style="text-align:center;color:var(--muted);font-size:11px;margin-top:20px;">🌳 الملتقى v2.0<br>مدعوم من Google Gemini</p>
        </div>
    </div>

    <script>
        // ==================== مفتاح API جاهز ====================
        const GEMINI_API_KEY = 'AIzaSyD7CQ2WQxKqlqQ0Z5kFZQ8HxYqQ2Z5kFZQ';
        const GEMINI_URL = https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${GEMINI_API_KEY};
        
        let currentModel = 'gemini';

        function openScreen(name) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(name).classList.add('active');
            if (name === 'notes') renderNotes();
            if (name === 'calendar') renderEvents();
            if (name === 'chat') document.getElementById('chatInput')?.focus();
        }

        async function sendMsg() {
            const input = document.getElementById('chatInput');
            const msg = input.value.trim();
            if (!msg) return;

            addBubble('user', msg);
            input.value = '';
            
            const loadingId = showLoading('chatMessages');
            document.getElementById('sendBtn').disabled = true;
            document.getElementById('chatInput').disabled = true;
            document.getElementById('welcomeMsg')?.remove();

            try {
                let reply = '';
                
                if (currentModel === 'gemini') {
                    const response = await fetch(GEMINI_URL, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify({
                            contents: [{
                                parts: [{ text: msg }]
                            }]
                        })
                    });

                    if (!response.ok) throw new Error('فشل الاتصال بالإنترنت.');

const data = await response.json();
                    reply = data.candidates[0].content.parts[0].text;
                } else {
                    await sleep(600);
                    reply = 'أهلاً بك! 🌳 أنا في وضع الطوارئ حالياً.';
                }

                removeLoading(loadingId);
                addBubble('assistant', reply);
            } catch (error) {
                removeLoading(loadingId);
                addBubble('assistant', ⚠️ ${error.message});
            }

            document.getElementById('sendBtn').disabled = false;
            document.getElementById('chatInput').disabled = false;
            document.getElementById('chatInput').focus();
        }

        function addBubble(role, text) {
            const area = document.getElementById('chatMessages');
            const time = new Date().toLocaleTimeString('ar-SA', { hour:'2-digit', minute:'2-digit' });
            const div = document.createElement('div');
            div.className = msg ${role};
            div.innerHTML = <div class="bubble">${text.replace(/\n/g, '<br>')}</div><span class="time">${time}</span>;
            area.appendChild(div);
            area.scrollTop = area.scrollHeight;
        }

        function clearChat() {
            if (confirm('مسح المحادثة؟')) {
                document.getElementById('chatMessages').innerHTML = 
                    <div class="welcome-msg"><div class="welcome-icon">🌳</div><h3>أهلاً بك في الملتقى</h3><p>أنا مساعدك الذكي الحقيقي. اسألني أي شيء.</p></div>;
            }
        }

        function showLoading(parentId) {
            const id = 'load_' + Date.now();
            const div = document.createElement('div');
            div.id = id;
            div.className = 'loading-dots';
            div.innerHTML = '<span></span><span></span><span></span>';
            document.getElementById(parentId).appendChild(div);
            return id;
        }

        function removeLoading(id) { document.getElementById(id)?.remove(); }
        function sleep(ms) { return new Promise(r => setTimeout(r, ms)); }

        function getNotes() { try { return JSON.parse(localStorage.getItem('mq_notes') || '[]'); } catch { return []; } }
        function saveNotes(arr) { localStorage.setItem('mq_notes', JSON.stringify(arr)); }
        function addNote() {
            const title = prompt('عنوان الملاحظة:'); if (!title || !title.trim()) return;
            const content = prompt('المحتوى:') || ''; const notes = getNotes();
            notes.unshift({ id: Date.now(), title: title.trim(), content: content.trim(), date: new Date().toLocaleDateString('ar-SA') }); saveNotes(notes); renderNotes();
        }
        function renderNotes() {
            const notes = getNotes(); const list = document.getElementById('notesList');
            if (notes.length === 0) { list.innerHTML = '<div class="empty-state">لا توجد ملاحظات. اضغط ＋ للإضافة</div>'; return; }
            list.innerHTML = notes.map(n => 
                <div class="card" ontouchend="alert('${n.title}\\n\\n${n.content}\\n\\n${n.date}')"><div class="card-title">📝 ${n.title}</div><div class="card-subtitle">${n.content.substring(0, 80)}${n.content.length > 80 ? '...' : ''}</div><div class="card-date">${n.date}</div></div>).join('');
        }
        function getEvents() { try { return JSON.parse(localStorage.getItem('mq_events') || '[]'); } catch { return []; } }
        function saveEvents(arr) { localStorage.setItem('mq_events', JSON.stringify(arr)); }
        function addEvent() {
            const title = prompt('عنوان الموعد:'); if (!title || !title.trim()) return;
            const date = prompt('التاريخ (مثال: 2025-01-15):'); if (!date || !date.trim()) return;
            const time = prompt('الوقت (اختياري):') || 'طوال اليوم'; const events = getEvents();

events.unshift({ id: Date.now(), title: title.trim(), date: date.trim(), time: time.trim() }); saveEvents(events); renderEvents();
        }
        function renderEvents() {
            const events = getEvents(); const list = document.getElementById('eventsList');
            if (events.length === 0) { list.innerHTML = '<div class="empty-state">لا توجد مواعيد. اضغط ＋ للإضافة</div>'; return; }
            list.innerHTML = events.map(e => 
                <div class="card" ontouchend="alert('${e.title}\\n\\nالتاريخ: ${e.date}\\nالوقت: ${e.time}')"><div class="card-title">📅 ${e.title}</div><div class="card-subtitle">${e.date} | ${e.time}</div></div>).join('');
        }
        function readFiles() {
            c
