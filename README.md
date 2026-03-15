# SurfCoquimbo 🏄

App web PWA para visualizar condiciones de surf en tiempo real en la Region de Coquimbo, Chile.

**Live:** https://ttpsecspa.github.io/coquimbo-surf/

## Caracteristicas

- **Surf Score**: Indicador de 0-100 que evalua las condiciones actuales para surfear
- **Oleaje en tiempo real**: Altura, periodo y direccion de olas y swell
- **Viento**: Velocidad, direccion y deteccion offshore/onshore con brujula visual
- **Clima**: Temperatura, UV, temperatura del agua (correccion Humboldt) y recomendacion de traje
- **Recomendacion de tabla avanzada**: Tipo de tabla, talla, quillas, nivel y tip segun condiciones y tipo de spot
- **4 spots de surf**: Totoralillo, Punta de Choros, El Faro, Tongoy
- **Comparar spots**: Todos los spots lado a lado con puntajes, tipo de ola, rango y nivel
- **Mejor hora para surfear**: Recomienda la hora optima del dia
- **Indicadores completos**: Amanecer/atardecer, luna, traje, orientacion, tipo de break, rango de olas, nivel y peligros
- **Grafico de mareas**: Simulacion de mareas basada en fase lunar
- **Pronostico horario**: Proximas 24 horas con score por hora
- **Pronostico 7 dias**: Vision semanal con barras de oleaje
- **Alertas**: Notificacion de condiciones epicas o oleaje peligroso
- **PWA instalable**: Se puede instalar como app en celular
- **Auto-refresh**: Actualizacion automatica cada 15 minutos

## Spots (datos verificados)

| Spot | Tipo | Cara | Mejor Viento | Mejor Swell | Rango Olas | Nivel |
|------|------|------|--------------|-------------|------------|-------|
| Totoralillo | Point break (3 picos) | W | ENE (offshore) | WSW | 1.0-2.5m+ | Intermedio-Avanzado |
| Punta de Choros | Beach break | W | ESE (offshore) | SW | 1.0-2.5m | Todos |
| El Faro | Beach break (A-frame) | WNW | ESE (offshore) | SW | 0.3-1.5m | Principiante-Intermedio |
| Tongoy | Beach break (bahia) | N | S (offshore) | NW | 0.3-1.0m | Principiante |

## Recomendacion de Tabla

El sistema recomienda tablas basandose en:
- **Altura de ola** y **periodo** del swell
- **Tipo de spot** (point break vs beach break)
- **Velocidad del viento** (condiciones limpias vs choppy)
- Incluye: tipo de tabla, talla, configuracion de quillas, nivel requerido y tip practico

| Olas | Tabla | Quillas | Nivel |
|------|-------|---------|-------|
| < 0.3m | SUP / Bodyboard | Single fin | Todos |
| 0.3 - 0.6m | Longboard (9-10 ft) | Single/2+1 | Principiante |
| 0.6 - 1.0m | Funboard / Mini-mal (7-8'6") | Thruster/2+1 | Todos |
| 1.0 - 1.5m | Fish / Hybrid (5'6"-6'6") | Twin/Quad | Intermedio |
| 1.5 - 2.0m | Shortboard (5'8"-6'2") | Thruster | Intermedio-Avanzado |
| 2.0 - 2.5m | Shortboard performance (5'10"-6'2") | Thruster | Avanzado |
| 2.5 - 3.5m | Step-up (6'2"-7') | Thruster grande | Avanzado |
| 3.5m+ | Gun (7'-9') | Thruster stiff | Experto |

## Datos

Usa la API gratuita de [Open-Meteo](https://open-meteo.com):
- **Marine API**: Datos de oleaje (altura, periodo, direccion, swell, SST)
- **Weather API**: Clima, viento, UV, temperaturas

## Tech

- HTML/CSS/JS vanilla (zero dependencies)
- PWA con Service Worker (offline support)
- Responsive mobile-first
- Canvas para grafico de mareas
- Glassmorphism UI con animaciones
