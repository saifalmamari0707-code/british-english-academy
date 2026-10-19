# british-english-academy

<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#58cc02">
<title>British English Academy</title>
<style>
:root{--green:#58cc02;--dark:#168000;--ink:#263238;--muted:#64748b;--bg:#f5fff0;--card:#fff}
*{box-sizing:border-box}
body{margin:0;font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Arial,sans-serif;background:var(--bg);color:var(--ink)}
header{background:#fff;padding:16px;border-bottom:2px solid #e3efdc;position:sticky;top:0;z-index:5}
.top{max-width:850px;margin:auto;display:flex;justify-content:space-between;align-items:center;gap:10px}
.logo{font-weight:900;color:var(--dark);font-size:18px}
.points{background:#fff5d7;border-radius:20px;padding:9px 12px;font-weight:bold}
main{max-width:850px;margin:auto;padding:18px}
.hero{background:linear-gradient(135deg,#58cc02,#b7ef75);padding:24px;border-radius:24px;color:#163b08}
.hero h1{margin-top:0;font-size:27px}
.hero p{line-height:1.8}
.card{background:var(--card);border:2px solid #e4eddf;border-radius:20px;padding:18px;margin:16px 0;box-shadow:0 3px 0 #e4eddf}
h2{font-size:21px}
.small{color:var(--muted);line-height:1.8}
button,select,input{font:inherit}
button{border:0;border-radius:14px;padding:12px 16px;background:var(--green);color:#163b08;font-weight:800;cursor:pointer;margin:4px 0}
button:active{transform:translateY(1px)}
.secondary{background:#eaf7e2}
.nav{display:grid;grid-template-columns:repeat(4,1fr);gap:6px;margin:16px 0}
.nav button{font-size:13px;padding:12px 4px;background:#fff;border:2px solid #e3efdc;color:var(--ink)}
.nav button.active{background:#e4ffd5;border-color:var(--green)}
.word{font-size:32px;font-weight:900;text-align:center;margin:15px}
.translation{text-align:center;font-size:21px;color:var(--dark)}
.example{background:#f3f9ee;padding:13px;border-radius:12px;line-height:1.8}
.progress{height:12px;background:#e4eddf;border-radius:20px;overflow:hidden}
.progress div{height:100%;background:var(--green);width:0;transition:.3s}
.option{display:block;width:100%;text-align:right;background:#fff;border:2px solid #e1e9dc;color:var(--ink)}
.option:focus,.option:hover{border-color:var(--green)}
#feedback{font-weight:bold;min-height:26px}
.chatlog{height:180px;overflow:auto;background:#f7faf5;border-radius:12px;padding:10px;line-height:1.7}
.msg{padding:9px 12px;border-radius:12px;margin:7px 0;background:#e5f6d9}
.me{background:#e4efff}
input,select{width:100%;padding:12px;border:2px solid #dce8d5;border-radius:12px;background:white;margin:7px 0}
footer{text-align:center;padding:25px;color:var(--muted);font-size:13px}
.hidden{display:none}
@media(min-width:600px){.hero h1{font-size:34px}.nav button{font-size:15px}}
</style>
</head>
<body>
<header>
 <div class="top">
  <div class="logo">🇬🇧 British English Academy</div>
  <div class="points">⭐ <span id="points">0</span> نقطة</div>
 </div>
</header>

<main>
 <section class="hero">
  <h1>تعلّم الإنجليزية البريطانية 🇬🇧</h1>
  <p>ابدأ من الصفر، تعلّم الكلمات، استمع إلى النطق، واختبر مستواك خطوة بخطوة.</p>
  <button onclick="showTab('lesson')">ابدأ التعلّم ←</button>
 </section>

 <div class="nav">
  <button class="active" id="nav-lesson" onclick="showTab('lesson')">📚 الدروس</button>
  <button id="nav-quiz" onclick="showTab('quiz')">🧠 الاختبار</button>
  <button id="nav-chat" onclick="showTab('chat')">💬 المحادثة</button>
  <button id="nav-progress" onclick="showTab('progress')">🏆 تقدّمي</button>
 </div>

 <section id="lesson" class="tab">
  <div class="card">
   <h2>📘 الدرس الأول: التحيات</h2>
   <p class="small">المستوى: مبتدئ A1 — استمع إلى الكلمة ثم كرّر نطقها.</p>
   <div class="word" id="word">Hello</div>
   <div class="translation" id="translation">مرحباً</div>
   <p class="example" id="example">Hello, how are you?<br>مرحباً، كيف حالك؟</p>
   <button onclick="speak()">🔊 استمع للنطق البريطاني</button>
   <button class="secondary" onclick="nextWord()">الكلمة التالية ←</button>
   <p class="small" id="wordCount">الكلمة 1 من 5</p>
  </div>
  <div class="card">
   <h2>🗺️ مسار التعلّم</h2>
   <p>🟢 المستوى 1: الكلمات الأساسية</p>
   <p>🔒 المستوى 2: تكوين الجمل</p>
   <p>🔒 المستوى 3: المحادثة اليومية</p>
   <p class="small">ستفتح المستويات التالية تدريجياً عند إضافة دروسها.</p>
  </div>
 </section>

 <section id="quiz" class="tab hidden">
  <div class="card">
   <h2>🧠 اختبر نفسك</h2>
   <p id="question">ما معنى Hello؟</p>
   <div id="options"></div>
   <p id="feedback" aria-live="polite"></p>
   <button onclick="nextQuestion()">السؤال التالي ←</button>
  </div>
 </section>

 <section id="chat" class="tab hidden">
  <div class="card">
   <h2>💬 تدرّب على المحادثة</h2>
   <p class="small">تدرّب على حوار بسيط باللغة الإنجليزية مع ترجمة عربية.</p>
   <div class="chatlog" id="chatlog">
    <div class="msg">Teacher: Hello! How are you?<br>المعلّم: مرحباً! كيف حالك؟</div>
   </div>
   <input id="reply" placeholder="اكتب إجابتك بالإنجليزية..." dir="auto">
   <button onclick="sendReply()">إرسال</button>
   <button class="secondary" onclick="speakText('Hello! How are you?')">🔊 استمع للسؤال</button>
   <p class="small">هذه محادثة تدريبية مبرمجة وليست ذكاءً اصطناعياً متصلاً. سنضيف الذكاء الاصطناعي لاحقاً.</p>
  </div>
 </section>

 <section id="progress" class="tab hidden">
  <div class="card">
   <h2>🏆 إنجازاتك</h2>
   <p>النقاط: <strong id="points2">0</strong> ⭐</p>
   <p>الكلمات التي تعلّمتها: <strong id="learned">0</strong> من 5</p>
   <div class="progress"><div id="bar"></div></div>
   <p class="small" id="progressText">ابدأ أول درس لتسجيل تقدمك.</p>
   <button class="secondary" onclick="resetProgress()">إعادة التقدم من البداية</button>
  </div>
 </section>
</main>
<footer>British English Academy · تعلّم كل يوم، وتقدّم كل يوم 🇬🇧</footer>

<script>
const words=[
 {en:"Hello",ar:"مرحباً",ex:"Hello, how are you?"},
 {en:"Thank you",ar:"شكراً لك",ex:"Thank you very much."},
 {en:"Good morning",ar:"صباح الخير",ex:"Good morning, everyone."},
 {en:"Please",ar:"من فضلك",ex:"Can I have some water, please?"},
 {en:"Goodbye",ar:"إلى اللقاء",ex:"Goodbye! See you tomorrow."}
];
const questions=[
 {q:"ما معنى Hello؟",opts:["وداعاً","مرحباً","شكراً"],a:1},
 {q:"ما معنى Thank you؟",opts:["من فضلك","صباح الخير","شكراً لك"],a:2},
 {q:"كيف تقول صباح الخير؟",opts:["Good morning","Goodbye","Please"],a:0},
 {q:"ما معنى Please؟",opts:["مرحباً","من فضلك","إلى اللقاء"],a:1},
 {q:"كيف تقول إلى اللقاء؟",opts:["Thank you","Hello","Goodbye"],a:2}
];
let index=0,qi=0;
let state={points:0,learned:[],answered:[]};
try{state={...state,...JSON.parse(localStorage.getItem("bea-progress")||"{}")}}catch(e){}
function save(){
 try{localStorage.setItem("bea-progress",JSON.stringify(state))}catch(e){}
 updateProgress();
}
function updateProgress(){
 document.getElementById("points").textContent=state.points;
 document.getElementById("points2").textContent=state.points;
 document.getElementById("learned").textContent=state.learned.length;
 document.getElementById("bar").style.width=(state.learned.length/words.length*100)+"%";
 document.getElementById("progressText").textContent=state.learned.length===5?"أكملت الكلمات الأساسية! أحسنت 🎉":"أكملت "+state.learned.length+" من "+words.length+" كلمات.";
}
function renderWord(){
 const w=words[index];
 document.getElementById("word").textContent=w.en;
 document.getElementById("translation").textContent=w.ar;
 document.getElementById("example").innerHTML=w.ex+"<br>"+translateExample(index);
 document.getElementById("wordCount").textContent="الكلمة "+(index+1)+" من "+words.length;
}
function translateExample(i){
 return ["مرحباً، كيف حالك؟","شكراً جزيلاً.","صباح الخير للجميع.","هل يمكنني الحصول على بعض الماء، من فضلك؟","إلى اللقاء! أراك غداً."][i];
}
function nextWord(){
 state.learned=Array.from(new Set([...state.learned,index]));
 if(!state.learned.includes((index+1)%words.length)){}
 index=(index+1)%words.length;
 state.learned=Array.from(new Set([...state.learned,index]));
 save();renderWord();
}
function speak(){speakText(words[index].en)}
function speakText(text){
 if(!("speechSynthesis" in window)){alert("النطق غير مدعوم في هذا المتصفح.");return}
 speechSynthesis.cancel();
 const u=new SpeechSynthesisUtterance(text);
 u.lang="en-GB";u.rate=.82;
 const voices=speechSynthesis.getVoices();
 const british=voices.find(v=>v.lang==="en-GB");
 if(british)u.voice=british;
 speechSynthesis.speak(u);
}
function showTab(id){
 document.querySelectorAll(".tab").forEach(el=>el.classList.add("hidden"));
 document.getElementById(id).classList.remove("hidden");
 document.querySelectorAll(".nav button").forEach(el=>el.classList.remove("active"));
 document.getElementById("nav-"+id).classList.add("active");
 if(id==="quiz")renderQuestion();
 if(id==="progress")updateProgress();
}
function renderQuestion(){
 const q=questions[qi];
 document.getElementById("question").textContent=q.q;
 document.getElementById("feedback").textContent="";
 const box=document.getElementById("options");box.innerHTML="";
 q.opts.forEach((opt,i)=>{
  const b=document.createElement("button");
  b.className="option";b.textContent=opt;
  b.onclick=()=>answer(i);box.appendChild(b);
 });
}
function answer(i){
 const key=qi;
 if(state.answered.includes(key)){return}
 if(i===questions[qi].a){
  document.getElementById("feedback").textContent="إجابة صحيحة! أحسنت 🎉";
  state.points+=10;
 }else{
  document.getElementById("feedback").textContent="ليست صحيحة. الإجابة: "+questions[qi].opts[questions[qi].a];
 }
 state.answered.push(key);save();
}
function nextQuestion(){qi=(qi+1)%questions.length;renderQuestion()}
function sendReply(){
 const input=document.getElementById("reply"),v=input.value.trim();
 if(!v)return;
 const log=document.getElementById("chatlog");
 const me=document.createElement("div");me.className="msg me";me.textContent="You: "+v;log.appendChild(me);
 const lower=v.toLowerCase();
 let en="Nice to meet you!";let ar="سعيد بلقائك!";
 if(lower.includes("fine")||lower.includes("good")){en="That is great! What is your name?";ar="هذا رائع! ما اسمك؟"}
 else if(lower.includes("name")){en="Lovely to meet you. Where are you from?";ar="سعيد بمعرفتك. من أين أنت؟"}
 else if(lower.includes("oman")){en="Oman is a beautiful country!";ar="عُمان بلد جميل!"}
 else if(lower.includes("hello")||lower.includes("hi")){en="Hello! How are you?";ar="مرحباً! كيف حالك؟"}
 const bot=document.createElement("div");bot.className="msg";bot.textContent="Teacher: "+en+" — "+ar;log.appendChild(bot);
 input.value="";log.scrollTop=log.scrollHeight;
 state.points+=2;save();
}
function resetProgress(){
 if(confirm("هل تريد إعادة النقاط والتقدم إلى الصفر؟")){
  state={points:0,learned:[],answered:[]};save();renderWord();renderQuestion();
 }
}
renderWord();renderQuestion();updateProgress();
</script>
</body>
</html>

