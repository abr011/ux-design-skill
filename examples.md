# Full Page Examples

Complete HTML templates demonstrating GitLab Pajamas design tokens and forgiving software patterns in context.

---

## Login Form

A simple login page using design tokens.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login</title>
  <style>
    :root {
      --color-background: #fafafa;
      --color-text: #1f2937;
      --color-text-muted: #9ca3af;
      --color-primary: #6366f1;
      --color-primary-hover: #4f46e5;
      --color-border-strong: #d1d5db;
      --space-1: 4px;
      --space-2: 8px;
      --space-3: 12px;
      --space-4: 16px;
      --space-5: 24px;
      --space-6: 32px;
      --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      --font-size-sm: 14px;
      --font-size-md: 16px;
      --radius-md: 6px;
    }

    *, *::before, *::after { box-sizing: border-box; }

    body {
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      line-height: 1.5;
      color: var(--color-text);
      background: var(--color-background);
      margin: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
    }

    main {
      width: 100%;
      max-width: 400px;
      padding: var(--space-6);
    }

    h1 {
      margin: 0 0 var(--space-6) 0;
      font-size: 24px;
    }

    .form-label {
      display: block;
      margin-bottom: var(--space-4);
    }

    .form-label-text {
      display: block;
      font-size: var(--font-size-sm);
      font-weight: 500;
      margin-bottom: var(--space-1);
    }

    .form-input {
      display: block;
      width: 100%;
      padding: var(--space-2) var(--space-3);
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      color: var(--color-text);
      background: white;
      border: 1px solid var(--color-border-strong);
      border-radius: var(--radius-md);
    }

    .form-input:focus {
      outline: none;
      border-color: var(--color-primary);
      box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.15);
    }

    .form-input::placeholder {
      color: var(--color-text-muted);
    }

    .btn {
      display: block;
      width: 100%;
      padding: var(--space-3) var(--space-4);
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      font-weight: 500;
      background: var(--color-primary);
      color: white;
      border: none;
      border-radius: var(--radius-md);
      cursor: pointer;
    }

    .btn:hover {
      background: var(--color-primary-hover);
    }

    .login-footer {
      text-align: center;
      margin-top: var(--space-5);
      font-size: var(--font-size-sm);
    }

    .login-footer a {
      color: var(--color-primary);
    }
  </style>
</head>
<body>
  <main>
    <h1>Sign In</h1>

    <form>
      <label class="form-label">
        <span class="form-label-text">Email</span>
        <input type="email" class="form-input" name="email" placeholder="you@example.com" required>
      </label>

      <label class="form-label">
        <span class="form-label-text">Password</span>
        <input type="password" class="form-input" name="password" placeholder="Your password" required>
      </label>

      <button type="submit" class="btn">Sign In</button>
    </form>

    <p class="login-footer">
      Don't have an account? <a href="#">Sign up</a>
    </p>
  </main>
</body>
</html>
```

---

## Registration with Steps

Multi-step registration form with step indicator.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Registration</title>
  <style>
    :root {
      --color-background: #fafafa;
      --color-background-subtle: #f0f0f0;
      --color-text: #1f2937;
      --color-text-muted: #9ca3af;
      --color-primary: #6366f1;
      --color-primary-hover: #4f46e5;
      --color-border-strong: #d1d5db;
      --color-danger: #ef4444;
      --space-1: 4px;
      --space-2: 8px;
      --space-3: 12px;
      --space-4: 16px;
      --space-5: 24px;
      --space-6: 32px;
      --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      --font-size-sm: 14px;
      --font-size-md: 16px;
      --radius-md: 6px;
    }

    *, *::before, *::after { box-sizing: border-box; }

    body {
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      line-height: 1.5;
      color: var(--color-text);
      background: var(--color-background);
      margin: 0;
    }

    .container {
      max-width: 600px;
      margin: 0 auto;
      padding: var(--space-5);
    }

    .steps {
      display: flex;
      align-items: center;
      gap: var(--space-6);  /* Whitespace separation, no connectors */
      padding: var(--space-5) 0;
    }

    .step {
      display: flex;
      align-items: center;
      gap: var(--space-2);
    }

    .step-number {
      width: 24px;
      height: 24px;
      border-radius: 50%;
      background: var(--color-background-subtle);
      color: var(--color-text-muted);
      font-size: 13px;
      font-weight: 600;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .step-label {
      font-size: 14px;
      color: var(--color-text-muted);
    }

    .step.active .step-number {
      background: var(--color-text);
      color: white;
    }

    .step.active .step-label {
      color: var(--color-text);
      font-weight: 600;
    }

    h1 {
      margin: 0 0 var(--space-6) 0;
      font-size: 24px;
    }

    form {
      max-width: 400px;
    }

    .form-label {
      display: block;
      margin-bottom: var(--space-4);
    }

    .form-label-text {
      display: block;
      font-size: var(--font-size-sm);
      font-weight: 500;
      margin-bottom: var(--space-1);
    }

    .form-input {
      display: block;
      width: 100%;
      padding: var(--space-2) var(--space-3);
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      color: var(--color-text);
      background: white;
      border: 1px solid var(--color-border-strong);
      border-radius: var(--radius-md);
    }

    .form-input:focus {
      outline: none;
      border-color: var(--color-primary);
      box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.15);
    }

    .form-input-error {
      border-color: var(--color-danger);
    }

    .form-error {
      display: block;
      font-size: var(--font-size-sm);
      color: var(--color-danger);
      margin-top: var(--space-1);
    }

    .btn {
      padding: var(--space-3) var(--space-5);
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      font-weight: 500;
      background: var(--color-primary);
      color: white;
      border: none;
      border-radius: var(--radius-md);
      cursor: pointer;
    }

    .btn:hover {
      background: var(--color-primary-hover);
    }
  </style>
</head>
<body>
  <main class="container">
    <div class="steps">
      <div class="step active">
        <span class="step-number">1</span>
        <span class="step-label">Basic Info</span>
      </div>
      <div class="step">
        <span class="step-number">2</span>
        <span class="step-label">Verification</span>
      </div>
    </div>

    <h1>Basic Information</h1>

    <form>
      <label class="form-label">
        <span class="form-label-text">Full Name</span>
        <input type="text" class="form-input" name="name" placeholder="John Smith">
      </label>

      <label class="form-label">
        <span class="form-label-text">Email</span>
        <input type="email" class="form-input form-input-error" name="email" value="john@" aria-invalid="true" aria-describedby="email-error">
        <small id="email-error" class="form-error">Please check the @ symbol and domain (e.g., name@example.com)</small>
      </label>

      <label class="form-label">
        <span class="form-label-text">Phone</span>
        <input type="tel" class="form-input" name="phone" placeholder="+1 555 123 4567">
      </label>

      <button type="submit" class="btn">Continue</button>
    </form>
  </main>
</body>
</html>
```

