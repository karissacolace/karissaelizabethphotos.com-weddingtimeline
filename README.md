<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Karissa Elizabeth Photos – Wedding Timeline Generator</title>
  <style>
    body {
      font-family: Georgia, 'Times New Roman', serif;
      background-color: #f7f7f5;
      color: #111;
      margin: 0;
      padding: 40px 20px;
    }

    .container {
      max-width: 900px;
      margin: 0 auto;
      background: #ffffff;
      padding: 40px;
      border-radius: 10px;
    }

    h1 {
      text-align: center;
      font-weight: 400;
      margin-bottom: 10px;
    }

    h2 {
      margin-top: 40px;
      font-weight: 400;
    }

    p.subtitle {
      text-align: center;
      color: #666;
      margin-bottom: 40px;
    }

    label {
      display: block;
      margin-top: 20px;
      font-weight: 600;
    }

    input, select {
      width: 100%;
      padding: 10px;
      margin-top: 8px;
      font-size: 16px;
    }

    button {
      margin-top: 30px;
      padding: 14px 20px;
      font-size: 16px;
      background-color: #c7cfc5; /* sage green */
      border: none;
      cursor: pointer;
      border-radius: 6px;
    }

    .timeline {
      margin-top: 40px;
      line-height: 1.8;
    }

    .footer {
      margin-top: 60px;
      text-align: center;
      font-size: 14px;
      color: #777;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Karissa Elizabeth Photos</h1>
    <p class="subtitle">Wedding Day Timeline Generator</p>

    <label for="ceremony">Ceremony Start Time</label>
    <input type="time" id="ceremony" />

    <label for="firstLook">First Look?</label>
    <select id="firstLook">
      <option value="yes">Yes</option>
      <option value="no">No</option>
    </select>

    <button onclick="generateTimeline()">Generate Timeline</button>

    <div id="timeline" class="timeline"></div>

    <div class="footer">
      Created with intention by Karissa Elizabeth Photos
    </div>
  </div>

  <script>
    function generateTimeline() {
      const ceremonyTime = document.getElementById('ceremony').value;
      const firstLook = document.getElementById('firstLook').value;
      const timelineDiv = document.getElementById('timeline');

      if (!ceremonyTime) {
        timelineDiv.innerHTML = '<p>Please select a ceremony time.</p>';
        return;
      }

      const [hours, minutes] = ceremonyTime.split(':').map(Number);
      const ceremonyDate = new Date();
      ceremonyDate.setHours(hours, minutes);

      function formatTime(date) {
        let h = date.getHours();
        let m = date.getMinutes();
        const ampm = h >= 12 ? 'PM' : 'AM';
        h = h % 12 || 12;
        m = m.toString().padStart(2, '0');
        return `${h}:${m} ${ampm}`;
      }

      let output = '<h2>Your Wedding Day Timeline</h2>';

      if (firstLook === 'yes') {
        const firstLookTime = new Date(ceremonyDate.getTime() - 120 * 60000);
        output += `<p><strong>${formatTime(firstLookTime)}</strong> – First Look & Portraits</p>`;
      }

      const ceremonyStart = formatTime(ceremonyDate);
      output += `<p><strong>${ceremonyStart}</strong> – Ceremony Begins</p>`;

      const ceremonyEnd = new Date(ceremonyDate.getTime() + 30 * 60000);
      output += `<p><strong>${formatTime(ceremonyEnd)}</strong> – Ceremony Ends</p>`;

      timelineDiv.innerHTML = output;
    }
  </script>
</body>
</html>
