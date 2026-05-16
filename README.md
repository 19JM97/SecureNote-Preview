# SecureNote-Preview[SecureNote_v19_updated (1).html](https://github.com/user-attachments/files/27851780/SecureNote_v19_updated.1.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SecureNote</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=JetBrains+Mono:wght@300;400;500&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
/* ===== DARK MODE (default) — "Secure Workspace" palette ===== */
:root{
--bg:#111315;--surface:#1a1d21;--surface2:#22262b;--surface3:#2a2f36;
--border:#2e3440;--border2:#3d4657;
--gold:#d4a62a;--gold2:#e8c56a;--gold-dim:#7a5e18;
--text:#f1f1f1;--text2:#b7b7b7;--text3:#6e7280;
--danger:#c94c4c;--success:#4cc98a;--info:#4a8fc9;
--warn:#d4a62a;
--radius:10px;--radius-sm:6px;
--shadow:0 4px 24px rgba(0,0,0,.5);
--img-border:#2e3440;
}
/* ===== LIGHT MODE ===== */
:root.light{
--bg:#f5f3ee;--surface:#ffffff;--surface2:#f0ede6;--surface3:#e8e4dc;
--border:#ddd8ce;--border2:#c8c2b6;
--gold:#b8922a;--gold2:#c9a84c;--gold-dim:#8a6b1e;
--text:#1a1714;--text2:#4a4440;--text3:#8a8480;
--danger:#c94c4c;--success:#2e9e6a;--info:#2e6ea8;
--warn:#b8922a;
--shadow:0 4px 24px rgba(0,0,0,.1);
--img-border:#ddd8ce;
}
/* Auto-detect system preference (overridden by manual toggle) */
@media(prefers-color-scheme:light){
  :root:not(.dark){
    --bg:#f5f3ee;--surface:#ffffff;--surface2:#f0ede6;--surface3:#e8e4dc;
    --border:#ddd8ce;--border2:#c8c2b6;
    --gold:#b8922a;--gold2:#c9a84c;--gold-dim:#8a6b1e;
    --text:#1a1714;--text2:#4a4440;--text3:#8a8480;
    --danger:#c94c4c;--success:#2e9e6a;--info:#2e6ea8;
    --warn:#b8922a;
    --shadow:0 4px 24px rgba(0,0,0,.1);
    --img-border:#ddd8ce;
  }
}
*{margin:0;padding:0;box-sizing:border-box;}
html,body{height:100%;overflow:hidden;}
body{
background:var(--bg);color:var(--text);
font-family:'Inter','DM Sans',sans-serif;font-size:16px;
}
/* THEME TRANSITION */
*{transition:background-color .25s ease,border-color .25s ease,color .15s ease;}
input,textarea,button{transition:background-color .25s ease,border-color .25s ease,color .15s ease,transform .1s ease,opacity .2s ease;}
/* SCREENSHOT/PRINT BLOCK */
@media print{body{display:none!important;}}
body::before{
content:'';position:fixed;inset:0;pointer-events:none;z-index:99999;
}

/* GRAIN */
body::after{
content:'';position:fixed;inset:0;pointer-events:none;z-index:9998;
background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
opacity:.6;
}

/* GRAIN - lighter in light mode */
:root.light body::after,:root:not(.dark) body::after{opacity:.2;}

/* THEME TOGGLE BUTTON */
.theme-toggle{
background:none;border:1px solid var(--border);border-radius:20px;
padding:4px 10px;cursor:pointer;font-size:12px;color:var(--text2);
display:flex;align-items:center;gap:5px;transition:all .2s;
font-family:'DM Sans',sans-serif;
}
.theme-toggle:hover{border-color:var(--gold-dim);color:var(--gold);}
.theme-toggle svg{width:13px;height:13px;stroke:currentColor;fill:none;stroke-width:2;}

/* THEME BUTTON 3-STATE ICONS */
#theme-btn{position:relative;overflow:visible;}
#theme-btn .theme-icon-wrap{
  display:flex;align-items:center;justify-content:center;
  transition:transform .35s cubic-bezier(.34,1.56,.64,1),opacity .25s ease;
}
@keyframes theme-spin-in{
  from{transform:rotate(-90deg) scale(.5);opacity:0;}
  to{transform:rotate(0deg) scale(1);opacity:1;}
}
@keyframes theme-spin-out{
  from{transform:rotate(0deg) scale(1);opacity:1;}
  to{transform:rotate(90deg) scale(.5);opacity:0;}
}
#theme-btn.animating .theme-icon-wrap{animation:theme-spin-in .35s cubic-bezier(.34,1.56,.64,1) forwards;}
/* Theme state indicator dot */
#theme-btn::after{
  content:'';position:absolute;bottom:4px;right:4px;
  width:5px;height:5px;border-radius:50%;
  background:var(--gold);opacity:0;transition:opacity .3s;
}
#theme-btn.theme-auto::after{background:#4a8fc9;opacity:1;}
#theme-btn.theme-light::after{background:var(--gold2);opacity:1;}
#theme-btn.theme-dark::after{background:var(--text3);opacity:1;}

/* ACCOUNT SETTINGS MODAL */
.acct-section{
  background:var(--surface2);border-radius:var(--radius-sm);
  padding:16px;margin-bottom:16px;border:1px solid var(--border);
}
.acct-section-title{
  font-size:11px;font-weight:600;color:var(--text3);letter-spacing:.6px;
  text-transform:uppercase;margin-bottom:12px;
}
.acct-input-group{display:flex;flex-direction:column;gap:10px;}
.acct-input-row{display:flex;flex-direction:column;gap:4px;}
.acct-input-row label{font-size:11px;color:var(--text3);font-weight:500;letter-spacing:.4px;text-transform:uppercase;}
.acct-input-row input{
  background:var(--surface);border:1px solid var(--border);
  border-radius:var(--radius-sm);padding:8px 12px;
  color:var(--text);font-family:'DM Sans',sans-serif;font-size:13px;outline:none;
  transition:border-color .2s;
}
.acct-input-row input:focus{border-color:var(--gold-dim);}
.acct-save-btn{
  padding:8px 16px;background:rgba(201,168,76,.15);border:1px solid var(--gold-dim);
  border-radius:var(--radius-sm);color:var(--gold);font-size:12px;font-weight:500;
  cursor:pointer;font-family:'DM Sans',sans-serif;transition:.2s;margin-top:4px;
  letter-spacing:.2px;
}
.acct-save-btn:hover{background:rgba(201,168,76,.25);}
#acct-alert{margin-bottom:0;margin-top:10px;}

/* SCREENS */
.screen{
position:fixed;inset:0;display:flex;align-items:center;justify-content:center;
transition:opacity .4s ease,transform .4s ease;
}
.screen.hidden{opacity:0;pointer-events:none;transform:translateY(16px);}

/* CARD */
.card{
background:var(--surface);border:1px solid var(--border);
border-radius:16px;padding:40px;width:420px;
}
.card-logo{
font-family:'Playfair Display',serif;font-size:28px;font-weight:600;
color:var(--gold);letter-spacing:-0.5px;margin-bottom:6px;text-align:center;
}
.card-sub{font-size:13px;color:var(--text2);text-align:center;margin-bottom:32px;}

/* FORM ELEMENTS */
label{font-size:12px;font-weight:500;color:var(--text2);letter-spacing:.5px;text-transform:uppercase;display:block;margin-bottom:6px;}
input[type=text],input[type=password],input[type=number]{
width:100%;background:var(--surface2);border:1px solid var(--border);
border-radius:var(--radius-sm);padding:11px 14px;color:var(--text);
font-family:'Inter','DM Sans',sans-serif;font-size:14px;outline:none;
transition:border-color .2s,background .2s;
}
input[type=text]:focus,input[type=password]:focus,input[type=number]:focus{border-color:var(--gold-dim);background:var(--surface3);}
.form-group{margin-bottom:20px;}

/* BUTTONS */
.btn{
width:100%;padding:12px;border:none;border-radius:var(--radius-sm);
font-family:'Inter','DM Sans',sans-serif;font-size:15px;font-weight:500;
cursor:pointer;transition:all .2s;letter-spacing:.2px;
}
.btn-gold{background:var(--gold);color:#1a1200;}
.btn-gold:hover{background:var(--gold2);transform:translateY(-1px);}
.btn-outline{background:transparent;border:1px solid var(--border);color:var(--text2);}
.btn-outline:hover{border-color:var(--border2);color:var(--text);transform:translateY(-1px);}
.btn:active{transform:scale(.98);}
.btn:disabled{opacity:.4;cursor:not-allowed;}

/* ALERT */
.alert{
padding:10px 14px;border-radius:var(--radius-sm);font-size:13px;margin-bottom:16px;display:none;
}
.alert.danger{background:rgba(201,76,76,.15);border:1px solid rgba(201,76,76,.3);color:#f08080;}
.alert.success{background:rgba(76,201,138,.15);border:1px solid rgba(76,201,138,.3);color:#70e0a8;}
.alert.warn{background:rgba(201,168,76,.15);border:1px solid rgba(201,168,76,.3);color:var(--gold2);}
.alert.show{display:block;}

/* DIVIDER */
.divider{display:flex;align-items:center;gap:12px;margin:20px 0;}
.divider::before,.divider::after{content:'';flex:1;height:1px;background:var(--border);}
.divider span{font-size:12px;color:var(--text3);}

/* LOCK ICON */
.lock-icon{
width:56px;height:56px;background:rgba(201,168,76,.1);border:1px solid var(--gold-dim);
border-radius:50%;display:flex;align-items:center;justify-content:center;
margin:0 auto 20px;
}
.lock-icon svg{width:24px;height:24px;stroke:var(--gold);fill:none;stroke-width:1.8;}

/* SETUP STEPS */
.steps{display:flex;gap:8px;margin-bottom:28px;justify-content:center;}
.step{width:28px;height:4px;border-radius:2px;background:var(--border);transition:.3s;}
.step.active{background:var(--gold);}
.step.done{background:var(--gold-dim);}

/* DIRECTORY SELECT */
.dir-box{
background:var(--surface2);border:1px dashed var(--border2);border-radius:var(--radius-sm);
padding:16px;text-align:center;cursor:pointer;transition:.2s;margin-bottom:18px;
}
.dir-box:hover{border-color:var(--gold-dim);background:var(--surface3);}
.dir-box svg{width:28px;height:28px;stroke:var(--text3);fill:none;stroke-width:1.5;margin-bottom:8px;}
.dir-box.selected svg{stroke:var(--gold);}
.dir-box.selected{border-color:var(--gold-dim);border-style:solid;}
.dir-name{font-size:13px;font-weight:500;color:var(--text2);}
.dir-box.selected .dir-name{color:var(--gold);}

/* ===== MAIN APP ===== */
#app-screen{display:none;flex-direction:row;}
#app-screen.active{display:flex;}

/* SIDEBAR — full width, no editor beside it */
.sidebar{
width:100%;min-width:0;height:100vh;background:var(--surface);
border-right:none;display:flex;flex-direction:column;
max-width:100%;overflow-x:hidden;
}
.sidebar-header{
padding:16px 14px 12px;border-bottom:1px solid var(--border);
display:flex;align-items:center;justify-content:space-between;
min-width:0;gap:8px;
}
.sidebar-header>div:first-child{
  min-width:0;flex:1;overflow:hidden;
}
.sidebar-header>div:last-child{
  flex-shrink:0;display:flex;gap:4px;
}
.sidebar-logo{
font-family:'Playfair Display',serif;font-size:20px;color:var(--gold);font-weight:600;
}
.sidebar-user{font-size:12px;color:var(--text3);margin-top:3px;}
.icon-btn{
background:none;border:none;cursor:pointer;color:var(--text2);
width:36px;height:36px;display:flex;align-items:center;justify-content:center;
border-radius:var(--radius-sm);transition:all .2s;
}
.icon-btn:hover{background:var(--surface3);color:var(--text);transform:translateY(-1px);}
.icon-btn:active{transform:scale(.95);}
.icon-btn svg{width:18px;height:18px;stroke:currentColor;fill:none;stroke-width:1.8;}

/* SEARCH */
.search-wrap{padding:12px 12px 8px;border-bottom:1px solid var(--border);}
.search-input{
width:100%;background:var(--surface2);border:1px solid var(--border);
border-radius:var(--radius-sm);padding:9px 12px 9px 34px;
color:var(--text);font-family:'Inter','DM Sans',sans-serif;font-size:14px;outline:none;
transition:.2s;position:relative;
}
.search-input::placeholder{color:var(--text3);}
.search-input:focus{border-color:var(--gold-dim);background:var(--surface3);}
.search-wrap-inner{position:relative;}
.search-wrap-inner svg{
position:absolute;left:10px;top:50%;transform:translateY(-50%);
width:16px;height:16px;stroke:var(--text3);fill:none;stroke-width:1.8;
pointer-events:none;
}

/* NOTE LIST */
.note-list{flex:1;overflow-y:auto;padding:8px 8px;}
.note-list::-webkit-scrollbar{width:4px;}
.note-list::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px;}
.note-item{
padding:12px 14px;border-radius:8px;cursor:pointer;margin-bottom:3px;
border:1px solid transparent;transition:all .15s;
}
.note-item:hover{background:var(--surface2);transform:translateX(2px);}
.note-item.active{background:var(--surface2);border-color:var(--border);}
.note-item-title{
font-size:14px;font-weight:500;color:var(--text);
white-space:nowrap;overflow:hidden;text-overflow:ellipsis;margin-bottom:4px;
}
.note-item-preview{
font-size:12px;color:var(--text2);
white-space:nowrap;overflow:hidden;text-overflow:ellipsis;
}
.note-item-date{font-size:11px;color:var(--text3);margin-top:4px;}
.note-item.active .note-item-title{color:var(--gold);}
.note-item .enc-badge{font-size:10px;color:var(--gold-dim);margin-left:4px;}
.empty-notes{padding:32px 12px;text-align:center;color:var(--text3);font-size:14px;}

/* NEW NOTE BTN */
.new-btn{
margin:8px;padding:10px;background:rgba(212,166,42,.12);border:1px solid var(--gold-dim);
border-radius:var(--radius-sm);color:var(--gold);font-size:14px;font-weight:500;
cursor:pointer;display:flex;align-items:center;justify-content:center;gap:6px;transition:all .2s;
font-family:'Inter','DM Sans',sans-serif;overflow:hidden;min-width:0;
}
.new-btn:hover{background:rgba(212,166,42,.22);transform:translateY(-1px);}
.new-btn svg{width:16px;height:16px;stroke:currentColor;fill:none;stroke-width:2;}

/* SIDEBAR FOOTER */
.sidebar-footer{
padding:10px 14px;border-top:1px solid var(--border);
display:flex;flex-direction:column;gap:4px;overflow:hidden;
}
.storage-info{font-size:12px;color:var(--text2);}
.storage-dot{
display:inline-block;width:7px;height:7px;border-radius:50%;background:var(--success);margin-right:5px;
}
.usb-indicator{font-size:11px;display:flex;align-items:center;gap:4px;}
.usb-indicator.disconnected{color:var(--danger);}
.usb-indicator.connected{color:var(--success);}
.credit{font-size:11px;color:var(--text3);text-align:center;padding:4px 0;border-top:1px solid var(--border);margin-top:2px;letter-spacing:.5px;}
.credit span{color:var(--gold-dim);font-weight:600;}

/* EDITOR */
.editor{flex:1;display:flex;flex-direction:column;height:100vh;}
.editor-bar{
padding:16px 24px;border-bottom:1px solid var(--border);
display:flex;align-items:center;gap:10px;background:var(--surface);
backdrop-filter:blur(10px);
}
.editor-title{
flex:1;background:none;border:none;color:var(--text);
font-family:'Playfair Display',serif;font-size:24px;outline:none;
font-weight:600;
}
.editor-title::placeholder{color:var(--text3);}
.save-status{font-size:12px;color:var(--text3);white-space:nowrap;}
.save-status.saved{color:var(--success);}
.save-status.unsaved{color:var(--gold);}
.editor-meta{
padding:9px 24px;font-size:12px;color:var(--text2);
background:var(--surface);border-bottom:1px solid var(--border);
display:flex;gap:16px;
}
/* EDITOR BODY */
.editor-body{
flex:1;overflow-y:auto;background:var(--bg);
display:flex;flex-direction:column;
}
.editor-body::-webkit-scrollbar{width:6px;}
.editor-body::-webkit-scrollbar-thumb{background:var(--border2);border-radius:3px;}
textarea#note-content{
flex:1;min-height:200px;padding:28px 36px;
background:none;border:none;outline:none;resize:none;
color:var(--text);font-family:'JetBrains Mono',monospace;font-size:15px;
line-height:1.85;
}
textarea#note-content::placeholder{color:var(--text3);}

/* EMPTY STATE */
.editor-empty{
flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;
gap:12px;color:var(--text3);background:var(--bg);
}
.editor-empty svg{width:48px;height:48px;stroke:var(--border2);fill:none;stroke-width:1.2;}
.editor-empty p{font-size:14px;}
.editor-empty small{font-size:12px;}

/* MODAL */
.modal-overlay{
position:fixed;inset:0;background:rgba(0,0,0,.7);
display:flex;align-items:center;justify-content:center;z-index:5000;
transition:.2s;
}
.modal-overlay.hidden{opacity:0;pointer-events:none;}
.modal{
background:var(--surface);border:1px solid var(--border);border-radius:14px;
padding:28px;width:360px;
}
.modal h3{font-size:16px;font-weight:600;margin-bottom:8px;}
.modal p{font-size:13px;color:var(--text2);margin-bottom:20px;}
.modal-btns{display:flex;gap:10px;}
.modal-btns .btn{padding:9px;}

/* ===== LOCK / UNLOCK ANIMATIONS ===== */
@keyframes lockFade{
  0%{opacity:1;transform:scale(1);}
  100%{opacity:0;transform:scale(0.95);}
}
@keyframes unlockZoom{
  0%{opacity:0;transform:scale(1.05);}
  100%{opacity:1;transform:scale(1);}
}
.lock-animation{animation:lockFade 0.4s ease forwards;}
.unlock-animation{animation:unlockZoom 0.4s ease forwards;}

/* ===== NOTE LOCKED BLUR ===== */
.note-item-preview.is-locked{
  filter:blur(4px);
  user-select:none;
  pointer-events:none;
  opacity:0.6;
}
.note-locked-badge{
  font-size:11px;
  margin-left:4px;
  vertical-align:middle;
}

/* TOAST */
.toast{
position:fixed;bottom:24px;right:24px;background:var(--surface2);border:1px solid var(--border);
padding:12px 18px;border-radius:var(--radius-sm);font-size:14px;color:var(--text);
z-index:2000;transition:.3s;opacity:0;transform:translateY(8px);max-width:340px;
backdrop-filter:blur(10px);box-shadow:var(--shadow);
}
.toast.show{opacity:1;transform:translateY(0);}
.toast.danger{border-color:rgba(201,76,76,.4);color:#f08080;}
.toast.warn{border-color:rgba(212,166,42,.4);color:var(--gold2);}

/* WORD COUNT BAR */
.editor-toolbar{
padding:8px 24px;background:var(--surface);border-top:1px solid var(--border);
display:flex;align-items:center;gap:16px;justify-content:space-between;
}
.wc{font-size:12px;color:var(--text2);}

/* SCROLLBAR */
.note-list::-webkit-scrollbar-track{background:transparent;}

/* SECURITY BADGE ROW */
.sec-badges{
display:flex;flex-wrap:wrap;gap:4px;padding:6px 10px;
border-bottom:1px solid var(--border);background:var(--surface);
overflow:hidden;
}
.sec-badge{
font-size:10px;padding:2px 6px;border-radius:3px;letter-spacing:.2px;font-weight:600;
background:rgba(212,166,42,.1);border:1px solid rgba(212,166,42,.2);color:var(--gold-dim);
white-space:nowrap;
}
.sec-badge.active{background:rgba(76,201,138,.1);border-color:rgba(76,201,138,.2);color:var(--success);}

/* AUDIT LOG MODAL */
.audit-list{
max-height:280px;overflow-y:auto;font-family:'JetBrains Mono',monospace;
font-size:12px;line-height:1.7;color:var(--text2);
background:var(--surface2);border-radius:var(--radius-sm);padding:12px;
border:1px solid var(--border);
}
.audit-entry{padding:2px 0;border-bottom:1px solid rgba(255,255,255,.03);}
.audit-entry.fail{color:#f08080;}
.audit-entry.ok{color:var(--success);}

/* SETTINGS PANEL */
.settings-row{
display:flex;align-items:center;justify-content:space-between;
padding:12px 0;border-bottom:1px solid var(--border);
}
.settings-row:last-child{border-bottom:none;}
.settings-label{font-size:14px;color:var(--text);}
.settings-label small{display:block;font-size:12px;color:var(--text3);margin-top:2px;}
.toggle{
width:36px;height:20px;background:var(--border2);border-radius:10px;
cursor:pointer;position:relative;transition:.2s;border:none;
}
.toggle.on{background:var(--gold-dim);}
.toggle::after{
content:'';position:absolute;top:3px;left:3px;width:14px;height:14px;
border-radius:50%;background:#fff;transition:.2s;
}
.toggle.on::after{left:19px;}
.small-input{
width:60px;background:var(--surface2);border:1px solid var(--border);
border-radius:4px;padding:4px 8px;color:var(--text);
font-family:'Inter','DM Sans',sans-serif;font-size:13px;outline:none;text-align:center;
}

/* PIN dots */
.pin-dots{display:flex;gap:8px;justify-content:center;margin:16px 0;}
.pin-dot{width:12px;height:12px;border-radius:50%;background:var(--border2);transition:.2s;}
.pin-dot.filled{background:var(--gold);}

/* LOCK OVERLAY */
#lock-overlay{
position:fixed;inset:0;background:rgba(17,19,21,.97);z-index:9000;
display:flex;align-items:center;justify-content:center;
transition:.3s;
}
#lock-overlay.hidden{opacity:0;pointer-events:none;}

/* EXPORT badge */
.hmac-ok{color:var(--success);font-size:10px;margin-left:6px;}
.hmac-fail{color:var(--danger);font-size:10px;margin-left:6px;}

/* CLIPBOARD TIMER */
.clip-timer{
position:fixed;top:12px;right:16px;font-size:11px;color:var(--gold);
background:var(--surface2);border:1px solid var(--gold-dim);
padding:4px 10px;border-radius:4px;z-index:8000;display:none;
}
/* ===== IMAGE GALLERY ===== */
.img-gallery{
display:flex;flex-wrap:wrap;gap:10px;padding:0 28px 16px;
}
.img-thumb-wrap{
position:relative;border-radius:8px;overflow:hidden;
border:1px solid var(--img-border);cursor:pointer;
transition:transform .15s,box-shadow .15s;
}
.img-thumb-wrap:hover{transform:translateY(-2px);box-shadow:0 6px 20px rgba(0,0,0,.25);}
.img-thumb{
width:120px;height:90px;object-fit:cover;display:block;
}
.img-thumb-del{
position:absolute;top:4px;right:4px;
background:rgba(201,76,76,.85);border:none;border-radius:50%;
width:20px;height:20px;cursor:pointer;color:#fff;font-size:11px;
display:flex;align-items:center;justify-content:center;
opacity:0;transition:.15s;
}
.img-thumb-wrap:hover .img-thumb-del{opacity:1;}

/* IMAGE DROP ZONE */
.img-dropzone{
border:1.5px dashed var(--border2);border-radius:8px;
padding:12px 20px;margin:0 28px 12px;
display:flex;align-items:center;gap:10px;cursor:pointer;
font-size:12px;color:var(--text3);transition:.2s;
}
.img-dropzone:hover,.img-dropzone.dragover{
border-color:var(--gold-dim);color:var(--gold);background:rgba(201,168,76,.05);
}
.img-dropzone svg{width:18px;height:18px;stroke:currentColor;fill:none;stroke-width:1.8;flex-shrink:0;}

/* IMAGE LIGHTBOX */
#img-lightbox{
position:fixed;inset:0;background:rgba(0,0,0,.92);
z-index:10000;display:flex;align-items:center;justify-content:center;
}
#img-lightbox.hidden{display:none;}
#img-lightbox img{
max-width:90vw;max-height:88vh;border-radius:8px;
box-shadow:0 8px 48px rgba(0,0,0,.6);
}
.lb-close{
position:absolute;top:16px;right:20px;
background:rgba(255,255,255,.12);border:none;border-radius:50%;
width:36px;height:36px;cursor:pointer;color:#fff;font-size:20px;
display:flex;align-items:center;justify-content:center;
}
.lb-close:hover{background:rgba(255,255,255,.22);}
.lb-info{
position:absolute;bottom:16px;left:50%;transform:translateX(-50%);
font-size:12px;color:rgba(255,255,255,.5);
}

/* PASTE IMAGE HINT */
.paste-hint{
font-size:11px;color:var(--text3);padding:0 28px 8px;
display:flex;align-items:center;gap:6px;
}
.paste-hint kbd{
background:var(--surface2);border:1px solid var(--border);
border-radius:3px;padding:1px 5px;font-size:10px;font-family:'JetBrains Mono',monospace;
}

/* ===== PASSWORD STRENGTH METER ===== */
.pw-strength-wrap{margin-top:6px;}
.pw-strength-bar{height:3px;border-radius:2px;background:var(--border);overflow:hidden;margin-bottom:4px;}
.pw-strength-fill{height:100%;width:0%;transition:width .3s,background .3s;border-radius:2px;}
.pw-strength-label{font-size:10px;color:var(--text3);letter-spacing:.3px;}

/* ===== SESSION TIMEOUT BANNER ===== */
#session-warn{
position:fixed;top:0;left:0;right:0;z-index:8500;
background:rgba(201,168,76,.95);color:#1a1200;
padding:10px 20px;font-size:13px;font-weight:500;
display:flex;align-items:center;justify-content:center;gap:12px;
transform:translateY(-100%);transition:transform .3s;
}
#session-warn.show{transform:translateY(0);}
#session-warn-count{font-weight:700;font-size:15px;}
#session-warn-extend{
background:rgba(0,0,0,.15);border:1px solid rgba(0,0,0,.2);
border-radius:4px;padding:3px 10px;cursor:pointer;font-size:12px;font-weight:600;
color:#1a1200;font-family:'DM Sans',sans-serif;
}

/* ===== NOTE LOCK ===== */
.note-locked-badge{
display:inline-flex;align-items:center;gap:4px;
font-size:9px;padding:2px 6px;border-radius:3px;
background:rgba(74,143,201,.1);border:1px solid rgba(74,143,201,.25);
color:var(--info);margin-left:6px;vertical-align:middle;
}
.note-lock-overlay{
position:absolute;inset:0;background:rgba(17,19,21,.93);
backdrop-filter:blur(12px);
display:flex;flex-direction:column;align-items:center;justify-content:center;
gap:12px;z-index:200;
}
.note-lock-overlay.hidden{display:none;}
#editor-body-wrap{position:relative;}

/* ===== TAGS ===== */
.tags-wrap{
padding:8px 24px 8px;display:flex;flex-wrap:wrap;align-items:center;gap:6px;
background:var(--surface);border-bottom:1px solid var(--border);
}
.tag-chip{
display:inline-flex;align-items:center;gap:4px;
background:rgba(212,166,42,.12);border:1px solid rgba(212,166,42,.25);
border-radius:20px;padding:2px 8px 2px 8px;font-size:12px;color:var(--gold);
}
.tag-chip-del{
background:none;border:none;cursor:pointer;color:var(--gold-dim);
font-size:12px;line-height:1;padding:0;margin-left:2px;
}
.tag-input{
background:none;border:none;outline:none;color:var(--text2);
font-family:'Inter','DM Sans',sans-serif;font-size:12px;
min-width:80px;max-width:120px;
}
.tag-input::placeholder{color:var(--text3);}
.note-item-tags{display:flex;gap:3px;flex-wrap:wrap;margin-top:4px;}
.note-tag-mini{
font-size:10px;padding:1px 6px;border-radius:10px;
background:rgba(212,166,42,.1);color:var(--gold-dim);
border:1px solid rgba(212,166,42,.15);
}
.tag-filter-wrap{
padding:4px 8px;display:flex;gap:4px;flex-wrap:wrap;align-items:center;
border-bottom:1px solid var(--border);background:var(--surface);
}
.tag-filter-chip{
font-size:11px;padding:2px 8px;border-radius:10px;
background:var(--surface2);border:1px solid var(--border);
color:var(--text2);cursor:pointer;transition:.15s;
font-family:'Inter','DM Sans',sans-serif;
}
.tag-filter-chip.active{background:rgba(212,166,42,.15);border-color:var(--gold-dim);color:var(--gold);}
.tag-filter-label{font-size:11px;color:var(--text3);margin-right:2px;}

/* ===== PIN BADGE on note list ===== */
.note-item-pin{
font-size:11px;margin-right:4px;vertical-align:middle;
}
.note-item.pinned .note-item-title{color:var(--gold);}

/* ===== MARKDOWN PREVIEW ===== */
.md-preview{
flex:1;padding:28px 36px;overflow-y:auto;
color:var(--text);font-family:'Inter','DM Sans',sans-serif;
font-size:var(--editor-font-size,15px);line-height:1.85;
}
.md-preview h1{font-family:'Playfair Display',serif;font-size:1.8em;font-weight:600;color:var(--gold);margin-bottom:12px;margin-top:8px;border-bottom:1px solid var(--border);padding-bottom:8px;}
.md-preview h2{font-family:'Playfair Display',serif;font-size:1.4em;font-weight:600;color:var(--gold2);margin:16px 0 8px;}
.md-preview h3{font-size:1.1em;font-weight:600;color:var(--text);margin:12px 0 6px;}
.md-preview strong{font-weight:700;color:var(--text);}
.md-preview em{font-style:italic;color:var(--text2);}
.md-preview code{font-family:'JetBrains Mono',monospace;font-size:.85em;background:var(--surface2);padding:1px 5px;border-radius:3px;border:1px solid var(--border);}
.md-preview pre{background:var(--surface2);border:1px solid var(--border);border-radius:8px;padding:14px;overflow-x:auto;margin:10px 0;}
.md-preview pre code{background:none;border:none;padding:0;}
.md-preview ul,.md-preview ol{padding-left:20px;margin:8px 0;}
.md-preview li{margin-bottom:3px;}
.md-preview blockquote{border-left:3px solid var(--gold-dim);margin:10px 0;padding:6px 14px;color:var(--text2);background:var(--surface2);border-radius:0 4px 4px 0;}
.md-preview hr{border:none;border-top:1px solid var(--border);margin:16px 0;}
.md-preview a{color:var(--info);text-decoration:underline;}
.md-preview p{margin-bottom:8px;}
.md-preview table{border-collapse:collapse;width:100%;margin:10px 0;}
.md-preview th,.md-preview td{border:1px solid var(--border);padding:6px 10px;font-size:13px;}
.md-preview th{background:var(--surface2);font-weight:600;}
.md-toggle-btn{
font-size:10px;padding:2px 8px;border-radius:10px;
border:1px solid var(--border);background:var(--surface2);
color:var(--text3);cursor:pointer;font-family:'DM Sans',sans-serif;
transition:.15s;white-space:nowrap;
}
.md-toggle-btn.on{border-color:var(--gold-dim);color:var(--gold);background:rgba(201,168,76,.1);}

