# SurfCoquimbo 🏄

App web para visualizar condiciones de surf en tiempo real en Coquimbo, Chile.

## Caracteristicas

- **Surf Score**: Indicador de 0-100 que evalua las condiciones actuales para surfear
- **Oleaje en tiempo real**: Altura, periodo y direccion de olas y swell
- **Viento**: Velocidad, direccion y deteccion offshore/onshore con brujula visual
- **Clima**: Temperatura, UV, temperatura del agua y recomendacion de traje
- **5 spots de surf**: La Herradura, Peñuelas, Totoralillo, El Faro, Punta de Choros
- **Pronostico horario**: Proximas 24 horas
- **Pronostico 7 dias**: Vision semanal con barras de oleaje
- **Indicadores**: Amanecer/atardecer, tipo de ola, orientacion del spot, mejor viento

## Datos

Usa la API gratuita de [Open-Meteo](https://open-meteo.com):
- **Marine API**: Datos de oleaje (altura, periodo, direccion, swell)
- **Weather API**: Clima, viento, UV, temperaturas

## Uso

Simplemente abre `index.html` en tu navegador. No requiere instalacion ni servidor.

## Tech

- HTML/CSS/JS vanilla
- Sin dependencias externas
- Responsive (mobile-first)
- Glassmorphism UI con animaciones de olas

## Spots

| Spot | Tipo | Orientacion | Mejor Viento |
|------|------|-------------|--------------|
| La Herradura | Beach break | W | E |
| Peñuelas | Beach break | NW | SE |
| Totoralillo | Point break | W | E |
| El Faro | Reef break | W | E |
| Punta de Choros | Point break | NW | SE |
