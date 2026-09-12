# Security Policy

## Scope

This policy applies to the CalcPro website and its calculator, currency converter,
budget manager, and physics/engineering tools.

CalcPro is a client-side static website. It does not provide user accounts,
authentication, payment processing, or a server-side database.

## Supported versions

| Version | Supported |
| --- | --- |
| CalcPro v1.0 | Yes |

Only the latest published version receives security fixes.

## Reporting a vulnerability

Please do not publicly disclose a vulnerability before it has been reviewed.

Report security issues privately to the website owner or repository maintainer
using the project's private security-reporting channel. Include:

- A short description of the issue
- The affected page or feature
- Reproduction steps or a proof of concept
- The potential impact
- Browser and operating-system information

Do not include real passwords, financial records, personal data, or other
sensitive information in a report. Use test data only.

We will acknowledge a valid report when practicable, investigate it, and
coordinate a fix or mitigation. Please allow reasonable time for remediation
before public disclosure.

## Data and privacy

CalcPro stores calculator history, settings, budget entries, and saved currency
rates in the browser's `localStorage`. This storage is not encrypted and is not
a security boundary.

Users should:

- Use test or non-sensitive data when using a public or shared computer
- Clear browser data before giving a device to another person
- Avoid entering passwords, payment-card details, government identifiers, or
  highly sensitive financial information
- Understand that browser extensions or other scripts running in the same
  browser origin may be able to access local storage

Currency rates are informational. Users should verify rates with a trusted
financial provider before making financial decisions.

## Deployment requirements

Before publishing, deploy the site over HTTPS and configure security response
headers at the hosting provider:

```css
Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; connect-src 'self' https://open.er-api.com; img-src 'self' data:; frame-src 'self'; object-src 'none'; base-uri 'none'; frame-ancestors 'self'; form-action 'self'; upgrade-insecure-requests
Referrer-Policy: strict-origin-when-cross-origin
X-Content-Type-Options: nosniff
Permissions-Policy: camera=(), microphone=(), geolocation=()
Strict-Transport-Security: max-age=31536000; includeSubDomains
```

The inline script and styles currently require the `unsafe-inline` allowances
shown above. For stronger protection, move inline JavaScript and CSS into
separate files, then remove those allowances and use a strict nonce or hash
policy.

Do not publish API keys, private credentials, secrets, or personal data in the
static files. Keep third-party scripts and analytics to a minimum.

## Security limitations

CalcPro is not an authenticated financial-management service. It should not be
used as the sole record for accounting, tax, payroll, investment, or payment
decisions.

The website's security depends on the hosting provider serving the files
unchanged over HTTPS and applying the recomme