/* ===== EDITOR FONT SIZE ===== */
textarea#note-content{font-size:var(--editor-font-size,14px);}

/* ===== FIND & REPLACE ===== */
#find-replace-bar{
background:var(--surface);border-bottom:1px solid var(--border);
padding:8px 16px;display:flex;align-items:center;gap:8px;
}
#find-replace-bar.hidden{display:none;}
#find-replace-bar input{
background:var(--surface2);border:1px solid var(--border);
border-radius:var(--radius-sm);padding:5px 10px;color:var(--text);
font-family:'DM Sans',sans-serif;font-size:12px;outline:none;width:140px;
}
#find-replace-bar input:focus{border-color:var(--gold-dim);}
.fr-btn{
padding:4px 10px;font-size:11px;border-radius:var(--radius-sm);
border:1px solid var(--border);background:var(--surface2);
color:var(--text2);cursor:pointer;font-family:'DM Sans',sans-serif;transition:.15s;
}
.fr-btn:hover{border-color:var(--gold-dim);color:var(--gold);}
.fr-info{font-size:10px;color:var(--text3);min-width:50px;}
#fr-close{background:none;border:none;color:var(--text3);cursor:pointer;font-size:16px;padding:0 4px;}

/* ===== APPEARANCE SETTINGS ===== */
.color-swatches{display:flex;gap:6px;flex-wrap:wrap;margin-top:6px;}
.color-swatch{
width:22px;height:22px;border-radius:50%;cursor:pointer;
border:2px solid transparent;transition:.15s;
}
.color-swatch.active{border-color:var(--text);transform:scale(1.2);}
.font-slider-wrap{display:flex;align-items:center;gap:10px;}
.font-slider{
-webkit-appearance:none;height:3px;background:var(--border2);
border-radius:2px;outline:none;cursor:pointer;flex:1;
accent-color:var(--gold);
}
.view-toggle-wrap{display:flex;gap:6px;}
.view-toggle-btn{
padding:5px 12px;font-size:11px;border-radius:var(--radius-sm);
border:1px solid var(--border);background:var(--surface2);
color:var(--text3);cursor:pointer;font-family:'DM Sans',sans-serif;transition:.15s;
}
.view-toggle-btn.active{border-color:var(--gold-dim);color:var(--gold);background:rgba(201,168,76,.1);}

/* COMPACT VIEW */
body.compact-view .note-item{padding:6px 10px;margin-bottom:1px;}
body.compact-view .note-item-preview{display:none;}
body.compact-view .note-item-date{font-size:9px;}

/* NOTE-LEVEL LOCK MODAL */
#note-pass-modal .modal{width:380px;}

/* ===== NOTE COLOR LABELS ===== */
.note-item{border-left:3px solid transparent;}
.note-item.color-red{border-left-color:#c94c4c;}
.note-item.color-orange{border-left-color:#c97a4c;}
.note-item.color-yellow{border-left-color:#c9a84c;}
.note-item.color-green{border-left-color:#4cc98a;}
.note-item.color-blue{border-left-color:#4a8fc9;}
.note-item.color-purple{border-left-color:#9a4cc9;}
.color-picker-wrap{display:flex;gap:6px;align-items:center;margin-left:4px;}
.note-color-dot{width:14px;height:14px;border-radius:50%;cursor:pointer;border:2px solid transparent;transition:.15s;flex-shrink:0;}
.note-color-dot:hover,.note-color-dot.active{border-color:var(--text);transform:scale(1.25);}
.note-color-dot.none{background:var(--border2);border-style:dashed;}

/* ===== TRASH ===== */
.trash-section{padding:4px 8px;border-bottom:1px solid var(--border);background:var(--surface);}
.trash-btn{
  width:100%;padding:8px 12px;background:none;border:1px solid var(--border);
  border-radius:var(--radius-sm);color:var(--text2);font-size:13px;
  cursor:pointer;display:flex;align-items:center;gap:6px;transition:all .15s;
  font-family:'Inter','DM Sans',sans-serif;
}
.trash-btn:hover{border-color:var(--danger);color:var(--danger);transform:translateY(-1px);}
.trash-btn svg{width:14px;height:14px;stroke:currentColor;fill:none;stroke-width:2;}
.trash-count-badge{
  background:rgba(201,76,76,.2);border:1px solid rgba(201,76,76,.3);
  color:#f08080;border-radius:10px;padding:1px 6px;font-size:9px;font-weight:600;
  margin-left:auto;
}
/* Trash modal note item */
.trash-note-item{
  padding:10px 12px;border-radius:8px;background:var(--surface2);
  border:1px solid var(--border);margin-bottom:6px;
}
.trash-note-title{font-size:13px;font-weight:500;color:var(--text);margin-bottom:4px;}
.trash-note-date{font-size:10px;color:var(--text3);margin-bottom:8px;}
.trash-note-actions{display:flex;gap:6px;}
.trash-restore-btn{
  padding:4px 10px;font-size:11px;border-radius:var(--radius-sm);
  background:rgba(76,201,138,.12);border:1px solid rgba(76,201,138,.25);
  color:var(--success);cursor:pointer;font-family:'DM Sans',sans-serif;transition:.15s;
}
.trash-restore-btn:hover{background:rgba(76,201,138,.22);}
.trash-perm-btn{
  padding:4px 10px;font-size:11px;border-radius:var(--radius-sm);
  background:rgba(201,76,76,.12);border:1px solid rgba(201,76,76,.25);
  color:#f08080;cursor:pointer;font-family:'DM Sans',sans-serif;transition:.15s;
}
.trash-perm-btn:hover{background:rgba(201,76,76,.22);}

/* ===== FOLDERS ===== */
.folder-section{
  padding:4px 8px;border-bottom:1px solid var(--border);background:var(--surface);
}
.folder-list-wrap{display:flex;flex-direction:column;gap:2px;}
.folder-chip{
  display:flex;align-items:center;gap:6px;padding:7px 10px;
  border-radius:var(--radius-sm);cursor:pointer;transition:all .15s;
  font-size:13px;color:var(--text2);border:1px solid transparent;
  font-family:'Inter','DM Sans',sans-serif;background:none;text-align:left;width:100%;
  min-width:0;overflow:hidden;
}
.folder-chip span:not(.folder-count){
  white-space:nowrap;overflow:hidden;text-overflow:ellipsis;min-width:0;flex:1;
}
.folder-chip:hover{background:var(--surface2);color:var(--text);transform:translateX(2px);}
.folder-chip.active{background:var(--surface2);border-color:var(--border);color:var(--gold);}
.folder-chip svg{width:14px;height:14px;stroke:currentColor;fill:none;stroke-width:2;flex-shrink:0;}
.folder-count{margin-left:auto;font-size:11px;color:var(--text3);}
.folder-add-btn{
  padding:4px 8px;background:none;border:none;color:var(--text3);
  font-size:12px;cursor:pointer;display:flex;align-items:center;gap:4px;
  font-family:'Inter','DM Sans',sans-serif;transition:.15s;border-radius:var(--radius-sm);
}
.folder-add-btn:hover{color:var(--gold);}
.folder-add-btn svg{width:13px;height:13px;stroke:currentColor;fill:none;stroke-width:2.5;}
.folder-header{
  display:flex;align-items:center;justify-content:space-between;
  padding:2px 4px;margin-bottom:3px;
}
.folder-header-label{font-size:11px;color:var(--text3);font-weight:600;letter-spacing:.5px;text-transform:uppercase;}
.folder-section-toggle{
  font-size:11px;color:var(--text3);background:none;border:none;cursor:pointer;
  padding:0 2px;font-family:'Inter','DM Sans',sans-serif;transition:.15s;
}
.folder-section-toggle:hover{color:var(--text);}

/* ===== TEMPLATES ===== */
.template-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:16px;}
.template-card{
  padding:12px;border:1px solid var(--border);border-radius:8px;
  cursor:pointer;transition:.15s;background:var(--surface2);
}
.template-card:hover{border-color:var(--gold-dim);background:var(--surface3);}
.template-icon{font-size:20px;margin-bottom:6px;}
.template-name{font-size:12px;font-weight:500;color:var(--text);}
.template-desc{font-size:10px;color:var(--text3);margin-top:2px;}

/* ===== EXPORT SINGLE NOTE ===== */
.export-format-wrap{display:flex;gap:8px;margin-bottom:16px;}
.export-fmt-btn{
  flex:1;padding:9px;border:1px solid var(--border);border-radius:var(--radius-sm);
  background:var(--surface2);color:var(--text2);cursor:pointer;
  font-family:'DM Sans',sans-serif;font-size:13px;transition:.15s;
}
.export-fmt-btn:hover,.export-fmt-btn.active{border-color:var(--gold-dim);color:var(--gold);background:rgba(201,168,76,.1);}

/* ===== INTERACTIVE CHECKLISTS ===== */
.md-preview .task-list-item{list-style:none;display:flex;align-items:flex-start;gap:8px;margin-bottom:4px;}
.md-preview .task-list-item input[type=checkbox]{
  width:15px;height:15px;accent-color:var(--gold);margin-top:3px;cursor:pointer;flex-shrink:0;
}
.md-preview .task-list-item.checked span{text-decoration:line-through;opacity:.5;}
.task-checkbox{
  width:15px;height:15px;accent-color:var(--gold);cursor:pointer;
  vertical-align:middle;margin-right:6px;flex-shrink:0;
}

/* ===== DRAG REORDER ===== */
.note-item{cursor:grab;}
.note-item.dragging{opacity:.4;cursor:grabbing;}
.note-item.drag-over{border-top:2px solid var(--gold)!important;border-top-color:var(--gold)!important;}

/* ===== SECURITY PANEL (Floating Dashboard) ===== */
#shield-btn.panel-open{color:var(--gold);}
#shield-btn.panel-open svg{filter:drop-shadow(0 0 4px var(--gold-dim));}

.security-drawer{
  position:fixed;          /* fixed so nothing clips it */
  /* top/left set by JS on open */
  width:262px;
  background:var(--surface);
  border:1px solid var(--gold-dim);
  border-radius:14px;
  padding:16px;
  display:none;
  z-index:9500;            /* above everything except PIN overlay */
  box-shadow:0 16px 48px rgba(0,0,0,.6),0 0 0 1px rgba(212,166,42,.08);
}
.security-drawer.open{display:block;animation:secPanelIn .22s cubic-bezier(.34,1.56,.64,1);}
@keyframes secPanelIn{
  from{opacity:0;transform:translateY(-6px) scale(.97);}
  to{opacity:1;transform:translateY(0) scale(1);}
}




.sec-panel-title{
  font-size:11px;font-weight:600;letter-spacing:.6px;text-transform:uppercase;
  color:var(--text3);margin-bottom:10px;display:flex;align-items:center;gap:6px;
}
.sec-panel-title svg{width:12px;height:12px;stroke:var(--gold);fill:none;stroke-width:2.5;}
.sec-panel-divider{border:none;border-top:1px solid var(--border);margin:10px 0;}

.sec-pill-grid{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:12px;}
.sec-pill{
  font-size:10px;padding:3px 9px;border-radius:20px;font-weight:600;
  letter-spacing:.3px;border:1px solid var(--border);
  background:var(--surface2);color:var(--text3);
  display:flex;align-items:center;gap:4px;white-space:nowrap;
  transition:all .2s;
}
.sec-pill svg{width:9px;height:9px;flex-shrink:0;}
.sec-pill.ok{
  background:rgba(76,201,138,.1);border-color:rgba(76,201,138,.3);color:var(--success);
}
.sec-pill.ok svg{stroke:var(--success);}
.sec-pill.warn{
  background:rgba(212,166,42,.1);border-color:rgba(212,166,42,.3);color:var(--gold2);
}
.sec-pill.warn svg{stroke:var(--gold2);}
.sec-pill.danger{
  background:rgba(201,76,76,.1);border-color:rgba(201,76,76,.3);color:#f08080;
}
.sec-pill.danger svg{stroke:#f08080;}

.sec-panel-row{
  display:flex;align-items:center;justify-content:space-between;
  font-size:12px;color:var(--text2);padding:5px 0;
  border-bottom:1px solid var(--border);
}
.sec-panel-row:last-of-type{border-bottom:none;}
.sec-panel-row-label{display:flex;align-items:center;gap:5px;color:var(--text3);font-size:11px;}
.sec-panel-row-label svg{width:11px;height:11px;stroke:currentColor;fill:none;stroke-width:2;}
.sec-panel-val{font-size:11px;font-weight:500;}
.sec-panel-val.ok{color:var(--success);}
.sec-panel-val.warn{color:var(--gold2);}
.sec-panel-val.danger{color:#f08080;}

.sec-panel-actions{margin-top:12px;display:flex;flex-direction:column;gap:6px;}
.sec-panel-btn{
  width:100%;padding:8px;font-size:11px;font-weight:500;
  border-radius:8px;cursor:pointer;font-family:'Inter',sans-serif;
  letter-spacing:.3px;transition:all .15s;display:flex;align-items:center;
  justify-content:center;gap:6px;
}
.sec-panel-btn svg{width:12px;height:12px;stroke:currentColor;fill:none;stroke-width:2;}
.sec-panel-btn.gold{
  background:rgba(212,166,42,.1);border:1px solid rgba(212,166,42,.3);color:var(--gold);
}
.sec-panel-btn.gold:hover{background:rgba(212,166,42,.22);}
.sec-panel-btn.danger{
  background:rgba(201,76,76,.08);border:1px solid rgba(201,76,76,.25);color:#f08080;
}
.sec-panel-btn.danger:hover{background:rgba(201,76,76,.18);}


/* USB lock flash animation */
@keyframes usbLockFlash{
  0%,100%{background:rgba(17,19,21,.97);}
  50%{background:rgba(40,10,10,.97);}
}
#lock-overlay.usb-lock-flash{animation:usbLockFlash .4s ease 3;}

/* ===== APPEARANCE MODAL EXTRAS ===== */
@keyframes previewScan{
  0%{transform:translateX(-100%);}100%{transform:translateX(200%);}
}
@keyframes appearLockPulse{
  0%,100%{filter:drop-shadow(0 0 4px rgba(212,166,42,.3));}
  50%{filter:drop-shadow(0 0 14px rgba(212,166,42,.75));}
}
@keyframes modalScaleIn{
  from{opacity:0;transform:scale(.93) translateY(10px);}
  to{opacity:1;transform:scale(1) translateY(0);}
}
.modal-overlay:not(.hidden) .modal{animation:modalScaleIn .25s cubic-bezier(.34,1.56,.64,1);}
.appearance-theme-btn:hover{border-color:var(--gold-dim)!important;color:var(--gold)!important;transform:translateY(-2px);box-shadow:0 4px 12px rgba(0,0,0,.3);}
.appearance-theme-btn:active{transform:scale(.97);}

/* HACKER THEME */
:root.theme-hacker{
  --bg:#000800;--surface:#001200;--surface2:#001a00;--surface3:#002200;
  --border:rgba(0,255,0,.18);--border2:rgba(0,255,0,.3);
  --gold:#22ff22;--gold2:#55ff55;--gold-dim:#008800;
  --text:#ccffcc;--text2:#88cc88;--text3:#446644;
  --danger:#ff4444;--success:#22ff22;--info:#44aaff;
}
/* MIDNIGHT BLUE THEME */
:root.theme-midnight{
  --bg:#060b1a;--surface:#0d1830;--surface2:#111f3a;--surface3:#162444;
  --border:rgba(74,111,165,.25);--border2:rgba(74,111,165,.4);
  --gold:#6b9bd2;--gold2:#88b5e8;--gold-dim:#2a4a7a;
  --text:#ccdcf0;--text2:#8aaccc;--text3:#4a6a8a;
  --danger:#e05555;--success:#44cc88;--info:#5599dd;
}
/* FROST THEME */
:root.theme-frost{
  --bg:#0e1820;--surface:#152230;--surface2:#1c2c3e;--surface3:#223448;
  --border:rgba(200,220,240,.15);--border2:rgba(200,220,240,.28);
  --gold:#a0c8e8;--gold2:#c0d8f0;--gold-dim:#406080;
  --text:#d0e4f4;--text2:#90a8bc;--text3:#506070;
  --danger:#cc4444;--success:#44aacc;--info:#6699cc;
}
/* PURE BLACK AMOLED */
:root.theme-pure-black{
  --bg:#000000;--surface:#0a0a0a;--surface2:#111111;--surface3:#181818;
  --border:#1e1e1e;--border2:#2a2a2a;
  --gold:#ffffff;--gold2:#e0e0e0;--gold-dim:#555555;
  --text:#f0f0f0;--text2:#aaaaaa;--text3:#666666;
}

/* ===== TRASH PIN CODE ===== */
.trash-pin-dots{display:flex;gap:8px;justify-content:center;margin:12px 0;}
.trash-pin-dot{width:10px;height:10px;border-radius:50%;background:var(--border2);transition:.2s;}
.trash-pin-dot.filled{background:var(--gold);}
.trash-pin-input-wrap{position:relative;}

/* ===== QUICK-ACCESS DRAWER ===== */
/* ===== QUICK ACTIONS — PREMIUM GLASSMORPHISM (FINAL) ===== */
:root{
  --qa-bg:      rgba(17,19,21,0.65);
  --qa-bg-light:rgba(245,243,238,0.68);
  --qa-blur:    20px;
  --qa-border:  rgba(212,166,42,0.20);
  --qa-border-h:rgba(212,166,42,0.55);
  --qa-glow:    rgba(212,166,42,0.45);
  --qa-glow-sm: rgba(212,166,42,0.16);
  --qa-r-panel: 22px;
  --qa-r-btn:   13px;
  --qa-ease:    cubic-bezier(0.25,0.8,0.25,1);
  --qa-spring:  cubic-bezier(0.34,1.56,0.64,1);
}

/* ── Trigger strip ── */
.qa-drawer-wrap{
  position:relative;
  border-top:1px solid rgba(212,166,42,0.12);
  background:transparent;
}

.qa-toggle-btn{
  width:100%; padding:11px 16px;
  background:linear-gradient(135deg,rgba(212,166,42,0.06) 0%,rgba(212,166,42,0.02) 100%);
  border:none;
  display:flex; align-items:center; gap:9px;
  color:var(--gold); cursor:pointer;
  font-family:'Inter','DM Sans',sans-serif;
  font-size:11px; font-weight:700; letter-spacing:0.7px; text-transform:uppercase;
  transition:background .25s var(--qa-ease), color .2s, text-shadow .2s;
  position:relative; z-index:2; overflow:hidden; min-width:0;
  backdrop-filter:blur(8px);
  -webkit-backdrop-filter:blur(8px);
}
/* shimmer sweep */
.qa-toggle-btn::before{
  content:''; position:absolute; inset:0;
  background:linear-gradient(100deg,transparent 20%,rgba(212,166,42,0.09) 50%,transparent 80%);
  transform:translateX(-110%);
  transition:transform 0.55s ease;
}
.qa-toggle-btn:hover::before{ transform:translateX(110%); }
.qa-toggle-btn:hover{
  color:var(--gold2);
  background:linear-gradient(135deg,rgba(212,166,42,0.12) 0%,rgba(212,166,42,0.05) 100%);
  text-shadow:0 0 16px var(--qa-glow-sm);
}
.qa-toggle-btn svg{
  width:15px; height:15px; stroke:currentColor; fill:none; stroke-width:2; flex-shrink:0;
  filter:drop-shadow(0 0 3px var(--qa-glow-sm));
  transition:filter .25s;
}
.qa-toggle-btn:hover svg{ filter:drop-shadow(0 0 6px var(--qa-glow)); }
.qa-arrow{
  margin-left:auto; width:13px; height:13px;
  stroke:currentColor; fill:none; stroke-width:2.5;
  transition:transform 0.30s cubic-bezier(0.4,0,0.2,1);
}
.qa-drawer-wrap.open .qa-arrow{ transform:rotate(180deg); }

/* ── Floating popup ── */
.qa-tray{
  position:fixed; top:50%; left:50%;
  transform:translate(-50%,-50%) scale(0.93) translateY(14px);
  width:336px;
  /* core glass */
  background:var(--qa-bg);
  backdrop-filter:blur(var(--qa-blur)) saturate(160%);
  -webkit-backdrop-filter:blur(var(--qa-blur)) saturate(160%);
  /* glowing border */
  border:1px solid var(--qa-border);
  border-radius:var(--qa-r-panel);
  /* layered shadow: depth + gold ambient */
  box-shadow:
    0 2px 0 inset rgba(255,255,255,0.04),
    0 30px 70px rgba(0,0,0,0.80),
    0 0 0 1px var(--qa-border),
    0 0 50px rgba(212,166,42,0.05);
  padding:6px 15px 18px;
  z-index:3500;
  pointer-events:none; opacity:0;
  transition:opacity .26s ease, transform .32s var(--qa-spring);
}
:root.light .qa-tray,:root:not(.dark) .qa-tray{
  background:var(--qa-bg-light);
  border-color:rgba(180,148,55,0.28);
  box-shadow:0 20px 56px rgba(0,0,0,0.15),0 0 0 1px rgba(180,148,55,0.28);
}
.qa-drawer-wrap.open .qa-tray{
  pointer-events:all; opacity:1;
  transform:translate(-50%,-50%) scale(1) translateY(0);
}
/* glowing drag handle */
.qa-tray::before{
  content:''; display:block;
  width:40px; height:3px;
  background:linear-gradient(90deg,transparent,var(--gold),transparent);
  border-radius:2px; margin:8px auto 15px;
  opacity:0.60; box-shadow:0 0 10px var(--qa-glow);
}
/* top-left ambient radial */
.qa-tray::after{
  content:''; position:absolute; inset:0; border-radius:var(--qa-r-panel);
  background:
    radial-gradient(ellipse at 12% 0%, rgba(212,166,42,0.07) 0%, transparent 52%),
    radial-gradient(ellipse at 88% 100%,rgba(212,166,42,0.04) 0%, transparent 48%);
  pointer-events:none; z-index:0;
}

/* ── Popup header ── */
.qa-popup-header{
  display:flex; align-items:center; justify-content:space-between;
  padding:0 3px 9px;
  border-bottom:1px solid rgba(212,166,42,0.15);
  margin-bottom:11px;
  position:relative; z-index:1;
}
.qa-popup-title{
  font-size:9px; font-weight:800; letter-spacing:1px; text-transform:uppercase;
  color:var(--gold); display:flex; align-items:center; gap:6px;
  text-shadow:0 0 12px var(--qa-glow-sm);
}
.qa-popup-title svg{
  width:12px; height:12px; stroke:var(--gold); fill:none; stroke-width:2.5;
  filter:drop-shadow(0 0 5px var(--qa-glow));
}
.qa-popup-close{
  background:rgba(255,255,255,0.04);
  border:1px solid rgba(255,255,255,0.08);
  cursor:pointer; color:var(--text3);
  width:23px; height:23px; display:flex; align-items:center; justify-content:center;
  border-radius:7px;
  transition:all .22s var(--qa-ease);
}
.qa-popup-close:hover{
  background:rgba(201,76,76,0.18);
  border-color:rgba(201,76,76,0.42);
  color:#f08080;
  box-shadow:0 0 12px rgba(201,76,76,0.20);
}
.qa-popup-close svg{ width:12px; height:12px; stroke:currentColor; fill:none; stroke-width:2.5; }

/* ── Backdrop ── */
#qa-backdrop{
  position:fixed; inset:0; z-index:3499; display:none;
  background:rgba(0,0,0,0.52);
  backdrop-filter:blur(3px);
  -webkit-backdrop-filter:blur(3px);
}
.qa-drawer-wrap.open ~ #qa-backdrop,
body.qa-open #qa-backdrop{ display:block; }

/* ── Button grid ── */
.qa-grid{
  display:grid; grid-template-columns:repeat(3,1fr);
  gap:9px; padding:2px 1px;
  position:relative; z-index:1; min-width:0;
}

/* ── Base button ── */
.qa-btn{
  display:flex; flex-direction:column; align-items:center; justify-content:center;
  gap:8px; padding:15px 6px 13px;
  border-radius:var(--qa-r-btn);
  background:rgba(255,255,255,0.03);
  border:1px solid rgba(212,166,42,0.20);
  cursor:pointer; color:var(--text2);
  font-size:10px; font-weight:600; letter-spacing:0.25px;
  font-family:'Inter','DM Sans',sans-serif;
  position:relative; overflow:hidden; text-align:center;
  line-height:1.3; min-width:0; word-break:break-word;
  backdrop-filter:blur(4px);
  -webkit-backdrop-filter:blur(4px);
  transition:
    transform    .24s var(--qa-spring),
    border-color .22s var(--qa-ease),
    background   .22s var(--qa-ease),
    box-shadow   .22s var(--qa-ease),
    color        .18s var(--qa-ease);
}
:root.light .qa-btn,:root:not(.dark) .qa-btn{
  background:rgba(0,0,0,0.03);
}
/* diagonal shimmer */
.qa-btn::before{
  content:''; position:absolute; inset:0;
  background:linear-gradient(130deg,transparent 28%,rgba(212,166,42,0.10) 50%,transparent 72%);
  transform:translateX(-115%) rotate(6deg);
  transition:transform .48s ease;
}
.qa-btn:hover::before{ transform:translateX(130%) rotate(6deg); }
/* icon */
.qa-btn svg{
  width:21px; height:21px; stroke:currentColor; fill:none; stroke-width:1.9;
  transition:
    transform .24s var(--qa-spring),
    filter    .22s var(--qa-ease);
}
/* hover state */
.qa-btn:hover{
  background:rgba(212,166,42,0.09);
  border-color:rgba(212,166,42,0.55);
  color:var(--gold2);
  transform:translateY(-3px) scale(1.03);
  box-shadow:
    0 8px 26px rgba(0,0,0,0.40),
    0 0 0   1px rgba(212,166,42,0.22),
    0 0 18px rgba(212,166,42,0.07),
    inset 0 1px 0 rgba(255,255,255,0.06);
}
:root.light .qa-btn:hover,:root:not(.dark) .qa-btn:hover{
  background:rgba(160,120,20,0.08);
}
.qa-btn:hover svg{
  transform:translateY(-1px) scale(1.13);
  filter:drop-shadow(0 0 5px var(--qa-glow-sm));
}
.qa-btn:active{ transform:scale(0.95) translateY(0); }
.qa-btn:active::after{
  content:''; position:absolute; inset:0;
  border-radius:var(--qa-r-btn);
  background:rgba(212,166,42,0.18);
  animation:iconRipple .35s ease-out;
}

/* ── Colour variants ── */
.qa-btn.gold{
  border-color:rgba(212,166,42,0.32); color:var(--gold);
  background:rgba(212,166,42,0.07);
  box-shadow:inset 0 1px 0 rgba(212,166,42,0.10);
}
.qa-btn.gold:hover{
  background:rgba(212,166,42,0.16); border-color:var(--gold); color:var(--gold2);
  box-shadow:0 8px 28px rgba(0,0,0,0.40),0 0 22px var(--qa-glow-sm),0 0 0 1px rgba(212,166,42,0.45),inset 0 1px 0 rgba(255,255,255,0.09);
}
.qa-btn.gold:hover svg{ filter:drop-shadow(0 0 8px var(--qa-glow)); animation:iconGlowPulse .8s ease infinite; }

.qa-btn.danger{
  border-color:rgba(201,76,76,0.28); color:#f08080;
  background:rgba(201,76,76,0.06);
}
.qa-btn.danger:hover{
  background:rgba(201,76,76,0.14); border-color:rgba(201,76,76,0.58); color:#ff9090;
  box-shadow:0 8px 24px rgba(0,0,0,0.38),0 0 16px rgba(201,76,76,0.20),0 0 0 1px rgba(201,76,76,0.32);
}
.qa-btn.danger:hover svg{ filter:drop-shadow(0 0 6px rgba(201,76,76,0.55)); animation:iconWobble .45s ease; }

.qa-btn.info{
  border-color:rgba(74,143,201,0.24); color:var(--info);
  background:rgba(74,143,201,0.06);
}
.qa-btn.info:hover{
  background:rgba(74,143,201,0.14); border-color:rgba(74,143,201,0.50);
  box-shadow:0 8px 24px rgba(0,0,0,0.38),0 0 14px rgba(74,143,201,0.18),0 0 0 1px rgba(74,143,201,0.28);
}
.qa-btn.info:hover svg{ filter:drop-shadow(0 0 6px rgba(74,143,201,0.50)); }

.qa-btn.success{
  border-color:rgba(76,201,138,0.24); color:var(--success);
  background:rgba(76,201,138,0.06);
}
.qa-btn.success:hover{
  background:rgba(76,201,138,0.14); border-color:rgba(76,201,138,0.50);
  box-shadow:0 8px 24px rgba(0,0,0,0.38),0 0 14px rgba(76,201,138,0.18),0 0 0 1px rgba(76,201,138,0.28);
}
.qa-btn.success:hover svg{ filter:drop-shadow(0 0 6px rgba(76,201,138,0.50)); }

/* ===== ICON ANIMATIONS ===== */

/* --- Keyframes --- */
@keyframes iconBounce{
  0%{transform:scale(1);}40%{transform:scale(1.42);}70%{transform:scale(.88);}100%{transform:scale(1);}
}
@keyframes iconWobble{
  0%,100%{transform:rotate(0deg);}20%{transform:rotate(-13deg);}50%{transform:rotate(11deg);}75%{transform:rotate(-5deg);}
}
@keyframes iconSpin{
  from{transform:rotate(0deg);}to{transform:rotate(360deg);}
}
@keyframes iconSpinBack{
  from{transform:rotate(0deg);}to{transform:rotate(-360deg);}
}
@keyframes iconJiggle{
  0%,100%{transform:rotate(0deg) translate(0,0);}
  25%{transform:rotate(-9deg) translate(-1px,1px);}
  75%{transform:rotate(9deg) translate(1px,-1px);}
}
@keyframes iconGlowPulse{
  0%,100%{filter:drop-shadow(0 0 3px rgba(212,166,42,.3));}
  50%{filter:drop-shadow(0 0 10px rgba(212,166,42,.8));}
}
@keyframes iconGlowDanger{
  0%,100%{filter:drop-shadow(0 0 3px rgba(201,76,76,.3));}
  50%{filter:drop-shadow(0 0 10px rgba(201,76,76,.85));}
}
@keyframes iconPop{
  0%{transform:scale(1);}30%{transform:scale(1.3);}60%{transform:scale(.92);}100%{transform:scale(1);}
}
@keyframes iconSlideRight{
  0%{transform:translateX(0);}40%{transform:translateX(5px);}70%{transform:translateX(-2px);}100%{transform:translateX(0);}
}
@keyframes iconPulse{
  0%,100%{transform:scale(1);}50%{transform:scale(1.18);}
}
@keyframes iconFlip{
  0%{transform:rotateY(0deg);}50%{transform:rotateY(90deg);}100%{transform:rotateY(0deg);}
}
@keyframes iconShake{
  0%,100%{transform:translateX(0);}20%{transform:translateX(-4px);}40%{transform:translateX(4px);}60%{transform:translateX(-3px);}80%{transform:translateX(3px);}
}
@keyframes iconRipple{
  from{opacity:1;transform:scale(.2);}to{opacity:0;transform:scale(2.2);}
}
@keyframes checkPop{
  0%{transform:scale(0);opacity:0;}60%{transform:scale(1.35);opacity:1;}100%{transform:scale(1);opacity:1;}
}

/* --- Assignments --- */

/* Pin/Star — bounce */
#pin-btn:hover svg{animation:iconBounce .4s cubic-bezier(.34,1.56,.64,1);}

/* Trash / Delete — wobble */
.trash-btn:hover svg,
button[onclick="confirmDelete()"]:hover svg{animation:iconWobble .5s ease;}

/* Security Settings gear — spin */
#settings-btn:hover svg,
button[onclick="openSettings()"]:hover svg{animation:iconSpin .55s cubic-bezier(.4,0,.2,1);}

/* Account / User — flip */
#account-btn:hover svg,
button[onclick="openAccountSettings()"]:hover svg{animation:iconFlip .5s ease;}

/* Theme toggle — pulse */
#theme-btn:hover svg{animation:iconPulse .5s ease;}

/* Save (floppy) — jiggle */
button[onclick="saveCurrentNote()"]:hover svg,
button[title*="Save"]:hover svg{animation:iconJiggle .4s ease;}

/* Copy to clipboard — pop */
button[onclick="copyToClipboard()"]:hover svg{animation:iconPop .35s cubic-bezier(.34,1.56,.64,1);}

/* Export — slide up */
button[onclick="openExportModal()"]:hover svg,
button[onclick="exportEncrypted()"]:hover svg{animation:iconSlideRight .4s ease;}

/* Note-level lock buttons — gold glow */
button[onclick="openNoteLock()"]:hover svg,
button[onclick="lockCurrentNote()"]:hover svg{
  animation:iconGlowPulse .85s ease infinite;color:var(--gold);
}

/* Logout — slide right */
button[onclick="doLogout()"]:hover svg{animation:iconSlideRight .4s ease;}

/* Image upload — pop */
button[onclick="triggerImageUpload()"]:hover svg{animation:iconPop .35s cubic-bezier(.34,1.56,.64,1);}

/* MD toggle, find/replace — shake */
button[onclick="toggleMarkdown()"]:hover,
button[onclick="openFindReplace()"]:hover svg{animation:iconShake .35s ease;}

/* New Note button icon — spin */
.new-btn:hover svg{animation:iconSpin .4s cubic-bezier(.4,0,.2,1);}

/* Re-lock shackle lift */
@keyframes shackleLift{
  0%{transform:translateY(0);}50%{transform:translateY(-4px);}100%{transform:translateY(0);}
}
#note-relock-btn:hover .relock-shackle{animation:shackleLift .35s cubic-bezier(.34,1.56,.64,1);}
#relock-icon{transition:transform .15s ease;}

/* QA drawer home icon — bounce */
@keyframes homeBounce{
  0%{transform:scale(1);}50%{transform:scale(1.22);}75%{transform:scale(.92);}100%{transform:scale(1);}
}
.qa-toggle-btn:hover .qa-home-icon{animation:homeBounce .35s cubic-bezier(.34,1.56,.64,1);}

/* QA Appearance btn — spin (globe) */
.qa-btn.gold:hover svg{animation:iconSpinBack .6s cubic-bezier(.4,0,.2,1);}

/* QA New Note btn (2nd) — pop */
.qa-btn:nth-child(2):hover svg{animation:iconPop .35s cubic-bezier(.34,1.56,.64,1);}

/* QA Logout btn (3rd) — slide */
.qa-btn:nth-child(3):hover svg{animation:iconSlideRight .4s ease;}

/* Ripple on all icon-btns on click */
.icon-btn{position:relative;overflow:hidden;}
.icon-btn:active::after{
  content:'';position:absolute;inset:0;border-radius:var(--radius-sm);
  background:rgba(212,166,42,.18);animation:iconRipple .38s ease-out;
}

/* Lift — all icon-btns */
.icon-btn:hover{transform:translateY(-2px);}
.icon-btn:active{transform:scale(.94);}

/* Folder add btn spin */
.folder-add-btn:hover svg{animation:iconSpin .4s cubic-bezier(.4,0,.2,1);}


/* ===== FLOATING NOTE EDITOR OVERLAY ===== */
#note-float-backdrop{
  position:fixed;inset:0;
  background:rgba(0,0,0,0);
  backdrop-filter:blur(0px);-webkit-backdrop-filter:blur(0px);
  z-index:4000;
  display:none;
  transition:background .3s ease,backdrop-filter .3s ease;
}
#note-float-backdrop.open{
  display:block;
  background:rgba(0,0,0,.55);
  backdrop-filter:blur(6px);-webkit-backdrop-filter:blur(6px);
}
#note-float-panel{
  position:fixed;
  top:50%;left:50%;
  transform:translate(-50%,-46%) scale(.97);
  width:min(820px,92vw);
  max-height:88vh;
  background:var(--surface);
  border:1px solid var(--border2);
  border-radius:18px;
  box-shadow:0 24px 80px rgba(0,0,0,.7),0 0 0 1px rgba(212,166,42,.08);
  display:flex;flex-direction:column;
  z-index:4001;
  opacity:0;pointer-events:none;
  transition:transform .3s cubic-bezier(.34,1.56,.64,1),opacity .25s ease;
  overflow:hidden;
}
#note-float-panel.open{
  transform:translate(-50%,-50%) scale(1);
  opacity:1;pointer-events:all;
}
/* Close button */
#note-float-close{
  position:absolute;top:14px;right:14px;
  width:32px;height:32px;
  background:var(--surface2);border:1px solid var(--border);
  border-radius:50%;cursor:pointer;
  display:flex;align-items:center;justify-content:center;
  color:var(--text2);z-index:10;transition:all .2s;
  font-size:16px;line-height:1;
}
#note-float-close:hover{background:var(--surface3);color:var(--text);border-color:var(--border2);transform:scale(1.08);}
#note-float-close svg{width:14px;height:14px;stroke:currentColor;fill:none;stroke-width:2.5;}

/* Float panel inner — the actual editor reused inside */
#note-float-panel .editor-bar{
  border-radius:18px 18px 0 0;
  padding-right:54px; /* space for close btn */
  flex-shrink:0;
}
#note-float-panel .editor-body{
  flex:1;overflow-y:auto;min-height:0;
}
#note-float-panel .editor-toolbar{
  border-radius:0 0 18px 18px;flex-shrink:0;
}
#note-float-panel .tags-wrap{flex-shrink:0;}
#note-float-panel .editor-meta{flex-shrink:0;}
#note-float-panel #find-replace-bar{flex-shrink:0;}

