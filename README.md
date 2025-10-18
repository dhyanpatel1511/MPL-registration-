<!doctype html>

<html lang="hi">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>MPL — Mangalam Premier League | Registration</title>
  <style>
    :root{--bg:#061325;--card:#0b2340;--accent:#f9c74f;--muted:#cbd5e1}
    *{box-sizing:border-box;font-family:Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial}
    body{margin:0;background:linear-gradient(180deg, #0a1b2b 0%, #05202b 100%);color:#fff;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:24px}
    .wrap{width:100%;max-width:980px}
    header{display:flex;gap:16px;align-items:center}
    .logo{width:86px;height:86px;border-radius:8px;background:linear-gradient(135deg,#f6b042,#f26c4f);display:flex;align-items:center;justify-content:center;color:#05202b;font-weight:800;font-size:20px;box-shadow:0 6px 18px rgba(0,0,0,0.45)}
    h1{margin:0;font-size:28px}
    p.lead{color:var(--muted);margin:6px 0 18px}.grid{display:grid;grid-template-columns:1fr 380px;gap:18px}
.card{background:rgba(255,255,255,0.03);padding:18px;border-radius:12px;box-shadow:0 8px 30px rgba(2,6,23,0.6)}

.match-info{display:flex;flex-direction:column;gap:8px}
.time{font-weight:700;color:var(--accent);font-size:18px}
ul.rules{margin:10px 0 0;padding-left:18px;color:var(--muted)}

form{display:flex;flex-direction:column;gap:10px}
label{font-size:13px;color:var(--muted)}
input,select,button,textarea{padding:10px;border-radius:8px;border:0;background:rgba(255,255,255,0.04);color:#fff;outline:none}
input::placeholder{color:#89a0b8}
.row{display:flex;gap:8px}
.row .half{flex:1}
button{cursor:pointer;background:var(--accent);color:#05202b;font-weight:700;border-radius:10px;padding:12px}
.meta{font-size:13px;color:#9fb0c3}
.footer-note{font-size:12px;color:#94a6b6;margin-top:8px}

/* cricket interior styling */
.stadium{background-image:linear-gradient(180deg, rgba(0,0,0,0.25), rgba(0,0,0,0.55)), url('https://images.unsplash.com/photo-1517649763962-0c623066013b?auto=format&fit=crop&w=1600&q=60');background-size:cover;background-position:center;border-radius:12px;padding:18px}
.stadium .title{font-size:18px;font-weight:800}

@media (max-width:900px){.grid{grid-template-columns:1fr}.logo{width:64px;height:64px}.stadium{display:block}}

  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="logo">MPL</div>
      <div>
        <h1>MPL — Mangalam Premier League</h1>
        <p class="lead">Cricket tournament registration • Match time: <strong>08:30 — 11:30</strong></p>
      </div>
    </header><div style="height:18px"></div>

<div class="grid">
  <section class="card">
    <div class="stadium">
      <div class="title">Join the action — MPL Mangalam Premier League</div>
      <p class="meta">Entry fee: ₹20 • Please arrive on time</p>
    </div>

    <div style="height:12px"></div>

    <div class="match-info">
      <div class="time">Match time: 08:30 — 11:30</div>
      <div class="meta">Short rules:</div>
      <ul class="rules">
        <li>Sab apne time pe aa jana.</li>
        <li>Entry fee ₹20 (paise collection offline by organizers).</li>
      </ul>
    </div>

    <div style="height:12px"></div>
    <div class="footer-note">Note: Ye link sirf registration ke liye hai. Paise aap organizers se offline collect kar lena.</div>
  </section>

  <aside class="card">
    <h3 style="margin:0 0 8px 0">Register now</h3>

    <!-- IMPORTANT: Replace ACTION_URL_HERE with your form endpoint (Formspree / Getform / Google Apps Script / your server) -->
    <form id="regForm" method="POST" action="ACTION_URL_HERE" onsubmit="return onSubmit(event)">
      <label for="name">Naam</label>
      <input id="name" name="name" placeholder="Aapka poora naam" required>

      <label for="phone">Phone (WhatsApp)</label>
      <input id="phone" name="phone" placeholder="+91 9XXXXXXXXX" required>

      <label for="team">Team (agar individual ho to leave blank)</label>
      <input id="team" name="team" placeholder="Team name">

      <label for="notes">Kuch note (optional)</label>
      <textarea id="notes" name="notes" rows="3" placeholder="Extra info agar ho"></textarea>

      <div class="row">
        <div class="half">
          <label>Match</label>
          <input value="MPL — Mangalam Premier League" disabled>
        </div>
        <div class="half">
          <label>Entry fee</label>
          <input value="₹20" disabled>
        </div>
      </div>

      <button type="submit">Register</button>
    </form>

    <div id="message" style="margin-top:10px;font-size:13px;color:#cfe8ff;display:none"></div>

    <div style="height:10px"></div>
    <div style="font-size:12px;color:#9fb0c3">Tip: Agar aapko backend nahi banana to Formspree (formspree.io) ya Getform.io par free form bana ke <strong>action</strong> URL yahan paste kar do — submissions seedhe aapke email ya dashboard par aa jayenge.</div>
  </aside>
</div>

  </div>  <script>
    function onSubmit(e){
      // basic client-side validation & nice UX
      e.preventDefault();
      const form = document.getElementById('regForm');
      const name = form.name.value.trim();
      const phone = form.phone.value.trim();
      if(!name || !phone){
        showMsg('Naam aur phone bharna zaruri hai');
        return false;
      }

      const action = form.getAttribute('action');
      if(!action || action.includes('ACTION_URL_HERE')){
        // fallback: open user's email client with filled content (mailto) — helpful if no backend
        const subject = encodeURIComponent('MPL Registration — ' + name);
        const body = encodeURIComponent('Name: '+name+'\nPhone: '+phone+'\nTeam: '+form.team.value+'\nNotes: '+form.notes.value+'\nMatch: MPL Mangalam Premier League\nEntry fee: ₹20');
        window.location.href = 'mailto:organizer@example.com?subject='+subject+'&body='+body;
        showMsg('Aapke device ka email client khul jaayega — ya phir form action set karen (Formspree/Getform)');
        return false;
      }

      // If action exists, submit normally (will redirect or show response based on endpoint)
      showMsg('Sending registration...');
      form.submit();
      return true;
    }

    function showMsg(t){
      const el = document.getElementById('message');
      el.style.display = 'block';
      el.textContent = t;
    }
  </script></body>
</html>
