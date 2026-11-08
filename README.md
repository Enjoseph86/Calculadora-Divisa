# Calculadora científica con conversor BCV

Aplicación web instalable (PWA) que reúne una calculadora científica, el historial de cálculos y un conversor de dólares a bolívares con la tasa oficial del BCV, incluida la tasa vigente de cualquier fecha.

## Funciones

- Operaciones con prioridad, paréntesis, multiplicación implícita, potencias, raíces, factoriales y porcentajes.
- Trigonometría en grados o radianes, logaritmos, exponenciales y constantes π y e.
- Memoria (MC, MR, M+, M−), `Ans`, historial de hasta 30 cálculos y teclado físico opcional.
- Conversor USD ⇄ VES con la tasa del BCV, selector de fecha, tasa manual y caché para usar sin conexión.
- Botones para llevar el monto o el resultado del conversor a la calculadora y seguir operando con ellos.
- Instalable en el móvil: funciona a pantalla completa y sin conexión una vez abierta. Los datos (historial, memoria, tasas y fecha elegida) quedan en el dispositivo.

## Archivos

| Archivo | Uso |
| --- | --- |
| `index.html` | La aplicación completa (HTML, CSS y JavaScript, sin dependencias). |
| `manifest.webmanifest` | Manifiesto que permite instalarla como app. |
| `sw.js` | Service worker: funcionamiento sin conexión. |
| `icon-192.png`, `icon-512.png` | Iconos de la app. |

## Cómo usarla

Abre `index.html` en el navegador. Para que funcione como app instalable y sin conexión, sírvela por HTTP(S); por ejemplo:

```bash
python3 -m http.server 8000
```

y visita http://localhost:8000.

## Publicarla con GitHub Pages

1. En el repositorio, entra en **Settings → Pages**.
2. En **Source**, elige **Deploy from a branch**, la rama `main` y la carpeta `/ (root)`.
3. Guarda. En uno o dos minutos estará disponible en `https://TU-USUARIO.github.io/TU-REPO/`.

Desde esa dirección se puede instalar en Android (Chrome → menú ⋮ → «Instalar aplicación») y en iPhone (Safari → Compartir → «Añadir a pantalla de inicio»).

## La tasa del BCV

- **Tasa actual:** `https://ve.dolarapi.com/v1/dolares/oficial`
- **Tasa por fecha:** `https://ve.dolarapi.com/v1/historicos/dolares/oficial/AAAA/MM/DD`

Los datos son los publicados por el BCV y distribuidos por DolarApi.com. Si el día elegido no tuvo publicación (fin de semana o feriado), la app usa la última tasa anterior e indica su fecha. El calendario permite fechas desde el 03/01/2023, que es el inicio de la serie disponible. Si no hay conexión, se usa la última tasa guardada o puedes escribirla a mano; la tasa manual se guarda asociada a esa fecha.

Las tasas son informativas. Para operaciones oficiales, verifica siempre en el sitio del BCV.

## Privacidad

Todo el funcionamiento es local. La app no envía datos personales a ningún servidor; solo consulta las tasas públicas indicadas y guarda el historial, la memoria y las tasas consultadas en el almacenamiento del navegador.
