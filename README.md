<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>今天的我 📔</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@500;700;800&family=Noto+Sans+TC:wght@400;500;700;900&display=swap" rel="stylesheet">
<style>
  :root{
    --ink:#2c2a3d;
    --ink-soft:#7d7894;
    --paper:#faf7f2;
    --card:#ffffff;
    --line:#ece7dd;
    --todo:#ff8a5b;
    --todo-soft:#fff0e6;
    --wish:#6a8eff;
    --wish-soft:#eaf0ff;
    --gold:#f4b740;
    --green:#3fae6a;
    --radius:18px;
    --shadow:0 8px 24px rgba(44,42,61,.08);
    font-size:16px;
  }
  *{box-sizing:border-box;margin:0;padding:0;}
  html,body{height:100%;}
  body{
    font-family:"Noto Sans TC",sans-serif;
    color:var(--ink);
    background:var(--paper);
    min-height:100%;
    -webkit-tap-highlight-color:transparent;
  }
  .num{font-family:"Baloo 2","Noto Sans TC",sans-serif;}
  button{font-family:inherit;cursor:pointer;border:none;background:none;color:inherit;}
  input{font-family:inherit;}

  /* ---------- 登入畫面 ---------- */
  #loginView{
    min-height:100vh;display:flex;flex-direction:column;
    align-items:center;justify-content:center;gap:20px;padding:24px;text-align:center;
  }
  .brand{font-size:2rem;font-weight:900;letter-spacing:.02em;}
  .brand .dot{color:var(--todo);}
  .brand-sub{color:var(--ink-soft);font-size:.95rem;max-width:280px;line-height:1.7;}
  .gbtn{
    display:flex;align-items:center;gap:10px;
    background:var(--card);border:1.5px solid var(--line);
    padding:13px 26px;border-radius:999px;font-weight:700;font-size:.98rem;
    box-shadow:var(--shadow);transition:transform .15s ease, box-shadow .15s ease;
  }
  .gbtn:active{transform:scale(.97);}
  .gbtn svg{width:20px;height:20px;}
  #loginErr{color:#d9534f;font-size:.85rem;min-height:1.2em;}

  /* ---------- 邀請碼選擇畫面 ---------- */
  #spaceView{
    min-height:100vh;display:none;flex-direction:column;align-items:center;
    justify-content:center;gap:18px;padding:24px;text-align:center;
  }
  #spaceView.show{display:flex;}
  .space-card{
    background:var(--card);border-radius:var(--radius);box-shadow:var(--shadow);
    padding:28px 24px;max-width:340px;width:100%;display:flex;flex-direction:column;gap:14px;
  }
  .space-title{font-weight:800;font-size:1.15rem;}
  .space-desc{color:var(--ink-soft);font-size:.85rem;line-height:1.6;}
  .seg{display:flex;background:var(--paper);border-radius:999px;padding:4px;gap:4px;}
  .seg button{flex:1;padding:9px 0;border-radius:999px;font-weight:700;font-size:.88rem;color:var(--ink-soft);transition:.2s;}
  .seg button.active{background:var(--ink);color:#fff;}
  .code-input{
    width:100%;padding:14px;border:1.5px solid var(--line);border-radius:12px;
    font-size:1.3rem;text-align:center;letter-spacing:.25em;font-weight:800;
    font-family:"Baloo 2",sans-serif;text-transform:uppercase;
  }
  .code-input:focus{outline:none;border-color:var(--todo);}
  .primary-btn{
    background:var(--ink);color:#fff;padding:13px;border-radius:12px;font-weight:700;font-size:.95rem;
    transition:transform .15s ease;
  }
  .primary-btn:active{transform:scale(.97);}
  .primary-btn:disabled{opacity:.4;}
  .code-display{
    font-family:"Baloo 2",sans-serif;font-size:1.6rem;font-weight:800;letter-spacing:.2em;
    background:var(--todo-soft);color:var(--todo);padding:14px;border-radius:12px;
  }
  #spaceErr{color:#d9534f;font-size:.82rem;min-height:1.2em;}
  .small-link{color:var(--ink-soft);font-size:.82rem;text-decoration:underline;margin-top:4px;}

  /* ---------- 主畫面 ---------- */
  #appView{display:none;min-height:100vh;flex-direction:column;}
  #appView.show{display:flex;}

  .topbar{
    display:flex;align-items:center;justify-content:space-between;
    padding:16px 18px 12px;
  }
  .topbar .brand{font-size:1.15rem;}
  .avatar-wrap{position:relative;}
  .avatar{width:36px;height:36px;border-radius:50%;border:2px solid var(--card);box-shadow:var(--shadow);object-fit:cover;}
  .menu{
    position:absolute;right:0;top:44px;background:var(--card);border-radius:14px;
    box-shadow:var(--shadow);padding:8px;display:none;flex-direction:column;min-width:170px;z-index:30;
  }
  .menu.show{display:flex;}
  .menu button{padding:10px 12px;border-radius:10px;text-align:left;font-size:.88rem;font-weight:600;}
  .menu button:active{background:var(--paper);}
  .menu .code-row{padding:10px 12px;font-size:.78rem;color:var(--ink-soft);border-bottom:1px solid var(--line);margin-bottom:4px;}
  .menu .code-row b{display:block;font-family:"Baloo 2",sans-serif;font-size:1rem;letter-spacing:.15em;color:var(--ink);margin-top:2px;}

  .tabs{
    display:flex;gap:6px;padding:0 18px 12px;
  }
  .tab{
    flex:1;padding:10px 0;text-align:center;border-radius:12px;font-weight:700;font-size:.88rem;
    color:var(--ink-soft);background:var(--card);transition:.2s;
  }
  .tab.active{background:var(--ink);color:#fff;}

  .page{display:none;flex:1;padding:0 18px 100px;overflow-y:auto;}
  .page.show{display:block;}

  /* 清單頁 */
  .list-toggle{display:flex;gap:8px;margin-bottom:16px;}
  .list-toggle button{
    flex:1;padding:12px 0;border-radius:14px;font-weight:800;font-size:.92rem;
    background:var(--card);color:var(--ink-soft);box-shadow:var(--shadow);transition:.2s;
    display:flex;align-items:center;justify-content:center;gap:6px;
  }
  .list-toggle button.active.todo{background:var(--todo);color:#fff;}
  .list-toggle button.active.wish{background:var(--wish);color:#fff;}

  .add-row{display:flex;gap:8px;margin-bottom:16px;}
  .add-row input{
    flex:1;padding:12px 14px;border:1.5px solid var(--line);border-radius:12px;font-size:.92rem;background:var(--card);
  }
  .add-row input:focus{outline:none;border-color:var(--todo);}
  .add-row button{
    width:46px;height:46px;border-radius:12px;background:var(--ink);color:#fff;
    font-size:1.3rem;font-weight:700;flex-shrink:0;
  }
  .add-row button:active{transform:scale(.94);}

  .item-list{display:flex;flex-direction:column;gap:10px;}
  .item{
    display:flex;align-items:center;gap:12px;background:var(--card);
    padding:13px 14px;border-radius:14px;box-shadow:var(--shadow);
    animation:popin .25s ease;
  }
  @keyframes popin{from{opacity:0;transform:translateY(6px);}to{opacity:1;transform:translateY(0);}}
  .check{
    width:24px;height:24px;border-radius:50%;border:2px solid var(--line);flex-shrink:0;
    display:flex;align-items:center;justify-content:center;transition:.2s;
  }
  .item.todo .check{border-color:var(--todo);}
  .item.wish .check{border-color:var(--wish);}
  .item.done .check{background:var(--green);border-color:var(--green);}
  .check svg{width:14px;height:14px;opacity:0;transition:.15s;}
  .item.done .check svg{opacity:1;}
  .item-text{flex:1;font-size:.92rem;line-height:1.4;word-break:break-word;}
  .item.done .item-text{color:var(--ink-soft);text-decoration:line-through;}
  .item-del{color:var(--ink-soft);font-size:1.1rem;padding:4px;flex-shrink:0;}
  .empty-state{text-align:center;color:var(--ink-soft);font-size:.85rem;padding:50px 20px;line-height:1.8;}
  .empty-state .em{font-size:2rem;display:block;margin-bottom:8px;}

  /* 日曆頁 */
  .cal-head{display:flex;align-items:center;justify-content:space-between;margin:8px 0 16px;}
  .cal-head h2{font-size:1.1rem;font-weight:800;}
  .cal-nav{display:flex;gap:6px;}
  .cal-nav button{
    width:32px;height:32px;border-radius:8px;background:var(--card);box-shadow:var(--shadow);
    display:flex;align-items:center;justify-content:center;font-weight:700;
  }
  .cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:6px;margin-bottom:18px;}
  .cal-dow{text-align:center;font-size:.72rem;color:var(--ink-soft);font-weight:700;padding-bottom:4px;}
  .cal-cell{
    aspect-ratio:1;border-radius:10px;display:flex;flex-direction:column;align-items:center;justify-content:center;
    font-size:.8rem;font-weight:600;background:var(--card);position:relative;color:var(--ink);
    box-shadow:0 2px 6px rgba(44,42,61,.05);
  }
  .cal-cell.empty{background:transparent;box-shadow:none;}
  .cal-cell.today{outline:2px solid var(--todo);outline-offset:-2px;}
  .cal-cell .dots{display:flex;gap:3px;margin-top:3px;}
  .cal-cell .dot{width:5px;height:5px;border-radius:50%;}
  .dot.todo{background:var(--todo);}
  .dot.wish{background:var(--wish);}
  .cal-cell.selected{background:var(--ink);color:#fff;}

  .day-detail{background:var(--card);border-radius:16px;box-shadow:var(--shadow);padding:16px;}
  .day-detail h3{font-size:.95rem;font-weight:800;margin-bottom:10px;}
  .day-detail .dgroup{margin-bottom:12px;}
  .day-detail .dgroup-title{font-size:.78rem;color:var(--ink-soft);font-weight:700;margin-bottom:6px;}
  .day-detail .ditem{
    display:flex;align-items:center;gap:8px;font-size:.86rem;padding:6px 0;
  }
  .day-detail .ditem .dot{width:6px;height:6px;border-radius:50%;flex-shrink:0;}
  .day-detail .ditem.done{color:var(--ink-soft);text-decoration:line-through;}
  .day-empty{color:var(--ink-soft);font-size:.82rem;text-align:center;padding:14px;}

  /* toast */
  #toast{
    position:fixed;bottom:24px;left:50%;transform:translateX(-50%) translateY(20px);
    background:var(--ink);color:#fff;padding:11px 22px;border-radius:999px;font-size:.85rem;font-weight:600;
    opacity:0;transition:.25s;pointer-events:none;z-index:100;box-shadow:0 8px 20px rgba(0,0,0,.2);white-space:nowrap;
  }
  #toast.show{opacity:1;transform:translateX(-50%) translateY(0);}

  ::-webkit-scrollbar{display:none;}
</style>
</head>
<body>

<!-- 登入畫面 -->
<div id="loginView">
  <div class="brand">今天的我<span class="dot">.</span></div>
  <div class="brand-sub">把要做的事跟想做的事都記下來，每完成一件就打一個勾 ✅</div>
  <button class="gbtn" id="loginBtn">
    <svg viewBox="0 0 48 48"><path fill="#FFC107" d="M43.6 20.5H42V20H24v8h11.3c-1.6 4.7-6.1 8-11.3 8-6.6 0-12-5.4-12-12s5.4-12 12-12c3.1 0 5.8 1.1 8 3l5.7-5.7C34.6 6.5 29.6 4.5 24 4.5 13.2 4.5 4.5 13.2 4.5 24S13.2 43.5 24 43.5 43.5 34.8 43.5 24c0-1.2-.1-2.4-.3-3.5z"/><path fill="#FF3D00" d="M6.3 14.7l6.6 4.8C14.6 16 18.9 13 24 13c3.1 0 5.8 1.1 8 3l5.7-5.7C34.6 6.5 29.6 4.5 24 4.5c-7.7 0-14.4 4.4-17.7 10.2z"/><path fill="#4CAF50" d="M24 43.5c5.5 0 10.4-1.9 14.2-5.1l-6.6-5.4c-2 1.5-4.6 2.4-7.6 2.4-5.2 0-9.6-3.3-11.3-8l-6.6 5.1c3.3 6.6 10 11 18 11z"/><path fill="#1976D2" d="M43.6 20.5H42V20H24v8h11.3c-.8 2.3-2.2 4.2-4.1 5.5l6.6 5.4C40.9 36.5 43.5 30.8 43.5 24c0-1.2-.1-2.4-.3-3.5z"/></svg>
    使用 Google 帳號登入
  </button>
  <div id="loginErr"></div>
</div>

<!-- 邀請碼選擇畫面 -->
<div id="spaceView">
  <div class="space-card">
    <div class="space-title">建立新的本子 📔 還是加入朋友的？</div>
    <div class="seg">
      <button id="segCreate" class="active">建立新的</button>
      <button id="segJoin">加入朋友的</button>
    </div>

    <div id="createPane">
      <div class="space-desc">幫你生一組專屬代碼，給朋友這組代碼，他就能一起看、一起編輯。</div>
      <button class="primary-btn" id="createBtn">建立我的本子</button>
    </div>

    <div id="joinPane" style="display:none;">
      <div class="space-desc">輸入朋友給你的 6 碼代號（數字+英文）</div>
      <input type="text" id="joinCodeInput" class="code-input" maxlength="6" placeholder="A3F9K2">
      <button class="primary-btn" id="joinBtn">加入</button>
    </div>

    <div id="spaceErr"></div>
  </div>
</div>

<!-- 主畫面 -->
<div id="appView">
  <div class="topbar">
    <div class="brand">今天的我<span class="dot">.</span></div>
    <div class="avatar-wrap">
      <img id="userAvatar" class="avatar" src="" alt="">
      <div class="menu" id="userMenu">
        <div class="code-row">這本子的代碼<b id="menuCode">------</b></div>
        <button id="copyCodeBtn">📋 複製代碼</button>
        <button id="switchSpaceBtn">🔄 切換 / 加入其他本子</button>
        <button id="logoutBtn">🚪 登出</button>
      </div>
    </div>
  </div>

  <div class="tabs">
    <button class="tab active" data-page="listPage">✅ 清單</button>
    <button class="tab" data-page="calPage">📅 日曆</button>
  </div>

  <!-- 清單頁 -->
  <div class="page show" id="listPage">
    <div class="list-toggle">
      <button class="active todo" id="toggleTodo">📌 要做的事</button>
      <button class="wish" id="toggleWish">⭐ 想做的事</button>
    </div>

    <div class="add-row">
      <input type="text" id="itemInput" placeholder="新增一件事...">
      <button id="addBtn">＋</button>
    </div>

    <div class="item-list" id="itemList"></div>
  </div>

  <!-- 日曆頁 -->
  <div class="page" id="calPage">
    <div class="cal-head">
      <div class="cal-nav"><button id="prevMonth">‹</button></div>
      <h2 id="calMonthLabel">2026年6月</h2>
      <div class="cal-nav"><button id="nextMonth">›</button></div>
    </div>
    <div class="cal-grid" id="calGrid"></div>
    <div class="day-detail" id="dayDetail"></div>
  </div>
</div>

<div id="toast"></div>

<!-- ⭐ Firebase 設定區（待貼上） ⭐ -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
import {
  getAuth, GoogleAuthProvider, signInWithPopup, signOut, onAuthStateChanged
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";
import {
  getFirestore, doc, getDoc, setDoc, updateDoc, deleteDoc,
  collection, query, orderBy, onSnapshot, serverTimestamp, addDoc
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

// ⭐ 請把你的 Firebase 設定貼在這裡 ⭐
const firebaseConfig = {
  apiKey: "AIzaSyAzwy5AOueAvh-O4WoU4BznbVMdQJBHgZ4",
  authDomain: "todo-app-d20ad.firebaseapp.com",
  projectId: "todo-app-d20ad",
  storageBucket: "todo-app-d20ad.firebasestorage.app",
  messagingSenderId: "201836062560",
  appId: "1:201836062560:web:aac7ced99365f6dcfa6005"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const provider = new GoogleAuthProvider();

let currentUser = null;
let currentSpaceId = null;
let unsubItems = null;
let activeList = "todo"; // todo | wish
let calDate = new Date();
let selectedDay = null;
let allItems = []; // cached items for current space

const $ = (id) => document.getElementById(id);
function toast(msg){
  const t = $("toast");
  t.textContent = msg;
  t.classList.add("show");
  clearTimeout(toast._tm);
  toast._tm = setTimeout(()=>t.classList.remove("show"), 1800);
}
function genCode(){
  const chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789"; // 避開易混淆字元
  let code = "";
  for(let i=0;i<6;i++) code += chars[Math.floor(Math.random()*chars.length)];
  return code;
}
async function genUniqueCode(){
  let code, exists = true, tries = 0;
  while(exists && tries < 20){
    code = genCode();
    const snap = await getDoc(doc(db, "spaces", code));
    exists = snap.exists();
    tries++;
  }
  return code;
}

// ---------- 登入 ----------
$("loginBtn").onclick = async () => {
  $("loginErr").textContent = "";
  try{
    await signInWithPopup(auth, provider);
  }catch(e){
    $("loginErr").textContent = "登入失敗，再試一次看看";
  }
};
$("logoutBtn").onclick = async () => {
  await signOut(auth);
  location.reload();
};

onAuthStateChanged(auth, async (user) => {
  if(user){
    currentUser = user;
    $("userAvatar").src = user.photoURL || "";
    const userDoc = await getDoc(doc(db, "users", user.uid));
    if(userDoc.exists() && userDoc.data().spaceId){
      enterSpace(userDoc.data().spaceId);
    }else{
      $("loginView").style.display = "none";
      $("spaceView").classList.add("show");
    }
  }else{
    $("loginView").style.display = "flex";
    $("spaceView").classList.remove("show");
    $("appView").classList.remove("show");
  }
});

// ---------- 建立 / 加入本子 ----------
$("segCreate").onclick = () => {
  $("segCreate").classList.add("active");
  $("segJoin").classList.remove("active");
  $("createPane").style.display = "block";
  $("joinPane").style.display = "none";
  $("spaceErr").textContent = "";
};
$("segJoin").onclick = () => {
  $("segJoin").classList.add("active");
  $("segCreate").classList.remove("active");
  $("joinPane").style.display = "block";
  $("createPane").style.display = "none";
  $("spaceErr").textContent = "";
};

$("createBtn").onclick = async () => {
  $("createBtn").disabled = true;
  const code = await genUniqueCode();
  await setDoc(doc(db, "spaces", code), {
    createdBy: currentUser.uid,
    createdAt: serverTimestamp(),
    members: [currentUser.uid]
  });
  await setDoc(doc(db, "users", currentUser.uid), { spaceId: code }, { merge: true });
  enterSpace(code);
};

$("joinBtn").onclick = async () => {
  const code = $("joinCodeInput").value.trim().toUpperCase();
  if(code.length !== 6){
    $("spaceErr").textContent = "代碼要剛好 6 個字喔";
    return;
  }
  const snap = await getDoc(doc(db, "spaces", code));
  if(!snap.exists()){
    $("spaceErr").textContent = "找不到這組代碼，再檢查一下";
    return;
  }
  const data = snap.data();
  const members = data.members || [];
  if(!members.includes(currentUser.uid)){
    await updateDoc(doc(db, "spaces", code), { members: [...members, currentUser.uid] });
  }
  await setDoc(doc(db, "users", currentUser.uid), { spaceId: code }, { merge: true });
  enterSpace(code);
};

function enterSpace(spaceId){
  currentSpaceId = spaceId;
  $("loginView").style.display = "none";
  $("spaceView").classList.remove("show");
  $("appView").classList.add("show");
  $("menuCode").textContent = spaceId;
  listenItems();
  renderCalendar();
}

// ---------- 選單 ----------
$("userAvatar").onclick = () => $("userMenu").classList.toggle("show");
document.addEventListener("click", (e) => {
  if(!$("userAvatar").contains(e.target) && !$("userMenu").contains(e.target)){
    $("userMenu").classList.remove("show");
  }
});
$("copyCodeBtn").onclick = async () => {
  try{
    await navigator.clipboard.writeText(currentSpaceId);
    toast("代碼已複製 📋");
  }catch(e){
    toast("代碼是：" + currentSpaceId);
  }
  $("userMenu").classList.remove("show");
};
$("switchSpaceBtn").onclick = () => {
  $("appView").classList.remove("show");
  $("spaceView").classList.add("show");
  $("userMenu").classList.remove("show");
};

// ---------- 分頁切換 ----------
document.querySelectorAll(".tab").forEach(tab => {
  tab.onclick = () => {
    document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
    document.querySelectorAll(".page").forEach(p=>p.classList.remove("show"));
    tab.classList.add("active");
    $(tab.dataset.page).classList.add("show");
  };
});

// ---------- 清單功能 ----------
$("toggleTodo").onclick = () => switchList("todo");
$("toggleWish").onclick = () => switchList("wish");
function switchList(type){
  activeList = type;
  $("toggleTodo").classList.toggle("active", type==="todo");
  $("toggleWish").classList.toggle("active", type==="wish");
  renderItems();
}

$("addBtn").onclick = addItem;
$("itemInput").onkeydown = (e) => { if(e.key === "Enter") addItem(); };

async function addItem(){
  const input = $("itemInput");
  const text = input.value.trim();
  if(!text) return;
  input.value = "";
  await addDoc(collection(db, "spaces", currentSpaceId, "items"), {
    text, type: activeList, done: false,
    createdAt: serverTimestamp(),
    doneAt: null
  });
}

function listenItems(){
  if(unsubItems) unsubItems();
  const q = query(collection(db, "spaces", currentSpaceId, "items"), orderBy("createdAt", "desc"));
  unsubItems = onSnapshot(q, (snap) => {
    allItems = [];
    snap.forEach(d => allItems.push({ id:d.id, ...d.data() }));
    renderItems();
    renderCalendar();
    if(selectedDay) renderDayDetail(selectedDay);
  });
}

function renderItems(){
  const list = $("itemList");
  const filtered = allItems.filter(i => i.type === activeList);
  if(filtered.length === 0){
    list.innerHTML = `<div class="empty-state"><span class="em">${activeList==="todo"?"📌":"⭐"}</span>${activeList==="todo"?"還沒有要做的事，新增一件吧":"還沒有想做的事，新增一個願望吧"}</div>`;
    return;
  }
  list.innerHTML = "";
  filtered.forEach(item => {
    const div = document.createElement("div");
    div.className = `item ${item.type} ${item.done ? "done":""}`;
    div.innerHTML = `
      <button class="check" data-id="${item.id}" data-done="${item.done}">
        <svg viewBox="0 0 24 24" fill="none"><path d="M5 13l4 4L19 7" stroke="#fff" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/></svg>
      </button>
      <div class="item-text">${esc(item.text)}</div>
      <button class="item-del" data-del="${item.id}">🗑️</button>
    `;
    list.appendChild(div);
  });
  list.querySelectorAll(".check").forEach(btn => {
    btn.onclick = async () => {
      const id = btn.dataset.id;
      const done = btn.dataset.done === "true";
      await updateDoc(doc(db, "spaces", currentSpaceId, "items", id), {
        done: !done,
        doneAt: !done ? serverTimestamp() : null
      });
    };
  });
  list.querySelectorAll("[data-del]").forEach(btn => {
    btn.onclick = async () => {
      await deleteDoc(doc(db, "spaces", currentSpaceId, "items", btn.dataset.del));
      toast("刪掉了");
    };
  });
}

function esc(s){
  const d = document.createElement("div");
  d.textContent = s;
  return d.innerHTML;
}

// ---------- 日曆功能 ----------
const DOW = ["日","一","二","三","四","五","六"];
$("prevMonth").onclick = () => { calDate.setMonth(calDate.getMonth()-1); renderCalendar(); };
$("nextMonth").onclick = () => { calDate.setMonth(calDate.getMonth()+1); renderCalendar(); };

function ymd(date){
  return `${date.getFullYear()}-${String(date.getMonth()+1).padStart(2,"0")}-${String(date.getDate()).padStart(2,"0")}`;
}
function itemDateKey(item){
  // 用完成日期分類；若未完成則用建立日期（讓「今天新增的」也看得到）
  const ts = item.done && item.doneAt ? item.doneAt : item.createdAt;
  if(!ts || !ts.toDate) return null;
  return ymd(ts.toDate());
}

function renderCalendar(){
  const year = calDate.getFullYear();
  const month = calDate.getMonth();
  $("calMonthLabel").textContent = `${year}年${month+1}月`;

  const firstDay = new Date(year, month, 1);
  const startWeekday = firstDay.getDay();
  const daysInMonth = new Date(year, month+1, 0).getDate();
  const todayKey = ymd(new Date());

  // 統計每天有什麼
  const dayMap = {};
  allItems.forEach(item => {
    const key = itemDateKey(item);
    if(!key) return;
    if(!dayMap[key]) dayMap[key] = { todo:false, wish:false };
    dayMap[key][item.type] = true;
  });

  const grid = $("calGrid");
  grid.innerHTML = "";
  DOW.forEach(d => {
    const el = document.createElement("div");
    el.className = "cal-dow";
    el.textContent = d;
    grid.appendChild(el);
  });
  for(let i=0;i<startWeekday;i++){
    const el = document.createElement("div");
    el.className = "cal-cell empty";
    grid.appendChild(el);
  }
  for(let d=1; d<=daysInMonth; d++){
    const cellDate = new Date(year, month, d);
    const key = ymd(cellDate);
    const cell = document.createElement("div");
    cell.className = "cal-cell";
    if(key === todayKey) cell.classList.add("today");
    if(key === selectedDay) cell.classList.add("selected");
    let dotsHtml = "";
    if(dayMap[key]){
      dotsHtml = `<div class="dots">${dayMap[key].todo?'<span class="dot todo"></span>':''}${dayMap[key].wish?'<span class="dot wish"></span>':''}</div>`;
    }
    cell.innerHTML = `<span>${d}</span>${dotsHtml}`;
    cell.onclick = () => {
      selectedDay = key;
      renderCalendar();
      renderDayDetail(key);
    };
    grid.appendChild(cell);
  }

  if(!selectedDay){
    selectedDay = todayKey;
    renderDayDetail(todayKey);
  }
}

function renderDayDetail(key){
  const detail = $("dayDetail");
  const dayItems = allItems.filter(item => itemDateKey(item) === key);
  const dateObj = new Date(key + "T00:00:00");
  const label = `${dateObj.getMonth()+1}月${dateObj.getDate()}日`;

  if(dayItems.length === 0){
    detail.innerHTML = `<h3>${label}</h3><div class="day-empty">這天還沒有紀錄</div>`;
    return;
  }
  const todos = dayItems.filter(i=>i.type==="todo");
  const wishes = dayItems.filter(i=>i.type==="wish");

  let html = `<h3>${label}</h3>`;
  if(todos.length){
    html += `<div class="dgroup"><div class="dgroup-title">📌 要做的事</div>`;
    todos.forEach(i => {
      html += `<div class="ditem ${i.done?'done':''}"><span class="dot todo"></span>${esc(i.text)}</div>`;
    });
    html += `</div>`;
  }
  if(wishes.length){
    html += `<div class="dgroup"><div class="dgroup-title">⭐ 想做的事</div>`;
    wishes.forEach(i => {
      html += `<div class="ditem ${i.done?'done':''}"><span class="dot wish"></span>${esc(i.text)}</div>`;
    });
    html += `</div>`;
  }
  detail.innerHTML = html;
}

</script>
</body>
</html>
