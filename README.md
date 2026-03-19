<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Sample Website — Demo</title>
  <meta name="description" content="A small sample website for testing and demos." />
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <header class="site-header">
    <div class="container header-inner">
      <a class="brand" href="#">SampleSite</a>

      <button id="navToggle" class="nav-toggle" aria-label="Toggle navigation">
        ☰
      </button>

      <nav id="mainNav" class="main-nav" aria-label="Main navigation">
        <ul>
          <li><a href="#hero">Home</a></li>
          <li><a href="#features">Features</a></li>
          <li><a href="#contact">Contact</a></li>
          <li><a href="#about">About</a></li>
        </ul>
      </nav>

      <button id="themeToggle" class="theme-toggle" aria-label="Toggle theme">🌙</button>
    </div>
  </header>

  <main>
    <section id="hero" class="hero">
      <div class="container hero-inner">
        <div class="hero-text">
          <h1>Welcome to the Sample Website</h1>
          <p>A simple responsive site you can use to test GitHub Pages or try out web templates.</p>
          <p>
            <a class="btn" href="#contact">Get in touch</a>
            <a class="btn ghost" href="#features">See features</a>
          </p>
        </div>
        <div class="hero-image">
          <!-- Replace the image URL with one in your repo if you add assets/hero.jpg -->
          <img src="https://images.unsplash.com/photo-1506765515384-028b60a970df?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder" alt="Hero illustration" />
        </div>
      </div>
    </section>

    <section id="features" class="container features">
      <h2>Features</h2>
      <div class="grid">
        <article class="card">
          <h3>Responsive Layout</h3>
          <p>Looks good on phones, tablets, and desktops with a clean, flexible layout.</p>
        </article>

        <article class="card">
          <h3>Theme Switcher</h3>
          <p>Light and dark mode toggles preserved in localStorage for convenience.</p>
        </article>

        <article class="card">
          <h3>Accessible Nav</h3>
          <p>Keyboard-friendly navigation and ARIA attributes for better accessibility.</p>
        </article>
      </div>
    </section>

    <section id="about" class="container about">
      <h2>About this Demo</h2>
      <p>This repository is intended as a minimal, well-commented starting point for static websites. Feel free to modify files, add images under an assets/ folder, and enable GitHub Pages to publish.</p>
    </section>

    <section id="contact" class="container contact">
      <h2>Contact Us</h2>
      <form id="contactForm" class="form" novalidate>
        <div class="form-row">
          <label for="name">Name</label>
          <input id="name" name="name" required minlength="2" />
          <span class="error" aria-live="polite"></span>
        </div>

        <div class="form-row">
          <label for="email">Email</label>
          <input id="email" name="email" type="email" required />
          <span class="error" aria-live="polite"></span>
        </div>

        <div class="form-row">
          <label for="message">Message</label>
          <textarea id="message" name="message" rows="5" required minlength="10"></textarea>
          <span class="error" aria-live="polite"></span>
        </div>

        <div class="form-row">
          <button type="submit" class="btn">Send Message</button>
          <button type="reset" class="btn ghost">Reset</button>
        </div>

        <div id="formFeedback" class="form-feedback" role="status" aria-live="polite"></div>
      </form>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container">
      <p>© <span id="year"></span> SampleSite — Built for testing and demos</p>
    </div>
  </footer>

  <script src="script.js" defer></script>
</body>
</html>
:root{
  --bg: #ffffff;
  --text: #111827;
  --muted: #6b7280;
  --accent: #2563eb;
  --card: #f8fafc;
  --radius: 10px;
  --max-width: 1100px;
}

[data-theme="dark"]{
  --bg: #0b1220;
  --text: #e6eef8;
  --muted: #9aa6b2;
  --accent: #60a5fa;
  --card: #071021;
}

*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0;
  font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
  background:var(--bg);
  color:var(--text);
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
  line-height:1.5;
}

.container{
  width:90%;
  max-width:var(--max-width);
  margin:0 auto;
}

/* Header */
.site-header{
  border-bottom:1px solid rgba(0,0,0,0.06);
  background:linear-gradient(180deg, rgba(255,255,255,0.6), transparent);
  position:sticky;
  top:0;
  z-index:40;
  backdrop-filter: blur(6px);
}
.header-inner{
  display:flex;
  align-items:center;
  gap:1rem;
  padding:1rem 0;
}
.brand{
  font-weight:700;
  color:var(--text);
  text-decoration:none;
  font-size:1.1rem;
}
.nav-toggle{
  display:none;
  background:none;
  border:0;
  font-size:1.4rem;
  cursor:pointer;
}
.main-nav ul{
  list-style:none;
  margin:0;
  padding:0;
  display:flex;
  gap:0.75rem;
}
.main-nav a{
  color:var(--muted);
  text-decoration:none;
  padding:0.5rem .6rem;
  border-radius:8px;
}
.main-nav a:hover{ color:var(--text); background:rgba(0,0,0,0.03) }

.theme-toggle{
  margin-left:auto;
  background:none;
  border:0;
  font-size:1.1rem;
  cursor:pointer;
}

