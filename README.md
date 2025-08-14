<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Villa Helpdesk — 181 Villas</title>
<style>
  :root{
    --bg:#f6f7fb;
    --card:#ffffff;
    --ink:#1f2937;
    --muted:#6b7280;
    --brand:#0ea5e9;      /* Sky */
    --brand-2:#10b981;    /* Emerald */
    --accent:#2563eb;     /* Blue */
    --danger:#ef4444;
    --warn:#f59e0b;
    --ok:#10b981;
    --chip:#eef2ff;
    --border:#e5e7eb;
    --shadow:0 10px 20px rgba(0,0,0,.06);
    --radius:14px;
  }
  *{box-sizing:border-box}
  html,body{margin:0;padding:0;background:var(--bg);color:var(--ink);font:14px/1.35 system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji"}
  .container{max-width:1200px;margin:24px auto;padding:0 16px}

  header{
    display:flex;align-items:center;justify-content:space-between;
    margin-bottom:18px
  }
  .brand{
    display:flex;align-items:center;gap:12px
  }
  .brand-badge{
    width:48px;height:48px;border-radius:12px;background:linear-gradient(135deg,var(--brand),var(--brand-2));
    display:grid;place-items:center;color:white;font-size:22px;box-shadow:var(--shadow)
  }
  h1{margin:0;font-size:22px}
  .sub{color:var(--muted);font-size:13px}

  .cards{display:grid;grid-template-columns:repeat(5,1fr);gap:12px;margin:16px 0}
  .card{
    background:var(--card);border:1px solid var(--border);border-radius:12px;padding:14px;box-shadow:var(--shadow);
    display:flex;flex-direction:column;gap:6px;min-height:84px
  }
  .card small{color:var(--muted)}
  .metric{font-size:22px;font-weight:700}
  .pill{display:inline-flex;align-items:center;gap:8px;padding:6px 10px;border-radius:999px;background:#f1f5f9;border:1px solid var(--border);color:var(--ink)}

  .toolbar{
    display:flex;flex-wrap:wrap;gap:10px;align-items:center;margin:10px 0
  }
  .toolbar .group{display:flex;gap:8px;flex-wrap:wrap}
  input[type="text"], input[type="tel"], input[type="number"], select, textarea, input[type="datetime-local"]{
    padding:9px 10px;border:1px solid var(--border);border-radius:10px;background:white;outline:none;min-width:0
  }
  input::placeholder, textarea::placeholder{color:#9ca3af}
  textarea{resize:vertical;min-height:80px}
  .btn{
    padding:10px 12px;border:1px solid var(--border);border-radius:10px;background:white;cursor:pointer;
    display:inline-flex;align-items:center;gap:8px
  }
  .btn.primary{background:linear-gradient(135deg,var(--accent),#60a5fa);color:white;border-color:transparent}
  .btn.success{background:linear-gradient(135deg,var(--brand-2),#34d399);color:white;border-color:transparent}
  .btn.warn{background:linear-gradient(135deg,var(--warn),#fbbf24);color:white;border-color:transparent}
  .btn.ghost{background:#f8fafc}
  .btn.red{background:linear-gradient(135deg,var(--danger),#f87171);color:white;border-color:transparent}
  .btn:disabled{opacity:.6;cursor:not-allowed}

  .table-wrap{
    background:var(--card);border:1px solid var(--border);border-radius:12px;box-shadow:var(--shadow);overflow:auto
  }
  table{border-collapse:separate;border-spacing:0;width:100%}
  thead th{position:sticky;top:0;background:#f8fafc;border-bottom:1px solid var(--border);text-align:left;font-weight:600;color:#475569;padding:12px}
  tbody td{border-bottom:1px solid var(--border);padding:12px;vertical-align:top}
  tbody tr:hover{background:#f9fafb}
  .id{font-family:ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", monospace;color:#334155}
  .badge{padding:4px 8px;border-radius:999px;font-weight:600;font-size:12px;display:inline-block;border:1px solid transparent}
  .status-open{background:#eff6ff;color:#1d4ed8;border-color:#bfdbfe}
  .status-progress{background:#ecfeff;color:#0891b2;border-color:#a5f3fc}
  .status-hold{background:#fff7ed;color:#c2410c;border-color:#fed7aa}
  .status-resolved{background:#ecfdf5;color:#047857;border-color:#a7f3d0}
  .status-closed{background:#f1f5f9;color:#334155;border-color:#e2e8f0}
  .prio-low{background:#f1f5f9;color:#334155}
  .prio-medium{background:#eef2ff;color:#3730a3}
  .prio-high{background:#fffbeb;color:#b45309}
  .prio-urgent{background:#fee2e2;color:#b91c1c}

  .modal{position:fixed;inset:0;background:rgba(15,23,42,.5);display:none;align-items:center;justify-content:center;padding:20px}
  .modal.show{display:flex}
  .sheet{background:var(--card);border-radius:16px;border:1px solid var(--border);box-shadow:0 24px 64px rgba(0,0,0,.2);max-width:980px;width:100%;max-height:90vh;overflow:auto}
  .sheet header{padding:16px 18px;border-bottom:1px solid var(--border)}
  .sheet .body{display:grid;grid-template-columns:1.2fr .8fr;gap:16px;padding:16px}
  .section{display:flex;flex-direction:column;gap:12px}
  .row{display:grid;grid-template-columns:1fr 1fr;gap:10px}
  .row3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px}
  .muted{color:var(--muted)}
  .timeline{display:flex;flex-direction:column;gap:10px}
  .note{border:1px dashed var(--border);padding:10px;border-radius:10px;background:#fafafa}
  .note small{color:var(--muted)}
  .footer{display:flex;justify-content:space-between;gap:10px;padding:12px 16px;border-top:1px solid var(--border);background:#f8fafc;border-bottom-left-radius:16px;border-bottom-right-radius:16px}

  .toast{position:fixed;bottom:18px;right:18px;display:flex;flex-direction:column;gap:8px;z-index:9999}
  .toast .t{background:#111827;color:white;padding:10px 12px;border-radius:10px;box-shadow:var(--shadow);opacity:.95}

  @media (max-width:960px){
    .cards{grid-template-columns:repeat(2,1fr)}
    .sheet .body{grid-template-columns:1fr}
    .row,.row3{grid-template-columns:1fr}
  }
  @media (max-width:560px){
    header{flex-direction:column;align-items:flex-start;gap:6px}
    .cards{grid-template-columns:1fr}
  }
</style>
</head>
<body>
  <div class="container">
    <header>
      <div class="brand">
        <div class="brand-badge">🏡</div>
        <div>
          <h1>Compound Helpdesk</h1>
          <div class="sub">181 villas • Electrical • Plumbing • AC • Carpentry • Cleaning</div>
        </div>
      </div>
      <div class="group">
        <button class="btn primary" id="btnNew">➕ New ticket</button>
        <button class="btn ghost" id="btnExportCsv">⬇️ Export CSV</button>
        <button class="btn ghost" id="btnExportJson">⬇️ Backup JSON</button>
      </div>
    </header>

    <div class="cards" id="summaryCards">
      <!-- Summary cards injected -->
    </div>

    <div class="toolbar">
      <div class="group" style="flex:1 1 auto">
        <input id="q" type="text" placeholder="Search ID, villa, requester, phone, description…" style="flex:1 1 360px" />
        <select id="status">
          <option value="">Status — All</option>
        </select>
        <select id="category">
          <option value="">Category — All</option>
        </select>
        <select id="priority">
          <option value="">Priority — All</option>
        </select>
        <input id="villa" type="number" min="1" max="181" placeholder="Villa #" style="width:110px" />
        <select id="sort">
          <option value="new">Sort: Newest</option>
          <option value="old">Sort: Oldest</option>
          <option value="prio">Sort: Priority (High→Low)</option>
          <option value="villa">Sort: Villa #</option>
        </select>
      </div>
      <div class="group">
        <button class="btn" id="btnClear">Clear</button>
        <button class="btn success" id="btnSeed">Load sample</button>
      </div>
    </div>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th style="width:120px">Ticket</th>
            <th style="width:80px">Villa</th>
            <th style="width:120px">Category</th>
            <th style="width:120px">Priority</th>
            <th style="width:140px">Status</th>
            <th>Requester</th>
            <th style="width:140px">Assigned</th>
            <th style="width:160px">Created</th>
            <th style="width:160px">Updated</th>
            <th style="width:80px"></th>
          </tr>
        </thead>
        <tbody id="tbody">
          <!-- rows -->
        </tbody>
      </table>
    </div>
  </div>

  <!-- Modal -->
  <div class="modal" id="modal">
    <div class="sheet">
      <header>
        <div style="display:flex;align-items:center;justify-content:space-between;width:100%">
          <div>
            <div id="modalTitle" style="font-weight:700;font-size:18px">New Ticket</div>
            <div class="sub" id="modalSub"></div>
          </div>
          <button class="btn" id="btnClose">✖️ Close</button>
        </div>
      </header>
      <div class="body">
        <div class="section">
          <div class="row3">
            <div>
              <label>Villa No</label>
              <input id="f_villa" type="number" min="1" max="181" placeholder="1–181" />
            </div>
            <div>
              <label>Requester name</label>
              <input id="f_requester" type="text" placeholder="Resident name" />
            </div>
            <div>
              <label>Phone</label>
              <input id="f_phone" type="tel" placeholder="05x-xxx-xxxx" />
            </div>
          </div>
          <div class="row3">
            <div>
              <label>Category</label>
              <select id="f_category"></select>
            </div>
            <div>
              <label>Priority</label>
              <select id="f_priority"></select>
            </div>
            <div>
              <label>Status</label>
              <select id="f_status"></select>
            </div>
          </div>
          <div class="row">
            <div>
              <label>Assigned to</label>
              <input id="f_assigned" type="text" placeholder="Technician / Team" />
            </div>
            <div>
              <label>Preferred time (optional)</label>
              <input id="f_when" type="datetime-local" />
            </div>
          </div>
          <div>
            <label>Description</label>
            <textarea id="f_desc" placeholder="Describe the issue…"></textarea>
          </div>

          <div class="row">
            <button class="btn primary" id="btnSave">💾 Save</button>
            <button class="btn warn" id="btnResolve">✅ Mark Resolved</button>
          </div>
        </div>

        <div class="section">
          <div>
            <div class="pill" id="ticketInfo">ID — n/a</div>
          </div>

          <div class="timeline" id="notesList"></div>

          <div class="row">
            <input id="f_note" type="text" placeholder="Add an internal note…" />
            <button class="btn" id="btnAddNote">➕ Add note</button>
          </div>

          <div class="row">
            <button class="btn red" id="btnDelete">🗑️ Delete ticket</button>
            <div></div>
          </div>
        </div>
      </div>
      <div class="footer">
        <div class="muted" id="metaLeft">Created —</div>
        <div class="muted" id="metaRight">Due —</div>
      </div>
    </div>
  </div>

  <div class="toast" id="toast"></div>

<script>
(function(){
  // Constants
  const KEY='villa_helpdesk_tickets_v1';
  const KEY_COUNTER='villa_helpdesk_counter_v1';
  const CATEGORIES=['Electrical','Plumbing','AC','Carpentry','Cleaning','Other'];
  const PRIORITIES=['Low','Medium','High','Urgent'];
  const STATUSES=['Open','In Progress','On Hold','Resolved','Closed'];
  const SLA_HOURS={ Low:72, Medium:48, High:24, Urgent:6 };

  // State
  let tickets=[];
  let activeId=null;

  // Elements
  const els={
    tbody: $('#tbody'),
    q: $('#q'),
    status: $('#status'),
    category: $('#category'),
    priority: $('#priority'),
    villa: $('#villa'),
    sort: $('#sort'),
    btnNew: $('#btnNew'),
    btnClear: $('#btnClear'),
    btnSeed: $('#btnSeed'),
    btnExportCsv: $('#btnExportCsv'),
    btnExportJson: $('#btnExportJson'),
    modal: $('#modal'),
    btnClose: $('#btnClose'),
    f_villa: $('#f_villa'),
    f_requester: $('#f_requester'),
    f_phone: $('#f_phone'),
    f_category: $('#f_category'),
    f_priority: $('#f_priority'),
    f_status: $('#f_status'),
    f_assigned: $('#f_assigned'),
    f_when: $('#f_when'),
    f_desc: $('#f_desc'),
    f_note: $('#f_note'),
    btnAddNote: $('#btnAddNote'),
    btnSave: $('#btnSave'),
    btnDelete: $('#btnDelete'),
    btnResolve: $('#btnResolve'),
    notesList: $('#notesList'),
    ticketInfo: $('#ticketInfo'),
    modalTitle: $('#modalTitle'),
    modalSub: $('#modalSub'),
    metaLeft: $('#metaLeft'),
    metaRight: $('#metaRight'),
    summaryCards: $('#summaryCards'),
    toast: $('#toast')
  };

  // Init selects
  initSelect(els.status, ['','Open','In Progress','On Hold','Resolved','Closed'], ['All','Open','In Progress','On Hold','Resolved','Closed']);
  initSelect(els.category, ['','Electrical','Plumbing','AC','Carpentry','Cleaning','Other'], ['All','Electrical','Plumbing','AC','Carpentry','Cleaning','Other']);
  initSelect(els.priority, ['','Low','Medium','High','Urgent'], ['All','Low','Medium','High','Urgent']);

  initSelect(els.f_category, CATEGORIES);
  initSelect(els.f_priority, PRIORITIES);
  initSelect(els.f_status, STATUSES);

  // Load data
  tickets = load(KEY) || [];
  if (!tickets.length) {
    // Optional: auto-seed once to show preview
    seedSample();
    toast('Loaded sample tickets (demo).');
  }
  render();

  // Events
  [els.q, els.status, els.category, els.priority, els.villa, els.sort]
    .forEach(el => el.addEventListener('input', render));

  els.btnClear.addEventListener('click', ()=>{
    els.q.value=''; els.status.value=''; els.category.value=''; els.priority.value='';
    els.villa.value=''; els.sort.value='new'; render();
  });

  els.btnSeed.addEventListener('click', ()=>{
    seedSample(true);
    render();
    toast('Sample tickets added.');
  });

  els.btnExportCsv.addEventListener('click', exportCSV);
  els.btnExportJson.addEventListener('click', exportJSON);

  els.btnNew.addEventListener('click', ()=>openModal());
  els.btnClose.addEventListener('click', closeModal);

  els.btnSave.addEventListener('click', saveTicket);
  els.btnDelete.addEventListener('click', deleteTicket);
  els.btnResolve.addEventListener('click', ()=> {
    if(!activeId) return;
    const t = tickets.find(x=>x.id===activeId);
    if (!t) return;
    if (t.status==='Resolved' || t.status==='Closed') {
      toast('Ticket already resolved/closed.');
      return;
    }
    const prev = t.status;
    t.status='Resolved';
    t.updatedAt=Date.now();
    t.notes.push(note(`Status changed from ${prev} to Resolved`));
    persist();
    fillModal(t);
    render();
    toast('Marked as resolved.');
  });

  els.btnAddNote.addEventListener('click', ()=>{
    if(!activeId) return;
    const txt = (els.f_note.value||'').trim();
    if(!txt) return;
    const t = tickets.find(x=>x.id===activeId);
    t.notes.push(note(txt));
    t.updatedAt=Date.now();
    els.f_note.value='';
    persist();
    fillModal(t);
    render();
  });

  // Functions
  function render(){
    renderSummary();
    const filtered = getFiltered();
    renderTable(filtered);
  }

  function renderSummary(){
    const total = tickets.length;
    const byStatus = countBy(tickets, 'status');
    const open = (byStatus['Open']||0);
    const prog = (byStatus['In Progress']||0);
    const hold = (byStatus['On Hold']||0);
    const resolved = (byStatus['Resolved']||0);
    const closed = (byStatus['Closed']||0);
    const active = open+prog+hold;

    els.summaryCards.innerHTML = `
      ${card('All tickets', total, '🗂️')}
      ${card('Active', active, '📌')}
      ${card('Open', open, '🟦')}
      ${card('In Progress', prog, '🛠️')}
      ${card('Resolved', resolved, '✅')}
    `;
  }

  function card(label, value, icon){
    return `
      <div class="card">
        <small>${label}</small>
        <div class="metric">${value}</div>
        <div class="muted">${icon}</div>
      </div>
    `;
  }

  function getFiltered(){
    let arr = [...tickets];
    const q = (els.q.value||'').trim().toLowerCase();
    const st = els.status.value;
    const cat = els.category.value;
    const pr = els.priority.value;
    const v = parseInt(els.villa.value,10);

    if (q){
      arr = arr.filter(t=>{
        const hay = `${t.id} ${t.villa} ${t.requester} ${t.phone} ${t.category} ${t.priority} ${t.status} ${t.assignedTo} ${t.description}`.toLowerCase();
        return hay.includes(q);
      });
    }
    if (st) arr = arr.filter(t=>t.status===st);
    if (cat) arr = arr.filter(t=>t.category===cat);
    if (pr) arr = arr.filter(t=>t.priority===pr);
    if (!isNaN(v)) arr = arr.filter(t=>t.villa===v);

    const sort = els.sort.value;
    if (sort==='new') arr.sort((a,b)=>b.createdAt - a.createdAt);
    if (sort==='old') arr.sort((a,b)=>a.createdAt - b.createdAt);
    if (sort==='prio') {
      const rank={Urgent:4, High:3, Medium:2, Low:1};
      arr.sort((a,b)=> (rank[b.priority]-rank[a.priority]) || (b.createdAt-a.createdAt));
    }
    if (sort==='villa') arr.sort((a,b)=> a.villa - b.villa || (b.createdAt-a.createdAt));

    return arr;
  }

  function renderTable(rows){
    els.tbody.innerHTML = rows.map(t=>`
      <tr>
        <td class="id">${t.id}</td>
        <td>${t.villa}</td>
        <td>${chip(t.category)}</td>
        <td>${prioBadge(t.priority)}</td>
        <td>${statusBadge(t.status)}</td>
        <td>
          <div>${escapeHtml(t.requester||'-')}</div>
          <small class="muted">${escapeHtml(t.phone||'')}</small>
        </td>
        <td>${escapeHtml(t.assignedTo||'-')}</td>
        <td><small>${dt(t.createdAt)}</small></td>
        <td><small>${dt(t.updatedAt)}</small></td>
        <td><button class="btn" data-id="${t.id}">Open</button></td>
      </tr>
    `).join('') || `
      <tr><td colspan="10" class="muted" style="text-align:center;padding:30px">No tickets match your filters.</td></tr>
    `;
    // Bind row buttons
    els.tbody.querySelectorAll('button[data-id]').forEach(b=>{
      b.addEventListener('click', ()=> openModal(b.getAttribute('data-id')));
    });
  }

  function openModal(id){
    activeId = id || null;
    els.modal.classList.add('show');
    if (!id){
      els.modalTitle.textContent='New Ticket';
      els.modalSub.textContent='';
      els.ticketInfo.textContent='ID — not assigned yet';
      els.metaLeft.textContent='';
      els.metaRight.textContent='';

      // Defaults
      els.f_villa.value='';
      els.f_requester.value='';
      els.f_phone.value='';
      els.f_category.value=CATEGORIES[0];
      els.f_priority.value='Medium';
      els.f_status.value='Open';
      els.f_assigned.value='';
      els.f_when.value='';
      els.f_desc.value='';
      els.f_note.value='';
      els.notesList.innerHTML = `<div class="note"><small>Notes will appear here after you create the ticket.</small></div>`;
      els.btnDelete.disabled=true;
      els.btnResolve.disabled=true;
      return;
    }
    const t = tickets.find(x=>x.id===id);
    fillModal(t);
  }

  function fillModal(t){
    activeId = t.id;
    els.modalTitle.textContent = `Ticket ${t.id}`;
    els.modalSub.textContent = `${t.category} • Villa ${t.villa} • ${t.priority}`;
    els.ticketInfo.textContent = `ID — ${t.id}`;
    els.metaLeft.textContent = `Created: ${dt(t.createdAt)} • Updated: ${dt(t.updatedAt)}`;
    const due = t.dueAt ? dt(t.dueAt) : 'n/a';
    els.metaRight.textContent = `Due: ${due}`;

    els.f_villa.value=t.villa;
    els.f_requester.value=t.requester||'';
    els.f_phone.value=t.phone||'';
    els.f_category.value=t.category;
    els.f_priority.value=t.priority;
    els.f_status.value=t.status;
    els.f_assigned.value=t.assignedTo||'';
    els.f_when.value = t.preferredAt ? toInputDateTime(t.preferredAt) : '';
    els.f_desc.value=t.description||'';
    els.f_note.value='';

    els.notesList.innerHTML = (t.notes && t.notes.length ? t.notes : [])
      .slice().reverse()
      .map(n=> `<div class="note"><div>${escapeHtml(n.text)}</div><small>${dt(n.at)}</small></div>`)
      .join('') || `<div class="note"><small>No notes yet.</small></div>`;

    els.btnDelete.disabled=false;
    els.btnResolve.disabled = (t.status==='Resolved' || t.status==='Closed');
  }

  function closeModal(){
    els.modal.classList.remove('show');
    activeId=null;
  }

  function saveTicket(){
    // Validation
    const v = parseInt(els.f_villa.value,10);
    if (isNaN(v) || v<1 || v>181){ return toast('Villa number must be between 1 and 181'); }
    const category = els.f_category.value;
    const priority = els.f_priority.value;
    const status = els.f_status.value;
    const desc = (els.f_desc.value||'').trim();
    if (!desc){ return toast('Please add a brief description.'); }

    const payload = {
      villa: v,
      requester: (els.f_requester.value||'').trim(),
      phone: (els.f_phone.value||'').trim(),
      category, priority, status,
      assignedTo: (els.f_assigned.value||'').trim(),
      preferredAt: els.f_when.value ? new Date(els.f_when.value).getTime() : null,
      description: desc
    };

    if (!activeId){
      // Create
      const id = nextId();
      const now = Date.now();
      const t = {
        id,
        ...payload,
        createdAt: now,
        updatedAt: now,
        dueAt: computeDue(now, priority),
        notes: [note('Ticket created')]
      };
      tickets.unshift(t);
      persist();
      render();
      fillModal(t);
      toast(`Ticket ${id} created.`);
      activeId = id;
      return;
    }

    // Update
    const t = tickets.find(x=>x.id===activeId);
    if (!t) return;

    // Track status change in notes
    if (t.status !== payload.status){
      t.notes.push(note(`Status changed from ${t.status} to ${payload.status}`));
    }
    // Track reassignment
    if ((t.assignedTo||'') !== payload.assignedTo){
      t.notes.push(note(`Assigned to: ${payload.assignedTo || '—'}`));
    }

    Object.assign(t, payload);
    t.updatedAt = Date.now();
    if (!t.dueAt) t.dueAt = computeDue(t.createdAt, t.priority);

    persist();
    render();
    fillModal(t);
    toast(`Ticket ${t.id} saved.`);
  }

  function deleteTicket(){
    if (!activeId) return;
    const t = tickets.find(x=>x.id===activeId);
    if (!t) return;
    const ok = confirm(`Delete ticket ${t.id}? This cannot be undone.`);
    if (!ok) return;
    tickets = tickets.filter(x=>x.id!==activeId);
    persist();
    render();
    closeModal();
    toast(`Ticket ${t.id} deleted.`);
  }

  // Helpers
  function nextId(){
    let n = parseInt(localStorage.getItem(KEY_COUNTER)||'0',10);
    n++;
    localStorage.setItem(KEY_COUNTER, String(n));
    const year = new Date().getFullYear();
    return `VIL-${year}-${String(n).padStart(4,'0')}`;
  }
  function computeDue(createdAt, priority){
    const h = SLA_HOURS[priority] || 48;
    return createdAt + h*3600*1000;
  }
  function persist(){
    save(KEY, tickets);
  }
  function exportCSV(){
    const cols=['id','villa','category','priority','status','requester','phone','assignedTo','createdAt','updatedAt','dueAt','preferredAt','description'];
    const head = cols.join(',');
    const rows = tickets.map(t=> cols.map(c=> csv( c.includes('At') ? dt(t[c]) : (t[c]??'') ) ).join(','));
    download('helpdesk_tickets.csv',[head].concat(rows).join('\n'),'text/csv');
  }
  function exportJSON(){
    download('helpdesk_backup.json', JSON.stringify(tickets,null,2), 'application/json');
  }
  function download(name, content, type){
    const blob = new Blob([content], {type});
    const a = document.createElement('a');
    a.href=URL.createObjectURL(blob);
    a.download=name;
    document.body.appendChild(a); a.click(); a.remove();
    setTimeout(()=>URL.revokeObjectURL(a.href), 500);
  }
  function note(text){ return { at: Date.now(), text }; }

  function prioBadge(p){
    const cls = {
      Low:'prio-low',
      Medium:'prio-medium',
      High:'prio-high',
      Urgent:'prio-urgent'
    }[p]||'';
    return `<span class="badge ${cls}">${p}</span>`;
  }
  function statusBadge(s){
    const map = {
      'Open':'status-open',
      'In Progress':'status-progress',
      'On Hold':'status-hold',
      'Resolved':'status-resolved',
      'Closed':'status-closed'
    };
    return `<span class="badge ${map[s]||''}">${s}</span>`;
  }
  function chip(text){ return `<span class="badge" style="background:var(--chip);color:#4338ca;border-color:#e2e8f0">${escapeHtml(text)}</span>`; }

  function dt(ts){ if (!ts) return '—'; const d=new Date(ts); return d.toLocaleString(); }
  function toInputDateTime(ts){
    const d = new Date(ts);
    const pad = n=>String(n).padStart(2,'0');
    return `${d.getFullYear()}-${pad(d.getMonth()+1)}-${pad(d.getDate())}T${pad(d.getHours())}:${pad(d.getMinutes())}`;
  }

  function countBy(arr, key){
    return arr.reduce((a,x)=> (a[x[key]]=(a[x[key]]||0)+1, a), {});
  }

  function seedSample(append=false){
    const now = Date.now();
    const techs = ['Ali','Khalid','Omar','Hassan','Fatima','Sara','—'];
    const issues = [
      ['Electrical','High','Short circuit in kitchen socket'],
      ['Plumbing','Urgent','Water leak under sink'],
      ['AC','High','AC not cooling at night'],
      ['Carpentry','Low','Door hinge squeaking'],
      ['Cleaning','Medium','Common area deep clean request'],
      ['Electrical','Medium','Replace light bulbs in hallway'],
      ['AC','Urgent','AC water dripping'],
      ['Plumbing','Medium','Low water pressure in shower'],
      ['Carpentry','Medium','Wardrobe handle loose'],
      ['Cleaning','Low','Garden waste pickup']
    ];
    const statuses = ['Open','In Progress','On Hold','Resolved','Open','Open','In Progress','Resolved','Open','Open'];

    const sample = issues.map((it, i)=> {
      const [cat, prio, desc] = it;
      const created = now - (i+1)*86400000 + (i*3600000);
      const id = nextId();
      const st = statuses[i];
      return {
        id,
        villa: 1 + (i*9) % 181,
        requester: ['Ahmed','Fatima','Ali','Sara','Maryam','Yousef','Noor','Hamad','Layla','Othman'][i%10],
        phone: `05${Math.floor(10000000+Math.random()*89999999)}`,
        category: cat,
        priority: prio,
        status: st,
        assignedTo: techs[i%techs.length],
        preferredAt: null,
        description: desc,
        createdAt: created,
        updatedAt: created + 7200000,
        dueAt: computeDue(created, prio),
        notes: [note('Ticket created')]
      };
    });

    tickets = append ? sample.concat(tickets) : sample;
    persist();
  }

  // Storage helpers
  function save(key, val){ localStorage.setItem(key, JSON.stringify(val)); }
  function load(key){ const x = localStorage.getItem(key); try{return x?JSON.parse(x):null}catch(e){return null} }

  // Tiny helpers
  function $(sel){ return document.querySelector(sel); }
  function initSelect(el, vals, labels){
    el.innerHTML = (vals||[]).map((v,i)=>`<option value="${escapeAttr(v)}">${escapeHtml(labels?labels[i]:v)}</option>`).join('');
  }
  function escapeHtml(s){
    return String(s).replace(/[&<>"']/g, c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#039;'}[c]));
  }
  function escapeAttr(s){ return String(s).replace(/"/g,'&quot;'); }
  function csv(v){ const s=String(v??''); return `"${s.replace(/"/g,'""')}"`; }

  // Toast
  function toast(msg){
    const div = document.createElement('div');
    div.className='t';
    div.textContent=msg;
    els.toast.appendChild(div);
    setTimeout(()=>{ div.style.opacity='.0'; div.style.transform='translateY(6px)'; }, 2500);
    setTimeout(()=> div.remove(), 3200);
  }

  // Close modal on backdrop click
  els.modal.addEventListener('click', (e)=>{ if (e.target===els.modal) closeModal(); });

})();
</script>
</body>
</html>
