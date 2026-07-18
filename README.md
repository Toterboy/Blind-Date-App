# Blind-Date-App
A privacy-focused dating app built with Flutter that prioritizes personality over looks, featuring E2E encryption, blind matching modes, and a daily live "Dating Hour" event. This project is still under active development and not yet fully functional, contributions and feedback are welcome.

Eine moderne Dating-App, die auf **Persönlichkeit vor Aussehen** setzt. Statt sich nur auf Fotos zu verlassen, kombiniert die App intelligentes Matching, verschiedene Kennenlern-Modi und ein starkes Sicherheitskonzept, um authentischere Verbindungen zu ermöglichen.

## Über die App

Blind Date App ist für **Android, iOS und Web** konzipiert und basiert auf **Flutter**, **Riverpod** (State Management) und **go_router** (Navigation) im **Material 3** Design.

---

## Kernfunktionen

### Onboarding & Registrierung
- Einführungs-/Erklärungsscreen (nur beim allerersten App-Start)
- Registrierung mit Name, E-Mail (Domain-Validierung), Passwort, Geburtsdatum (Tag/Monat/Jahr), Geschlecht
- **Einladungscode-Pflicht** bei der Registrierung (Bot-Schutz) – Codes werden vom Entwickler vergeben oder durch Einladungslinks von bestehenden Nutzern generiert
- **Video-Verifizierung** mit Liveness-Check nach der Registrierung
- Einmalige Standort-Abfrage zur Fake-Account-Erkennung
- Persönlichkeitstest (MBTI-Style, z. B. ENTP, INFJ) als Teil der Einrichtung nach der Registrierung
- Fortschrittsanzeige während der Einrichtung (Schritt-Format statt unschöner Prozent-Nachkommastellen)
- Zurück-Button zwischen den Einrichtungsschritten

### Matching-Algorithmus
- Zentraler, gewichteter Matching-Score basierend auf:
  - Entfernung (km, Bundesland oder ganz Deutschland wählbar)
  - Gemeinsame Interessen
  - Persönlichkeits-Kompatibilität (MBTI-Matrix)
  - Alter innerhalb der gewählten Präferenzen
- Strikte Geschlechts- und Altersfilter (keine falschen Vorschläge)

### Swipe-Modi
1. **Klassischer Swipe-Modus** – mit Untermenü für Bilder, Video, Audio oder nur Text (Video/Audio vorerst deaktiviert)
2. **Zufallschat-Modus** – automatische Zuordnung zu einem Text-Chat basierend auf Alter/Distanz-Einstellungen
3. **Dating Hour (Event-Modus)** – täglich 20:00–21:00 Uhr:
   - Beitritt ab 19:50 Uhr möglich
   - Zwei zufällig zugeordnete Personen chatten direkt (ohne Profilansicht)
   - Nach 5 Minuten: beide können "Annehmen" oder "Ablehnen"
   - Match nur, wenn BEIDE annehmen
   - Freundlich formulierte Ablehnungs-Nachricht bei Absage
   - Individuelle Präferenzen (Alter, Geschlecht, besondere Eigenschaft) vor Event-Start einstellbar

### Sicherheit & Datenschutz
- **Ende-zu-Ende-Verschlüsselung** aller Chat-Nachrichten via Signal Protocol
- **Peer-to-Peer-Kommunikation** (WebRTC) für Event- und Zufallschat-Modus
- Foto-Moderation: automatischer Abgleich mit Verifizierungs-Video (Verwarnung bei Nicht-Übereinstimmung, Sperre bei zweitem Vorfall)
- Nacktbilder/-videos führen zur sofortigen Account-Sperre
- Altersschutz-System:
  - Ab 20 Jahren keine Sichtbarkeit von 16-/17-Jährigen mehr
  - Minderjährige (16–17) können ihren Filter nur bis max. 20 Jahre einstellen
  - Profilfotos von 16–17-Jährigen nur für Gleichaltrige sichtbar
  - Profilfotos von 18–19-Jährigen nur nach Match sichtbar (nicht deaktivierbar)
  - Automatische Freischaltung aller Funktionen mit Erreichen des 20. Lebensjahres
- "Nutzer melden"-Funktion in Chats und Profilen
- "Match auflösen"-Button in jedem Chat (mit Sicherheitsabfrage)