---

## Address Form with Input Widths

Demonstrating proper input width sizing based on expected content.

```html
<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Adresa</title>
  <style>
    :root {
      --color-background: #fafafa;
      --color-text: #1f2937;
      --color-text-secondary: #6b7280;
      --color-text-muted: #9ca3af;
      --color-primary: #6366f1;
      --color-primary-hover: #4f46e5;
      --color-border-strong: #d1d5db;
      --space-1: 4px;
      --space-2: 8px;
      --space-3: 12px;
      --space-4: 16px;
      --space-5: 24px;
      --space-6: 32px;
      --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      --font-size-sm: 14px;
      --font-size-md: 16px;
      --radius-md: 6px;
    }

    *, *::before, *::after { box-sizing: border-box; }

    body {
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      line-height: 1.5;
      color: var(--color-text);
      background: var(--color-background);
      margin: 0;
    }

    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: var(--space-6);
    }

    h1 {
      margin: 0 0 var(--space-2) 0;
      font-size: 24px;
    }

    .subtitle {
      color: var(--color-text-secondary);
      margin: 0 0 var(--space-6) 0;
    }

    .form-row {
      display: flex;
      gap: var(--space-4);
      flex-wrap: wrap;
      margin-bottom: var(--space-4);
    }

    .form-label {
      display: block;
    }

    .form-label-text {
      display: block;
      font-size: var(--font-size-sm);
      font-weight: 500;
      margin-bottom: var(--space-1);
    }

    .form-hint {
      display: block;
      font-size: 12px;
      color: var(--color-text-muted);
      margin-top: var(--space-1);
    }

    .form-input {
      display: block;
      width: 100%;
      padding: var(--space-2) var(--space-3);
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      color: var(--color-text);
      background: white;
      border: 1px solid var(--color-border-strong);
      border-radius: var(--radius-md);
    }

    .form-input:focus {
      outline: none;
      border-color: var(--color-primary);
      box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.15);
    }

    .form-input::placeholder {
      color: var(--color-text-muted);
    }

    /* Input Width Utilities - width on INPUT, not label */
    .input-xs .form-input { width: 100px; }   /* PSČ, CVV */
    .input-sm .form-input { width: 180px; }   /* dates, phone, IČO */
    .input-md .form-input { width: 320px; }   /* names, emails */

    /* Keep short labels on one line */
    .form-label-text-nowrap { white-space: nowrap; }

    @media (max-width: 576px) {
      .input-xs .form-input,
      .input-sm .form-input,
      .input-md .form-input {
        width: 100%;
      }
      .form-row {
        flex-direction: column;
      }
    }

    .btn-group {
      display: flex;
      gap: var(--space-2);
      margin-top: var(--space-6);
    }

    .btn {
      padding: var(--space-3) var(--space-5);
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      font-weight: 500;
      border-radius: var(--radius-md);
      cursor: pointer;
      border: 1px solid transparent;
    }

    .btn-primary {
      background: var(--color-primary);
      color: white;
    }

    .btn-primary:hover {
      background: var(--color-primary-hover);
    }

    .btn-secondary {
      background: white;
      color: var(--color-text);
      border-color: var(--color-border-strong);
    }

    .btn-secondary:hover {
      background: var(--color-background);
    }
  </style>
</head>
<body>
  <main class="container">
    <h1>Dodací adresa</h1>
    <p class="subtitle">Kam máme objednávku doručit?</p>

    <form>
      <!-- Full name: medium width -->
      <div class="form-row">
        <label class="form-label input-md">
          <span class="form-label-text">Jméno a příjmení</span>
          <input type="text" class="form-input" name="name" placeholder="Jan Novák">
        </label>
      </div>

      <!-- Street: medium, House number: extra small -->
      <div class="form-row">
        <label class="form-label input-md">
          <span class="form-label-text">Ulice</span>
          <input type="text" class="form-input" name="street" placeholder="Hlavní">
        </label>
        <label class="form-label input-xs">
          <span class="form-label-text form-label-text-nowrap">Č.p.</span>
          <input type="text" class="form-input" name="house_number" placeholder="123">
        </label>
      </div>

      <!-- City: small, Postal code: extra small -->
      <div class="form-row">
        <label class="form-label input-sm">
          <span class="form-label-text">Město</span>
          <input type="text" class="form-input" name="city" placeholder="Praha">
        </label>
        <label class="form-label input-xs">
          <span class="form-label-text form-label-text-nowrap">PSČ</span>
          <input type="text" class="form-input" name="zip" inputmode="numeric" placeholder="110 00">
          <small class="form-hint">5 číslic</small>
        </label>
      </div>

      <!-- Phone: small -->
      <div class="form-row">
        <label class="form-label input-sm">
          <span class="form-label-text">Telefon</span>
          <input type="tel" class="form-input" name="phone" placeholder="+420 123 456 789">
          <small class="form-hint">Pro kurýra</small>
        </label>
      </div>

      <div class="btn-group">
        <button type="button" class="btn btn-secondary">Zpět</button>
        <button type="submit" class="btn btn-primary">Pokračovat k platbě</button>
      </div>
    </form>
  </main>
</body>
</html>
```

