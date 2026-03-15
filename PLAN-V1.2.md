# SurfCoquimbo v1.2 - SUPER PLAN
## "StormSurf Chile Edition"

---

## VISION
Convertir SurfCoquimbo en la app de surf mas completa de Chile, con nivel de analisis
tipo Stormsurf pero enfocado 100% en la costa chilena. Datos de grado profesional,
descomposicion de swells, modelos de olas, MJO, mareas reales y mas.

---

## ARQUITECTURA DE DATOS (todo gratis, sin API keys)

| Dato | Fuente | Auth | CORS | Formato |
|------|--------|------|------|---------|
| Olas + 3 swells descompuestos | Open-Meteo Marine API | No | Si | JSON |
| Viento (GFS + ECMWF) | Open-Meteo GFS/ECMWF API | No | Si | JSON |
| SST alta resolucion | Open-Meteo Marine + NOAA ERDDAP | No | Si | JSON |
| Mareas reales | Marea API (api.marea.ooo) | No | Si | JSON |
| MJO fase/pronostico | NOAA PSL (proxy) | No | No* | TXT |
| Corrientes oceanicas | Open-Meteo Marine | No | Si | JSON |
| Altimetria satelital | CMEMS (proxy) | Registro | No* | JSON |

*Requieren un proxy simple (Cloudflare Worker gratis)

---

## NUEVAS FUNCIONALIDADES

### 1. DESCOMPOSICION DE SWELLS (Prioridad ALTA)
**Inspirado en**: Stormsurf Buoy Reports - swell trains

- Mostrar hasta 3 swells separados (primario, secundario, terciario) + wind swell
- Cada swell con: altura, periodo, direccion, origen estimado
- Grafico polar tipo "rosa de swells" mostrando de donde viene cada swell
- Codigo de colores por tipo: groundswell largo (verde), swell medio (cyan), windswell (amarillo)

**API Open-Meteo params:**
```
swell_wave_height, swell_wave_direction, swell_wave_period, swell_wave_peak_period,
secondary_swell_wave_height, secondary_swell_wave_direction, secondary_swell_wave_period,
tertiary_swell_wave_height, tertiary_swell_wave_direction, tertiary_swell_wave_period,
wind_wave_height, wind_wave_direction, wind_wave_period, wind_wave_peak_period
```

### 2. GRAFICO DE MAREAS REALES (Prioridad ALTA)
**Inspirado en**: Stormsurf tide charts

- Reemplazar simulacion por datos reales de api.marea.ooo
- Grafico con curva suave mostrando niveles cada hora
- Marcadores de marea alta y baja con hora exacta
- Indicador de marea actual (subiendo/bajando)
- Coeficiente de marea (spring/neap)

**API Marea:**
```
GET https://api.marea.ooo/v1/tides?latitude=-29.95&longitude=-71.35
```

### 3. MAPA DE SWELLS DEL PACIFICO SUR (Prioridad ALTA)
**Inspirado en**: Stormsurf Pacific Forecast

- Canvas con mapa del Pacifico Sur (Chile como punto de referencia)
- Circulos concentricos mostrando swells viajando hacia Chile
- Lineas de Great Circle desde las tormentas generadoras
- Overlay de presion atmosferica / sistemas de baja presion
- Estimacion de llegada de swells (distancia / velocidad del grupo)

**Formula velocidad de grupo:**
```
V_grupo (km/h) = 5.6 * T_periodo (s)
Tiempo_llegada (h) = Distancia_km / V_grupo
```

### 4. INDICADOR MJO (Prioridad MEDIA)
**Inspirado en**: Stormsurf MJO Forecast

- Diagrama de fase MJO (Wheeler-Hendon)
- Fase actual (1-8) con indicacion de impacto en Chile
- Pronostico MJO 15 dias
- Correlacion MJO-swell para Chile:
  * Fase 5-6-7 (Pacifico Oeste): Aumenta actividad de tormentas en alta latitud sur
  * Fase 8-1 (Hemisferio Oeste): Posibles swells desde NW
  * Fase 2-3-4 (Indian Ocean): Menor actividad para Chile

