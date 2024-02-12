<body>
<h1>Termux RTMP Server Configuration Reference</h1>

<p>Below is the code to install Node-Media-Server on Termux and start the RTMP server. You can copy and paste this code into your Termux terminal.</p>

<!-- Installation Instructions -->
<div style="border: 1px solid black; padding: 10px;">
    <h2>Install Node-Media-Server</h2>
    <pre><code>pkg update && pkg upgrade -y
mkdir rtmp
cd rtmp
pkg install nodejs -y
npm install node-media-server</code></pre>
</div>

<!-- App Config Instructions -->
<div style="border: 1px solid black; padding: 10px;">
    <h2>Configure JS App In rtmp Dir</h2>
    <pre><code>nano app.js</code></pre>
</div>

<!-- Code For app.js -->
<div style="border: 1px solid black; padding: 10px;">
    <h2>Code For Config</h2>
    <pre><code>const NodeMediaServer = require('node-media-server');

const config = {
  rtmp: {
    port: 1935,
    chunk_size: 60000,
    gop_cache: true,
    ping: 30,
    ping_timeout: 60
  },
  http: {
    port: 8000,
    allow_origin: '*'
  }
};

const nms = new NodeMediaServer(config);
nms.run();</code></pre>
</div>

<!-- Start app.js -->
<div style="border: 1px solid black; padding: 10px;">
    <h2>Starting The Server</h2>
    <pre><code>
        cd rtmp
        node app.js</code></pre>
</div>

<!-- To View From Anywhere In The World -->
<div style="border: 1px solid black; padding: 10px;">
     <h2>Using Serveo To View From Anywhere In The World This Will Give You A Link
     Open A New Termux Seesion (OPTIONAL) </h2>
     <pre><code>ssh -R 80:localhost:1935 serveo.net</code></pre>
</div>

<!-- Sending Video To Server -->
<h2>Sending Video To Server From Gopro Hero 9 Using The Quik App</h2>
<ol>
        <li>On the Device Running Termux Start The Mobile Hotspot.</li>
        <li>Open The Quik App And Connect The Gopro. Select Live Stream And Chose Other/RTMP.</li>
<li>Connect The Gopro To Your Mobile Hotspot. This Setup Will Not Incur Extra Charges On An
Unlimited Mobile Plan, Even If You Have Limited Hotspot This Will Work Over The Limit.</li>
<li>Using Another Device, Find The Ip Address Of Your Mobile Hotspot.</li>
<li>Enter rtmp://mobile-hotspot-ip/live/stream , replace <code>mobile-hotspot-ip</code> With IP Address Of Mobile Hotspot.</li>
<li>Press Start Streaming And You Should See Node-Media-Server Output Logs On The Termux Session</li>
</ol>

<!-- VLC Instructions -->
<h2>Access the RTMP Stream</h2>
<p>To view the RTMP stream, follow these instructions in VLC:</p>
<ol>
    <li>Open VLC media player.</li>
    <li>Go to <strong>Media</strong> -> <strong>Open Network Stream</strong>.</li>
    <li>Enter the following URL: <code>rtmp://localhost/live/stream</code></li>
    <li>If accessing from another device on the same network, replace <code>localhost</code> with the IP address of your Termux instance.</li>
    <li>If accessing from the internet, replace <code>localhost</code> with the link generated by Serveo.net without http:// .</li>
</ol>

<div style="border: 1px solid black; padding: 10px;">
<h2>Any questions Feel Free To Tweet At Me @CentreTrucking</h2>
<p>FFMPEG Can Be Used To Stream To X (Formerly Twitter) Using The Relay Function</p>
</div>

</body>
</html>
