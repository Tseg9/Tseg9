
const express = require('express');
const fetch = require('node-fetch');
const app = express();
const port = 3000;

// Replace with your ipinfo.io API token
const IPINFO_TOKEN = 'YOUR_IPINFO_TOKEN';

app.get('/get-location', async (req, res) => {
  try {
    // Get the user's IP address from the request
    const ipAddress = req.headers['x-forwarded-for'] || req.connection.remoteAddress;
    //Remove IPv6 prefix, if any
    const cleanIpAddress = ipAddress.replace(/^.*:/, '');

    const response = await fetch(`https://ipinfo.io/${cleanIpAddress}?token=${IPINFO_TOKEN}`);

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
    res.json(data);

  } catch (error) {
    console.error('Error fetching IP geolocation:', error);
    res.status(500).json({ error: 'Failed to get location' });
  }
});

app.listen(port, () => {
  console.log(`Server listening at http://localhost:${port}`);
});












/*onst myName(Hi, I'm @Tseg9)
console.log(myName)
- 👋 Hi, I’m @Tseg9
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Tseg9/Tseg9 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.*/
--->
