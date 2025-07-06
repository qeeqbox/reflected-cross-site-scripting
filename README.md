<p align="center"> <img src="https://raw.githubusercontent.com/qeeqbox/dom-based-cross-site-scripting/main/content/dom-based-cross-site-scripting.svg"></p>

An application enables users to control the Document Object Model (DOM) environment. A threat actor can exploit this feature by injecting a malicious payload into a trusted web application. When users interact with this malicious payload, their browsers execute it. This vulnerability is not reflected in the HTTP request or response and occurs on the client side.

Clone this current repo recursively
```sh
git clone --recursive https://github.com/qeeqbox/dom-based-cross-site-scripting
```
Run the webapp using Python
```sh
python3 default-credential/vulnerable-web-app/webapp.py
```
Open the webapp in your browser 127.0.0.1:5142
<p align="center"> <img src="https://raw.githubusercontent.com/qeeqbox/dom-based-cross-site-scripting/main/content/1.png"></p>
Right-click on the page and click on View Page source, the page source will show the static content, one of the contents is JavaScript that handles the fragment identifier (# symbol) in the URL, which is meant to move users into specific sections of the page
<p align="center"> <img src="https://raw.githubusercontent.com/qeeqbox/dom-based-cross-site-scripting/main/content/2.png"></p>
If you type the URL + #test, it will take you to the test section, it does not exist but the test keyword gets embedded in the page
<p align="center"> <img src="https://raw.githubusercontent.com/qeeqbox/dom-based-cross-site-scripting/main/content/3.png"></p>
A threat actor could embed a malicious payload and send it to a victim using social engineering attacks. If the victim falls for it, their browser will execute a malicious payload
<p align="center"> <img src="https://raw.githubusercontent.com/qeeqbox/dom-based-cross-site-scripting/main/content/4.png"></p>

## Code
This logic will check the current URL for fragment identifiers. If # is part of the URL, it will pass it to the flash_message function()
```js
jQuery(document).ready(function($) {
  if (window.location.hash) {
    let hash_value = window.location.hash.substring(1);
      flash_message(`Moving to ${decodeURIComponent(hash_value)} section`)
  }
});
```
The flash_message function() embeds the user-controlled input directly into a div box without sanitizing it
```py
function flash_message(msg) {
  $("#error-dialog-box").html(msg)
  $("#error-dialog-box").dialog("open");
}
```
 
## Impact
Vary

## Risk
- Session Hijacking
- Credential Theft

## Redemption
- Client input validation
- Output encoding
- Browser built-in XSS preveiton

## ID
cb251c97-067d-4f13-8195-4f918273f41b
