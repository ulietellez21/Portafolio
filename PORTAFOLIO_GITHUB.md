# Portafolio GitHub — Ulises Téllez Landón
> Documentación completa de la sesión de trabajo · 23 Abril 2026

---

## Perfil de GitHub

**Usuario:** `ulietellez21`
**URL:** https://github.com/ulietellez21

### Datos configurados
| Campo | Valor |
|---|---|
| Nombre | Ulises Téllez Landón |
| Bio | Full Stack Developer · Turning ideas into digital products \| Code + Design |
| Ubicación | Texcoco, Estado de México |
| Sitio web | https://ulietellez21.github.io |

---

## Repositorios creados

### 1. portfolio-personal
**URL:** https://github.com/ulietellez21/portfolio-personal
**Demo en vivo:** https://ulietellez21.github.io/portfolio-personal/
**Archivos en:** `/tmp/portfolio-personal/`

#### Stack
- React 18 + TypeScript + Vite
- Tailwind CSS v3
- Framer Motion (animaciones)
- Lucide React (iconos)

#### Estructura
```
src/
├── components/
│   ├── Navbar.tsx       — nav fija con toggle dark mode y menú mobile
│   ├── Hero.tsx         — sección principal con animaciones
│   ├── About.tsx        — sobre mí con highlights
│   ├── Skills.tsx       — grid de categorías de tecnologías
│   ├── Projects.tsx     — tarjetas de proyectos con links demo/repo
│   ├── Contact.tsx      — sección de contacto
│   ├── Footer.tsx       — pie de página
│   └── Icons.tsx        — SVGs de GitHub y LinkedIn (lucide no los incluye)
├── data/
│   └── portfolio.ts     — FUENTE ÚNICA: datos personales, skills y proyectos
└── index.css            — Tailwind + Google Fonts (Inter)
```

#### Para modificar contenido
Todo el contenido editable está en `src/data/portfolio.ts`:
- `personalInfo` — nombre, email, bio, links
- `skills` — categorías y tecnologías
- `projects` — lista de proyectos con `demo`, `repo`, `tech`, `type`, `private`

#### Campos de proyecto
```ts
{
  title: string
  description: string
  tech: string[]
  type: 'Full Stack' | 'Frontend' | 'Backend' | 'IA' | 'Design'
  status: string
  demo?: string      // URL de demo en vivo (muestra botón "Ver en vivo")
  repo?: string      // URL del repo en GitHub (muestra ícono GitHub)
  private?: boolean  // true = muestra candado, oculta links
}
```

#### Deploy
- GitHub Pages vía GitHub Actions (`.github/workflows/deploy.yml`)
- Se despliega automáticamente en cada push a `main`
- Base URL configurada en `vite.config.ts`: `base: '/portfolio-personal/'`

---

### 2. rest-api-auth
**URL:** https://github.com/ulietellez21/rest-api-auth
**Archivos en:** `/tmp/rest-api-auth/`

#### Stack
- Node.js + Express 5 + TypeScript
- JWT (jsonwebtoken) — access token 15min + refresh token 7d
- bcryptjs — hash de contraseñas
- Zod — validación de inputs
- Swagger/OpenAPI 3.0 (swagger-jsdoc + swagger-ui-express)
- Helmet + CORS

#### Estructura
```
src/
├── config/swagger.ts        — definición OpenAPI con schemas
├── controllers/
│   └── authController.ts    — lógica: register, login, refresh, logout, profile
├── middleware/
│   └── auth.ts              — middleware JWT (Bearer token)
├── models/
│   └── userStore.ts         — store en memoria (reemplazar por Prisma+PostgreSQL)
├── routes/
│   └── auth.ts              — rutas con anotaciones @openapi
└── index.ts                 — entry point, Express app
```

#### Endpoints
| Método | Ruta | Auth | Descripción |
|---|---|---|---|
| POST | `/api/auth/register` | No | Crear cuenta |
| POST | `/api/auth/login` | No | Iniciar sesión |
| POST | `/api/auth/refresh` | No | Renovar access token |
| POST | `/api/auth/logout` | No | Cerrar sesión |
| GET | `/api/auth/me` | Bearer | Perfil del usuario |

