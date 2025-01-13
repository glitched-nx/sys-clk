# sys-clk

Ein Switch-Systemmodul, mit dem du CPU/GPU/RAM-Takte entsprechend der laufenden Anwendung und dem Dock-Status einstellen kannst.

## Installation

Die folgenden Anweisungen setzen voraus, dass du eine Nintendo Switch mit Atmosphère besitzt, die mindestens auf die neueste stabile Version aktualisiert ist.
Kopiere die Ordner `atmosphere` und `switch` in das Hauptverzeichnis deiner SD-Karte und überschreibe Dateien, wenn du dazu aufgefordert wirst. Kopiere auch den `config`-Ordner, wenn du nicht aktualisierst, um die Standardeinstellungen zu übernehmen.

**Hinweis:** Für sys-clk-overlay muss [Tesla](https://gbatemp.net/threads/tesla-the-nintendo-switch-overlay-menu.557362/) installiert und aktiv sein

## Wichtige Dateien

* Konfigurationsdatei zum Einstellen eigener Takte je nach Dock-Status und Titel-ID, wie unten beschrieben

    `/config/sys-clk/config.ini`

* Log-Datei für Protokolle, wenn aktiviert

    `/config/sys-clk/log.txt`

* Log-Flag-Datei aktiviert die Protokollierung, wenn sie existiert

    `/config/sys-clk/log.flag`

* CSV-Datei für Titel-ID, Profil, Takte und Temperaturen, wenn aktiviert

    `/config/sys-clk/context.csv`

* sys-clk Manager-App (über das hbmenu erreichbar)

    `/switch/sys-clk-manager.nro`

* sys-clk Overlay (überall über das [Tesla-Menü](https://gbatemp.net/threads/tesla-the-nintendo-switch-overlay-menu.557362/) erreichbar)

    `/switch/.overlays/sys-clk-overlay.ovl`
    
* sys-clk Kern-Systemmodul

    `/atmosphere/contents/00FF0000636C6BFF/exefs.nsp`
    `/atmosphere/contents/00FF0000636C6BFF/flags/boot2.flag`

## Konfiguration

Du kannst Voreinstellungen in der INI-Konfigurationsdatei unter `/config/sys-clk/config.ini` anpassen. Nutze dafür diese Vorlage für jede App:

```
[Application Title ID]
docked_cpu=
docked_gpu=
docked_mem=
handheld_charging_cpu=
handheld_charging_gpu=
handheld_charging_mem=
handheld_charging_usb_cpu=
handheld_charging_usb_gpu=
handheld_charging_usb_mem=
handheld_charging_official_cpu=
handheld_charging_official_gpu=
handheld_charging_official_mem=
handheld_cpu=
handheld_gpu=
handheld_mem=
```

* Ersetze `Application Title ID` mit der Titel-ID des Spiels/der Anwendung, die du anpassen möchtest.
Eine Liste der Spiele-Titel-IDs findest du im [Switchbrew Wiki](https://switchbrew.org/wiki/Title_list/Games).
* Frequenzen werden in MHz angegeben und auf die nächstmöglichen Werte angepasst (siehe Takttabelle unten).
* Wenn ein Schlüssel fehlt, leer ist oder auf 0 steht, wird er ignoriert und die Standardtakte werden verwendet.
* Beim Laden sucht sys-clk die Frequenzen in dieser Reihenfolge und nimmt die erste gefundene:
    1. Ladegerät-spezifische Einstellung (USB oder Offiziell) `handheld_charging_usb_X` oder `handheld_charging_official_X`
    2. Allgemeine Ladeeinstellung `handheld_charging_X`
    3. Handheld-Einstellung `handheld_X`