/* ===== LOCKED-MODE: compact panel for password-locked notes ===== */
#note-float-panel.locked-mode{
  width:min(420px,92vw);
  max-height:fit-content;
  /* smooth resize */
  transition:width .3s cubic-bezier(.34,1.56,.64,1),
             max-height .35s ease,
             transform .3s cubic-bezier(.34,1.56,.64,1),
             opacity .25s ease;
}
/* Hide everything except the lock overlay */
#note-float-panel.locked-mode .editor-bar,
#note-float-panel.locked-mode .tags-wrap,
#note-float-panel.locked-mode .editor-meta,
#note-float-panel.locked-mode #find-replace-bar,
#note-float-panel.locked-mode .editor-toolbar{
  display:none !important;
}
/* Let editor-body shrink to content */
#note-float-panel.locked-mode #editor-body-wrap{
  flex:none;
  overflow:visible;
  position:static;
  min-height:0;
}
/* Hide everything inside editor-body except the lock overlay */
#note-float-panel.locked-mode #editor-body-wrap > *:not(#note-lock-overlay){
  display:none !important;
}
/* Override overlay to flow normally (not absolute) */
#note-float-panel.locked-mode .note-lock-overlay{
  position:static !important;
  background:#0d0f12;
  border-radius:0 0 18px 18px;
  padding:36px 36px 44px;
  min-height:0;
  backdrop-filter:none;
}
#note-float-panel.locked-mode .note-lock-overlay>div{
  max-width:100%;
  padding:0;
}
/* Close button stays on top */
#note-float-panel.locked-mode #note-float-close{
  z-index:20;
  background:rgba(255,255,255,.06);
  border-color:rgba(255,255,255,.1);
  color:rgba(255,255,255,.5);
}
#note-float-panel.locked-mode #note-float-close:hover{
  background:rgba(255,255,255,.12);
  color:rgba(255,255,255,.85);
}
/* Compact title bar strip shown in locked mode */
#note-float-panel.locked-mode .editor-bar.lock-bar-visible{
  display:flex !important;
  background:#0d0f12;
  border-bottom:1px solid rgba(255,255,255,.06);
  border-radius:18px 18px 0 0;
  padding:12px 54px 12px 18px;
  min-height:0;
  align-items:center;
}
</style>
</head>
<body>

<!-- HIDE NOTES HINT -->


<!-- SESSION TIMEOUT WARNING -->
<div id="session-warn">
  ⏱ &nbsp;Session locking in <span id="session-warn-count">30</span>s due to inactivity &nbsp;
  <button id="session-warn-extend" onclick="extendSession()">Stay Active</button>
</div>

<!-- CLIPBOARD TIMER BANNER -->
<div class="clip-timer" id="clip-timer">📋 Clipboard clears in <span id="clip-countdown">30</span>s</div>

<!-- BOOT SCREEN -->
<div class="screen" id="boot-screen">
  <div style="text-align:center">
    <div class="lock-icon" style="margin:0 auto 16px">
      <svg viewBox="0 0 24 24"><rect x="3" y="11" width="18" height="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>
    </div>
    <button onclick="init()" style="background:none;border:none;cursor:pointer;padding:0;display:block;margin:0 auto" title="Go to Home">
      <div style="font-family:'Playfair Display',serif;font-size:22px;color:var(--gold);transition:opacity .2s" onmouseover="this.style.opacity='.75'" onmouseout="this.style.opacity='1'">SecureNote</div>
    </button>
    <div style="font-size:12px;color:var(--text3);margin-top:6px">Loading…</div>
  </div>
</div>

<!-- CONNECT USB SCREEN -->
<div class="screen hidden" id="connect-screen">
  <div class="card">
    <div style="text-align:center;margin-bottom:12px"><svg width="72" height="72" viewBox="0 0 120 120" xmlns="http://www.w3.org/2000/svg" style="display:block;margin:0 auto" aria-label="SecureNote logo">
  <circle cx="60" cy="58" r="50" fill="none" stroke="var(--gold)" stroke-width="2.5" opacity="0.5"/>
  <rect x="46" y="22" width="38" height="50" rx="3" fill="var(--surface3)" stroke="var(--gold)" stroke-width="2"/>
  <line x1="52" y1="34" x2="78" y2="34" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <line x1="52" y1="42" x2="78" y2="42" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <line x1="52" y1="50" x2="78" y2="50" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <rect x="52" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <rect x="62" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <rect x="72" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <line x1="72" y1="38" x2="88" y2="68" stroke="var(--gold)" stroke-width="3" stroke-linecap="round"/>
  <polygon points="88,68 82,65 86,75" fill="var(--gold)" opacity="0.9"/>
  <path d="M30 48 L30 65 Q30 76 40 80 Q50 76 50 65 L50 48 L40 44 Z" fill="var(--gold)" opacity="0.85"/>
  <rect x="35" y="61" width="10" height="8" rx="1.5" fill="var(--bg)"/>
  <path d="M36.5 61 Q36.5 56 40 56 Q43.5 56 43.5 61" fill="none" stroke="var(--bg)" stroke-width="2"/>
  <circle cx="40" cy="65" r="1.5" fill="var(--gold)"/>
</svg></div>
    <button onclick="init()" style="background:none;border:none;cursor:pointer;padding:0;display:block;width:100%" title="Back to Home">
      <div class="card-logo" style="transition:opacity .2s" onmouseover="this.style.opacity='.75'" onmouseout="this.style.opacity='1'">SecureNote</div>
    </button>
    <div class="card-sub">Select your USB drive folder to continue</div>
    <div id="alert-connect" class="alert danger"></div>
    <p style="font-size:13px;color:var(--text2);line-height:1.6;margin-bottom:20px;text-align:center">
      Make sure your USB is plugged in, then click below and select its folder.
    </p>
    <button class="btn btn-gold" onclick="connectUSB()" id="btn-connect">
      📁 &nbsp;Select USB Folder
    </button>
    <div style="margin-top:12px;text-align:center;font-size:12px;color:var(--text3)">
      Works on any computer — your vault stays on the USB
    </div>
    <div style="margin-top:20px;text-align:center;font-size:11px;color:var(--text3);border-top:1px solid var(--border);padding-top:12px">
      Crafted by <span style="color:var(--gold-dim);font-weight:600">JMR</span>
    </div>
  </div>
</div>

<!-- SETUP SCREEN -->
<div class="screen hidden" id="setup-screen">
  <div class="card">
    <div style="text-align:center;margin-bottom:8px"><svg width="72" height="72" viewBox="0 0 120 120" xmlns="http://www.w3.org/2000/svg" style="display:block;margin:0 auto" aria-label="SecureNote logo">
  <circle cx="60" cy="58" r="50" fill="none" stroke="var(--gold)" stroke-width="2.5" opacity="0.5"/>
  <rect x="46" y="22" width="38" height="50" rx="3" fill="var(--surface3)" stroke="var(--gold)" stroke-width="2"/>
  <line x1="52" y1="34" x2="78" y2="34" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <line x1="52" y1="42" x2="78" y2="42" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <line x1="52" y1="50" x2="78" y2="50" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <rect x="52" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <rect x="62" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <rect x="72" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <line x1="72" y1="38" x2="88" y2="68" stroke="var(--gold)" stroke-width="3" stroke-linecap="round"/>
  <polygon points="88,68 82,65 86,75" fill="var(--gold)" opacity="0.9"/>
  <path d="M30 48 L30 65 Q30 76 40 80 Q50 76 50 65 L50 48 L40 44 Z" fill="var(--gold)" opacity="0.85"/>
  <rect x="35" y="61" width="10" height="8" rx="1.5" fill="var(--bg)"/>
  <path d="M36.5 61 Q36.5 56 40 56 Q43.5 56 43.5 61" fill="none" stroke="var(--bg)" stroke-width="2"/>
  <circle cx="40" cy="65" r="1.5" fill="var(--gold)"/>
</svg></div>
    <button onclick="init()" style="background:none;border:none;cursor:pointer;padding:0;display:block;width:100%" title="Back to Home">
      <div class="card-logo" style="transition:opacity .2s" onmouseover="this.style.opacity='.75'" onmouseout="this.style.opacity='1'">SecureNote</div>
    </button>
    <div class="card-sub">First-time setup — store everything on your USB</div>
    <div class="steps">
      <div class="step active" id="step1-dot"></div>
      <div class="step" id="step2-dot"></div>
      <div class="step" id="step3-dot"></div>
      <div class="step" id="step4-dot"></div>
    </div>
    <div id="alert-setup" class="alert danger"></div>

    <!-- Step 1: Credentials -->
    <div id="setup-step1">
      <div class="form-group">
        <label>Username</label>
        <input type="text" id="setup-username" placeholder="Choose a username" autocomplete="off">
      </div>
      <div class="form-group">
        <label>Password (Main Vault)</label>
        <input type="password" id="setup-password" placeholder="Create a strong password" autocomplete="new-password" oninput="updatePwStrength(this.value)">
        <div class="pw-strength-wrap">
          <div class="pw-strength-bar"><div class="pw-strength-fill" id="pw-strength-fill"></div></div>
          <div class="pw-strength-label" id="pw-strength-label"></div>
        </div>
      </div>
      <div class="form-group">
        <label>Confirm Password</label>
        <input type="password" id="setup-confirm" placeholder="Repeat password" autocomplete="new-password">
      </div>
      <div class="form-group">
        <label>Decoy Password <span style="color:var(--text3);font-size:10px">(opens empty vault)</span></label>
        <input type="password" id="setup-decoy" placeholder="Optional fake password" autocomplete="new-password">
      </div>
      <button class="btn btn-gold" onclick="setupStep1Next()">Continue →</button>
    </div>

    <!-- Step 2: 2FA PIN Setup -->
    <div id="setup-step2" style="display:none">
      <p style="font-size:13px;color:var(--text2);margin-bottom:16px;line-height:1.6">
        Set a <strong style="color:var(--text)">4-digit PIN</strong> for two-factor authentication. After your password, you'll be asked for this PIN.
      </p>
      <div class="form-group">
        <label>4-Digit PIN</label>
        <input type="password" id="setup-pin" placeholder="e.g. 1234" maxlength="4" pattern="[0-9]*" inputmode="numeric">
      </div>
      <div class="form-group">
        <label>Confirm PIN</label>
        <input type="password" id="setup-pin-confirm" placeholder="Repeat PIN" maxlength="4" pattern="[0-9]*" inputmode="numeric">
      </div>
      <div style="font-size:12px;color:var(--text3);margin-bottom:16px">Leave both blank to skip 2FA PIN.</div>
      <button class="btn btn-gold" onclick="setupStep2Next()">Continue →</button>
      <button class="btn btn-outline" onclick="goToStep(1)" style="margin-top:8px">← Back</button>
    </div>

    <!-- Step 3: USB folder -->
    <div id="setup-step3" style="display:none">
      <p style="font-size:13px;color:var(--text2);margin-bottom:16px;line-height:1.6">
        Select your <strong style="color:var(--text)">USB drive folder</strong> as the storage location.
      </p>
      <div class="dir-box" id="dir-box" onclick="pickDirectory()">
        <svg viewBox="0 0 24 24"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg>
        <div class="dir-name" id="dir-name">Click to select USB folder</div>
        <div style="font-size:11px;color:var(--text3);margin-top:4px" id="dir-hint">e.g. D:\ or E:\SecureNote</div>
      </div>
      <button class="btn btn-gold" onclick="setupStep3Next()" id="btn-setup3">Select Folder First</button>
      <button class="btn btn-outline" onclick="goToStep(2)" style="margin-top:8px">← Back</button>
    </div>

    <!-- Step 4: Confirm -->
    <div id="setup-step4" style="display:none">
      <div style="text-align:center;padding:8px 0 20px">
        <div style="width:52px;height:52px;border-radius:50%;background:rgba(76,201,138,.1);border:1px solid rgba(76,201,138,.3);display:flex;align-items:center;justify-content:center;margin:0 auto 14px">
          <svg style="width:24px;height:24px;stroke:#4cc98a;fill:none;stroke-width:2" viewBox="0 0 24 24"><polyline points="20 6 9 17 4 12"/></svg>
        </div>
        <div style="font-size:15px;font-weight:500;margin-bottom:6px">Ready to go</div>
        <div style="font-size:13px;color:var(--text2)">AES-256-GCM encrypted vault will be created on your USB.</div>
      </div>
      <div id="setup-summary" style="background:var(--surface2);border-radius:var(--radius-sm);padding:14px;font-size:12px;margin-bottom:18px"></div>
      <button class="btn btn-gold" onclick="finishSetup()">Create My Vault</button>
      <button class="btn btn-outline" onclick="goToStep(3)" style="margin-top:8px">← Back</button>
    </div>
  </div>
</div>

<!-- LOGIN SCREEN -->
<div class="screen hidden" id="login-screen">
  <div class="card">
    <div style="text-align:center;margin-bottom:12px"><svg width="72" height="72" viewBox="0 0 120 120" xmlns="http://www.w3.org/2000/svg" style="display:block;margin:0 auto" aria-label="SecureNote logo">
  <circle cx="60" cy="58" r="50" fill="none" stroke="var(--gold)" stroke-width="2.5" opacity="0.5"/>
  <rect x="46" y="22" width="38" height="50" rx="3" fill="var(--surface3)" stroke="var(--gold)" stroke-width="2"/>
  <line x1="52" y1="34" x2="78" y2="34" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <line x1="52" y1="42" x2="78" y2="42" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <line x1="52" y1="50" x2="78" y2="50" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <rect x="52" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <rect x="62" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <rect x="72" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <line x1="72" y1="38" x2="88" y2="68" stroke="var(--gold)" stroke-width="3" stroke-linecap="round"/>
  <polygon points="88,68 82,65 86,75" fill="var(--gold)" opacity="0.9"/>
  <path d="M30 48 L30 65 Q30 76 40 80 Q50 76 50 65 L50 48 L40 44 Z" fill="var(--gold)" opacity="0.85"/>
  <rect x="35" y="61" width="10" height="8" rx="1.5" fill="var(--bg)"/>
  <path d="M36.5 61 Q36.5 56 40 56 Q43.5 56 43.5 61" fill="none" stroke="var(--bg)" stroke-width="2"/>
  <circle cx="40" cy="65" r="1.5" fill="var(--gold)"/>
</svg></div>
    <button onclick="init()" style="background:none;border:none;cursor:pointer;padding:0;display:block;width:100%" title="Back to Home">
      <div class="card-logo" style="transition:opacity .2s" onmouseover="this.style.opacity='.75'" onmouseout="this.style.opacity='1'">SecureNote</div>
    </button>
    <div class="card-sub">Enter your credentials to unlock your vault</div>
    <div id="alert-login" class="alert danger"></div>
    <div class="form-group">
      <label>Username</label>
      <input type="text" id="login-username" placeholder="Username" autocomplete="off" onkeydown="if(event.key==='Enter')document.getElementById('login-password').focus()">
    </div>
    <div class="form-group">
      <label>Password</label>
      <input type="password" id="login-password" placeholder="Password" autocomplete="current-password" onkeydown="if(event.key==='Enter')doLogin()">
    </div>
    <div id="lockout-timer" style="display:none;text-align:center;font-size:12px;color:var(--danger);margin-bottom:12px"></div>
    <button class="btn btn-gold" onclick="doLogin()" id="btn-login">Unlock Vault</button>
    <div class="divider"><span>or</span></div>
    <button class="btn btn-outline" onclick="showSelectUSB()">
      <svg style="width:14px;height:14px;stroke:currentColor;fill:none;stroke-width:2;vertical-align:-2px;margin-right:6px" viewBox="0 0 24 24"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg>
      Select Different USB Folder
    </button>
    <div style="margin-top:16px;text-align:center">
      <button onclick="resetAll()" style="background:none;border:none;color:var(--text3);font-size:11px;cursor:pointer;text-decoration:underline">Reset / New Setup</button>
    </div>
    <div style="margin-top:16px;text-align:center;font-size:11px;color:var(--text3);border-top:1px solid var(--border);padding-top:12px">
      Crafted by <span style="color:var(--gold-dim);font-weight:600">JMR</span>
    </div>
  </div>
</div>

<!-- 2FA PIN SCREEN -->
<div class="screen hidden" id="pin-screen">
  <div class="card" style="width:380px">
    <div class="lock-icon">
      <svg viewBox="0 0 24 24"><rect x="3" y="11" width="18" height="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>
    </div>
    <div class="card-logo">2-Factor PIN</div>
    <div class="card-sub">Enter your 4-digit PIN to continue</div>
    <div id="alert-pin" class="alert danger"></div>
    <div class="pin-dots">
      <div class="pin-dot" id="pd0"></div>
      <div class="pin-dot" id="pd1"></div>
      <div class="pin-dot" id="pd2"></div>
      <div class="pin-dot" id="pd3"></div>
    </div>
    <input type="password" id="pin-input" maxlength="4" pattern="[0-9]*" inputmode="numeric"
      placeholder="••••" style="text-align:center;letter-spacing:8px;font-size:20px"
      oninput="onPinInput()" onkeydown="if(event.key==='Enter')verifyPin()">
    <button class="btn btn-gold" onclick="verifyPin()" style="margin-top:16px">Verify PIN</button>
    <button class="btn btn-outline" onclick="showScreen('login-screen');document.getElementById('pin-input').value='';resetPinDots();" style="margin-top:8px">← Back</button>
  </div>
</div>

<!-- MAIN APP -->
<div id="app-screen">
  <!-- Sidebar -->
  <div class="sidebar">
    <div class="sidebar-header">
      <div>
        <div style="display:flex;align-items:center;gap:8px"><svg width="30" height="30" viewBox="0 0 120 120" xmlns="http://www.w3.org/2000/svg" style="display:block;flex-shrink:0" aria-label="SecureNote logo">
  <circle cx="60" cy="58" r="50" fill="none" stroke="var(--gold)" stroke-width="2.5" opacity="0.5"/>
  <rect x="46" y="22" width="38" height="50" rx="3" fill="var(--surface3)" stroke="var(--gold)" stroke-width="2"/>
  <line x1="52" y1="34" x2="78" y2="34" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <line x1="52" y1="42" x2="78" y2="42" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <line x1="52" y1="50" x2="78" y2="50" stroke="var(--gold)" stroke-width="1.2" opacity="0.4"/>
  <rect x="52" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <rect x="62" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <rect x="72" y="19" width="5" height="6" rx="2.5" fill="var(--gold)" opacity="0.8"/>
  <line x1="72" y1="38" x2="88" y2="68" stroke="var(--gold)" stroke-width="3" stroke-linecap="round"/>
  <polygon points="88,68 82,65 86,75" fill="var(--gold)" opacity="0.9"/>
  <path d="M30 48 L30 65 Q30 76 40 80 Q50 76 50 65 L50 48 L40 44 Z" fill="var(--gold)" opacity="0.85"/>
  <rect x="35" y="61" width="10" height="8" rx="1.5" fill="var(--bg)"/>
  <path d="M36.5 61 Q36.5 56 40 56 Q43.5 56 43.5 61" fill="none" stroke="var(--bg)" stroke-width="2"/>
  <circle cx="40" cy="65" r="1.5" fill="var(--gold)"/>
</svg><div class="sidebar-logo">SecureNote</div></div>
        <div class="sidebar-user" id="user-label"></div>
      </div>
      <div>
        <button class="icon-btn theme-auto" id="theme-btn" onclick="toggleTheme()" title="Theme: Auto / Light / Dark">
          <span class="theme-icon-wrap"><svg id="theme-icon" viewBox="0 0 24 24" style="width:17px;height:17px;stroke:currentColor;fill:none;stroke-width:1.8"><circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/><line x1="12" y1="21" x2="12" y2="23"/><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/><line x1="1" y1="12" x2="3" y2="12"/><line x1="21" y1="12" x2="23" y2="12"/><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/></svg></span>
        </button>
        <button class="icon-btn" id="settings-btn" onclick="openSettings()" title="Security Settings">
          <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>
        </button>
        <button class="icon-btn" id="account-btn" onclick="openAccountSettings()" title="Account Settings (Change Name / Password)">
          <svg viewBox="0 0 24 24"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
        </button>
      </div>
    </div>
    <!-- Security Badges -->
    <div class="sec-badges" id="sec-badges"></div>
    <div class="search-wrap">
      <div class="search-wrap-inner">
        <svg viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
        <input class="search-input" type="text" placeholder="Search notes…" id="search-input" oninput="renderNoteList()">
      </div>
    </div>
    <div style="display:flex;gap:8px;margin:8px 8px 4px">
      <button class="new-btn" style="flex:1;margin:0" onclick="openTemplateModal()">
        <svg viewBox="0 0 24 24"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg>
        New Note
      </button>
    </div>
    <!-- Folders section -->
    <div class="folder-section" id="folder-section">
      <div class="folder-header">
        <span class="folder-header-label">📁 Folders</span>
        <button class="folder-add-btn" onclick="openFolderManager()" title="Manage folders">
          <svg viewBox="0 0 24 24"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg>
        </button>
      </div>
      <div class="folder-list-wrap" id="folder-list-wrap"></div>
    </div>
    <div class="tag-filter-wrap" id="tag-filter-wrap" style="display:none">
      <span class="tag-filter-label">Tags:</span>
      <div id="tag-filter-chips"></div>
    </div>
    <div class="note-list" id="note-list"></div>
    <div class="trash-section">
      <button class="trash-btn" onclick="openTrash()">
        <svg viewBox="0 0 24 24"><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2L5 6"/><path d="M10 11v6"/><path d="M14 11v6"/></svg>
        Trash
        <span class="trash-count-badge" id="trash-count-badge" style="display:none">0</span>
      </button>
    </div>
    <!-- Quick-Access Floating Popup -->
    <div class="qa-drawer-wrap" id="qa-drawer">
      <button class="qa-toggle-btn" onclick="toggleQADrawer()" title="Quick Actions">
        <svg class="qa-home-icon" viewBox="0 0 24 24"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>
        Quick Actions
        <svg class="qa-arrow" viewBox="0 0 24 24"><polyline points="18 15 12 9 6 15"/></svg>
      </button>
      <div class="qa-tray">
        <div class="qa-popup-header">
          <div class="qa-popup-title">
            <svg viewBox="0 0 24 24"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/></svg>
            Quick Actions
          </div>
          <button class="qa-popup-close" onclick="toggleQADrawer(false)" title="Close">
            <svg viewBox="0 0 24 24"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
          </button>
        </div>
        <div class="qa-grid">
          <button class="qa-btn gold" onclick="openAppearanceModal();toggleQADrawer(false)" title="Appearance">
            <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M12 2a10 10 0 0 1 0 20"/><circle cx="12" cy="12" r="4"/></svg>
            Appearance
          </button>
          <button class="qa-btn" onclick="openTemplateModal();toggleQADrawer(false)" title="New Note">
            <svg viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="12" y1="18" x2="12" y2="12"/><line x1="9" y1="15" x2="15" y2="15"/></svg>
            New Note
          </button>
          <button class="qa-btn" onclick="doLogout();toggleQADrawer(false)" title="Lock &amp; Logout">
            <svg viewBox="0 0 24 24"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" y1="12" x2="9" y2="12"/></svg>
            Logout
          </button>
        </div>
      </div>
    </div>
    <!-- Backdrop to close popup when clicking outside -->
    <div id="qa-backdrop" onclick="toggleQADrawer(false)"></div>
    <div class="sidebar-footer">
      <div style="display:flex;align-items:center;justify-content:space-between">
        <div class="storage-info"><span class="storage-dot" id="usb-dot"></span><span id="usb-status-text">USB Vault Connected</span></div>
        <div id="note-count" style="font-size:11px;color:var(--text3)"></div>
      </div>
      <div class="usb-indicator connected" id="usb-indicator">
        <svg style="width:10px;height:10px;stroke:currentColor;fill:none;stroke-width:2" viewBox="0 0 24 24"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg>
        <span id="usb-name-label">USB Connected</span>
      </div>
      <div class="credit">Crafted by <span>JMR</span></div>
    </div>
  </div><!-- end sidebar -->
</div><!-- end app-screen -->

<!-- ===== FLOATING NOTE EDITOR BACKDROP ===== -->
<div id="note-float-backdrop" onclick="closeFloatEditor()"></div>