#### Docs interactivas
`http://localhost:3000/api-docs`

#### Variables de entorno (`.env`)
```
PORT=3000
JWT_SECRET=clave_secreta
REFRESH_SECRET=clave_refresh
```

#### Para pasar a producción con PostgreSQL
Reemplazar `src/models/userStore.ts` con Prisma:
```bash
npm install prisma @prisma/client
npx prisma init
```

---

### 3. data-dashboard
**URL:** https://github.com/ulietellez21/data-dashboard
**Demo en vivo:** https://ulietellez21.github.io/data-dashboard/
**Archivos en:** `/tmp/data-dashboard/`

#### Stack
- React 18 + TypeScript + Vite
- Recharts (gráficas)
- Tailwind CSS v3
- Lucide React

#### Componentes
| Componente | Tipo de gráfica | Datos |
|---|---|---|
| `KpiCard` | Métrica con tendencia | ingresos, usuarios, conversión, ticket |
| `RevenueChart` | Área (doble) | ingresos vs ganancia mensual |
| `UserGrowthChart` | Barras agrupadas | usuarios registrados vs activos |
| `CategoryChart` | Donut | distribución por categoría |
| `TopProducts` | Lista con tendencia | top 5 productos por ingresos |
| `Sidebar` | Navegación lateral | — |

#### Para cambiar datos
Editar `src/data/mockData.ts` — contiene todos los datos de ejemplo.

#### Deploy
GitHub Pages automático en cada push a `main`.

---

### 4. fullstack-task-manager
**URL:** https://github.com/ulietellez21/fullstack-task-manager
**Archivos en:** `/tmp/fullstack-task-manager/`

#### Stack
| Capa | Tecnología |
|---|---|
| Frontend | React 18 + TypeScript + Tailwind + Axios |
| Backend | FastAPI (Python) + SQLAlchemy |
| Base de datos | SQLite (dev) — reemplazar por PostgreSQL en prod |
| Auth | JWT con python-jose |
| Docs | Swagger UI automático en `/docs` |

#### Estructura backend
```
backend/
├── app/
│   ├── core/
│   │   ├── config.py      — SECRET_KEY, ALGORITHM, expiración tokens
│   │   ├── database.py    — SQLAlchemy engine + SessionLocal
│   │   └── security.py    — hash/verify password, create/decode JWT
│   ├── models/models.py   — User, Task (SQLAlchemy ORM)
│   ├── schemas/schemas.py — Pydantic schemas (validación de entrada/salida)
│   ├── routers/
│   │   ├── auth.py        — /api/auth/* endpoints
│   │   └── tasks.py       — /api/tasks/* CRUD
│   └── main.py            — FastAPI app, CORS, routers
└── requirements.txt
```

#### Cómo correr localmente
```bash
# Backend
cd backend && source venv/bin/activate
uvicorn app.main:app --reload
# → http://localhost:8000/docs

# Frontend
cd frontend && npm run dev
# → http://localhost:5173
```

#### Variables de entorno backend
```
SECRET_KEY=clave_secreta_django
```

#### Para migrar a PostgreSQL
Cambiar en `app/core/database.py`:
```python
SQLALCHEMY_DATABASE_URL = "postgresql://user:password@localhost/taskflow"
```

---

### 5. ui-design-system
**URL:** https://github.com/ulietellez21/ui-design-system
**Demo en vivo:** https://ulietellez21.github.io/ui-design-system/
**Archivos en:** `/tmp/ui-design-system/`

#### Stack
- React 18 + TypeScript + Vite
- Tailwind CSS v3 con tokens de color personalizados
- Storybook (`@storybook/react-vite`)
- clsx (composición de clases)
- Lucide React

#### Componentes disponibles
| Componente | Props clave | Variantes |
|---|---|---|
| `Button` | variant, size, loading, leftIcon, rightIcon, fullWidth | primary, secondary, outline, ghost, danger |
| `Badge` | variant, dot | default, primary, success, warning, danger, outline |
| `Input` | label, error, hint, leftElement, rightElement | — |
| `Card` + sub-componentes | padding, shadow, hoverable | — |
| `Alert` | variant, title, onClose | info, success, warning, error |
| `Spinner` | size, variant, label | sm, md, lg, xl |

