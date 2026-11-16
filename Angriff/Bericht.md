# Angriff auf die HTL Braunau
## Metainformationen
### Verfasser: David Weinberger & Lukas Haselberger & Simon Klingesberger & Flori Bub Zöhner
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


