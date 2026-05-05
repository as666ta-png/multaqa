<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>🌳 الملتقى v3.3</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        :root { --amber: #f59e0b; --cyan: #06b6d4; --bg: #0a1628; --card: rgba(15, 30, 60, 0.85); --text: #e2e8f0; }
        body { font-family: sans-serif; background: linear-gradient(160deg, #0a1628, #0f2a45); color: var(--text); min-height: 100vh; direction: rtl; }
      .screen { display: none; min-height: 100vh; }
      .screen.active { display: block; }
      .header { display: flex; align-items: center; padding: 12px 15px; background: rgba(10, 22, 40, 0.9); border-bottom: 1px solid rgba(255,255,0.08); gap: 10px; }
      .header h2 { flex: 1; text-align: center; font-size: 17px; }
      .header-btn { width: 36px; height: 36px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.15); background: rgba(255,255,255,0.05); color: white; font-size: 18px; cursor: pointer; }
      .main-container { padding: 30px 20px; text-align: center; }
      .tree-logo { font-size: 70px; margin-bottom: 10px; }
      .app-name { font-size: 38px; font-weight: 900; background: linear-gradient(135deg, #06b6d4, #3b82f6, #f59e0b); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 5px; }
      .app-tagline { font-size: 14px; color: #94a3b8; margin-bottom: 40px; }
      .menu-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; max-width: 400px; margin: 0 auto; }
      .menu-btn { background: var(--card); border: 1px solid rgba(255,255,255,0.08); border-radius: 18px; padding: 22px 15px; cursor: pointer; }
      .menu-btn.icon { font-size: 36px; display: block; margin-bottom: 8px; }
      .menu-btn.label { font-size: 14px; font-weight: 700; color: var(--amber); display: block; margin-bottom: 3px; }
      .menu-btn.desc { font-size: 10px; color: #94a3b8; }
      .chat-area { height: calc(100vh - 140px); overflow-y: auto; padding: 15px; }
      .msg { margin-bottom: 14px; }
      .msg.user { text-align: left; }
      .msg.bubble { display: inline-block; max-width: 85%; padding: 12px 16px; border-radius: 18px; font-size: 14px; }
      .msg.user.bubble { background: linear-gradient(135deg, #f59e0b, #eab308); color: #0a1628; }
      .msg.assistant.bubble { background: var(--card); border: 1px solid rgba(255,255,255,0.08); text-align: right; }
      .chat-bar { display: flex; gap: 8px; padding: 10px 15px; background: rgba(10, 22, 40, 0.95); border-top: 1px solid rgba(255,255,255,0.08); position: fixed; bottom: 0; width: 100%; }
      .chat-bar input { flex: 1; padding: 12px 16px; border-radius: 25px; border: 1px solid rgba(255,255,255,0.12); background: rgba(255,255,255,0.06); color: white; font-size: 16px; }
      .chat-bar.send { width: 44px; height: 44px; border-radius: 50%; border: none; background: linear-gradient(135deg, #f59e0b, #eab308); color: #0a1628; font-size: 18px; }
      .content-area { padding: 20px 15px; }
      .setting-row { background: var(--card); border: 1px solid rgba(255,255,255,0.08); border-radius: 14px; padding: 16px; margin-bottom: 12px; }
      .setting-row label { display: block; font-weight: 700; color: var(--amber); margin-bottom: 8px; font-size: 14px; }
      .big-input { width: 100%; padding: 14px 18px; border-radius: 14px; border: 1px solid rgba(255,255,255,0.12); background: rgba(255,255,255,0.06); color: white; font-size: 16px; margin-bottom: 12px; -webkit-user-select: text; user-select: text; }
      .action-btn { width: 100%; padding: 14px; border-radius: 14px; border: none; background: linear-gradient(135deg, #06b6d4, #0ea5e9); color: white; font-size: 15px; font-weight: 700; }
      .error-msg { background: rgba(239, 68, 0.15); border: 1px solid rgba(239, 68, 68, 0.4); color: #fca5a5; padding: 12px; border-radius: 12px; margin: 10px 15px; text-align: center; }
    </style>
</head>
<body>
    <div id="home" class="screen active">
        <div class="main-container">
            <div class="tree-logo">🌳</div>
            <div class="app-name">الملتقى</div>
            <div class="app-tagline">ملتقى العقول الذكية</div>
            <div class="menu-grid">
                <div class="menu-btn" onclick="openScreen('chat')"><span class="icon">💬</span><span class="label">محادثة</span><span class="desc">تحدث مع مساعدك</span></div>
                <div class="menu-btn" onclick="openScreen('settings')"><span class="icon">⚙️</span><span class="label">الإعدادات</span><span class="desc">أضف المفتاح هنا</span></div>
            </div>
        </div>
    </div>

    <div id="chat" class="screen">
        <div class="header"><button class="header-btn" onclick="openScreen('home')">←</button><h2>💬 المحادثة</h2><span style="width:36px;"></span></div>
        <div id="errorBox"></div>
        <div class="chat-area" id="chatMessages">
            <div style="text-align:center;padding:50px 20px;color:#94a3b8">
                <div style="font-size:55px;margin-bottom:15px">🌳</div>
                <h3>أهلاً بك في الملتقى</h3>
                <p>فعّل المفتاح من الإعدادات أولاً</p>
            </div>
        </div>
        <div class="chat-bar">
            <input type="text" id="chatInput" placeholder="اكتب رسالتك..." onkeypress="if(event.key==='Enter')sendMsg()">
            <button class="send" onclick="sendMsg()">🚀</button>
        </div>
    </div>

    <div id="settings" class="screen">
        <div class="header"><button class="header-btn" onclick="openScreen('home')">←</button><h2>⚙️ الإعدادات</h2><span style="width:36px;"></span></div>
        <div class="content-area">
            <div class="setting-row">
                <label>مفتاح Gemini API</label>
                <input type="text" id="apiKeyInput" class="big-input" placeholder="اضغط هنا والصق المفتاح AIza..." autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false">
                <button class="action-btn" onclick="saveKey()">حفظ وتفعيل المفتاح</button>
                <p id="keyStatus" style="text-align:center;margin-top:10px;color:#94a3b8;font-size:13px">الحالة: غير مُفعّل ❌</p>
            </div>
        </div>
    </div>

    <script>
        let GEMINI_API_KEY = '';
        const GEMINI_URL = 'https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent';

        function openScreen(name) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(name).classList.add('active');
            if(name === 'settings') {
                setTimeout(() => document.getElementById('apiKeyInput').focus(), 100);
            }
        }

        function saveKey() {
            const key = document.getElementById('apiKeyInput').value.trim();
            if (!key) {
                alert('اكتب المفتاح أول');
                return;
            }
            GEMINI_API_KEY = key;
            document.getElementById('keyStatus').innerHTML = 'الحالة: مُفعّل ✅';
            document.getElementById('keyStatus').style.color = '#4ade80';
            document.getElementById('errorBox').innerHTML = '';
            alert('تم حفظ المفتاح! تقدر تستخدم المحادثة الحين');
        }

        async function sendMsg() {
            if (!GEMINI_API_KEY) {
                document.getElementById('errorBox').innerHTML = '<div class="error-msg">⚠️ لازم تفعّل المفتاح من الإعدادات أول</div>';
                openScreen('settings');
                return;
            }

            const input = document.getElementById('chatInput');
            const msg = input.value.trim();
            if (!msg) return;

            addBubble('user', msg);
            input.value = '';

            const loadingId = addBubble('assistant', 'جاري التفكير... ⏳');

            try {
                const response = await fetch(GEMINI_URL + '?key=' + GEMINI_API_KEY, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: msg }] }]
                    })
                });

                document.getElementById(loadingId).remove();

                if (!response.ok) {
                    const err = await response.json();
                    throw new Error(err.error?.message || 'خطأ من السيرفر');
                }

                const data = await response.json();
                const reply = data.candidates[0].content.parts[0].text;
                addBubble('assistant', reply);
            } catch (error) {
                document.getElementById(loadingId).remove();
                addBubble('assistant', '⚠️ خطأ: ' + error.message + '<br><br>تأكد من المفتاح والإنترنت');
            }
        }

        function addBubble(role, text) {
            const area = document.getElementById('chatMessages');
            const id = 'msg_' + Date.now();
            const div = document.createElement('div');
            div.className = 'msg ' + role;
            div.id = id;
            div.innerHTML = '<div class="bubble">' + text.replace(/\n/g, '<br>') + '</div>';
            area.appendChild(div);
            area.scrollTop = area.scrollHeight;
            return id;
        }
    </script>
</body>
</html>
