<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
<meta name="theme-color" content="#F2F2F7">
<title>DMX Pro Master v9 by SoloSiden</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<style>
:root{
  --blue:#007AFF; --green:#34C759; --orange:#FF9500; --red:#FF3B30;
  --bg:#F2F2F7; --card:#FFFFFF; --text:#000000; --gray:#8E8E93;
  --fill:rgba(118,118,128,.14); --sep:rgba(60,60,67,.14); --input:#FFFFFF;
  --safe-t:env(safe-area-inset-top,0px); --safe-b:env(safe-area-inset-bottom,0px);
}
:root[data-theme="dark"]{
  --bg:#000000; --card:#1C1C1E; --text:#FFFFFF; --gray:#98989F;
  --fill:rgba(118,118,128,.24); --sep:rgba(84,84,88,.55); --input:#2C2C2E;
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html{-webkit-text-size-adjust:100%}
body{
  margin:0; background:var(--bg); color:var(--text);
  font-family:-apple-system,BlinkMacSystemFont,"SF Pro Text","Segoe UI",Roboto,sans-serif;
  padding:calc(var(--safe-t) + 12px) 16px calc(var(--safe-b) + 150px);
  -webkit-user-select:none; user-select:none; touch-action:manipulation;
  overscroll-behavior-y:none;
}
body.locked{overflow:hidden}
input,select,button,textarea{font-family:inherit;-webkit-user-select:text;user-select:text}
button{cursor:pointer;border:none;background:none;color:inherit;padding:0;touch-action:manipulation}
button:active{opacity:.6}

.top{display:flex;align-items:center;justify-content:space-between;margin:4px 4px 6px}
.top h1{font-size:28px;letter-spacing:-.8px;margin:0}
.icon-btn{width:44px;height:44px;border-radius:12px;font-size:20px;color:var(--blue);display:flex;align-items:center;justify-content:center;flex:none}
.icon-btn.sm{width:40px;height:40px;font-size:18px}

.cat{font-size:12px;font-weight:800;color:var(--gray);margin:24px 6px 8px;text-transform:uppercase;letter-spacing:.3px}
.card{background:var(--card);border-radius:16px;padding:12px 12px 12px 16px;margin-bottom:10px;box-shadow:0 2px 8px rgba(0,0,0,.06)}
.row{display:flex;justify-content:space-between;align-items:center;gap:8px}
.card .name{font-weight:600;font-size:17px;overflow-wrap:anywhere}
.card .meta{font-size:13px;color:var(--gray);margin-top:2px}
.card-bottom{display:flex;align-items:center;justify-content:space-between;gap:10px;margin-top:8px}
.mode-select{flex:1;min-width:0;height:44px;padding:0 12px;border-radius:12px;border:none;background:var(--fill);color:var(--blue);font-size:16px;font-weight:600;-webkit-appearance:none;appearance:none}
.mode-single{flex:1;color:var(--blue);font-weight:600;font-size:16px;padding-left:2px}
.stepper{display:flex;align-items:center;background:var(--fill);border-radius:12px;flex:none}
.step-btn{color:var(--blue);font-size:28px;width:46px;height:44px;font-weight:500;line-height:1}
.qty-input{width:54px;height:44px;border:none;background:transparent;text-align:center;color:var(--text);font-size:20px;font-weight:700;outline:none;padding:0;-moz-appearance:textfield}
.qty-input::-webkit-outer-spin-button,.qty-input::-webkit-inner-spin-button{-webkit-appearance:none;margin:0}

.add-btn{display:block;width:100%;margin:18px 0 0;padding:15px;border-radius:14px;background:var(--card);color:var(--blue);font-weight:700;font-size:16px;border:1.5px dashed var(--sep)}
.empty{text-align:center;color:var(--gray);padding:40px 10px}

.u-head{display:flex;justify-content:space-between;font-weight:800;color:var(--blue);margin:26px 2px 6px}
.p-bar{height:8px;background:var(--fill);border-radius:4px;margin:0 0 12px;overflow:hidden}
.p-bar-fill{height:100%;transition:width .3s}
.plist{background:var(--card);border-radius:14px;overflow:hidden}
.prow{display:flex;justify-content:space-between;align-items:center;padding:12px 14px;border-bottom:1px solid var(--sep)}
.prow:last-child{border-bottom:none}
.prow .paddr b{color:var(--blue);font-size:17px}
.prow .paddr small{color:var(--gray);margin-left:6px;font-size:12px}
.note{background:rgba(255,149,0,.15);color:var(--orange);padding:12px 14px;border-radius:12px;font-size:13px;font-weight:600;margin-top:18px}
.link-red{display:block;text-align:center;margin:30px auto 10px;color:var(--red);font-weight:600;font-size:15px;padding:10px}

.fab-group{position:fixed;left:16px;right:16px;bottom:calc(var(--safe-b) + 16px);display:none;gap:12px;z-index:50}
.fab-btn{flex:1;padding:18px;border-radius:18px;font-weight:700;color:#fff;font-size:16px;box-shadow:0 8px 20px rgba(0,0,0,.22)}

/* layers */
.layer{position:fixed;inset:0;z-index:1000;display:none}
.layer.open{display:block}
.layer.full{background:var(--bg);overflow-y:auto;-webkit-overflow-scrolling:touch;overscroll-behavior:contain;
  padding:calc(var(--safe-t) + 12px) 20px calc(var(--safe-b) + 24px)}
.layer.sheet-wrap{background:rgba(0,0,0,.45)}
.layer.sheet-wrap.open{display:flex;align-items:flex-end}
.sheet{width:100%;max-height:88vh;max-height:88dvh;overflow-y:auto;-webkit-overflow-scrolling:touch;overscroll-behavior:contain;
  background:var(--bg);border-radius:22px 22px 0 0;padding:16px 16px calc(var(--safe-b) + 20px);animation:up .25s ease-out}
@keyframes up{from{transform:translateY(40px);opacity:.4}to{transform:none;opacity:1}}
.bar{display:flex;justify-content:space-between;align-items:center;min-height:44px}
.bar .t{font-weight:700;font-size:17px}
.link{color:var(--blue);font-weight:600;font-size:17px;padding:10px 4px}
.link.bold{font-weight:700}

.field{margin-top:14px}
.field label{display:block;font-size:12px;font-weight:700;color:var(--gray);text-transform:uppercase;margin:0 6px 6px}
.field input{width:100%;height:48px;padding:0 14px;border-radius:12px;border:none;background:var(--input);color:var(--text);font-size:16px;outline:none}
.field small{display:block;color:var(--gray);font-size:12px;margin:6px 6px 0}
.err{color:var(--red);font-size:13px;font-weight:600;margin:12px 6px 0;min-height:16px}
.btn{display:block;width:100%;padding:15px;border-radius:14px;font-weight:700;font-size:17px;margin-top:12px;text-align:center}
.btn.primary{background:var(--blue);color:#fff}
.btn.danger{background:rgba(255,59,48,.14);color:var(--red)}
.btn.armed{background:var(--red);color:#fff}
.btn.plain{background:var(--card);color:var(--text)}

/* power */
.pwr-box{padding:28px;border-radius:24px;text-align:center;color:#fff;margin:16px 0 18px}
.pwr-green{background:linear-gradient(135deg,#34C759,#248A3D)}
.pwr-orange{background:linear-gradient(135deg,#FF9500,#C97600)}
.pwr-red{background:linear-gradient(135deg,#FF3B30,#AF2922)}
.pwr-kw{font-size:52px;font-weight:900;letter-spacing:-1px}
.pwr-a{font-weight:700;opacity:.92;margin-top:4px}
.info-card{background:var(--card);border-radius:14px;padding:14px 16px;margin-bottom:10px}
.brk{display:flex;justify-content:space-between;padding:6px 0;font-size:15px;gap:10px}
.brk span:last-child{color:var(--gray);white-space:nowrap}

/* addr */
.addr-wrap{text-align:center;margin-top:6px}
.badge{background:var(--blue);color:#fff;padding:6px 16px;border-radius:10px;font-weight:800;display:inline-block;margin-bottom:12px}
#c-name{font-weight:700;color:var(--gray);margin-bottom:2px;text-transform:uppercase;font-size:12px;min-height:15px}
#c-addr{font-size:clamp(90px,32vw,130px);font-weight:900;color:var(--blue);line-height:1;letter-spacing:-5px}
#c-range{color:var(--gray);font-size:14px;font-weight:600;min-height:18px;margin-top:4px}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:24px}
.addr-btn{background:var(--card);padding:14px 8px;border-radius:14px;text-align:center;min-height:64px}
.addr-btn b{font-size:15px;overflow-wrap:anywhere}
.addr-btn .last{color:var(--green);font-size:12px;font-weight:800;display:block;margin-top:4px}
.addr-btn:disabled{opacity:.25}
.hist{margin-top:24px;text-align:left;background:var(--fill);border-radius:16px;padding:16px}
.hist small{font-weight:800;color:var(--blue);text-transform:uppercase}
.hrow{display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--sep);font-size:14px}
.hrow:last-child{border-bottom:none}
.hrow b{color:var(--blue)}
</style>
</head>
<body>

<header class="top">
  <h1>DMX Master Pro</h1>
  <button class="icon-btn" data-act="settings" aria-label="Настройки">⚙︎</button>
</header>

<div id="fixture-list"></div>
<button class="add-btn" data-act="add">＋ Новый прибор</button>
<div id="result-area"></div>

<div class="fab-group" id="fabs">
  <button class="fab-btn" style="background:var(--orange)" data-act="openPwr">⚡ POWER</button>
  <button class="fab-btn" style="background:var(--blue)" data-act="openAddr">📍 ADDR</button>
</div>

<!-- Нагрузка -->
<div class="layer full" id="layer-pwr">
  <div class="bar"><span></span><button class="link bold" data-act="close" data-layer="pwr">Закрыть</button></div>
  <h1 style="margin:8px 0 0;letter-spacing:-.8px">Нагрузка</h1>
  <div id="pwr-card" class="pwr-box pwr-green">
    <div class="pwr-kw" id="pwr-kw">0 кВт</div>
    <div class="pwr-a" id="pwr-a">0 А</div>
  </div>
  <div id="pwr-recs"></div>
</div>

<!-- Адресация -->
<div class="layer full" id="layer-addr">
  <div class="bar">
    <button class="link" data-act="undo">↩︎ Отменить</button>
    <button class="link bold" data-act="close" data-layer="addr">Готово</button>
  </div>
  <div class="addr-wrap">
    <div id="uni-info-box"></div>
    <div id="c-name">ВЫБОР</div>
    <div id="c-addr">---</div>
    <div id="c-range"></div>
    <div class="grid" id="c-btns"></div>
    <div class="hist">
      <small>История (Last 5):</small>
      <div id="history-content" style="margin-top:8px"></div>
    </div>
    <button class="link-red" data-act="resetProgress">Сбросить прогресс</button>
  </div>
</div>

<!-- Редактор прибора -->
<div class="layer sheet-wrap" id="layer-edit">
  <div class="sheet">
    <div class="bar">
      <button class="link" data-act="close" data-layer="edit">Отмена</button>
      <span class="t" id="e-title">Новый прибор</span>
      <button class="link bold" data-act="saveFixture">Сохранить</button>
    </div>
    <div class="field"><label for="e-name">Название</label><input id="e-name" type="text" maxlength="40" autocomplete="off" autocapitalize="words"></div>
    <div class="field"><label for="e-cat">Категория</label><input id="e-cat" type="text" maxlength="24" list="cat-list" autocomplete="off" placeholder="Spots, Washes, Other…"><datalist id="cat-list"></datalist></div>
    <div class="field"><label for="e-w">Мощность, Вт</label><input id="e-w" type="number" inputmode="numeric" min="0" max="100000" placeholder="750"></div>
    <div class="field"><label for="e-modes">Режимы (каналы)</label><input id="e-modes" type="text" inputmode="text" autocomplete="off" placeholder="35, 21"><small>Через запятую. Каждое число — количество каналов (1–512).</small></div>
    <div class="err" id="e-err"></div>
    <button class="btn danger" id="e-del" data-act="deleteFixture">Удалить прибор</button>
  </div>
</div>

<!-- Настройки -->
<div class="layer sheet-wrap" id="layer-settings">
  <div class="sheet">
    <div class="bar">
      <span></span><span class="t">Настройки</span>
      <button class="link bold" data-act="saveSettings">Готово</button>
    </div>
    <div class="field"><label for="s-uni">Начальный Universe</label><input id="s-uni" type="number" inputmode="numeric" min="1" max="999"></div>
    <div class="field"><label for="s-addr">Начальный адрес</label><input id="s-addr" type="number" inputmode="numeric" min="1" max="512"></div>
    <div class="err" id="s-err"></div>
    <button class="btn plain" data-act="resetQty">Обнулить все количества</button>
    <button class="btn danger" id="s-reset" data-act="resetLib">Сбросить библиотеку приборов</button>
  </div>
</div>

<script>
(function () {
'use strict';

/* ---------- Telegram / платформа ---------- */
const tg = (window.Telegram && window.Telegram.WebApp) || null;
const $ = id => document.getElementById(id);

function applyTheme() {
  let dark;
  if (tg && tg.colorScheme) dark = tg.colorScheme === 'dark';
  else dark = !!(window.matchMedia && matchMedia('(prefers-color-scheme: dark)').matches);
  document.documentElement.dataset.theme = dark ? 'dark' : 'light';
  const bg = dark ? '#000000' : '#F2F2F7';
  try { if (tg) { tg.setHeaderColor(bg); tg.setBackgroundColor(bg); } } catch (e) {}
}
function haptic(kind) {
  try {
    if (tg && tg.HapticFeedback) {
      if (kind === 'select') tg.HapticFeedback.selectionChanged();
      else tg.HapticFeedback.impactOccurred(kind || 'light');
    } else if (navigator.vibrate) navigator.vibrate(30);
  } catch (e) {}
}
if (tg) {
  try { tg.ready(); tg.expand(); if (tg.disableVerticalSwipes) tg.disableVerticalSwipes(); } catch (e) {}
  try { tg.onEvent('themeChanged', applyTheme); } catch (e) {}
}
applyTheme();
if (window.matchMedia) {
  try { matchMedia('(prefers-color-scheme: dark)').addEventListener('change', applyTheme); } catch (e) {}
}

/* ---------- Утилиты ---------- */
const esc = s => String(s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const clamp = (v, a, b) => Math.min(b, Math.max(a, v));
const uid = () => 'f' + Date.now().toString(36) + Math.random().toString(36).slice(2, 7);
const toInt = v => { const n = parseInt(v, 10); return isNaN(n) ? null : n; };

const KEY = 'dmxpro_v9';
const store = {
  mem: null,
  get() { try { return localStorage.getItem(KEY); } catch (e) { return this.mem; } },
  set(v) { this.mem = v; try { localStorage.setItem(KEY, v); } catch (e) {} }
};

/* ---------- Данные ---------- */
const DEFAULT_LIB = [
  ['Spots','Scenius Profile',[37],2000], ['Spots','Mythos',[30],750], ['Spots','Raptor',[18],500],
  ['Spots','Sharpy 330',[19],550], ['Spots','Azor SP2',[37],550], ['Spots','Arolla Profile',[39],550],
  ['Washes','K-20 B-EYE',[35,21],750], ['Washes','K-10 B-EYE',[35,21],500], ['Washes','Robe 1200',[21],600],
  ['Other','Stormy',[7],750], ['Other','SunRise',[4],400], ['Other','Blinder BIS',[2],200],
  ['Other','FOS 100',[10],300], ['Other','Hazer',[2],1500]
];
const MAX_FIXTURES = 100, MAX_QTY = 999, MAX_ROWS = 3000;

function defaultFixtures() {
  return DEFAULT_LIB.map(([cat, name, modes, w]) => ({ id: uid(), cat, name, w, modes: modes.slice(), mode: modes[0], qty: 0 }));
}
function sanitizeFixture(f) {
  if (!f || typeof f !== 'object') return null;
  const name = String(f.name || '').trim().slice(0, 40);
  if (!name) return null;
  const modes = [...new Set((Array.isArray(f.modes) ? f.modes : []).map(toInt).filter(n => n !== null && n >= 1 && n <= 512))].slice(0, 8);
  if (!modes.length) return null;
  const w = clamp(toInt(f.w) || 0, 0, 100000);
  const mode = modes.includes(toInt(f.mode)) ? toInt(f.mode) : modes[0];
  return {
    id: typeof f.id === 'string' && f.id ? f.id : uid(),
    cat: String(f.cat || 'Other').trim().slice(0, 24) || 'Other',
    name, w, modes, mode, qty: clamp(toInt(f.qty) || 0, 0, MAX_QTY)
  };
}
function load() {
  try {
    const raw = store.get();
    if (raw) {
      const s = JSON.parse(raw);
      if (s && Array.isArray(s.fixtures)) {
        const seen = new Set();
        const fixtures = s.fixtures.map(sanitizeFixture).filter(f => f && !seen.has(f.id) && seen.add(f.id)).slice(0, MAX_FIXTURES);
        const st = s.settings || {};
        return { fixtures, settings: { startUni: clamp(toInt(st.startUni) || 1, 1, 999), startAddr: clamp(toInt(st.startAddr) || 1, 1, 512) } };
      }
    }
  } catch (e) {}
  return { fixtures: defaultFixtures(), settings: { startUni: 1, startAddr: 1 } };
}
let state = load();
function save() { store.set(JSON.stringify(state)); }
const find = id => state.fixtures.find(f => f.id === id);

function groups() {
  const m = new Map();
  state.fixtures.forEach(f => { if (!m.has(f.cat)) m.set(f.cat, []); m.get(f.cat).push(f); });
  return m;
}

/* ---------- Расчёт патча ---------- */
let patch = [], totalW = 0, truncated = false;
function computePatch() {
  const res = [];
  truncated = false;
  let u = state.settings.startUni, a = state.settings.startAddr;
  outer:
  for (const items of groups().values()) {
    for (const f of items) {
      const ch = f.mode;
      for (let i = 1; i <= f.qty; i++) {
        if (res.length >= MAX_ROWS) { truncated = true; break outer; }
        if (a + ch - 1 > 512) { u++; a = 1; }  // прибор не делится между универсами
        res.push({ fid: f.id, name: f.name, i, u, a, ch });
        a += ch;
      }
    }
  }
  return res;
}

/* ---------- Прогресс адресации ---------- */
let progress = {}, history = [], sig = '';
function syncProgress() {
  const s = patch.map(p => p.fid + ':' + p.i + ':' + p.u + ':' + p.a).join('|');
  if (s !== sig) { sig = s; progress = {}; history = []; }
}

/* ---------- Рендер списка ---------- */
function cardHtml(f) {
  const modeHtml = f.modes.length > 1
    ? `<select class="mode-select" data-id="${f.id}" aria-label="Режим">${f.modes.map(m => `<option value="${m}"${m === f.mode ? ' selected' : ''}>${m} CH</option>`).join('')}</select>`
    : `<div class="mode-single">${f.modes[0]} CH</div>`;
  return `<div class="card" data-id="${f.id}">
    <div class="row">
      <div><div class="name">${esc(f.name)}</div><div class="meta">${f.w} Вт</div></div>
      <button class="icon-btn sm" data-act="edit" data-id="${f.id}" aria-label="Изменить">✎</button>
    </div>
    <div class="card-bottom">
      ${modeHtml}
      <div class="stepper">
        <button class="step-btn" data-act="dec" data-id="${f.id}" aria-label="Меньше">−</button>
        <input class="qty-input" type="number" inputmode="numeric" pattern="[0-9]*" min="0" max="${MAX_QTY}" value="${f.qty}" data-id="${f.id}" aria-label="Количество">
        <button class="step-btn" data-act="inc" data-id="${f.id}" aria-label="Больше">+</button>
      </div>
    </div>
  </div>`;
}
function renderList() {
  const root = $('fixture-list');
  if (!state.fixtures.length) { root.innerHTML = '<div class="empty">Библиотека пуста.<br>Добавьте первый прибор.</div>'; return; }
  let html = '';
  groups().forEach((items, cat) => {
    html += `<div class="cat">${esc(cat)}</div>` + items.map(cardHtml).join('');
  });
  root.innerHTML = html;
}

/* ---------- Результаты ---------- */
function renderResults() {
  const res = $('result-area');
  if (!patch.length) { res.innerHTML = ''; $('fabs').style.display = 'none'; return; }
  $('fabs').style.display = 'flex';
  const byU = new Map();
  patch.forEach(p => { if (!byU.has(p.u)) byU.set(p.u, []); byU.get(p.u).push(p); });
  let html = '';
  if (byU.size > 1) html += '<div class="note">Прибор не может делиться между универсами — не поместившиеся приборы перенесены в следующий Universe.</div>';
  [...byU.keys()].sort((a, b) => a - b).forEach(u => {
    const rows = byU.get(u);
    const end = Math.max(...rows.map(p => p.a + p.ch - 1));
    const pct = Math.min(100, end / 512 * 100);
    html += `<div class="u-head"><span>Universe ${u}</span><span>${end}/512</span></div>
      <div class="p-bar"><div class="p-bar-fill" style="width:${pct}%;background:${pct > 90 ? 'var(--red)' : 'var(--blue)'}"></div></div>
      <div class="plist">${rows.map(p => `<div class="prow"><span>${esc(p.name)} #${p.i}</span><span class="paddr"><b>${p.a}</b><small>–${p.a + p.ch - 1}</small></span></div>`).join('')}</div>`;
  });
  if (truncated) html += `<div class="note">Показаны первые ${MAX_ROWS} приборов.</div>`;
  html += '<button class="link-red" data-act="resetQty">Очистить все вычисления</button>';
  res.innerHTML = html;
}

/* ---------- Адресация ---------- */
function renderAddr() {
  const cur = history[0];
  $('c-name').textContent = cur ? `${cur.name} #${cur.i}` : 'ВЫБОР';
  $('c-addr').textContent = cur ? cur.a : '---';
  $('c-range').textContent = cur ? `${cur.a}–${cur.a + cur.ch - 1} · ${cur.ch} CH` : '';
  $('uni-info-box').innerHTML = cur ? `<span class="badge">UNIVERSE ${cur.u}</span>` : '';

  const box = $('c-btns');
  const ids = [...new Set(patch.map(p => p.fid))];
  if (!ids.length) box.innerHTML = '<div class="empty" style="grid-column:1/-1">Нет приборов</div>';
  else box.innerHTML = ids.map(fid => {
    const items = patch.filter(p => p.fid === fid);
    const done = progress[fid] || 0;
    const name = esc(items[0].name);
    if (done >= items.length) return `<button class="addr-btn" disabled><b>${name}</b><br><small>DONE</small></button>`;
    const last = done > 0 ? items[done - 1].a : '---';
    return `<button class="addr-btn" data-act="pick" data-id="${fid}"><b>${name} #${done + 1}</b><span class="last">LAST: ${last}</span></button>`;
  }).join('');

  $('history-content').innerHTML = history.slice(0, 5).map(i =>
    `<div class="hrow"><span>${esc(i.name)} #${i.i}</span><b>U${i.u} : ${i.a}</b></div>`).join('')
    || '<div style="color:var(--gray);font-size:14px;padding:6px 0">Пока пусто</div>';
}
function pick(fid) {
  const items = patch.filter(p => p.fid === fid);
  const done = progress[fid] || 0;
  if (done >= items.length) return;
  history.unshift(items[done]);
  progress[fid] = done + 1;
  haptic('medium');
  renderAddr();
}
function undo() {
  if (!history.length) return;
  const last = history.shift();
  progress[last.fid] = Math.max(0, (progress[last.fid] || 1) - 1);
  haptic('select');
  renderAddr();
}

/* ---------- Нагрузка ---------- */
function renderPwr() {
  const kw = totalW / 1000;
  const amps = Math.round(totalW / 230), perPhase = Math.round(totalW / 3 / 230);
  $('pwr-kw').textContent = kw.toFixed(1) + ' кВт';
  $('pwr-a').textContent = `${amps} А (230 В) · ≈${perPhase} А на фазу`;
  $('pwr-card').className = 'pwr-box ' + (kw > 35 ? 'pwr-red' : kw > 15 ? 'pwr-orange' : 'pwr-green');
  let h = '';
  if (totalW > 0) h += `<div class="info-card"><b>32A CEE:</b> ${Math.ceil(totalW / 15000)} шт</div>`;
  if (totalW > 15000) h += `<div class="info-card"><b>63A CEE:</b> ${Math.ceil(totalW / 35000)} шт</div>`;
  if (totalW > 35000) h += `<div class="info-card"><b>125A CEE:</b> ${Math.ceil(totalW / 70000)} шт</div>`;
  const used = state.fixtures.filter(f => f.qty > 0);
  if (used.length) {
    h += '<div class="info-card">' + used.map(f =>
      `<div class="brk"><span>${esc(f.name)} × ${f.qty}</span><span>${((f.qty * f.w) / 1000).toFixed(2)} кВт</span></div>`).join('') + '</div>';
  }
  $('pwr-recs').innerHTML = h;
}

/* ---------- Пересчёт ---------- */
function recompute() {
  patch = computePatch();
  totalW = state.fixtures.reduce((s, f) => s + f.qty * f.w, 0);
  syncProgress();
  renderResults();
  if (isOpen('addr')) renderAddr();
  if (isOpen('pwr')) renderPwr();
  save();
}

/* ---------- Слои (оверлеи) ---------- */
const stack = [];
const isOpen = id => stack.includes(id);
function syncChrome() {
  document.body.classList.toggle('locked', stack.length > 0);
  try {
    if (tg && tg.BackButton) stack.length ? tg.BackButton.show() : tg.BackButton.hide();
  } catch (e) {}
}
function openLayer(id) {
  if (isOpen(id)) return;
  stack.push(id);
  $('layer-' + id).classList.add('open');
  syncChrome();
}
function closeLayer(id) {
  const i = stack.indexOf(id);
  if (i < 0) return;
  stack.splice(i, 1);
  $('layer-' + id).classList.remove('open');
  if (document.activeElement && document.activeElement.blur) document.activeElement.blur();
  syncChrome();
}
function closeTop() { if (stack.length) closeLayer(stack[stack.length - 1]); }
try { if (tg && tg.BackButton) tg.BackButton.onClick(closeTop); } catch (e) {}
document.addEventListener('keydown', e => { if (e.key === 'Escape') closeTop(); });

/* ---------- Редактор прибора ---------- */
let editingId = null, delArmed = false, libArmed = false;
function resetArmed() {
  delArmed = false; libArmed = false;
  const d = $('e-del'); d.textContent = 'Удалить прибор'; d.classList.remove('armed');
  const r = $('s-reset'); r.textContent = 'Сбросить библиотеку приборов'; r.classList.remove('armed');
}
function openEdit(id) {
  const f = id ? find(id) : null;
  if (!id && state.fixtures.length >= MAX_FIXTURES) { alert('Достигнут лимит: ' + MAX_FIXTURES + ' приборов.'); return; }
  editingId = f ? f.id : null;
  $('e-title').textContent = f ? 'Изменить прибор' : 'Новый прибор';
  $('e-name').value = f ? f.name : '';
  $('e-cat').value = f ? f.cat : '';
  $('e-w').value = f ? f.w : '';
  $('e-modes').value = f ? f.modes.join(', ') : '';
  $('e-err').textContent = '';
  $('e-del').style.display = f ? 'block' : 'none';
  $('cat-list').innerHTML = [...groups().keys()].map(c => `<option value="${esc(c)}">`).join('');
  resetArmed();
  openLayer('edit');
}
function saveFixture() {
  const name = $('e-name').value.trim();
  const cat = $('e-cat').value.trim() || 'Other';
  const wRaw = $('e-w').value.trim();
  const w = wRaw === '' ? 0 : toInt(wRaw);
  const modes = [...new Set($('e-modes').value.split(/[,;\s]+/).filter(Boolean).map(toInt))];
  const err = m => { $('e-err').textContent = m; haptic('heavy'); };
  if (!name) return err('Введите название.');
  if (w === null || w < 0 || w > 100000) return err('Мощность: от 0 до 100000 Вт.');
  if (!modes.length || modes.some(m => m === null || m < 1 || m > 512)) return err('Режимы: числа от 1 до 512 через запятую.');
  if (modes.length > 8) return err('Не более 8 режимов.');
  const dup = state.fixtures.find(f => f.id !== editingId && f.name.toLowerCase() === name.toLowerCase());
  if (dup) return err('Прибор с таким названием уже есть.');

  if (editingId) {
    const f = find(editingId);
    if (!f) return closeLayer('edit');
    Object.assign(f, { name, cat: cat.slice(0, 24), w, modes });
    if (!modes.includes(f.mode)) f.mode = modes[0];
  } else {
    state.fixtures.push({ id: uid(), name, cat: cat.slice(0, 24), w, modes, mode: modes[0], qty: 0 });
  }
  haptic('light');
  closeLayer('edit');
  renderList();
  recompute();
}
function deleteFixture() {
  if (!editingId) return;
  if (!delArmed) {
    delArmed = true;
    const d = $('e-del'); d.textContent = 'Точно удалить? Нажмите ещё раз'; d.classList.add('armed');
    haptic('heavy');
    return;
  }
  state.fixtures = state.fixtures.filter(f => f.id !== editingId);
  editingId = null;
  closeLayer('edit');
  renderList();
  recompute();
}

/* ---------- Настройки ---------- */
function openSettings() {
  $('s-uni').value = state.settings.startUni;
  $('s-addr').value = state.settings.startAddr;
  $('s-err').textContent = '';
  resetArmed();
  openLayer('settings');
}
function saveSettings() {
  const u = toInt($('s-uni').value), a = toInt($('s-addr').value);
  if (u === null || u < 1 || u > 999) { $('s-err').textContent = 'Universe: от 1 до 999.'; return; }
  if (a === null || a < 1 || a > 512) { $('s-err').textContent = 'Адрес: от 1 до 512.'; return; }
  state.settings.startUni = u; state.settings.startAddr = a;
  closeLayer('settings');
  recompute();
}
function resetQty() {
  state.fixtures.forEach(f => f.qty = 0);
  progress = {}; history = [];
  renderList();
  recompute();
  closeLayer('settings');
}
function resetLib() {
  if (!libArmed) {
    libArmed = true;
    const r = $('s-reset'); r.textContent = 'Точно сбросить? Нажмите ещё раз'; r.classList.add('armed');
    haptic('heavy');
    return;
  }
  state = { fixtures: defaultFixtures(), settings: { startUni: 1, startAddr: 1 } };
  progress = {}; history = [];
  closeLayer('settings');
  renderList();
  recompute();
}

/* ---------- События ---------- */
function setQty(f, v, inputEl) {
  f.qty = clamp(v, 0, MAX_QTY);
  if (inputEl) inputEl.value = f.qty;
  recompute();
}
document.addEventListener('click', e => {
  const el = e.target.closest('[data-act]');
  if (!el) return;
  const act = el.dataset.act, id = el.dataset.id;
  switch (act) {
    case 'inc': case 'dec': {
      const f = find(id); if (!f) return;
      const inp = document.querySelector(`.qty-input[data-id="${id}"]`);
      setQty(f, f.qty + (act === 'inc' ? 1 : -1), inp);
      haptic('select');
      break;
    }
    case 'edit': openEdit(id); break;
    case 'add': openEdit(null); break;
    case 'saveFixture': saveFixture(); break;
    case 'deleteFixture': deleteFixture(); break;
    case 'settings': openSettings(); break;
    case 'saveSettings': saveSettings(); break;
    case 'resetQty': resetQty(); break;
    case 'resetLib': resetLib(); break;
    case 'openPwr': renderPwr(); openLayer('pwr'); break;
    case 'openAddr': renderAddr(); openLayer('addr'); break;
    case 'close': closeLayer(el.dataset.layer); break;
    case 'pick': pick(id); break;
    case 'undo': undo(); break;
    case 'resetProgress': progress = {}; history = []; renderAddr(); break;
  }
});
// тап по затемнению закрывает шторку
document.querySelectorAll('.sheet-wrap').forEach(w => w.addEventListener('click', e => {
  if (e.target === w) closeLayer(w.id.replace('layer-', ''));
}));
document.addEventListener('input', e => {
  const t = e.target;
  if (t.classList && t.classList.contains('qty-input')) {
    const f = find(t.dataset.id); if (!f) return;
    const v = toInt(t.value);
    f.qty = v === null ? 0 : clamp(v, 0, MAX_QTY);
    if (v !== null && v > MAX_QTY) t.value = MAX_QTY;
    recompute();
  }
});
document.addEventListener('change', e => {
  const t = e.target;
  if (t.classList.contains('qty-input')) { const f = find(t.dataset.id); if (f) t.value = f.qty; }
  else if (t.classList.contains('mode-select')) {
    const f = find(t.dataset.id); if (!f) return;
    const m = toInt(t.value);
    if (f.modes.includes(m)) { f.mode = m; haptic('select'); recompute(); }
  }
});
document.addEventListener('focusin', e => {
  if (e.target.classList && e.target.classList.contains('qty-input')) setTimeout(() => { try { e.target.select(); } catch (x) {} }, 0);
});
window.addEventListener('pagehide', save);
document.addEventListener('visibilitychange', () => { if (document.hidden) save(); });

/* ---------- Старт ---------- */
renderList();
recompute();
})();
</script>
</body>
</html>
