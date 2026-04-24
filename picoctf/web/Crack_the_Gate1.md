# Crack The Gate 1
Category: Web Exploitation  
Date: 24.04.2026  
Difficulty: Easy

Author: Yahaya Meddy
Description
We’re in the middle of an investigation. One of our persons of interest, ctf player, 
is believed to be hiding sensitive data inside a restricted web portal. 
We’ve uncovered the email address he uses to log in: ctf-player@picoctf.org. 
Unfortunately, we don’t know the password, and the usual guessing techniques haven’t worked. 
But something feels off... it’s almost like the developer left a secret way in. Can you figure it out?

Additional details will be available after launching your challenge instance.

Tools : 
1. Chrome (using dev-tools)
2. Google with AI (research about what kind of encoder and needed tools)
3. ROT13 encode - decoder (web based)
4. ModHeader as Chrome extension (to modify request header)


How to get Flag : 
1. try to log in with the given ctf-player@picoctf.org email address
 just put randomly as password (however the credential will be invalid).
 (returns response status:401)

2. I tried to inspect the page source and it seems that the developer forgot
 to erase an important and sensitve note as comment.
 comment : 
  <!-- ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf" -->
  <!-- Remove before pushing to production! -->  

3. I tried to google what kind of comment the dev used or usually use. It turns out
 that it is ROT13 encoding, so : 
 ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf" -> 
 NOTE: Jack - temporary bypass: use header "X-Dev-Access: yes"
 
4. I set ModHeader tool as extension in chrome and used it. Clicked + and chose Mod
 set name as X-Dev-Accept and value as yes.

5. Reload page -> returns response status:200, which means authorized

Side note : 
I used firefox beforehand and analysed the network in dev-tools. I can copy the request as Fetch
and pasted to console. Edit the header by injecting : "X-Dev-Access" : "yes",
before the : "content-type": "application/json"
Resent it and it returns response status:200 but not authorized
The reason is because the injection works locally.
There is difference between background request (via console) and the browser navigation
If the site was reloaded or login button was clicked, it will send standart request header again
Therefore such tool like ModHeader is really helpful, so a modified additional header can be 
always injected in each request.

Flag : picoCTF{brut4_f0rc4_1a386e6f}

What I learned : 
1. Bad Configured Source Code : The Developer forgot to erase a sensitive note as comment in 
 the source code, so attacker could get sensitive information about how to bypass an authentification.
 And probably in the backend such bypass function are not erased, so still can be used after production.
 This opens an opportunity for attacker to exploit the bypass function.
