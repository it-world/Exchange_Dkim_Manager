<p align="center">
  <a href="https://dkim-manager.eu/en/">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://dkim-manager.eu/assets/brand/logo-itw-exchange-dkim-manager-invert.svg">
      <img src="https://dkim-manager.eu/assets/brand/logo-itw-exchange-dkim-manager.svg" width="440" alt="ITW Exchange DKIM Manager">
    </picture>
  </a>
</p>

<p align="center">
  <img src="https://dkim-manager.eu/assets/images/flags/at.svg" height="16" alt="Flag of Austria">
  <img src="https://dkim-manager.eu/assets/images/flags/eu.svg" height="16" alt="Flag of the European Union">
  <b>Made in Austria (EU)</b> by IT-world ITW GmbH, Vienna
</p>

# ITW Exchange DKIM Manager

Signs the outgoing mail of a Microsoft Exchange Server with DKIM and seals forwarded mail with ARC.
Transport agents do the work inside the Exchange Transport service; a Windows program installs them
and manages domains, keys, DNS records, statistics and logs.

> [!IMPORTANT]
> **Rules of use: businesses only.**
>
> * **Only businesses** may use this software, and only for business purposes.
>   **Use by consumers or private individuals is prohibited.**
> * **Free of charge, but no resale:** the software may not be sold or offered for a fee, not even
>   as part of another product.
> * **No changes:** no modification and no reverse engineering. The source code is not provided.
> * **No public re-hosting:** do not offer it for public download. IT service providers may install
>   it for customers that are businesses and pass it on complete and unmodified. They may charge for
>   their own services.
> * **No warranty, no claim to support, and liability excluded** as far as the law permits. Use at
>   your own risk and test before productive use.
> * Austrian law applies; the place of jurisdiction is Vienna.
>
> This is a summary. The [license agreement](https://dkim-manager.eu/en/license/) applies in full,
> and in case of doubt the [German version](https://dkim-manager.eu/lizenz/) prevails. Installing or
> using the software means accepting it and confirming that you are a business.

## Features

All screenshots show sample data.

### DKIM signing

* Signs every outgoing mail per domain with RSA (2048, 3072 or 4096 bit), optionally with a second
  signature with Ed25519.
* Generates keys or uses existing PEM keys; algorithm, canonicalization and the signed headers are
  configurable.
* Suggests the DNS records and checks them in the internal and the external DNS.

![Configuration of domains and keys](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/configuration.png)

<details>
<summary>DKIM header configuration, DNS checks</summary>

![DKIM Header Configuration](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/dkim-header-configuration.png)

![External DNS check](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/external-dns-check.png)

![Check DNS of all domains](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/dns-check-all-domains.png)

</details>

### Automatic key rotation

* Changes the keys of a domain by a plan (every week up to every year), with keys created in advance.
* Switches only when every external DNS server shows the new key; the old record is removed after
  the overlap days.
* Every step goes into an audit trail.

![Automatic key rotation](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/key-rotation.png)

### Signatures, banners and disclaimers of ITW Disclaimer

* Inserts the signatures, banners and disclaimers of ITW Disclaimer into outgoing mail before it is
  signed, so the DKIM signature covers them. No extra transport agent.
* Rules from ITW Disclaimer: user before group before domain, internal or external recipients,
  validity times and campaigns; placeholders are filled from the Active Directory.
* Signed or encrypted mail, meeting requests and automatic replies are left as they are. Mode Off,
  Test (chosen senders only) or On on the Sync tab.
* The license of ITW Disclaimer is checked on every server; the master asks the IT-world license
  server over HTTPS, with signed fallback hosts (proxy possible, can be switched off). After the grace of an ended license
  nothing is inserted. Senders are only counted, as a one-way hash.
* No second signature when the Outlook add-in of ITW Disclaimer already inserted one.

### ARC and mail check

* ARC (RFC 8617): checks inbound mail (SPF, DKIM, DMARC, ARC) and seals mail that leaves the
  organization again. DMARC aggregate and failure reports.
* Mail check: one header `X-ITW-Mail-Check: clean | suspicious | fail` on mail from the Internet,
  for transport rules or a spam filter. Mail is only marked, never blocked.

![ARC configuration](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/arc-configuration.png)

### Active Directory DNS

* Writes the DKIM records straight into the Active Directory DNS, with an account of its own that the
  program can create and grant the rights.

<details>
<summary>Active Directory DNS, DNS admin user</summary>

![Active Directory DNS](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/ad-dns-settings.png)

![Create DNS admin user](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/create-dns-admin-user.png)

![Administrator account](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/administrator-account.png)

</details>

### Several servers

* A master hands configuration, keys, program version and the signature bundles of ITW Disclaimer to
  its clients over HTTPS with mutual TLS: pinned certificates, signed manifests, keys encrypted per
  client.
* Combined statistics of all servers.

![Sync](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/sync.png)

### eFa-next

* Sends the DKIM keys and records of the domains to one or many eFa-next filters over their
  provisioning API (mutual TLS, pinned certificate, token), also after every key rotation.

![eFa-next](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/efa-next.png)

### Statistics, reports and notifications

* Counters per domain and period, comparison with the previous period, PDF reports.
* E-mail notifications for errors and reports, OpenTelemetry (OTLP) export.
* Counts only: no addresses are stored.

![Statistics with evaluation per period](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/statistics.png)

<details>
<summary>Domain statistics, PDF report, notifications, OpenTelemetry, log</summary>

![Domain Statistics](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/domain-statistics.png)

![PDF report](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/pdf-report.png)

![E-mail notifications](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/email-notifications.png)

![OpenTelemetry](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/opentelemetry.png)

![Log](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/log.png)

</details>

### Operation and security

* Status of the program and the Exchange transport service, order of the transport agents.
* Update check; every update is checked against its `.sha256` file and, on a signed installation,
  against the signature of IT-world. Backup before every update, return to an earlier release.
* Passwords in the configuration encrypted, own NTFS permissions for keys and backups, audit mode
  with a checked hash chain.
* Migration from Exchange DKIM Signer 3.4.0 and 4.4.x, English and German interface, help for every
  window.
* No telemetry: the program only checks whether a new version exists.

![Status](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/status.png)

<details>
<summary>Advanced configuration, transport agent, releases, backup, support, help, about</summary>

![Advanced Configuration](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/advanced-configuration.png)

![Transport Agent](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/transport-agent.png)

![Earlier releases](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/earlier-releases.png)

![Backup](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/backup.png)

![Support information](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/support-information.png)

![Help](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/help.png)

![About](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/about.png)

</details>

### License and installation

<details>
<summary>License acceptance, installation, license, terms of use</summary>

![License acceptance](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/license-acceptance.png)

![Installation](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/installation.png)

![License](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/license.png)

![Terms of use](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/terms-of-use.png)

</details>

## Requirements

| Item | Requirement |
|---|---|
| Exchange Server | 2013 CU23 or later, 2016 CU13 or later, 2019, Subscription Edition |
| Exchange role | Mailbox server with the Microsoft Exchange Transport service |
| Operating system | A Windows Server version supported by the Exchange version, with desktop experience |
| Runtime | .NET Framework 4.8 and Windows PowerShell |
| Account | Local administrator on the Exchange server |
| DNS | Ability to publish TXT records for the signing domains |

## Installation

1. Download the setup: [dkim-manager.eu/installer](https://dkim-manager.eu/installer).
2. Run it, confirm the administrator prompt, accept the license and follow the installation. The
   Microsoft Exchange Transport service is stopped meanwhile, so plan a short break in mail flow.
3. Add your domains, generate keys, publish the DNS records and enable signing.

If the transport service stops with `0x80131515` ("Operation is not supported"), the files are
still blocked:

```powershell
Get-ChildItem "C:\Program Files\ITW Exchange DKIM Manager" -Recurse -File | Unblock-File
Restart-Service MSExchangeTransport
```

## Support

* Questions, problems and ideas: [GitHub issues](https://github.com/it-world/Exchange_Dkim_Manager/issues). There is no claim to an answer or a fix.
* Optional paid support by IT-world ITW GmbH: dkim-manager-support@it-world.eu.

## License

Copyright © IT-world ITW GmbH, Vienna, Austria (https://it-world.eu). Freeware for businesses, under
the *Freeware License Agreement for Businesses* in `LICENSE_EN.txt` (German: `LICENSE_DE.txt`), part
of every release. Third-party components and their licenses are listed in `3rdPartyLicenses.txt`.