<!-- ===== FLOATING NOTE EDITOR PANEL ===== -->
<div id="note-float-panel">
  <!-- Close button -->
  <button id="note-float-close" onclick="closeFloatEditor()" title="Close (Esc)">
    <svg viewBox="0 0 24 24"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
  </button>
  <div id="editor-content" style="display:flex;flex-direction:column;flex:1;overflow:hidden;min-height:0">
      <div class="editor-bar">
        <input class="editor-title" id="note-title" type="text" placeholder="Note title…" oninput="markUnsaved()">
        <span class="save-status" id="save-status">Unsaved</span>
        <span id="hmac-status" style="font-size:10px"></span>
        <button class="md-toggle-btn" id="md-toggle" onclick="toggleMarkdown()" title="Toggle Markdown Preview">MD</button>
        <button class="icon-btn" id="pin-btn" onclick="togglePin()" title="Pin/Unpin Note">
          <svg viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
        </button>
        <!-- Color label picker -->
        <div class="color-picker-wrap" id="color-picker-wrap">
          <div class="note-color-dot none active" id="color-none" onclick="setNoteColor(null)" title="No color" style="background:transparent;border:1.5px dashed var(--border2)"></div>
          <div class="note-color-dot" style="background:#c94c4c" onclick="setNoteColor('red')" data-color="red" title="Red - Urgent"></div>
          <div class="note-color-dot" style="background:#c97a4c" onclick="setNoteColor('orange')" data-color="orange" title="Orange"></div>
          <div class="note-color-dot" style="background:#c9a84c" onclick="setNoteColor('yellow')" data-color="yellow" title="Yellow"></div>
          <div class="note-color-dot" style="background:#4cc98a" onclick="setNoteColor('green')" data-color="green" title="Green - Personal"></div>
          <div class="note-color-dot" style="background:#4a8fc9" onclick="setNoteColor('blue')" data-color="blue" title="Blue - Work"></div>
          <div class="note-color-dot" style="background:#9a4cc9" onclick="setNoteColor('purple')" data-color="purple" title="Purple"></div>
        </div>
        <button class="icon-btn" id="note-lock-set-btn" onclick="openNoteLock()" title="Note-level Password Lock">
          <svg viewBox="0 0 24 24"><rect x="3" y="11" width="18" height="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>
        </button>
        <button class="icon-btn" id="note-relock-btn" onclick="lockCurrentNote()" title="Lock Note Now (Ctrl+Shift+L)" style="display:none;color:var(--info)">
          <svg viewBox="0 0 24 24" id="relock-icon"><rect x="3" y="11" width="18" height="11" rx="2"/><path class="relock-shackle" d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>
        </button>
        <button class="icon-btn" onclick="triggerImageUpload()" title="Add Image (or paste Ctrl+V)">
          <svg viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></svg>
        </button>
        <button class="icon-btn" onclick="exportEncrypted()" title="Encrypted Export">
          <svg viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
        </button>
        <button class="icon-btn" onclick="copyToClipboard()" title="Copy to clipboard (auto-clears in 30s)">
          <svg viewBox="0 0 24 24"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"/></svg>
        </button>
        <button class="icon-btn" onclick="openExportModal()" title="Export note (.txt/.md)">
          <svg viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
        </button>
        <button class="icon-btn" onclick="saveCurrentNote()" title="Save (Ctrl+S)">
          <svg viewBox="0 0 24 24"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg>
        </button>
        <button class="icon-btn" onclick="confirmDelete()" title="Move to Trash" style="color:var(--danger)">
          <svg viewBox="0 0 24 24"><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2L5 6"/><path d="M10 11v6"/><path d="M14 11v6"/><path d="M9 6V4h6v2"/></svg>
        </button>
      </div>
      <!-- Tags Row -->
      <div class="tags-wrap" id="tags-wrap">
        <div id="tag-chips-display"></div>
        <input class="tag-input" id="tag-input" type="text" placeholder="+ add tag…" maxlength="20" onkeydown="onTagKeydown(event)">
      </div>
      <!-- Find & Replace -->
      <div id="find-replace-bar" class="hidden">
        <input type="text" id="fr-find" placeholder="Find…" oninput="frHighlight()">
        <input type="text" id="fr-replace" placeholder="Replace…">
        <button class="fr-btn" onclick="frReplaceCurrent()">Replace</button>
        <button class="fr-btn" onclick="frReplaceAll()">All</button>
        <button class="fr-btn" onclick="frPrev()">↑</button>
        <button class="fr-btn" onclick="frNext()">↓</button>
        <span class="fr-info" id="fr-info"></span>
        <button id="fr-close" onclick="closeFindReplace()">✕</button>
      </div>
      <div class="editor-meta">
        <span id="note-created"></span>
        <span id="note-updated"></span>
        <span id="read-time" style="margin-left:auto"></span>
      </div>
      <div class="editor-body" id="editor-body-wrap">
        <!-- Note lock overlay -->
        <div class="note-lock-overlay hidden" id="note-lock-overlay">
          <div style="text-align:center;width:100%">
            <!-- Lock icon -->
            <div style="width:64px;height:64px;background:rgba(212,166,42,.12);border:1.5px solid rgba(212,166,42,.25);border-radius:50%;display:flex;align-items:center;justify-content:center;margin:0 auto 18px">
              <svg viewBox="0 0 24 24" style="width:28px;height:28px;stroke:var(--gold);fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round">
                <rect x="3" y="11" width="18" height="11" rx="2"/>
                <path d="M7 11V7a5 5 0 0 1 10 0v4"/>
              </svg>
            </div>
            <div style="font-size:16px;font-weight:600;color:#f1f1f1;margin-bottom:5px;font-family:'Playfair Display',serif">Note Locked</div>
            <div style="font-size:12px;color:rgba(255,255,255,.35);margin-bottom:24px;letter-spacing:.2px">This note has its own password</div>
            <input type="password" id="note-lock-input" placeholder="Enter note password…"
              style="width:100%;background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.12);border-radius:8px;padding:11px 14px;color:#f1f1f1;font-family:'Inter','DM Sans',sans-serif;font-size:14px;outline:none;margin-bottom:10px;transition:border-color .2s;box-sizing:border-box;"
              onfocus="this.style.borderColor='rgba(212,166,42,.5)'" onblur="this.style.borderColor='rgba(255,255,255,.12)'"
              onkeydown="if(event.key==='Enter')unlockNote()">
            <button onclick="unlockNote()" style="width:100%;padding:11px;background:var(--gold);color:#1a1200;border:none;border-radius:8px;font-family:'Inter','DM Sans',sans-serif;font-size:14px;font-weight:600;cursor:pointer;letter-spacing:.3px;transition:background .2s,transform .1s;" onmouseover="this.style.background='var(--gold2)'" onmouseout="this.style.background='var(--gold)'" onmousedown="this.style.transform='scale(.98)'" onmouseup="this.style.transform=''">Unlock</button>
            <div id="note-lock-err" style="font-size:11px;color:#f08080;margin-top:10px;min-height:16px"></div>
          </div>
        </div>
        <!-- Image Gallery -->
        <div id="img-gallery" class="img-gallery"></div>
        <!-- Drop zone -->
        <div class="img-dropzone" id="img-dropzone" onclick="triggerImageUpload()" 
          ondragover="onImgDragOver(event)" ondragleave="onImgDragLeave(event)" ondrop="onImgDrop(event)">
          <svg viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></svg>
          Click to add image, drag & drop, or <kbd style="background:var(--surface2);border:1px solid var(--border);border-radius:3px;padding:1px 5px;font-size:10px;font-family:'JetBrains Mono',monospace;margin-left:4px">Ctrl+V</kbd> to paste from clipboard
        </div>
        <input type="file" id="img-file-input" accept="image/*" multiple style="display:none" onchange="onImageFileSelected(event)">
        <textarea id="note-content" placeholder="Start writing… (supports Markdown)" oninput="markUnsaved();updateWordCount()"></textarea>
        <div class="md-preview hidden" id="md-preview"></div>
      </div>
      <div class="editor-toolbar">
        <div class="wc" id="word-count">0 words · 0 chars</div>
        <div style="display:flex;align-items:center;gap:8px">
          <span style="font-size:10px;color:var(--text3)">A</span>
          <input type="range" class="font-slider" id="font-slider" min="11" max="20" value="14" oninput="applyFontSize(this.value)" title="Font size">
          <span style="font-size:13px;color:var(--text3)">A</span>
          <button class="icon-btn" onclick="saveCurrentNote()" title="Save">
            <svg viewBox="0 0 24 24" style="width:15px;height:15px"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg>
          </button>
        </div>
      </div>
  </div><!-- end editor-content -->
</div><!-- end note-float-panel -->


<!-- LOCK OVERLAY (Idle/Auto) -->
<div id="lock-overlay" class="hidden">
  <div style="text-align:center">
    <div class="lock-icon" style="margin:0 auto 20px;width:72px;height:72px">
      <svg viewBox="0 0 24 24" style="width:32px;height:32px"><rect x="3" y="11" width="18" height="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>
    </div>
    <div style="font-family:'Playfair Display',serif;font-size:22px;color:var(--gold);margin-bottom:8px">Vault Locked</div>
    <div style="font-size:13px;color:var(--text3);margin-bottom:24px" id="lock-reason">Session locked due to inactivity</div>
    <div class="form-group" style="width:280px;margin:0 auto 16px">
      <label>Password to Resume</label>
      <input type="password" id="resume-password" placeholder="Enter your password" autocomplete="current-password" onkeydown="if(event.key==='Enter')resumeSession()">
    </div>
    <div id="alert-resume" class="alert danger" style="width:280px;margin:0 auto 12px"></div>
    <button class="btn btn-gold" onclick="resumeSession()" style="width:280px">Unlock</button>
    <div style="margin-top:12px">
      <button onclick="doLogout();hideOverlay();" style="background:none;border:none;color:var(--text3);font-size:12px;cursor:pointer;text-decoration:underline">Full Logout</button>
    </div>
  </div>
</div>

<!-- Delete Confirm Modal (soft delete → trash) -->
<div class="modal-overlay hidden" id="delete-modal">
  <div class="modal">
    <h3>🗑 Move to Trash?</h3>
    <p>"<span id="delete-note-name"></span>" will be moved to Trash. You can restore it or permanently delete it from there.</p>
    <div class="modal-btns">
      <button class="btn btn-outline" onclick="closeModal('delete-modal')">Cancel</button>
      <button class="btn" style="background:var(--danger);color:#fff" onclick="deleteCurrentNote()">Move to Trash</button>
    </div>
  </div>
</div>

<!-- Locked-Note Delete Password Modal -->
<div class="modal-overlay hidden" id="locked-delete-modal">
  <div class="modal" style="width:360px">
    <h3>🔒 Password Required to Delete</h3>
    <p style="font-size:13px;color:var(--text2);margin-bottom:16px">
      "<span id="locked-delete-note-name"></span>" is password locked. Enter the note password to confirm moving it to Trash.
    </p>
    <div id="locked-delete-alert" class="alert danger" style="margin-bottom:12px"></div>
    <div style="margin-bottom:14px">
      <label style="font-size:11px;font-weight:600;color:var(--text3);letter-spacing:.5px;text-transform:uppercase;display:block;margin-bottom:6px">Note Password</label>
      <input type="password" id="locked-delete-pass" placeholder="Enter note password…"
        style="width:100%;background:var(--surface2);border:1px solid var(--border);border-radius:var(--radius-sm);padding:10px 13px;color:var(--text);font-family:'Inter','DM Sans',sans-serif;font-size:14px;outline:none;"
        onkeydown="if(event.key==='Enter')verifyLockedNoteDelete()">
    </div>
    <div class="modal-btns">
      <button class="btn btn-outline" onclick="closeModal('locked-delete-modal');document.getElementById('locked-delete-pass').value=''">Cancel</button>
      <button class="btn" style="background:var(--danger);color:#fff" onclick="verifyLockedNoteDelete()">
        🗑 Confirm &amp; Move to Trash
      </button>
    </div>
  </div>
</div>

<!-- TRASH MODAL -->
<div class="modal-overlay hidden" id="trash-modal">
  <div class="modal" style="width:480px">
    <h3>🗑 Trash</h3>
    <p>Deleted notes are stored here. Restore or permanently delete them.</p>
    <div id="trash-pin-gate" style="display:none;margin-bottom:12px;background:var(--surface2);border:1px solid var(--border);border-radius:8px;padding:16px;text-align:center">
      <div style="font-size:13px;color:var(--text2);margin-bottom:10px">🔒 Enter Trash PIN to access</div>
      <div class="trash-pin-dots" id="trash-pin-dots-wrap">
        <div class="trash-pin-dot" id="tpd0"></div>
        <div class="trash-pin-dot" id="tpd1"></div>
        <div class="trash-pin-dot" id="tpd2"></div>
        <div class="trash-pin-dot" id="tpd3"></div>
        <div class="trash-pin-dot" style="display:none" id="tpd4"></div>
        <div class="trash-pin-dot" style="display:none" id="tpd5"></div>
        <div class="trash-pin-dot" style="display:none" id="tpd6"></div>
        <div class="trash-pin-dot" style="display:none" id="tpd7"></div>
      </div>
      <input type="password" id="trash-pin-input" maxlength="8" pattern="[0-9]*" inputmode="numeric"
        placeholder="PIN" style="text-align:center;letter-spacing:6px;font-size:18px;width:140px;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-sm);padding:8px 12px;color:var(--text);font-family:'DM Sans',sans-serif;outline:none;margin-bottom:10px"
        oninput="onTrashPinInput()" onkeydown="if(event.key==='Enter')verifyTrashPin()">
      <br>
      <div id="trash-pin-err" style="font-size:11px;color:var(--danger);margin-bottom:8px"></div>
      <button onclick="verifyTrashPin()" style="padding:7px 20px;background:var(--gold);color:#1a1200;border:none;border-radius:var(--radius-sm);font-family:'DM Sans',sans-serif;font-size:13px;font-weight:500;cursor:pointer">Unlock Trash</button>
    </div>
    <div id="trash-contents" style="display:none">
      <div id="trash-list" style="max-height:300px;overflow-y:auto;margin-bottom:12px"></div>
      <div style="display:flex;gap:8px">
        <button class="btn btn-outline" style="flex:1" onclick="restoreAllFromTrash()">↩ Restore All</button>
        <button class="btn" style="flex:1;background:rgba(201,76,76,.15);border:1px solid rgba(201,76,76,.3);color:#f08080" onclick="emptyTrash()">🔥 Empty Trash</button>
      </div>
    </div>
    <div style="margin-top:12px;display:flex;gap:8px;align-items:center">
      <button class="btn btn-outline" onclick="closeModal('trash-modal');S._trashUnlocked=false">Close</button>
      <button class="btn btn-outline" style="font-size:11px" onclick="openTrashPinSettings()" id="trash-pin-settings-btn">⚙ Trash PIN Settings</button>
    </div>
  </div>
</div>

<!-- TRASH PIN SETUP MODAL -->
<div class="modal-overlay hidden" id="trash-pin-setup-modal">
  <div class="modal" style="width:380px">
    <h3>🔐 Trash PIN Settings</h3>
    <p id="trash-pin-setup-desc">Set a 4–8 digit PIN to protect the Trash.</p>

    <!-- Current PIN row — only shown when a PIN already exists -->
    <div id="trash-pin-current-row" style="display:none;margin-bottom:12px">
      <label style="font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:.4px;display:block;margin-bottom:5px">Current Trash PIN <span style="color:var(--danger)">*</span></label>
      <input type="password" id="trash-pin-current" placeholder="Enter current PIN to confirm" maxlength="8" pattern="[0-9]*" inputmode="numeric"
        style="width:100%;background:var(--surface2);border:1px solid var(--border);border-radius:var(--radius-sm);padding:9px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:13px;outline:none;letter-spacing:6px;text-align:center">
    </div>

    <div style="margin-bottom:12px">
      <label style="font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:.4px;display:block;margin-bottom:5px">New Trash PIN (4–8 digits, leave blank to remove)</label>
      <input type="password" id="trash-pin-new" placeholder="e.g. 12345678" maxlength="8" pattern="[0-9]*" inputmode="numeric"
        style="width:100%;background:var(--surface2);border:1px solid var(--border);border-radius:var(--radius-sm);padding:9px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:13px;outline:none;letter-spacing:6px;text-align:center">
    </div>
    <div style="margin-bottom:16px">
      <label style="font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:.4px;display:block;margin-bottom:5px">Confirm New PIN</label>
      <input type="password" id="trash-pin-new-confirm" placeholder="Repeat PIN" maxlength="8" pattern="[0-9]*" inputmode="numeric"
        style="width:100%;background:var(--surface2);border:1px solid var(--border);border-radius:var(--radius-sm);padding:9px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:13px;outline:none;letter-spacing:6px;text-align:center">
    </div>
    <div id="trash-pin-setup-err" class="alert danger" style="margin-bottom:12px"></div>
    <div style="display:flex;gap:8px">
      <button class="btn btn-gold" style="flex:1" onclick="saveTrashPin()">Save PIN</button>
      <button id="trash-pin-remove-btn" class="btn" style="flex:1;background:rgba(201,76,76,.15);border:1px solid rgba(201,76,76,.3);color:#f08080;display:none" onclick="removeTrashPin()">🗑 Remove PIN</button>
      <button class="btn btn-outline" style="flex:1" onclick="closeModal('trash-pin-setup-modal')">Cancel</button>
    </div>
  </div>
</div>

<!-- TEMPLATE MODAL -->
<div class="modal-overlay hidden" id="template-modal">
  <div class="modal" style="width:420px">
    <h3>📋 New Note</h3>
    <p>Choose a template or start blank</p>
    <div class="template-grid">
      <div class="template-card" onclick="applyTemplate('blank')">
        <div class="template-icon">📝</div>
        <div class="template-name">Blank Note</div>
        <div class="template-desc">Start from scratch</div>
      </div>
      <div class="template-card" onclick="applyTemplate('daily')">
        <div class="template-icon">📅</div>
        <div class="template-name">Daily Journal</div>
        <div class="template-desc">Date + mood + log</div>
      </div>
      <div class="template-card" onclick="applyTemplate('meeting')">
        <div class="template-icon">🤝</div>
        <div class="template-name">Meeting Notes</div>
        <div class="template-desc">Attendees, agenda, actions</div>
      </div>
      <div class="template-card" onclick="applyTemplate('todo')">
        <div class="template-icon">✅</div>
        <div class="template-name">To-Do List</div>
        <div class="template-desc">Interactive checkboxes</div>
      </div>
      <div class="template-card" onclick="applyTemplate('idea')">
        <div class="template-icon">💡</div>
        <div class="template-name">Idea Capture</div>
        <div class="template-desc">Quick idea + details</div>
      </div>
      <div class="template-card" onclick="applyTemplate('password')">
        <div class="template-icon">🔐</div>
        <div class="template-name">Credentials</div>
        <div class="template-desc">Secure logins template</div>
      </div>
    </div>
    <button class="btn btn-outline" onclick="closeModal('template-modal')">Cancel</button>
  </div>
</div>

<!-- FOLDER MANAGER MODAL -->
<div class="modal-overlay hidden" id="folder-modal">
  <div class="modal" style="width:400px">
    <h3>📁 Folder Manager</h3>
    <p>Organize your notes into folders</p>
    <div style="display:flex;gap:8px;margin-bottom:14px">
      <input type="text" id="folder-new-name" placeholder="New folder name…" maxlength="30"
        style="flex:1;background:var(--surface2);border:1px solid var(--border);border-radius:var(--radius-sm);padding:8px 12px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:13px;outline:none"
        onkeydown="if(event.key==='Enter')addFolder()">
      <button class="btn btn-gold" style="width:auto;padding:8px 16px" onclick="addFolder()">Add</button>
    </div>
    <div id="folder-manage-list" style="max-height:260px;overflow-y:auto;margin-bottom:16px"></div>
    <div style="display:flex;gap:8px">
      <button class="btn btn-outline" onclick="closeModal('folder-modal')">Done</button>
    </div>
  </div>
</div>

<!-- NOTE EXPORT MODAL -->
<div class="modal-overlay hidden" id="note-export-modal">
  <div class="modal" style="width:380px">
    <h3>📤 Export Note</h3>
    <p>Download this note as a plain file</p>
    <div class="export-format-wrap">
      <button class="export-fmt-btn active" id="exp-txt-btn" onclick="selectExportFmt('txt')">📄 .txt</button>
      <button class="export-fmt-btn" id="exp-md-btn" onclick="selectExportFmt('md')">🖊 .md</button>
    </div>
    <div style="margin-bottom:16px;font-size:12px;color:var(--text3)" id="export-preview-label">
      Exports the note title + content as plain text.
    </div>
    <div style="display:flex;gap:8px">
      <button class="btn btn-gold" style="flex:1" onclick="doExportPlain()">⬇ Download</button>
      <button class="btn btn-outline" style="flex:1" onclick="closeModal('note-export-modal')">Cancel</button>
    </div>
  </div>
</div>

<!-- Audit Log Modal -->
<div class="modal-overlay hidden" id="audit-modal">
  <div class="modal" style="width:480px">
    <h3>Login Audit Log</h3>
    <p>Recent login attempts (stored on USB)</p>
    <div class="audit-list" id="audit-list"></div>
    <div style="margin-top:16px">
      <button class="btn btn-outline" onclick="closeModal('audit-modal')">Close</button>
    </div>
  </div>
</div>

<!-- Settings Modal -->
<div class="modal-overlay hidden" id="settings-modal">
  <div class="modal" style="width:460px">
    <h3>🔒 Security Settings</h3>
    <p>Configure auto-lock and security preferences</p>
    <div id="settings-content">
      <div class="settings-row">
        <div class="settings-label">Auto-Lock on Idle
          <small>Lock after inactivity</small>
        </div>
        <div style="display:flex;align-items:center;gap:8px">
          <input class="small-input" type="number" id="idle-minutes" min="1" max="120" value="5"> min
          <button class="toggle" id="idle-toggle" onclick="toggleSetting('idle')"></button>
        </div>
      </div>
      <div class="settings-row">
        <div class="settings-label">Clipboard Auto-Clear
          <small>Clear clipboard after 30 seconds</small>
        </div>
        <button class="toggle on" id="clip-toggle" onclick="toggleSetting('clip')"></button>
      </div>
      <div class="settings-row">
        <div class="settings-label">USB Presence Check
          <small>Lock if USB is unplugged</small>
        </div>
        <button class="toggle on" id="usb-toggle" onclick="toggleSetting('usb')"></button>
      </div>
      <div class="settings-row">
        <div class="settings-label">Note Encryption (AES-256-GCM)
          <small>Encrypt all note content</small>
        </div>
        <button class="toggle on" id="enc-toggle" onclick="toggleSetting('enc')"></button>
      </div>
      <div class="settings-row">
        <div class="settings-label">Encrypt Titles
          <small>Encrypt note titles too</small>
        </div>
        <button class="toggle on" id="enc-title-toggle" onclick="toggleSetting('encTitle')"></button>
      </div>
      <div class="settings-row">
        <div class="settings-label">HMAC Integrity Check
          <small>Cryptographic signature per note</small>
        </div>
        <button class="toggle on" id="hmac-toggle" onclick="toggleSetting('hmac')"></button>
      </div>
    </div>
    <div style="margin-top:20px;display:flex;gap:10px">
      <button class="btn btn-gold" onclick="saveSettings()">Save Settings</button>
      <button class="btn btn-outline" onclick="closeModal('settings-modal')">Cancel</button>
    </div>
  </div>
</div>

<!-- Encrypted Export Modal -->
<div class="modal-overlay hidden" id="export-modal">
  <div class="modal">
    <h3>📦 Encrypted Export</h3>
    <p>Export current note as an AES-256-GCM encrypted backup file. Import with your vault password.</p>
    <div style="margin-bottom:12px">
      <button class="btn btn-gold" onclick="doExport()">Export Encrypted Backup</button>
    </div>
    <button class="btn btn-outline" onclick="closeModal('export-modal')">Cancel</button>
  </div>
</div>

<!-- Image Lightbox -->
<div id="img-lightbox" class="hidden" onclick="closeLightbox()">
  <button class="lb-close" onclick="closeLightbox()">✕</button>
  <img id="lb-img" src="" alt="Note image">
  <div class="lb-info" id="lb-info"></div>
</div>

<!-- Note Lock Setup Modal -->
<div class="modal-overlay hidden" id="note-pass-modal">
  <div class="modal" style="width:400px">
    <h3>🔒 Note Password</h3>
    <p id="note-pass-modal-desc">Lock this note with its own password</p>
    <div id="note-pass-set-section">
      <!-- Old password row — only shown when note already has a password -->
      <div id="note-old-pass-row" style="display:none;margin-bottom:12px">
        <label style="font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:.4px;display:block;margin-bottom:5px">Current Note Password <span style="color:var(--danger)">*</span></label>
        <input type="password" id="note-old-pass" placeholder="Enter current note password" style="width:100%;background:var(--surface2);border:1px solid var(--border);border-radius:var(--radius-sm);padding:9px 12px;color:var(--text);font-family:'Inter','DM Sans',sans-serif;font-size:13px;outline:none;">
      </div>
      <div style="margin-bottom:12px">
        <label style="font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:.4px;display:block;margin-bottom:5px">New Note Password</label>
        <input type="password" id="note-new-pass" placeholder="Set a password for this note" style="width:100%;background:var(--surface2);border:1px solid var(--border);border-radius:var(--radius-sm);padding:9px 12px;color:var(--text);font-family:'Inter','DM Sans',sans-serif;font-size:13px;outline:none;">
      </div>
      <div style="margin-bottom:16px">
        <label style="font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:.4px;display:block;margin-bottom:5px">Confirm New Password</label>
        <input type="password" id="note-new-pass-confirm" placeholder="Repeat password" style="width:100%;background:var(--surface2);border:1px solid var(--border);border-radius:var(--radius-sm);padding:9px 12px;color:var(--text);font-family:'Inter','DM Sans',sans-serif;font-size:13px;outline:none;">
      </div>
      <div id="note-pass-alert" class="alert danger" style="margin-bottom:12px"></div>
      <div style="display:flex;gap:8px">
        <button class="btn btn-gold" onclick="setNoteLock()" style="flex:1">Set Lock</button>
        <button class="btn" onclick="removeNoteLock()" id="note-remove-lock-btn" style="flex:1;background:rgba(201,76,76,.15);border:1px solid rgba(201,76,76,.3);color:#f08080;display:none">Remove Lock</button>
      </div>
    </div>
    <div style="margin-top:12px">
      <button class="btn btn-outline" onclick="closeModal('note-pass-modal')">Cancel</button>
    </div>
  </div>
</div>

