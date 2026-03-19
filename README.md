<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Your Name — Art Portfolio</title>

  <!-- Simple, readable fonts from Google -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">

  <style>
    /* ====== Base ====== */
    :root{
      --bg: #ffffff;
      --card: #f7f7f8;
      --text: #111217;
      --muted: #6b6f76;
      --accent: #222222;
      --glass: rgba(255,255,255,0.6);
      --shadow: 0 6px 18px rgba(12,14,17,0.06);
      --gap: 20px;
    }
    [data-theme="dark"]{
      --bg: #0f1113;
      --card: #121315;
      --text: #edf0f2;
      --muted: #9aa0a6;
      --accent: #f5f5f5;
      --glass: rgba(12,14,16,0.4);
      --shadow: 0 8px 30px rgba(0,0,0,0.6);
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: "Inter", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background: linear-gradient(180deg,var(--bg), color-mix(in srgb, var(--bg) 98%, transparent));
      color:var(--text);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      line-height:1.45;
      padding:32px;
    }

    /* ====== Layout ====== */
    .container{
      max-width:1200px;
      margin:0 auto;
    }

    header{
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:16px;
      margin-bottom:24px;
    }

    .brand{
      display:flex;
      gap:16px;
      align-items:center;
    }
    .logo{
      width:56px;height:56px;border-radius:8px;
      background: linear-gradient(135deg,var(--accent), color-mix(in srgb,var(--accent) 60%, transparent));
      display:flex;align-items:center;justify-content:center;
      color:var(--card);font-family:"Playfair Display",serif;font-weight:700;
      box-shadow:var(--shadow);
      flex:0 0 56px;
    }
    .brand h1{
      margin:0;font-family:"Playfair Display",serif;font-weight:700;font-size:1.1rem;
      letter-spacing:0.02em;
    }
    .brand p{margin:0;font-size:0.9rem;color:var(--muted)}

    .controls{
      display:flex;gap:12px;align-items:center;
    }
    .btn{
      background:transparent;border:1px solid rgba(0,0,0,0.07);padding:9px 12px;border-radius:8px;
      font-size:0.9rem;color:var(--text);cursor:pointer;
      transition:transform .12s ease, background .12s ease, color .12s ease;
      display:inline-flex;align-items:center;gap:8px;
      backdrop-filter: blur(6px);
    }
    [data-theme="dark"] .btn{border-color: rgba(255,255,255,0.06)}
    .btn:active{transform:translateY(1px)}
    .cta{
      background:var(--accent);color:var(--card);box-shadow:var(--shadow);border:none;
    }

    /* Intro / About */
    .hero{
      display:grid;
      grid-template-columns:1fr 340px;
      gap:var(--gap);
      align-items:start;
      margin-bottom:28px;
    }
    .intro{
      padding:22px;border-radius:12px;background:linear-gradient(180deg,var(--card), color-mix(in srgb, var(--card) 98%, transparent));
      box-shadow:var(--shadow);
    }
    .intro h2{font-family:"Playfair Display",serif;margin:0 0 6px 0}
    .intro p{margin:0;color:var(--muted)}
    .bio{
      margin-top:16px;color:var(--muted);font-size:0.95rem;
    }

    .meta{
      padding:18px;border-radius:12px;background:linear-gradient(180deg,var(--glass), transparent);
      box-shadow:var(--shadow);align-self:stretch;
      display:flex;flex-direction:column;gap:12px;
      border:1px solid rgba(0,0,0,0.03);
    }
    .meta .info{font-size:0.95rem}
    .meta .info b{display:block;font-weight:600;margin-bottom:6px}

    /* Gallery */
    .gallery-wrap{margin-top:6px}
    .filters{display:flex;gap:8px;margin-bottom:12px;flex-wrap:wrap}
    .filter{padding:8px 10px;border-radius:999px;background:transparent;border:1px solid rgba(0,0,0,0.06);font-size:0.9rem;cursor:pointer}
    .filter.active{background:var(--accent);color:var(--card);border:none}

    .grid{
      display:grid;
      grid-template-columns:repeat(3,1fr);
      gap:18px;
    }
    .card{
      border-radius:12px;overflow:hidden;background:var(--card);box-shadow:var(--shadow);
      position:relative;
      cursor:pointer;
      min-height:180px;
      display:flex;align-items:center;justify-content:center;
    }
    .card img{width:100%;height:100%;object-fit:cover;display:block;transition:transform .35s ease}
    .card:hover img{transform:scale(1.03)}
    .card .meta-label{
      position:absolute;left:12px;bottom:12px;background:rgba(0,0,0,0.45);color:white;padding:6px 8px;border-radius:8px;font-size:0.85rem;
    }

    /* Lightbox */
    .lightbox{
      position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:linear-gradient(180deg,rgba(2,6,10,0.6),rgba(2,6,10,0.7));z-index:60;
      padding:24px;
    }
    .lightbox.open{display:flex}
    .lightbox .sheet{
      max-width:1100px;width:100%;max-height:92vh;background:transparent;display:flex;gap:18px;align-items:center;
    }
    .lightbox img{max-width:75vw;max-height:86vh;border-radius:10px;box-shadow:0 20px 60px rgba(2,8,12,0.6);object-fit:contain}
    .lightbox .info{
      color:var(--card);max-width:320px;
    }
    .lightbox .info h3{margin:0 0 8px 0;font-family:"Playfair Display",serif}
    .lightbox .info p{margin:0;color:var(--muted)}
    .lightbox .close{
      position:absolute;right:20px;top:20px;background:transparent;border:1px solid rgba(255,255,255,0.12);color:white;padding:8px 10px;border-radius:8px;cursor:pointer;
    }

    /* Footer */
    footer{margin-top:36px;color:var(--muted);font-size:0.92rem;display:flex;justify-content:space-between;align-items:center}

    /* Responsive */
    @media (max-width:1000px){
      .hero{grid-template-columns:1fr}
      .grid{grid-template-columns:repeat(2,1fr)}
      .lightbox img{max-width:66vw}
    }
    @media (max-width:600px){
      body{padding:18px}
      .grid{grid-template-columns:1fr}
      .logo{width:44px;height:44px}
      .brand h1{font-size:1rem}
      .lightbox img{max-width:90vw}
      .lightbox .info{display:none}
    }

  </style>
