# Django-Tenants Test

[Alle Informationen kommen von dieser Dokumentation](https://books.agiliq.com/projects/django-multi-tenant/en/latest/introduction.htmll)

## Shared Database with shared schema

Bei dieser Art wird ein Tenant Model erstellt, von diesem Model erben alle anderen Datenhalter Model.
Die Tenants werden über eine Subdomain identifiziert, heisst:
Wenn der name der Webseite www.example.com ist, dann findet man die Daten von Potter unter potter.example.com und die Daten von Thor auf thor.example.com.
Wenn wir nun Daten erstellen müssen wir für jeden erstellten Datensatz den Tenant angeben, damit die Daten nur auf der Subdomain zu sehen sind.
Die Nachteile bei dieser Methode sind:
* Schlechte aufteilung der Tenants Daten
* Redundanter Code
Die Vorteile bei dieser Methode sind:
* Es ist relativ leicht zu implementieren.
* Es ist gut für kleinere Applikationen.

## Shared Database with isolated schema

Bei dieser Art wird für jeden Tenant ein Schema in der Datenbank kreiert. Diese Schemas sind verlinkt mit urls, auf welchen die Tenants dann ihre Daten erstellen und abspeichern.
Die Implementation ist etwas komplizierter und ist nicht mit einer SQLite Datenbank möglich. In meinem Beispiel habe ich es mit einer Postgres Datenbank umgesetzt.
Das Gute ist, dass die Schemen komplett unabhängig voneinander sind, dass heisst man könnte ein Schema pro Benutzergruppe erstellen und könnte so berechtigungs Probleme erleichtern.
Diese Art löst alle Probleme der vorherigen art und Sie wird in der Dokumentation als beste Variante betitelt.
Diese Art ist leicht auszubauen oder anzupassen.

## Isolated database with shared app server

Diese Art ist gleich wie die Art mit dem isolierten Datenbankschema, jedoch wird bei dieser Art für jeden Tenant eine Datenbank kreiert.

## Completly isolated tenants using Docker

Bei dieser Art wird für jeden Tenant ein ganzer Datenbankserver, auf einem Dockercontainer, gestartet.
Diese Methode scheint bei vielen Tenants eher umständlich, da für jeden Tenants ein dockercontainer gestartet werden muss.

## Fazit

In der Dokumentation wird gesagt, dass die 2 Art die beste sei, weil es gute isolationsmöglichkeiten der Daten bietet, weil es einfach veränder- und erweiterbar ist und weil es fast keinen Aufwand braucht neue Tenants zu erstellen.