/* Hero */
.hero{
  padding:3rem 0;
}
.hero-inner{
  display:flex;
  gap:2rem;
  align-items:center;
}
.hero-text{flex:1}
.hero-text h1{margin:0 0 .5rem; font-size:clamp(1.6rem, 3vw, 2.4rem)}
.hero-text p{color:var(--muted)}
.hero-image{flex:1; text-align:right}
.hero-image img{max-width:100%; border-radius:12px; box-shadow: 0 6px 18px rgba(2,6,23,0.08)}

/* Buttons */
.btn{
  display:inline-block;
  padding:.6rem .9rem;
  background:var(--accent);
  color:white;
  border-radius:8px;
  text-decoration:none;
  border:0;
  cursor:pointer;
}
.btn.ghost{
  background:transparent;
  color:var(--accent);
  border:1px solid rgba(37,99,235,0.12);
}

/* Features */
.features{padding:2rem 0}
.grid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:1rem;
}
.card{
  background:var(--card);
  border-radius:var(--radius);
  padding:1rem;
  box-shadow: 0 4px 12px rgba(2,6,23,0.04);
}

/* About & Contact */
.about{padding:1.5rem 0}
.contact{padding:2rem 0}
.form-row{margin-bottom:0.75rem}
input,textarea{
  width:100%;
  padding:.6rem .75rem;
  border-radius:8px;
  border:1px solid rgba(0,0,0,0.08);
  background:transparent;
  color:var(--text);
}
.error{color:#ef4444; font-size:.85rem; display:block; margin-top:.25rem; min-height:1em}
.form-feedback{margin-top:.6rem; color:var(--muted)}

/* Footer */
.site-footer{
  border-top:1px solid rgba(0,0,0,0.06);
  padding:1rem 0;
  margin-top:2rem;
  color:var(--muted);
}

/* Responsive */
@media (max-width:900px){
  .hero-inner{flex-direction:column-reverse; text-align:center}
  .hero-image{text-align:center}
  .grid{grid-template-columns:repeat(2,1fr)}
}

@media (max-width:700px){
  .nav-toggle{display:inline-block}
  .main-nav{position:absolute; right:0; top:64px; background:var(--bg); border-radius:10px; box-shadow:0 8px 28px rgba(2,6,23,0.12); transform-origin:top right; display:none; padding:0.5rem}
  .main-nav ul{flex-direction:column}
  .main-nav.show{display:block}
  .grid{grid-template-columns:1fr}
}
// Lightweight JS for interactivity: menu toggle, form validation, theme
document.addEventListener('DOMContentLoaded', function () {
  // DOM refs
  const navToggle = document.getElementById('navToggle');
  const mainNav = document.getElementById('mainNav');
  const themeToggle = document.getElementById('themeToggle');
  const yearEl = document.getElementById('year');
  const contactForm = document.getElementById('contactForm');
  const formFeedback = document.getElementById('formFeedback');

  // set year
  if (yearEl) yearEl.textContent = new Date().getFullYear();

  // nav toggle for small screens
  if (navToggle && mainNav) {
    navToggle.addEventListener('click', function () {
      mainNav.classList.toggle('show');
      const expanded = navToggle.getAttribute('aria-expanded') === 'true';
      navToggle.setAttribute('aria-expanded', (!expanded).toString());
    });
  }

  // theme toggle (localStorage)
  const userPref = localStorage.getItem('site-theme');
  if (userPref) {
    document.documentElement.setAttribute('data-theme', userPref);
    themeToggle.textContent = userPref === 'dark' ? '☀️' : '🌙';
  }

  themeToggle.addEventListener('click', function () {
    const current = document.documentElement.getAttribute('data-theme');
    const next = current === 'dark' ? 'light' : 'dark';
    if (next === 'dark') {
      document.documentElement.setAttribute('data-theme', 'dark');
      themeToggle.textContent = '☀️';
      localStorage.setItem('site-theme', 'dark');
    } else {
      document.documentElement.removeAttribute('data-theme');
      themeToggle.textContent = '🌙';
      localStorage.setItem('site-theme', 'light');
    }
  });

  // Simple form validation & simulated submit
  function showError(input, message) {
    const row = input.closest('.form-row');
    if (!row) return;
    const err = row.querySelector('.error');
    err.textContent = message || '';
    input.setAttribute('aria-invalid', !!message);
  }

  contactForm.addEventListener('submit', function (e) {
    e.preventDefault();
    formFeedback.textContent = '';

    const name = contactForm.name;
    const email = contactForm.email;
    const message = contactForm.message;

    let ok = true;
    // Name
    if (!name.value || name.value.trim().length < 2) {
      showError(name, 'Please enter your name (2+ characters).');
      ok = false;
    } else showError(name, '');

    // Email
    if (!email.value || !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email.value)) {
      showError(email, 'Please enter a valid email address.');
      ok = false;
    } else showError(email, '');

    // Message
    if (!message.value || message.value.trim().length < 10) {
      showError(message, 'Please enter a message (10+ characters).');
      ok = false;
    } else showError(message, '');

    if (!ok) {
      formFeedback.textContent = 'Please fix the errors above and try again.';
      return;
    }

    // Simulate sending
    const submitBtn = contactForm.querySelector('button[type="submit"]');
    submitBtn.disabled = true;
    submitBtn.textContent = 'Sending...';

    setTimeout(() => {
      submitBtn.disabled = false;
      submitBtn.textContent = 'Send Message';
      formFeedback.textContent = 'Thanks — your message was received (simulated).';
      contactForm.reset();
    }, 1100);
  });
});
