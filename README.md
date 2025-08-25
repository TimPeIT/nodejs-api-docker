# Node.js API in Docker

Dies ist eine einfache Express-basierte Node.js API, die in einem Docker-Container läuft.

## 🚀 Startanleitung

```bash
# Projekt klonen oder in Ordner wechseln
docker build -t meine-nodejs-api:1.0 .
docker run -d -p 3000:3000 meine-nodejs-api:1.0


    "Works on my machine"-Problem

Ein Docker-Container löst dieses Problem, weil alle Abhängigkeiten, Konfigurationen und Laufzeitumgebungen im Container definiert sind. Es spielt keine Rolle, welches Betriebssystem mein Kollege verwendet – solange Docker installiert ist, funktioniert die Anwendung genau gleich.

    Infrastructure as Code

Das Dockerfile beschreibt präzise, wie meine Anwendung in einem Container gebaut und gestartet wird. Es ist eine "Bauanleitung" für die Infrastruktur, die jederzeit reproduzierbar ist – deshalb wird es auch als Infrastructure as Code bezeichnet.

    Trennung von Code und Abhängigkeiten

Wir kopieren nicht direkt node_modules ins Image, sondern lassen sie im Container mit npm ci installieren. Dadurch stellen wir sicher, dass:

Keine lokalen, plattformspezifischen Abhängigkeiten enthalten sind

Kleinere, saubere Images gebaut werden

Die Installation reproduzierbar über package-lock.json bleibt

    Ports: EXPOSE vs. docker run -p

EXPOSE 3000 im Dockerfile dokumentiert, dass der Container diesen Port verwendet.

docker run -p 3000:3000 verbindet den Container-Port (rechts) mit einem Host-Port (links), sodass du im Browser auf die Anwendung zugreifen kannst.

    Namensräume

Warum ist <username>/<repository> wichtig?

Das Format verhindert Namenskonflikte. Wenn alle einfach my-app nennen könnten, gäbe es Chaos. So gehört jedes Image eindeutig zu einem Benutzer.

    Tag vs. Build

Was ist der Unterschied zwischen docker tag und docker build -t?

docker build -t erstellt ein neues Image mit einem Namen/Tag.

docker tag erstellt keinen neuen Inhalt, sondern vergibt nur ein zusätzliches Etikett für ein bestehendes Image (keine Duplizierung).

    Versionierung

Du hast einen kleinen Fehler behoben – welche Version?

Ich würde :1.0.1 verwenden (semantische Versionierung: PATCH-Level).
Große neue Features → :1.1,
kompatible Änderungen → :1.0.1.

Warum wichtig?
Damit Nutzer gezielt stabile oder neue Versionen nutzen können.

    Öffentlich vs. Privat

Wann würdest du ein privates Repo verwenden?

Bei sensiblen Projekten, internen Tools oder wenn Quellcode nicht öffentlich gemacht werden soll. Zum Beispiel bei CI/CD-Builds mit geheimen Konfigurationen.

## 🔗 Docker Hub

Mein Image ist öffentlich erreichbar unter:  
➡️ [https://hub.docker.com/r/timpeit/my-react-app](https://hub.docker.com/r/timpeit/my-react-app)
