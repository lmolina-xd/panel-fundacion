<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Panel — Fundación Scherbovsky</title>
  <style>
    :root {
      --bg: #f0f4f8; --card: #fff;
      --blue: #2563eb; --green: #059669; --purple: #7c3aed;
      --text: #1e293b; --muted: #64748b; --border: #e2e8f0;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: 'Segoe UI', system-ui, sans-serif; background: var(--bg); color: var(--text); min-height: 100vh; }
    header { background: #fff; border-bottom: 1px solid var(--border); padding: 18px 36px; display: flex; align-items: center; gap: 14px; flex-wrap: wrap; }
    .logo { width: 42px; height: 42px; background: linear-gradient(135deg,#2563eb,#7c3aed); border-radius: 10px; display:flex; align-items:center; justify-content:center; color:#fff; font-weight:800; font-size:17px; flex-shrink:0; }
    header h1 { font-size: 1.15rem; font-weight: 700; }
    header p { font-size: 0.8rem; color: var(--muted); }
    .search { margin-left: auto; }
    .search input { border: 1px solid var(--border); border-radius: 8px; padding: 8px 13px; font-size: 0.84rem; outline: none; width: 210px; }
    .search input:focus { border-color: var(--blue); }
    main { max-width: 1080px; margin: 0 auto; padding: 32px 20px; }
    .section { margin-bottom: 38px; }
    .sec-head { display: flex; align-items: center; gap: 10px; margin-bottom: 16px; }
    .sec-ico { width: 30px; height: 30px; border-radius: 8px; display:flex; align-items:center; justify-content:center; font-size:15px; }
    .sec-ico.t { background:#dbeafe; } .sec-ico.s { background:#d1fae5; } .sec-ico.f { background:#ede9fe; }
    .sec-head h2 { font-size: .95rem; font-weight: 700; }
    .badge { font-size:.75rem; background:var(--bg); color:var(--muted); border:1px solid var(--border); border-radius:20px; padding:2px 9px; }
    .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(230px, 1fr)); gap: 12px; }
    .card { background: var(--card); border: 1px solid var(--border); border-radius: 11px; padding: 16px 18px; text-decoration: none; color: inherit; display:flex; align-items:flex-start; gap:12px; transition: transform .15s, box-shadow .15s, border-color .15s; }
    .card:hover { transform: translateY(-2px); box-shadow: 0 8px 22px rgba(0,0,0,.09); }
    .card.t:hover { border-color: var(--blue); } .card.s:hover { border-color: var(--green); } .card.f:hover { border-color: var(--purple); }
    .c-ico { width:36px; height:36px; border-radius:9px; display:flex; align-items:center; justify-content:center; font-size:17px; flex-shrink:0; }
    .card.t .c-ico { background:#dbeafe; } .card.s .c-ico { background:#d1fae5; } .card.f .c-ico { background:#ede9fe; }
    .c-body { flex:1; min-width:0; }
    .c-title { font-size:.88rem; font-weight:600; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; margin-bottom:3px; }
    .c-desc { font-size:.76rem; color:var(--muted); line-height:1.4; }
    .c-arr { color:var(--border); font-size:13px; margin-top:2px; flex-shrink:0; transition:color .15s; }
    .card:hover .c-arr { color:var(--muted); }
    .hidden { display:none !important; }
    footer { text-align:center; padding:28px; font-size:.76rem; color:var(--muted); }
  </style>
</head>
<body>
<header>
  <div class="logo">FS</div>
  <div><h1>Fundación Scherbovsky</h1><p>Panel de accesos · documentos internos</p></div>
  <div class="search"><input id="q" type="text" placeholder="Buscar…" oninput="filter()" /></div>
</header>

<main>
  <div class="section" id="sec-t">
    <div class="sec-head"><div class="sec-ico t">📊</div><h2>Trackers</h2><span class="badge" id="cnt-t"></span></div>
    <div class="grid" id="g-t"></div>
  </div>
  <div class="section" id="sec-s">
    <div class="sec-head"><div class="sec-ico s">📋</div><h2>Planillas</h2><span class="badge" id="cnt-s"></span></div>
    <div class="grid" id="g-s"></div>
  </div>
  <div class="section" id="sec-f">
    <div class="sec-head"><div class="sec-ico f">📝</div><h2>Formularios</h2><span class="badge" id="cnt-f"></span></div>
    <div class="grid" id="g-f"></div>
  </div>
</main>
<footer>Fundación Scherbovsky · Uso interno</footer>

<script>
// ── COMPLETÁ ESTA LISTA CON NOMBRES Y LINKS REALES ──────────────────
const docs = [
  // Trackers  → type:"t"
  { type:"t", icon:"🫁", title:"Tracker Respiratorio",     desc:"Seguimiento de pacientes respiratorios",  url:"#" },
  { type:"t", icon:"💊", title:"Tracker Medicación",       desc:"Control de medicación activa",            url:"#" },
  { type:"t", icon:"📅", title:"Tracker Turnos",           desc:"Estado y asistencia de turnos",           url:"#" },
  { type:"t", icon:"🩺", title:"Tracker Estudios",         desc:"Estudios pendientes y realizados",        url:"#" },
  { type:"t", icon:"📈", title:"Tracker Evolución",        desc:"Evolución clínica por paciente",          url:"#" },

  // Planillas → type:"s"
  { type:"s", icon:"👥", title:"Pacientes Activos",        desc:"Base de datos de pacientes activos",      url:"#" },
  { type:"s", icon:"🏥", title:"Internaciones",            desc:"Registro de internaciones",               url:"#" },
  { type:"s", icon:"📊", title:"Estadísticas Mensuales",   desc:"Resumen mensual de atenciones",           url:"#" },
  { type:"s", icon:"💰", title:"Facturación",              desc:"Control de facturación y obras sociales", url:"#" },
  { type:"s", icon:"🔬", title:"Laboratorio",              desc:"Historial de resultados",                 url:"#" },

  // Formularios → type:"f"
  { type:"f", icon:"📋", title:"Ingreso de Paciente",      desc:"Alta y datos iniciales",                  url:"#" },
  { type:"f", icon:"🩻", title:"Solicitud de Estudio",     desc:"Pedido de estudios complementarios",      url:"#" },
  { type:"f", icon:"✍️", title:"Consentimiento Informado", desc:"Formulario de consentimiento",            url:"#" },
  { type:"f", icon:"📞", title:"Seguimiento Telefónico",   desc:"Registro de contacto con paciente",       url:"#" },
];
// ────────────────────────────────────────────────────────────────────

function build() {
  ["t","s","f"].forEach(tp => {
    const items = docs.filter(d => d.type === tp);
    document.getElementById("cnt-"+tp).textContent = items.length;
    document.getElementById("g-"+tp).innerHTML = items.map(d =>
      `<a class="card ${tp}" href="${d.url}" target="_blank" data-k="${(d.title+d.desc).toLowerCase()}">
        <div class="c-ico">${d.icon}</div>
        <div class="c-body"><div class="c-title">${d.title}</div><div class="c-desc">${d.desc}</div></div>
        <div class="c-arr">↗</div>
      </a>`
    ).join("");
  });
}

function filter() {
  const q = document.getElementById("q").value.toLowerCase().trim();
  document.querySelectorAll(".card").forEach(c =>
    c.classList.toggle("hidden", !!q && !c.dataset.k.includes(q))
  );
  ["t","s","f"].forEach(tp => {
    const vis = document.querySelectorAll(`#g-${tp} .card:not(.hidden)`).length;
    document.getElementById("sec-"+tp).classList.toggle("hidden", vis === 0);
  });
}

build();
</script>
</body>
</html>
