# 🧱 zer0.de's Docker Media Stack

Ein vollständiges, selbstgehostetes Medien-Ökosystem – automatisiert und über VPN geschützt.

---

## 📌 Features

- ✅ Gluetun VPN (z. B. Mullvad, Surfshark)
- ✅ qBittorrent & SABnzbd (VPN-basiert)
- ✅ Radarr, Sonarr, Prowlarr – vollautomatische Verwaltung
- ✅ Watchtower für Container-Aktualisierung
- ✅ Heimdall als Startseite
- ✅ Portainer für Container-Management
- ✅ LAN-Zugriff trotz VPN dank `LOCAL_NETWORK`

---

## 📁 Ordnerstruktur

```
./
├── docker-compose.yml
├── README.md
└── config/
    ├── gluetun/
    │   └── custom.conf           # <- deine .ovpn umbenennen!
    ├── radarr/
    ├── sonarr/
    ├── sabnzbd/
    ├── qbittorrent/
    ├── portainer/
    ├── heimdall/
    └── Downloads/
        ├── complete/
        ├── incomplete/
        ├── Movies/
        └── Serien/
```

---

## 🛠 Vorbereitung

### 1. Verzeichnisse anlegen

```bash
mkdir -p ./config/Downloads/{complete,incomplete,Movies,Serien}
mkdir -p ./config/{gluetun,radarr,sonarr,sabnzbd,qbittorrent,portainer,heimdall}
```

### 2. VPN konfigurieren

- `.ovpn`-Datei deines VPN-Anbieters nach `./config/gluetun/custom.conf` kopieren
- Deine Zugangsdaten in `docker-compose.yml` unter `OPENVPN_USER/PASSWORD` eintragen

### 3. Stack starten

```bash
docker compose up -d
```

---

## 🖥 Zugriffe & Ports

| Dienst        | URL                        | Port    |
|---------------|----------------------------|---------|
| qBittorrent   | http://localhost:8080      | 8080    |
| SABnzbd       | http://localhost:8085      | 8085    |
| Radarr        | http://localhost:7878      | 7878    |
| Sonarr        | http://localhost:8989      | 8989    |
| Prowlarr      | http://localhost:9696      | 9696    |
| Heimdall      | http://localhost           | 80      |
| Portainer     | http://localhost:9000      | 9000    |

> 📍 Standard-Zugang qBittorrent: `admin / Pass findest du in der log: "docker log qbittorrent" .`

---

## 🧱 Docker Compose (enthalten)




## ✅ Tipps & Hinweise

- Plex kann über Overseerr/Sonarr/Radarr automatisch eingebunden werden.
- Falls LAN-Zugriff auf Plex, Radarr oder andere Dienste nicht geht:
  - VPN-Container: prüfe `LOCAL_NETWORK`
  - Radarr/Sonarr: besser mit `network_mode: host` wie hier
- Portweiterleitung nur bei unterstützten Anbietern (z. B. **Mullvad**)

---

## 🧠 Noch was?

- DSLite? Kein Problem – alles läuft lokal.
- Zugriff von außen ist nicht vorgesehen, aber möglich (z. B. via Reverse Proxy, IPv6, Cloudflare Tunnel).
- Du kannst die Dienste aufteilen – z. B. Gluetun + Downloader separat vom Rest.
- Overseer ist Optional, kann ich aber mit einfügen.

---

## 📜 Lizenz

Made with ❤️ by zer0.de
Feel free to fork, improve, or open issues.
