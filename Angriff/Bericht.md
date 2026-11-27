# Angriff auf die HTL Braunau
## Metainformationen
### Verfasser: David Weinberger & Lukas Haselberger & Simon Klingesberger & Flori Bub Zöhner(nicht performativ)
### Klasse: 5AHITS
### Fach: ITSE-Labor

## Idee bzw. Ideenerweiterung
Die Anfangsidee war es, dass wir eine Website bauen, welche dann einen Login durch Benutzername und Passwort bietet und man dann durch die Anmeldung an einem Gewinnspiel der HTL Braunau teilnehmen kann, wo man einen 100 Euro Buffetgutschein gewinnen kann.           

Dann haben wir weiterhin überlegt, das noch auszubauen, damit man auch die Klasse angeben muss, da dann der Reiz steigen würde, mehrere Leute aus seiner Klasse für das Gewinnspiel zu motivieren.       
Da eine Website zu bauen und auch eine Domain zu hosten eher auffällig ist, und doch vielen Schülern auffallen wird, haben wir uns jetzt überlegt, dass wir eine Umfrage machen mit Microsoft Forms. In dieser Umfrage wird dann ein Feld für Benutzername, Passwort und Klasse erscheinen, damit der Gewinner dann auch erreicht werden kann.       

Anschließend haben wir herausgefunden, wie wir die E-Mails verschicken können, ohne dass bei der E-Mail dabei steht, dass sie von "Extern" gesendet wurde. Und zudem ist es auch auffällig, wenn die Absender-E-Mail-Adresse irgendeine fremde E-Mail-Adresse ist. Allerdings haben wir herausgefunden, dass es einen automatischen Phishing-Schutz bei den Microsoft Forms Umfragen gibt, dadurch kann man dann kein Passwort eingeben, wenn die E-Mail von einer Schul-E-Mail kommt.       

### Fertige Idee
Geeinigt haben wir uns am Ende darauf, von einer externen E-Mail zu schicken und eine Domain zu kaufen und anschließend per Vibe-Coding eine Website zu erstellen. Wir haben uns gedacht, da das Buffet sowieso eingemietet ist und eine andere Firma mit einer anderen E-Mail sein könnte, werden wir uns eine realistische E-Mail erstellen, welche "Buffet-HtlBraunau" oder so ähnlich heißt. 

## Programme
### Ausgabe der Schüler der HTL-Braunau
```
var emailSchueler = from s in db.Schueler

                    where !s.Klassen.Name.StartsWith("5")

                    select s.EMailAdresse1;

Console.WriteLine(emailSchueler.Count());

foreach(string e in emailSchueler)

{
    Console.WriteLine(e);
}
```
### Ausgabe der Lehrer der HTL-Braunau
```
var emailLehrer = from l in db.Lehrer
                  select l.EMailAdresse;

Console.WriteLine(emailLehrer.Count());

foreach (string e in emailLehrer)
{
    Console.WriteLine(e);
}
```
## Bau der Website
 
### Technischer Aufbau
 
Die Website ist eine einzelne statische HTML-Datei (`index.html`) mit eingebettetem
CSS und JavaScript – also ohne Framework. Dadurch ist sie schnell, leicht zu hosten
und überall lauffähig. Optisch orientiert sie sich an einer typischen
Microsoft-/Schul-Anmeldeseite: eine weiße Karte in der Mitte, dahinter ein
Vollbild-Foto der Schule als Hintergrund und das HTL-Logo oben.
 
### Mehrstufiger Anmeldeablauf
 
Statt alle Felder auf einmal zu zeigen, führt die Seite Schritt für Schritt durch den
Vorgang – genau wie echte Login-Dienste. Die einzelnen Schritte werden per JavaScript
ein- und ausgeblendet:
 
1. **E-Mail-Adresse** – Eingabe und Prüfung, ob die Adresse auf `@htl-braunau.at` endet.

2. **Kennwort** – wird eingegeben, aber bewusst **nicht gespeichert und nicht übertragen**.

3. **Rolle** – Auswahl zwischen *Schüler* und *Lehrer*.

4. **Klasse** (nur für Schüler) – zuerst Jahrgang wählen, danach erscheinen im zweiten
   Dropdown automatisch die passenden Klassen dieses Jahrgangs. Lehrer überspringen
   diesen Schritt.

5. **Danke-Seite** – Bestätigung der „Anmeldung".
 
### Design-Details für mehr Realismus
 
- **Hintergrundfoto + Abdunkelung:** Das Schulfoto füllt den Bildschirm, eine leichte
  dunkle Ebene darüber hält die weiße Karte gut lesbar.

- **Lade-Rad (Spinner):** Nach dem Absenden einzelner Schritte (Passwort, Rolle,
  Klasse) erscheint kurz ein drehendes Lade-Rad, bevor es weitergeht. Das wirkt wie
  ein echter Server-Vorgang.

- **Abhängige Dropdowns:** Die Klassen sind je Jahrgang hinterlegt, sodass immer nur
  real existierende Klassen zur Auswahl stehen.
 
### Speicherung der Eingaben
 
Bei der Datenspeicherung haben wir mehrere Varianten durchlaufen:
 
1. **Lokal (erste Version):** Ein kleiner Python-Server (`server.py`) bzw. ein
   PHP-Skript (`save.php`) nahm die Eingaben entgegen und schrieb sie in eine
   CSV-Datei (`anmeldungen.csv`). Eine `.htaccess`-Datei sperrte den direkten
   Browser-Zugriff auf diese Datei.

2. **Problem beim Online-Hosting:** Die Domain läuft auf **Vercel**. Vercel führt
   jedoch **kein PHP** aus und erlaubt **kein dauerhaftes Schreiben von Dateien** –
   die CSV-Lösung funktionierte dort also nicht.

3. **Finale Lösung – Google Sheet:** Die Seite sendet die Eingaben per `fetch` an ein
   **Google-Apps-Script** (Web-App), das jede Anmeldung als neue Zeile in ein
   **Google Sheet** schreibt. So sind die Daten sofort in einer Tabelle sichtbar,
   ganz ohne eigenen Server.
 
Gespeichert werden ausschließlich **Zeitstempel, E-Mail, Rolle und Klasse** – das

**Passwort wird an keiner Stelle gespeichert oder verschickt**. Zusätzlich prüft auch
das Skript serverseitig, dass nur `@htl-braunau.at`-Adressen übernommen werden.
 
### Hosting und Veröffentlichung
Der Code liegt in einem GitHub-Repository. Die Domain wird über **Vercel**
bereitgestellt, das bei jedem Push automatisch die neueste Version veröffentlicht
(Continuous Deployment). Eine Änderung am Code ist dadurch nach kurzer Zeit live.
 





