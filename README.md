# carroll-crm
Carroll Group Sales CRM 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Carroll Group - Sales CRM Pro</title>
    <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root{--red:#C00000;--red-dark:#8B0000;--red-light:#E53935;--bg:#0D0D0D;--card:#1A1A1A;--elevated:#242424;--input:#2A2A2A;--text:#FFF;--text2:#A0A0A0;--muted:#666;--border:#333;--success:#00C853;--warning:#FFB300;--info:#29B6F6;--purple:#AB47BC;--orange:#FF7043}
        *{margin:0;padding:0;box-sizing:border-box}body{font-family:'IBM Plex Sans',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;line-height:1.5}
        .header{background:linear-gradient(180deg,var(--card),var(--bg));border-bottom:1px solid var(--border);padding:1rem 2rem;position:sticky;top:0;z-index:100}
        .header-content{max-width:1900px;margin:0 auto;display:flex;align-items:center;justify-content:space-between}
        .logo-section{display:flex;align-items:center;gap:1rem}.logo{width:48px;height:48px;background:var(--red);border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:1.2rem}
        .brand h1{font-size:1.25rem;font-weight:700}.brand span{font-size:.75rem;color:var(--text2);text-transform:uppercase;letter-spacing:.1em}
        .user-info{display:flex;align-items:center;gap:.75rem;color:var(--text2);font-size:.875rem}
        .user-avatar{width:36px;height:36px;background:var(--red);border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:600;color:#fff}
        .sync-status{display:flex;align-items:center;gap:.5rem;padding:.4rem .75rem;background:var(--elevated);border-radius:20px;font-size:.75rem}
        .sync-dot{width:8px;height:8px;border-radius:50%;background:var(--muted)}.sync-dot.connected{background:var(--success)}.sync-dot.syncing{background:var(--warning);animation:pulse 1s infinite}
        @keyframes pulse{0%,100%{opacity:1}50%{opacity:.5}}
        .nav-tabs{background:var(--card);border-bottom:1px solid var(--border);padding:0 2rem}.nav-tabs ul{max-width:1900px;margin:0 auto;display:flex;list-style:none;overflow-x:auto}
        .nav-tabs a{display:block;padding:1rem 1.25rem;color:var(--text2);text-decoration:none;font-weight:500;font-size:.8rem;border-bottom:2px solid transparent;white-space:nowrap}
        .nav-tabs a:hover{color:var(--text);background:var(--elevated)}.nav-tabs a.active{color:var(--red-light);border-bottom-color:var(--red)}
        .main-content{max-width:1900px;margin:0 auto;padding:1.5rem 2rem}.tab-content{display:none}.tab-content.active{display:block;animation:fadeIn .3s}
        @keyframes fadeIn{from{opacity:0}to{opacity:1}}
        .stats-row{display:grid;grid-template-columns:repeat(6,1fr);gap:1rem;margin-bottom:1.5rem}
        .stat-card{background:var(--card);border:1px solid var(--border);border-radius:8px;padding:1rem;position:relative;overflow:hidden}
        .stat-card::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:var(--red)}
        .stat-card.success::before{background:var(--success)}.stat-card.warning::before{background:var(--warning)}.stat-card.info::before{background:var(--info)}.stat-card.purple::before{background:var(--purple)}.stat-card.orange::before{background:var(--orange)}
        .stat-label{font-size:.65rem;text-transform:uppercase;letter-spacing:.1em;color:var(--text2);margin-bottom:.25rem}
        .stat-value{font-size:1.5rem;font-weight:700;font-family:'JetBrains Mono',monospace}.stat-change{font-size:.7rem;margin-top:.25rem}.stat-change.up{color:var(--success)}.stat-change.down{color:var(--red-light)}
        .charts-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:1rem;margin-bottom:1.5rem}
        .chart-card{background:var(--card);border:1px solid var(--border);border-radius:8px;overflow:hidden}.chart-card.wide{grid-column:span 2}
        .chart-header{background:var(--elevated);padding:.75rem 1rem;border-bottom:1px solid var(--border)}.chart-title{font-size:.8rem;font-weight:600;text-transform:uppercase}
        .chart-body{padding:1rem;height:250px}
        .variables-panel{background:var(--card);border:1px solid var(--border);border-radius:8px;margin-bottom:1.5rem}
        .variables-header{background:var(--elevated);padding:.75rem 1rem;border-bottom:1px solid var(--border);display:flex;justify-content:space-between;cursor:pointer}
        .variables-body{padding:1rem;display:none}.variables-body.open{display:block}
        .variables-grid{display:grid;grid-template-columns:repeat(5,1fr);gap:1rem}
        .var-group label{display:block;font-size:.65rem;text-transform:uppercase;color:var(--text2);margin-bottom:.25rem}
        .var-group input,.var-group select{width:100%;background:var(--input);border:1px solid var(--border);border-radius:4px;padding:.4rem .6rem;color:var(--text);font-size:.8rem;font-family:'JetBrains Mono',monospace}
        .alerts-section{display:grid;grid-template-columns:repeat(3,1fr);gap:1rem;margin-bottom:1.5rem}
        .alert-card{background:var(--card);border:1px solid var(--border);border-radius:8px;padding:1rem}.alert-card.danger{border-color:var(--red)}.alert-card.warning{border-color:var(--warning)}
        .alert-title{font-size:.75rem;font-weight:600;text-transform:uppercase;margin-bottom:.5rem}.alert-list{max-height:120px;overflow-y:auto}
        .alert-item{padding:.4rem 0;border-bottom:1px solid var(--border);font-size:.8rem;display:flex;justify-content:space-between}.alert-item:last-child{border-bottom:none}
        .goals-section{background:var(--card);border:1px solid var(--border);border-radius:8px;padding:1rem;margin-bottom:1.5rem}
        .goals-grid{display:grid;grid-template-columns:repeat(5,1fr);gap:1rem}.goal-item{text-align:center}
        .goal-label{font-size:.7rem;color:var(--text2);text-transform:uppercase;margin-bottom:.5rem}
        .goal-progress{height:8px;background:var(--elevated);border-radius:4px;overflow:hidden;margin-bottom:.25rem}
        .goal-bar{height:100%;background:var(--red);border-radius:4px}.goal-bar.complete{background:var(--success)}.goal-value{font-size:.75rem;font-family:'JetBrains Mono',monospace}
        .dashboard-bottom{display:grid;grid-template-columns:1fr 1fr;gap:1rem}
        .section-card{background:var(--card);border:1px solid var(--border);border-radius:8px;overflow:hidden}
        .section-header{background:var(--elevated);padding:.75rem 1rem;border-bottom:1px solid var(--border);font-size:.8rem;font-weight:600;text-transform:uppercase}
        .section-body{padding:.75rem 1rem;max-height:250px;overflow-y:auto}
        .activity-item{display:flex;gap:.75rem;padding:.5rem 0;border-bottom:1px solid var(--border)}.activity-item:last-child{border-bottom:none}
        .activity-icon{width:28px;height:28px;background:var(--elevated);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:.75rem}
        .activity-content{flex:1}.activity-title{font-weight:500;font-size:.8rem}.activity-meta{font-size:.7rem;color:var(--muted)}
        .table-container{background:var(--card);border:1px solid var(--border);border-radius:8px;overflow:hidden}
        .table-header{background:var(--elevated);padding:.75rem 1rem;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;gap:1rem;flex-wrap:wrap}
        .table-title{font-size:1rem;font-weight:600}.table-actions{display:flex;gap:.5rem;flex-wrap:wrap}
        .search-input{background:var(--input);border:1px solid var(--border);border-radius:6px;padding:.4rem .75rem;color:var(--text);font-size:.8rem;width:180px}
        .search-input::placeholder{color:var(--muted)}.table-scroll{overflow-x:auto}table{width:100%;border-collapse:collapse}thead{background:var(--bg)}
        th{padding:.6rem .75rem;text-align:left;font-size:.65rem;font-weight:600;text-transform:uppercase;color:var(--text2);border-bottom:1px solid var(--border);white-space:nowrap}
        td{padding:.6rem .75rem;border-bottom:1px soli