**Datos:** NOAA PSL OMI/RMM index via Cloudflare Worker proxy

### 5. MODELOS MULTI-NIVEL (Prioridad MEDIA)
**Inspirado en**: Stormsurf 5-level zoom models

Niveles de zoom para el modelo de olas:
1. **Global**: Todo el Pacifico Sur - ver tormentas generadoras
2. **Regional**: Costa de Sudamerica (20°S - 45°S)
3. **Local**: Region de Coquimbo ampliada
4. **Spot**: Cada playa individual

Cada nivel muestra:
- Altura de olas (color gradient)
- Direccion del swell (flechas)
- Periodo pico (overlay)
- Viento (barbas)

### 6. PRONOSTICO EXTENDIDO 16 DIAS (Prioridad MEDIA)
**Inspirado en**: Stormsurf extended forecast

- Timeline extendido de 7 a 16 dias
- Grafico de barras apiladas (primario + secundario swell)
- Indicador de confianza del pronostico (decrece con dias)
- Eventos de swell marcados con etiquetas ("Swell SW grande dia 12")

**Open-Meteo soporta hasta 16 dias con modelo GFS**

### 7. CORRIENTES OCEANICAS (Prioridad BAJA)
- Velocidad y direccion de corriente en cada spot
- Indicador de corriente de Humboldt
- Alerta si corrientes peligrosas

**API:** `ocean_current_velocity, ocean_current_direction`

### 8. SST MAPA DE CALOR (Prioridad BAJA)
- Mapa de temperatura superficial del mar
- Costa de Chile (20°S - 45°S)
- Datos de NOAA ERDDAP MUR SST (1km resolucion)
- Visualizar upwelling de Humboldt

---

## MEJORAS UI/UX

### Dashboard Redesign
- **Hero section**: Surf Score + Swell principal + Viento + Marea en una vista
- **Swell decomposition card**: Visual tipo espectro con los 3+ swells
- **Timeline interactivo**: Slider para moverse hora a hora viendo como cambian las olas
- **Mapa mini**: Costa de Coquimbo con los 5 spots y estado de color por score

### Modo Mapa
- Vista mapa completa con todos los spots de Chile
- Click en spot para ver condiciones
- Colores por surf score
- Expandible a futuro a toda la costa chilena

### Notificaciones Push
- PWA notifications cuando las condiciones sean EPICAS
- Configurar umbral de score por spot
- Alertas de swell grande incoming

### Modo Oscuro / Claro
- Toggle dia/noche
- Modo "sesion" con pantalla minima para llevar al agua

---

## SPOTS EXPANDIDOS (Chile completo futuro)

### Fase 1 (v1.2): Region de Coquimbo - 5 spots actuales
- Totoralillo, Punta de Choros, El Faro, Tongoy, Peñuelas

### Fase 2 (v1.3): Zona Central
- Pichilemu (Punta de Lobos, La Puntilla, Infiernillo)
- Matanzas
- Topocalma
- Puertecillo
- Cachagua

### Fase 3 (v1.4): Norte + Sur
- Arica (La Capilla, El Laucho)
- Iquique (Huayquique, Cavancha)
- Constitucion
- Cobquecura
- Buchupureo

---

## IMPLEMENTACION TECNICA

### Stack
- **Frontend**: HTML/CSS/JS vanilla (mantener zero dependencies)
- **Canvas**: Graficos custom para mapas, swells, mareas
- **PWA**: Service Worker con cache inteligente
- **Proxy**: Cloudflare Worker gratuito para MJO y datos que no soportan CORS

