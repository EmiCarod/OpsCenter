# OpsCenter · ITS Cipolletti

Aplicación de laboratorio para Práctica Profesionalizante I.

Incluye dashboard visual, servicios, incidentes, eventos, `/live`, `/ready`, `/health`, `/version`, métricas simples, `/slow`, `/fail`, MySQL/MariaDB, scripts de verificación y plantilla systemd.

## Instalación

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
```

Editar `.env` y luego:

```bash
set -a
source .env
set +a
uvicorn app.main:app --host 127.0.0.1 --port "$APP_PORT"
```

Verificar:

```bash
curl -i http://127.0.0.1:8101/live
curl -i http://127.0.0.1:8101/ready
curl -i http://127.0.0.1:8101/health
curl -i http://127.0.0.1:8101/version
```

## systemd de usuario

```bash
mkdir -p ~/.config/systemd/user
cp opscenter.service.template ~/.config/systemd/user/opscenter.service
```

Editar `REPLACE_DOMAIN` y `REPLACE_PORT`, luego:

```bash
systemctl --user daemon-reload
systemctl --user enable --now opscenter
systemctl --user status opscenter
journalctl --user -u opscenter -f
```
