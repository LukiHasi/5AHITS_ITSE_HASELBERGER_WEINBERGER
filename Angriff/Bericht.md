# Angriff auf die HTL Braunau
## Metainformationen
### Verfasser: David Weinberger & Lukas Haselberger & Simon Klingesberger & Flori Zöhner
### Klasse: 5AHITS
### Fach: ITSE-Labor

## Idee bzw. Ideenerweiterung
Die Anfangsidee war es das wir einen Website bauen welche dann einen login durch Benutzername und Passwort bietet und man dann durch die Anmeldung an einem Gewinnspiel der HTL Braunau teilzunehmen, wo man einen 100 Euro Buffetgutschein gewinnen kann.           

Dann haben wir weiterhin überlegt dass noch auszubauen damit man auch die Klasse angeben muss, da dann der Reiz steigen würde mehrere Leute aus seiner Klasse für das Gewinnspiel zu motivieren.       
Dadurch eine Website zu bauen und auch einen Domäne zu hosten eher auffällig ist, und doch vielen Schülern auffallen wird, haben wir uns jetzt überlegt dass wir eine Umfrage machen mit Microsoft Forms. In dieser Umfrage wird dann ein Feld für Benutzername, Passwort und Klasse erscheinen, damit der Gewinner dann auch erreicht werden kann.       

Anschließend haben wir herausgefunden wie wir die Emails verschicken können ohne dass bei der Email dabei steht dass es von "Extern" gesendet wurde. Und zudem ist es auch auffällig wenn die Absender Email Adresse irgendeine fremde Email Adresse ist. Allerdings haben wir herausgefunden dass es einen automatischen fishing Schutz bei den Microsoft Forms Umfragen gibt, dadurch kann man dann kein Passwort eingeben, wenn die Email von einer Schulemail kommt.       

### Fertige Idee
Geeinigt haben wir uns am Ende darauf von einer externen Email zu schicken, und eine Domäne zu kaufen und anschließend per Vibe-Coding eine Website zu erstellen. Wir haben uns Gedacht da das Buffet sowieso eingemietet ist und eine andere Firma mit einer anderen Email sein könnte, werden wir uns eine realistische Email erstellen, welche "Buffet-HtlBraunau" oder so ähnlich heißt. 

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
