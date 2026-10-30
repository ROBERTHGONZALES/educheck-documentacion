# EduCheck — Parte 3: Documentación y despliegue

Documentación, build listo para demostrar y utilidades de despliegue del sistema de
asistencia escolar EduCheck.

> Proyecto dividido en 3 partes:
> 1. Backend Django (`parte-1-backend-django`)
> 2. Frontend React (`parte-2-frontend-react`)
> 3. **Documentación y despliegue** (este repositorio)

## Contenido

| Ruta | Descripción |
| --- | --- |
| `README-LOCAL-WINDOWS.md` | guía original de instalación en Windows |
| `dist/` | interfaz ya compilada, lista para servir sin `npm install` |
| `deploy/educheck.sh` | arranque/parada de MariaDB + Django + Vite en Linux/macOS |
| `deploy/my.cnf.example` | configuración de MariaDB local |
| `deploy/seed_demo.py` | carga datos de demostración (colegio, grados, secciones, alumnos) |
| `COMO-UNIR-LAS-PARTES.md` | instrucciones para juntar las 3 partes |

## Unir las 3 partes

```text
educheck/
├── backend/          ← contenido de parte-1-backend-django
├── src/              ← contenido de parte-2-frontend-react
├── packages/
├── public/
├── index.html
├── package.json
├── vite.config.ts
└── deploy/           ← contenido de parte-3 (esta parte)
```

Detalle paso a paso en `COMO-UNIR-LAS-PARTES.md`.

## Arranque rápido (Linux/macOS)

```bash
# 1) base de datos
mysql -u root -p < backend/sql/create_database.sql

# 2) backend
cd backend && python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env      # edita MARIADB_URL y DJANGO_SECRET_KEY
python manage.py migrate
cd ..

# 3) frontend
npm install

# 4) todo junto
./deploy/educheck.sh start
```

Abre `http://127.0.0.1:5173`.

## Usuarios de demostración

| Usuario | Contraseña | Rol |
| --- | --- | --- |
| `director` | `EduCheck2026!` | director |
| `auxiliar` | `EduCheck2026!` | auxiliar |

`deploy/seed_demo.py` crea además alumnos, grados y secciones de ejemplo.
