# Calculadora Científica Pro

Aplicación web instalable (PWA) que reúne una **calculadora científica**, **historial de cálculos**, **conversor de divisas** (USD/USDT/VES con múltiples tasas) y **convertidor de unidades** (14 categorías, 140+ unidades).

## ✨ Funciones Principales

### 🧮 Calculadora Científica
- Operaciones con prioridad, paréntesis, multiplicación implícita, potencias, raíces, factoriales y porcentajes
- Trigonometría en grados o radianes, logaritmos, exponenciales y constantes π y e
- Memoria (MC, MR, M+, M−), `Ans`, historial de hasta 30 cálculos
- Teclado físico opcional y teclado virtual responsivo
- **Sin separadores de miles** en resultados (solo punto/coma decimal)
- Copia limpia de resultados al portapapeles

### 💱 Conversor de Divisas (3 modos)
| Modo | Descripción | Fuente |
|------|-------------|--------|
| **USD → VES** | Tasa oficial BCV | `ve.dolarapi.com/v1/dolares/oficial` |
| **USDT (P2P) → VES** | Tasa Binance P2P (tiempo real) | API directa `p2p.binance.com` + fallback `paralelo` |
| **USD → USDT** | Relación BCV / P2P (1 USD = BCV/P2P USDT) | Calculada automáticamente |

- **Binance P2P directo**: POST a `p2p.binance.com/bapi/c2c/v2/friendly/c2c/adv/search` con mediana de top 10 ofertas
- **Fallback automático**: `ve.dolarapi.com/v1/dolares/paralelo` si falla Binance
- Selector de fecha con caché histórico (90 días por tasa)
- Tasa manual editable y persistente
- Botones para llevar montos/resultados a la calculadora

### 📐 Convertidor de Unidades (14 categorías)
| Categoría | Unidades clave |
|-----------|----------------|
| **Longitud** | mm, cm, m, km, in, ft, yd, mi, nmi, ly, au, pc |
| **Masa/Peso** | mg, g, kg, t, oz, lb, st, ct, gr, oz_t, slug |
| **Temperatura** | °C, °F, K, °R, °Ré (con offsets correctos) |
| **Volumen** | ml, l, m³, gal, qt, pt, cup, fl oz, tbsp, tsp, bbl |
| **Área** | mm², cm², m², km², ha, a, in², ft², yd², ac, mi² |
| **Velocidad** | m/s, km/h, mph, kn, ft/s, Mach, c |
| **Tiempo** | ns, µs, ms, s, min, h, d, wk, mo, yr, dec, cent |
| **Energía** | J, kJ, cal, kcal, Wh, kWh, BTU, ft·lb, eV, therm |
| **Presión** | Pa, kPa, MPa, bar, mbar, atm, psi, Torr, mmHg, inHg, kgf/cm² |
| **Potencia** | W, kW, MW, HP, cv, BTU/h, kcal/h, ft·lb/s |
| **Datos** | b, B, kb/kB, KiB, Mb/MB, MiB, Gb/GB, GiB, Tb/TB, TiB, Pb/PB |
| **Ángulo** | °, rad, gon, turn, ', ", mil |
| **Frecuencia** | Hz, kHz, MHz, GHz, THz, RPM, RPS |
| **Fuerza** | N, kN, MN, kgf, gf, lbf, pdl, kip |

- Selector de categoría → unidades From/To auto-pobladas
- Botón intercambio (⇅), chips de conversiones rápidas
- Fórmula de conversión visible en detalle
- Llevar valor origen o resultado a la calculadora

### 🎨 Temas y UI Moderna
- **Modo oscuro** (por defecto) y **modo claro** con detección automática del sistema
- Toggle de tema en cabecera (persiste en localStorage)
- Diseño *glassmorphism*, sombras elevadas, animaciones suaves
- **Responsive**: escritorio (2 columnas), móvil (1 columna)
- Accesibilidad: `prefers-reduced-motion`, `prefers-contrast: high`, ARIA labels
- PWA instalable: funciona offline, pantalla completa, iconos adaptativos

### 🪶 Vista Minimalista
Interruptor en la barra superior (icono de flechas hacia adentro) que alterna entre **vista completa** y **vista minimalista**:

