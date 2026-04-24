24.04.2026

Web Exploitation

Old Session

Task
Author: David Gaviria
Description
Proper session timeout controls are critical for securing user accounts. 
If a user logs in on a public or shared computer but doesn’t explicitly
log out (instead simply closing the browser tab), and session expiration dates 
are misconfigured, the session may remain active indefinitely.
This then allows an attacker using the same browser later to access the user’s 
account without needing credentials, exploiting the fact that sessions never 
expire and remain authenticated.

Additional details will be available after launching your challenge instance.

Your friend tells you to check out a new social media platform he built a few 
years ago. Although its still under development,
he said the site is almost complete.
He also mentioned that he hates constantly logging into sites, 
and so has made his page that 'once you login, you never have to log-out 
again'! Browse here, and find the flag!

Tools : 
Chrome (using dev-tools)
Google (research about cookies)

How to get Flag : 
1. register (I just let the username and password to be empty
 cause I'm too lazy)
2. log in with your new account
3. you'll see the comment from one of the users about wierd /sessions page
 once you logged in
4. there is this information in /sessions page : 
1) session:fAEsVpyd7h1as-z60RAYUYs3AUk1CC5CfjOUFFsJzYA, {'_permanent': True, 'key': 'admin'}
2) session:KjSBYXoJuzDlecg1WkoQ2xP2T7aS2NKMlomz1Vcb35A, {'_permanent': True, 'key': ''}
5. back to social media page, open dev-tools (Fn+F12) -> 
 storage -> cookies -> http.. -> change value from cookies -> reload page -> 
 welcome admin shows in page (changed to other alive session)

Flag : picoCTF{s3t_s3ss10n_3xp1rat10n5_53a328ed}

What I learned : 
1. Weakness about infinite alive session : bad idea cause it creates infinite
 open windows of opportunity for the  attacker to steal the session tokens and 
 mimic another user using this tokens and in this case is cookie.(XSS)
