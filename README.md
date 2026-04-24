# Cas de Violence en Milieu Scolaire
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Suivi des Violences en Milieu Scolaire</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;800&family=Source+Sans+3:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --navy: #0a1628;
    --blue: #1a3a6b;
    --blue-mid: #2563a8;
    --blue-light: #3b82f6;
    --blue-pale: #dbeafe;
    --red: #c0392b;
    --red-light: #e74c3c;
    --red-pale: #fde8e8;
    --green: #1a6b3a;
    --green-light: #27ae60;
    --green-pale: #d1fae5;
    --gold: #d4a017;
    --gold-light: #f59e0b;
    --white: #ffffff;
    --gray-50: #f8fafc;
    --gray-100: #f1f5f9;
    --gray-200: #e2e8f0;
    --gray-300: #cbd5e1;
    --gray-500: #64748b;
    --gray-700: #334155;
    --gray-900: #0f172a;
    --shadow-sm: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.08);
    --shadow-md: 0 4px 16px rgba(0,0,0,0.12);
    --shadow-lg: 0 8px 32px rgba(0,0,0,0.16);
    --radius: 12px;
    --radius-sm: 8px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

  body {
    font-family: 'Source Sans 3', sans-serif;
    background: var(--gray-50);
    color: var(--gray-900);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── HEADER ── */
  header {
    background: linear-gradient(135deg, var(--navy) 0%, var(--blue) 60%, var(--blue-mid) 100%);
    color: white;
    padding: 0;
    position: sticky;
    top: 0;
    z-index: 100;
    box-shadow: var(--shadow-lg);
  }

  .header-top {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 14px 16px 10px;
    border-bottom: 1px solid rgba(255,255,255,0.1);
  }

  .header-logo {
    width: 44px; height: 44px;
    background: rgba(255,255,255,0.15);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    font-size: 22px;
    flex-shrink: 0;
  }

  .header-title h1 {
    font-family: 'Playfair Display', serif;
    font-size: 15px;
    font-weight: 700;
    line-height: 1.2;
    letter-spacing: 0.01em;
  }

  .header-title p {
    font-size: 11px;
    opacity: 0.7;
    margin-top: 2px;
  }

  .header-meta {
    padding: 8px 16px;
    display: flex;
    gap: 8px;
    align-items: center;
  }

  .header-meta input {
    background: rgba(255,255,255,0.12);
    border: 1px solid rgba(255,255,255,0.2);
    color: white;
    padding: 5px 10px;
    border-radius: 6px;
    font-size: 12px;
    font-family: inherit;
    flex: 1;
  }

  .header-meta input::placeholder { color: rgba(255,255,255,0.5); }

  /* ── BOTTOM NAV ── */
  nav {
    position: fixed;
    bottom: 0; left: 0; right: 0;
    background: white;
    display: flex;
    border-top: 2px solid var(--gray-200);
    z-index: 100;
    box-shadow: 0 -4px 20px rgba(0,0,0,0.08);
  }

  .nav-btn {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 10px 4px 8px;
    background: none;
    border: none;
    cursor: pointer;
    color: var(--gray-500);
    font-size: 10px;
    font-family: inherit;
    font-weight: 600;
    letter-spacing: 0.03em;
    transition: color 0.2s;
    gap: 4px;
    -webkit-tap-highlight-color: transparent;
  }

  .nav-btn .nav-icon { font-size: 22px; }

  .nav-btn.active {
    color: var(--blue-mid);
  }

  .nav-btn.active .nav-icon {
    transform: scale(1.1);
  }

  /* ── PAGES ── */
  .page {
    display: none;
    padding: 14px 14px 90px;
    min-height: calc(100vh - 120px);
  }

  .page.active { display: block; }

  /* ── CARDS ── */
  .card {
    background: white;
    border-radius: var(--radius);
    box-shadow: var(--shadow-sm);
    margin-bottom: 14px;
    overflow: hidden;
  }

  .card-header {
    padding: 14px 16px 10px;
    border-bottom: 1px solid var(--gray-100);
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .card-header-icon {
    width: 34px; height: 34px;
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 16px;
    flex-shrink: 0;
  }

  .card-header h2 {
    font-family: 'Playfair Display', serif;
    font-size: 15px;
    font-weight: 700;
    color: var(--navy);
    flex: 1;
  }

  .card-body { padding: 14px 16px; }

  /* ── FORM ELEMENTS ── */
  .form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    margin-bottom: 10px;
  }

  .form-group { display: flex; flex-direction: column; gap: 4px; }

  .form-group label {
    font-size: 11px;
    font-weight: 700;
    color: var(--gray-500);
    letter-spacing: 0.06em;
    text-transform: uppercase;
  }

  .form-group select,
  .form-group input,
  .form-group textarea {
    padding: 10px 12px;
    border: 1.5px solid var(--gray-200);
    border-radius: var(--radius-sm);
    font-family: inherit;
    font-size: 14px;
    color: var(--gray-900);
    background: var(--gray-50);
    transition: border-color 0.2s;
    -webkit-appearance: none;
  }

  .form-group select:focus,
  .form-group input:focus,
  .form-group textarea:focus {
    outline: none;
    border-color: var(--blue-light);
    background: white;
  }

  textarea { resize: vertical; min-height: 70px; }

  /* ── BUTTONS ── */
  .btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 6px;
    padding: 11px 18px;
    border: none;
    border-radius: var(--radius-sm);
    font-family: inherit;
    font-weight: 700;
    font-size: 13px;
    cursor: pointer;
    letter-spacing: 0.02em;
    transition: all 0.18s;
    -webkit-tap-highlight-color: transparent;
  }

  .btn-primary { background: var(--blue-mid); color: white; }
  .btn-primary:active { background: var(--blue); transform: scale(0.97); }

  .btn-danger { background: var(--red); color: white; }
  .btn-danger:active { background: #a93226; transform: scale(0.97); }

  .btn-success { background: var(--green-light); color: white; }
  .btn-success:active { background: var(--green); transform: scale(0.97); }

  .btn-gold { background: var(--gold); color: white; }
  .btn-gold:active { transform: scale(0.97); }

  .btn-outline {
    background: transparent;
    border: 2px solid var(--blue-mid);
    color: var(--blue-mid);
  }

  .btn-sm { padding: 7px 12px; font-size: 12px; }
  .btn-full { width: 100%; }

  .btn-group {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
  }

  .btn-group .btn { flex: 1; min-width: 120px; }

  /* ── DATA TABLE ── */
  .table-wrapper {
    overflow-x: auto;
    border-radius: var(--radius-sm);
    border: 1px solid var(--gray-200);
    -webkit-overflow-scrolling: touch;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 12px;
    min-width: 620px;
  }

  thead { background: var(--navy); color: white; }

  thead th {
    padding: 10px 10px;
    text-align: left;
    font-weight: 700;
    letter-spacing: 0.04em;
    font-size: 11px;
    white-space: nowrap;
  }

  tbody tr { border-bottom: 1px solid var(--gray-100); }
  tbody tr:last-child { border-bottom: none; }
  tbody tr:nth-child(even) { background: var(--gray-50); }

  tbody td {
    padding: 9px 10px;
    vertical-align: middle;
  }

  .badge {
    display: inline-block;
    padding: 3px 8px;
    border-radius: 20px;
    font-size: 11px;
    font-weight: 700;
  }

  .badge-t1 { background: var(--blue-pale); color: var(--blue); }
  .badge-t2 { background: var(--green-pale); color: var(--green); }
  .badge-t3 { background: var(--red-pale); color: var(--red); }

  /* ── STAT CARDS ── */
  .stat-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    margin-bottom: 14px;
  }

  .stat-card {
    background: white;
    border-radius: var(--radius);
    padding: 14px 12px;
    box-shadow: var(--shadow-sm);
    display: flex;
    flex-direction: column;
    gap: 4px;
    border-left: 4px solid transparent;
  }

  .stat-card.blue { border-color: var(--blue-light); }
  .stat-card.red { border-color: var(--red-light); }
  .stat-card.green { border-color: var(--green-light); }
  .stat-card.gold { border-color: var(--gold-light); }

  .stat-number {
    font-family: 'Playfair Display', serif;
    font-size: 28px;
    font-weight: 800;
    color: var(--navy);
    line-height: 1;
  }

  .stat-label {
    font-size: 11px;
    font-weight: 600;
    color: var(--gray-500);
    letter-spacing: 0.04em;
    text-transform: uppercase;
  }

  /* ── CHARTS ── */
  .chart-container {
    position: relative;
    height: 220px;
    width: 100%;
    padding: 0 4px;
  }

  .chart-container.tall { height: 260px; }

  /* ── ANALYSIS BOX ── */
  .analysis-box {
    background: linear-gradient(135deg, #eef4ff 0%, #f0fdf4 100%);
    border-radius: var(--radius);
    padding: 14px;
    border: 1px solid var(--blue-pale);
    margin-bottom: 10px;
  }

  .analysis-box h3 {
    font-family: 'Playfair Display', serif;
    font-size: 14px;
    color: var(--navy);
    margin-bottom: 8px;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .analysis-item {
    display: flex;
    gap: 8px;
    margin-bottom: 6px;
    font-size: 13px;
    line-height: 1.4;
    color: var(--gray-700);
  }

  .analysis-item .dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--blue-mid);
    flex-shrink: 0;
    margin-top: 5px;
  }

  /* ── SENSITIVITY MESSAGES ── */
  .trimestre-section {
    border: 1.5px solid var(--gray-200);
    border-radius: var(--radius-sm);
    margin-bottom: 10px;
    overflow: hidden;
  }

  .trimestre-header {
    background: var(--gray-100);
    padding: 10px 14px;
    font-weight: 700;
    font-size: 13px;
    color: var(--navy);
    border-bottom: 1px solid var(--gray-200);
  }

  .trimestre-body { padding: 12px 14px; }

  /* ── RAPPORT SECTION ── */
  .rapport-section {
    background: white;
    border: 1px solid var(--gray-200);
    border-radius: var(--radius);
    padding: 16px;
    margin-bottom: 14px;
  }

  .rapport-section h3 {
    font-family: 'Playfair Display', serif;
    font-size: 15px;
    color: var(--navy);
    margin-bottom: 10px;
    padding-bottom: 8px;
    border-bottom: 2px solid var(--blue-pale);
  }

  .rapport-section p, .rapport-section li {
    font-size: 13px;
    color: var(--gray-700);
    line-height: 1.6;
  }

  .rapport-section ul { padding-left: 18px; margin-top: 6px; }
  .rapport-section li { margin-bottom: 4px; }

  /* ── TOAST ── */
  #toast {
    position: fixed;
    bottom: 80px;
    left: 50%;
    transform: translateX(-50%) translateY(20px);
    background: var(--navy);
    color: white;
    padding: 10px 20px;
    border-radius: 30px;
    font-size: 13px;
    font-weight: 600;
    opacity: 0;
    transition: all 0.3s;
    z-index: 999;
    white-space: nowrap;
    pointer-events: none;
  }

  #toast.show {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }

  /* ── EMPTY STATE ── */
  .empty-state {
    text-align: center;
    padding: 40px 20px;
    color: var(--gray-500);
  }

  .empty-state .empty-icon { font-size: 48px; margin-bottom: 12px; }
  .empty-state p { font-size: 14px; }

  /* ── LOADING ── */
  #pdfLoading {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(10,22,40,0.85);
    z-index: 999;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    gap: 16px;
    color: white;
    font-size: 15px;
    font-weight: 600;
  }

  #pdfLoading.show { display: flex; }

  .spinner {
    width: 44px; height: 44px;
    border: 4px solid rgba(255,255,255,0.2);
    border-top-color: white;
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
  }

  @keyframes spin { to { transform: rotate(360deg); } }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 4px; height: 4px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--gray-300); border-radius: 4px; }

  /* ── PRINT / PDF ── */
  #pdfContent {
    display: none;
    font-family: 'Source Sans 3', Arial, sans-serif;
    font-size: 12px;
    color: #111;
  }

  /* Niveau tags */
  .niveau-tag {
    display: inline-block;
    background: var(--navy);
    color: white;
    padding: 2px 7px;
    border-radius: 4px;
    font-size: 11px;
    font-weight: 700;
  }

  /* Action buttons in table */
  .table-actions { display: flex; gap: 4px; }
  .btn-icon {
    width: 28px; height: 28px;
    border-radius: 6px;
    border: none;
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    font-size: 14px;
    transition: transform 0.15s;
  }
  .btn-icon:active { transform: scale(0.9); }
  .btn-icon-edit { background: var(--blue-pale); }
  .btn-icon-delete { background: var(--red-pale); }

  /* Divider */
  .divider {
    height: 1px;
    background: var(--gray-200);
    margin: 12px 0;
  }

  /* Progress bar */
  .progress-bar {
    height: 6px;
    background: var(--gray-200);
    border-radius: 10px;
    overflow: hidden;
    margin-top: 4px;
  }
  .progress-fill {
    height: 100%;
    border-radius: 10px;
    transition: width 0.6s ease;
  }

  /* Commentaire inputs */
  .comment-grid { display: grid; gap: 8px; }
  .comment-item { display: flex; flex-direction: column; gap: 4px; }
  .comment-item label { font-size: 12px; font-weight: 700; color: var(--gray-500); }
  .comment-item textarea {
    padding: 8px 10px;
    border: 1.5px solid var(--gray-200);
    border-radius: var(--radius-sm);
    font-family: inherit;
    font-size: 13px;
    resize: vertical;
    min-height: 60px;
  }
  .comment-item textarea:focus { outline: none; border-color: var(--blue-light); }