---

## Dashboard with Cards

A dashboard layout using card grid instead of tables.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dashboard</title>
  <style>
    :root {
      --color-background: #fafafa;
      --color-text: #1f2937;
      --color-text-secondary: #6b7280;
      --color-primary: #6366f1;
      --color-primary-hover: #4f46e5;
      --color-border: #e5e7eb;
      --color-border-strong: #d1d5db;
      --space-2: 8px;
      --space-3: 12px;
      --space-4: 16px;
      --space-5: 24px;
      --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      --font-size-sm: 14px;
      --font-size-md: 16px;
      --radius-md: 6px;
      --radius-lg: 8px;
    }

    *, *::before, *::after { box-sizing: border-box; }

    body {
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      line-height: 1.5;
      color: var(--color-text);
      background: var(--color-background);
      margin: 0;
    }

    .header {
      background: white;
      border-bottom: 1px solid var(--color-border);
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: var(--space-5);
    }

    .nav {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding-top: var(--space-4);
      padding-bottom: var(--space-4);
    }

    .nav-brand {
      font-size: 18px;
      font-weight: 600;
    }

    .nav-links {
      display: flex;
      gap: var(--space-5);
      list-style: none;
      margin: 0;
      padding: 0;
    }

    .nav-links a {
      color: var(--color-text-secondary);
      text-decoration: none;
    }

    .nav-links a:hover {
      color: var(--color-text);
    }

    h1 {
      margin: 0 0 var(--space-5) 0;
      font-size: 24px;
    }

    .card-grid {
      display: grid;
      gap: var(--space-4);
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    }

    .card {
      display: flex;
      flex-direction: column;
      background: white;
      border: 1px solid var(--color-border);
      border-radius: var(--radius-lg);
      padding: var(--space-5);
      cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .card:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }

    .card-header {
      font-weight: 600;
      margin-bottom: var(--space-3);
    }

    .card-body {
      flex-grow: 1;
      color: var(--color-text-secondary);
    }

    .card-body p {
      margin: 0 0 var(--space-3) 0;
    }

    .card-meta {
      font-size: var(--font-size-sm);
      color: var(--color-text-secondary);
    }

    /* Footer at bottom due to flex-grow on card-body. No border-top. */
    .card-footer {
      display: flex;
      gap: var(--space-2);
      justify-content: flex-end;
      margin-top: var(--space-4);
      padding-top: var(--space-4);
    }

    .btn {
      padding: var(--space-2) var(--space-4);
      font-family: var(--font-family);
      font-size: var(--font-size-sm);
      font-weight: 500;
      border-radius: var(--radius-md);
      cursor: pointer;
      border: 1px solid transparent;
    }

    .btn-outline {
      background: transparent;
      color: var(--color-primary);
      border-color: var(--color-primary);
    }

    .btn-outline:hover {
      background: var(--color-primary);
      color: white;
    }

    .btn-secondary {
      background: white;
      color: var(--color-text);
      border-color: var(--color-border-strong);
    }

    .btn-secondary:hover {
      background: var(--color-background);
    }

    .toast-container {
      position: fixed;
      bottom: var(--space-4);
      right: var(--space-4);
      z-index: 1000;
    }

    .toast {
      display: flex;
      align-items: center;
      gap: var(--space-4);
      padding: var(--space-4) var(--space-5);
      background: white;
      border-radius: var(--radius-lg);
      box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
      min-width: 280px;
      animation: slideIn 0.3s ease;
      position: relative;
      overflow: hidden;
    }

    @keyframes slideIn {
      from { transform: translateX(100%); opacity: 0; }
      to { transform: translateX(0); opacity: 1; }
    }

    .toast-message { flex: 1; }

    .toast-undo {
      background: none;
      border: none;
      color: var(--color-primary);
      font-weight: 600;
      cursor: pointer;
      padding: var(--space-2);
    }

    .toast-undo:hover { text-decoration: underline; }

    .toast-timer {
      position: absolute;
      bottom: 0;
      left: 0;
      height: 3px;
      background: var(--color-primary);
      animation: timer 5s linear forwards;
    }

    @keyframes timer {
      from { width: 100%; }
      to { width: 0%; }
    }

    .toast.hiding {
      animation: slideOut 0.3s ease forwards;
    }

    @keyframes slideOut {
      to { transform: translateX(100%); opacity: 0; }
    }
  </style>
