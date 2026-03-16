# MyProjects
New project for my own

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>EEM — Enterprise Employee Management</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet"/>
<style>
/* ═══ RESET & ROOT ═══════════════════════════════════════════════════════════ */
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#f4faf6;
  --white:#fff;
  --sidebar:#0d4a2f;
  --sidebar-w:220px;
  --topbar-h:56px;
  --blue:#16a34a;--blue-l:#f0fdf4;--blue-xl:#dcfce7;--blue-d:#15803d;
  --teal:#0d9488;--teal-l:#f0fdfa;
  --green:#057a55;--green-l:#def7ec;--green-xl:#a7f3d0;
  --red:#c81e1e;--red-l:#fde8e8;--red-xl:#fca5a5;
  --amber:#92400e;--amber-l:#fef3c7;--amber-xl:#fde68a;
  --orange:#c2410c;--orange-l:#fff7ed;
  --purple:#5521b5;--purple-l:#edebfe;
  --border:#e2e8f0;--border2:#cbd5e1;
  --grey50:#f8fafc;--grey100:#f1f5f9;--grey200:#e2e8f0;--grey300:#cbd5e1;
  --grey400:#94a3b8;--grey500:#64748b;--grey600:#475569;--grey700:#334155;
  --grey800:#1e293b;--grey900:#0f172a;
  --text:#1e293b;--text-m:#64748b;--text-l:#94a3b8;
  --sh-sm:0 1px 3px rgba(0,0,0,.08);
  --sh-md:0 4px 12px rgba(0,0,0,.10);
  --sh-lg:0 8px 28px rgba(0,0,0,.13);
  --r:8px;--r-lg:12px;
  --font:'DM Sans',system-ui,sans-serif;
  --mono:'DM Mono',monospace;
}
html,body{height:100%;overflow:hidden;font-family:var(--font);font-size:13px;color:var(--text)}
input,select,button,textarea{font-family:var(--font);font-size:13px}
button{cursor:pointer;border:none;background:none}
::-webkit-scrollbar{width:4px;height:4px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:#a7f3d0;border-radius:10px}

/* ═══ LAYOUT ══════════════════════════════════════════════════════════════════ */
#app{display:flex;flex-direction:column;height:100vh;overflow:hidden;min-width:860px}
#content-area{flex:1;display:flex;flex-direction:column;overflow:hidden;min-width:0}

/* ═══ TOP NAVIGATION BAR ═══════════════════════════════════════════════════ */
#topnav{
  flex-shrink:0;height:52px;
  background:#0d4a2f;
  display:flex;align-items:center;
  padding:0 16px;gap:0;
  z-index:100;position:relative;
  border-bottom:1px solid rgba(255,255,255,.07);
  overflow:visible;
}
/* Brand */
.tn-brand{display:flex;align-items:center;gap:10px;flex-shrink:0;padding-right:24px;border-right:1px solid rgba(255,255,255,.08);margin-right:4px}
.tn-logo{width:30px;height:30px;border-radius:7px;background:linear-gradient(135deg,#22c55e,#15803d);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:13px;color:#fff;box-shadow:0 2px 6px rgba(22,163,74,.4);flex-shrink:0}
.tn-name{color:#f1f5f9;font-weight:700;font-size:13px;letter-spacing:-.01em;white-space:nowrap}
.tn-ver{display:none}
/* Nav items */
.tn-nav{display:flex;align-items:stretch;height:52px;gap:0;flex:1;padding-left:4px;min-width:0}
.tn-item{
  display:flex;align-items:center;gap:6px;
  padding:0 10px;cursor:pointer;
  color:rgba(255,255,255,.55);font-weight:500;font-size:11px;
  transition:all .15s;white-space:nowrap;
  border-bottom:2px solid transparent;position:relative;flex-shrink:0;
}
.tn-item:hover{color:rgba(255,255,255,.9);background:rgba(255,255,255,.05)}
.tn-item.active{color:#86efac;border-bottom-color:#22c55e;background:rgba(22,163,74,.15)}
.tn-item .tn-icon{font-size:13px}
.tn-item .tn-arrow{font-size:8px;color:rgba(255,255,255,.3);transition:transform .2s;margin-left:2px}
.tn-item.open .tn-arrow{transform:rotate(180deg)}
.tn-item:hover .tn-arrow{transform:rotate(180deg)}
/* hidden menu items per client */
.tn-item.hidden,.tn-sub-item.hidden{display:none!important}
/* Dropdown submenu */
.tn-dropdown{
  position:fixed;top:52px;left:0;
  background:#fff;border:1px solid var(--border);border-radius:10px;
  box-shadow:0 8px 28px rgba(0,0,0,.18);min-width:200px;
  display:none;flex-direction:column;padding:6px 0;z-index:9000;
  animation:dropDown .15s ease;
}
.tn-item:hover > .tn-dropdown{display:flex}
@keyframes dropDown{from{opacity:0;transform:translateY(-6px)}to{opacity:1;transform:translateY(0)}}
.tn-sub-item{
  display:flex;align-items:center;gap:8px;
  padding:9px 16px;cursor:pointer;
  color:var(--grey700);font-size:12px;font-weight:500;
  transition:background .1s;white-space:nowrap;
}
.tn-sub-item:hover{background:#f0fdf4;color:#15803d}
.tn-sub-item.active{background:#dcfce7;color:#15803d;font-weight:600}
.tn-sub-icon{font-size:13px;width:18px;text-align:center;flex-shrink:0}
.tn-spacer{flex:1}
/* Right side controls */
.tn-right{display:flex;align-items:center;gap:6px;flex-shrink:0;padding-left:6px}
/* Client switcher */
.client-switcher{position:relative}
.client-btn{
  display:flex;align-items:center;gap:7px;
  padding:4px 9px;border-radius:6px;
  background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.12);
  color:#f1f5f9;font-size:11px;font-weight:600;cursor:pointer;
  transition:all .15s;white-space:nowrap;
}
.client-btn:hover{background:rgba(255,255,255,.13);border-color:rgba(255,255,255,.2)}
.client-btn .client-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.client-btn .client-arrow{font-size:8px;color:rgba(255,255,255,.4);margin-left:2px;transition:transform .2s}
.client-switcher.open .client-arrow{transform:rotate(180deg)}
.client-dropdown{
  position:absolute;top:calc(100% + 6px);right:0;
  background:#fff;border:1px solid var(--border);border-radius:10px;
  box-shadow:0 8px 28px rgba(0,0,0,.15);min-width:220px;
  display:none;flex-direction:column;padding:8px 0;z-index:600;
  animation:dropDown .15s ease;
}
.client-switcher.open .client-dropdown{display:flex}
.client-option{
  display:flex;align-items:center;gap:10px;
  padding:9px 16px;cursor:pointer;transition:background .1s;
}
.client-option:hover{background:var(--grey50)}
.client-option.active{background:#dcfce7}
.client-option-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0}
.client-option-name{font-size:12px;font-weight:600;color:var(--grey900)}
.client-option-role{font-size:10px;color:var(--text-m);margin-top:1px}
.client-option-badge{margin-left:auto;font-size:9px;font-weight:700;padding:2px 6px;border-radius:8px}
/* Notification button */
.notif-btn{
  position:relative;width:30px;height:30px;border-radius:7px;
  background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.1);
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;transition:all .15s;font-size:16px;color:rgba(255,255,255,.7);
}
.notif-btn:hover{background:rgba(255,255,255,.13)}
.notif-count{
  position:absolute;top:-4px;right:-4px;
  min-width:17px;height:17px;border-radius:10px;
  background:#c81e1e;border:2px solid #0d4a2f;
  font-size:9px;font-weight:700;color:#fff;
  display:flex;align-items:center;justify-content:center;
  padding:0 3px;
}
/* Notification panel */
.notif-panel{
  position:absolute;top:calc(100% + 6px);right:0;
  background:#fff;border:1px solid var(--border);border-radius:12px;
  box-shadow:0 10px 32px rgba(0,0,0,.15);width:360px;
  display:none;flex-direction:column;z-index:600;
  animation:dropDown .15s ease;overflow:hidden;
}
.notif-btn-wrap{position:relative}
.notif-btn-wrap.open .notif-panel{display:flex}
.notif-panel-hd{padding:14px 16px 10px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;flex-shrink:0}
.notif-panel-title{font-size:13px;font-weight:700;color:var(--grey900)}
.notif-mark-all{font-size:11px;color:#16a34a;cursor:pointer;font-weight:600}
.notif-mark-all:hover{text-decoration:underline}
.notif-list{max-height:380px;overflow-y:auto}
.notif-item{
  display:flex;gap:12px;padding:12px 16px;cursor:pointer;
  border-bottom:1px solid var(--grey100);transition:background .1s;
  position:relative;
}
.notif-item:last-child{border-bottom:none}
.notif-item:hover{background:var(--grey50)}
.notif-item.unread{background:#f0fdf4}
.notif-item.unread:hover{background:#dcfce7}
.notif-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;margin-top:4px}
.notif-icon{width:34px;height:34px;border-radius:8px;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:16px}
.notif-body{flex:1;min-width:0}
.notif-title{font-size:12px;font-weight:600;color:var(--grey900)}
.notif-desc{font-size:11px;color:var(--text-m);margin-top:2px;line-height:1.4}
.notif-time{font-size:10px;color:var(--text-l);margin-top:4px}
.notif-unread-dot{width:7px;height:7px;border-radius:50%;background:#16a34a;flex-shrink:0;margin-top:5px}
.notif-panel-ft{padding:10px 16px;border-top:1px solid var(--border);text-align:center}
.notif-panel-ft a{font-size:12px;color:#16a34a;font-weight:600;cursor:pointer}
/* Breadcrumb bar */
#breadbar{
  height:36px;flex-shrink:0;
  background:var(--white);border-bottom:1px solid var(--border);
  border-left:3px solid #16a34a;
  display:flex;align-items:center;padding:0 20px;gap:12px;
  box-shadow:var(--sh-sm);
}
.tb-breadcrumb{font-size:11px;color:var(--text-m);display:flex;align-items:center;gap:5px}
.tb-breadcrumb span{color:var(--text-l)}
/* Avatar */
.tn-avatar{width:30px;height:30px;border-radius:50%;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.15);display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;color:rgba(255,255,255,.8);cursor:pointer;flex-shrink:0}
.tn-avatar:hover{background:rgba(255,255,255,.2)}
/* Divider */
.tn-divider{width:1px;height:18px;background:rgba(255,255,255,.1);margin:0 2px;flex-shrink:0}
/* old topbar compat */
.tb-spacer{flex:1}
.tb-btn{padding:5px 11px;border-radius:6px;font-size:11px;font-weight:500;color:var(--grey600);border:1px solid var(--border);background:var(--white);transition:all .15s}
.tb-btn:hover{background:var(--grey50)}


#client-btn-name{display:none}.user-btn,.client-btn{padding:5px 8px}}
/* ── User panel ──────────────────────────────────────────────── */
.user-btn-wrap{position:relative}
.user-btn{display:flex;align-items:center;gap:6px;padding:4px 8px 4px 5px;border-radius:7px;background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.12);cursor:pointer;transition:all .15s}
.user-btn:hover,.user-btn-wrap.open .user-btn{background:rgba(255,255,255,.14);border-color:rgba(255,255,255,.25)}
.user-avatar-circle{width:24px;height:24px;border-radius:50%;background:linear-gradient(135deg,#22c55e,#15803d);display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;color:#fff;flex-shrink:0;border:1.5px solid rgba(255,255,255,.25)}
.user-btn-name{font-size:11px;font-weight:600;color:#f1f5f9;line-height:1;white-space:nowrap}
.user-btn-role{display:none}
.user-btn-chevron{font-size:9px;color:rgba(255,255,255,.4);margin-left:2px;transition:transform .2s}
.user-btn-wrap.open .user-btn-chevron{transform:rotate(180deg)}
.user-panel{position:absolute;top:calc(100% + 8px);right:0;background:#fff;border:1px solid var(--border);border-radius:12px;box-shadow:0 12px 36px rgba(0,0,0,.18);width:300px;display:none;flex-direction:column;z-index:600;overflow:hidden;animation:dropDown .18s ease}
.user-btn-wrap.open .user-panel{display:flex}
.user-panel-hd{padding:18px 18px 14px;background:linear-gradient(135deg,#052e16 0%,#0d4a2f 100%);display:flex;align-items:center;gap:14px}
.user-panel-avatar{width:46px;height:46px;border-radius:50%;flex-shrink:0;background:linear-gradient(135deg,#22c55e,#15803d);display:flex;align-items:center;justify-content:center;font-size:16px;font-weight:700;color:#fff;border:2px solid rgba(255,255,255,.25);box-shadow:0 2px 8px rgba(0,0,0,.3)}
.user-panel-info{flex:1;min-width:0}
.user-panel-name{font-size:14px;font-weight:700;color:#f0fdf4;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.user-panel-id{font-size:10px;color:rgba(255,255,255,.5);font-family:var(--mono);margin-top:2px}
.user-online-dot{display:flex;align-items:center;gap:5px;margin-top:5px}
.user-online-ind{width:7px;height:7px;border-radius:50%;background:#22c55e;flex-shrink:0}
.user-online-txt{font-size:10px;color:rgba(255,255,255,.55)}
.user-panel-body{padding:10px 0}
.user-row{display:flex;align-items:center;gap:12px;padding:8px 18px}
.user-row-icon{width:32px;height:32px;border-radius:8px;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:15px}
.user-row-lbl{font-size:10px;font-weight:600;color:var(--text-m);text-transform:uppercase;letter-spacing:.06em}
.user-row-val{font-size:12px;font-weight:600;color:var(--grey900);margin-top:1px;display:flex;align-items:center;gap:4px;flex-wrap:wrap}
.user-panel-div{height:1px;background:var(--border);margin:4px 0}
.role-badge{display:inline-flex;align-items:center;padding:2px 8px;border-radius:10px;font-size:10px;font-weight:700}
.user-panel-ft{padding:12px 18px;border-top:1px solid var(--border)}
.signout-btn{width:100%;padding:9px 0;border-radius:8px;background:#fde8e8;border:1px solid #fca5a5;color:#c81e1e;font-size:12px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;transition:all .15s;font-family:var(--font)}
.signout-btn:hover{background:#fca5a5}

/* ── Checks Execution Centre ─────────────────────────────────────────── */
.chk-rdrop{position:absolute;top:calc(100% + 4px);left:0;width:420px;background:var(--white);border:1px solid var(--border);border-radius:10px;box-shadow:0 8px 28px rgba(0,0,0,.15);z-index:9999;display:none;overflow:hidden}
.chk-rdrop.open{display:grid;grid-template-columns:180px 1fr}
.rdrop-cats{border-right:1px solid var(--grey100);padding:6px 0}
.rdrop-cat{display:flex;align-items:center;gap:8px;padding:9px 12px;cursor:pointer;transition:background .1s;font-size:12px;color:var(--grey700)}
.rdrop-cat:hover,.rdrop-cat.active{background:#dcfce7}
.rdrop-cat.active .cat-label{color:#15803d;font-weight:700}
.rdrop-subs{padding:8px 0}
.rdrop-sub-head{padding:4px 12px 8px;font-size:9px;font-weight:700;color:var(--grey400);letter-spacing:.08em;text-transform:uppercase}
.rdrop-sub{display:flex;align-items:center;justify-content:space-between;padding:8px 12px;cursor:pointer;transition:background .1s;font-size:12px;color:var(--grey700)}
.rdrop-sub:hover{background:var(--grey50)}
.rdrop-sub.selected{background:#dcfce7;color:#15803d;font-weight:600}
.chk-progress-bar{height:6px;background:var(--grey200);border-radius:4px;overflow:hidden;width:90px}
.chk-progress-fill{height:100%;border-radius:4px;transition:width .4s ease}
.count-badge-g{font-size:11px;font-weight:700;background:#fff;color:#15803d;padding:2px 8px;border-radius:10px;border:1px solid var(--green-xl)}
.count-badge-r{font-size:11px;font-weight:700;background:#fff;color:#b91c1c;padding:2px 8px;border-radius:10px;border:1px solid var(--red-xl)}
.spin-sm{width:12px;height:12px;border:2px solid rgba(255,255,255,.35);border-top-color:#fff;border-radius:50%;animation:spin .7s linear infinite;display:inline-block;vertical-align:middle}
.highlighted{background:#f0fdf4}
.skeleton-row{height:6px;background:var(--grey200);border-radius:3px;animation:skPulse 1.2s ease-in-out infinite alternate}
@keyframes skPulse{from{opacity:.4}to{opacity:.9}}
.split-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px}
.panel-valid{border:2px solid var(--green-xl)!important}
.panel-issues{border:2px solid var(--red-xl)!important}
.panel-head{padding:8px 14px;display:flex;align-items:center;gap:8px}
.panel-head-valid{background:var(--green-l);border-bottom:1px solid var(--green-xl);border-radius:var(--r-lg) var(--r-lg) 0 0}
.panel-head-issues{background:var(--red-l);border-bottom:1px solid var(--red-xl);border-radius:var(--r-lg) var(--r-lg) 0 0}
.panel-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0}
.panel-rows{overflow-y:auto;max-height:260px}
.panel-row{align-items:center;padding:7px 10px;border-bottom:1px solid var(--grey100);cursor:pointer;transition:background .1s}
.panel-row:hover{background:var(--grey50)}
.panel-row.selected{background:#dcfce7}
/* ═══ MAIN ════════════════════════════════════════════════════════════════════ */
#main{flex:1;overflow:hidden;display:flex;flex-direction:column}
.page{display:none;flex:1;overflow:hidden;flex-direction:column}
.page.active{display:flex}
.page-body{flex:1;overflow-y:auto;padding:24px}

/* ═══ COMPONENTS ══════════════════════════════════════════════════════════════ */
.card{background:var(--white);border-radius:var(--r-lg);border:1px solid var(--border);box-shadow:var(--sh-sm)}
.card-hd{padding:14px 20px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:10px}
.card-title{font-size:13px;font-weight:700;color:var(--grey900)}
.btn{display:inline-flex;align-items:center;gap:6px;padding:7px 16px;border-radius:6px;font-size:12px;font-weight:600;transition:all .15s;border:1px solid transparent;white-space:nowrap}
.btn-sm{padding:5px 12px;font-size:11px}
.btn-xs{padding:3px 9px;font-size:10px}
.btn-primary{background:#16a34a;color:#fff;box-shadow:0 1px 3px rgba(22,163,74,.3)}
.btn-primary:hover{background:#15803d}
.btn-secondary{background:var(--white);color:var(--grey700);border-color:var(--border)}
.btn-secondary:hover{background:var(--grey50)}
.btn-success{background:var(--green);color:#fff}
.btn-success:hover{background:#046c4e}
.btn-danger{background:var(--red-l);color:var(--red);border-color:var(--red-xl)}
.btn-danger:hover{background:#fca5a5}
.btn-ghost{color:#15803d;background:#f0fdf4;border-color:#bbf7d0}
.btn-ghost:hover{background:#dcfce7}
.badge{display:inline-flex;align-items:center;gap:4px;padding:2px 8px;border-radius:12px;font-size:10px;font-weight:700}
.badge-dot{width:5px;height:5px;border-radius:50%;flex-shrink:0}
.pill{padding:2px 7px;border-radius:5px;font-size:10px;font-weight:700}
.tag{padding:2px 7px;border-radius:20px;font-size:10px;font-weight:600}
.form-row{display:flex;gap:14px;flex-wrap:wrap}
.form-group{display:flex;flex-direction:column;gap:5px;min-width:0}
.form-group.flex-1{flex:1}
.form-group.w-half{width:calc(50% - 7px)}
.form-group.w-third{width:calc(33.333% - 10px)}
.lbl{font-size:10px;font-weight:700;color:var(--grey500);text-transform:uppercase;letter-spacing:.06em}
.inp,.sel{
  height:34px;padding:0 10px;border:1px solid var(--border);border-radius:6px;
  font-size:12px;color:var(--text);background:var(--white);
  transition:border-color .15s,box-shadow .15s;outline:none;width:100%;
}
.inp:focus,.sel:focus{border-color:#16a34a;box-shadow:0 0 0 3px rgba(22,163,74,.12)}
.sel{appearance:none;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath d='M2 4l4 4 4-4' stroke='%2394a3b8' stroke-width='1.5' fill='none' stroke-linecap='round' stroke-linejoin='round'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 10px center;padding-right:28px}
.inp.mono{font-family:var(--mono);font-size:11px}
.tab-bar{display:flex;border-bottom:2px solid var(--border);gap:0;overflow-x:auto}
.tab-bar::-webkit-scrollbar{height:0}
.tab-item{padding:10px 18px;font-size:12px;font-weight:600;color:var(--text-m);cursor:pointer;white-space:nowrap;border-bottom:2px solid transparent;margin-bottom:-2px;transition:all .15s}
.tab-item:hover{color:var(--grey800)}
.tab-item.active{color:#16a34a;border-bottom-color:#16a34a}
.tab-content{display:none}
.tab-content.active{display:block}
.data-table{width:100%;border-collapse:collapse;font-size:12px}
.data-table th{padding:9px 12px;text-align:left;font-size:10px;font-weight:700;color:var(--grey500);letter-spacing:.06em;text-transform:uppercase;background:var(--grey50);border-bottom:1px solid var(--border);white-space:nowrap}
.data-table td{padding:9px 12px;border-bottom:1px solid var(--grey100);color:var(--text);vertical-align:middle}
.data-table tr:last-child td{border-bottom:none}
.data-table tbody tr:hover{background:var(--grey50)}
.data-table tbody tr.selected{background:#dcfce7}
.mono{font-family:var(--mono);font-size:11px}
#toast{position:fixed;bottom:20px;right:20px;z-index:999;bac
