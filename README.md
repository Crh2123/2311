<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>PWA Builder</title>
  <meta name="theme-color" content="#2196f3">
  <style>
    body { font-family: sans-serif; margin: 2rem; background: #e3f2fd; }
    h1 { color: #0d47a1; }
    input, textarea, button { width: 100%; margin: 0.5rem 0; padding: 0.75rem; font-size: 1rem; }
    button { background: #1976d2; color: white; border: none; cursor: pointer; }
    iframe { width: 100%; height: 300px; margin-top: 1rem; border: 1px solid #aaa; }
  </style>
</head>
<body>
  <h1>📱 Make Your Own PWA</h1>
  <input id="title" placeholder="Page Title (e.g. My Store)">
  <textarea id="message" placeholder="Message or offer..."></textarea>
  <input id="paylink" placeholder="Payment Link (PayPal, Stripe, etc.)">
  <input id="contact" placeholder="Your Contact Info (email, Telegram)">
  <button onclick="create()">Generate Landing Page</button>
  <a id="download" style="display:none;" download="landing.html">Download Page</a>
  <iframe id="preview"></iframe>

  <script>
    function create() {
      const title = document.getElementById("title").value;
      const message = document.getElementById("message").value;
      const paylink = document.getElementById("paylink").value;
      const contact = document.getElementById("contact").value;

      const html = `
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>${title}</title>
  <style>
    body { font-family: sans-serif; text-align: center; padding: 2rem; background: #fff; }
    h1 { color: #0d47a1; }
    a.button { display: inline-block; padding: 1rem 2rem; background: #1976d2; color: white; text-decoration: none; margin: 1rem 0; }
    p.contact { margin-top: 2rem; font-size: 0.9rem; color: #555; }
  </style>
</head>
<body>
  <h1>${title}</h1>
  <p>${message}</p>
  <a class="button" href="${paylink}" target="_blank">💸 Pay Now</a>
  <p class="contact">📞 Contact: ${contact}</p>
</body>
</html>
      `.trim();

      const blob = new Blob([html], {type: 'text/html'});
      const url = URL.createObjectURL(blob);
      document.getElementById("preview").src = url;

      const download = document.getElementById("download");
      download.href = url;
      download.style.display = 'inline-block';
      download.textContent = '⬇️ Download Landing Page';
    }

    if ('serviceWorker' in navigator) {
      navigator.serviceWorker.register('data:text/javascript;base64,')
        .catch(() => {});
    }
  </script>
</body>
</html>