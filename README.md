<h1>Inspecting RADIUS Traffic with Wireshark</h1>

<h2>Overview</h2>
In this lab, we'll start up a RADIUS server on port 1812. RADIUS supplies centralized authorization, authentication and accounting management for users that are connecting to the service.
<br />
<br />

<h2>Process</h2>
We'll start by using IdBlender to create a public RADIUS server.
<br />
<img src="https://imgur.com/TxvSUGH.png" alt="public RADIUS server"/>
<img src="https://imgur.com/3Ujf66l.png" alt="credentials in RADIUS server"/>
This should now indicate that we’ve set up a RADIUS server:
<img src="https://imgur.com/aLVkSJW.png" alt="created identities" />
Now we can open wireshark and put in a filter for port 1812 (the port RADIUS operates with)

We can open wireshark and run inspecting traffic, but nothing seems to happen.
<img src="https://imgur.com/eR8dnxi.png" alt="wireshark interface" />
Now we need to use the client in our RADIUS server architecture. We will use a program use NTRadPing.
If we put in all of our credentials, the port number RADIUS works on and the IP address that we were provided with our RADIUS server and hit send. We see Access=Accept
<img src=https://imgur.com/JWwBvVy.png" alt="NTRadPing" />
If we try an incorrect password we get a different result.
<img src="https://imgur.com/urnuwEj.png" alt="NTRadPing incorrect password"/>
Opening wireshark and inspecting the first packet we can see that the username is sent in cleartext and the password is encrypted:
<img src="https://imgur.com/oCrc3lU.png" alt="wireshark encrypted password"/>
We can also see that the first request was successful and the second one failed.
<img src="https://imgur.com/nfu0ihA.png" alt="pass and fail"/>
RADIUS uses a secret key and the MD5 hashing algorithm to hide the passwords.
<img src="https://imgur.com/8psUe9C.png" alt="password encryption"/>
<img src="https://imgur.com/A2dgH0s.png" alt="preferences menu"/>
<img src="https://imgur.com/3JTJH0Z.png" alt="wireshark preferences"/>
Now we can open our Access-Request packet and see that our password is now shown in plain text.
<img src="https://imgur.com/PtRFqLj.png" alt="plaintext password" />