</style>
</head>
<body>

<header>
  <div class="header-top">
    <div class="header-logo">🏫</div>
    <div class="header-title">
      <h1>Suivi des Violences Scolaires</h1>
      <p>Rapport – Proviseur de Lycée</p>
    </div>
  </div>
  <div class="header-meta">
    <input type="text" id="schoolName" placeholder="Nom du lycée…" style="flex:2">
    <input type="text" id="schoolYear" placeholder="Année scolaire" value="2024–2025" style="flex:1">
  </div>
</header>

<!-- ══════════════ PAGE : SAISIE ══════════════ -->
<div id="page-saisie" class="page active">

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#dbeafe">📝</div>
      <h2>Ajouter un incident</h2>
    </div>
    <div class="card-body">
      <div class="form-row">
        <div class="form-group">
          <label>Trimestre</label>
          <select id="f-trimestre">
            <option value="T1">1er Trimestre</option>
            <option value="T2">2e Trimestre</option>
            <option value="T3">3e Trimestre</option>
          </select>
        </div>
        <div class="form-group">
          <label>Niveau</label>
          <select id="f-niveau">
            <option>6e</option><option>5e</option><option>4e</option>
            <option>3e</option><option>2nde</option><option>1ère</option><option>Tle</option>
          </select>
        </div>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>Type de violence</label>
          <select id="f-type">
            <option>Violence physique</option>
            <option>Violence verbale</option>
            <option>Violence psychologique</option>
            <option>Menace / intimidation</option>
            <option>Bagarre</option>
          </select>
        </div>
        <div class="form-group">
          <label>Lieu</label>
          <select id="f-lieu">
            <option>Classe</option>
            <option>Cour</option>
            <option>Sortie école</option>
          </select>
        </div>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>Acteurs</label>
          <select id="f-acteurs">
            <option>Élève–Élève</option>
            <option>Élève–Professeur</option>
          </select>
        </div>
        <div class="form-group">
          <label>Nombre d'incidents</label>
          <input type="number" id="f-nb" min="1" value="1" placeholder="ex: 3">
        </div>
      </div>
      <input type="hidden" id="editId" value="">
      <div class="btn-group">
        <button class="btn btn-primary" onclick="addIncident()">➕ Ajouter</button>
        <button class="btn btn-outline btn-sm" onclick="cancelEdit()">✕ Annuler</button>
      </div>
    </div>
  </div>

  <!-- Informations complémentaires par trimestre -->
  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#d1fae5">💬</div>
      <h2>Informations par trimestre</h2>
    </div>
    <div class="card-body" style="padding-top:10px">
      <div class="trimestre-section">
        <div class="trimestre-header">🔵 1er Trimestre</div>
        <div class="trimestre-body">
          <div class="form-group" style="margin-bottom:8px">
            <label>Message de sensibilisation</label>
            <textarea id="msg-T1" placeholder="Campagne de sensibilisation menée…"></textarea>
          </div>
          <div class="form-group">
            <label>Mesures prises</label>
            <textarea id="mesures-T1" placeholder="Sanctions, convocations, médiations…"></textarea>
          </div>
        </div>
      </div>
      <div class="trimestre-section">
        <div class="trimestre-header">🟢 2e Trimestre</div>
        <div class="trimestre-body">
          <div class="form-group" style="margin-bottom:8px">
            <label>Message de sensibilisation</label>
            <textarea id="msg-T2" placeholder="Campagne de sensibilisation menée…"></textarea>
          </div>
          <div class="form-group">
            <label>Mesures prises</label>
            <textarea id="mesures-T2" placeholder="Sanctions, convocations, médiations…"></textarea>
          </div>
        </div>
      </div>
      <div class="trimestre-section">
        <div class="trimestre-header">🔴 3e Trimestre</div>
        <div class="trimestre-body">
          <div class="form-group" style="margin-bottom:8px">
            <label>Message de sensibilisation</label>
            <textarea id="msg-T3" placeholder="Campagne de sensibilisation menée…"></textarea>
          </div>
          <div class="form-group">
            <label>Mesures prises</label>
            <textarea id="mesures-T3" placeholder="Sanctions, convocations, médiations…"></textarea>
          </div>
        </div>
      </div>
      <button class="btn btn-success btn-full" onclick="saveMeta()">💾 Enregistrer</button>
    </div>
  </div>

  <!-- Tableau des incidents -->
  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#fde8e8">📋</div>
      <h2>Incidents enregistrés</h2>
      <div style="margin-left:auto;display:flex;gap:6px">
        <button class="btn btn-outline btn-sm" onclick="exportCSV()">📤 CSV</button>
        <label class="btn btn-outline btn-sm" style="cursor:pointer">
          📥 Import
          <input type="file" accept=".csv" style="display:none" onchange="importCSV(event)">
        </label>
      </div>
    </div>
    <div class="card-body" style="padding:0">
      <div id="tableContainer" class="table-wrapper">
        <div class="empty-state">
          <div class="empty-icon">📭</div>
          <p>Aucun incident enregistré.<br>Ajoutez votre premier incident ci-dessus.</p>
        </div>
      </div>
    </div>
  </div>

</div>

<!-- ══════════════ PAGE : STATISTIQUES ══════════════ -->
<div id="page-stats" class="page">

  <div class="stat-grid" id="statCards"></div>

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#dbeafe">📊</div>
      <h2>Incidents par trimestre</h2>
    </div>
    <div class="card-body">
      <div class="chart-container"><canvas id="chartTrimestre"></canvas></div>
    </div>
  </div>

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#fde8e8">🔴</div>
      <h2>Types de violence par trimestre</h2>
    </div>
    <div class="card-body">
      <div class="chart-container tall"><canvas id="chartTypes"></canvas></div>
    </div>
  </div>

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#d1fae5">🥧</div>
      <h2>Répartition des violences</h2>
    </div>
    <div class="card-body">
      <div class="chart-container"><canvas id="chartPie"></canvas></div>
    </div>
  </div>

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#fef9c3">📍</div>
      <h2>Lieux et acteurs</h2>
    </div>
    <div class="card-body">
      <div class="chart-container tall"><canvas id="chartLieux"></canvas></div>
    </div>
  </div>

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#f3e8ff">🎓</div>
      <h2>Violences par niveau</h2>
    </div>
    <div class="card-body">
      <div class="chart-container"><canvas id="chartNiveaux"></canvas></div>
    </div>
  </div>

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#ffedd5">📈</div>
      <h2>Comparaison niveaux / trimestres</h2>
    </div>
    <div class="card-body">
      <div class="chart-container tall"><canvas id="chartComparaison"></canvas></div>
    </div>
  </div>

  <!-- Tableau statistique -->
  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#dbeafe">🔢</div>
      <h2>Tableau statistique</h2>
    </div>
    <div class="card-body" style="padding:0">
      <div id="statTable" class="table-wrapper"></div>
    </div>
  </div>

  <!-- Classement -->
  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#fde8e8">🏆</div>
      <h2>Classement des niveaux</h2>
    </div>
    <div class="card-body">
      <div id="rankingList"></div>
    </div>
  </div>

  <!-- Analyse automatique -->
  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#d1fae5">🤖</div>
      <h2>Analyse automatique</h2>
    </div>
    <div class="card-body">
      <div id="autoAnalysis"></div>
    </div>
  </div>

</div>

