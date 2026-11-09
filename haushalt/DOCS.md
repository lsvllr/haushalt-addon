# Haushalt

## Einstellungen

- **app_url**: öffentliche Adresse, z. B. `https://haus.vollrath.app` (ohne `/` am Ende).
- **secret_key**: Schlüssel für die Anmelde-Cookies. Beim Umzug den bisherigen Wert übernehmen, sonst sind
  alle Geräte abgemeldet. Leer: die App nimmt `.secret_key` aus dem Datenordner oder erzeugt einen.
- **reminder_hour**: ab dieser Stunde (Berliner Zeit) schickt die App die tägliche Erinnerung an Fälliges selbst,
  einmal am Tag je Zuhause. War der Pi zu der Zeit aus, kommt sie nach dem Start am selben Tag.
- **cron_token**: optional. Nur nötig, um `POST /cron/reminders` von außen auszulösen (Test mit `?force=1`).
  Eine HA-Automation dafür braucht es nicht mehr; eine bestehende schadet nicht (kein doppelter Versand).
- **admin_password**: Passwort für `/admin` (Einladungslinks).
- **gemini_api_key**: für den Bon-Scan.
- **allow_legacy_sessions**: alte Sitzungen aus der Zeit vor den Zuhause zulassen.

Nach dem Ändern speichern und das Add-on neu starten.

## Daten

Liegen in `/addon_configs/<id>_haushalt` (Samba-Freigabe `addon_configs`) und sind in den HA-Backups enthalten.
Das Add-on stoppt während eines Backups kurz. SQLite läuft im WAL-Modus: neben `haushalt.db` liegen
`haushalt.db-wal` und `-shm`. Zum Kopieren von Hand das Add-on vorher stoppen.

## Erreichbarkeit

Kein Port nach außen. Im HA-Netz unter `<Hostname>:8000` (Hostname siehe Info-Seite des Add-ons), öffentlich über
das Cloudflared-Add-on (Public Hostname im Tunnel → `http://<Hostname>:8000`). Der Watchdog prüft `/healthz`
und startet das Add-on bei Bedarf neu.
