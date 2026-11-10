# EWB Phishing URL Awareness Checker

## Overview
Phishing uses fake links and messages to steal passwords, card numbers, or OTPs. This command-line tool reads the text of a URL and points out six visible warning signs. It never opens or visits the link.

## Features
- Detects an @ symbol in the URL
- Flags unusually long URLs (over 100 characters)
- Flags IP-address hostnames
- Flags many hostname segments (5 or more)
- Flags punycode-style hostnames (xn--)
- Flags the HTTP scheme
- Improvement A: loops so you can check many URLs, type q to quit
- Improvement C: malformed input shows a clear message instead of crashing

## Requirements
Python 3.10 or later. No extra packages.

## How to Run
Windows: `python phishing_checker.py`
Mac/Linux: `python3 phishing_checker.py`

## Example Output
```
Enter a sample URL (or type q to quit): http://192.0.2.10/account

Result:
- Uses an IP address instead of a familiar domain.
- Uses HTTP. HTTPS alone does not prove trust.

REVIEW CAREFULLY: 2 warning sign(s) found.
Never enter passwords from unexpected links.
```

## Testing
Five sample tests are recorded in `tests/test_samples.md`. All five passed on Python 3.13.

| # | Input | Expected | Result |
|---|-------|----------|--------|
| 1 | https://www.example.com/login | No warning signs | PASS |
| 2 | http://192.0.2.10/account | IP address + HTTP | PASS |
| 3 | http://example.com@sample.invalid/login | @ symbol + HTTP | PASS |
| 4 | https://a.b.c.d.e.example.invalid/path | Many hostname segments | PASS |
| 5 | https://xn--example.invalid/ | Punycode-style hostname | PASS |

## Screenshots
![Sample run](screenshots/sample_run.png)
![Test results](screenshots/test_results.png)

## Improvements
1. **Loop with quit (A)** - The program now stays open and checks several URLs until the user types q. I tested it by entering several samples in a row and then q.
2. **Safer parsing (C)** - Input like `http://[bad` used to crash with ValueError. It is now wrapped in try/except and returns a friendly message. I tested it with that input and confirmed the program keeps running.

## Limitations
This is an educational tool. It only reads URL text. It does not visit URLs, scan for malware, or prove that a URL is safe. No warning signs found does NOT mean a URL is safe. A tricky name such as secure-login.example.invalid can pass with no warnings.

## Ethical Use
Use sample strings only. Do not collect credentials. Do not use this project to deceive anyone or to test websites without permission.

## Author
Jasmine Banu D, Cybersecurity Course, EWB Courses