### Aktuelles-Screen
- Übersicht über neue Nachrichten (bis 5 Personen mit Profilbild), neue Likes und neue Matches (einheitliche Feldbreiten, dynamische Höhe)
- Eigener Likes-Screen mit getrennten Listen: vergebene Likes vs. erhaltene Likes (vergebene Likes zurückziehbar)
- Zugriff auf Einstellungen über Zahnrad-Icon
- Zentraler "Leute entdecken"-Button

### Chat-Funktionen
- Text-, Bild- und Sprachnachrichten
- Audio-Anrufe innerhalb der App
- Navigation zum Profil durch Klick auf Name/Profilbild
- Blind-Chat-Option für nicht beantwortete Likes

### Profil
- Mehrere Profilbilder
- Zahnrad-Icon für direkten Zugriff auf Einstellungen
- Profil-Vorschau-Funktion (Ansicht wie andere Nutzer das Profil sehen)
- Spenden-Button mit "Spender"-Badge nach abgeschlossener Spende
- "App empfehlen"-Button mit "Empfehler"-Badge nach erfolgreichem Teilen
- Eigenes Geschlecht nur hier änderbar (nicht in den Einstellungen)

### Einstellungen
- Klare visuelle Kennzeichnung ausgewählter Optionen (Privatsphäre, Darstellung)
- Zentral synchronisierte Präferenzen (Geschlecht-Präferenz, Alter, Entfernung) zwischen Einrichtung und Einstellungen

### Swipe-Screen
- Undo-Button (links vom X-Button, ab erstem Swipe sichtbar, zunächst ausgegraut)
- Anzeige des Persönlichkeitstyps auf der Karte, falls vorhanden
- Spender-/Empfehler-Badges neben dem Alter

---

## Tech-Stack

| Bereich | Technologie |
|---------|-------------|
| Framework | Flutter (Android, iOS, Web) |
| State Management | Riverpod |
| Navigation | go_router |
| Design | Material 3 |
| Verschlüsselung | Signal Protocol (libsignal_protocol_dart) |
| Peer-to-Peer | WebRTC (flutter_webrtc) |
| Medien-Sharing | image_picker, record / flutter_sound |
| App-Weiterempfehlung | share_plus |

---

## Projektstruktur (Auszug)

```
lib/
├── models/
│   ├── user.dart
│   ├── personality_type.dart
│   ├── blind_chat.dart
│   ├── dating_hour_session.dart
│   ├── invitation_code.dart
│   └── verification_video.dart
├── services/
│   ├── matching_service.dart
│   ├── encryption_service.dart
│   ├── webrtc_service.dart
│   ├── verification_service.dart
│   ├── dating_hour_service.dart
│   └── content_moderation_service.dart
├── utils/
│   └── age_calculator.dart
├── providers/
│   └── user_preferences_provider.dart
└── screens/
    ├── onboarding/
    ├── swipe/
    ├── chat/
    ├── matches/
    ├── aktuelles/
    ├── profile/
    └── settings/
```

---

## Hinweis zum Entwicklungsstand

Diese App befindet sich in aktiver Entwicklung. Folgende Bereiche sind aktuell als **Platzhalter/Mock** implementiert und müssten für eine echte Produktionsversion durch professionelle Dienste ersetzt werden:

- Automatischer Gesichtsabgleich (Profilbild vs. Verifizierungs-Video) → z. B. AWS Rekognition, Google Cloud Vision
- Content-Moderation für unangemessene Inhalte → z. B. Google Cloud Vision SafeSearch
- Zahlungsabwicklung für Spenden-Funktion (aktuell Mock-Zahlung)

---

## Lizenz

Dieses Projekt steht unter der GNU Affero General Public License v3.0 (AGPLv3).

Das bedeutet insbesondere:
- Der Code darf verwendet, verändert und weiterverbreitet werden.
- Wird die Software (auch als Server-/Cloud-Dienst) genutzt oder verändert, muss der 
  Quellcode ebenfalls unter der AGPLv3 offengelegt werden.
- Eine kommerzielle Nutzung als geschlossenes, proprietäres Produkt ist damit ausgeschlossen.

---

## Kontakt

Bei Fragen oder Vorschlägen gerne ein Issue im Repository erstellen.