<!-- Appearance Settings Modal -->
<div class="modal-overlay hidden" id="appearance-modal">
  <div class="modal" style="width:520px;max-height:92vh;overflow-y:auto;background:rgba(22,26,30,.97);backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);border:1px solid rgba(212,166,42,.18);box-shadow:0 32px 80px rgba(0,0,0,.7),0 0 0 1px rgba(212,166,42,.06),inset 0 1px 0 rgba(255,255,255,.06)">
    <div style="display:flex;align-items:center;gap:10px;margin-bottom:4px">
      <div style="width:36px;height:36px;border-radius:10px;background:rgba(212,166,42,.12);border:1px solid rgba(212,166,42,.25);display:flex;align-items:center;justify-content:center;font-size:17px;animation:appearLockPulse 2s ease infinite">🎨</div>
      <div>
        <h3 style="margin:0;font-size:16px">Appearance</h3>
        <p style="margin:0;font-size:12px;color:var(--text3)">Live preview — changes apply instantly</p>
      </div>
    </div>

    <!-- LIVE PREVIEW STRIP -->
    <div id="appearance-preview-strip" style="margin:14px 0 8px;background:var(--bg);border:1px solid var(--border);border-radius:10px;padding:14px 18px;position:relative;overflow:hidden;transition:all .3s">
      <div style="position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,transparent,var(--gold),transparent);animation:previewScan 2.5s ease infinite"></div>
      <div style="font-family:'Playfair Display',serif;font-size:calc(var(--editor-font-size,14px) * 1.2px);color:var(--gold);font-weight:600;margin-bottom:4px;transition:font-size .15s">SecureNote Preview</div>
      <div style="font-family:'JetBrains Mono',monospace;font-size:var(--editor-font-size,14px);color:var(--text2);line-height:1.6;transition:font-size .15s">The quick brown fox jumps over the lazy dog. Your notes look exactly like this.</div>
      <div style="margin-top:8px;display:flex;gap:6px">
        <span id="ap-badge-1" style="font-size:10px;padding:2px 8px;border-radius:10px;background:rgba(76,201,138,.1);border:1px solid rgba(76,201,138,.3);color:var(--success);transition:.3s">🟢 Encrypted</span>
        <span id="ap-badge-2" style="font-size:10px;padding:2px 8px;border-radius:10px;background:rgba(212,166,42,.1);border:1px solid var(--gold-dim);color:var(--gold);transition:.3s">🔒 Secured</span>
        <span id="ap-badge-3" style="font-size:10px;padding:2px 8px;border-radius:10px;background:rgba(74,143,201,.1);border:1px solid rgba(74,143,201,.3);color:var(--info);transition:.3s">AES-256</span>
      </div>
    </div>

    <!-- FONT SIZE -->
    <div class="settings-row" style="flex-direction:column;align-items:flex-start;gap:8px">
      <div class="settings-label" style="width:100%;display:flex;justify-content:space-between">
        <span>Editor Font Size</span>
        <span style="background:var(--surface2);border:1px solid var(--border);border-radius:6px;padding:2px 10px;font-size:13px;color:var(--gold);font-family:'JetBrains Mono',monospace" id="font-size-label">14</span>px
      </div>
      <div class="font-slider-wrap" style="width:100%">
        <span style="font-size:10px;color:var(--text3)">11</span>
        <input type="range" class="font-slider" id="font-slider-modal" min="11" max="22" value="14" oninput="livePreviewFontSize(this.value)" style="flex:1">
        <span style="font-size:13px;color:var(--text3)">22</span>
      </div>
    </div>

    <!-- ACCENT COLOR -->
    <div class="settings-row" style="flex-direction:column;align-items:flex-start;gap:10px">
      <div class="settings-label">Accent Color <small>Changes the highlight color throughout the app</small></div>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <div class="color-swatch active" style="background:#c9a84c" onclick="livePreviewAccent('gold')" data-accent="gold" title="Gold (Default)"></div>
        <div class="color-swatch" style="background:#4a8fc9" onclick="livePreviewAccent('blue')" data-accent="blue" title="Sapphire Blue"></div>
        <div class="color-swatch" style="background:#4cc98a" onclick="livePreviewAccent('green')" data-accent="green" title="Emerald Green"></div>
        <div class="color-swatch" style="background:#c94c8a" onclick="livePreviewAccent('rose')" data-accent="rose" title="Rose Pink"></div>
        <div class="color-swatch" style="background:#c97a4c" onclick="livePreviewAccent('amber')" data-accent="amber" title="Amber Orange"></div>
        <div class="color-swatch" style="background:#9a4cc9" onclick="livePreviewAccent('violet')" data-accent="violet" title="Deep Violet"></div>
        <div class="color-swatch" style="background:#c9a84c;border:2px solid #a07820;background:linear-gradient(135deg,#c9a84c,#8b6914)" onclick="livePreviewAccent('dark-gold')" data-accent="dark-gold" title="Dark Gold"></div>
        <div class="color-swatch" style="background:#22ff22" onclick="livePreviewAccent('hacker')" data-accent="hacker" title="Hacker Green"></div>
        <div class="color-swatch" style="background:#4a6fa5" onclick="livePreviewAccent('midnight')" data-accent="midnight" title="Midnight Blue"></div>
        <div class="color-swatch" style="background:#e0e8f0" onclick="livePreviewAccent('frost')" data-accent="frost" title="Frost White"></div>
        <div class="color-swatch" style="background:#ffffff" onclick="livePreviewAccent('amoled')" data-accent="amoled" title="AMOLED White"></div>
      </div>
    </div>

    <!-- THEME PRESETS -->
    <div style="margin-top:4px;margin-bottom:4px">
      <div style="font-size:11px;color:var(--text3);font-weight:600;letter-spacing:.5px;text-transform:uppercase;margin-bottom:8px">Theme Presets</div>
      <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px">
        <button class="appearance-theme-btn" onclick="applyThemePreset('default')" style="padding:8px;border-radius:8px;border:1px solid var(--border);background:var(--surface2);cursor:pointer;font-size:11px;color:var(--text2);font-family:'Inter',sans-serif;transition:.2s">
          <div style="width:100%;height:20px;background:linear-gradient(135deg,#111315,#1a1d21);border-radius:4px;margin-bottom:5px;border:1px solid #2e3440"></div>
          Dark Vault
        </button>
        <button class="appearance-theme-btn" onclick="applyThemePreset('pure-black')" style="padding:8px;border-radius:8px;border:1px solid var(--border);background:var(--surface2);cursor:pointer;font-size:11px;color:var(--text2);font-family:'Inter',sans-serif;transition:.2s">
          <div style="width:100%;height:20px;background:#000;border-radius:4px;margin-bottom:5px;border:1px solid #111"></div>
          Pure Black
        </button>
        <button class="appearance-theme-btn" onclick="applyThemePreset('hacker')" style="padding:8px;border-radius:8px;border:1px solid rgba(0,255,0,.2);background:rgba(0,20,0,.5);cursor:pointer;font-size:11px;color:#22ff22;font-family:'JetBrains Mono',monospace;transition:.2s">
          <div style="width:100%;height:20px;background:linear-gradient(135deg,#001200,#002200);border-radius:4px;margin-bottom:5px;border:1px solid rgba(0,255,0,.3)"></div>
          Hacker
        </button>
        <button class="appearance-theme-btn" onclick="applyThemePreset('midnight')" style="padding:8px;border-radius:8px;border:1px solid rgba(74,111,165,.35);background:rgba(10,15,30,.7);cursor:pointer;font-size:11px;color:#6b9bd2;font-family:'Inter',sans-serif;transition:.2s">
          <div style="width:100%;height:20px;background:linear-gradient(135deg,#060b1a,#0d1830);border-radius:4px;margin-bottom:5px;border:1px solid rgba(74,111,165,.3)"></div>
          Midnight Blue
        </button>
        <button class="appearance-theme-btn" onclick="applyThemePreset('frost')" style="padding:8px;border-radius:8px;border:1px solid rgba(200,220,240,.4);background:rgba(240,248,255,.08);cursor:pointer;font-size:11px;color:#a0bcd0;font-family:'Inter',sans-serif;transition:.2s">
          <div style="width:100%;height:20px;background:linear-gradient(135deg,#1a2530,#253040);border-radius:4px;margin-bottom:5px;border:1px solid rgba(200,220,240,.25)"></div>
          Frost
        </button>
        <button class="appearance-theme-btn" onclick="applyThemePreset('light')" style="padding:8px;border-radius:8px;border:1px solid #ddd8ce;background:#f5f3ee;cursor:pointer;font-size:11px;color:#4a4440;font-family:'Inter',sans-serif;transition:.2s">
          <div style="width:100%;height:20px;background:linear-gradient(135deg,#f5f3ee,#e8e4dc);border-radius:4px;margin-bottom:5px;border:1px solid #ddd8ce"></div>
          Light
        </button>
      </div>
    </div>

    <!-- NOTE LIST DENSITY -->
    <div class="settings-row">
      <div class="settings-label">Note List Density<small>How compact the note list looks</small></div>
      <div class="view-toggle-wrap">
        <button class="view-toggle-btn active" id="view-comfortable" onclick="setViewMode('comfortable')">Comfortable</button>
        <button class="view-toggle-btn" id="view-compact" onclick="setViewMode('compact')">Compact</button>
      </div>
    </div>

    <!-- SECURITY VISUALS -->
    <div style="margin:8px 0 0">
      <div style="font-size:11px;color:var(--text3);font-weight:600;letter-spacing:.5px;text-transform:uppercase;margin-bottom:8px">🔐 Security Status</div>
      <div style="display:flex;flex-wrap:wrap;gap:6px" id="appearance-sec-pills">
        <span class="sec-pill ok"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="20 6 9 17 4 12"/></svg> AES-256-GCM Active</span>
        <span class="sec-pill ok"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="20 6 9 17 4 12"/></svg> Local Encryption Enabled</span>
        <span class="sec-pill ok"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="20 6 9 17 4 12"/></svg> USB Vault Active</span>
        <span class="sec-pill warn"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M10.29 3.86L1.82 18a2 2 0 001.71 3h16.94a2 2 0 001.71-3L13.71 3.86a2 2 0 00-3.42 0z"/></svg> PBKDF2 310k Iterations</span>
      </div>
    </div>

    <!-- ANIMATED LOCK ICON -->
    <div style="display:flex;align-items:center;justify-content:center;gap:16px;padding:14px;background:var(--surface2);border:1px solid var(--border);border-radius:10px;margin-top:10px">
      <div id="appearance-lock-anim" style="position:relative;width:44px;height:44px">
        <svg viewBox="0 0 24 24" fill="none" stroke="var(--gold)" stroke-width="1.5" style="width:44px;height:44px;filter:drop-shadow(0 0 8px rgba(212,166,42,.4));animation:appearLockPulse 2s ease infinite">
          <rect x="3" y="11" width="18" height="11" rx="2"/>
          <path class="lock-shackle-anim" d="M7 11V7a5 5 0 0 1 10 0v4"/>
        </svg>
        <div style="position:absolute;inset:0;border-radius:50%;background:radial-gradient(circle,rgba(212,166,42,.15),transparent 70%);animation:appearLockPulse 2s ease infinite"></div>
      </div>
      <div>
        <div style="font-size:12px;font-weight:600;color:var(--text);margin-bottom:4px">Vault Mode Active</div>
        <div style="font-size:11px;color:var(--text3)">Your notes are end-to-end encrypted</div>
        <div style="margin-top:6px;display:flex;gap:6px">
          <span style="font-size:9px;padding:2px 6px;border-radius:6px;background:rgba(76,201,138,.12);border:1px solid rgba(76,201,138,.25);color:var(--success)">🟢 Active</span>
          <span style="font-size:9px;padding:2px 6px;border-radius:6px;background:rgba(212,166,42,.1);border:1px solid rgba(212,166,42,.25);color:var(--gold)">🔐 Protected</span>
        </div>
      </div>
    </div>

    <!-- SMART DASHBOARD -->
    <div style="margin-top:10px">
      <div style="font-size:11px;color:var(--text3);font-weight:600;letter-spacing:.5px;text-transform:uppercase;margin-bottom:8px">📊 Vault Dashboard</div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:6px" id="appearance-dashboard">
        <div style="background:var(--surface2);border:1px solid var(--border);border-radius:8px;padding:10px 12px">
          <div style="font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.4px;margin-bottom:4px">Total Notes</div>
          <div style="font-size:20px;font-weight:700;color:var(--gold);font-family:'JetBrains Mono',monospace" id="dash-total-notes">—</div>
        </div>
        <div style="background:var(--surface2);border:1px solid var(--border);border-radius:8px;padding:10px 12px">
          <div style="font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.4px;margin-bottom:4px">Locked Notes</div>
          <div style="font-size:20px;font-weight:700;color:var(--info);font-family:'JetBrains Mono',monospace" id="dash-locked-notes">—</div>
        </div>
        <div style="background:var(--surface2);border:1px solid var(--border);border-radius:8px;padding:10px 12px">
          <div style="font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.4px;margin-bottom:4px">In Trash</div>
          <div style="font-size:20px;font-weight:700;color:var(--danger);font-family:'JetBrains Mono',monospace" id="dash-trash-notes">—</div>
        </div>
        <div style="background:var(--surface2);border:1px solid var(--border);border-radius:8px;padding:10px 12px">
          <div style="font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.4px;margin-bottom:4px">Pinned</div>
          <div style="font-size:20px;font-weight:700;color:var(--success);font-family:'JetBrains Mono',monospace" id="dash-pinned-notes">—</div>
        </div>
      </div>
    </div>

    <div style="margin-top:16px;display:flex;gap:10px">
      <button class="btn btn-gold" onclick="saveAppearance()">✓ Save & Apply</button>
      <button class="btn btn-outline" onclick="cancelAppearance()">Cancel</button>
    </div>
  </div>
</div>

<!-- Account Settings Modal -->
<div class="modal-overlay hidden" id="acct-modal">
  <div class="modal" style="width:420px">
    <h3>👤 Account Settings</h3>
    <p style="margin-bottom:16px">Change your display name or vault password</p>

    <!-- Change Name -->
    <div class="acct-section">
      <div class="acct-section-title">Display Name</div>
      <div class="acct-input-group">
        <div class="acct-input-row">
          <label>New Username</label>
          <input type="text" id="acct-new-name" placeholder="Enter new username" autocomplete="off">
        </div>
        <div>
          <button class="acct-save-btn" onclick="saveAccountName()">✓ &nbsp;Update Name</button>
        </div>
      </div>
    </div>

    <!-- Change Password -->
    <div class="acct-section">
      <div class="acct-section-title">Change Password</div>
      <div class="acct-input-group">
        <div class="acct-input-row">
          <label>Current Password</label>
          <input type="password" id="acct-cur-pass" placeholder="Your current password" autocomplete="current-password">
        </div>
        <div class="acct-input-row">
          <label>New Password</label>
          <input type="password" id="acct-new-pass" placeholder="New password (min 4 chars)" autocomplete="new-password">
        </div>
        <div class="acct-input-row">
          <label>Confirm New Password</label>
          <input type="password" id="acct-confirm-pass" placeholder="Repeat new password" autocomplete="new-password">
        </div>
        <div>
          <button class="acct-save-btn" onclick="saveAccountPassword()">✓ &nbsp;Update Password</button>
        </div>
      </div>
    </div>

    <div id="acct-alert" class="alert danger"></div>
    <div style="margin-top:16px">
      <button class="btn btn-outline" onclick="closeModal('acct-modal');clearAcctFields()">Close</button>
    </div>
  </div>
</div>

<!-- Toast -->
<div class="toast" id="toast"></div>

<script>
// ====== SECURITY STATE ======
let S = {
  dirHandle: null,
  notesDir: null,
  username: '',
  notes: [],
  currentNoteId: null,
  unsaved: false,
  setupStep: 1,
  setupCreds: null,
  setupDirHandle: null,
  // Session state
  encKey: null,
  macKey: null,
  isDecoy: false,
  // Security settings
  settings: {
    idleEnabled: true,
    idleMinutes: 5,
    clipboardClear: true,
    usbCheck: true,
    encryptContent: true,
    encryptTitle: true,
    hmac: true,
  },
  // Runtime counters
  idleTimer: null,
  usbCheckTimer: null,
  clipboardTimer: null,
  clipCountdown: null,
  escCount: 0,
  escTimer: null,
  lockoutUntil: 0,
  lockoutTimer: null,
  pendingUsername: null,
  pendingIsDecoy: false,
  noteImages: {},
  theme: 'auto',
  // NEW v4 state
  sessionWarnTimer: null,
  sessionWarnCountdown: null,
  mdMode: false,           // markdown preview toggle
  activeTagFilter: null,   // tag filter in sidebar
  noteLockedUnlocked: {},  // {noteId: true} if unlocked this session
  appearance: {
    fontSize: 14,
    accent: 'gold',
    viewMode: 'comfortable',
  },
  frMatches: [],
  frIndex: 0,
  activeFolderFilter: null,
  _trashUnlocked: false,
};

// ====== INDEXEDDB ======
function openDB(){
  return new Promise((res,rej)=>{
    const r=indexedDB.open('SecureNoteDB2',1);
    r.onupgradeneeded=e=>e.target.result.createObjectStore('store');
    r.onsuccess=e=>res(e.target.result);
    r.onerror=rej;
  });
}
async function dbGet(key){
  const db=await openDB();
  return new Promise((res,rej)=>{
    const t=db.transaction('store','readonly');
    const r=t.objectStore('store').get(key);
    r.onsuccess=e=>res(e.target.result);
    r.onerror=rej;
  });
}
async function dbSet(key,val){
  const db=await openDB();
  return new Promise((res,rej)=>{
    const t=db.transaction('store','readwrite');
    const r=t.objectStore('store').put(val,key);
    r.onsuccess=()=>res();
    r.onerror=rej;
  });
}
async function dbDel(key){
  const db=await openDB();
  return new Promise((res,rej)=>{
    const t=db.transaction('store','readwrite');
    const r=t.objectStore('store').delete(key);
    r.onsuccess=()=>res();
    r.onerror=rej;
  });
}

// ====== CRYPTO (AES-256-GCM) ======
const ENC = new TextEncoder();
const DEC = new TextDecoder();

async function hashPassword(pass, salt){
  const data = ENC.encode(pass+salt);
  const buf = await crypto.subtle.digest('SHA-256', data);
  return Array.from(new Uint8Array(buf)).map(b=>b.toString(16).padStart(2,'0')).join('');
}

async function deriveKey(password, saltHex){
  const saltBytes = hexToBytes(saltHex);
  const keyMaterial = await crypto.subtle.importKey('raw', ENC.encode(password), 'PBKDF2', false, ['deriveKey']);
  const key = await crypto.subtle.deriveKey(
    {name:'PBKDF2', salt:saltBytes, iterations:310000, hash:'SHA-256'},
    keyMaterial,
    {name:'AES-GCM', length:256},
    false,
    ['encrypt','decrypt']
  );
  return key;
}

async function deriveMacKey(password, saltHex){
  const saltBytes = hexToBytes(saltHex);
  const keyMaterial = await crypto.subtle.importKey('raw', ENC.encode(password+'_mac'), 'PBKDF2', false, ['deriveKey']);
  const key = await crypto.subtle.deriveKey(
    {name:'PBKDF2', salt:saltBytes, iterations:100000, hash:'SHA-256'},
    keyMaterial,
    {name:'HMAC', hash:'SHA-256', length:256},
    false,
    ['sign','verify']
  );
  return key;
}

async function aesEncrypt(key, plaintext){
  const iv = crypto.getRandomValues(new Uint8Array(12));
  const ct = await crypto.subtle.encrypt({name:'AES-GCM', iv}, key, ENC.encode(plaintext));
  const out = new Uint8Array(iv.length + ct.byteLength);
  out.set(iv, 0);
  out.set(new Uint8Array(ct), iv.length);
  return btoa(String.fromCharCode(...out));
}

async function aesDecrypt(key, b64){
  const raw = Uint8Array.from(atob(b64), c=>c.charCodeAt(0));
  const iv = raw.slice(0, 12);
  const ct = raw.slice(12);
  const pt = await crypto.subtle.decrypt({name:'AES-GCM', iv}, key, ct);
  return DEC.decode(pt);
}

async function hmacSign(key, data){
  const sig = await crypto.subtle.sign('HMAC', key, ENC.encode(data));
  return Array.from(new Uint8Array(sig)).map(b=>b.toString(16).padStart(2,'0')).join('');
}

async function hmacVerify(key, data, sig){
  const expected = await hmacSign(key, data);
  return expected === sig;
}

function genSalt(){
  return Array.from(crypto.getRandomValues(new Uint8Array(32))).map(b=>b.toString(16).padStart(2,'0')).join('');
}
function hexToBytes(hex){
  const b=new Uint8Array(hex.length/2);
  for(let i=0;i<hex.length;i+=2)b[i/2]=parseInt(hex.slice(i,i+2),16);
  return b;
}
function genId(){
  return Date.now().toString(36)+Math.random().toString(36).slice(2,8);
}

// ====== FILE SYSTEM ======
async function getOrCreateDir(parent,name){return parent.getDirectoryHandle(name,{create:true});}
async function writeFile(dir,name,content){
  const fh=await dir.getFileHandle(name,{create:true});
  const w=await fh.createWritable();
  await w.write(content);
  await w.close();
}
async function readFile(dir,name){
  try{const fh=await dir.getFileHandle(name);const f=await fh.getFile();return await f.text();}
  catch{return null;}
}
async function deleteFileFS(dir,name){try{await dir.removeEntry(name);}catch{}}
async function listFiles(dir){
  const files=[];
  for await(const entry of dir.values()){if(entry.kind==='file')files.push(entry.name);}
  return files;
}

// Secure overwrite before delete
async function secureDeleteFile(dir, name){
  try{
    const fh = await dir.getFileHandle(name, {create:false});
    const f = await fh.getFile();
    const size = f.size || 1024;
    // Overwrite with random data 3 times
    for(let i=0;i<3;i++){
      const rnd = crypto.getRandomValues(new Uint8Array(size));
      const w = await fh.createWritable();
      await w.write(rnd);
      await w.close();
    }
    await dir.removeEntry(name);
  }catch{}
}

// ====== AUDIT LOG ======
let auditLog = [];
async function addAuditEntry(type, user, detail){
  const entry = {
    ts: Date.now(),
    type, // 'ok' | 'fail' | 'lockout'
    user: user||'?',
    detail: detail||'',
    ip: 'local'
  };
  auditLog.push(entry);
  // Persist to USB
  try{
    if(S.dirHandle){
      const vaultDir = await getOrCreateDir(S.dirHandle,'notepad_vault');
      await writeFile(vaultDir,'audit.json',JSON.stringify(auditLog.slice(-500)));
    }
  }catch{}
}
async function loadAuditLog(){
  try{
    if(!S.dirHandle)return;
    const vaultDir = await getOrCreateDir(S.dirHandle,'notepad_vault');
    const raw = await readFile(vaultDir,'audit.json');
    if(raw) auditLog = JSON.parse(raw);
  }catch{}
}

// ====== LOCKOUT SYSTEM ======
let failedAttempts = 0;
const MAX_ATTEMPTS = 5;
const LOCKOUT_MS = 30 * 60 * 1000;

function isLockedOut(){return Date.now() < S.lockoutUntil;}

function recordFailedAttempt(user){
  failedAttempts++;
  addAuditEntry('fail', user, `Failed attempt ${failedAttempts}/${MAX_ATTEMPTS}`);
  if(failedAttempts >= MAX_ATTEMPTS){
    S.lockoutUntil = Date.now() + LOCKOUT_MS;
    failedAttempts = 0;
    saveLockoutState();
    addAuditEntry('lockout', user, 'Account locked for 30 minutes');
    startLockoutCountdown();
    return true;
  }
  return false;
}

function saveLockoutState(){
  try{localStorage.setItem('sn_lockout', S.lockoutUntil);}catch{}
}
function loadLockoutState(){
  try{const v=localStorage.getItem('sn_lockout');if(v)S.lockoutUntil=parseInt(v);}catch{}
}
function startLockoutCountdown(){
  const el=document.getElementById('lockout-timer');
  if(!el)return;
  const loginBtn=document.getElementById('btn-login');
  function tick(){
    const rem=S.lockoutUntil-Date.now();
    if(rem<=0){
      el.style.display='none';
      if(loginBtn)loginBtn.disabled=false;
      if(S.lockoutTimer)clearInterval(S.lockoutTimer);
      return;
    }
    const m=Math.floor(rem/60000);
    const s=Math.floor((rem%60000)/1000);
    el.textContent=`🔒 Too many failed attempts. Try again in ${m}:${s.toString().padStart(2,'0')}`;
    el.style.display='block';
    if(loginBtn)loginBtn.disabled=true;
  }
  tick();
  if(S.lockoutTimer)clearInterval(S.lockoutTimer);
  S.lockoutTimer=setInterval(tick,1000);
}

// ====== IDLE AUTO-LOCK ======
function resetIdleTimer(){
  if(!S.settings.idleEnabled)return;
  // Clear existing timers
  if(S.idleTimer)clearTimeout(S.idleTimer);
  if(S.sessionWarnTimer)clearTimeout(S.sessionWarnTimer);
  if(S.sessionWarnCountdown)clearInterval(S.sessionWarnCountdown);
  hideSessionWarn();
  const lockMs=S.settings.idleMinutes*60000;
  const warnMs=lockMs-30000; // warn 30s before
  // Show warning 30s before lock
  if(warnMs>0){
    S.sessionWarnTimer=setTimeout(()=>{
      if(!document.getElementById('app-screen').classList.contains('active'))return;
      showSessionWarn();
    },warnMs);
  }
  S.idleTimer=setTimeout(()=>{
    if(document.getElementById('app-screen').classList.contains('active')){
      hideSessionWarn();
      showLockOverlay('🕐 Auto-locked due to inactivity');
    }
  },lockMs);
}

function showSessionWarn(){
  const banner=document.getElementById('session-warn');
  if(!banner)return;
  banner.classList.add('show');
  let secs=30;
  document.getElementById('session-warn-count').textContent=secs;
  if(S.sessionWarnCountdown)clearInterval(S.sessionWarnCountdown);
  S.sessionWarnCountdown=setInterval(()=>{
    secs--;
    const el=document.getElementById('session-warn-count');
    if(el)el.textContent=Math.max(0,secs);
    if(secs<=0)clearInterval(S.sessionWarnCountdown);
  },1000);
}
function hideSessionWarn(){
  const banner=document.getElementById('session-warn');
  if(banner)banner.classList.remove('show');
  if(S.sessionWarnCountdown){clearInterval(S.sessionWarnCountdown);S.sessionWarnCountdown=null;}
}
function extendSession(){
  hideSessionWarn();
  resetIdleTimer();
  showToast('Session extended ✓');
}

function setupIdleDetection(){
  ['mousemove','keydown','click','touchstart','scroll'].forEach(evt=>{
    document.addEventListener(evt,resetIdleTimer,{passive:true});
  });
  resetIdleTimer();
}

// ====== USB PRESENCE CHECK — SUPER ACTIVE (1s polling) ======
function startUsbCheck(){
  if(S.usbCheckTimer)clearInterval(S.usbCheckTimer);
  let usbMissingCount=0;
  let lastKnownGood=Date.now();

  async function runUsbCheck(){
    if(!S.settings.usbCheck)return;
    if(!S.dirHandle)return;
    if(!document.getElementById('app-screen').classList.contains('active'))return;
    try{
      // Try to read a sentinel to confirm USB is truly present
      const perm=await S.dirHandle.queryPermission({mode:'readwrite'});
      if(perm!=='granted'){throw new Error('Permission lost');}
      // Secondary check: attempt a lightweight directory iteration
      let canRead=false;
      try{for await(const _ of S.dirHandle.values()){canRead=true;break;}}catch{}
      if(!canRead){throw new Error('Cannot read USB');}
      // USB OK
      usbMissingCount=0;
      lastKnownGood=Date.now();
      document.getElementById('usb-dot').style.background='var(--success)';
      document.getElementById('usb-status-text').textContent='USB Vault Connected';
      document.getElementById('usb-indicator').className='usb-indicator connected';
      document.getElementById('usb-name-label').textContent='USB Connected';
    }catch{
      usbMissingCount++;
      document.getElementById('usb-dot').style.background='var(--danger)';
      document.getElementById('usb-status-text').textContent='USB Disconnected!';
      document.getElementById('usb-indicator').className='usb-indicator disconnected';
      document.getElementById('usb-name-label').textContent='⚠ USB Unplugged!';
      if(usbMissingCount===1){
        // IMMEDIATE lock on first detection
        const overlay=document.getElementById('lock-overlay');
        if(overlay){overlay.classList.add('usb-lock-flash');setTimeout(()=>overlay.classList.remove('usb-lock-flash'),1400);}
        showLockOverlay('⚠ USB unplugged — vault locked automatically');
        showToast('⚠ USB removed! Vault locked immediately.','warn');
        addAuditEntry('fail',S.username||'?','Auto-locked: USB removed');
      }
      if(usbMissingCount>=3){
        // 3 checks still missing → auto logout
        showToast('🚨 USB still missing — signing out!','warn');
        setTimeout(()=>{
          addAuditEntry('fail',S.username||'?','Auto sign-out: USB removed');
          doLogout();
        },1200);
      }
    }
  }

  // Poll every 1 second for super-fast response
  S.usbCheckTimer=setInterval(runUsbCheck,1000);

  // Also check immediately when tab becomes visible again
  document.addEventListener('visibilitychange',()=>{
    if(!document.hidden && S.settings.usbCheck && S.dirHandle){
      runUsbCheck();
    }
  });

  // Also check on window focus
  window.addEventListener('focus',()=>{
    if(S.settings.usbCheck && S.dirHandle){
      runUsbCheck();
    }
  });
}

// ====== CLIPBOARD AUTO-CLEAR ======
function copyToClipboard(){
  if(!S.currentNoteId)return;
  const content=document.getElementById('note-content').value;
  if(!content){showToast('Nothing to copy','warn');return;}
  navigator.clipboard.writeText(content).then(()=>{
    showToast('Copied! Will clear in 30s','warn');
    if(!S.settings.clipboardClear)return;
    startClipboardCountdown();
  }).catch(()=>showToast('Copy failed'));
}
function startClipboardCountdown(){
  if(S.clipCountdown)clearInterval(S.clipCountdown);
  if(S.clipboardTimer)clearTimeout(S.clipboardTimer);
  let secs=30;
  const banner=document.getElementById('clip-timer');
  const cd=document.getElementById('clip-countdown');
  banner.classList.add('show');
  cd.textContent=secs;
  S.clipCountdown=setInterval(()=>{
    secs--;
    cd.textContent=secs;
    if(secs<=0){
      clearInterval(S.clipCountdown);
      banner.classList.remove('show');
    }
  },1000);
  S.clipboardTimer=setTimeout(async()=>{
    try{await navigator.clipboard.writeText('');}catch{}
    clearInterval(S.clipCountdown);
    banner.classList.remove('show');
    showToast('Clipboard cleared 🔒');
  },30000);
}

// ====== LOCK OVERLAY ======
function showLockOverlay(reason){
  document.getElementById('lock-reason').textContent=reason||'Vault locked';
  document.getElementById('lock-overlay').classList.remove('hidden');
  document.getElementById('resume-password').value='';
  hideAlert('alert-resume');
}
function hideOverlay(){
  document.getElementById('lock-overlay').classList.add('hidden');
}

async function resumeSession(){
  const p=document.getElementById('resume-password').value;
  if(!p){showAlert('alert-resume','Enter your password.');return;}
  if(isLockedOut()){showAlert('alert-resume','Account is locked. Please wait.');return;}
  try{
    const vaultDir=await getOrCreateDir(S.dirHandle,'notepad_vault');
    const raw=await readFile(vaultDir,'credentials.json');
    if(!raw){showAlert('alert-resume','Vault not found.');return;}
    const creds=JSON.parse(raw);
    const hash=await hashPassword(p,creds.salt);
    let ok=false;
    if(hash===creds.hash){ok=true;}
    else if(creds.decoyHash){
      const dh=await hashPassword(p,creds.salt);
      if(dh===creds.decoyHash)ok=true; // decoy just unlocks
    }
    if(!ok){
      recordFailedAttempt(S.username);
      showAlert('alert-resume','Wrong password.');
      return;
    }
    hideOverlay();
    resetIdleTimer();
    addAuditEntry('ok',S.username,'Session resumed');
  }catch(e){showAlert('alert-resume','Error: '+e.message);}
}

// ====== NOTE ENCRYPTION HELPERS ======
async function encryptNote(note){
  if(!S.encKey||S.isDecoy)return note; // decoy never encrypts
  const enc=Object.assign({},note);
  if(S.settings.encryptContent && note.content){
    enc.content=await aesEncrypt(S.encKey,note.content);
    enc.contentEncrypted=true;
  }
  if(S.settings.encryptTitle && note.title){
    enc.title=await aesEncrypt(S.encKey,note.title);
    enc.titleEncrypted=true;
  }
  if(S.settings.hmac && S.macKey){
    const sigData = (enc.title||'')+(enc.content||'')+(note.id||'');
    enc.hmac=await hmacSign(S.macKey, sigData);
  }
  return enc;
}

async function decryptNote(note){
  const dec=Object.assign({},note);
  if(!S.encKey||S.isDecoy)return dec;
  try{
    if(dec.contentEncrypted && dec.content){
      dec.content=await aesDecrypt(S.encKey,dec.content);
      dec.contentEncrypted=false;
    }
    if(dec.titleEncrypted && dec.title){
      dec.title=await aesDecrypt(S.encKey,dec.title);
      dec.titleEncrypted=false;
    }
  }catch{dec.decryptError=true;}
  return dec;
}

async function verifyNoteHmac(note){
  if(!S.settings.hmac||!S.macKey||!note.hmac)return null;
  const sigData=(note.title||'')+(note.content||'')+(note.id||'');
  return hmacVerify(S.macKey,sigData,note.hmac);
}

// ====== UI HELPERS ======
function show(id){document.getElementById(id).classList.remove('hidden');}
function hide(id){document.getElementById(id).classList.add('hidden');}
function showScreen(name){
  ['boot-screen','connect-screen','setup-screen','login-screen','pin-screen'].forEach(s=>{
    const el=document.getElementById(s);
    if(el){if(s===name)el.classList.remove('hidden');else el.classList.add('hidden');}
  });
  const app=document.getElementById('app-screen');
  if(name==='app-screen'){
    app.classList.add('active');
  }else{
    app.classList.remove('active');
  }
}
function showAlert(id,msg,type='danger'){
  const el=document.getElementById(id);
  if(!el)return;
  el.textContent=msg;el.className='alert '+type+' show';
}
function hideAlert(id){
  const el=document.getElementById(id);
  if(el)el.className='alert danger';
}
let toastTimer=null;
function showToast(msg,type='',ms=2500){
  const t=document.getElementById('toast');
  t.textContent=msg;t.className='toast show'+(type?' '+type:'');
  if(toastTimer)clearTimeout(toastTimer);
  toastTimer=setTimeout(()=>t.classList.remove('show'),ms);
}
function fmtDate(ts){
  if(!ts)return'';
  const d=new Date(ts);
  return d.toLocaleDateString(undefined,{month:'short',day:'numeric',year:'numeric'})+' '+
    d.toLocaleTimeString(undefined,{hour:'2-digit',minute:'2-digit'});
}
function closeModal(id){document.getElementById(id).classList.add('hidden');}

function updateSecBadges(){
  const cfg=S.settings;
  const badges=[
    {label:'AES-256',on:cfg.encryptContent},
    {label:'HMAC',on:cfg.hmac},
    {label:'Auto-Lock',on:cfg.idleEnabled},
    {label:'Clip-Clear',on:cfg.clipboardClear},
    {label:'USB-Check',on:cfg.usbCheck},
  ];
  document.getElementById('sec-badges').innerHTML=badges.map(b=>
    `<span class="sec-badge${b.on?' active':''}">${b.label}</span>`
  ).join('');
}

// ====== CONNECT / USB ======
async function connectUSB(){
  const btn=document.getElementById('btn-connect');
  btn.disabled=true;btn.textContent='Opening…';
  try{
    const h=await window.showDirectoryPicker({mode:'readwrite'});
    S.dirHandle=h;
    await dbSet('dirHandle',h);
    const vaultDir=await getOrCreateDir(h,'notepad_vault');
    const raw=await readFile(vaultDir,'credentials.json');
    if(raw){
      await loadAuditLog();
      showScreen('login-screen');
      showAlert('alert-login','USB "'+h.name+'" connected. Enter your credentials.','success');
    }else{
      S.setupDirHandle=h;
      document.getElementById('dir-box').classList.add('selected');
      document.getElementById('dir-name').textContent=h.name;
      document.getElementById('dir-hint').textContent='Folder selected ✓';
      document.getElementById('btn-setup3').textContent='Continue →';
      document.getElementById('btn-setup3').onclick=setupStep3Next;
      showScreen('setup-screen');
    }
  }catch(e){
    if(e.name!=='AbortError')showAlert('alert-connect','Could not open folder: '+e.message);
  }
  btn.disabled=false;btn.textContent='📁 \u00a0Select USB Folder';
}

