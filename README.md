# ITW Exchange DKIM Manager

Version **4.6.5.5**

Made in Austria (EU) by IT-world ITW GmbH, Vienna.

## About

ITW Exchange DKIM Manager signs the outgoing mail of a Microsoft Exchange Server with
[DKIM](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail) and seals forwarded mail with
[ARC](https://www.rfc-editor.org/rfc/rfc8617) (Authenticated Received Chain). It consists of
transport agents that run inside the Microsoft Exchange Transport service and a Windows program
(`ITW-DkimManager.exe`) that installs them, manages domains, keys and DNS records, and shows
statistics and logs.

The program sends no telemetry. It only asks the release repository whether a new version exists.

## Features

### DKIM signing

* **ITW Exchange DKIM Signer Agent** signs outgoing mail per domain, using the DKIM implementation
  of [MimeKit](https://mimekit.net/).
* RSA keys of 2048, 3072 or 4096 bit; keys below 2048 bit are refused and the program warns about
  them at every start.
* Optional second signature with **Ed25519** (RFC 8463). Per domain: RSA, Ed25519 or both.
* Key generation for one or all domains, or use of existing PEM keys.
* **Automatic key rotation** per domain in a window of its own: every week up to every year, keys
  created up to 24 months in advance (selector `<yyyyMMdd>_rsa` / `<yyyyMMdd>_ed25519`), a file of the DNS
  records with the date by which each has to be public, the switch only after the external DNS shows the new
  key, then the internal DNS; the old record leaves the internal DNS after 3 days and the old keys are zipped
  with the rotation log. DNS records and keys can be exported, every step is in an audit trail.
* Configurable algorithm, canonicalization and signed headers.
* Changes to the configuration take effect without restarting the transport service.

### ARC (RFC 8617)

* **ITW Exchange ARC Receive Agent** checks inbound mail (SPF, DKIM, DMARC, ARC), removes forged
  `Authentication-Results` and writes its own.
* **ITW Exchange ARC Sealer Agent** seals mail that leaves the organization again (forwarding,
  redirects, distribution lists), optionally the own mail too. It is always the last transport
  agent, directly after the DKIM agent.
* Seals with the DKIM signer's key by default; an own selector, key file or certificate is optional.
* DMARC aggregate reports (rua) and failure reports (ruf, only after a GDPR warning is confirmed).
* **Mail check** (ARC configuration, page Inbound): one header `X-ITW-Mail-Check: clean | suspicious | fail`
  with the single results (`spf=pass dkim=pass dmarc=pass`) on every mail from the Internet, for transport
  rules, Outlook rules or a spam filter. Forged headers of that name are removed; mail is only marked, never
  blocked. Works with the ARC sealer switched off as well.
* Both agents are registered with every installation and update and stay disabled until
  "Activate the ARC sealer" (tab Configuration) or the mail check is switched on.

### DNS

* Suggested TXT records per domain and a check whether they are published, against configurable
  DNS servers.
* **DNS check of all domains**: every selector of every enabled domain in the internal and the
  external DNS, OK / warning / error per selector, with the DMARC record of both sides, and as a
  PDF report for audits (scope, method, overview, notes, page x of y, SHA-256 file).
* **DNS export**: all records grouped by domain, to the clipboard and to `dns-records.txt`.
* Optional direct write of the records into the **Active Directory DNS** over LDAP or LDAPS,
  including creation of the DNS account and the zone permissions.

### Synchronization of several Exchange servers

* Roles **stand-alone, master, client or management** on the Sync tab. Management is a master without
  agents of its own: a server without Exchange or without the transport role that only manages the others.
* The master copies `config.ini` and the keys to its clients over the Windows administrative
  share, manually or automatically after every change; a client can fetch from its master.
* A client with an older version is brought to the master's version.
* Automatic updates can be switched off while the sync is used.

### Statistics and reports

* Counters for processed, signed, failed and unsigned messages, per sending domain, and the ARC
  results (SPF/DKIM/DMARC/ARC pass rates, seals).
* Evaluations per period (day to year or free range) with trend chart, comparison with the previous
  period and an assessment, including the signing time (average, minimum, maximum).
* The Status tab shows since when the transport service runs and the time of the last signature.
* **PDF reports** (monthly, quarterly, annual management report, weekly operations report, e-mail
  security report or custom), written by the program itself.
* With the sync, statistics and reports add up all servers and show a per-server table.
* Counts only: no addresses are stored.
* **E-mail notifications**: error messages from a chosen level (fatal, error, warning) and the PDF
  statistics and forensic reports daily, weekly or monthly by mail, through one SMTP account or one each.
* **OpenTelemetry**: counters and event log entries to a collector over OTLP/HTTP (JSON), with a
  bearer token or an API key if the collector asks for one.

### Security

* Passwords in `config.ini` are stored **encrypted** (AES-256-CBC with HMAC-SHA256); the key is
  `keys\config-secret.key`.
* `keys\` and `backups\` get their own NTFS permissions (SYSTEM and Administrators full control,
  NETWORK SERVICE read).
* The build runs the .NET SDK's security analyzers; a finding stops the build.
* **Audit mode**: every change of a setting goes into `logs\audit.log` with Windows account, computer
  and time; passwords are never written. The audit files carry a SHA-256 hash chain that the program
  checks.

### Update, backup and operation

* **Automatic update** from GitHub or an internal Git server (`UpdateRepository` in `config.ini`),
  with a copy of the installation (program, configuration, keys) in `backups\` before every update;
  the archive is checked against the `.sha256` file of the release before it is unpacked.
* Backup and restore of configuration and keys as a ZIP archive.
* Migration from Exchange DKIM Signer 3.4.0 and 4.4.x. The Migration tab appears only when such an
  installation is found, or when the program is started with `/migration` (or `--migration`).
* Log tab with the agents' event log entries, forensic log (level 5) and all log files in `logs\`.
* Errors and warnings of DKIM and ARC agents in the Windows Application log.
* User interface in English or German, switched at once in the menu **Language / Sprache**; every
  check box, selection, input field, button and submenu - in popups too - explains itself in a tooltip in both languages.
* All settings in one file, `config.ini`.

## Requirements

| Item | Requirement |
|---|---|
| Exchange Server | 2013 CU23 (15.0.1497.2) or later, 2016 CU13 (15.1.1779.2) or later, 2019 RTM (15.2.221.12) or later, Subscription Edition |
| Exchange role | Mailbox server with the Microsoft Exchange Transport service. For the sync role Management a Windows Server without Exchange is enough |
| Operating system | A Windows Server version supported by the Exchange version, with desktop experience (the program has a graphical interface) |
| Runtime | .NET Framework 4.8 and Windows PowerShell (both part of Windows Server) |
| Account | Local administrator on the Exchange server; for the sync also administrator on each client and access to its C$ share (SMB, port 445) |
| DNS | Ability to publish TXT records for the signing domains; optionally written straight into AD-integrated DNS zones (write permission on the zone) |
| Internet | Not needed for signing; only for the optional update check and the DNS check against external DNS servers |

## Installation

1. Download `ITW_Exchange_Dkim_Manager_Setup-<version>.exe` from the
   [releases](https://github.com/it-world/Exchange_Dkim_Manager/releases)
   (or the latest via [dkim-manager.eu/installer](https://dkim-manager.eu/installer)).
2. Run it and confirm the administrator prompt. Read and accept the license (a PDF copy is saved on
   your desktop) and follow the installation. Without the acceptance the program cannot be used.

Alternatively download `ITW_Exchange_Dkim_Manager-<version>.zip`, extract it to a local folder
(**not** into `C:\Program Files`), run `Unblock-DkimManager.ps1` and then `ITW-DkimManager.exe` as
Administrator.

The program installs into `C:\Program Files\ITW Exchange DKIM Manager`. The Microsoft Exchange
Transport service is stopped during the installation, so plan a short break in mail flow. An
installation of the previous generation in `C:\Program Files\Exchange DkimSigner` is moved there,
together with `config.ini`, `keys\` and `backups\`.

Then add your domains, generate keys, publish the DNS records and enable signing.

If the transport service stops with `0x80131515` ("Operation is not supported"), the files are
still blocked:

```powershell
Get-ChildItem "C:\Program Files\ITW Exchange DKIM Manager" -Recurse -File | Unblock-File
Restart-Service MSExchangeTransport
```

Release notes for every version are in the description of each release.

## Support

* Questions, problems and ideas: [GitHub issues](https://github.com/it-world/Exchange_Dkim_Manager/issues).
* Optional paid support by IT-world ITW GmbH: dkim-manager-support@it-world.eu.
* The window **Support information** (About tab) shows both and builds a report to attach.

## Licenses

### ITW Exchange DKIM Manager

Copyright © IT-world ITW GmbH, Vienna, Austria (https://it-world.eu).

The program is **freeware for businesses**, distributed in object code only, under the
*Freeware License Agreement for Businesses* in `LICENSE_EN.txt` (German: `LICENSE_DE.txt`), which
is part of every release archive. In short: free of charge, use by businesses only (not by
consumers or private individuals), no resale, no reverse engineering, no warranty, Austrian law.
The full terms of the license files apply. `DISCLAIMER.md` holds the terms of use.

### Third-party components

The libraries in `build\lib` and the font shipped with the program:

| Component | Version | License | Copyright |
|---|---|---|---|
| MimeKit (`MimeKit.dll`, `MimeKit.xml`) | 4.18.1 | MIT | .NET Foundation and Contributors |
| BouncyCastle.Cryptography | 2.7.0 | MIT | The Legion of the Bouncy Castle Inc. |
| Heijden.Dns | 2.0.0.6 | MIT | (2011, holder not stated in the assembly) |
| System.Buffers | 4.6.1 | MIT | .NET Foundation and Contributors |
| System.Memory | 4.6.3 | MIT | .NET Foundation and Contributors |
| System.Numerics.Vectors | 4.6.1 | MIT | .NET Foundation and Contributors |
| System.Runtime.CompilerServices.Unsafe | 6.1.2 | MIT | .NET Foundation and Contributors |
| Source Sans 3 (font) | | SIL Open Font License 1.1 | Adobe |
| System.Management.Automation | Windows PowerShell 5.1 | Microsoft (see note) | Microsoft Corporation |

The full license texts are in `3rdPartyLicenses.txt` and `SourceSans3-OFL.txt` in every release
archive.

Note: `System.Management.Automation.dll` in `build\lib` is the assembly of the Windows PowerShell
installation and is used for the build. It is not part of the release archive of 4.6.4.136; the
program uses the copy of Windows PowerShell on the server.
