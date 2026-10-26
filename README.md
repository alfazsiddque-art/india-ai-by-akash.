# india-ai-by-akash.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#081528">
<title>INDIA AI — by Akash</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#081528;color:#fff;font-family:Arial,sans-serif}
header{padding:20px;background:#101f35;border-bottom:3px solid #138808}
h1{margin:0;font-size:24px}
header p{color:#cbd5e1}
main{padding:18px;max-width:700px;margin:auto}
.hero,.panel,.tile{background:#101f35;border:1px solid #30415b;border-radius:16px;padding:18px;margin-bottom:14px}
.hero h2{font-size:28px}
.orange{color:#ff9933}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
button{cursor:pointer;border:1px solid #30415b;border-radius:12px;padding:14px;background:#172b45;color:#fff;font-size:16px}
.tile{text-align:left;min-height:90px}
.tile b{display:block;margin-top:8px}
textarea{width:100%;min-height:100px;background:#071222;color:#fff;border:1px solid #40516a;border-radius:12px;padding:12px;font-size:16px}
.primary{background:#ff9933;color:#111827;font-weight:bold;border:0;margin-top:10px}
#answer{white-space:pre-wrap;line-height:1.5}
small{color:#bdc9da}
</style>
</head>
<body>
<header>
<h1>🇮🇳 INDIA AI <span class="orange">— by Akash</span></h1>
<p>Your ideas. Your language. Your future.</p>
</header>
<main>
<section class="hero">
<p class="orange">WELCOME TO YOUR AI WORKSPACE</p>
<h2>What will you create today?</h2>
<p>Explore chat, translation, image ideas, video ideas and voice tools.</p>
</section>
<div class="grid">
<button class="tile" onclick="show('chat')">💬<b>AI Chat</b><small>Ask questions</small></button>
<button class="tile" onclick="show('translate')">🌐<b>Translation</b><small>Language tools</small></button>
<button class="tile" onclick="show('images')">🎨<b>Image ideas</b><small>Build image prompts</small></button>
<button class="tile" onclick="show('video')">🎬<b>Video ideas</b><small>Build video prompts</small></button>
<button class="tile" onclick="show('voice')">🎙️<b>Voice</b><small>Read text aloud</small></button>
<button class="tile" onclick="show('history')">🗂️<b>History</b><small>Saved on this device</small></button>
</div>
<p><small>Starter version: real AI chat, translation and image/video generation are not connected yet.</small></p>
<section id="chat" class="panel">
<h2>💬 AI Chat</h2>
<textarea id="message" placeholder="Type your message..."></textarea>
<button class="primary" onclick="send()">Send message</button>
<button onclick="clearChat()">Clear chat</button>
<div id="answer"></div>
</section>
<section id="translate" class="panel" hidden>
<h2>🌐 Translation</h2>
<textarea placeholder="Paste the text you want to translate..."></textarea>
<p><small>Connect a translation service to enable real translations.</small></p>
</section>
<section id="images" class="panel" hidden>
<h2>🎨 Image prompt</h2>
<textarea id="imageText" placeholder="Describe the picture you want..."></textarea>
<button class="primary" onclick="savePrompt('Image', 'imageText')">Save image prompt</button>
</section>
<section id="video" class="panel" hidden>
<h2>🎬 Video prompt</h2>
<textarea id="videoText" placeholder="Describe your video, scenes and sound..."></textarea>
<button class="primary" onclick="savePrompt('Video', 'videoText')">Save video prompt</button>
</section>
<section id="voice" class="panel" hidden>
<h2>🎙️ Voice</h2>
<textarea id="voiceText" placeholder="Enter text to read aloud..."></textarea>
<button class="primary" onclick="speak()">Read aloud</button>
</section>
<section id="history" class="panel" hidden>
<h2>🗂️ Saved prompts</h2><div id="saved"></div>
</section>
</main>
<script>
const sections=['chat','translate','images','video','voice','history'];
function show(id){sections.forEach(s=>document.getElementById(s).hidden=s!==id)}
function send(){
const m=document.getElementById('message').value.trim();if(!m)return;
let h=JSON.parse(localStorage.getItem('indiaChat')||'[]');
h.push('You: '+m,'INDIA AI: This prototype is not connected to a real AI model yet.');
localStorage.setItem('indiaChat',JSON.stringify(h));document.getElementById('message').value='';drawChat();
}
function drawChat(){let h=JSON.parse(localStorage.getItem('indiaChat')||'[]');document.getElementById('answer').textContent=h.join('\n\n')}
function clearChat(){localStorage.removeItem('indiaChat');drawChat()}
function savePrompt(type,id){let v=document.getElementById(id).value.trim();if(!v)return;let a=JSON.parse(localStorage.getItem('indiaPrompts')||'[]');a.unshift(type+': '+v);localStorage.setItem('indiaPrompts',JSON.stringify(a));alert('Saved on this device')}
function speak(){let v=document.getElementById('voiceText').value;if(v&&'speechSynthesis'in window)speechSynthesis.speak(new SpeechSynthesisUtterance(v));else alert('Voice playback is not supported in this browser')}
document.getElementById('saved').textContent=JSON.parse(localStorage.getItem('indiaPrompts')||'[]').join('\n\n')||'No saved prompts yet.';
drawChat();
</script>
</body>
</html>