async function showSelectUSB(){
  try{
    const h=await window.showDirectoryPicker({mode:'readwrite'});
    S.dirHandle=h;
    await dbSet('dirHandle',h);
    const vaultDir=await getOrCreateDir(h,'notepad_vault');
    const raw=await readFile(vaultDir,'credentials.json');
    if(raw){
      await loadAuditLog();
      showAlert('alert-login','USB "'+h.name+'" connected. Enter your credentials.','success');
    }else{
      showAlert('alert-login','No vault found in "'+h.name+'". Use a fresh USB or check the folder.');
    }
  }catch(e){
    if(e.name!=='AbortError')showAlert('alert-login','Could not access folder: '+e.message);
  }
}

async function requestPermission(handle){
  try{const p=await handle.requestPermission({mode:'readwrite'});return p==='granted';}
  catch{return false;}
}

// ====== SETUP ======
function setupStep1Next(){
  const u=document.getElementById('setup-username').value.trim();
  const p=document.getElementById('setup-password').value;
  const c=document.getElementById('setup-confirm').value;
  const d=document.getElementById('setup-decoy').value;
  if(!u){showAlert('alert-setup','Please enter a username.');return;}
  if(p.length<4){showAlert('alert-setup','Password must be at least 4 characters.');return;}
  if(p!==c){showAlert('alert-setup','Passwords do not match.');return;}
  if(d && d===p){showAlert('alert-setup','Decoy password must differ from main password.');return;}
  hideAlert('alert-setup');
  S.setupCreds={username:u,password:p,decoy:d};
  goToStep(2);
}

function setupStep2Next(){
  const pin=document.getElementById('setup-pin').value;
  const pinc=document.getElementById('setup-pin-confirm').value;
  if(pin&&pin.length!==4){showAlert('alert-setup','PIN must be exactly 4 digits.');return;}
  if(pin&&pin!==pinc){showAlert('alert-setup','PINs do not match.');return;}
  if(pin&&!/^\d{4}$/.test(pin)){showAlert('alert-setup','PIN must be 4 digits only.');return;}
  hideAlert('alert-setup');
  S.setupCreds.pin=pin||'';
  goToStep(3);
}

async function pickDirectory(){
  try{
    const h=await window.showDirectoryPicker({mode:'readwrite'});
    S.setupDirHandle=h;
    document.getElementById('dir-box').classList.add('selected');
    document.getElementById('dir-name').textContent=h.name;
    document.getElementById('dir-hint').textContent='Folder selected ✓';
    document.getElementById('btn-setup3').textContent='Continue →';
    document.getElementById('btn-setup3').onclick=setupStep3Next;
  }catch(e){if(e.name!=='AbortError')showAlert('alert-setup','Could not access folder: '+e.message);}
}

function setupStep3Next(){
  if(!S.setupDirHandle){showAlert('alert-setup','Please select your USB folder first.');return;}
  hideAlert('alert-setup');
  const sum=document.getElementById('setup-summary');
  sum.innerHTML=`
    <div style="display:flex;justify-content:space-between;margin-bottom:6px">
      <span style="color:var(--text2)">Username</span><span style="font-weight:500">${esc(S.setupCreds.username)}</span>
    </div>
    <div style="display:flex;justify-content:space-between;margin-bottom:6px">
      <span style="color:var(--text2)">Password</span><span style="font-weight:500">${'•'.repeat(S.setupCreds.password.length)}</span>
    </div>
    <div style="display:flex;justify-content:space-between;margin-bottom:6px">
      <span style="color:var(--text2)">2FA PIN</span><span style="font-weight:500">${S.setupCreds.pin?'Enabled ✓':'Skipped'}</span>
    </div>
    <div style="display:flex;justify-content:space-between;margin-bottom:6px">
      <span style="color:var(--text2)">Decoy Vault</span><span style="font-weight:500">${S.setupCreds.decoy?'Enabled ✓':'None'}</span>
    </div>
    <div style="display:flex;justify-content:space-between">
      <span style="color:var(--text2)">USB Folder</span><span style="font-weight:500;color:var(--gold)">${S.setupDirHandle.name}</span>
    </div>`;
  goToStep(4);
}

async function finishSetup(){
  try{
    const h=S.setupDirHandle;
    const vaultDir=await getOrCreateDir(h,'notepad_vault');
    await getOrCreateDir(vaultDir,'notes');
    const salt=genSalt();
    const hash=await hashPassword(S.setupCreds.password,salt);
    const creds={username:S.setupCreds.username,salt,hash};
    if(S.setupCreds.decoy){
      creds.decoyHash=await hashPassword(S.setupCreds.decoy,salt);
    }
    if(S.setupCreds.pin){
      const pinSalt=genSalt();
      creds.pinSalt=pinSalt;
      creds.pinHash=await hashPassword(S.setupCreds.pin,pinSalt);
    }
    await writeFile(vaultDir,'credentials.json',JSON.stringify(creds));
    await dbSet('dirHandle',h);
    // Derive encryption key
    S.encKey=await deriveKey(S.setupCreds.password,salt);
    S.macKey=await deriveMacKey(S.setupCreds.password,salt);
    S._has2fa=!!S.setupCreds.pin;
    S.dirHandle=h;
    S.notesDir=await getOrCreateDir(vaultDir,'notes');
    S.username=S.setupCreds.username;
    S.isDecoy=false;
    await loadNotes();
    showScreen('app-screen');
    document.getElementById('user-label').textContent=S.username;
    document.getElementById('usb-name-label').textContent=h.name;
    startSecuritySystems();
    updateSecBadges();
    showToast('Vault created with AES-256-GCM encryption ✓');
    addAuditEntry('ok',S.username,'Vault created');
  }catch(e){showAlert('alert-setup','Setup failed: '+e.message);}
}

function goToStep(n){
  S.setupStep=n;
  [1,2,3,4].forEach(i=>{
    const el=document.getElementById('setup-step'+i);
    if(el)el.style.display=i===n?'block':'none';
    const dot=document.getElementById('step'+i+'-dot');
    if(!dot)return;
    if(i<n)dot.className='step done';
    else if(i===n)dot.className='step active';
    else dot.className='step';
  });
}

// ====== LOGIN ======
async function doLogin(){
  if(isLockedOut()){startLockoutCountdown();return;}
  const u=document.getElementById('login-username').value.trim();
  const p=document.getElementById('login-password').value;
  if(!u||!p){showAlert('alert-login','Please enter username and password.');return;}
  const btn=document.getElementById('btn-login');
  btn.disabled=true;btn.textContent='Checking…';
  try{
    if(!S.dirHandle){showAlert('alert-login','Please select your USB folder first.');btn.disabled=false;btn.textContent='Unlock Vault';return;}
    const granted=await requestPermission(S.dirHandle);
    if(!granted){showAlert('alert-login','Permission to USB folder denied.');btn.disabled=false;btn.textContent='Unlock Vault';return;}
    const vaultDir=await getOrCreateDir(S.dirHandle,'notepad_vault');
    const raw=await readFile(vaultDir,'credentials.json');
    if(!raw){showAlert('alert-login','No vault found on this USB folder.');btn.disabled=false;btn.textContent='Unlock Vault';return;}
    const creds=JSON.parse(raw);
    if(creds.username!==u){
      const locked=recordFailedAttempt(u);
      showAlert('alert-login',locked?'Account locked for 30 minutes.':'Invalid username or password.');
      btn.disabled=false;btn.textContent='Unlock Vault';return;
    }
    const hash=await hashPassword(p,creds.salt);
    let isDecoy=false;
    if(hash===creds.hash){
      isDecoy=false;
    }else if(creds.decoyHash && hash===creds.decoyHash){
      isDecoy=true;
    }else{
      const locked=recordFailedAttempt(u);
      showAlert('alert-login',locked?'Account locked for 30 minutes.':'Invalid username or password.');
      btn.disabled=false;btn.textContent='Unlock Vault';return;
    }

    // Check if 2FA PIN required
    if(creds.pinHash && !isDecoy){
      S.pendingUsername=u;
      S.pendingPassword=p;
      S.pendingIsDecoy=false;
      S._pendingCreds=creds;
      btn.disabled=false;btn.textContent='Unlock Vault';
      hideAlert('alert-login');
      showScreen('pin-screen');
      document.getElementById('pin-input').focus();
      return;
    }

    await completeLogin(u, p, creds, isDecoy);
    btn.disabled=false;btn.textContent='Unlock Vault';
  }catch(e){
    showAlert('alert-login','Error: '+e.message);
    btn.disabled=false;btn.textContent='Unlock Vault';
  }
}

async function completeLogin(u, p, creds, isDecoy){
  if(!isDecoy){
    S.encKey=await deriveKey(p,creds.salt);
    S.macKey=await deriveMacKey(p,creds.salt);
  }else{
    S.encKey=null;
    S.macKey=null;
  }
  S._has2fa=!!creds.pinHash;
  S.isDecoy=isDecoy;
  const vaultDir=await getOrCreateDir(S.dirHandle,'notepad_vault');
  S.notesDir=await getOrCreateDir(vaultDir,'notes');
  S.username=u;
  failedAttempts=0;
  addAuditEntry('ok',u,isDecoy?'Decoy vault opened':'Login successful');
  await loadNotes();
  showScreen('app-screen');
  document.getElementById('user-label').textContent=u+(isDecoy?' (decoy)':'');
  document.getElementById('usb-name-label').textContent=S.dirHandle.name;
  hideAlert('alert-login');
  startSecuritySystems();
  updateSecBadges();
  if(isDecoy)showToast('Decoy vault opened (empty)','warn');
}

// ====== 2FA PIN ======
function onPinInput(){
  const val=document.getElementById('pin-input').value;
  for(let i=0;i<4;i++){
    document.getElementById('pd'+i).classList.toggle('filled',i<val.length);
  }
}
function resetPinDots(){for(let i=0;i<4;i++)document.getElementById('pd'+i).classList.remove('filled');}

async function verifyPin(){
  const pin=document.getElementById('pin-input').value;
  if(pin.length!==4){showAlert('alert-pin','Enter your 4-digit PIN.');return;}
  const creds=S._pendingCreds;
  if(!creds){showAlert('alert-pin','Session expired. Go back.');return;}
  const hash=await hashPassword(pin,creds.pinSalt);
  if(hash!==creds.pinHash){
    showAlert('alert-pin','Wrong PIN.');
    document.getElementById('pin-input').value='';
    resetPinDots();
    return;
  }
  document.getElementById('pin-input').value='';
  resetPinDots();
  hideAlert('alert-pin');
  await completeLogin(S.pendingUsername,S.pendingPassword,creds,false);
}

// ====== SECURITY SYSTEMS START ======
function startSecuritySystems(){
  setupIdleDetection();
  startUsbCheck();
  resetIdleTimer();
}

// ====== SETTINGS ======
function openSettings(){
  const s=S.settings;
  document.getElementById('idle-minutes').value=s.idleMinutes;
  setToggle('idle-toggle',s.idleEnabled);
  setToggle('clip-toggle',s.clipboardClear);
  setToggle('usb-toggle',s.usbCheck);
  setToggle('enc-toggle',s.encryptContent);
  setToggle('enc-title-toggle',s.encryptTitle);
  setToggle('hmac-toggle',s.hmac);
  show('settings-modal');
}
function setToggle(id,val){
  const el=document.getElementById(id);
  if(val)el.classList.add('on');else el.classList.remove('on');
}
function toggleSetting(key){
  const map={idle:'idle-toggle',clip:'clip-toggle',usb:'usb-toggle',enc:'enc-toggle',encTitle:'enc-title-toggle',hmac:'hmac-toggle'};
  const el=document.getElementById(map[key]);
  el.classList.toggle('on');
}
function saveSettings(){
  S.settings.idleEnabled=document.getElementById('idle-toggle').classList.contains('on');
  S.settings.idleMinutes=parseInt(document.getElementById('idle-minutes').value)||5;
  S.settings.clipboardClear=document.getElementById('clip-toggle').classList.contains('on');
  S.settings.usbCheck=document.getElementById('usb-toggle').classList.contains('on');
  S.settings.encryptContent=document.getElementById('enc-toggle').classList.contains('on');
  S.settings.encryptTitle=document.getElementById('enc-title-toggle').classList.contains('on');
  S.settings.hmac=document.getElementById('hmac-toggle').classList.contains('on');
  resetIdleTimer();
  closeModal('settings-modal');
  updateSecBadges();
  showToast('Security settings saved ✓');
}

// ====== AUDIT LOG ======
async function openAuditLog(){
  const list=document.getElementById('audit-list');
  if(auditLog.length===0){
    list.innerHTML='<div style="color:var(--text3)">No audit entries yet.</div>';
  }else{
    list.innerHTML=[...auditLog].reverse().slice(0,100).map(e=>`
      <div class="audit-entry ${e.type}">
        [${new Date(e.ts).toLocaleString()}] ${e.type.toUpperCase()} — ${esc(e.user)} — ${esc(e.detail)}
      </div>`).join('');
  }
  show('audit-modal');
}

// ====== ENCRYPTED EXPORT ======
function exportEncrypted(){show('export-modal');}

async function doExport(){
  if(!S.currentNoteId){showToast('No note selected');return;}
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n){return;}
  try{
    const salt=genSalt();
    const key=await deriveKey(document.getElementById('login-password')?document.getElementById('login-password').value:'export',salt);
    const payload=JSON.stringify({
      title:n.title,content:n.content,
      id:n.id,createdAt:n.createdAt,updatedAt:n.updatedAt
    });
    const iv=crypto.getRandomValues(new Uint8Array(12));
    const ct=await crypto.subtle.encrypt({name:'AES-GCM',iv},key,ENC.encode(payload));
    const out={v:2,salt,iv:Array.from(iv),ct:Array.from(new Uint8Array(ct))};
    const blob=new Blob([JSON.stringify(out)],{type:'application/json'});
    const url=URL.createObjectURL(blob);
    const a=document.createElement('a');
    a.href=url;a.download='securenote_export_'+n.id+'.enc.json';
    a.click();URL.revokeObjectURL(url);
    closeModal('export-modal');
    showToast('Encrypted export downloaded ✓');
  }catch(e){showToast('Export failed: '+e.message);}
}

// ====== LOGOUT / RESET ======
function doLogout(){
  S.currentNoteId=null;S.notes=[];S.unsaved=false;
  S.encKey=null;S.macKey=null;S.isDecoy=false;
  if(S.idleTimer)clearTimeout(S.idleTimer);
  if(S.usbCheckTimer)clearInterval(S.usbCheckTimer);
  if(S.clipboardTimer)clearTimeout(S.clipboardTimer);
  if(S.clipCountdown)clearInterval(S.clipCountdown);
  document.getElementById('clip-timer').classList.remove('show');
  showScreen('login-screen');
  document.getElementById('login-password').value='';
  hideAlert('alert-login');
}

async function resetAll(){
  if(!confirm('This will clear the saved USB folder link. Your USB notes are safe. Continue?'))return;
  await dbDel('dirHandle');
  S.dirHandle=null;S.setupCreds=null;S.setupDirHandle=null;S.setupStep=1;
  goToStep(1);
  document.getElementById('setup-username').value='';
  document.getElementById('setup-password').value='';
  document.getElementById('setup-confirm').value='';
  document.getElementById('setup-decoy').value='';
  document.getElementById('setup-pin').value='';
  document.getElementById('setup-pin-confirm').value='';
  document.getElementById('dir-box').classList.remove('selected');
  document.getElementById('dir-name').textContent='Click to select USB folder';
  document.getElementById('dir-hint').textContent='e.g. D:\\ or E:\\SecureNote';
  showScreen('connect-screen');
}

// ====== NOTES ======
async function loadNotes(){
  S.notes=[];
  try{
    const files=await listFiles(S.notesDir);
    for(const f of files){
      if(!f.endsWith('.json'))continue;
      const raw=await readFile(S.notesDir,f);
      if(raw){
        try{
          let n=JSON.parse(raw);
          n=await decryptNote(n);
          // Restore images from the saved note data
          if(Array.isArray(n.images) && n.images.length>0){
            S.noteImages[n.id]=n.images;
          }
          S.notes.push(n);
        }catch{}
      }
    }
    S.notes.sort((a,b)=>(b.updatedAt||0)-(a.updatedAt||0));
  }catch(e){console.error(e);}
  renderNoteList();
}

function renderNoteList(){
  const q=document.getElementById('search-input').value.toLowerCase();
  const list=document.getElementById('note-list');
  let filtered=S.notes.filter(n=>{
    if(!q&&!S.activeTagFilter)return true;
    const textMatch=!q||((n.title||'').toLowerCase().includes(q)||(n.content||'').toLowerCase().includes(q));
    const tagMatch=!S.activeTagFilter||((n.tags||[]).includes(S.activeTagFilter));
    return textMatch&&tagMatch;
  });
  // Pinned first
  filtered.sort((a,b)=>{
    if(a.pinned&&!b.pinned)return -1;
    if(!a.pinned&&b.pinned)return 1;
    return (b.updatedAt||0)-(a.updatedAt||0);
  });
  if(filtered.length===0){
    list.innerHTML='<div class="empty-notes">'+(q||S.activeTagFilter?'No notes match':'No notes yet.<br>Create your first note!')+'</div>';
  }else{
    list.innerHTML=filtered.map(n=>{
      const isLocked=n.notePassHash&&!S.noteLockedUnlocked[n.id];
      const tags=(n.tags||[]).map(t=>`<span class="note-tag-mini">${esc(t)}</span>`).join('');
      const locked=n.notePassHash?`<span class="note-locked-badge">🔒</span>`:'';
      // Hide title AND preview when locked
      const displayTitle=isLocked?'🔒 Locked Note':esc(n.title||'Untitled');
      const previewClass=isLocked?'note-item-preview is-locked':'note-item-preview';
      const previewContent=isLocked?'Protected Content':esc((n.content||'').slice(0,60)||'No content');
      return`<div class="note-item${n.id===S.currentNoteId?' active':''}${n.pinned?' pinned':''}" onclick="openNote('${n.id}')">
        <div class="note-item-title">${n.pinned?'<span class="note-item-pin">📌</span>':''}${displayTitle}${locked}<span class="enc-badge">${S.encKey&&!S.isDecoy?'🔒':''}</span></div>
        <div class="${previewClass}">${previewContent}</div>
        ${tags&&!isLocked?`<div class="note-item-tags">${tags}</div>`:''}
        <div class="note-item-date">${fmtDate(n.updatedAt)}</div>
      </div>`;
    }).join('');
  }
  document.getElementById('note-count').textContent=S.notes.length+' note'+(S.notes.length!==1?'s':'');
  renderTagFilter();
}

function renderTagFilter(){
  const wrap=document.getElementById('tag-filter-wrap');
  const chips=document.getElementById('tag-filter-chips');
  if(!wrap||!chips)return;
  // Collect all unique tags across all notes
  const allTags=[...new Set(S.notes.flatMap(n=>n.tags||[]))].sort();
  if(allTags.length===0){wrap.style.display='none';return;}
  wrap.style.display='flex';
  // Build chips: "All" chip + one per tag
  chips.innerHTML=[
    `<button class="tag-filter-chip${!S.activeTagFilter?' active':''}" onclick="setTagFilter(null)">All</button>`,
    ...allTags.map(t=>`<button class="tag-filter-chip${S.activeTagFilter===t?' active':''}" onclick="setTagFilter(${JSON.stringify(t)})">${esc(t)}</button>`)
  ].join('');
}

function setTagFilter(tag){
  S.activeTagFilter=(S.activeTagFilter===tag)?null:tag;
  renderNoteList();
}

function esc(s){if(!s)return'';return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}

async function newNote(){
  if(S.unsaved){const ok=confirm('You have unsaved changes. Discard them?');if(!ok)return;}
  const n={id:genId(),title:'',content:'',createdAt:Date.now(),updatedAt:Date.now()};
  // Auto-assign to active folder (including hidden vault)
  if(S.activeFolderFilter)n.folder=S.activeFolderFilter;
  S.notes.unshift(n);S.currentNoteId=n.id;
  S.noteImages[n.id]=[];
  renderNoteList();showEditor(n);
  document.getElementById('note-title').focus();markUnsaved();
}

async function openNote(id){
  if(S.unsaved&&S.currentNoteId!==id){if(!confirm('Discard unsaved changes?'))return;}
  const n=S.notes.find(x=>x.id===id);
  if(!n)return;
  S.currentNoteId=id;renderNoteList();showEditor(n);
  // HMAC verification
  if(S.settings.hmac&&S.macKey&&n.hmac){
    // We need raw note from disk to verify
    try{
      const rawJson=await readFile(S.notesDir,id+'.json');
      if(rawJson){
        const rawNote=JSON.parse(rawJson);
        const ok=await hmacVerify(S.macKey,(rawNote.title||'')+(rawNote.content||'')+(rawNote.id||''),rawNote.hmac||'');
        const hEl=document.getElementById('hmac-status');
        hEl.textContent=ok?'✔ HMAC OK':'⚠ HMAC FAIL';
        hEl.className=ok?'hmac-ok':'hmac-fail';
      }
    }catch{}
  }else{
    document.getElementById('hmac-status').textContent='';
  }
  markSaved();
}

function showEditor(n){
  const ec=document.getElementById('editor-content');
  if(ec) ec.style.display='flex';
  const isLocked=n.notePassHash&&!S.noteLockedUnlocked[n.id];
  // Hide title when locked — show placeholder instead
  const titleInput=document.getElementById('note-title');
  if(isLocked){
    titleInput.value='🔒 Locked Note';
    titleInput.readOnly=true;
    titleInput.style.color='var(--text3)';
  }else{
    titleInput.value=n.title||'';
    titleInput.readOnly=false;
    titleInput.style.color='';
  }
  document.getElementById('note-content').value=n.content||'';
  document.getElementById('note-created').textContent='Created: '+fmtDate(n.createdAt);
  document.getElementById('note-updated').textContent='Saved: '+fmtDate(n.updatedAt);
  document.getElementById('delete-note-name').textContent=n.title||'Untitled';
  updateWordCount();
  renderImageGallery();
  renderTagChips(n);
  const pinBtn=document.getElementById('pin-btn');
  if(pinBtn)pinBtn.style.color=n.pinned?'var(--gold)':'';
  // Note lock overlay + animation
  const lockOverlay=document.getElementById('note-lock-overlay');
  const textarea=document.getElementById('note-content');
  const floatPanel=document.getElementById('note-float-panel');
  if(isLocked){
    lockOverlay.classList.remove('hidden');
    textarea.style.display='none';
    if(floatPanel)floatPanel.classList.add('locked-mode');
    animateLockScreen();
    // Auto-focus password input once panel opens
    setTimeout(()=>document.getElementById('note-lock-input')?.focus(),350);
  }else{
    lockOverlay.classList.add('hidden');
    textarea.style.display='';
    if(floatPanel)floatPanel.classList.remove('locked-mode');
  }
  if(S.mdMode)renderMarkdown();
  updateRelockBtn();
  // Open the floating panel
  openFloatEditor();
}

let _markUnsavedDebounce=null;
function markUnsaved(){
  S.unsaved=true;
  const ss=document.getElementById('save-status');
  if(ss){ss.textContent='Unsaved';ss.className='save-status unsaved';}
  // Debounced auto-save after 2.5s of inactivity
  if(_markUnsavedDebounce)clearTimeout(_markUnsavedDebounce);
  _markUnsavedDebounce=setTimeout(()=>{
    if(S.unsaved&&S.currentNoteId){
      const ss2=document.getElementById('save-status');
      if(ss2){ss2.textContent='Saving…';ss2.className='save-status unsaved';}
      saveCurrentNote();
    }
  },2500);
}

async function saveCurrentNote(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  n.title=document.getElementById('note-title').value||'Untitled';
  n.content=document.getElementById('note-content').value;
  n.updatedAt=Date.now();
  // Embed images into the note so they persist on disk
  n.images=S.noteImages[S.currentNoteId]||[];
  try{
    const toSave=await encryptNote(n);
    await writeFile(S.notesDir,n.id+'.json',JSON.stringify(toSave));
    markSaved();
    document.getElementById('note-updated').textContent='Saved: '+fmtDate(n.updatedAt);
    document.getElementById('delete-note-name').textContent=n.title;
    S.notes.sort((a,b)=>(b.updatedAt||0)-(a.updatedAt||0));
    renderNoteList();
    showToast('Note saved to USB 🔒 ✓');
  }catch(e){showToast('Save failed: '+e.message);}
}

function updateWordCount(){
  const c=document.getElementById('note-content').value;
  const words=c.trim()?c.trim().split(/\s+/).length:0;
  const readMins=Math.max(1,Math.round(words/200));
  document.getElementById('word-count').textContent=words+' word'+(words!==1?'s':'')+' · '+c.length+' chars';
  const rt=document.getElementById('read-time');
  if(rt)rt.textContent=words>0?'~'+readMins+' min read':'';
}

function confirmDelete(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  // If note has a password lock → require password before trashing
  if(n.notePassHash){
    document.getElementById('locked-delete-note-name').textContent=n.title||'Untitled';
    document.getElementById('locked-delete-pass').value='';
    hideAlert('locked-delete-alert');
    show('locked-delete-modal');
    setTimeout(()=>document.getElementById('locked-delete-pass').focus(),120);
    return;
  }
  show('delete-modal');
}

// Verify note password before allowing locked note to go to trash
async function verifyLockedNoteDelete(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n||!n.notePassHash){closeModal('locked-delete-modal');return;}
  const p=document.getElementById('locked-delete-pass').value;
  if(!p){showAlert('locked-delete-alert','Please enter the note password.');return;}
  const hash=await hashPassword(p,n.notePassSalt);
  if(hash!==n.notePassHash){
    showAlert('locked-delete-alert','Incorrect note password. Cannot delete.');
    document.getElementById('locked-delete-pass').value='';
    document.getElementById('locked-delete-pass').focus();
    return;
  }
  // Password correct — proceed to soft-delete
  closeModal('locked-delete-modal');
  document.getElementById('locked-delete-pass').value='';
  await deleteCurrentNote();
}

async function deleteCurrentNote(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n){closeModal('delete-modal');return;}
  try{
    // Soft delete — move to trash (keep on disk, mark deleted)
    n.deleted=true;
    n.deletedAt=Date.now();
    const enc=await encryptNote(n);
    await writeFile(S.notesDir,n.id+'.json',JSON.stringify(enc));
    // Clear unlock state for this note
    delete S.noteLockedUnlocked[n.id];
    S.currentNoteId=null;S.unsaved=false;
    closeModal('delete-modal');
    closeFloatEditor();
    updateTrashBadge();
    renderNoteList();
    renderFolderList();
    showToast('Note moved to Trash 🗑');
  }catch(e){closeModal('delete-modal');showToast('Move to trash failed: '+e.message);}
}

// ====== THEME ======
const THEME_ICONS = {
  light: `<circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/><line x1="12" y1="21" x2="12" y2="23"/><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/><line x1="1" y1="12" x2="3" y2="12"/><line x1="21" y1="12" x2="23" y2="12"/><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/>`,
  dark: `<path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>`,
  auto: `<rect x="2" y="3" width="20" height="14" rx="2"/><path d="M8 21h8M12 17v4"/><circle cx="12" cy="10" r="3" fill="currentColor" opacity=".4"/>`
};
const THEME_TITLES = {auto:'Auto (System)',light:'Light Mode',dark:'Dark Mode'};

function applyTheme(mode){
  const root=document.documentElement;
  root.classList.remove('light','dark');
  if(mode==='light')root.classList.add('light');
  else if(mode==='dark')root.classList.add('dark');
  const btn=document.getElementById('theme-btn');
  const icon=document.getElementById('theme-icon');
  if(icon) icon.innerHTML = THEME_ICONS[mode] || THEME_ICONS.auto;
  if(btn){
    btn.className='icon-btn theme-'+mode;
    btn.title='Theme: '+(THEME_TITLES[mode]||'Auto')+' — click to cycle';
    // Trigger animation
    btn.classList.remove('animating');
    void btn.offsetWidth; // reflow
    btn.classList.add('animating');
    setTimeout(()=>btn.classList.remove('animating'),400);
  }
  try{localStorage.setItem('sn_theme',mode);}catch{}
}
function toggleTheme(){
  // Cycle: auto → light → dark → auto
  const cur=S.theme;
  const next = cur==='auto'?'light': cur==='light'?'dark':'auto';
  S.theme=next;
  applyTheme(next);
  showToast('Theme: '+THEME_TITLES[next]);
}
function initTheme(){
  try{
    const saved=localStorage.getItem('sn_theme');
    if(saved){S.theme=saved;applyTheme(saved);}
    else{S.theme='auto';applyTheme('auto');}
  }catch{applyTheme('auto');}
}

// ====== IMAGE SYSTEM ======
function triggerImageUpload(){
  document.getElementById('img-file-input').click();
}

function onImageFileSelected(e){
  const files=Array.from(e.target.files);
  files.forEach(f=>readImageFile(f));
  e.target.value=''; // reset so same file can be added again
}

function readImageFile(file){
  if(!file.type.startsWith('image/')){showToast('Only image files supported','warn');return;}
  const maxMB=5;
  if(file.size>maxMB*1024*1024){showToast(`Image too large (max ${maxMB}MB)`,'warn');return;}
  const reader=new FileReader();
  reader.onload=ev=>{
    addImageToNote({
      id:'img_'+Date.now()+'_'+Math.random().toString(36).slice(2,6),
      dataUrl:ev.target.result,
      name:file.name,
      size:file.size,
      addedAt:Date.now()
    });
  };
  reader.readAsDataURL(file);
}

function addImageToNote(imgObj){
  if(!S.currentNoteId)return;
  if(!S.noteImages[S.currentNoteId])S.noteImages[S.currentNoteId]=[];
  S.noteImages[S.currentNoteId].push(imgObj);
  renderImageGallery();
  markUnsaved();
  showToast('Image added 🖼');
}

function removeImageFromNote(imgId){
  if(!S.currentNoteId)return;
  const imgs=S.noteImages[S.currentNoteId]||[];
  S.noteImages[S.currentNoteId]=imgs.filter(x=>x.id!==imgId);
  renderImageGallery();
  markUnsaved();
}

function renderImageGallery(){
  const gallery=document.getElementById('img-gallery');
  const dropzone=document.getElementById('img-dropzone');
  if(!gallery)return;
  const imgs=S.noteImages[S.currentNoteId]||[];
  if(imgs.length===0){
    gallery.innerHTML='';
    if(dropzone)dropzone.style.display='flex';
    return;
  }
  if(dropzone)dropzone.style.display='flex';
  gallery.innerHTML=imgs.map((img,i)=>`
    <div class="img-thumb-wrap" title="${esc(img.name||'Image')}">
      <img class="img-thumb" src="${img.dataUrl}" alt="${esc(img.name||'Image')}" onclick="openLightbox('${img.id}')">
      <button class="img-thumb-del" onclick="event.stopPropagation();removeImageFromNote('${img.id}')" title="Remove image">✕</button>
    </div>
  `).join('');
}

