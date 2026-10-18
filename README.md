ITW Exchange DKIM Manager
> **For use by organisations only.** Private individuals and consumers are not permitted to
> use this software. Anyone who does so nevertheless acts without the permission of the
> provider and is responsible for all consequences of that use themselves.
>
> **No warranty.** This software is provided free of charge and strictly *as is*, without
> warranty of any kind. There is no obligation to supply updates, fix defects, or answer
> support requests. You use it at your own risk. The full terms are in
> **[DISCLAIMER.md](DISCLAIMER.md)**, in German and in English.
DKIM signing for on-premises Microsoft Exchange Server, by it-world GmbH.
The tool configures the transport agent that signs outgoing mail with DKIM, generates and
manages the key pairs, publishes the matching DNS records, and shows how signing is going.
Download
Releases are published as a ZIP archive whose file name carries the version:
```
ITW_Exchange_Dkim_Manager-<version>.zip
```
Download the newest archive from the
Releases page, then:
Extract the archive.
Run `ITW-DkimManager.exe` as Administrator.
Follow the installer. It registers the transport agent, installs the files into
`C:\Program Files\ITW Exchange DKIM Manager`, and writes the DNS records for your domains.
If Windows blocks the executable because it was downloaded, run
`Unblock-DkimManager.ps1` from the same folder as Administrator.
Check for updates
The tool looks for a newer release when it starts and asks whether to install it.
Nothing is downloaded and nothing is changed before that question is answered with Yes.
The checkbox Check for updates at startup on the Status tab switches the question
off; the check itself still runs, so the version and the changelog stay current either way.
```ini
[General]
LogLevel = 3
CheckForUpdatesOnStartup = true
```
A `config.ini` that was written before this option existed has no key for it, and reads as
the default, which is on. A value that is neither `true` nor `false` is ignored rather than
guessed at.
When it does not start
`ITW-DkimManager.exe --debug` writes `dkim-manager-debug.log` next to the executable. The
file is opened before anything else happens and records the command line, the paths, the
operating system, the runtime and the assembly version, and for the installation folder
whether it exists and whether it holds a `config.ini` and a `keys` folder.
A failure before the window opens produces a message box with the exception and the path of
the log instead of nothing. The file is also written when the program runs into trouble
later, while the window is already up.
```powershell
& "C:\Program Files\ITW Exchange DKIM Manager\ITW-DkimManager.exe" --debug
```
The file is written with the time in front of every line. The clearest report comes from a
start that fails, and it is the one that is hardest to get.
