# Meine Medikamente – Offline PWA und iOS-Vorbereitung

## Auf dem iPhone testen (ohne Mac)

1. Den Inhalt dieses Ordners unverändert auf einen **HTTPS-Webhost** (z. B. Netlify Drop oder Cloudflare Pages) hochladen. Eine ZIP-Datei muss ggf. zuerst entpackt werden.
2. Die HTTPS-Adresse in **Safari** öffnen und einmal vollständig laden.
3. Über **Teilen → Zum Home-Bildschirm** installieren.
4. Flugmodus aktivieren und die App erneut vom Home-Bildschirm starten. Medikamente, Häkchen, Verlauf und Backups funktionieren offline.

Eine lokale `file://`-Datei oder eine ZIP-Datei direkt auf dem iPhone aktiviert keinen Service Worker; daher ist eine einmalige HTTPS-Bereitstellung erforderlich. Diese Ausgabe ist ein Quellcodepaket, keine veröffentlichte Website und keine signierte iPhone-App.

## iOS-App für TestFlight / App Store

- `npm install`
- Die Beispiel-Bundle-ID in `capacitor.config.json` auf eine eigene eindeutige ID ändern.
- `npx cap add ios && npx cap sync ios`
- Das iOS-Projekt in Xcode oder einem dafür geeigneten macOS-Cloud-Build-Dienst bauen, signieren und testen.
- Apple Developer Program, App Store Connect, Datenschutzangaben, Screenshots, Prüfung und ggf. TestFlight sind erforderlich.
- Native Erinnerungen werden über `@capacitor/local-notifications` angefordert. Auf einem echten iPhone testen und Benachrichtigungsrechte gewähren. Die PWA zeigt **keine verlässlichen automatischen Hintergrundalarme**.

## Wichtige Hinweise

- Ein Einnahmezeitpunkt pro Eintrag; täglich, ausgewählte Wochentage, alle X Tage oder monatlich an einem Kalendertag. Mehrere Zeiten können als separate Einträge angelegt werden. Die optionale Darreichungsform kann z. B. Tablette oder Pen sein. Native Erinnerungen sind im Beispiel derzeit nur für tägliche Einträge vorgesehen; andere Rhythmen benötigen vor App-Store-Veröffentlichung eine erweiterte native Terminplanung.
- Daten liegen ausschließlich im lokalen Gerätespeicher (`localStorage`). **Regelmäßig JSON-Backup exportieren**; Browserdaten-Löschung oder Deinstallation können Daten vernichten. Keine Cloud-Synchronisierung.
- Die App ist eine Dokumentationshilfe, kein Medizinprodukt oder Ersatz für ärztliche Anweisungen. Für den App Store müssen Funktionen, Datenschutz, Barrierefreiheit und App-Review-Vorgaben noch geprüft werden.
- Vor einer produktiven Veröffentlichung sollte `webDir` in einen dedizierten Build-Ordner umgestellt und die nativen Build-/Signing-Einstellungen vervollständigt werden. Die aktuelle Konfiguration ist ein **Startprojekt**, keine garantiert einreichungsfertige IPA.
