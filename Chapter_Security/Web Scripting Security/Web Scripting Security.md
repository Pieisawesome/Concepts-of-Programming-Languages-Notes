# Web Scripting Security

## Brief Overview of How Web Browsers and Network Work

The browser sends requests to the website. This is sent through HTTP(S) requests. These methods include GET, to retrieve a resource, and POST, submit a form. The server sends a reply (response pages), which may include code. This reply is call a HTTP(S) response and is stateless request/response protocol.

Cookies are used to store state info on your computer. Cookies add state to HTTP(S). Cookies are a name/value pair.

Overall, cookies are stored by the browser and are used to store specific information about the user. And if a cookie is saved on your computer, only the website the created the cookie can read it.

## Cross Site Scripting (XSS Attacks)

Web vulnerability that lets malicious hacker inject undesired commands into legitimate client-side code executed by a browser. Commonly used on forums, message boards, and web pages that allow comments.

These scripts can access local files on the client side host, and webpages resources maintained by the browser; including cookies and Domain Object Model (DOM) objects.

Domain Object Model objects hold private information, control what users see and, if used maliciously, can impersonate the user.

### Reflected XSS
Malicious script comes form the current HTTP request.

Malicious JavaScript is send as part of the victim's request to the website. Commonly found in phishing attacks.

![Steps showing how Reflected XSS works. 1) Attacker or Attacker Server sends a link that has Javascript in <script> tags in it to the victim. Note that this only works if the victim clicks on that link. 2) Redirects user to the website using that link and script inside of it. 3) The website runs the script in link and sends the cookies back to the user. 4) Once arrived back, the cookie is then sent to the attacker's server.](Reflected_XSS.png)

### Stored XSS (Persistent XSS)
Malicious script comes form website's database.

Application receives data from untrusted source and includes that data within its later HTTP responses in an unsafe way.

![Steps showing how Stored XSS works. 1) Attacker sends a post or comment that has Javascript in <script> tags on the website. The comment is now stored on the website's database. 2) A user goes to access that website page which contains the script. 3) Website sends script to the user's browser which then the script runs on. 4) The script runs and sends private information to the attacker, like cookies.](image.png)

Different from reflected XSS as the attacker does not need to find ways for users to click on their links. They simply just have to wait for users to encounter it on the application.


### DOM-based XSS
Vulnerability exist in client-side code rather than server-side code.

