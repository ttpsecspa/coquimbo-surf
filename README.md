# SurfCoquimbo 🏄

App web PWA para visualizar condiciones de surf en tiempo real en la Region de Coquimbo, Chile.

**Live:** https://ttpsecspa.github.io/coquimbo-surf/

## Caracteristicas

- **Surf Score**: Indicador de 0-100 que evalua las condiciones actuales para surfear
- **Oleaje en tiempo real**: Altura, periodo y direccion de olas y swell
- **Viento**: Velocidad, direccion y deteccion offshore/onshore con brujula visual
- **Clima**: Temperatura, UV, temperatura del agua y recomendacion de traje
- **Recomendacion de tabla**: Sugiere tipo de tabla (longboard, fish, shortboard, gun) segun olas
- **5 spots de surf**: Totoralillo, Punta de Choros, El Faro, Tongoy, Peñuelas
- **Comparar spots**: Ve todos los spots lado a lado con puntajes en tiempo real
- **Mejor hora para surfear**: Recomienda la hora optima del dia
- **Grafico de mareas**: Simulacion de mareas basada en fase lunar
- **Fase lunar**: Con efecto en las mareas
- **Pronostico horario**: Proximas 24 horas con score por hora
- **Pronostico 7 dias**: Vision semanal con barras de oleaje
- **Alertas**: Notificacion de condiciones epicas o oleaje peligroso
- **PWA instalable**: Se puede instalar como app en celular
- **Auto-refresh**: Actualizacion automatica cada 15 minutos
- **Compartir**: Boton para compartir condiciones actuales

## Spots

| Spot | Tipo | Orientacion | Mejor Viento | Mejor Swell |
|------|------|-------------|--------------|-------------|
| Totoralillo | Point break (roca) | W-SW | ENE | WSW |
| Punta de Choros | Beach break | SW | ESE | SW |
| El Faro | Beach break | NW-W | ESE | NW |
| Tongoy | Beach break | W-NW | ESE | WSW |
| Peñuelas | Beach break (bahia) | NW-N | SSE | NW |

## Recomendacion de Tabla

| Olas | Periodo | Tabla Recomendada |
|------|---------|-------------------|
| < 0.3m | - | SUP / Bodyboard |
| 0.3 - 1.0m | < 8s | Longboard (8-10 ft) |
| 1.0 - 1.8m | 8-12s | Funboard / Fish (6'2"-7'6") |
| 1.5 - 2.5m | 10-14s | Shortboard (5'6"-6'2") |
| 2.5 - 3.5m | 12s+ | Step-up / Gun corta (6'2"-7') |
| 3.5m+ | 14s+ | Gun (7'-9') |

## Datos

Usa la API gratuita de [Open-Meteo](https://open-meteo.com):
- **Marine API**: Datos de oleaje (altura, periodo, direccion, swell)
- **Weather API**: Clima, viento, UV, temperaturas

## Tech

- HTML/CSS/JS vanilla (zero dependencies)
- PWA con Service Worker (offline support)
- Responsive mobile-first
- Canvas para grafico de mareas
- Glassmorphism UI con animaciones