</head>
<body>
  <header class="header">
    <nav class="nav container">
      <strong class="nav-brand">App</strong>
      <ul class="nav-links">
        <li><a href="#">Overview</a></li>
        <li><a href="#">Projects</a></li>
        <li><a href="#">Archive</a></li>
      </ul>
    </nav>
  </header>

  <main class="container">
    <h1>Your Projects (3)</h1>

    <div class="card-grid" id="project-grid">
      <article class="card">
        <header class="card-header">Website Redesign</header>
        <div class="card-body">
          <p>Complete redesign of company website including responsive layouts.</p>
          <small class="card-meta">Last updated: 2 days ago</small>
        </div>
        <footer class="card-footer">
          <button class="btn btn-outline">Edit</button>
          <button class="btn btn-secondary" onclick="archiveItem(this)">Archive</button>
        </footer>
      </article>

      <article class="card">
        <header class="card-header">Mobile App</header>
        <div class="card-body">
          <p>iOS and Android app for order tracking and notifications.</p>
          <small class="card-meta">Last updated: 5 days ago</small>
        </div>
        <footer class="card-footer">
          <button class="btn btn-outline">Edit</button>
          <button class="btn btn-secondary" onclick="archiveItem(this)">Archive</button>
        </footer>
      </article>

      <article class="card">
        <header class="card-header">Dashboard Analytics</header>
        <div class="card-body">
          <p>Internal tool for sales data visualization and reporting.</p>
          <small class="card-meta">Last updated: 1 week ago</small>
        </div>
        <footer class="card-footer">
          <button class="btn btn-outline">Edit</button>
          <button class="btn btn-secondary" onclick="archiveItem(this)">Archive</button>
        </footer>
      </article>
    </div>
  </main>

  <div class="toast-container" aria-live="polite"></div>

  <script>
    let lastArchivedItem = null;
    let toastTimeout = null;

    function showToast(message, undoCallback) {
      const container = document.querySelector('.toast-container');
      const existingToast = container.querySelector('.toast');
      if (existingToast) {
        existingToast.remove();
        clearTimeout(toastTimeout);
      }

      const toast = document.createElement('div');
      toast.className = 'toast';
      toast.setAttribute('role', 'status');
      toast.innerHTML = `
        <span class="toast-message">${message}</span>
        ${undoCallback ? '<button class="toast-undo">Undo</button>' : ''}
        <div class="toast-timer"></div>
      `;

      container.appendChild(toast);

      if (undoCallback) {
        const undoBtn = toast.querySelector('.toast-undo');
        undoBtn.addEventListener('click', () => {
          undoCallback();
          removeToast(toast);
        });
      }

      toastTimeout = setTimeout(() => {
        removeToast(toast);
        lastArchivedItem = null;
      }, 5000);
    }

    function removeToast(toast) {
      toast.classList.add('hiding');
      setTimeout(() => toast.remove(), 300);
      clearTimeout(toastTimeout);
    }

    function archiveItem(button) {
      const item = button.closest('article');
      const itemName = item.querySelector('.card-header')?.textContent || 'Item';

      lastArchivedItem = {
        element: item,
        parent: item.parentNode,
        nextSibling: item.nextSibling
      };

      item.style.display = 'none';

      showToast(`${itemName} archived.`, () => {
        if (lastArchivedItem) {
          lastArchivedItem.element.style.display = '';
          lastArchivedItem = null;
        }
      });
    }
  </script>
