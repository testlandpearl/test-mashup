# test-mashup
SAP Service Cloud mashup test page
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Atea - Service Cloud Mashup Example</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: "72", Arial, sans-serif;
      background: #f5f6f7;
      color: #32363a;
      padding: 24px;
    }
    .card {
      background: #fff;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      padding: 24px;
      max-width: 520px;
      margin: 0 auto;
    }
    .header {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 20px;
      border-bottom: 2px solid #0070f2;
      padding-bottom: 12px;
    }
    .sap-dot {
      width: 36px; height: 36px;
      background: #0070f2;
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      color: #fff; font-weight: bold; font-size: 14px;
    }
    h1 { font-size: 18px; color: #0070f2; }
    .subtitle { font-size: 12px; color: #6a6d70; margin-top: 2px; }
    .param-section { margin-top: 16px; }
    .param-label {
      font-size: 11px;
      font-weight: bold;
      color: #6a6d70;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      margin-bottom: 4px;
    }
    .param-value {
      font-size: 15px;
      color: #32363a;
      background: #f5f6f7;
      border: 1px solid #d9d9d9;
      border-radius: 4px;
      padding: 8px 12px;
      min-height: 36px;
    }
    .param-value.missing { color: #bb0000; font-style: italic; font-size: 13px; }
    .divider { border: none; border-top: 1px solid #e5e5e5; margin: 20px 0; }
    .info-box {
      background: #e8f4fd;
      border-left: 4px solid #0070f2;
      border-radius: 4px;
      padding: 12px 14px;
      font-size: 13px;
      line-height: 1.5;
    }
    .info-box strong { color: #0070f2; }
    .timestamp { font-size: 11px; color: #6a6d70; margin-top: 16px; text-align: right; }
    table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 13px; }
    th { background: #0070f2; color: #fff; padding: 8px 10px; text-align: left; }
    td { padding: 7px 10px; border-bottom: 1px solid #e5e5e5; }
    tr:last-child td { border-bottom: none; }
  </style>
</head>
<body>
<div class="card">
  <div class="header">
    <div class="sap-dot">SAP</div>
    <div>
      <h1>Atea Mashup – Example</h1>
      <div class="subtitle">SAP Sales and Service Cloud Version 2 · HTML Mashup Demo</div>
    </div>
  </div>

  <div class="param-section">
    <div class="param-label">Account ID (par1)</div>
    <div class="param-value" id="accountId">–</div>
  </div>

  <div class="param-section" style="margin-top:12px;">
    <div class="param-label">Case ID (par2)</div>
    <div class="param-value" id="caseId">–</div>
  </div>

  <hr class="divider"/>

  <div class="info-box">
    <strong>How this works:</strong><br/>
    SAP Sales and Service Cloud Version 2 passes values from the current screen to this page via URL parameters
    (<code>par1</code>, <code>par2</code>). The page reads these on load and displays them above.
    In a real mashup, you would use these IDs to call an external API or S/4HANA system.
  </div>

  <hr class="divider"/>

  <div class="param-label">All Received URL Parameters</div>
  <table id="paramTable">
    <tr><th>Parameter</th><th>Value</th></tr>
  </table>

  <div class="timestamp" id="timestamp"></div>
</div>

<script>
  // Read all URL parameters passed by SAP Sales and Service Cloud Version 2
  const params = new URLSearchParams(window.location.search);

  // Display named parameters
  const accountId = params.get('par1');
  const caseId    = params.get('par2');

  const acEl = document.getElementById('accountId');
  const csEl = document.getElementById('caseId');

  if (accountId) {
    acEl.textContent = accountId;
  } else {
    acEl.textContent = 'Not passed (par1 not set)';
    acEl.classList.add('missing');
  }

  if (caseId) {
    csEl.textContent = caseId;
  } else {
    csEl.textContent = 'Not passed (par2 not set)';
    csEl.classList.add('missing');
  }

  // Show ALL parameters in the table
  const table = document.getElementById('paramTable');
  let count = 0;
  params.forEach((val, key) => {
    const row = table.insertRow();
    row.insertCell(0).textContent = key;
    row.insertCell(1).textContent = val;
    count++;
  });
  if (count === 0) {
    const row = table.insertRow();
    const cell = row.insertCell(0);
    cell.colSpan = 2;
    cell.style.fontStyle = 'italic';
    cell.style.color = '#bb0000';
    cell.textContent = 'No parameters received – open via SAP Sales and Service Cloud Version 2 mashup to pass values.';
  }

  // Timestamp
  document.getElementById('timestamp').textContent =
    'Loaded: ' + new Date().toLocaleString();
</script>
</body>
</html>
