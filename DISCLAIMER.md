Nur für Unternehmen – Haftungsausschluss & Nutzungsbedingungen (Disclaimer)
ITW Exchange DKIM Manager
> **Nur zur Nutzung durch Unternehmen. Privatpersonen und Verbrauchern ist die Nutzung dieser
> Software nicht gestattet.**
---
Deutsch
1. Nur zur Nutzung durch Unternehmen (keine Privatnutzung)
Diese Software ist ausschließlich für die Nutzung durch Unternehmen bestimmt. Unternehmen in diesem Sinne sind juristische Personen des öffentlichen Rechts, Gesellschaften des bürgerlichen Rechts sowie Personen, die im Rahmen ihrer beruflichen oder wirtschaftlichen Tätigkeit handeln.
Privatpersonen und Verbraucher im Sinne des europäischen Verbraucherrechts sind zur Nutzung dieser Software nicht berechtigt. Dies ist keine Empfehlung, sondern eine ausdrückliche Bedingung der Bereitstellung.
Wer diese Software dennoch nutzt, handelt ohne Erlaubnis des Anbieters und trägt die Verantwortung für alle Folgen dieser Nutzung selbst. Der Anbieter übernimmt für eine solche Nutzung keinerlei Rechte, Pflichten oder Haftungen; die Haftungsbeschränkungen der Punkte 4 und 5 bleiben davon unberührt, soweit sie wirksam sind.
2. Unentgeltliche Bereitstellung ("As Is")
Diese Software wird Ihnen völlig unentgeltlich und kostenlos zur Verfügung gestellt. Es besteht keinerlei vertragliche Bindung oder ein Anspruch auf Bereitstellung, Nutzung, Weiterentwicklung, Updates oder Support.
3. Ausschluss der Gewährleistung
Die Software wird im IST-ZUSTAND ("AS IS") und ohne jegliche ausdrückliche oder stillschweigende Gewährleistung bereitgestellt. Der Nutzer trägt das gesamte Risiko hinsichtlich der Qualität, Leistungsfähigkeit und Fehlerfreiheit der Software.
4. Haftungsbeschränkung
Soweit gesetzlich zulässig (nach österreichischem Recht und EU-Recht), schließen die Autoren bzw. Betreiber dieses Repositories jegliche Haftung für direkte oder indirekte Schäden, Datenverluste, Betriebsausfälle oder Folgeschäden aus, die durch die Nutzung oder Nichtnutzung dieser Software entstehen. Eine Haftung für Vorsatz und grobe Fahrlässigkeit bleibt unberührt, sofern zwingendes Recht dies vorschreibt.
5. Keine Update- oder Wartungspflicht
Es gibt zu keinem Zeitpunkt eine Verpflichtung, Fehler zu beheben, Sicherheitsupdates bereitzustellen, neue Funktionen zu implementieren oder Supportanfragen zu beantworten. Die Nutzung erfolgt auf eigene Gefahr.
Hinweise zur Nutzung
Vor dem Einsatz auf einem Produktivserver. Diese Software verändert ausgehende E-Mails und schreibt in die DNS-Zone Ihrer Domäne. Beides ist ein Eingriff in eine bestehende Infrastruktur. Erstellen Sie vor dem ersten Einsatz eine Sicherung der Konfiguration und der DNS-Einträge. Die Werkzeuge dafür finden Sie in der Anwendung selbst unter Backup configuration und Export DNS records.
Transportschicht. Der Agent läuft als Teil von Microsoft Exchange und greift in die Nachrichtenverarbeitung ein. Testen Sie eine Version immer zuerst in einer Testumgebung.
Verfügbarkeit. Da keine Wartungspflicht besteht, kann ein Update jederzeit ausbleiben. Eine Änderung der Exchange-Version kann die Anpassung des Agents erfordern.
---
English
> **For use by organisations only. Private individuals and consumers are not permitted to use
> this software.**
1. Business Use Only (No Private Use)
This software is intended exclusively for use by organisations. Organisations in this sense are legal entities under public law, companies under private law, and persons acting in the course of their professional or commercial activity.
Private individuals and consumers within the meaning of European consumer law are not entitled to use this software. This is not a recommendation but an express condition of the provision.
Anyone who nevertheless uses this software acts without the permission of the provider and bears sole responsibility for all consequences of that use themselves. The provider accepts no rights, duties or liabilities for such a use; the limitations of liability under points 4 and 5 remain unaffected to the extent that they are valid.
2. Provided Free of Charge ("As Is")
This software is provided to you completely free of charge and at no cost. There is no contractual relationship of any kind and no entitlement to provision, use, further development, updates or support.
3. Disclaimer of Warranty
The software is provided IN THE STATE IT IS ("AS IS") and without any express or implied warranty of any kind. The user bears the entire risk with regard to the quality, performance and correctness of the software.
4. Limitation of Liability
To the extent permitted by law (Austrian law and EU law), the authors or operators of this repository exclude any liability for direct or indirect damage, loss of data, downtime or consequential damage arising from the use or non-use of this software. Liability for intent and gross negligence remains unaffected where mandatory law so requires.
5. No Obligation to Update or Maintain
At no time is there an obligation to fix defects, to supply security updates, to implement new features or to answer support requests. Use is at your own risk.
Notes on use
Before use on a production server. This software modifies outgoing email and writes into the
DNS zone of your domain. Both are interventions in an existing infrastructure. Create a backup
of the configuration and of the DNS entries before the first use. The tools for this are in the
application itself, under Backup configuration and Export DNS records.
Transport layer. The agent runs as part of Microsoft Exchange and takes part in message
processing. Always test a version in a test environment first.
Availability. Because there is no maintenance obligation, an update may be missing at any
time. A change of the Exchange version can require the agent to be adapted.
---
Lizenz / Licence
Die Bibliotheken Dritter, die mitgeliefert werden, stehen unter ihren eigenen Lizenzen.
Die wichtigsten sind:
The third party libraries that are delivered with it are under their own licences.
The most important ones are:
Bibliothek / Library	Lizenz / Licence
MimeKit	MIT
BouncyCastle .NET	MIT
Heijden.Dns	MIT