</body>
</html>
```

---

## Company Registration Form (Business Example)

Demonstrating input width sizing for business data entry (IČO, DIČ, addresses).

```html
<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Registrace firmy</title>
  <style>
    :root {
      --color-background: #fafafa;
      --color-background-subtle: #f0f0f0;
      --color-text: #1f2937;
      --color-text-secondary: #6b7280;
      --color-text-muted: #9ca3af;
      --color-primary: #6366f1;
      --color-primary-hover: #4f46e5;
      --color-border: #e5e7eb;
      --color-border-strong: #d1d5db;
      --space-1: 4px;
      --space-2: 8px;
      --space-3: 12px;
      --space-4: 16px;
      --space-5: 24px;
      --space-6: 32px;
      --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      --font-size-sm: 14px;
      --font-size-md: 16px;
      --radius-md: 6px;
      --radius-lg: 8px;
    }

    *, *::before, *::after { box-sizing: border-box; }

    body {
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      line-height: 1.5;
      color: var(--color-text);
      background: var(--color-background);
      margin: 0;
    }

    .container {
      max-width: 700px;
      margin: 0 auto;
      padding: var(--space-6);
    }

    h1 {
      margin: 0 0 var(--space-2) 0;
      font-size: 24px;
    }

    .subtitle {
      color: var(--color-text-secondary);
      margin: 0 0 var(--space-6) 0;
    }

    .section {
      margin-bottom: var(--space-6);
    }

    .section-title {
      font-size: var(--font-size-sm);
      font-weight: 600;
      color: var(--color-text-secondary);
      text-transform: uppercase;
      letter-spacing: 0.05em;
      margin: 0 0 var(--space-4) 0;
    }

    .form-row {
      display: flex;
      gap: var(--space-4);
      flex-wrap: wrap;
      margin-bottom: var(--space-4);
    }

    .form-label {
      display: block;
    }

    .form-label-text {
      display: block;
      font-size: var(--font-size-sm);
      font-weight: 500;
      margin-bottom: var(--space-1);
    }

    .form-hint {
      display: block;
      font-size: 12px;
      color: var(--color-text-muted);
      margin-top: var(--space-1);
    }

    .form-input {
      display: block;
      width: 100%;
      padding: var(--space-2) var(--space-3);
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      color: var(--color-text);
      background: white;
      border: 1px solid var(--color-border-strong);
      border-radius: var(--radius-md);
    }

    .form-input:focus {
      outline: none;
      border-color: var(--color-primary);
      box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.15);
    }

    .form-input::placeholder {
      color: var(--color-text-muted);
    }

    /* Input Width Utilities - width on INPUT, not label */
    .input-xs .form-input { width: 100px; }
    .input-sm .form-input { width: 180px; }
    .input-md .form-input { width: 320px; }

    /* Keep short labels on one line */
    .form-label-text-nowrap { white-space: nowrap; }

    @media (max-width: 576px) {
      .input-xs .form-input,
      .input-sm .form-input,
      .input-md .form-input {
        width: 100%;
      }
      .form-row {
        flex-direction: column;
      }
    }

    .btn {
      padding: var(--space-3) var(--space-5);
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      font-weight: 500;
      background: var(--color-primary);
      color: white;
      border: none;
      border-radius: var(--radius-md);
      cursor: pointer;
    }

    .btn:hover {
      background: var(--color-primary-hover);
    }
  </style>
</head>
<body>
  <main class="container">
    <h1>Registrace firmy</h1>
    <p class="subtitle">Vyplňte údaje o vaší společnosti</p>

    <form>
      <div class="section">
        <h2 class="section-title">Základní údaje</h2>

        <!-- Company name: medium -->
        <div class="form-row">
          <label class="form-label input-md">
            <span class="form-label-text">Název společnosti</span>
            <input type="text" class="form-input" name="company_name" placeholder="ACME s.r.o.">
          </label>
        </div>

        <!-- IČO: small, DIČ: small -->
        <div class="form-row">
          <label class="form-label input-sm">
            <span class="form-label-text">IČO</span>
            <input type="text" class="form-input" name="ico" inputmode="numeric" placeholder="12345678">
            <small class="form-hint">8 číslic</small>
          </label>
          <label class="form-label input-sm">
            <span class="form-label-text">DIČ</span>
            <input type="text" class="form-input" name="dic" placeholder="CZ12345678">
            <small class="form-hint">Pouze plátci DPH</small>
          </label>
        </div>
      </div>

      <div class="section">
        <h2 class="section-title">Sídlo společnosti</h2>

        <!-- Street + number: medium, house number: xs -->
        <div class="form-row">
          <label class="form-label input-md">
            <span class="form-label-text">Ulice</span>
            <input type="text" class="form-input" name="street" placeholder="Václavské náměstí">
          </label>
          <label class="form-label input-xs">
            <span class="form-label-text form-label-text-nowrap">Č.p.</span>
            <input type="text" class="form-input" name="house_number" placeholder="1">
          </label>
        </div>

        <!-- City: small, ZIP: xs -->
        <div class="form-row">
          <label class="form-label input-sm">
            <span class="form-label-text">Město</span>
            <input type="text" class="form-input" name="city" placeholder="Praha">
          </label>
          <label class="form-label input-xs">
            <span class="form-label-text form-label-text-nowrap">PSČ</span>
            <input type="text" class="form-input" name="zip" inputmode="numeric" placeholder="110 00">
          </label>
        </div>
      </div>

      <div class="section">
        <h2 class="section-title">Kontaktní osoba</h2>

        <!-- Name: medium -->
        <div class="form-row">
          <label class="form-label input-md">
            <span class="form-label-text">Jméno a příjmení</span>
            <input type="text" class="form-input" name="contact_name" placeholder="Jan Novák">
          </label>
        </div>

        <!-- Email: medium, Phone: small -->
        <div class="form-row">
          <label class="form-label input-md">
            <span class="form-label-text">Email</span>
            <input type="email" class="form-input" name="email" placeholder="jan@acme.cz">
          </label>
          <label class="form-label input-sm">
            <span class="form-label-text">Telefon</span>
            <input type="tel" class="form-input" name="phone" placeholder="+420 123 456 789">
          </label>
        </div>
      </div>

      <button type="submit" class="btn">Zaregistrovat společnost</button>
    </form>
  </main>
