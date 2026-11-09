# Haushalt

## Einstellungen

- **app_url**: öffentliche Adresse, z. B. `https://haus.vollrath.app` (ohne `/` am Ende).
- **secret_key**: Schlüssel für die Anmelde-Cookies. Beim Umzug den bisherigen Wert übernehmen, sonst sind
  alle Geräte abgemeldet. Leer: die App nimmt `.secret_key` aus dem Datenordner oder erzeugt einen.
- **cron_token**: Token für `POST /cron/reminders` (tägliche Erinnerung, HA-Automation mit `rest_command`).
- **admin_password**: Passwort für `/admin` (Einladungslinks).
- **gemini_api_key**: für den Bon-Scan.
- **allow_legacy_sessions**: alte Sitzungen aus der Zeit vor den Zuhause zulassen.

Nach dem Ändern speichern und das Add-on neu starten.

## Daten

Liegen in `/addon_configs/<id>_haushalt` (Samba-Freigabe `addon_configs`) und sind in den HA-Backups enthalten.
Das Add-on stoppt während eines Backups kurz.

## Erreichbarkeit

Kein Port nach außen. Im HA-Netz unter `<Hostname>:8000` (Hostname siehe Info-Seite des Add-ons), öffentlich über
das Cloudflared-Add-on (Public Hostname im Tunnel → `http://<Hostname>:8000`).