| Aspecto | Vista completa | Vista minimalista |
|---------|----------------|-------------------|
| Layout | 2 columnas en escritorio (calculadora + historial lateral) | 1 columna centrada (≤ 430 px) |
| Estilo | Glassmorphism, sombras y degradados | Superficies planas, sin sombras ni blur |
| Controles | Todos visibles | Se ocultan memoria, teclado virtual, fecha de tasa, "Usar monto/resultado" y conversiones rápidas |
| Historial | Panel lateral fijo | Button de historial que lo despliega debajo de la calculadora |
| Banner de instalación | Se muestra | Se oculta |

- La preferencia se guarda en `localStorage` (`minimalMode`) y se aplica **antes del primer pintado** (sin parpadeos)
- Los cálculos, las tasas y el resto de la lógica no cambian: sólo la presentación

### 💾 Persistencia Local
Todo se guarda en `localStorage` del navegador:
- Historial de cálculos (30 items)
- Memoria de calculadora
- Tasas de divisas (BCV + P2P + fechas + caché 90 días)
- Preferencias: tema, modo DEG/RAD, modo Estándar/Científica, vista minimalista, última pestaña, configuración de unidades

## 📁 Archivos

| Archivo | Descripción |
|---------|-------------|
| `index.html` | Aplicación completa (HTML + CSS + JS, sin dependencias externas) |
| `manifest.webmanifest` | Manifiesto PWA para instalación |
| `sw.js` | Service Worker para funcionamiento offline |
| `icon-192.png`, `icon-512.png` | Iconos de la app |

## 🚀 Cómo Usarla

### Desarrollo Local
```bash
python3 -m http.server 8000
# o
npx serve .
```
Visita `http://localhost:8000`

### Publicar en GitHub Pages
1. Settings → Pages
2. Source: **Deploy from a branch**, rama `main`, carpeta `/ (root)`
3. Guarda. Disponible en `https://TU-USUARIO.github.io/TU-REPO/`

### Instalar como App
- **Android/Chrome**: Menú ⋮ → «Instalar aplicación»
- **iOS/Safari**: Compartir → «Añadir a pantalla de inicio»
- **Desktop/Chrome/Edge**: Barra de direcciones → icono instalar

## 🔌 APIs de Tasas Utilizadas

| Tasa | Endpoint | Método | Notas |
|------|----------|--------|-------|
| **BCV Oficial** | `https://ve.dolarapi.com/v1/dolares/oficial` | GET | Tasa oficial diaria |
| **BCV Histórico** | `https://ve.dolarapi.com/v1/historicos/dolares/oficial/AAAA/MM/DD` | GET | Desde 03/01/2023 |
| **Binance P2P** | `https://p2p.binance.com/bapi/c2c/v2/friendly/c2c/adv/search` | POST | `asset:USDT, fiat:VES, tradeType:SELL` |
| **Paralelo (fallback)** | `https://ve.dolarapi.com/v1/dolares/paralelo` | GET | Proxy confiable |
| **Paralelo Histórico** | `https://ve.dolarapi.com/v1/historicos/dolares/paralelo/AAAA/MM/DD` | GET | Para historial P2P |

**Binance P2P**: Se obtiene la mediana de las 10 mejores ofertas (precio más bajo para comprador). Reintentos exponenciales (3 intentos, timeout 10s). Headers `User-Agent` y `Accept` para evitar bloqueos.

## 🛡️ Privacidad
- **100% local**: No se envían datos personales a servidores
- Solo consultas a APIs públicas de tasas indicadas arriba
- Historial, memoria, tasas y preferencias quedan en el dispositivo
- Service Worker cachea solo assets estáticos (HTML, CSS, JS, iconos, manifest)

## 📋 Requisitos
- Navegador moderno con soporte para:
  - `Intl.NumberFormat`, `localStorage`, `fetch`, `Service Worker`
  - CSS Grid, Flexbox, Custom Properties, `backdrop-filter`
- HTTPS (o localhost) para PWA y Service Worker

## 📝 Licencia
Uso libre. Las tasas son informativas; para operaciones oficiales verifica siempre en el sitio del BCV y Binance P2P.