</body>
</html>
```

---

## Empty State Example

When there are no items to display.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Projects</title>
  <style>
    :root {
      --color-background: #fafafa;
      --color-text: #1f2937;
      --color-text-secondary: #6b7280;
      --color-primary: #6366f1;
      --color-primary-hover: #4f46e5;
      --space-4: 16px;
      --space-5: 24px;
      --space-6: 32px;
      --space-8: 64px;
      --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      --font-size-md: 16px;
      --radius-md: 6px;
    }

    *, *::before, *::after { box-sizing: border-box; }

    body {
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      line-height: 1.5;
      color: var(--color-text);
      background: var(--color-background);
      margin: 0;
    }

    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: var(--space-5);
    }

    h1 {
      margin: 0 0 var(--space-5) 0;
      font-size: 24px;
    }

    .empty-state {
      text-align: center;
      padding: var(--space-8) var(--space-4);
      color: var(--color-text-secondary);
    }

    .empty-state p {
      font-size: 18px;
      margin: 0 0 var(--space-2) 0;
      color: var(--color-text);
    }

    .empty-state small {
      display: block;
      margin-bottom: var(--space-6);
    }

    .btn {
      padding: var(--space-3) var(--space-5);
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      font-weight: 500;
      background: var(--color-primary);
      color: white;
      border: none;
      border-radius: var(--radius-md);
      cursor: pointer;
    }

    .btn:hover {
      background: var(--color-primary-hover);
    }
  </style>
</head>
<body>
  <main class="container">
    <h1>Your Projects</h1>

    <div class="empty-state">
      <p>No projects yet</p>
      <small>Create your first project to get started</small>
      <button class="btn">Create Project</button>
    </div>
  </main>
</body>
</html>
```

---

## Loading States

Demonstrating loading indicators.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Loading States</title>
  <style>
    :root {
      --color-background: #fafafa;
      --color-background-subtle: #f0f0f0;
      --color-text: #1f2937;
      --color-text-secondary: #6b7280;
      --color-primary: #6366f1;
      --color-primary-hover: #4f46e5;
      --color-border: #e5e7eb;
      --space-2: 8px;
      --space-3: 12px;
      --space-4: 16px;
      --space-5: 24px;
      --space-6: 32px;
      --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      --font-size-md: 16px;
      --radius-md: 6px;
      --radius-lg: 8px;
    }

    *, *::before, *::after { box-sizing: border-box; }

    body {
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      line-height: 1.5;
      color: var(--color-text);
      background: var(--color-background);
      margin: 0;
    }

    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: var(--space-5);
    }

    h1 {
      margin: 0 0 var(--space-6) 0;
      font-size: 24px;
    }

    h2 {
      font-size: 18px;
      margin: 0 0 var(--space-4) 0;
    }

    section {
      margin-bottom: var(--space-6);
    }

    .demo-row {
      display: flex;
      align-items: center;
      gap: var(--space-4);
      margin-bottom: var(--space-4);
    }

    .spinner {
      width: 24px;
      height: 24px;
      border: 3px solid var(--color-border);
      border-top-color: var(--color-primary);
      border-radius: 50%;
      animation: spin 0.8s linear infinite;
    }

    @keyframes spin {
      to { transform: rotate(360deg); }
    }

    .btn {
      display: inline-flex;
      align-items: center;
      gap: var(--space-2);
      padding: var(--space-3) var(--space-5);
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      font-weight: 500;
      background: var(--color-primary);
      color: white;
      border: none;
      border-radius: var(--radius-md);
      cursor: pointer;
    }

    .btn:disabled {
      opacity: 0.7;
      cursor: not-allowed;
    }

    .spinner-sm {
      width: 16px;
      height: 16px;
      border-width: 2px;
      border-color: rgba(255,255,255,0.3);
      border-top-color: white;
    }

    .card {
      background: white;
      border: 1px solid var(--color-border);
      border-radius: var(--radius-lg);
      padding: var(--space-5);
    }

    .skeleton {
      background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
      background-size: 200% 100%;
      animation: shimmer 1.5s infinite;
      border-radius: var(--radius-md);
    }

    .skeleton-text {
      height: 1rem;
      margin-bottom: var(--space-2);
    }

    .skeleton-text.short {
      width: 60%;
    }

    @keyframes shimmer {
      0% { background-position: 200% 0; }
      100% { background-position: -200% 0; }
    }
  </style>
</head>
<body>
  <main class="container">
    <h1>Loading States</h1>

    <section>
      <h2>Spinner</h2>
      <div class="demo-row">
        <div class="spinner" aria-label="Loading"></div>
        <span>Loading data...</span>
      </div>
    </section>

    <section>
      <h2>Button Loading State</h2>
      <button class="btn" disabled>
        <div class="spinner spinner-sm"></div>
        Saving...
      </button>
    </section>

    <section>
      <h2>Skeleton Loading</h2>
      <article class="card">
        <div class="skeleton skeleton-text"></div>
        <div class="skeleton skeleton-text"></div>
        <div class="skeleton skeleton-text short"></div>
      </article>
    </section>
  </main>