<!-- ══════════════ PAGE : RAPPORT ══════════════ -->
<div id="page-rapport" class="page">

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#fef9c3">✍️</div>
      <h2>Commentaires</h2>
    </div>
    <div class="card-body">
      <div class="form-group" style="margin-bottom:10px">
        <label>Commentaire global</label>
        <textarea id="com-global" placeholder="Analyse globale de la situation de violence…" style="min-height:80px"></textarea>
      </div>
      <div class="divider"></div>
      <p style="font-size:12px;font-weight:700;color:var(--gray-500);letter-spacing:.05em;text-transform:uppercase;margin-bottom:8px">Par niveau</p>
      <div class="comment-grid">
        <!-- Champs générés dynamiquement selon NIVEAUX dans loadComments() -->
      </div>
      <div class="divider"></div>
      <div class="form-group">
        <label>Conclusion générale</label>
        <textarea id="com-conclusion" placeholder="Conclusion et perspectives pour l'année suivante…" style="min-height:90px"></textarea>
      </div>
      <button class="btn btn-success btn-full" onclick="saveComments()">💾 Enregistrer</button>
    </div>
  </div>

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#fde8e8">📄</div>
      <h2>Aperçu du rapport</h2>
    </div>
    <div class="card-body" id="rapportPreview">
      <p style="color:var(--gray-500);font-size:13px">L'aperçu s'affiche ici après génération.</p>
    </div>
  </div>

  <div class="btn-group">
    <button class="btn btn-gold btn-full" onclick="generatePDF()" style="font-size:15px;padding:14px">
      🖨️ Générer rapport PDF
    </button>
  </div>
  <div style="height:8px"></div>
  <div class="btn-group">
    <button class="btn btn-primary" onclick="previewRapport()">👁️ Aperçu</button>
    <button class="btn btn-outline" onclick="exportCSV()">📤 Export CSV</button>
  </div>

</div>

<!-- Loading overlay -->
<div id="pdfLoading">
  <div class="spinner"></div>
  <p>Génération du PDF en cours…</p>
</div>

<!-- Toast -->
<div id="toast"></div>

<!-- ══════════ PAGE PARAMÈTRES ══════════ -->
<div id="page-params" class="page">

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#dbeafe">🏫</div>
      <h2>Identité de l'établissement</h2>
    </div>
    <div class="card-body">
      <div class="form-group" style="margin-bottom:10px">
        <label>Nom du lycée</label>
        <input type="text" id="p-schoolName" placeholder="Ex : Lycée Classique d'Abidjan">
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>Année scolaire</label>
          <input type="text" id="p-schoolYear" placeholder="2024–2025">
        </div>
        <div class="form-group">
          <label>Nom du proviseur</label>
          <input type="text" id="p-proviseur" placeholder="M. / Mme …">
        </div>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>Ville / Commune</label>
          <input type="text" id="p-ville" placeholder="Ex : Abidjan">
        </div>
        <div class="form-group">
          <label>Région / District</label>
          <input type="text" id="p-region" placeholder="Ex : Lagunes">
        </div>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>Téléphone</label>
          <input type="text" id="p-tel" placeholder="+225 …">
        </div>
        <div class="form-group">
          <label>Email</label>
          <input type="text" id="p-email" placeholder="lycee@edu.ci">
        </div>
      </div>
      <div class="form-group">
        <label>Devise / Slogan</label>
        <input type="text" id="p-devise" placeholder="Ex : Excellence et Discipline">
      </div>
    </div>
  </div>

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#d1fae5">📋</div>
      <h2>Personnaliser les listes de saisie</h2>
    </div>
    <div class="card-body">
      <p style="font-size:11px;color:var(--gray-500);margin-bottom:12px">Séparez les valeurs par une virgule. Les listes de saisie seront mises à jour automatiquement.</p>
      <div class="form-group" style="margin-bottom:10px">
        <label>Niveaux scolaires</label>
        <input type="text" id="p-niveaux" oninput="previewList('niveaux')">
        <div id="preview-niveaux" style="margin-top:5px;display:flex;flex-wrap:wrap;gap:4px"></div>
      </div>
      <div class="form-group" style="margin-bottom:10px">
        <label>Types de violence</label>
        <input type="text" id="p-types" oninput="previewList('types')">
        <div id="preview-types" style="margin-top:5px;display:flex;flex-wrap:wrap;gap:4px"></div>
      </div>
      <div class="form-group" style="margin-bottom:10px">
        <label>Lieux</label>
        <input type="text" id="p-lieux" oninput="previewList('lieux')">
        <div id="preview-lieux" style="margin-top:5px;display:flex;flex-wrap:wrap;gap:4px"></div>
      </div>
      <div class="form-group" style="margin-bottom:10px">
        <label>Acteurs</label>
        <input type="text" id="p-acteurs" oninput="previewList('acteurs')">
        <div id="preview-acteurs" style="margin-top:5px;display:flex;flex-wrap:wrap;gap:4px"></div>
      </div>
    </div>
  </div>

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#fef9c3">✏️</div>
      <h2>Rubriques libres (rapport PDF)</h2>
    </div>
    <div class="card-body">
      <p style="font-size:11px;color:var(--gray-500);margin-bottom:10px">Ajoutez des rubriques personnalisées qui apparaîtront dans le rapport PDF.</p>
      <div id="champsLibres"></div>
      <button class="btn btn-outline btn-sm" onclick="addChampLibre()" style="margin-top:8px">➕ Ajouter une rubrique</button>
    </div>
  </div>

  <div class="card">
    <div class="card-header">
      <div class="card-header-icon" style="background:#fde8e8">📄</div>
      <h2>Paramètres du rapport PDF</h2>
    </div>
    <div class="card-body">
      <div class="form-group" style="margin-bottom:10px">
        <label>Titre du rapport</label>
        <input type="text" id="p-titreRapport" placeholder="Rapport Annuel de Suivi des Violences Scolaires">
      </div>
      <div class="form-group" style="margin-bottom:10px">
        <label>Sous-titre / Objet</label>
        <input type="text" id="p-soustitre" placeholder="À l'attention de la Direction Régionale de l'Éducation">
      </div>
      <div class="form-group" style="margin-bottom:10px">
        <label>Destinataire (ministère…)</label>
        <input type="text" id="p-destinataire" placeholder="Ex : Ministère de l'Éducation Nationale, Côte d'Ivoire">
      </div>
      <div class="form-group" style="margin-bottom:10px">
        <label>Mention légale / Confidentialité</label>
        <input type="text" id="p-mention" placeholder="Ex : Document confidentiel – Usage interne">
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>Couleur principale PDF</label>
          <select id="p-couleur">
            <option value="navy">Bleu marine (défaut)</option>
            <option value="green">Vert</option>
            <option value="red">Rouge</option>
            <option value="purple">Violet</option>
            <option value="orange">Orange</option>
          </select>
        </div>
        <div class="form-group">
          <label>Inclure graphiques</label>
          <select id="p-inclureGraphiques">
            <option value="1">Oui (recommandé)</option>
            <option value="0">Non</option>
          </select>
        </div>
      </div>
    </div>
  </div>

  <button class="btn btn-primary btn-full" onclick="saveParams()">💾 Enregistrer tous les paramètres</button>
  <div style="height:8px"></div>
  <button class="btn btn-danger btn-sm btn-full" style="opacity:.7" onclick="resetApp()">🗑️ Réinitialiser toutes les données</button>
  <div style="height:12px"></div>

</div>

<!-- Nav -->
<nav>
  <button class="nav-btn active" id="nav-saisie" onclick="showPage('saisie')">
    <span class="nav-icon">📝</span>
    <span>Saisie</span>
  </button>
  <button class="nav-btn" id="nav-stats" onclick="showPage('stats')">
    <span class="nav-icon">📊</span>
    <span>Stats</span>
  </button>
  <button class="nav-btn" id="nav-rapport" onclick="showPage('rapport')">
    <span class="nav-icon">📄</span>
    <span>Rapport</span>
  </button>
  <button class="nav-btn" id="nav-params" onclick="showPage('params')">
    <span class="nav-icon">⚙️</span>
    <span>Réglages</span>
  </button>
</nav>

<!-- Hidden PDF canvas area -->
<div id="pdfContent"></div>

<script>
// ══════════════════════════════════════════════
//  DATA STORE
// ══════════════════════════════════════════════
let NIVEAUX = ['6e','5e','4e','3e','2nde','1ère','Tle'];
let TYPES   = ['Violence physique','Violence verbale','Violence psychologique','Menace / intimidation','Bagarre'];
let LIEUX   = ['Classe','Cour','Sortie école'];
let ACTEURS = ['Élève–Élève','Élève–Professeur'];
const TRIM  = ['T1','T2','T3'];

let params = {
  schoolName:'', schoolYear:'2024–2025', proviseur:'', ville:'', region:'',
  tel:'', email:'', devise:'',
  niveaux: NIVEAUX.join(', '), types: TYPES.join(', '),
  lieux: LIEUX.join(', '), acteurs: ACTEURS.join(', '),
  titreRapport:'Rapport Annuel de Suivi des Violences Scolaires',
  soustitre:'', destinataire:'', mention:'',
  couleur:'navy', inclureGraphiques:'1',
  champsLibres: []
};

let incidents = [];
let meta      = { T1:{msg:'',mesures:''}, T2:{msg:'',mesures:''}, T3:{msg:'',mesures:''} };
let comments  = { global:'', niveaux:{}, conclusion:'' };
let charts    = {};
let editId    = null;

// ══════════════════════════════════════════════
//  PERSISTENCE
// ══════════════════════════════════════════════
function save() {
  localStorage.setItem('svsData', JSON.stringify({
    incidents, meta, comments, params
  }));
}

function load() {
  const d = localStorage.getItem('svsData');
  if (d) {
    const p = JSON.parse(d);
    incidents = p.incidents || [];
    meta      = p.meta      || meta;
    comments  = p.comments  || comments;
    if (p.params) params = Object.assign(params, p.params);
  }
  // Apply params to UI
  applyParams();
  // Sync header fields
  document.getElementById('schoolName').value = params.schoolName || '';
  document.getElementById('schoolYear').value = params.schoolYear || '2024–2025';
  // Load meta fields
  ['T1','T2','T3'].forEach(t => {
    if (meta[t]) {
      document.getElementById('msg-'+t).value     = meta[t].msg     || '';
      document.getElementById('mesures-'+t).value = meta[t].mesures || '';
    }
  });
  // Load comments
  loadComments();
}