#### Cómo importar componentes
```tsx
import { Button, Badge, Input, Card, Alert, Spinner } from './src'
```

#### Cómo ver Storybook
```bash
npm run storybook
# → http://localhost:6006
```

#### Agregar un componente nuevo
1. Crear carpeta `src/components/NombreComponente/`
2. Crear `NombreComponente.tsx` (componente) y `NombreComponente.stories.tsx` (stories)
3. Exportar desde `src/index.ts`

#### Colores del tema (tailwind.config.js)
```
primary: azul (#3b82f6)
success: verde (#22c55e)
warning: amarillo (#f59e0b)
danger: rojo (#ef4444)
```

---

### 6. ai-text-analyzer
**URL:** https://github.com/ulietellez21/ai-text-analyzer
**Archivos en:** `/tmp/ai-text-analyzer/`

#### Stack
- Python 3.11+
- Streamlit 1.30+
- Anthropic SDK (Claude Haiku)
- python-dotenv

#### Modos de análisis disponibles
| Modo | Descripción |
|---|---|
| 📝 Resumen | Resume texto en 3-5 oraciones |
| 😊 Sentimiento | Detecta positivo/negativo/neutro + porcentaje |
| 🔑 Palabras clave | Extrae 8-10 términos relevantes |
| ✍️ Mejorar redacción | Reescribe con mejor estilo |
| 🌐 Traducir al inglés | Traducción natural |
| ❓ Preguntas de comprensión | 5 preguntas con respuestas |
| 🐛 Revisar código | Bugs, mejoras, buenas prácticas |

#### Cómo correr
```bash
source venv/bin/activate
streamlit run app.py
# → http://localhost:8501
```

#### Variables de entorno (`.env`)
```
ANTHROPIC_API_KEY=sk-ant-...
```

#### Para agregar un modo nuevo
En `app.py`, agregar una entrada al diccionario `ANALYSIS_MODES`:
```python
ANALYSIS_MODES = {
    ...
    "🆕 Mi modo": "Instrucción para Claude sobre qué hacer con el texto.",
}
```

#### Deploy en Streamlit Cloud (gratis)
1. Ir a https://share.streamlit.io
2. Conectar repo `ai-text-analyzer`
3. En "Secrets" agregar: `ANTHROPIC_API_KEY = "sk-ant-..."`
4. Deploy — URL pública automática

---

## Repo privado — Dashboard Movums

**Repo:** `ulietellez21/Dashboard-Movums` (privado)
**Motivo:** Proyecto de cliente (agencia de viajes Movums)

### Alertas de seguridad detectadas y acciones tomadas
- ✅ Repo hecho privado
- ⚠️ `SECRET_KEY` de Django expuesta en `docs/migracion/PLAN_MIGRACION_NUEVO_SERVIDOR.md` — **debe rotarse en producción**
- Scripts de deploy con IPs de servidor expuestas (ya privados)

### Para rotar la SECRET_KEY en producción
```bash
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
# Reemplazar en el .env del servidor y reiniciar Gunicorn
```

---

## GitHub Actions — Deploy automático

Los repos con deploy automático a GitHub Pages son:
- `portfolio-personal`
- `data-dashboard`
- `ui-design-system`

Workflow en `.github/workflows/deploy.yml` — se dispara en cada push a `main`.

**Nota:** Se usa `npm install` en vez de `npm ci` porque el `package-lock.json` fue generado en macOS y puede desincronizarse con el entorno Linux de GitHub Actions.

---

## Próximos pasos sugeridos

- [ ] Agregar LinkedIn real al portfolio (`personalInfo.linkedin` en `portfolio.ts`)
- [ ] Deployar `ai-text-analyzer` en Streamlit Cloud y agregar su URL al portfolio
- [ ] Deployar backend de `fullstack-task-manager` en Render y actualizar URL del frontend
- [ ] Agregar foto de perfil a GitHub
- [ ] Agregar README al perfil de GitHub (`ulietellez21/ulietellez21`)
- [ ] Completar los proyectos del plan: Dashboard de datos con datos reales, Design System con más componentes
