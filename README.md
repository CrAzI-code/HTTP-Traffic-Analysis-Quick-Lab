🔍 HTTP Traffic Analysis — Quick Lab 

Author: Obiora Emmanuel Ikechukwu
Project: HTTP Traffic Analysis & Credential Exposure
Date: 08-11-2025

Summary
I captured local HTTP traffic to show how unencrypted requests can expose sensitive data — then compared that to HTTPS to see how encryption protects it.
Why this matters
Plain HTTP sends text anyone can read on the network - usernames, cookies, and form data can be intercepted. This lab shows that difference visually and practically using Wireshark.
What I built
A short capture of HTTP traffic (local test server and a public non-HTTPS site).


A Wireshark analysis highlighting exposed request headers, cookies, and credentials.


A simple comparison showing the same exchange over HTTPS (encrypted).
Environment 
Linux VM (Ubuntu/Kali), Wireshark, Python 3, Browser (Firefox/Chrome).
Quick checklist (what I did)
Started local HTTP server: python3 -m http.server 8080
Captured traffic in Wireshark on eth0 (or any)
Filtered HTTP: http and followed TCP streams
Compared with HTTPS traffic: tls / http filter



 Skills You’ll Learn
How to capture HTTP requests/responses


How to follow TCP and HTTP streams


How credentials and data appear in plaintext (insecurely)


Difference between HTTP and HTTPS in Wireshark captures


Step-by-Step Guide
Step 1: Start Wireshark
Open Wireshark in your Linux VM.


Select your network interface — usually eth0 or ens33 (for bridged/NAT networks).


Click “Start Capturing Packets.”


Run your own HTTP server 
In a terminal, run:
mkdir ~/http_project && cd ~/http_project
echo "Hello Wireshark!" > index.html
python3 -m http.server 8080


Now visit in browser: http://localhost:8080

Step 3: Filter HTTP Packets
In Wireshark, apply this filter:
Http

You’ll now see HTTP GET and POST requests, status codes, and responses.
Step 4: Analyze Requests
Click on any HTTP packet → expand:
Look at:
Request Method: GET or POST
Host: target website
User-Agent: browser type
Cookies: stored data
Authorization (if used): sometimes shows Base64-encoded credentials



Step 5: Follow TCP Stream
Right-click any HTTP packet →
 Follow → TCP Stream
You’ll see the entire conversation in one view — including request and server reply, such as:

You can decode the Base64 to reveal the username and password.
Run this in terminal:   echo dXNlcjpwYXNzd29yZA== | base64 -d


Step 6: Observe HTTP vs HTTPS
Now, visit any HTTPS site, e.g.: Aliexpress


Apply the same Wireshark filter: Http or Tls


Notice:
HTTP requests disappear (they’re encrypted).


You’ll only see TLS handshake and encrypted data (no readable text).


Compare both — this demonstrates how encryption protects your data.


Challenges Faced
Identifying useful traffic among background system connections.


Ensuring Wireshark had permission to capture packets (needed sudo).


Some modern browsers auto-redirected HTTP to HTTPS, limiting what I could capture.



What I Learned
This project gave me hands-on experience with:
Using Wireshark effectively to monitor network activity.


Applying filters to isolate specific types of traffic (HTTP).


Understanding how HTTP requests and responses look at the packet level.


Recognizing the importance of encryption in protecting data over networks.


By the end of this project, I was able to:

 ✅ Capture real HTTP traffic
 
 ✅ Follow TCP streams to see client-server conversations
 
 ✅ Identify sensitive information visible in plaintext
 
 ✅ Save and document the capture for analysis

Next Steps
In future projects, I plan to:
Analyze HTTPS traffic using SSL key logging for decryption.


Compare secure vs insecure protocols.


Explore DNS, ARP, and TLS handshake captures.