function applyParams() {
  // Sync lists from params
  if (params.niveaux) NIVEAUX = params.niveaux.split(',').map(s=>s.trim()).filter(Boolean);
  if (params.types)   TYPES   = params.types.split(',').map(s=>s.trim()).filter(Boolean);
  if (params.lieux)   LIEUX   = params.lieux.split(',').map(s=>s.trim()).filter(Boolean);
  if (params.acteurs) ACTEURS = params.acteurs.split(',').map(s=>s.trim()).filter(Boolean);
  // Sync header
  document.getElementById('schoolName').value = params.schoolName || '';
  document.getElementById('schoolYear').value = params.schoolYear || '2024–2025';
  // Rebuild form selects
  rebuildSelects();
}

function rebuildSelects() {
  const sel = (id, arr) => {
    const el = document.getElementById(id);
    if (!el) return;
    const cur = el.value;
    el.innerHTML = arr.map(v=>`<option>${v}</option>`).join('');
    if (arr.includes(cur)) el.value = cur;
  };
  sel('f-niveau',  NIVEAUX);
  sel('f-type',    TYPES);
  sel('f-lieu',    LIEUX);
  sel('f-acteurs', ACTEURS);
}

// ══════════════════════════════════════════════
//  NAVIGATION
// ══════════════════════════════════════════════
function showPage(p) {
  document.querySelectorAll('.page').forEach(el => el.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(el => el.classList.remove('active'));
  document.getElementById('page-'+p).classList.add('active');
  document.getElementById('nav-'+p).classList.add('active');
  if (p === 'stats')  { updateStats(); }
  if (p === 'rapport'){ loadComments(); previewRapport(); }
  if (p === 'params') { loadParamsForm(); }
}

// ══════════════════════════════════════════════
//  INCIDENTS CRUD
// ══════════════════════════════════════════════
function addIncident() {
  const nb = parseInt(document.getElementById('f-nb').value);
  if (!nb || nb < 1) { toast('⚠️ Nombre invalide'); return; }

  const inc = {
    id:        editId || Date.now().toString(),
    trimestre: document.getElementById('f-trimestre').value,
    niveau:    document.getElementById('f-niveau').value,
    type:      document.getElementById('f-type').value,
    lieu:      document.getElementById('f-lieu').value,
    acteurs:   document.getElementById('f-acteurs').value,
    nb
  };

  if (editId) {
    const idx = incidents.findIndex(i => i.id === editId);
    if (idx > -1) incidents[idx] = inc;
    editId = null;
    document.getElementById('editId').value = '';
  } else {
    incidents.push(inc);
  }

  document.getElementById('f-nb').value = 1;
  save();
  renderTable();
  toast('✅ Incident enregistré');
}

function editIncident(id) {
  const inc = incidents.find(i => i.id === id);
  if (!inc) return;
  editId = id;
  document.getElementById('f-trimestre').value = inc.trimestre;
  document.getElementById('f-niveau').value    = inc.niveau;
  document.getElementById('f-type').value      = inc.type;
  document.getElementById('f-lieu').value      = inc.lieu;
  document.getElementById('f-acteurs').value   = inc.acteurs;
  document.getElementById('f-nb').value        = inc.nb;
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function deleteIncident(id) {
  incidents = incidents.filter(i => i.id !== id);
  save();
  renderTable();
  toast('🗑️ Supprimé');
}

function cancelEdit() {
  editId = null;
  document.getElementById('f-nb').value = 1;
}

// ══════════════════════════════════════════════
//  RENDER TABLE
// ══════════════════════════════════════════════
function renderTable() {
  const c = document.getElementById('tableContainer');
  if (!incidents.length) {
    c.innerHTML = `<div class="empty-state"><div class="empty-icon">📭</div><p>Aucun incident enregistré.<br>Ajoutez votre premier incident ci-dessus.</p></div>`;
    return;
  }
  const trimColor = { T1:'badge-t1', T2:'badge-t2', T3:'badge-t3' };
  const trimLabel = { T1:'T1', T2:'T2', T3:'T3' };
  c.innerHTML = `
    <table>
      <thead>
        <tr>
          <th>Trim.</th><th>Niveau</th><th>Type</th><th>Lieu</th><th>Acteurs</th><th>Nb</th><th>Actions</th>
        </tr>
      </thead>
      <tbody>
        ${incidents.map(i => `
          <tr>
            <td><span class="badge ${trimColor[i.trimestre]||''}">${i.trimestre}</span></td>
            <td><span class="niveau-tag">${i.niveau}</span></td>
            <td style="font-size:11px">${i.type}</td>
            <td style="font-size:11px">${i.lieu}</td>
            <td style="font-size:11px">${i.acteurs}</td>
            <td><strong>${i.nb}</strong></td>
            <td>
              <div class="table-actions">
                <button class="btn-icon btn-icon-edit" onclick="editIncident('${i.id}')">✏️</button>
                <button class="btn-icon btn-icon-delete" onclick="deleteIncident('${i.id}')">🗑️</button>
              </div>
            </td>
          </tr>
        `).join('')}
      </tbody>
    </table>`;
}

// ══════════════════════════════════════════════
//  META SAVE
// ══════════════════════════════════════════════
function saveMeta() {
  ['T1','T2','T3'].forEach(t => {
    meta[t].msg     = document.getElementById('msg-'+t).value;
    meta[t].mesures = document.getElementById('mesures-'+t).value;
  });
  save();
  toast('✅ Informations enregistrées');
}

// ══════════════════════════════════════════════
//  STATISTICS
// ══════════════════════════════════════════════
function getTotalByTrim(t) {
  return incidents.filter(i => i.trimestre === t).reduce((s,i) => s+i.nb, 0);
}

function getTotalByNiveau(n) {
  return incidents.filter(i => i.niveau === n).reduce((s,i) => s+i.nb, 0);
}

function getTotalByType(tp) {
  return incidents.filter(i => i.type === tp).reduce((s,i) => s+i.nb, 0);
}

function getTotalByLieu(l) {
  return incidents.filter(i => i.lieu === l).reduce((s,i) => s+i.nb, 0);
}

function getTotalByActeurs(a) {
  return incidents.filter(i => i.acteurs === a).reduce((s,i) => s+i.nb, 0);
}

function grandTotal() {
  return incidents.reduce((s,i) => s+i.nb, 0);
}

function updateStats() {
  if (!incidents.length) {
    document.getElementById('statCards').innerHTML = `<div class="empty-state" style="grid-column:1/-1"><div class="empty-icon">📊</div><p>Ajoutez des incidents pour voir les statistiques.</p></div>`;
    return;
  }
  const gt = grandTotal();
  const t1 = getTotalByTrim('T1');
  const t2 = getTotalByTrim('T2');
  const t3 = getTotalByTrim('T3');

  // Stat cards
  document.getElementById('statCards').innerHTML = `
    <div class="stat-card blue">
      <div class="stat-number">${gt}</div>
      <div class="stat-label">Total incidents</div>
    </div>
    <div class="stat-card red">
      <div class="stat-number">${t1}</div>
      <div class="stat-label">1er Trimestre</div>
    </div>
    <div class="stat-card green">
      <div class="stat-number">${t2}</div>
      <div class="stat-label">2e Trimestre</div>
    </div>
    <div class="stat-card gold">
      <div class="stat-number">${t3}</div>
      <div class="stat-label">3e Trimestre</div>
    </div>`;

  renderCharts(t1,t2,t3,gt);
  renderStatTable(t1,t2,t3,gt);
  renderRanking(gt);
  renderAutoAnalysis(t1,t2,t3,gt);
}

// ══════════════════════════════════════════════
//  CHARTS
// ══════════════════════════════════════════════
const COLORS = {
  blue:   '#2563a8', red: '#c0392b', green: '#27ae60',
  gold:   '#d4a017', purple: '#7c3aed', orange: '#ea580c',
  teal:   '#0d9488', pink: '#db2777'
};
const PAL = Object.values(COLORS);

function destroyChart(id) { if (charts[id]) { charts[id].destroy(); delete charts[id]; } }

function renderCharts(t1,t2,t3,gt) {
  // Chart 1 – Barres trimestres
  destroyChart('chartTrimestre');
  charts['chartTrimestre'] = new Chart(document.getElementById('chartTrimestre'), {
    type: 'bar',
    data: {
      labels: ['1er Trimestre','2e Trimestre','3e Trimestre'],
      datasets: [{
        label: 'Incidents',
        data: [t1, t2, t3],
        backgroundColor: [COLORS.blue, COLORS.green, COLORS.red],
        borderRadius: 6
      }]
    },
    options: chartOpts('Incidents')
  });

  // Chart 2 – Types par trimestre (groupé)
  destroyChart('chartTypes');
  charts['chartTypes'] = new Chart(document.getElementById('chartTypes'), {
    type: 'bar',
    data: {
      labels: ['T1','T2','T3'],
      datasets: TYPES.map((tp, idx) => ({
        label: tp,
        data: TRIM.map(t => incidents.filter(i => i.trimestre===t && i.type===tp).reduce((s,i)=>s+i.nb,0)),
        backgroundColor: PAL[idx],
        borderRadius: 4
      }))
    },
    options: { ...chartOpts('Incidents'), plugins: { legend: { display: true, position: 'bottom', labels: { font: { size: 10 }, boxWidth: 12 } } } }
  });

  // Chart 3 – Camembert types
  destroyChart('chartPie');
  const typeData = TYPES.map(tp => getTotalByType(tp));
  charts['chartPie'] = new Chart(document.getElementById('chartPie'), {
    type: 'doughnut',
    data: {
      labels: TYPES,
      datasets: [{ data: typeData, backgroundColor: PAL, borderWidth: 2, borderColor: '#fff' }]
    },
    options: {
      responsive: true, maintainAspectRatio: false,
      plugins: { legend: { position: 'bottom', labels: { font: { size: 10 }, boxWidth: 12 } } }
    }
  });

  // Chart 4 – Lieux + Acteurs (empilé)
  destroyChart('chartLieux');
  charts['chartLieux'] = new Chart(document.getElementById('chartLieux'), {
    type: 'bar',
    data: {
      labels: [...LIEUX, ...ACTEURS],
      datasets: [{
        label: 'Incidents',
        data: [...LIEUX.map(l => getTotalByLieu(l)), ...ACTEURS.map(a => getTotalByActeurs(a))],
        backgroundColor: [...LIEUX.map((_,i) => PAL[i]), ...ACTEURS.map((_,i) => PAL[i+4])],
        borderRadius: 6
      }]
    },
    options: chartOpts('Incidents')
  });

  // Chart 5 – Par niveau
  destroyChart('chartNiveaux');
  charts['chartNiveaux'] = new Chart(document.getElementById('chartNiveaux'), {
    type: 'bar',
    data: {
      labels: NIVEAUX,
      datasets: [{
        label: 'Total incidents',
        data: NIVEAUX.map(n => getTotalByNiveau(n)),
        backgroundColor: NIVEAUX.map((_,i) => PAL[i % PAL.length]),
        borderRadius: 6
      }]
    },
    options: chartOpts('Incidents')
  });

  // Chart 6 – Niveaux par trimestre
  destroyChart('chartComparaison');
  charts['chartComparaison'] = new Chart(document.getElementById('chartComparaison'), {
    type: 'bar',
    data: {
      labels: NIVEAUX,
      datasets: TRIM.map((t,i) => ({
        label: t === 'T1' ? '1er Trimestre' : t === 'T2' ? '2e Trimestre' : '3e Trimestre',
        data: NIVEAUX.map(n => incidents.filter(inc => inc.trimestre===t && inc.niveau===n).reduce((s,i)=>s+i.nb,0)),
        backgroundColor: [COLORS.blue, COLORS.green, COLORS.red][i],
        borderRadius: 4
      }))
    },
    options: { ...chartOpts('Incidents'), plugins: { legend: { display: true, position: 'bottom', labels: { font: { size: 10 }, boxWidth: 12 } } } }
  });
}

function chartOpts(yLabel) {
  return {
    responsive: true, maintainAspectRatio: false,
    plugins: { legend: { display: false } },
    scales: {
      y: { beginAtZero: true, ticks: { precision: 0, font: { size: 10 } }, grid: { color: '#f1f5f9' } },
      x: { ticks: { font: { size: 10 } }, grid: { display: false } }
    }
  };
}

// ══════════════════════════════════════════════
//  STAT TABLE
// ══════════════════════════════════════════════
function renderStatTable(t1,t2,t3,gt) {
  const el = document.getElementById('statTable');
  if (!gt) { el.innerHTML = ''; return; }
  el.innerHTML = `
    <table>
      <thead>
        <tr>
          <th>Niveau</th>
          <th>T1</th><th>T2</th><th>T3</th>
          <th>Total</th><th>%</th>
        </tr>
      </thead>
      <tbody>
        ${NIVEAUX.map(n => {
          const nt1 = incidents.filter(i=>i.trimestre==='T1'&&i.niveau===n).reduce((s,i)=>s+i.nb,0);
          const nt2 = incidents.filter(i=>i.trimestre==='T2'&&i.niveau===n).reduce((s,i)=>s+i.nb,0);
          const nt3 = incidents.filter(i=>i.trimestre==='T3'&&i.niveau===n).reduce((s,i)=>s+i.nb,0);
          const tot = nt1+nt2+nt3;
          const pct = gt ? ((tot/gt)*100).toFixed(1) : 0;
          return `<tr>
            <td><span class="niveau-tag">${n}</span></td>
            <td>${nt1}</td><td>${nt2}</td><td>${nt3}</td>
            <td><strong>${tot}</strong></td>
            <td><span style="color:var(--blue-mid);font-weight:700">${pct}%</span></td>
          </tr>`;
        }).join('')}
        <tr style="background:var(--navy);color:white;font-weight:700">
          <td>TOTAL</td>
          <td>${t1}</td><td>${t2}</td><td>${t3}</td>
          <td>${gt}</td><td>100%</td>
        </tr>
      </tbody>
    </table>`;
}

// ══════════════════════════════════════════════
//  RANKING
// ══════════════════════════════════════════════
function renderRanking(gt) {
  const ranked = NIVEAUX.map(n => ({ n, tot: getTotalByNiveau(n) })).sort((a,b) => b.tot-a.tot);
  const el = document.getElementById('rankingList');
  el.innerHTML = ranked.map((r,i) => {
    const pct = gt ? ((r.tot/gt)*100).toFixed(1) : 0;
    const colors = ['#c0392b','#e67e22','#f39c12','#27ae60','#2563a8','#7c3aed','#0d9488'];
    return `
      <div style="margin-bottom:10px">
        <div style="display:flex;align-items:center;gap:8px;margin-bottom:3px">
          <span style="font-weight:800;color:${colors[i]};font-size:16px;width:20px">${i+1}</span>
          <span class="niveau-tag">${r.n}</span>
          <span style="font-size:13px;color:var(--gray-700);flex:1">${r.tot} incident${r.tot>1?'s':''}</span>
          <span style="font-size:12px;font-weight:700;color:var(--gray-500)">${pct}%</span>
        </div>
        <div class="progress-bar" style="margin-left:28px">
          <div class="progress-fill" style="width:${pct}%;background:${colors[i]}"></div>
        </div>
      </div>`;
  }).join('');
}

// ══════════════════════════════════════════════
//  AUTO ANALYSIS
// ══════════════════════════════════════════════
function renderAutoAnalysis(t1,t2,t3,gt) {
  const el = document.getElementById('autoAnalysis');
  if (!gt) { el.innerHTML = '<p style="color:var(--gray-500);font-size:13px">Données insuffisantes pour l\'analyse.</p>'; return; }

  const insights = [];

  // Tendance trimestrielle
  if (t2 < t1 && t1 > 0) insights.push(`Baisse observée au 2e trimestre (${t1} → ${t2} incidents, −${t1-t2}).`);
  if (t2 > t1 && t1 > 0) insights.push(`Hausse au 2e trimestre (${t1} → ${t2} incidents, +${t2-t1}).`);
  if (t3 > t2 && t2 > 0) insights.push(`Hausse au 3e trimestre (${t2} → ${t3} incidents, +${t3-t2}).`);
  if (t3 < t2 && t2 > 0) insights.push(`Baisse au 3e trimestre (${t2} → ${t3} incidents, −${t2-t3}).`);
  if (t1 === 0 && t2 === 0 && t3 === 0) insights.push('Aucun incident enregistré sur les trois trimestres.');

  // Niveau le plus touché
  const ranked = NIVEAUX.map(n => ({ n, tot: getTotalByNiveau(n) })).sort((a,b)=>b.tot-a.tot);
  if (ranked[0].tot > 0) insights.push(`Le niveau ${ranked[0].n} est le plus touché avec ${ranked[0].tot} incidents.`);
  if (ranked[ranked.length-1].tot === 0) insights.push(`Aucun incident enregistré en ${ranked[ranked.length-1].n}.`);

  // Type dominant
  const typeRanked = TYPES.map(t => ({ t, tot: getTotalByType(t) })).sort((a,b)=>b.tot-a.tot);
  if (typeRanked[0].tot > 0) insights.push(`Type de violence le plus fréquent : « ${typeRanked[0].t} » (${typeRanked[0].tot} cas).`);

  // Lieu dominant
  const lieuRanked = LIEUX.map(l => ({ l, tot: getTotalByLieu(l) })).sort((a,b)=>b.tot-a.tot);
  if (lieuRanked[0].tot > 0) insights.push(`Lieu le plus touché : « ${lieuRanked[0].l} » (${lieuRanked[0].tot} incidents).`);

  // Amélioration
  const improved = NIVEAUX.filter(n => {
    const byTrim = TRIM.map(t => incidents.filter(i=>i.trimestre===t&&i.niveau===n).reduce((s,i)=>s+i.nb,0));
    return byTrim[1] < byTrim[0] && byTrim[0] > 0;
  });
  if (improved.length) insights.push(`Amélioration constatée au 2e trimestre en : ${improved.join(', ')}.`);

  el.innerHTML = `
    <div class="analysis-box">
      <h3>🔍 Analyse globale</h3>
      ${insights.map(i => `<div class="analysis-item"><div class="dot"></div><span>${i}</span></div>`).join('')}
    </div>`;
}

// ══════════════════════════════════════════════
//  PARAMS FUNCTIONS
// ══════════════════════════════════════════════
function loadParamsForm() {
  const f = (id, val) => { const el=document.getElementById(id); if(el) el.value=val||''; };
  f('p-schoolName',   params.schoolName);
  f('p-schoolYear',   params.schoolYear);
  f('p-proviseur',    params.proviseur);
  f('p-ville',        params.ville);
  f('p-region',       params.region);
  f('p-tel',          params.tel);
  f('p-email',        params.email);
  f('p-devise',       params.devise);
  f('p-niveaux',      params.niveaux || NIVEAUX.join(', '));
  f('p-types',        params.types   || TYPES.join(', '));
  f('p-lieux',        params.lieux   || LIEUX.join(', '));
  f('p-acteurs',      params.acteurs || ACTEURS.join(', '));
  f('p-titreRapport', params.titreRapport);
  f('p-soustitre',    params.soustitre);
  f('p-destinataire', params.destinataire);
  f('p-mention',      params.mention);
  const cl = document.getElementById('p-couleur');
  if (cl) cl.value = params.couleur || 'navy';
  const ig = document.getElementById('p-inclureGraphiques');
  if (ig) ig.value = params.inclureGraphiques || '1';
  ['niveaux','types','lieux','acteurs'].forEach(k => previewList(k));
  renderChampsLibres();
}

function previewList(key) {
  const inp = document.getElementById('p-'+key);
  const out = document.getElementById('preview-'+key);
  if (!inp || !out) return;
  const vals = inp.value.split(',').map(s=>s.trim()).filter(Boolean);
  out.innerHTML = vals.map(v=>`<span style="background:var(--blue-pale);color:var(--blue);padding:2px 8px;border-radius:12px;font-size:11px;font-weight:600">${v}</span>`).join('');
}

function saveParams() {
  const g = id => { const el=document.getElementById(id); return el?el.value:''; };
  params.schoolName   = g('p-schoolName');
  params.schoolYear   = g('p-schoolYear');
  params.proviseur    = g('p-proviseur');
  params.ville        = g('p-ville');
  params.region       = g('p-region');
  params.tel          = g('p-tel');
  params.email        = g('p-email');
  params.devise       = g('p-devise');
  params.niveaux      = g('p-niveaux');
  params.types        = g('p-types');
  params.lieux        = g('p-lieux');
  params.acteurs      = g('p-acteurs');
  params.titreRapport = g('p-titreRapport');
  params.soustitre    = g('p-soustitre');
  params.destinataire = g('p-destinataire');
  params.mention      = g('p-mention');
  params.couleur      = g('p-couleur');
  params.inclureGraphiques = g('p-inclureGraphiques');
  // Save champs libres
  params.champsLibres = [];
  document.querySelectorAll('.champ-libre-row').forEach(row => {
    const titre = row.querySelector('.cl-titre').value.trim();
    const contenu = row.querySelector('.cl-contenu').value.trim();
    if (titre) params.champsLibres.push({ titre, contenu });
  });
  applyParams();
  save();
  toast('✅ Paramètres enregistrés');
}

let champsLibreCount = 0;
function renderChampsLibres() {
  const cont = document.getElementById('champsLibres');
  cont.innerHTML = '';
  champsLibreCount = 0;
  (params.champsLibres||[]).forEach(cl => addChampLibre(cl.titre, cl.contenu));
}

function addChampLibre(titre='', contenu='') {
  if (champsLibreCount >= 8) { toast('⚠️ Maximum 8 rubriques'); return; }
  champsLibreCount++;
  const id = 'cl-'+Date.now();
  const div = document.createElement('div');
  div.className = 'champ-libre-row';
  div.style.cssText = 'border:1.5px solid var(--gray-200);border-radius:8px;padding:10px;margin-bottom:8px';
  div.innerHTML = `
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:6px">
      <span style="font-size:11px;font-weight:700;color:var(--gray-500);text-transform:uppercase">Rubrique ${champsLibreCount}</span>
      <button class="btn-icon btn-icon-delete" onclick="this.closest('.champ-libre-row').remove();champsLibreCount--">🗑️</button>
    </div>
    <div class="form-group" style="margin-bottom:6px">
      <label>Titre de la rubrique</label>
      <input type="text" class="cl-titre" value="${titre}" placeholder="Ex : Recommandations, Bilan…">
    </div>
    <div class="form-group">
      <label>Contenu</label>
      <textarea class="cl-contenu" style="min-height:60px;padding:8px;border:1.5px solid var(--gray-200);border-radius:8px;font-family:inherit;font-size:13px;width:100%">${contenu}</textarea>
    </div>`;
  document.getElementById('champsLibres').appendChild(div);
}

function resetApp() {
  if (!confirm('Supprimer toutes les données ? Cette action est irréversible.')) return;
  localStorage.removeItem('svsData');
  incidents = []; meta = { T1:{msg:'',mesures:''}, T2:{msg:'',mesures:''}, T3:{msg:'',mesures:''} };
  comments  = { global:'', niveaux:{}, conclusion:'' };
  params = { schoolName:'', schoolYear:'2024–2025', proviseur:'', ville:'', region:'', tel:'', email:'', devise:'',
    niveaux: ['6e','5e','4e','3e','2nde','1ère','Tle'].join(', '),
    types: ['Violence physique','Violence verbale','Violence psychologique','Menace / intimidation','Bagarre'].join(', '),
    lieux: ['Classe','Cour','Sortie école'].join(', '),
    acteurs: ['Élève–Élève','Élève–Professeur'].join(', '),
    titreRapport:'Rapport Annuel de Suivi des Violences Scolaires',
    soustitre:'', destinataire:'', mention:'', couleur:'navy', inclureGraphiques:'1', champsLibres:[] };
  applyParams();
  renderTable();
  loadParamsForm();
  toast('🗑️ Données réinitialisées');
}

// ══════════════════════════════════════════════
//  COMMENTS (dynamiques selon NIVEAUX)
// ══════════════════════════════════════════════
function loadComments() {
  const cg = document.getElementById('com-global');
  const cc = document.getElementById('com-conclusion');
  if (cg) cg.value = comments.global || '';
  if (cc) cc.value = comments.conclusion || '';
  const grid = document.querySelector('.comment-grid');
  if (!grid) return;
  grid.innerHTML = NIVEAUX.map(n => {
    const sid = 'com-niv-' + n.replace(/[^a-zA-Z0-9]/g,'_');
    const val = (comments.niveaux && comments.niveaux[n]) || '';
    return `<div class="comment-item"><label>${n}</label><textarea id="${sid}" placeholder="Observations pour la ${n}…">${val}</textarea></div>`;
  }).join('');
}

function saveComments() {
  comments.global     = (document.getElementById('com-global')||{}).value || '';
  comments.conclusion = (document.getElementById('com-conclusion')||{}).value || '';
  comments.niveaux = {};
  NIVEAUX.forEach(n => {
    const sid = 'com-niv-' + n.replace(/[^a-zA-Z0-9]/g,'_');
    const el  = document.getElementById(sid);
    if (el) comments.niveaux[n] = el.value;
  });
  save();
  toast('✅ Commentaires enregistrés');
}

// ══════════════════════════════════════════════
//  RAPPORT PREVIEW
// ══════════════════════════════════════════════
function previewRapport() {
  saveComments();
  const school = params.schoolName || '[Nom du lycée]';
  const year   = params.schoolYear || '';
  const gt     = grandTotal();
  const t1 = getTotalByTrim('T1'), t2 = getTotalByTrim('T2'), t3 = getTotalByTrim('T3');

  const el = document.getElementById('rapportPreview');
  el.innerHTML = `
    <div class="rapport-section">
      <h3>📋 En-tête</h3>
      <p><strong>Établissement :</strong> ${school}</p>
      ${params.proviseur?`<p><strong>Proviseur :</strong> ${params.proviseur}</p>`:''}
      ${params.ville?`<p><strong>Ville :</strong> ${params.ville}${params.region?' – '+params.region:''}</p>`:''}
      <p><strong>Année scolaire :</strong> ${year}</p>
      ${params.destinataire?`<p><strong>Destinataire :</strong> ${params.destinataire}</p>`:''}
      <p><strong>Date de génération :</strong> ${new Date().toLocaleDateString('fr-FR')}</p>
    </div>
    <div class="rapport-section">
      <h3>📊 Résumé global</h3>
      <p>Total d'incidents enregistrés sur l'année : <strong>${gt}</strong></p>
      <ul>
        <li>1er Trimestre : <strong>${t1}</strong> incident${t1>1?'s':''}</li>
        <li>2e Trimestre : <strong>${t2}</strong> incident${t2>1?'s':''}</li>
        <li>3e Trimestre : <strong>${t3}</strong> incident${t3>1?'s':''}</li>
      </ul>
    </div>
    ${comments.global?`<div class="rapport-section"><h3>💬 Commentaire global</h3><p>${comments.global.replace(/\n/g,'<br>')}</p></div>`:''}
    <div class="rapport-section">
      <h3>🎓 Analyse par niveau</h3>
      ${NIVEAUX.map(n=>{const tot=getTotalByNiveau(n);const com=comments.niveaux&&comments.niveaux[n]?comments.niveaux[n]:'';return`<p style="margin-bottom:6px"><span class="niveau-tag">${n}</span> — ${tot} incident${tot>1?'s':''}.${com?' '+com:''}</p>`;}).join('')}
    </div>
    ${[1,2,3].map(q=>{const t='T'+q,m=meta[t];return(m&&(m.msg||m.mesures))?`<div class="rapport-section"><h3>📅 ${q===1?'1er':q+'e'} Trimestre – Informations</h3>${m.msg?`<p><strong>Sensibilisation :</strong> ${m.msg.replace(/\n/g,'<br>')}</p>`:''}${m.mesures?`<p style="margin-top:6px"><strong>Mesures prises :</strong> ${m.mesures.replace(/\n/g,'<br>')}</p>`:''}</div>`:''}).join('')}
    ${(params.champsLibres||[]).map(cl=>cl.titre?`<div class="rapport-section"><h3>📌 ${cl.titre}</h3><p>${(cl.contenu||'').replace(/\n/g,'<br>')}</p></div>`:'').join('')}
    ${comments.conclusion?`<div class="rapport-section"><h3>🏁 Conclusion générale</h3><p>${comments.conclusion.replace(/\n/g,'<br>')}</p></div>`:''}
  `;
}

// ══════════════════════════════════════════════
//  GRAPHIQUES HORS-ÉCRAN POUR PDF
//  Utilise setTimeout au lieu de rAF (plus fiable mobile/Android)
// ══════════════════════════════════════════════
function buildOffscreenChart(type, data, options, w, h) {
  w = w || 900; h = h || 420;
  return new Promise(function(resolve) {
    var canvas = document.createElement('canvas');
    canvas.width  = w;
    canvas.height = h;
    // Doit être dans le DOM visible mais hors écran
    canvas.style.cssText = 'position:fixed;left:-9999px;top:0;opacity:0;pointer-events:none;';
    document.body.appendChild(canvas);

    var opts = {
      responsive: false,
      animation: false,          // ← pas d'animation du tout
      plugins: { legend: { display: false } },
      scales: {
        y: { beginAtZero:true, ticks:{ precision:0, font:{size:14} }, grid:{ color:'#f0f0f0' } },
        x: { ticks:{ font:{size:12} }, grid:{ display:false } }
      }
    };
    // Merge options
    if (options) {
      if (options.plugins) Object.assign(opts.plugins, options.plugins);
      if (options.scales)  Object.assign(opts.scales,  options.scales);
      if (options.indexAxis) opts.indexAxis = options.indexAxis;
    }

    var chartInst = new Chart(canvas, { type:type, data:data, options:opts });

    // setTimeout 150ms : garantit que Chart.js a fini de dessiner
    setTimeout(function() {
      var out = document.createElement('canvas');
      out.width = w; out.height = h;
      var ctx = out.getContext('2d');
      ctx.fillStyle = '#ffffff';
      ctx.fillRect(0, 0, w, h);
      ctx.drawImage(canvas, 0, 0);
      var dataUrl = out.toDataURL('image/png', 1.0);
      chartInst.destroy();
      try { document.body.removeChild(canvas); } catch(e){}
      resolve(dataUrl);
    }, 150);
  });
}

async function renderAllChartsForPDF() {
  const gt = grandTotal();
  const t1=getTotalByTrim('T1'), t2=getTotalByTrim('T2'), t3=getTotalByTrim('T3');

  const colors = { blue:'#2563a8', red:'#c0392b', green:'#27ae60', gold:'#d4a017', purple:'#7c3aed', orange:'#ea580c', teal:'#0d9488', pink:'#db2777' };
  const PAL2   = Object.values(colors);

  const legendOpts = { display: true, position: 'bottom', labels: { font: { size: 12 }, boxWidth: 14, padding: 10 } };
  const noScales   = { y: { display: false }, x: { display: false } };

  // 1 – Barres par trimestre
  const img1 = await buildOffscreenChart('bar', {
    labels: ['1er Trimestre','2e Trimestre','3e Trimestre'],
    datasets: [{ label: 'Incidents', data: [t1,t2,t3],
      backgroundColor: [colors.blue, colors.green, colors.red], borderRadius: 8 }]
  }, {});

  // 2 – Types par trimestre (groupé)
  const img2 = await buildOffscreenChart('bar', {
    labels: ['T1','T2','T3'],
    datasets: TYPES.map((tp,i) => ({
      label: tp,
      data: TRIM.map(t => incidents.filter(inc=>inc.trimestre===t&&inc.type===tp).reduce((s,i)=>s+i.nb,0)),
      backgroundColor: PAL2[i], borderRadius: 5
    }))
  }, { plugins: { legend: legendOpts } }, 900, 480);

  // 3 – Camembert répartition types
  const pieData = TYPES.map(tp => getTotalByType(tp));
  const img3 = await buildOffscreenChart('doughnut', {
    labels: TYPES,
    datasets: [{ data: pieData, backgroundColor: PAL2, borderWidth: 3, borderColor: '#fff' }]
  }, { plugins: { legend: legendOpts }, scales: noScales }, 700, 480);

  // 4 – Lieux et acteurs
  const img4 = await buildOffscreenChart('bar', {
    labels: [...LIEUX, ...ACTEURS],
    datasets: [{ label: 'Incidents',
      data: [...LIEUX.map(l=>getTotalByLieu(l)), ...ACTEURS.map(a=>getTotalByActeurs(a))],
      backgroundColor: [...LIEUX.map((_,i)=>PAL2[i]), ...ACTEURS.map((_,i)=>PAL2[i+4])],
      borderRadius: 8 }]
  }, {});

  // 5 – Par niveau
  const img5 = await buildOffscreenChart('bar', {
    labels: NIVEAUX,
    datasets: [{ label: 'Incidents',
      data: NIVEAUX.map(n=>getTotalByNiveau(n)),
      backgroundColor: NIVEAUX.map((_,i)=>PAL2[i%PAL2.length]), borderRadius: 8 }]
  }, {});

  // 6 – Comparaison niveaux/trimestres
  const img6 = await buildOffscreenChart('bar', {
    labels: NIVEAUX,
    datasets: TRIM.map((t,i) => ({
      label: t==='T1'?'1er Trimestre':t==='T2'?'2e Trimestre':'3e Trimestre',
      data: NIVEAUX.map(n=>incidents.filter(inc=>inc.trimestre===t&&inc.niveau===n).reduce((s,i)=>s+i.nb,0)),
      backgroundColor: [colors.blue, colors.green, colors.red][i], borderRadius: 5
    }))
  }, { plugins: { legend: legendOpts } }, 900, 480);

  return [
    { label: 'Incidents par trimestre',            img: img1 },
    { label: 'Types de violence par trimestre',    img: img2 },
    { label: 'Répartition des violences',          img: img3 },
    { label: 'Lieux et acteurs',                   img: img4 },
    { label: 'Violences par niveau',               img: img5 },
    { label: 'Comparaison niveaux / trimestres',   img: img6 },
  ];
}

// ══════════════════════════════════════════════
//  PDF GENERATION
// ══════════════════════════════════════════════
async function generatePDF() {
  if (!incidents.length) { toast('⚠️ Aucun incident à inclure'); return; }
  saveComments();

  document.getElementById('pdfLoading').classList.add('show');
  await new Promise(r => setTimeout(r, 60));

  try {
    // Couleur principale selon params
    const palettes = {
      navy:   [10,22,40],   green:  [26,107,58],
      red:    [192,57,43],  purple: [109,40,217],
      orange: [234,88,12]
    };
    const PCOLOR = palettes[params.couleur] || palettes.navy;
    const PCOLOR2 = PCOLOR.map((c,i)=>Math.min(255,c+40)); // lighter variant

    // ── Générer images graphiques ──
    var chartImages = [];
    if (params.inclureGraphiques !== '0') {
      chartImages = await renderAllChartsForPDF();
    }

    const { jsPDF } = window.jspdf;
    const doc = new jsPDF({ unit: 'mm', format: 'a4' });
    const W = 210, H = 297, margin = 15;
    const contentW = W - margin * 2;
    let y = 20;

    const school = params.schoolName || 'Lycée';
    const year   = params.schoolYear || '';
    const titre  = params.titreRapport || 'Rapport Annuel de Suivi des Violences Scolaires';
    const gt     = grandTotal();
    const t1=getTotalByTrim('T1'), t2=getTotalByTrim('T2'), t3=getTotalByTrim('T3');

    function newPage() { doc.addPage(); y = 15; }
    function checkPage(extra) { if (y + (extra||0) > H-18) newPage(); }

    function sectionTitle(title, color) {
      color = color || PCOLOR;
      checkPage(14);
      doc.setFillColor(color[0],color[1],color[2]);
      doc.rect(margin, y, contentW, 7, 'F');
      doc.setTextColor(255,255,255);
      doc.setFont('helvetica','bold'); doc.setFontSize(10);
      doc.text(title, margin+3, y+5);
      doc.setTextColor(0,0,0); doc.setFont('helvetica','normal');
      y += 11;
    }

    function addText(text, size, bold, indent) {
      size=size||10; bold=bold||false; indent=indent||0;
      checkPage(10);
      doc.setFontSize(size);
      doc.setFont('helvetica', bold?'bold':'normal');
      var lines = doc.splitTextToSize(text, contentW - indent);
      doc.text(lines, margin + indent, y);
      y += lines.length * (size * 0.45) + 2;
    }

    function insertChartPair(left, right, hMM) {
      hMM = hMM || 78;
      var halfW = (contentW - 6) / 2;
      checkPage(hMM + 14);
      // Left
      doc.setFontSize(8); doc.setFont('helvetica','bold');
      doc.setTextColor(PCOLOR[0],PCOLOR[1],PCOLOR[2]);
      doc.text(left.label, margin, y);
      doc.setTextColor(0,0,0);
      doc.setDrawColor(200,210,230); doc.setLineWidth(0.4);
      doc.rect(margin, y+4, halfW, hMM);
      if (left.img) doc.addImage(left.img,'PNG',margin+1,y+5,halfW-2,hMM-2);
      // Right
      var rx = margin + halfW + 6;
      doc.setFontSize(8); doc.setFont('helvetica','bold');
      doc.setTextColor(PCOLOR[0],PCOLOR[1],PCOLOR[2]);
      doc.text(right.label, rx, y);
      doc.setTextColor(0,0,0);
      doc.rect(rx, y+4, halfW, hMM);
      if (right.img) doc.addImage(right.img,'PNG',rx+1,y+5,halfW-2,hMM-2);
      y += hMM + 12;
    }

    function insertChart(img, label, hMM) {
      hMM = hMM || 82;
      checkPage(hMM + 14);
      doc.setFontSize(8); doc.setFont('helvetica','bold');
      doc.setTextColor(PCOLOR[0],PCOLOR[1],PCOLOR[2]);
      doc.text(label, margin, y);
      doc.setTextColor(0,0,0); y += 4;
      doc.setDrawColor(200,210,230); doc.setLineWidth(0.4);
      doc.rect(margin, y, contentW, hMM);
      if (img) doc.addImage(img,'PNG',margin+1,y+1,contentW-2,hMM-2);
      y += hMM + 7;
    }

    // ══════════ EN-TÊTE PAGE 1 ══════════
    doc.setFillColor(PCOLOR[0],PCOLOR[1],PCOLOR[2]);
    doc.rect(0,0,W,42,'F');
    doc.setFillColor(PCOLOR2[0],PCOLOR2[1],PCOLOR2[2]);
    doc.rect(0,42,W,2,'F');
    doc.setFillColor(212,160,23);
    doc.rect(0,44,W,1,'F');

    doc.setTextColor(255,255,255);
    doc.setFontSize(15); doc.setFont('helvetica','bold');
    doc.text(titre, W/2, 12, {align:'center'});
    doc.setFontSize(13); doc.setFont('helvetica','normal');
    doc.text(school, W/2, 21, {align:'center'});
    if (params.proviseur) { doc.setFontSize(10); doc.text('Proviseur : '+params.proviseur, W/2, 29, {align:'center'}); }
    doc.setFontSize(9);
    doc.text('Année scolaire : '+year+'   |   Généré le '+new Date().toLocaleDateString('fr-FR'), W/2, 37, {align:'center'});
    doc.setTextColor(0,0,0);
    y = 52;

    // Sous-titre / destinataire
    if (params.soustitre || params.destinataire) {
      doc.setFontSize(9); doc.setFont('helvetica','italic');
      if (params.soustitre)    { doc.text(params.soustitre,    margin, y); y+=6; }
      if (params.destinataire) { doc.text('Destinataire : '+params.destinataire, margin, y); y+=6; }
      doc.setFont('helvetica','normal'); y+=3;
    }

    // ══════════ RÉSUMÉ ══════════
    sectionTitle('RÉSUMÉ GLOBAL');
    addText('Total incidents sur l\'année : '+gt, 11, true);
    addText('1er Trimestre : '+t1+'   |   2e Trimestre : '+t2+'   |   3e Trimestre : '+t3, 10);
    y += 5;

    // ══════════ TABLEAU DES INCIDENTS ══════════
    sectionTitle('TABLEAU DES INCIDENTS');
    var hdr=['Trim.','Niveau','Type de violence','Lieu','Acteurs','Nb'];
    var cW=[18,16,54,30,32,14];
    var x=margin;
    doc.setFillColor(PCOLOR[0],PCOLOR[1],PCOLOR[2]); doc.rect(margin,y,contentW,7,'F');
    doc.setTextColor(255,255,255); doc.setFont('helvetica','bold'); doc.setFontSize(8);
    hdr.forEach(function(h,i){ doc.text(h,x+2,y+5); x+=cW[i]; });
    doc.setTextColor(0,0,0); doc.setFont('helvetica','normal'); y+=7;
    incidents.forEach(function(inc,idx){
      checkPage(7);
      if(idx%2===0){doc.setFillColor(245,248,252);doc.rect(margin,y,contentW,6,'F');}
      x=margin; doc.setFontSize(8);
      [inc.trimestre,inc.niveau,inc.type,inc.lieu,inc.acteurs,''+inc.nb].forEach(function(cell,i){
        doc.text(doc.splitTextToSize(cell,cW[i]-2)[0],x+2,y+4); x+=cW[i];
      });
      y+=6;
    });
    y+=5;

    // ══════════ STATS PAR NIVEAU ══════════
    sectionTitle('STATISTIQUES PAR NIVEAU');
    var sH=['Niveau','T1','T2','T3','Total','%'],sC=[28,22,22,22,26,22];
    x=margin;
    doc.setFillColor(PCOLOR[0],PCOLOR[1],PCOLOR[2]); doc.rect(margin,y,contentW,7,'F');
    doc.setTextColor(255,255,255); doc.setFont('helvetica','bold'); doc.setFontSize(8);
    sH.forEach(function(h,i){ doc.text(h,x+2,y+5); x+=sC[i]; });
    doc.setTextColor(0,0,0); y+=7;
    NIVEAUX.forEach(function(n,idx){
      checkPage(7);
      var nt1=incidents.filter(function(i){return i.trimestre==='T1'&&i.niveau===n;}).reduce(function(s,i){return s+i.nb;},0);
      var nt2=incidents.filter(function(i){return i.trimestre==='T2'&&i.niveau===n;}).reduce(function(s,i){return s+i.nb;},0);
      var nt3=incidents.filter(function(i){return i.trimestre==='T3'&&i.niveau===n;}).reduce(function(s,i){return s+i.nb;},0);
      var tot=nt1+nt2+nt3, pct=gt?((tot/gt)*100).toFixed(1):'0.0';
      if(idx%2===0){doc.setFillColor(245,248,252);doc.rect(margin,y,contentW,6,'F');}
      x=margin; doc.setFontSize(8); doc.setFont('helvetica','normal');
      [''+n,''+nt1,''+nt2,''+nt3,''+tot,pct+'%'].forEach(function(v,i){ doc.text(v,x+2,y+4); x+=sC[i]; });
      y+=6;
    });
    checkPage(7);
    doc.setFillColor(PCOLOR[0],PCOLOR[1],PCOLOR[2]); doc.rect(margin,y,contentW,7,'F');
    doc.setTextColor(255,255,255); doc.setFont('helvetica','bold'); doc.setFontSize(8);
    x=margin;
    ['TOTAL',''+t1,''+t2,''+t3,''+gt,'100%'].forEach(function(v,i){ doc.text(v,x+2,y+5); x+=sC[i]; });
    doc.setTextColor(0,0,0); y+=11;

    // ══════════ ANALYSE ══════════
    sectionTitle('ANALYSE AUTOMATIQUE');
    if(t2<t1&&t1>0) addText('• Baisse au 2e trimestre : '+t1+' → '+t2+' incidents (−'+(t1-t2)+')',10);
    if(t2>t1&&t1>0) addText('• Hausse au 2e trimestre : '+t1+' → '+t2+' incidents (+'+(t2-t1)+')',10);
    if(t3>t2&&t2>0) addText('• Hausse au 3e trimestre : '+t2+' → '+t3+' incidents (+'+(t3-t2)+')',10);
    if(t3<t2&&t2>0) addText('• Baisse au 3e trimestre : '+t2+' → '+t3+' incidents (−'+(t2-t3)+')',10);
    var topN=NIVEAUX.map(function(n){return{n:n,tot:getTotalByNiveau(n)};}).sort(function(a,b){return b.tot-a.tot;})[0];
    if(topN.tot>0) addText('• Niveau le plus touché : '+topN.n+' ('+topN.tot+' incidents)',10);
    var topT=TYPES.map(function(t){return{t:t,tot:getTotalByType(t)};}).sort(function(a,b){return b.tot-a.tot;})[0];
    if(topT.tot>0) addText('• Type dominant : '+topT.t+' ('+topT.tot+' cas)',10);
    var topL=LIEUX.map(function(l){return{l:l,tot:getTotalByLieu(l)};}).sort(function(a,b){return b.tot-a.tot;})[0];
    if(topL.tot>0) addText('• Lieu le plus concerné : '+topL.l+' ('+topL.tot+' incidents)',10);
    y+=5;

    // ══════════ GRAPHIQUES ══════════
    if (chartImages.length >= 6) {
      newPage();
      doc.setFillColor(PCOLOR[0],PCOLOR[1],PCOLOR[2]); doc.rect(0,0,W,14,'F');
      doc.setTextColor(255,255,255); doc.setFont('helvetica','bold'); doc.setFontSize(13);
      doc.text('VISUALISATIONS STATISTIQUES', W/2, 9, {align:'center'});
      doc.setTextColor(0,0,0); y=20;

      insertChartPair({label:chartImages[0].label,img:chartImages[0].img},{label:chartImages[2].label,img:chartImages[2].img},82);
      insertChart(chartImages[1].img, chartImages[1].label, 88);

      newPage();
      doc.setFillColor(PCOLOR[0],PCOLOR[1],PCOLOR[2]); doc.rect(0,0,W,14,'F');
      doc.setTextColor(255,255,255); doc.setFont('helvetica','bold'); doc.setFontSize(13);
      doc.text('VISUALISATIONS STATISTIQUES (suite)', W/2, 9, {align:'center'});
      doc.setTextColor(0,0,0); y=20;

      insertChart(chartImages[3].img, chartImages[3].label, 82);
      insertChartPair({label:chartImages[4].label,img:chartImages[4].img},{label:chartImages[5].label,img:chartImages[5].img},88);
    }

    // ══════════ COMMENTAIRES ══════════
    var hasContent = comments.global || NIVEAUX.some(function(n){return comments.niveaux&&comments.niveaux[n];})
      || comments.conclusion || [1,2,3].some(function(q){var m=meta['T'+q];return m&&(m.msg||m.mesures);})
      || (params.champsLibres||[]).some(function(cl){return cl.titre;});

    if (hasContent) {
      newPage();
      if (comments.global) { sectionTitle('COMMENTAIRE GLOBAL'); addText(comments.global,10); y+=3; }

      var hasNivCom=NIVEAUX.some(function(n){return comments.niveaux&&comments.niveaux[n];});
      if(hasNivCom){
        sectionTitle('COMMENTAIRES PAR NIVEAU');
        NIVEAUX.forEach(function(n){
          if(comments.niveaux&&comments.niveaux[n]){ checkPage(14); addText(n+' :',10,true); addText(comments.niveaux[n],10,false,5); y+=2; }
        });
      }

      var hasMeta=[1,2,3].some(function(q){var m=meta['T'+q];return m&&(m.msg||m.mesures);});
      if(hasMeta){
        sectionTitle('INFORMATIONS TRIMESTRIELLES');
        [1,2,3].forEach(function(q){
          var t='T'+q,m=meta[t];
          if(m&&(m.msg||m.mesures)){
            checkPage(22);
            addText((q===1?'1er':q+'e')+' Trimestre',10,true);
            if(m.msg)     addText('Sensibilisation : '+m.msg,9,false,5);
            if(m.mesures) addText('Mesures prises : '+m.mesures,9,false,5);
            y+=3;
          }
        });
      }

      // Champs libres personnalisés
      (params.champsLibres||[]).forEach(function(cl){
        if(!cl.titre) return;
        sectionTitle(cl.titre.toUpperCase(), PCOLOR2);
        if(cl.contenu) addText(cl.contenu, 10);
        y+=3;
      });

      if(comments.conclusion){ sectionTitle('CONCLUSION GÉNÉRALE',[26,107,58]); addText(comments.conclusion,10); }
    }

    // ══════════ MENTION LÉGALE + FOOTERS ══════════
    var pageCount = doc.getNumberOfPages();
    for(var i=1;i<=pageCount;i++){
      doc.setPage(i);
      doc.setFillColor(240,244,250); doc.rect(0,H-10,W,10,'F');
      doc.setFontSize(8); doc.setTextColor(100); doc.setFont('helvetica','normal');
      doc.text('Page '+i+' / '+pageCount, margin, H-4);
      doc.text(school+'  –  '+year, W/2, H-4, {align:'center'});
      var mention = params.mention || new Date().toLocaleDateString('fr-FR');
      doc.text(mention, W-margin, H-4, {align:'right'});
    }

    doc.save('rapport-violences-'+(year||'lycee')+'.pdf');
    toast('✅ PDF avec graphiques généré !');

  } catch(e) {
    console.error(e);
    toast('❌ Erreur : ' + e.message);
  } finally {
    document.getElementById('pdfLoading').classList.remove('show');
  }
}

// ══════════════════════════════════════════════
//  CSV EXPORT / IMPORT
// ══════════════════════════════════════════════
function exportCSV() {
  if (!incidents.length) { toast('⚠️ Aucune donnée'); return; }
  const rows = [['Trimestre','Niveau','Type','Lieu','Acteurs','Nombre']];
  incidents.forEach(i => rows.push([i.trimestre, i.niveau, i.type, i.lieu, i.acteurs, i.nb]));
  const csv = rows.map(r => r.join(';')).join('\n');
  const blob = new Blob(['\ufeff'+csv], { type:'text/csv;charset=utf-8' });
  const url  = URL.createObjectURL(blob);
  const a    = document.createElement('a');
  a.href = url; a.download = 'incidents-violences.csv'; a.click();
  URL.revokeObjectURL(url);
  toast('✅ CSV exporté');
}

function importCSV(event) {
  const file = event.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = e => {
    try {
      const lines = e.target.result.split('\n').filter(Boolean);
      const imported = [];
      lines.slice(1).forEach(line => {
        const [trimestre,niveau,type,lieu,acteurs,nb] = line.split(';');
        if (trimestre && niveau) {
          imported.push({ id: Date.now().toString()+Math.random(), trimestre:trimestre.trim(), niveau:niveau.trim(), type:type.trim(), lieu:lieu.trim(), acteurs:acteurs.trim(), nb:parseInt(nb)||1 });
        }
      });
      incidents = [...incidents, ...imported];
      save();
      renderTable();
      toast(`✅ ${imported.length} ligne(s) importée(s)`);
    } catch(err) { toast('❌ Erreur d\'import'); }
  };
  reader.readAsText(file, 'utf-8');
  event.target.value = '';
}

// ══════════════════════════════════════════════
//  TOAST
// ══════════════════════════════════════════════
function toast(msg) {
  const el = document.getElementById('toast');
  el.textContent = msg;
  el.classList.add('show');
  setTimeout(() => el.classList.remove('show'), 2500);
}

// ══════════════════════════════════════════════
//  AUTO-SAVE ON INPUT
// ══════════════════════════════════════════════
document.getElementById('schoolName').addEventListener('input', function() {
  params.schoolName = this.value; save();
});
document.getElementById('schoolYear').addEventListener('input', function() {
  params.schoolYear = this.value; save();
});

// ══════════════════════════════════════════════
//  INIT
// ══════════════════════════════════════════════
load();
renderTable();
</script>
</body>
</html>