</body>
</html>
```

---

## Content Library with Series (Audiobook Player)

A media browsing interface showing individual book cards and series cards with genre filtering, demonstrating the Content Cards patterns from `components.md`. This example uses Czech language UI as a real-world reference implementation.

Key patterns demonstrated:
- Book cards with cover, metadata, series position, genre tags
- Series cards that group multiple books with AI-generated descriptions
- Genre filter tabs with counts
- Sticky header that hides on scroll down, shows on scroll up
- Now-playing bar fixed at bottom
- Lazy registration: "Přihlásit se" link in header (no login gate)

```html
<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Moje knihy — Přehrávač</title>
  <style>
    :root {
      --color-background: #fafafa;
      --color-background-subtle: #f0f0f0;
      --color-text: #1f2937;
      --color-text-secondary: #6b7280;
      --color-text-muted: #9ca3af;
      --color-primary: #6366f1;
      --color-primary-hover: #4f46e5;
      --color-border: #e5e7eb;
      --color-border-strong: #d1d5db;
      --space-1: 4px;
      --space-2: 8px;
      --space-3: 12px;
      --space-4: 16px;
      --space-5: 24px;
      --space-6: 32px;
      --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      --font-size-sm: 14px;
      --font-size-md: 16px;
      --radius-sm: 4px;
      --radius-md: 6px;
      --radius-lg: 8px;
      --radius-full: 9999px;
    }

    *, *::before, *::after { box-sizing: border-box; }

    body {
      font-family: var(--font-family);
      font-size: var(--font-size-md);
      line-height: 1.5;
      color: var(--color-text);
      background: var(--color-background);
      margin: 0;
      padding-bottom: 72px; /* space for now-playing bar */
    }

    /* Sticky header */
    .sticky-header {
      position: sticky;
      top: 0;
      background: var(--color-background);
      z-index: 100;
      border-bottom: 1px solid var(--color-border);
    }

    .header-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: var(--space-3) var(--space-4);
    }

    .header-title {
      font-size: 18px;
      font-weight: 700;
    }

    .header-login {
      color: var(--color-primary);
      text-decoration: none;
      font-size: var(--font-size-sm);
      font-weight: 500;
    }

    .header-login:hover {
      color: var(--color-primary-hover);
    }

    /* Genre filter pills */
    .filter-bar {
      display: flex;
      gap: var(--space-2);
      padding: var(--space-2) var(--space-4) var(--space-3);
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
    }

    .filter-chip {
      flex-shrink: 0;
      padding: var(--space-1) var(--space-3);
      border-radius: var(--radius-full);
      font-size: 13px;
      font-weight: 500;
      border: 1px solid var(--color-border-strong);
      background: white;
      color: var(--color-text-secondary);
      cursor: pointer;
    }

    .filter-chip.active {
      background: var(--color-text);
      color: white;
      border-color: var(--color-text);
    }

    .filter-chip .chip-count {
      font-size: 10px;
      opacity: 0.6;
      margin-left: 2px;
    }

    /* Book list */
    .book-list {
      padding: 0 var(--space-4);
    }

    /* Book Card */
    .book-card {
      display: flex;
      gap: var(--space-3);
      padding: var(--space-3) 0;
      cursor: pointer;
      border-bottom: 1px solid var(--color-border);
    }

    .book-card:last-child {
      border-bottom: none;
    }

    .book-card-cover {
      flex-shrink: 0;
      width: 80px;
      height: 80px;
      border-radius: var(--radius-sm);
      overflow: hidden;
      background: var(--color-background-subtle);
    }

    .book-card-cover img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .book-card-info {
      flex: 1;
      min-width: 0;
    }

    .book-card-title {
      font-size: 15px;
      font-weight: 600;
      color: var(--color-text);
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .book-card-meta {
      font-size: 13px;
      color: var(--color-text-secondary);
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .book-card-series {
      font-size: 12px;
      color: var(--color-primary);
      margin-top: 2px;
    }

    .book-card-tags {
      display: flex;
      gap: var(--space-1);
      margin-top: var(--space-1);
      flex-wrap: wrap;
    }

    .book-card-tags .tag {
      font-size: 11px;
      padding: 1px 6px;
      background: var(--color-background-subtle);
      border-radius: var(--radius-full);
      color: var(--color-text-secondary);
    }

    .book-card-duration {
      font-size: 12px;
      color: var(--color-text-muted);
      margin-top: 2px;
    }

    /* Series Card */
    .series-card {
      display: flex;
      gap: var(--space-3);
      padding: var(--space-3) 0;
      cursor: pointer;
      border-bottom: 1px solid var(--color-border);
    }

    .series-card-cover {
      position: relative;
      flex-shrink: 0;
      width: 80px;
      height: 80px;
      border-radius: var(--radius-sm);
      overflow: hidden;
      background: var(--color-background-subtle);
    }

    .series-card-cover img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .series-badge {
      position: absolute;
      top: 4px;
      left: 4px;
      background: rgba(0, 0, 0, 0.7);
      color: white;
      font-size: 10px;
      font-weight: 600;
      padding: 1px 5px;
      border-radius: var(--radius-sm);
      text-transform: uppercase;
    }

    .series-card-info {
      flex: 1;
      min-width: 0;
    }

    .series-card-title {
      font-size: 15px;
      font-weight: 600;
    }

    .series-card-meta {
      font-size: 13px;
      color: var(--color-text-secondary);
    }

    .series-card-desc {
      font-size: 13px;
      color: var(--color-text-secondary);
      margin-top: var(--space-1);
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }

    .series-card-status {
      font-size: 12px;
      color: var(--color-primary);
      margin-top: 2px;
    }

    /* Now-playing mini bar */
    .now-playing-bar {
      position: fixed;
      bottom: 0;
      left: 0;
      right: 0;
      background: white;
      border-top: 1px solid var(--color-border);
      display: flex;
      align-items: center;
      gap: var(--space-3);
      padding: var(--space-2) var(--space-4);
      z-index: 200;
    }

    .now-playing-cover {
      width: 40px;
      height: 40px;
      border-radius: var(--radius-sm);
      overflow: hidden;
      flex-shrink: 0;
      background: var(--color-background-subtle);
    }

    .now-playing-cover img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .now-playing-info {
      flex: 1;
      min-width: 0;
    }

    .now-playing-title {
      font-size: 13px;
      font-weight: 600;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .now-playing-meta {
      font-size: 11px;
      color: var(--color-text-secondary);
    }

    .now-playing-btn {
      width: 36px;
      height: 36px;
      border-radius: 50%;
      border: none;
      background: var(--color-text);
      color: white;
      font-size: 14px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
    }

    .now-playing-progress {
      position: absolute;
      top: 0;
      left: 0;
      height: 2px;
      background: var(--color-primary);
      width: 35%;
    }
  </style>
</head>
<body>
  <!-- Sticky header with title + login link + filter pills -->
  <header class="sticky-header">
    <div class="header-row">
      <span class="header-title">Moje knihy</span>
      <a href="#" class="header-login">Přihlásit se</a>
    </div>
    <div class="filter-bar">
      <button class="filter-chip active">Vše <span class="chip-count">2016</span></button>
      <button class="filter-chip">Fantasy <span class="chip-count">342</span></button>
      <button class="filter-chip">Sci-fi <span class="chip-count">287</span></button>
      <button class="filter-chip">Thriller <span class="chip-count">198</span></button>
    </div>
  </header>

  <!-- Book list: mix of series cards and individual book cards -->
  <main class="book-list">

    <!-- Series card (collapsed) -->
    <article class="series-card" data-series="Propast času">
      <div class="series-card-cover">
        <img src="https://placehold.co/160x160/e2e8f0/64748b?text=P%C4%8D" alt="" loading="lazy">
        <span class="series-badge">Série</span>
      </div>
      <div class="series-card-info">
        <div class="series-card-title">Propast času</div>
        <div class="series-card-meta">Roman Bureš · 3 knihy</div>
        <div class="series-card-desc">
          Jedné noci se celý svět změnil. Lidské dějiny se roztříštily a střípky
          civilizací od pravěku až po budoucnost se složily do chaotické koláže.
        </div>
        <div class="series-card-status">Rozposloucháno · Díl 1</div>
      </div>
    </article>

    <!-- Individual book card (part of a series) -->
    <article class="book-card" data-id="kralovstvi-duni">
      <div class="book-card-cover">
        <img src="https://placehold.co/160x160/e2e8f0/64748b?text=Duna" alt="" loading="lazy">
      </div>
      <div class="book-card-info">
        <div class="book-card-title">Duna</div>
        <div class="book-card-meta">Frank Herbert · Filip Jančík</div>
        <div class="book-card-series">Díl 1 z 6 — Duna</div>
        <div class="book-card-tags">
          <span class="tag">sci-fi</span>
          <span class="tag">space opera</span>
        </div>
        <div class="book-card-duration">21:33</div>
      </div>
    </article>

    <!-- Standalone book card (no series) -->
    <article class="book-card" data-id="martianka">
      <div class="book-card-cover">
        <img src="https://placehold.co/160x160/e2e8f0/64748b?text=M" alt="" loading="lazy">
      </div>
      <div class="book-card-info">
        <div class="book-card-title">Marťanka</div>
        <div class="book-card-meta">Andy Weir · Zbyšek Horák</div>
        <div class="book-card-tags">
          <span class="tag">sci-fi</span>
          <span class="tag">hard sci-fi</span>
        </div>
        <div class="book-card-duration">13:47</div>
      </div>
    </article>

  </main>

  <!-- Now-playing mini bar -->
  <div class="now-playing-bar">
    <div class="now-playing-progress"></div>
    <div class="now-playing-cover">
      <img src="https://placehold.co/80x80/e2e8f0/64748b?text=%E2%96%B6" alt="" loading="lazy">
    </div>
    <div class="now-playing-info">
      <div class="now-playing-title">Propast času</div>
      <div class="now-playing-meta">Kap. 4 · 1:23:45</div>
    </div>
    <button class="now-playing-btn" aria-label="Přehrát">▶</button>
  </div>
</body>
</html>
```
