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

## Screenshots

Sample data.

![Configuration of domains and keys](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/configuration.png)

![Statistics with evaluation per period](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/statistics.png)

![Automatic key rotation](https://raw.githubusercontent.com/it-world/Exchange_Dkim_Manager/master/screenshots/key-rotation.png)

## Features

* **DKIM signing** per domain with RSA (2048, 3072 or 4096 bit), optionally a second signature with
  Ed25519. Key generation or existing PEM keys; configurable algorithm, canonicalization and headers.
* **Automatic key rotation** per domain: the switch happens only after the external DNS shows the
  new key, and every step goes into an audit trail.
* **ARC (RFC 8617):** checks inbound mail (SPF, DKIM, DMARC, ARC) and seals mail that leaves the
  organization again. DMARC aggregate and failure reports.
* **Mail check:** one header `X-ITW-Mail-Check: clean | suspicious | fail` on mail from the Internet,
  for transport rules or a spam filter. Mail is only marked, never blocked.
* **DNS:** suggested records, a check of all domains against internal and external DNS with a PDF
  report, export of all records, optional direct write into Active Directory DNS.
* **Several servers:** sync of configuration and keys from a master to its clients, with combined
  statistics.
* **Statistics and reports:** counters per domain and period, PDF reports, e-mail notifications,
  OpenTelemetry export. Counts only: no addresses are stored.
* **Security:** passwords in the configuration encrypted, own NTFS permissions for keys and backups,
  audit mode with a checked hash chain.
* **Operation:** update check with a `.sha256` check and a backup before every update, backup and
  restore, migration from Exchange DKIM Signer 3.4.0 and 4.4.x, English and German interface.
* **No telemetry:** the program only asks the release repository whether a new version exists.

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