function openLightbox(imgId){
  if(!S.currentNoteId)return;
  const img=(S.noteImages[S.currentNoteId]||[]).find(x=>x.id===imgId);
  if(!img)return;
  document.getElementById('lb-img').src=img.dataUrl;
  document.getElementById('lb-info').textContent=img.name+(img.size?` · ${(img.size/1024).toFixed(1)} KB`:'');
  document.getElementById('img-lightbox').classList.remove('hidden');
}
function closeLightbox(){
  document.getElementById('img-lightbox').classList.add('hidden');
  document.getElementById('lb-img').src='';
}

// Drag & drop
function onImgDragOver(e){e.preventDefault();document.getElementById('img-dropzone').classList.add('dragover');}
function onImgDragLeave(e){document.getElementById('img-dropzone').classList.remove('dragover');}
function onImgDrop(e){
  e.preventDefault();
  document.getElementById('img-dropzone').classList.remove('dragover');
  const files=Array.from(e.dataTransfer.files);
  files.forEach(f=>readImageFile(f));
}

// Paste image from clipboard (Ctrl+V)
document.addEventListener('paste',e=>{
  if(!S.currentNoteId)return;
  // Only handle if editor area is active (not typing in inputs)
  if(['INPUT','TEXTAREA'].includes(document.activeElement.tagName)&&document.activeElement.id!=='note-content')return;
  const items=e.clipboardData&&e.clipboardData.items;
  if(!items)return;
  let handled=false;
  for(const item of items){
    if(item.type.startsWith('image/')){
      const file=item.getAsFile();
      if(file){readImageFile(file);handled=true;}
    }
  }
  if(handled)e.preventDefault();
});

// Image gallery is rendered directly inside showEditor, newNote, openNote — see those functions below.

// ====== QUICK-ACCESS DRAWER ======
function toggleQADrawer(forceClose){
  const drawer=document.getElementById('qa-drawer');
  const backdrop=document.getElementById('qa-backdrop');
  if(!drawer)return;
  const isOpen=drawer.classList.contains('open');
  const shouldOpen=(forceClose===undefined)?!isOpen:(forceClose===false?false:false);
  if(shouldOpen){
    drawer.classList.add('open');
    if(backdrop)backdrop.style.display='block';
  }else{
    drawer.classList.remove('open');
    if(backdrop)backdrop.style.display='none';
  }
}

// ====== RE-LOCK CURRENT NOTE ======
function lockCurrentNote(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n||!n.notePassHash)return;
  // Animate the shackle dropping before locking
  const icon=document.getElementById('relock-icon');
  if(icon){
    icon.style.transform='translateY(-3px)';
    setTimeout(()=>{icon.style.transform='';},120);
  }
  setTimeout(()=>{
    // Clear any previous password input + error
    const lockInput=document.getElementById('note-lock-input');
    const lockErr=document.getElementById('note-lock-err');
    if(lockInput)lockInput.value='';
    if(lockErr)lockErr.textContent='';
    delete S.noteLockedUnlocked[n.id];
    showEditor(n);
    renderNoteList();
    showToast('Note locked 🔒');
  },160);
}

// Update re-lock button visibility whenever a note is opened/unlocked
function updateRelockBtn(){
  const btn=document.getElementById('note-relock-btn');
  const lockSetBtn=document.getElementById('note-lock-set-btn');
  if(!btn)return;
  if(!S.currentNoteId){
    btn.style.display='none';
    if(lockSetBtn)lockSetBtn.style.display='none';
    return;
  }
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  const hasPass=n&&n.notePassHash;
  const isUnlocked=hasPass&&S.noteLockedUnlocked[n.id];
  // Re-lock button: only visible when note has a pass AND is currently unlocked
  btn.style.display=isUnlocked?'':'none';
  // Lock-set button: hidden when note is LOCKED (has pass but not yet unlocked)
  // Visible when: no password on note, OR note has password and IS unlocked
  if(lockSetBtn){
    const shouldHide=hasPass&&!isUnlocked;
    lockSetBtn.style.display=shouldHide?'none':'';
  }
}

// ====== KEYBOARD SHORTCUTS ======
document.addEventListener('keydown',e=>{
  if((e.ctrlKey||e.metaKey)&&e.key==='s'){e.preventDefault();saveCurrentNote();}
  if((e.ctrlKey||e.metaKey)&&e.key==='n'){e.preventDefault();openTemplateModal();}
  if((e.ctrlKey||e.metaKey)&&e.key==='f'){
    e.preventDefault();
    const fr=document.getElementById('find-replace-bar');
    if(fr){fr.classList.toggle('hidden');if(!fr.classList.contains('hidden'))document.getElementById('fr-find').focus();}
  }
  if((e.ctrlKey||e.metaKey)&&e.key==='d'){e.preventDefault();toggleTheme();}
  // Ctrl+Shift+L — re-lock current note
  if((e.ctrlKey||e.metaKey)&&e.shiftKey&&e.key==='L'){e.preventDefault();lockCurrentNote();}
});

// Auto-save every 30s
setInterval(()=>{if(S.unsaved&&S.currentNoteId)saveCurrentNote();},30000);

// ====== FLOATING NOTE EDITOR ======
function openFloatEditor(){
  const backdrop = document.getElementById('note-float-backdrop');
  const panel    = document.getElementById('note-float-panel');
  if(!backdrop||!panel) return;
  backdrop.style.display = 'block';
  // Force reflow for transition
  backdrop.offsetHeight;
  backdrop.classList.add('open');
  panel.classList.add('open');
  // Focus title if empty
  setTimeout(()=>{
    const t = document.getElementById('note-title');
    if(t && !t.value) t.focus();
    else if(t) document.getElementById('note-content')?.focus();
  }, 320);
}

function closeFloatEditor(){
  if(S.unsaved && S.currentNoteId){
    saveCurrentNote();
  }
  const backdrop = document.getElementById('note-float-backdrop');
  const panel    = document.getElementById('note-float-panel');
  if(!backdrop||!panel) return;
  panel.classList.remove('open','locked-mode');
  backdrop.classList.remove('open');
  setTimeout(()=>{ backdrop.style.display='none'; },300);
  S.currentNoteId = null;
  renderNoteList();
}

// Close float editor on Escape key
document.addEventListener('keydown', e=>{
  if(e.key==='Escape'){
    const panel = document.getElementById('note-float-panel');
    if(panel && panel.classList.contains('open')){
      e.preventDefault();
      e.stopPropagation();
      closeFloatEditor();
    }
  }
});

// ====== ACCOUNT SETTINGS ======
function openAccountSettings(){
  document.getElementById('acct-new-name').value=S.username||'';
  document.getElementById('acct-cur-pass').value='';
  document.getElementById('acct-new-pass').value='';
  document.getElementById('acct-confirm-pass').value='';
  hideAlert('acct-alert');
  show('acct-modal');
}
function clearAcctFields(){
  document.getElementById('acct-new-name').value='';
  document.getElementById('acct-cur-pass').value='';
  document.getElementById('acct-new-pass').value='';
  document.getElementById('acct-confirm-pass').value='';
  hideAlert('acct-alert');
}
async function saveAccountName(){
  const newName=document.getElementById('acct-new-name').value.trim();
  if(!newName){showAlert('acct-alert','Please enter a new username.');return;}
  if(newName===S.username){showAlert('acct-alert','That is already your current username.','warn');return;}
  try{
    const vaultDir=await getOrCreateDir(S.dirHandle,'notepad_vault');
    const raw=await readFile(vaultDir,'credentials.json');
    if(!raw){showAlert('acct-alert','Could not read vault credentials.');return;}
    const creds=JSON.parse(raw);
    creds.username=newName;
    await writeFile(vaultDir,'credentials.json',JSON.stringify(creds));
    S.username=newName;
    document.getElementById('user-label').textContent=newName;
    addAuditEntry('ok',newName,'Username changed');
    showAlert('acct-alert','Username updated successfully!','success');
    showToast('Username updated ✓');
  }catch(e){showAlert('acct-alert','Error: '+e.message);}
}
async function saveAccountPassword(){
  const curPass=document.getElementById('acct-cur-pass').value;
  const newPass=document.getElementById('acct-new-pass').value;
  const confPass=document.getElementById('acct-confirm-pass').value;
  if(!curPass){showAlert('acct-alert','Enter your current password.');return;}
  if(newPass.length<4){showAlert('acct-alert','New password must be at least 4 characters.');return;}
  if(newPass!==confPass){showAlert('acct-alert','New passwords do not match.');return;}
  try{
    const vaultDir=await getOrCreateDir(S.dirHandle,'notepad_vault');
    const raw=await readFile(vaultDir,'credentials.json');
    if(!raw){showAlert('acct-alert','Could not read vault credentials.');return;}
    const creds=JSON.parse(raw);
    // Verify current password
    const curHash=await hashPassword(curPass,creds.salt);
    if(curHash!==creds.hash){showAlert('acct-alert','Current password is incorrect.');return;}
    // Generate new salt + hash
    const newSalt=genSalt();
    const newHash=await hashPassword(newPass,newSalt);
    creds.salt=newSalt;
    creds.hash=newHash;
    // Re-hash decoy if exists (keep same decoy password string — we can't know it, so just keep old decoyHash logic note)
    // Re-derive encryption keys
    const newEncKey=await deriveKey(newPass,newSalt);
    const newMacKey=await deriveMacKey(newPass,newSalt);
    // Re-encrypt all notes with new key
    const noteFiles=await listFiles(S.notesDir);
    for(const f of noteFiles){
      if(!f.endsWith('.json'))continue;
      try{
        const nRaw=await readFile(S.notesDir,f);
        if(!nRaw)continue;
        let n=JSON.parse(nRaw);
        // Decrypt with old key
        const dec=await decryptNote(n);
        // Re-encrypt with new key — temporarily swap keys
        const oldKey=S.encKey, oldMac=S.macKey;
        S.encKey=newEncKey; S.macKey=newMacKey;
        const reenc=await encryptNote(dec);
        S.encKey=oldKey; S.macKey=oldMac;
        await writeFile(S.notesDir,f,JSON.stringify(reenc));
      }catch{}
    }
    await writeFile(vaultDir,'credentials.json',JSON.stringify(creds));
    // Apply new keys to session
    S.encKey=newEncKey;
    S.macKey=newMacKey;
    addAuditEntry('ok',S.username,'Password changed');
    document.getElementById('acct-cur-pass').value='';
    document.getElementById('acct-new-pass').value='';
    document.getElementById('acct-confirm-pass').value='';
    showAlert('acct-alert','Password changed successfully! All notes re-encrypted.','success');
    showToast('Password updated & notes re-encrypted ✓');
  }catch(e){showAlert('acct-alert','Error: '+e.message);}
}

// ====== TAGS ======
function renderTagChips(note){
  const display=document.getElementById('tag-chips-display');
  if(!display)return;
  const tags=note.tags||[];
  display.innerHTML=tags.map(t=>`<span class="tag-chip">${esc(t)}<button class="tag-chip-del" onclick="removeTag('${esc(t)}')" title="Remove tag">×</button></span>`).join('');
}
function onTagKeydown(e){
  if(e.key!=='Enter'&&e.key!==',')return;
  e.preventDefault();
  const input=document.getElementById('tag-input');
  const val=input.value.trim().replace(/,/g,'');
  if(!val)return;
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  if(!n.tags)n.tags=[];
  if(n.tags.includes(val)){input.value='';return;}
  if(n.tags.length>=10){showToast('Max 10 tags per note','warn');return;}
  n.tags.push(val);
  input.value='';
  renderTagChips(n);
  renderNoteList();
  markUnsaved();
}
function removeTag(tag){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  n.tags=(n.tags||[]).filter(t=>t!==tag);
  renderTagChips(n);
  renderNoteList();
  markUnsaved();
}