### Estructura de archivos propuesta
```
coquimbo-surf/
  index.html          # App principal
  manifest.json       # PWA manifest
  sw.js              # Service Worker
  js/
    app.js           # Logica principal
    api.js           # Fetch de datos
    charts.js        # Graficos canvas (mareas, swells, mapa)
    scoring.js       # Algoritmo de surf score
    mjo.js           # Analisis MJO
    swell-tracker.js # Tracking de swells del Pacifico
  css/
    styles.css       # Estilos principales
    mobile.css       # Responsive
  assets/
    coast-chile.json # Contorno costa para mapa
```

### API Calls Plan
```
// Fetch principal - todo en un solo call
marine-api.open-meteo.com/v1/marine?
  latitude=${lat}&longitude=${lon}&
  hourly=wave_height,wave_direction,wave_period,wave_peak_period,
    wind_wave_height,wind_wave_direction,wind_wave_period,wind_wave_peak_period,
    swell_wave_height,swell_wave_direction,swell_wave_period,swell_wave_peak_period,
    secondary_swell_wave_height,secondary_swell_wave_direction,secondary_swell_wave_period,
    tertiary_swell_wave_height,tertiary_swell_wave_direction,tertiary_swell_wave_period,
    ocean_current_velocity,ocean_current_direction,
    sea_surface_temperature&
  daily=wave_height_max,wave_direction_dominant,wave_period_max&
  timezone=America/Santiago&
  forecast_days=16

// Mareas reales
api.marea.ooo/v1/tides?latitude=${lat}&longitude=${lon}

// MJO (via proxy)
psl.noaa.gov/mjo/mjoindex/omi.1x.txt
```

---

## ROADMAP DE DESARROLLO

### Sprint 1 (Semana 1-2): Datos Reales
- [ ] Integrar descomposicion de 3 swells + wind waves desde Open-Meteo
- [ ] Integrar mareas reales desde Marea API
- [ ] Card de swells descompuestos con visual tipo espectro
- [ ] Grafico de mareas real con datos de api.marea.ooo
- [ ] Extender pronostico a 16 dias

### Sprint 2 (Semana 3-4): Analisis Avanzado
- [ ] Rosa de swells (polar chart canvas)
- [ ] Timeline interactivo hora a hora
- [ ] Surf score mejorado con swells individuales
- [ ] Separar codigo en modulos (js/, css/)
- [ ] Cloudflare Worker proxy para MJO

### Sprint 3 (Semana 5-6): Mapas y MJO
- [ ] Mapa del Pacifico Sur con swells (canvas)
- [ ] Great circle lines desde tormentas
- [ ] Indicador MJO con diagrama Wheeler-Hendon
- [ ] Estimacion de llegada de swells
- [ ] Mapa mini de spots con colores

### Sprint 4 (Semana 7-8): PWA y Pulido
- [ ] Notificaciones push para condiciones epicas
- [ ] Cache inteligente (offline completo)
- [ ] Modo sesion minimalista
- [ ] Performance optimization
- [ ] Testing en dispositivos reales
- [ ] Deploy final

---

## METRICAS DE EXITO
- Tiempo de carga < 2s
- Funciona 100% offline (datos cacheados)
- Score de Lighthouse > 95
- Instalable como PWA en iOS y Android
- Datos actualizados cada 15 min
- Precision del surf score validada con condiciones reales

---

## DIFERENCIADORES vs STORMSURF
1. **Solo Chile** - Datos locales precisos, no generico global
2. **100% gratis** - Sin suscripcion, sin ads
3. **PWA mobile-first** - Instalable, offline, rapida
4. **Recomendacion de tabla** - Unico en la industria
5. **Corriente de Humboldt** - SST corregida para la realidad costera
6. **Español nativo** - Para la comunidad surfera chilena
7. **Descomposicion de swells** - Nivel profesional en una app simple

---

*Plan creado: Marzo 2026*
*SurfCoquimbo - Hecho con amor para la comunidad surfera de Chile*
