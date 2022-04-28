<p align="center"> <img src="https://raw.githubusercontent.com/qeeqbox/reflected-cross-site-scripting/main/reflected-cross-site-scripting.png"></p>

An adversary may inject malicious content into HTTP requests. The content will be reflected in the HTTP response and executed in the victim's browser.

## Example #1
1. Adversary crafts an email with a malicious request to a vulnerable target and sends the email to Bob
2. Bob clicks on the email and sends the request to the vulnerable target
3. The target includes the malicious code as part of the response and sends it back to Bob
4. Bob's browser executes the malicious code that calls back the Adversary
 
## Impact
Vary

## Risk
- gain unauthorized access

## Redemption
- input validation
- output encoding
- Browser built-in XSS preveiton

## ID
cb251c97-067d-4f13-8195-4f918273f41b

## References
- [wiki](https://en.wikipedia.org/wiki/cross-site_scripting)
