<!DOCTYPE html>
<html>
<head>
  <title>Fake Account Detector</title>
  <style>
    body { font-family: Arial; padding: 30px; max-width: 600px; }
    input, button { padding: 10px; margin: 8px 0; width: 100%; }
    #result { font-size: 18px; font-weight: bold; margin-top: 20px; }
  </style>
</head>
<body>
  <h2>Fake Account Detector</h2>

  <label>Username:</label>
  <input type="text" id="username" placeholder="e.g., john123456">

  <label>Bio:</label>
  <input type="text" id="bio" placeholder="e.g., Love to travel and code.">

  <label>Profile Picture Present?</label>
  <select id="hasProfilePic">
    <option value="yes">Yes</option>
    <option value="no">No</option>
  </select>

  <label>Account Age (in days):</label>
  <input type="number" id="age" placeholder="e.g., 3">

  <label>Number of Posts:</label>
  <input type="number" id="posts" placeholder="e.g., 0">

  <label>Followers:</label>
  <input type="number" id="followers" placeholder="e.g., 5">

  <label>Following:</label>
  <input type="number" id="following" placeholder="e.g., 200">

  <button onclick="checkFake()">Check Account</button>

  <div id="result"></div>

  <script>
    function checkFake() {
      const username = document.getElementById("username").value;
      const bio = document.getElementById("bio").value.trim();
      const hasPic = document.getElementById("hasProfilePic").value;
      const age = parseInt(document.getElementById("age").value);
      const posts = parseInt(document.getElementById("posts").value);
      const followers = parseInt(document.getElementById("followers").value);
      const following = parseInt(document.getElementById("following").value);

      let score = 0;

      // Username with too many numbers
      if ((username.match(/\d/g) || []).length > 4) score++;

      // Short or empty bio
      if (bio.length < 10) score++;

      // No profile picture
      if (hasPic === "no") score++;

      // Very new account
      if (age < 7) score++;

      // No posts
      if (posts === 0) score++;

      // Follower-following imbalance
      if (following > 100 && followers < 10) score++;

      const result = document.getElementById("result");
      if (score >= 3) {
        result.innerText = "This account is likely FAKE.";
        result.style.color = "red";
      } else {
        result.innerText = "This account seems LEGIT.";
        result.style.color = "green";
      }
    }
  </script>
</body>
</html>