// ====== MARKDOWN PREVIEW ======
function toggleMarkdown(){
  S.mdMode=!S.mdMode;
  const btn=document.getElementById('md-toggle');
  const textarea=document.getElementById('note-content');
  const preview=document.getElementById('md-preview');
  if(!btn||!textarea||!preview)return;
  if(S.mdMode){
    btn.classList.add('on');
    textarea.classList.add('hidden');
    preview.classList.remove('hidden');
    renderMarkdown();
  }else{
    btn.classList.remove('on');
    textarea.classList.remove('hidden');
    preview.classList.add('hidden');
  }
}
function renderMarkdown(){
  const content=document.getElementById('note-content').value;
  const preview=document.getElementById('md-preview');
  if(!preview)return;
  let html=content
    .replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;')
    .replace(/^###### (.+)$/gm,'<h6>$1</h6>').replace(/^##### (.+)$/gm,'<h5>$1</h5>')
    .replace(/^#### (.+)$/gm,'<h4>$1</h4>').replace(/^### (.+)$/gm,'<h3>$1</h3>')
    .replace(/^## (.+)$/gm,'<h2>$1</h2>').replace(/^# (.+)$/gm,'<h1>$1</h1>')
    .replace(/\*\*\*(.+?)\*\*\*/g,'<strong><em>$1</em></strong>')
    .replace(/\*\*(.+?)\*\*/g,'<strong>$1</strong>').replace(/\*(.+?)\*/g,'<em>$1</em>')
    .replace(/~~(.+?)~~/g,'<del>$1</del>')
    .replace(/`([^`]+)`/g,'<code>$1</code>')
    .replace(/^---+$/gm,'<hr>')
    .replace(/\[([^\]]+)\]\(([^)]+)\)/g,'<a href="$2" target="_blank" rel="noopener">$1</a>')
    .replace(/^&gt; (.+)$/gm,'<blockquote>$1</blockquote>')
    .replace(/^- \[x\] (.+)$/gm,(m,p1)=>`<li class="task-list-item checked"><input type="checkbox" class="task-checkbox" checked onchange="syncCheckboxToContent(this)"> <span>${p1}</span></li>`)
    .replace(/^- \[ \] (.+)$/gm,(m,p1)=>`<li class="task-list-item"><input type="checkbox" class="task-checkbox" onchange="syncCheckboxToContent(this)"> <span>${p1}</span></li>`)
    .replace(/^[-*] (.+)$/gm,'<li>$1</li>')
    .replace(/^\d+\. (.+)$/gm,'<li>$1</li>');
  html=html.split('\n').map(l=>{
    if(l.match(/^<(h[1-6]|li|hr|blockquote|ul|ol|pre)/))return l;
    if(l.trim()==='')return '<br>';
    return `<p>${l}</p>`;
  }).join('\n');
  html=html.replace(/(<li[^>]*>.*<\/li>\n?)+/g,m=>`<ul style="list-style:none;padding-left:0">${m}</ul>`);
  preview.innerHTML=html;
}

// ====== NOTE-LEVEL LOCK ======
function openNoteLock(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  const hasPass=!!n.notePassHash;
  document.getElementById('note-old-pass') && (document.getElementById('note-old-pass').value='');
  document.getElementById('note-new-pass').value='';
  document.getElementById('note-new-pass-confirm').value='';
  hideAlert('note-pass-alert');
  const desc=document.getElementById('note-pass-modal-desc');
  if(desc)desc.textContent=hasPass?'Change or remove this note\'s password lock':'Lock this note with its own password';
  // Show/hide old password field
  const oldRow=document.getElementById('note-old-pass-row');
  if(oldRow)oldRow.style.display=hasPass?'block':'none';
  // Show/hide remove button
  const removeBtn=document.getElementById('note-remove-lock-btn');
  if(removeBtn)removeBtn.style.display=hasPass?'':'none';
  show('note-pass-modal');
}
async function setNoteLock(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  const p=document.getElementById('note-new-pass').value;
  const c=document.getElementById('note-new-pass-confirm').value;
  if(!p){showAlert('note-pass-alert','Enter a new password.');return;}
  if(p!==c){showAlert('note-pass-alert','Passwords do not match.');return;}
  // If note already has a password, require old password before changing
  if(n.notePassHash){
    const oldP=document.getElementById('note-old-pass').value;
    if(!oldP){showAlert('note-pass-alert','Enter your current note password to change it.');return;}
    const oldHash=await hashPassword(oldP,n.notePassSalt);
    if(oldHash!==n.notePassHash){showAlert('note-pass-alert','Current note password is incorrect.');return;}
  }
  const wasLocked=!!n.notePassHash;
  const salt=genSalt();
  const hash=await hashPassword(p,salt);
  n.notePassHash=hash;n.notePassSalt=salt;
  S.noteLockedUnlocked[n.id]=true;
  closeModal('note-pass-modal');
  markUnsaved();
  updateRelockBtn();
  showToast(wasLocked?'Note password updated 🔒':'Note password set 🔒');
}
async function removeNoteLock(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n||!n.notePassHash)return;
  // Always require current password before removing
  const p=document.getElementById('note-old-pass').value;
  if(!p){showAlert('note-pass-alert','Enter your current note password to remove the lock.');return;}
  const hash=await hashPassword(p,n.notePassSalt);
  if(hash!==n.notePassHash){showAlert('note-pass-alert','Incorrect password — cannot remove lock.');return;}
  delete n.notePassHash;delete n.notePassSalt;
  delete S.noteLockedUnlocked[n.id];
  // Restore real title in editor
  const titleInput=document.getElementById('note-title');
  if(titleInput){titleInput.value=n.title||'';titleInput.readOnly=false;titleInput.style.color='';}
  closeModal('note-pass-modal');
  renderNoteList();
  markUnsaved();
  showToast('Note lock removed ✓');
}
// ====== LOCK / UNLOCK ANIMATIONS ======
function animateLockScreen(){
  const editor=document.querySelector('.editor');
  if(!editor)return;
  editor.classList.remove('unlock-animation');
  editor.classList.add('lock-animation');
  setTimeout(()=>editor.classList.remove('lock-animation'),400);
}
function animateUnlockScreen(){
  const editor=document.querySelector('.editor');
  if(!editor)return;
  editor.classList.remove('lock-animation');
  editor.classList.add('unlock-animation');
  setTimeout(()=>editor.classList.remove('unlock-animation'),400);
}

async function unlockNote(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  const p=document.getElementById('note-lock-input').value;
  const errEl=document.getElementById('note-lock-err');
  if(!p){if(errEl)errEl.textContent='Enter the note password.';return;}
  const hash=await hashPassword(p,n.notePassSalt);
  if(hash!==n.notePassHash){if(errEl)errEl.textContent='Wrong password.';return;}
  S.noteLockedUnlocked[n.id]=true;
  // Restore real title
  const titleInput=document.getElementById('note-title');
  titleInput.value=n.title||'';
  titleInput.readOnly=false;
  titleInput.style.color='';
  document.getElementById('note-lock-overlay').classList.add('hidden');
  document.getElementById('note-content').style.display='';
  document.getElementById('note-lock-input').value='';
  if(errEl)errEl.textContent='';
  // Restore full panel
  const floatPanel=document.getElementById('note-float-panel');
  if(floatPanel)floatPanel.classList.remove('locked-mode');
  animateUnlockScreen();
  renderNoteList();
  updateRelockBtn();
  showToast('Note unlocked 🔓');
}

// ====== FIND & REPLACE ======
function openFindReplace(){
  document.getElementById('find-replace-bar').classList.remove('hidden');
  document.getElementById('fr-find').focus();
}
function closeFindReplace(){
  document.getElementById('find-replace-bar').classList.add('hidden');
  S.frMatches=[];S.frIndex=0;
  document.getElementById('fr-info').textContent='';
}
function frHighlight(){
  const term=document.getElementById('fr-find').value;
  S.frMatches=[];S.frIndex=0;
  if(!term){document.getElementById('fr-info').textContent='';return;}
  const content=document.getElementById('note-content').value;
  let idx=0;
  while((idx=content.indexOf(term,idx))!==-1){S.frMatches.push(idx);idx+=term.length;}
  document.getElementById('fr-info').textContent=S.frMatches.length?`${S.frIndex+1}/${S.frMatches.length}`:'No match';
}
function frNext(){if(!S.frMatches.length)return;S.frIndex=(S.frIndex+1)%S.frMatches.length;frGoTo();}
function frPrev(){if(!S.frMatches.length)return;S.frIndex=(S.frIndex-1+S.frMatches.length)%S.frMatches.length;frGoTo();}
function frGoTo(){
  const ta=document.getElementById('note-content');
  const term=document.getElementById('fr-find').value;
  const pos=S.frMatches[S.frIndex];
  ta.focus();ta.setSelectionRange(pos,pos+term.length);
  document.getElementById('fr-info').textContent=`${S.frIndex+1}/${S.frMatches.length}`;
}
function frReplaceCurrent(){
  if(!S.frMatches.length)return;
  const ta=document.getElementById('note-content');
  const term=document.getElementById('fr-find').value;
  const rep=document.getElementById('fr-replace').value;
  const pos=S.frMatches[S.frIndex];
  const content=ta.value;
  ta.value=content.slice(0,pos)+rep+content.slice(pos+term.length);
  markUnsaved();frHighlight();
}
function frReplaceAll(){
  const ta=document.getElementById('note-content');
  const term=document.getElementById('fr-find').value;
  const rep=document.getElementById('fr-replace').value;
  if(!term)return;
  const count=(ta.value.split(term).length-1);
  ta.value=ta.value.split(term).join(rep);
  markUnsaved();frHighlight();
  showToast(`Replaced ${count} occurrence(s) ✓`);
}

// ====== APPEARANCE ======
// ===== APPEARANCE LIVE PREVIEW =====
let _appearancePrevState = null; // snapshot before modal open
function openAppearanceModal(){
  // Snapshot current state
  _appearancePrevState = {
    fontSize: S.appearance.fontSize,
    accent: S.appearance.accent,
    viewMode: S.appearance.viewMode,
    themeClass: _currentThemeClass(),
  };
  // Sync slider
  const sl = document.getElementById('font-slider-modal');
  if(sl) sl.value = S.appearance.fontSize||14;
  const lbl = document.getElementById('font-size-label');
  if(lbl) lbl.textContent = S.appearance.fontSize||14;
  // Sync active swatch
  document.querySelectorAll('.color-swatch').forEach(d=>d.classList.toggle('active',d.dataset.accent===(S.appearance.accent||'gold')));
  // Update dashboard
  _updateAppearanceDashboard();
  show('appearance-modal');
}
function _currentThemeClass(){
  const cls = document.documentElement.className;
  const match = cls.match(/theme-[\w-]+/);
  return match ? match[0] : '';
}
function livePreviewFontSize(val){
  document.documentElement.style.setProperty('--editor-font-size',val+'px');
  const lbl=document.getElementById('font-size-label');
  if(lbl)lbl.textContent=val;
  S.appearance.fontSize=parseInt(val);
}
function livePreviewAccent(name){
  applyAccent(name);
  // Also update preview strip border color
  const strip = document.getElementById('appearance-preview-strip');
  if(strip) strip.style.borderColor = 'var(--gold-dim)';
}
function applyFontSize(val){
  document.documentElement.style.setProperty('--editor-font-size',val+'px');
  const lbl=document.getElementById('font-size-label');
  if(lbl)lbl.textContent=val;
  const sl1=document.getElementById('font-slider');
  const sl2=document.getElementById('font-slider-modal');
  if(sl1)sl1.value=val;
  if(sl2)sl2.value=val;
  S.appearance.fontSize=parseInt(val);
}
function applyAccent(name){
  const accents={
    gold:{g:'#c9a84c',g2:'#e8c56a',gd:'#6a5828'},
    blue:{g:'#4a8fc9',g2:'#6aaae8',gd:'#2a5a8a'},
    green:{g:'#4cc98a',g2:'#6ae8a8',gd:'#2a7a52'},
    rose:{g:'#c94c8a',g2:'#e86aaa',gd:'#8a2a5a'},
    amber:{g:'#c97a4c',g2:'#e8986a',gd:'#8a4a2a'},
    violet:{g:'#9a4cc9',g2:'#b86ae8',gd:'#6a2a8a'},
    'dark-gold':{g:'#a07820',g2:'#c9a84c',gd:'#5a4010'},
    hacker:{g:'#22ff22',g2:'#55ff55',gd:'#008800'},
    midnight:{g:'#6b9bd2',g2:'#88b5e8',gd:'#2a4a7a'},
    frost:{g:'#a0c8e8',g2:'#c0d8f0',gd:'#406080'},
    amoled:{g:'#ffffff',g2:'#e0e0e0',gd:'#888888'},
  };
  const a=accents[name]||accents.gold;
  const r=document.documentElement;
  r.style.setProperty('--gold',a.g);
  r.style.setProperty('--gold2',a.g2);
  r.style.setProperty('--gold-dim',a.gd);
  document.querySelectorAll('.color-swatch').forEach(d=>{
    d.classList.toggle('active',d.dataset.accent===name);
  });
  S.appearance.accent=name;
}
function applyThemePreset(preset){
  // Remove all theme classes
  const themes=['theme-hacker','theme-midnight','theme-frost','theme-pure-black'];
  themes.forEach(t=>document.documentElement.classList.remove(t));
  document.documentElement.classList.remove('light','dark');
  if(preset==='hacker'){
    document.documentElement.classList.add('dark','theme-hacker');
    livePreviewAccent('hacker');
  }else if(preset==='midnight'){
    document.documentElement.classList.add('dark','theme-midnight');
    livePreviewAccent('midnight');
  }else if(preset==='frost'){
    document.documentElement.classList.add('dark','theme-frost');
    livePreviewAccent('frost');
  }else if(preset==='pure-black'){
    document.documentElement.classList.add('dark','theme-pure-black');
    livePreviewAccent('amoled');
  }else if(preset==='light'){
    document.documentElement.classList.add('light');
    livePreviewAccent('gold');
  }else{
    document.documentElement.classList.add('dark');
    livePreviewAccent('gold');
  }
  S.appearance.themePreset = preset;
  showToast('Theme: '+preset+' ✓');
}
function cancelAppearance(){
  // Restore previous state
  if(_appearancePrevState){
    applyFontSize(_appearancePrevState.fontSize||14);
    applyAccent(_appearancePrevState.accent||'gold');
    setViewMode(_appearancePrevState.viewMode||'comfortable');
  }
  _appearancePrevState=null;
  closeModal('appearance-modal');
}
function saveAppearance(){
  try{localStorage.setItem('sn_appearance',JSON.stringify(S.appearance));}catch{}
  _appearancePrevState=null;
  closeModal('appearance-modal');
  showToast('Appearance saved ✓');
}
function loadAppearance(){
  try{
    const saved=localStorage.getItem('sn_appearance');
    if(saved){
      const a=JSON.parse(saved);
      if(a.fontSize)applyFontSize(a.fontSize);
      if(a.accent)applyAccent(a.accent);
      if(a.viewMode)setViewMode(a.viewMode);
      if(a.themePreset)applyThemePreset(a.themePreset);
      S.appearance=a;
    }
  }catch{}
}
function setViewMode(mode){
  document.body.classList.toggle('compact-view',mode==='compact');
  document.getElementById('view-comfortable')?.classList.toggle('active',mode==='comfortable');
  document.getElementById('view-compact')?.classList.toggle('active',mode==='compact');
  S.appearance.viewMode=mode;
}
function _updateAppearanceDashboard(){
  const total = (S.notes||[]).filter(n=>!n.deleted).length;
  const locked = (S.notes||[]).filter(n=>!n.deleted&&n.notePassHash).length;
  const trashed = (S.notes||[]).filter(n=>n.deleted).length;
  const pinned = (S.notes||[]).filter(n=>!n.deleted&&n.pinned).length;
  const setDash = (id,val)=>{ const el=document.getElementById(id); if(el)el.textContent=val; };
  setDash('dash-total-notes',total);
  setDash('dash-locked-notes',locked);
  setDash('dash-trash-notes',trashed);
  setDash('dash-pinned-notes',pinned);
}

// ====== AUTO-SAVE INDICATOR ======
let _autoSaveTimer = null;
function showSavingIndicator(){
  const ss = document.getElementById('save-status');
  if(ss){ ss.textContent='Saving…'; ss.className='save-status unsaved'; }
}
function markSaved(){
  S.unsaved=false;
  const ss=document.getElementById('save-status');
  if(ss){ ss.textContent='Saved'; ss.className='save-status saved'; }
  // Briefly show "Saved ✓" then fade back
  setTimeout(()=>{ if(ss&&ss.textContent==='Saved'){ ss.textContent='Saved ✓'; setTimeout(()=>{ if(ss.textContent==='Saved ✓')ss.textContent='Saved'; },1200); }},100);
}



// ====== PASSWORD STRENGTH ======
function updatePwStrength(val){
  const fill=document.getElementById('pw-strength-fill');
  const lbl=document.getElementById('pw-strength-label');
  if(!fill||!lbl)return;
  let score=0;
  if(val.length>=8)score++;
  if(val.length>=12)score++;
  if(/[A-Z]/.test(val))score++;
  if(/[0-9]/.test(val))score++;
  if(/[^A-Za-z0-9]/.test(val))score++;
  const levels=[
    {pct:0,color:'transparent',label:''},
    {pct:20,color:'#c94c4c',label:'Very Weak'},
    {pct:40,color:'#c97a4c',label:'Weak'},
    {pct:60,color:'#c9a84c',label:'Fair'},
    {pct:80,color:'#4a8fc9',label:'Strong'},
    {pct:100,color:'#4cc98a',label:'Very Strong'},
  ];
  const l=levels[score]||levels[0];
  fill.style.width=l.pct+'%';
  fill.style.background=l.color;
  lbl.textContent=l.label;
  lbl.style.color=l.color;
}

// ====== FOLDERS ======
function getFolders(){
  try{
    const v=localStorage.getItem('sn_folders');
    const folders=v?JSON.parse(v):[];
    // Remove any leftover hidden_vault entries
    const cleaned=folders.filter(f=>f.id!=='hidden_vault'&&!f.hidden);
    if(cleaned.length!==folders.length){
      localStorage.setItem('sn_folders',JSON.stringify(cleaned));
    }
    return cleaned;
  }
  catch{return[];}
}
function saveFolders(folders){try{localStorage.setItem('sn_folders',JSON.stringify(folders));}catch{}}

function renderFolderList(){
  const wrap=document.getElementById('folder-list-wrap');
  if(!wrap)return;
  // Filter out any leftover hidden_vault folder
  const folders=getFolders().filter(f=>f.id!=='hidden_vault'&&!f.hidden);
  let html=`<button class="folder-chip${!S.activeFolderFilter?' active':''}" onclick="setFolderFilter(null)">
    <svg viewBox="0 0 24 24"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg>
    All Notes
    <span class="folder-count">${S.notes.filter(n=>!n.deleted).length}</span>
  </button>`;
  folders.forEach(f=>{
    const count=S.notes.filter(n=>!n.deleted&&n.folder===f.id).length;
    html+=`<button class="folder-chip${S.activeFolderFilter===f.id?' active':''}" onclick="setFolderFilter('${f.id}')">
      <svg viewBox="0 0 24 24"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg>
      ${esc(f.name)}
      <span class="folder-count">${count}</span>
    </button>`;
  });
  wrap.innerHTML=html;
}

function setFolderFilter(folderId){
  S.activeFolderFilter=folderId;
  renderFolderList();
  renderNoteList();
}

function openFolderManager(){
  renderFolderManageList();
  show('folder-modal');
}
function renderFolderManageList(){
  const folders=getFolders();
  const list=document.getElementById('folder-manage-list');
  if(!folders.length){list.innerHTML='<div style="font-size:12px;color:var(--text3);text-align:center;padding:12px">No folders yet</div>';return;}
  list.innerHTML=folders.map(f=>`
    <div style="display:flex;align-items:center;gap:8px;padding:8px;background:var(--surface2);border:1px solid var(--border);border-radius:6px;margin-bottom:4px">
      <svg style="width:13px;height:13px;stroke:var(--gold);fill:none;stroke-width:2" viewBox="0 0 24 24"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg>
      <span style="flex:1;font-size:13px">${esc(f.name)}</span>
      <span style="font-size:10px;color:var(--text3)">${S.notes.filter(n=>!n.deleted&&n.folder===f.id).length} notes</span>
      <button onclick="deleteFolder('${f.id}')" style="background:none;border:none;color:var(--danger);cursor:pointer;font-size:13px;padding:0 4px" title="Delete folder">✕</button>
    </div>`).join('');
}
function addFolder(){
  const name=document.getElementById('folder-new-name').value.trim();
  if(!name)return;
  const folders=getFolders();
  if(folders.find(f=>f.name.toLowerCase()===name.toLowerCase())){showToast('Folder already exists','warn');return;}
  folders.push({id:'folder_'+Date.now(),name});
  saveFolders(folders);
  document.getElementById('folder-new-name').value='';
  renderFolderManageList();
  renderFolderList();
  showToast('Folder "'+name+'" created ✓');
}
function deleteFolder(fid){
  if(!confirm('Delete this folder? Notes inside will move to "All Notes".'))return;
  const folders=getFolders().filter(f=>f.id!==fid);
  saveFolders(folders);
  S.notes.forEach(n=>{if(n.folder===fid)delete n.folder;});
  if(S.activeFolderFilter===fid)S.activeFolderFilter=null;
  renderFolderManageList();
  renderFolderList();
  renderNoteList();
}

// ====== NOTE COLOR LABELS ======
function setNoteColor(color){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  n.color=color||null;
  // Update picker UI
  document.querySelectorAll('.note-color-dot').forEach(d=>{
    d.classList.remove('active');
    const dc=d.dataset.color;
    if((!color&&d.id==='color-none')||(color&&dc===color))d.classList.add('active');
  });
  markUnsaved();
}
function updateColorPicker(note){
  document.querySelectorAll('.note-color-dot').forEach(d=>{
    d.classList.remove('active');
    const dc=d.dataset.color;
    const c=note?note.color:null;
    if((!c&&d.id==='color-none')||(c&&dc===c))d.classList.add('active');
  });
}

// ====== TRASH (SOFT DELETE) ======
function getTrashPin(){try{return JSON.parse(localStorage.getItem('sn_trash_pin')||'null');}catch{return null;}}
function saveTrashPin(){ // called from modal
  const current=document.getElementById('trash-pin-current')?.value||'';
  const pin=document.getElementById('trash-pin-new').value;
  const conf=document.getElementById('trash-pin-new-confirm').value;
  const errEl=document.getElementById('trash-pin-setup-err');
  const existingPin=getTrashPin();

  // If a PIN already exists, require current PIN verification
  if(existingPin){
    if(!current){errEl.textContent='Enter your current Trash PIN to change it.';errEl.className='alert danger show';return;}
    // Verify current PIN async
    hashPassword(current, existingPin.salt).then(hash=>{
      if(hash!==existingPin.hash){errEl.textContent='Current Trash PIN is incorrect.';errEl.className='alert danger show';return;}
      _doSaveTrashPin(pin,conf,errEl);
    });
    return;
  }
  _doSaveTrashPin(pin,conf,errEl);
}
function _doSaveTrashPin(pin,conf,errEl){
  if(pin && (pin.length<4||pin.length>8)){errEl.textContent='PIN must be 4–8 digits.';errEl.className='alert danger show';return;}
  if(pin && !/^\d+$/.test(pin)){errEl.textContent='Only numbers allowed.';errEl.className='alert danger show';return;}
  if(pin !== conf){errEl.textContent='PINs do not match.';errEl.className='alert danger show';return;}
  if(pin){
    const salt=genSalt();
    hashPassword(pin,salt).then(hash=>{
      localStorage.setItem('sn_trash_pin',JSON.stringify({hash,salt,len:pin.length}));
      showToast('Trash PIN set ✓');
      closeModal('trash-pin-setup-modal');
      document.getElementById('trash-pin-new').value='';
      document.getElementById('trash-pin-new-confirm').value='';
      if(document.getElementById('trash-pin-current'))document.getElementById('trash-pin-current').value='';
      errEl.className='alert danger';
    });
  }else{
    localStorage.removeItem('sn_trash_pin');
    showToast('Trash PIN removed');
    closeModal('trash-pin-setup-modal');
    errEl.className='alert danger';
  }
}
function removeTrashPin(){
  const existingPin=getTrashPin();
  if(!existingPin){showToast('No PIN set','warn');return;}
  const current=document.getElementById('trash-pin-current')?.value||'';
  if(!current){
    document.getElementById('trash-pin-setup-err').textContent='Enter your current PIN to remove it.';
    document.getElementById('trash-pin-setup-err').className='alert danger show';
    return;
  }
  hashPassword(current,existingPin.salt).then(hash=>{
    if(hash!==existingPin.hash){
      document.getElementById('trash-pin-setup-err').textContent='Incorrect PIN.';
      document.getElementById('trash-pin-setup-err').className='alert danger show';
      return;
    }
    localStorage.removeItem('sn_trash_pin');
    showToast('Trash PIN removed ✓');
    closeModal('trash-pin-setup-modal');
  });
}
function openTrashPinSettings(){
  document.getElementById('trash-pin-new').value='';
  document.getElementById('trash-pin-new-confirm').value='';
  if(document.getElementById('trash-pin-current'))document.getElementById('trash-pin-current').value='';
  document.getElementById('trash-pin-setup-err').className='alert danger';
  const existingPin=getTrashPin();
  const currentRow=document.getElementById('trash-pin-current-row');
  const removeBtn=document.getElementById('trash-pin-remove-btn');
  const desc=document.getElementById('trash-pin-setup-desc');
  if(existingPin){
    if(currentRow)currentRow.style.display='block';
    if(removeBtn)removeBtn.style.display='';
    if(desc)desc.textContent='A PIN is currently set. Enter it to change or remove.';
  }else{
    if(currentRow)currentRow.style.display='none';
    if(removeBtn)removeBtn.style.display='none';
    if(desc)desc.textContent='Set a 4–8 digit PIN to protect the Trash.';
  }
  show('trash-pin-setup-modal');
}

function openTrash(){
  S._trashUnlocked=S._trashUnlocked||false;
  const trashPin=getTrashPin();
  const gate=document.getElementById('trash-pin-gate');
  const contents=document.getElementById('trash-contents');
  if(trashPin&&!S._trashUnlocked){
    gate.style.display='block';
    contents.style.display='none';
    document.getElementById('trash-pin-input').value='';
    resetTrashPinDots();
    document.getElementById('trash-pin-err').textContent='';
    // Resize dots based on PIN length
    const len=trashPin.len||4;
    for(let i=0;i<8;i++){
      const d=document.getElementById('tpd'+i);
      if(d)d.style.display=i<len?'block':'none';
    }
  }else{
    gate.style.display='none';
    contents.style.display='block';
    renderTrashList();
  }
  show('trash-modal');
}
function onTrashPinInput(){
  const val=document.getElementById('trash-pin-input').value;
  const len=getTrashPin()?.len||4;
  for(let i=0;i<len;i++){
    const d=document.getElementById('tpd'+i);
    if(d)d.classList.toggle('filled',i<val.length);
  }
}
function resetTrashPinDots(){for(let i=0;i<8;i++){const d=document.getElementById('tpd'+i);if(d)d.classList.remove('filled');}}
async function verifyTrashPin(){
  const val=document.getElementById('trash-pin-input').value;
  const trashPin=getTrashPin();
  if(!trashPin){S._trashUnlocked=true;document.getElementById('trash-pin-gate').style.display='none';document.getElementById('trash-contents').style.display='block';renderTrashList();return;}
  const hash=await hashPassword(val,trashPin.salt);
  if(hash===trashPin.hash){
    S._trashUnlocked=true;
    document.getElementById('trash-pin-gate').style.display='none';
    document.getElementById('trash-contents').style.display='block';
    renderTrashList();
    document.getElementById('trash-pin-err').textContent='';
    document.getElementById('trash-pin-input').value='';
    resetTrashPinDots();
  }else{
    document.getElementById('trash-pin-err').textContent='Wrong PIN';
    document.getElementById('trash-pin-input').value='';
    resetTrashPinDots();
  }
}

function renderTrashList(){
  const trashed=S.notes.filter(n=>n.deleted);
  const list=document.getElementById('trash-list');
  updateTrashBadge();
  if(!trashed.length){
    list.innerHTML='<div style="font-size:13px;color:var(--text3);text-align:center;padding:20px">Trash is empty</div>';
    return;
  }
  list.innerHTML=trashed.map(n=>`
    <div class="trash-note-item">
      <div class="trash-note-title">${esc(n.title||'Untitled')}</div>
      <div class="trash-note-date">Deleted: ${fmtDate(n.deletedAt||n.updatedAt)}</div>
      <div class="trash-note-actions">
        <button class="trash-restore-btn" onclick="restoreNote('${n.id}')">↩ Restore</button>
        <button class="trash-perm-btn" onclick="permanentlyDelete('${n.id}')">🔥 Delete Forever</button>
      </div>
    </div>`).join('');
}

function updateTrashBadge(){
  const count=S.notes.filter(n=>n.deleted).length;
  const badge=document.getElementById('trash-count-badge');
  if(badge){badge.textContent=count;badge.style.display=count>0?'':'none';}
}

function restoreNote(id){
  const n=S.notes.find(x=>x.id===id);
  if(!n)return;
  n.deleted=false;
  delete n.deletedAt;
  saveCurrentNoteById(id).then(()=>{renderTrashList();renderNoteList();renderFolderList();showToast('Note restored ✓');});
}
async function saveCurrentNoteById(id){
  const n=S.notes.find(x=>x.id===id);
  if(!n||!S.notesDir)return;
  try{const enc=await encryptNote(n);await writeFile(S.notesDir,id+'.json',JSON.stringify(enc));}catch{}
}
async function permanentlyDelete(id){
  if(!confirm('Permanently delete this note? This cannot be undone.'))return;
  try{await secureDeleteFile(S.notesDir,id+'.json');}catch{}
  S.notes=S.notes.filter(x=>x.id!==id);
  renderTrashList();renderNoteList();renderFolderList();showToast('Note permanently deleted 🔥');
}
async function emptyTrash(){
  const trashed=S.notes.filter(n=>n.deleted);
  if(!trashed.length){showToast('Trash is already empty');return;}
  if(!confirm(`Permanently delete all ${trashed.length} note(s) in Trash? Cannot be undone.`))return;
  for(const n of trashed){try{await secureDeleteFile(S.notesDir,n.id+'.json');}catch{}}
  S.notes=S.notes.filter(n=>!n.deleted);
  renderTrashList();renderNoteList();renderFolderList();showToast('Trash emptied 🔥');
}
async function restoreAllFromTrash(){
  const trashed=S.notes.filter(n=>n.deleted);
  if(!trashed.length){showToast('Trash is empty');return;}
  for(const n of trashed){n.deleted=false;delete n.deletedAt;await saveCurrentNoteById(n.id);}
  renderTrashList();renderNoteList();renderFolderList();showToast(`${trashed.length} note(s) restored ✓`);
}

// ====== TEMPLATES ======
const TEMPLATES={
  blank:{title:'',content:''},
  daily:{
    title:`Daily Journal — ${new Date().toLocaleDateString(undefined,{weekday:'long',year:'numeric',month:'long',day:'numeric'})}`,
    content:`## ${new Date().toLocaleDateString(undefined,{weekday:'long',year:'numeric',month:'long',day:'numeric'})}\n\n**Mood:** 😊\n\n### Today's Focus\n- [ ] \n- [ ] \n\n### Notes & Thoughts\n\n\n### Gratitude\n1. \n2. \n3. `
  },
  meeting:{
    title:'Meeting Notes — '+new Date().toLocaleDateString(),
    content:`## Meeting Notes\n**Date:** ${new Date().toLocaleDateString()}\n**Attendees:** \n**Agenda:** \n\n---\n\n### Discussion Points\n- \n\n### Decisions Made\n- \n\n### Action Items\n- [ ] \n- [ ] `
  },
  todo:{
    title:'To-Do List',
    content:`## To-Do List\n\n### 🔴 Urgent\n- [ ] \n\n### 🟡 This Week\n- [ ] \n- [ ] \n\n### 🟢 Someday\n- [ ] `
  },
  idea:{
    title:'💡 New Idea',
    content:`## Idea\n\n**Summary:** \n\n**Why it matters:** \n\n**Next Steps:**\n- [ ] Research\n- [ ] Draft\n- [ ] Review`
  },
  password:{
    title:'🔐 Credentials',
    content:`## Login Details\n\n**Service:** \n**Username/Email:** \n**Password:** \n**URL:** \n**Notes:** `
  }
};

function openTemplateModal(){
  if(S.unsaved){const ok=confirm('You have unsaved changes. Discard them?');if(!ok)return;}
  show('template-modal');
}
function applyTemplate(type){
  closeModal('template-modal');
  const tmpl=TEMPLATES[type];
  const n={id:genId(),title:tmpl.title,content:tmpl.content,createdAt:Date.now(),updatedAt:Date.now()};
  // Auto-assign to active folder (including hidden vault)
  if(S.activeFolderFilter)n.folder=S.activeFolderFilter;
  S.notes.unshift(n);S.currentNoteId=n.id;
  S.noteImages[n.id]=[];
  renderNoteList();renderFolderList();showEditor(n);
  if(!tmpl.title)document.getElementById('note-title').focus();
  else document.getElementById('note-content').focus();
  markUnsaved();
}

// ====== PLAIN EXPORT (TXT / MD) ======
let _exportFmt='txt';
function openExportModal(){
  if(!S.currentNoteId){showToast('No note selected','warn');return;}
  _exportFmt='txt';
  document.getElementById('exp-txt-btn').classList.add('active');
  document.getElementById('exp-md-btn').classList.remove('active');
  document.getElementById('export-preview-label').textContent='Exports the note title + content as plain text.';
  show('note-export-modal');
}
function selectExportFmt(fmt){
  _exportFmt=fmt;
  document.getElementById('exp-txt-btn').classList.toggle('active',fmt==='txt');
  document.getElementById('exp-md-btn').classList.toggle('active',fmt==='md');
  document.getElementById('export-preview-label').textContent=fmt==='md'?'Exports as Markdown file — great for editors like Obsidian.':'Exports as plain text file.';
}
function doExportPlain(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  const title=n.title||'Untitled';
  let body=_exportFmt==='md'
    ?`# ${title}\n\n${n.content||''}`
    :`${title}\n${'─'.repeat(title.length)}\n\n${n.content||''}`;
  const blob=new Blob([body],{type:'text/plain;charset=utf-8'});
  const url=URL.createObjectURL(blob);
  const a=document.createElement('a');
  a.href=url;a.download=title.replace(/[^a-z0-9_\- ]/gi,'_').slice(0,60)+('+_securenote.'+_exportFmt);
  a.click();URL.revokeObjectURL(url);
  closeModal('note-export-modal');
  showToast('Exported as .'+_exportFmt+' ✓');
}

// ====== INTERACTIVE CHECKLISTS in Markdown Preview ======
function renderMarkdownWithChecklists(text){
  // Transform - [ ] and - [x] into HTML checkboxes
  let html=text;
  // Replace - [x] checked
  html=html.replace(/^- \[x\] (.*)$/gm,(match,p1)=>`<li class="task-list-item checked" data-task-text="${esc(p1)}"><input type="checkbox" class="task-checkbox" checked onchange="syncCheckboxToContent(this)"> <span>${esc(p1)}</span></li>`);
  // Replace - [ ] unchecked
  html=html.replace(/^- \[ \] (.*)$/gm,(match,p1)=>`<li class="task-list-item" data-task-text="${esc(p1)}"><input type="checkbox" class="task-checkbox" onchange="syncCheckboxToContent(this)"> <span>${esc(p1)}</span></li>`);
  return html;
}

function syncCheckboxToContent(cb){
  const li=cb.closest('li');
  const taskText=li.dataset.taskText;
  const textarea=document.getElementById('note-content');
  let content=textarea.value;
  if(cb.checked){
    content=content.replace(`- [ ] ${taskText}`,`- [x] ${taskText}`);
    li.classList.add('checked');
  }else{
    content=content.replace(`- [x] ${taskText}`,`- [ ] ${taskText}`);
    li.classList.remove('checked');
  }
  textarea.value=content;
  markUnsaved();
}

// ====== DRAG-TO-REORDER NOTE LIST ======
function initDragReorder(){
  const list=document.getElementById('note-list');
  if(!list)return;
  let dragSrcId=null;
  list.addEventListener('dragstart',e=>{
    const item=e.target.closest('.note-item');
    if(!item)return;
    dragSrcId=item.dataset.noteId;
    item.classList.add('dragging');
    e.dataTransfer.effectAllowed='move';
    e.dataTransfer.setData('text/plain',dragSrcId);
  });
  list.addEventListener('dragover',e=>{
    e.preventDefault();
    e.dataTransfer.dropEffect='move';
    document.querySelectorAll('.note-item.drag-over').forEach(x=>x.classList.remove('drag-over'));
    const item=e.target.closest('.note-item');
    if(item&&item.dataset.noteId!==dragSrcId)item.classList.add('drag-over');
  });
  list.addEventListener('dragleave',e=>{
    const item=e.target.closest('.note-item');
    if(item)item.classList.remove('drag-over');
  });
  list.addEventListener('drop',e=>{
    e.preventDefault();
    document.querySelectorAll('.note-item.drag-over,.note-item.dragging').forEach(x=>x.classList.remove('drag-over','dragging'));
    const item=e.target.closest('.note-item');
    if(!item||!dragSrcId||item.dataset.noteId===dragSrcId)return;
    const targetId=item.dataset.noteId;
    const srcIdx=S.notes.findIndex(n=>n.id===dragSrcId);
    const tgtIdx=S.notes.findIndex(n=>n.id===targetId);
    if(srcIdx<0||tgtIdx<0)return;
    const [moved]=S.notes.splice(srcIdx,1);
    S.notes.splice(tgtIdx,0,moved);
    renderNoteList();
    dragSrcId=null;
  });
  list.addEventListener('dragend',e=>{
    document.querySelectorAll('.note-item.dragging,.note-item.drag-over').forEach(x=>x.classList.remove('dragging','drag-over'));
    dragSrcId=null;
  });
}

// ====== PATCH renderNoteList to support new features ======
const _origRenderNoteList=renderNoteList;
renderNoteList=function(){
  const q=document.getElementById('search-input').value.toLowerCase();
  const list=document.getElementById('note-list');
  let filtered=S.notes.filter(n=>{
    if(n.deleted)return false;
    if(S.activeFolderFilter&&n.folder!==S.activeFolderFilter)return false;
    if(!q&&!S.activeTagFilter)return true;
    const textMatch=!q||((n.title||'').toLowerCase().includes(q)||(n.content||'').toLowerCase().includes(q));
    const tagMatch=!S.activeTagFilter||((n.tags||[]).includes(S.activeTagFilter));
    return textMatch&&tagMatch;
  });
  filtered.sort((a,b)=>{
    if(a.pinned&&!b.pinned)return -1;
    if(!a.pinned&&b.pinned)return 1;
    return (b.updatedAt||0)-(a.updatedAt||0);
  });
  if(filtered.length===0){
    list.innerHTML='<div class="empty-notes">'+(q||S.activeTagFilter?'No notes match':'No notes yet.<br>Create your first note!')+'</div>';
  }else{
    list.innerHTML=filtered.map(n=>{
      const isLocked=n.notePassHash&&!S.noteLockedUnlocked[n.id];
      const tags=(n.tags||[]).map(t=>`<span class="note-tag-mini">${esc(t)}</span>`).join('');
      const locked=n.notePassHash?`<span class="note-locked-badge">🔒</span>`:'';
      const colorClass=n.color?' color-'+n.color:'';
      const displayTitle=isLocked?'🔒 Locked Note':esc(n.title||'Untitled');
      const previewClass=isLocked?'note-item-preview is-locked':'note-item-preview';
      const previewContent=isLocked?'Protected Content':esc((n.content||'').slice(0,60)||'No content');
      return`<div class="note-item${n.id===S.currentNoteId?' active':''}${n.pinned?' pinned':''}${colorClass}" 
        onclick="openNote('${n.id}')" 
        data-note-id="${n.id}" 
        draggable="true">
        <div class="note-item-title">${n.pinned?'<span class="note-item-pin">📌</span>':''}${displayTitle}${locked}<span class="enc-badge">${S.encKey&&!S.isDecoy?'🔒':''}</span></div>
        <div class="${previewClass}">${previewContent}</div>
        ${tags&&!isLocked?`<div class="note-item-tags">${tags}</div>`:''}
        <div class="note-item-date">${fmtDate(n.updatedAt)}</div>
      </div>`;
    }).join('');
  }
  document.getElementById('note-count').textContent=S.notes.filter(n=>!n.deleted).length+' note'+(S.notes.filter(n=>!n.deleted).length!==1?'s':'');
  renderTagFilter();
  updateTrashBadge();
};

// ====== PATCH showEditor to support color picker + folder ======
const _origShowEditor=showEditor;
showEditor=function(n){
  _origShowEditor(n);
  updateColorPicker(n);
  // openFloatEditor is already called inside showEditor
};

// ====== PATCH deleteCurrentNote to use Trash ======
async function deleteCurrentNote(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n){closeModal('delete-modal');return;}
  try{
    n.deleted=true;
    n.deletedAt=Date.now();
    const enc=await encryptNote(n);
    await writeFile(S.notesDir,n.id+'.json',JSON.stringify(enc));
    S.currentNoteId=null;S.unsaved=false;
    closeModal('delete-modal');
    // Close float editor
    const backdrop=document.getElementById('note-float-backdrop');
    const panel=document.getElementById('note-float-panel');
    if(panel)panel.classList.remove('open');
    if(backdrop){backdrop.classList.remove('open');setTimeout(()=>{backdrop.style.display='none';},300);}
    document.getElementById('hmac-status').textContent='';
    renderNoteList();renderFolderList();
    updateTrashBadge();
    showToast('Moved to Trash 🗑 (can be restored)');
  }catch(e){closeModal('delete-modal');showToast('Error: '+e.message);}
}

// ====== PATCH saveCurrentNote to include color+folder ======
const _origSaveCurrentNote=saveCurrentNote;
saveCurrentNote=async function(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  n.title=document.getElementById('note-title').value||'Untitled';
  n.content=document.getElementById('note-content').value;
  n.updatedAt=Date.now();
  n.images=S.noteImages[S.currentNoteId]||[];
  // color and folder are already set on the note object
  try{
    const toSave=await encryptNote(n);
    await writeFile(S.notesDir,n.id+'.json',JSON.stringify(toSave));
    markSaved();
    document.getElementById('note-updated').textContent='Saved: '+fmtDate(n.updatedAt);
    document.getElementById('delete-note-name').textContent=n.title;
    S.notes.sort((a,b)=>{
      if(a.pinned&&!b.pinned)return -1;
      if(!a.pinned&&b.pinned)return 1;
      return (b.updatedAt||0)-(a.updatedAt||0);
    });
    renderNoteList();
    showToast('Note saved to USB 🔒 ✓');
  }catch(e){showToast('Save failed: '+e.message);}
};

// ====== PATCH togglePin — fix the broken pin button ======
function togglePin(){
  if(!S.currentNoteId)return;
  const n=S.notes.find(x=>x.id===S.currentNoteId);
  if(!n)return;
  n.pinned=!n.pinned;
  const pinBtn=document.getElementById('pin-btn');
  if(pinBtn){
    pinBtn.style.color=n.pinned?'var(--gold)':'';
    pinBtn.title=n.pinned?'Unpin Note':'Pin Note';
  }
  markUnsaved();
  renderNoteList();
  showToast(n.pinned?'Note pinned 📌':'Note unpinned');
}

// ====== PATCH renderMarkdown to include checklist support ======
const _origRenderMarkdown=renderMarkdown;
renderMarkdown=function(){
  if(typeof renderMarkdown._running)return;
  const content=document.getElementById('note-content').value;
  const preview=document.getElementById('md-preview');
  if(!preview)return;
  // Simple markdown parser (reuse existing logic but add checklist support)
  let html=content
    .replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;')
    .replace(/^######\s(.+)$/gm,'<h6>$1</h6>')
    .replace(/^#####\s(.+)$/gm,'<h5>$1</h5>')
    .replace(/^####\s(.+)$/gm,'<h4>$1</h4>')
    .replace(/^###\s(.+)$/gm,'<h3>$1</h3>')
    .replace(/^##\s(.+)$/gm,'<h2>$1</h2>')
    .replace(/^#\s(.+)$/gm,'<h1>$1</h1>')
    .replace(/\*\*(.+?)\*\*/g,'<strong>$1</strong>')
    .replace(/\*(.+?)\*/g,'<em>$1</em>')
    .replace(/`(.+?)`/g,'<code>$1</code>')
    .replace(/^---$/gm,'<hr>')
    .replace(/\[([^\]]+)\]\(([^)]+)\)/g,'<a href="$2" target="_blank" rel="noopener">$1</a>')
    .replace(/^> (.+)$/gm,'<blockquote>$1</blockquote>');
  // Task lists
  html=html
    .replace(/^- \[x\] (.+)$/gm,(m,p1)=>`<li class="task-list-item checked"><input type="checkbox" class="task-checkbox" checked onchange="syncCheckboxToContent(this)" data-task="${p1.replace(/"/g,'&quot;')}"> <span>${p1}</span></li>`)
    .replace(/^- \[ \] (.+)$/gm,(m,p1)=>`<li class="task-list-item"><input type="checkbox" class="task-checkbox" onchange="syncCheckboxToContent(this)" data-task="${p1.replace(/"/g,'&quot;')}"> <span>${p1}</span></li>`);
  // Fix: patch syncCheckboxToContent to use data-task
  html=html
    .replace(/^- (.+)$/gm,'<li>$1</li>')
    .replace(/^\d+\.\s(.+)$/gm,'<li>$1</li>');
  html=html.replace(/\n/g,'<br>');
  preview.innerHTML='<ul style="list-style:none;padding:0">'+html.replace(/<li class="task/g,'TASKLIST<li class="task').split('TASKLIST').join('')+'</ul>';
  // Actually use simpler approach
  preview.innerHTML=html;
};

// Actually override with a cleaner version:
renderMarkdown=function(){
  const content=document.getElementById('note-content').value;
  const preview=document.getElementById('md-preview');
  if(!preview)return;
  let html=content
    .replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;')
    .replace(/^###### (.+)$/gm,'<h6>$1</h6>').replace(/^##### (.+)$/gm,'<h5>$1</h5>')
    .replace(/^#### (.+)$/gm,'<h4>$1</h4>').replace(/^### (.+)$/gm,'<h3>$1</h3>')
    .replace(/^## (.+)$/gm,'<h2>$1</h2>').replace(/^# (.+)$/gm,'<h1>$1</h1>')
    .replace(/\*\*\*(.+?)\*\*\*/g,'<strong><em>$1</em></strong>')
    .replace(/\*\*(.+?)\*\*/g,'<strong>$1</strong>').replace(/\*(.+?)\*/g,'<em>$1</em>')
    .replace(/~~(.+?)~~/g,'<del>$1</del>')
    .replace(/`([^`]+)`/g,'<code>$1</code>')
    .replace(/^---+$/gm,'<hr>')
    .replace(/\[([^\]]+)\]\(([^)]+)\)/g,'<a href="$2" target="_blank" rel="noopener">$1</a>')
    .replace(/^&gt; (.+)$/gm,'<blockquote>$1</blockquote>')
    // Task lists (must come before regular list)
    .replace(/^- \[x\] (.+)$/gm,(m,p1)=>`<li class="task-list-item checked"><input type="checkbox" class="task-checkbox" checked onchange="syncCheckboxToContent(this)"> <span>${p1}</span></li>`)
    .replace(/^- \[ \] (.+)$/gm,(m,p1)=>`<li class="task-list-item"><input type="checkbox" class="task-checkbox" onchange="syncCheckboxToContent(this)"> <span>${p1}</span></li>`)
    .replace(/^[-*] (.+)$/gm,'<li>$1</li>')
    .replace(/^\d+\. (.+)$/gm,'<li>$1</li>')
    .replace(/(<li.*<\/li>\n?)+/g,m=>`<ul style="list-style:none;padding-left:0">${m}</ul>`)
    .split('\n').map(l=>l.match(/^<[hblup]/)? l : `<p>${l}</p>`).join('');
  preview.innerHTML=html;
};

// ====== PATCH loadNotes to filter trashed from display ======
const _origLoadNotes=loadNotes;
loadNotes=async function(){
  S.notes=[];
  try{
    const files=await listFiles(S.notesDir);
    for(const f of files){
      if(!f.endsWith('.json'))continue;
      const raw=await readFile(S.notesDir,f);
      if(raw){
        try{
          let n=JSON.parse(raw);
          n=await decryptNote(n);
          if(Array.isArray(n.images)&&n.images.length>0)S.noteImages[n.id]=n.images;
          S.notes.push(n);
        }catch{}
      }
    }
    S.notes.sort((a,b)=>(b.updatedAt||0)-(a.updatedAt||0));
  }catch(e){console.error(e);}
  renderNoteList();
  renderFolderList();
  updateTrashBadge();
};

// ====== INIT EXTENSIONS — new state added to init() directly above ======

async function init(){
  S.activeFolderFilter=null;
  S._trashUnlocked=false;
  if(!window.showDirectoryPicker){
    document.getElementById('boot-screen').innerHTML=`
      <div style="text-align:center;padding:40px;max-width:400px">
        <div style="font-family:'Playfair Display',serif;font-size:22px;color:var(--gold);margin-bottom:12px">SecureNote</div>
        <div style="color:var(--danger);font-size:14px;margin-bottom:12px">⚠ File System Access API not supported</div>
        <div style="color:var(--text2);font-size:13px;line-height:1.6">Please open this file in <strong style="color:var(--text)">Google Chrome</strong> or <strong style="color:var(--text)">Microsoft Edge</strong> for USB storage support.</div>
        <div style="margin-top:20px;font-size:11px;color:var(--text3)">Crafted by <span style="color:var(--gold-dim);font-weight:600">JMR</span></div>
      </div>`;
    return;
  }
  loadLockoutState();
  if(isLockedOut())startLockoutCountdown();
  try{
    const h=await dbGet('dirHandle');
    if(h){
      const perm=await h.requestPermission({mode:'readwrite'});
      if(perm==='granted'){
        S.dirHandle=h;
        const vaultDir=await getOrCreateDir(h,'notepad_vault');
        const raw=await readFile(vaultDir,'credentials.json');
        if(raw){
          await loadAuditLog();
          showScreen('login-screen');
          return;
        }
        S.setupDirHandle=h;
        showScreen('setup-screen');
        return;
      }
    }
  }catch{}
  showScreen('connect-screen');
}

document.addEventListener('DOMContentLoaded',()=>{
  const observer=new MutationObserver(()=>{
    if(document.getElementById('app-screen')?.classList.contains('active')){
      initDragReorder();
      observer.disconnect();
    }
  });
  observer.observe(document.body,{attributes:true,subtree:true,attributeFilter:['class']});
  setTimeout(initDragReorder,2000);
});

</script>

<script>
init();
</script>
</body>
</html>