</head>
<body data-theme="light">
  <div class="container">
    <header>
      <div class="brand">
        <div class="logo" aria-hidden="true">YN</div>
        <div>
          <h1>Your Name</h1>
          <p>Artist — Visuals & Illustration</p>
        </div>
      </div>

      <div class="controls" role="toolbar" aria-label="Site controls">
        <button id="themeToggle" class="btn" title="Toggle light / dark">Toggle theme</button>
        <a class="btn cta" href="#contact" title="Contact">Contact</a>
      </div>
    </header>

    <section class="hero">
      <div class="intro">
        <h2>Selected Works</h2>
        <p class="subtitle">A small selection of recent projects, prints, and experimental pieces.</p>
        <div class="bio">
          <p>Hi — I'm Your Name, a visual artist working across illustration, print, and digital media. This portfolio is kept minimal so the artworks can speak. You can replace the images in the gallery below with your own works; each card contains a title and optional description.</p>
        </div>
      </div>

      <aside class="meta" aria-labelledby="about">
        <div class="info">
          <b id="about">Details</b>
          <div>Location: City, Country</div>
          <div>Mediums: Acrylic, Digital, Mixed Media</div>
          <div>Availability: Commissions open</div>
        </div>
        <div style="margin-top:auto">
          <div style="font-size:0.85rem;color:var(--muted)">Download CV / Press Kit</div>
          <div style="margin-top:8px">
            <a class="btn" href="#" download>Download</a>
          </div>
        </div>
      </aside>
    </section>

    <main class="gallery-wrap" id="galleryWrap">
      <div class="filters" id="filters">
        <button class="filter active" data-filter="*">All</button>
        <button class="filter" data-filter="illustration">Illustration</button>
        <button class="filter" data-filter="print">Print</button>
        <button class="filter" data-filter="experimental">Experimental</button>
      </div>

      <div class="grid" id="gallery">
        <!-- Gallery cards: Replace src, data-title, data-desc, data-category as needed.
             You can add/remove cards. Keep the same structure for automatic behaviors. -->
        <div class="card" data-title="Sea of Quiet" data-desc="Acrylic on canvas — 2024" data-category="print">
          <img src="https://images.unsplash.com/photo-1504198453319-5ce911bafcde?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=3f1f0e1a3c6d5978f2c40fa3e8b2f2d0" alt="Sea of Quiet">
          <div class="meta-label">Print</div>
        </div>

        <div class="card" data-title="Paper Birds" data-desc="Digital illustration — 2023" data-category="illustration">
          <img src="https://images.unsplash.com/photo-1526318472351-c75fcf070d2c?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=3e6b7f0b3b7d6f9a4b2e6bd5a0c8b7f9" alt="Paper Birds">
          <div class="meta-label">Illustration</div>
        </div>

        <div class="card" data-title="Nocturne Study" data-desc="Mixed media study — 2022" data-category="experimental">
          <img src="https://images.unsplash.com/photo-1519681393784-d120267933ba?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=196b558fc0e8d6a0e14e0b1f2b0a0f4a" alt="Nocturne Study">
          <div class="meta-label">Experimental</div>
        </div>

        <div class="card" data-title="Quiet Harbor" data-desc="Limited edition print — 2021" data-category="print">
          <img src="https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=6e9f4876f8d9c8e0b4c1a4b9d3f6aa7b" alt="Quiet Harbor">
          <div class="meta-label">Print</div>
        </div>

        <div class="card" data-title="Hidden City" data-desc="Poster series — 2020" data-category="illustration">
          <img src="https://images.unsplash.com/photo-1518709268805-4e9042af9f23?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=0b9cb6e5f7e8e4a6d2f1f1a5c9a6b8c7" alt="Hidden City">
          <div class="meta-label">Illustration</div>
        </div>

        <div class="card" data-title="Fragment Study" data-desc="Experimental collage — 2024" data-category="experimental">
          <img src="https://images.unsplash.com/photo-1526312426976-95d04a6f5cfd?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=9c2d1f7d5e7a3b4c6d8f9b0a1c2d3e4f" alt="Fragment Study">
          <div class="meta-label">Experimental</div>
        </div>
      </div>
    </main>

    <!-- Lightbox / modal for viewing artwork -->
    <div id="lightbox" class="lightbox" aria-hidden="true" role="dialog" aria-label="Artwork viewer">
      <button class="close" id="lightboxClose" aria-label="Close viewer">Close</button>
      <div class="sheet" role="document">
        <img id="lightboxImage" src="" alt="">
        <div class="info">
          <h3 id="lightboxTitle"></h3>
          <p id="lightboxDesc"></p>
          <div style="margin-top:14px">
            <a id="downloadBtn" class="btn" href="#" download>Download</a>
            <button id="shareBtn" class="btn" style="margin-left:8px">Share</button>
          </div>
        </div>
      </div>
    </div>

    <footer>
      <div>© <span id="year"></span> Your Name</div>
      <div>
        <a class="btn" href="#contact">Contact</a>
      </div>
    </footer>
  </div>

  <script>
    // ====== Configurable area ======
    // Replace the cards in the HTML gallery section above to update artworks.
    // Each .card should have: data-title, data-desc, data-category, and contain an <img src="...">.
    // You can also change the filter buttons (data-filter attribute) to match categories you use.
    // ====== End config area ======

    // Basic interactions: theme toggle, filters, lightbox, simple share & download.
    (function(){
      const body = document.body;
      const themeToggle = document.getElementById('themeToggle');
      const yearEl = document.getElementById('year');
      yearEl.textContent = new Date().getFullYear();

      // Simple theme toggle (persist in localStorage)
      const storedTheme = localStorage.getItem('site-theme') || 'light';
      body.setAttribute('data-theme', storedTheme);

      themeToggle.addEventListener('click', ()=>{
        const next = body.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
        body.setAttribute('data-theme', next);
        localStorage.setItem('site-theme', next);
      });

      // Filters
      const filters = document.getElementById('filters');
      const gallery = document.getElementById('gallery');
      const cards = Array.from(gallery.querySelectorAll('.card'));

      filters.addEventListener('click', (e)=>{
        const btn = e.target.closest('.filter');
        if(!btn) return;
        // set active class
        filters.querySelectorAll('.filter').forEach(f => f.classList.remove('active'));
        btn.classList.add('active');

        const filter = btn.dataset.filter;
        cards.forEach(c => {
          const cat = c.dataset.category || '*';
          if(filter === '*' || filter === cat){
            c.style.display = '';
          } else {
            c.style.display = 'none';
          }
        });
      });

      // Lightbox
      const lightbox = document.getElementById('lightbox');
      const lbImage = document.getElementById('lightboxImage');
      const lbTitle = document.getElementById('lightboxTitle');
      const lbDesc = document.getElementById('lightboxDesc');
      const lbClose = document.getElementById('lightboxClose');
      const downloadBtn = document.getElementById('downloadBtn');
      const shareBtn = document.getElementById('shareBtn');

      function openLightbox(card){
        const img = card.querySelector('img');
        const src = img.src;
        const title = card.dataset.title || '';
        const desc = card.dataset.desc || '';

        lbImage.src = src;
        lbImage.alt = title;
        lbTitle.textContent = title;
        lbDesc.textContent = desc;

        downloadBtn.href = src;
        downloadBtn.setAttribute('download', (title || 'artwork') + '.jpg');

        lightbox.classList.add('open');
        lightbox.setAttribute('aria-hidden','false');
        // trap focus if you want; simple approach: focus close
        lbClose.focus();
      }

      function closeLightbox(){
        lightbox.classList.remove('open');
        lightbox.setAttribute('aria-hidden','true');
        // clear image to free memory in some browsers
        lbImage.src = '';
      }

      cards.forEach(card => {
        card.addEventListener('click', ()=> openLightbox(card));
      });

      lbClose.addEventListener('click', closeLightbox);
      lightbox.addEventListener('click', (e)=>{
        if(e.target === lightbox) closeLightbox();
      });

      document.addEventListener('keydown', (e)=>{
        if(e.key === 'Escape') closeLightbox();
      });

      // Simple Web Share API fallback
      shareBtn.addEventListener('click', async ()=>{
        const url = lbImage.src;
        const title = lbTitle.textContent || document.title;
        try {
          if(navigator.share){
            await navigator.share({title, text: lbDesc.textContent, url});
          } else {
            // fallback: copy image URL to clipboard
            await navigator.clipboard.writeText(url);
            alert('Image URL copied to clipboard (share not supported).');
          }
        } catch (err) {
          console.warn('Share failed', err);
        }
      });

      // Accessibility small enhancement: keyboard navigation for gallery (Enter to open)
      gallery.addEventListener('keydown', (e)=>{
        const card = e.target.closest('.card');
        if(!card) return;
        if(e.key === 'Enter' || e.key === ' ') {
          e.preventDefault();
          openLightbox(card);
        }
      });

      // Make cards focusable
      cards.forEach(c => { c.tabIndex = 0; });

    })();
  </script>
</body>
</html>
