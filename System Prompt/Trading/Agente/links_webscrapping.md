# Solicitud: Recolección de Datos de Trading - v2.1

Necesito que visites las siguientes URLs de análisis cripto. Como muchas usan gráficos interactivos (canvas, SVG, JS), **tomá screenshot de cada página** y luego extraé los datos visibles del screenshot para generar el informe.

## Proceso General para cada URL

1. Navegá a la URL
2. Esperá que cargue completamente (3-5 segundos)
3. Tomá screenshot de la zona principal con datos
4. Extraé los valores numéricos visibles en el screenshot
5. Si no podés leer un valor, marcalo como [NO VISIBLE EN SCREENSHOT]

---

## ⚠️ PROCESOS ESPECIALES (LEER ANTES DE EMPEZAR)

### Para CryptoQuant (Exchange Reserve, Netflow):
Los valores de cambio % 24h requieren cálculo manual:

**Exchange Reserve Δ% 24h:**
1. Navegar a la URL
2. Esperar carga completa (5 segundos)
3. Configurar timeframe del gráfico a "1D" o "24h" si hay selector
4. **Hover punto ACTUAL (extremo derecho)** → anotar valor en BTC
5. **Hover punto HACE 24H (un día atrás)** → anotar valor en BTC
6. **Calcular:** `Δ% = ((actual - hace24h) / hace24h) × 100`
7. Reportar: "Exchange Reserve: [X] BTC | Δ24h: [+/-X%]"

**Exchange Netflow:**
1. Hover sobre las barras del último día
2. Barras ROJAS = salida (negativo, bullish)
3. Barras VERDES = entrada (positivo, bearish)
4. Sumar el netflow de las últimas 24h

**Si los tooltips no funcionan:**
- Buscar panel "Statistics" o valores numéricos en la página
- Usar estimación visual con nota `[ESTIMADO]`
- Anotar en errores: "Δ% calculado visualmente, precisión ±2%"

### Para LookIntoBitcoin (HODL Waves, MVRV Z-Score):
Los valores exactos de % están en tooltips:
1. Navegar a la URL
2. Esperar carga completa
3. **Hacer hover sobre la banda/línea relevante** en el extremo derecho del gráfico
4. Leer el % que aparece en el tooltip
5. Si no hay tooltip funcional, usar estimación visual con nota `[ESTIMADO ~X%]`

### Para Coinglass (Heatmap, Liquidation Map):
Los datos críticos están en zonas visuales:
1. Identificar **colores brillantes (amarillo/verde)** = alta concentración de liquidez
2. Anotar los niveles de precio donde aparecen esas concentraciones
3. Para Liquidation Map: leer las barras verdes (longs) y rojas (shorts) con sus valores en $M

---

## PARTE 1: URLs AUTOMÁTICAS (visitá estas en orden)

### 0. Precio y Dominance (extraer de header)
Antes de empezar, anotar de la primera página de Coinglass:
- **Precio BTC actual** (visible en header)
- **BTC Dominance %** (visible en header, ej: "Dominance: BTC 57.6%")

### Derivados (Coinglass)
| # | URL | Datos a extraer | Proceso especial |
|---|-----|-----------------|------------------|
| 1 | https://www.coinglass.com/pro/futures/LiquidationHeatMap | Zonas de liquidez arriba/abajo del precio, colores brillantes = magnet zones | Identificar niveles de precio con color amarillo/verde intenso |
| 2 | https://www.coinglass.com/pro/futures/LiquidationMap | Barras longs (verde) vs shorts (rojo), valores en $M | Leer valores numéricos de las barras |
| 3 | https://www.coinglass.com/pro/futures/OpenInterest | OI total en $B + cambio % 24h | Valor visible en panel principal |
| 4 | https://www.coinglass.com/FundingRate | Funding BTC (valor decimal, ej: 0.0045%) | Buscar fila de BTC, columna "Funding Rate" |
| 5 | https://www.coinglass.com/LongShortRatio | Ratio global + ratio top traders | Dos valores: "Global" y "Top Traders" |
| 6 | https://www.coinglass.com/pro/futures/Hyperliquid/HyperliquidLongShortRatio | Posicionamiento en Hyperliquid | Ratio L/S específico de Hyperliquid |

### On-Chain TIER 1 - CryptoQuant (señales primarias, refresh ~1h)
| # | URL | Datos a extraer | Proceso especial |
|---|-----|-----------------|------------------|
| 7 | https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-netflow-total | Valor en BTC (+entrada / -salida) últimas 24h | **HOVER sobre último punto** para valor exacto |
| 8 | https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-reserve | Valor actual en BTC + **Δ% 24h calculado** + tendencia | **HOVER 2 puntos** (actual + hace 24h) y calcular Δ% |
| 9 | https://cryptoquant.com/asset/btc/chart/market-indicator/mvrv-ratio | **CRÍTICO: Valor numérico actual (ej: 1.85)** | Valor visible en gráfico o panel lateral |

> ⚠️ **NOTA v2.1:** La URL anterior `/market-indicator/mvrv` estaba incorrecta. La correcta es `/mvrv-ratio`

### On-Chain TIER 2 - LookIntoBitcoin (confirmación macro, refresh ~24h)
| # | URL | Datos a extraer | Proceso especial |
|---|-----|-----------------|------------------|
| 10 | https://www.lookintobitcoin.com/charts/hodl-waves/ | % banda >1 año + % banda <3 meses | **HOVER sobre cada banda** en extremo derecho |
| 11 | https://www.lookintobitcoin.com/charts/mvrv-zscore/ | Valor numérico + zona de color (verde/amarillo/rojo) | Valor visible en leyenda o tooltip |
| 12 | https://www.lookintobitcoin.com/charts/pi-cycle-top-indicator/ | Estado de las líneas (sin señal/acercándose/cruzando) | Visual: ¿las dos líneas se tocan? |

### Complementarios
| # | URL | Datos a extraer | Proceso especial |
|---|-----|-----------------|------------------|
| 13 | https://alternative.me/crypto/fear-and-greed-index/ | Número (0-100) + clasificación (Extreme Fear/Fear/Neutral/Greed/Extreme Greed) | Valor grande visible en centro |

### Dominance (backup si no se vio en Coinglass)
| # | URL | Datos a extraer | Proceso especial |
|---|-----|-----------------|------------------|
| 14 | https://coinmarketcap.com/ | BTC Dominance %, ETH Dominance % | Visible en header/banner superior |

---

## PARTE 2: DATOS VÍA API (ejecutar con bash/curl)

### Calendario Económico (API gratuita, sin key)
```bash
# Esta semana (siempre disponible)
curl -s "https://nfs.faireconomy.media/ff_calendar_thisweek.json" | jq '[.[] | select(.impact == "High")]'

# Próxima semana (puede dar 404 los fines de semana - SI FALLA, OMITIR)
curl -s "https://nfs.faireconomy.media/ff_calendar_nextweek.json" | jq '[.[] | select(.impact == "High")]'
```

Campos relevantes por evento:
- `title`: Nombre del evento
- `country`: País/moneda
- `date`: Fecha
- `time`: Hora (ET timezone)
- `impact`: Impacto (filtrar solo "High")
- `forecast`: Pronóstico
- `previous`: Valor anterior

### CoinGecko API (alternativa gratuita para global metrics)
```bash
# Global data sin API key
curl -s "https://api.coingecko.com/api/v3/global" | jq '.data | {
  btc_dominance: .market_cap_percentage.btc,
  eth_dominance: .market_cap_percentage.eth,
  total_market_cap_usd: .total_market_cap.usd,
  total_volume_usd: .total_volume.usd,
  market_cap_change_24h: .market_cap_change_percentage_24h_usd
}'
```

### CoinMarketCap Global Metrics (OPCIONAL - requiere API key)
```bash
# Solo si tenés API key
curl -s -H "X-CMC_PRO_API_KEY: TU_KEY_AQUI" \
  "https://pro-api.coinmarketcap.com/v1/global-metrics/quotes/latest"
```

> ℹ️ Si no tenés CMC API key, usá CoinGecko como alternativa (arriba)

### Glassnode LTH/SOPR
❌ Requiere suscripción paga — **OMITIR**
Usamos CryptoQuant MVRV + LookIntoBitcoin HODL Waves como proxy

---

## Qué necesito de cada fuente (CHECKLIST)

### Coinglass ✓
- [ ] Liquidation Heatmap: Magnet zones (niveles de precio con alta liquidez)
- [ ] Liquidation Map: $M en longs vs $M en shorts
- [ ] Open Interest: Total $B + Δ% 24h
- [ ] Funding Rate BTC: Valor decimal (ej: 0.0047%)
- [ ] L/S Ratio: Global % + Top Traders ratio
- [ ] Hyperliquid L/S: Ratio específico
- [ ] **BONUS:** Precio BTC y BTC Dominance del header

### CryptoQuant (TIER 1) ✓
- [ ] Exchange Netflow 24h: Valor en BTC (+ o -)
- [ ] Exchange Reserve: Valor actual + **Δ% 24h** + tendencia
- [ ] **MVRV Ratio: Valor numérico exacto** ← CRÍTICO

### LookIntoBitcoin (TIER 2) ✓
- [ ] HODL Waves >1 año: X%
- [ ] HODL Waves <3 meses: X%
- [ ] MVRV Z-Score: Valor + zona color
- [ ] Pi Cycle: Estado de cruce

### Complementarios ✓
- [ ] Fear & Greed: Número + clasificación

### APIs ✓
- [ ] Calendario: Eventos High Impact próximos 7 días
- [ ] Global Metrics: Dominance, Market Cap, Volume (via CoinGecko o CMC)

---

## Thresholds de Anomalía (Paso 3 del Screening)

### TIER 1: Señales Intraday

| MVRV | Exchange Reserve 24h | Score | Anomaly Type |
|------|---------------------|-------|--------------|
| < 0.8 | Δ < -5% | +3 | 🚨 EXTREME_ACCUMULATION |
| 0.8 - 1.5 | Δ < -5% | +2 | ✅ ACCUMULATION_STRONG_HOLDING |
| > 3.5 | Δ > +5% | +3 | 🚨 EXTREME_DISTRIBUTION |
| 3.0 - 3.5 | Δ > +5% | +2 | ⚠️ DISTRIBUTION |
| 1.5 - 3.0 | Δ ±5% | +0 | → NEUTRAL |

### TIER 2: Confirmación Macro

| HODL >1y | MVRV Z-Score | Señal Macro | Confianza |
|----------|--------------|-------------|-----------|
| > 65% | < 0 | BULLISH | ALTA |
| < 55% | > 6 | BEARISH | ALTA |
| 55-65% | cualquier | NEUTRAL | BAJA |

### Integración

- Si TIER 1 y TIER 2 confirman → Score +1, Confianza ALTA
- Si divergen → Score -1, Confianza BAJA
- **Califica para Deep Dive:** Score ≥ 3

---

## Formato del Informe

```markdown
# Informe de Datos — Trading POD v2.1
Fecha/Hora UTC: [timestamp]
Precio BTC: $[X]

═══════════════════════════════════════════════════════════════
                    MERCADO GLOBAL
═══════════════════════════════════════════════════════════════
**Fuente: CoinGecko API / CoinMarketCap**
- BTC Dominance: [X%] ([+/-X%] 24h)
- ETH Dominance: [X%]
- Total Market Cap: $[X]T ([+/-X%] 24h)
- Total Volume 24h: $[X]B
- Stablecoin Market Cap: $[X]B (si disponible)

═══════════════════════════════════════════════════════════════
                    DERIVADOS (Coinglass)
═══════════════════════════════════════════════════════════════
**Liquidez:**
- Heatmap Magnet Zones: 
  └─ ARRIBA: $[X] (concentración: [ALTA/MEDIA/BAJA])
  └─ ABAJO: $[X] (concentración: [ALTA/MEDIA/BAJA])
- Liquidation Map: Longs $[X]M / Shorts $[X]M
- Magnet Zone Principal: [ARRIBA/ABAJO] — Volumen: $[X]M

**Posicionamiento:**
- Open Interest: $[X]B ([+/-X%] 24h)
- Funding BTC: [X%] — Estado: [Normal/Elevado/Extremo]
- L/S Ratio Global: [X%/X%]
- L/S Top Traders: [X:1] — Tendencia: [hacia longs/shorts]
- Hyperliquid L/S: [X:1]

═══════════════════════════════════════════════════════════════
              ON-CHAIN (Paso 3 del Screening)
═══════════════════════════════════════════════════════════════

**TIER 1 - Señales Primarias (CryptoQuant):**
- MVRV Ratio: [X]
  └─ Zona: [<0.8 Extreme Acc / 0.8-1.5 Acc / 1.5-3.0 Neutral / 3.0-3.5 Dist / >3.5 Extreme Dist]
- Exchange Reserve: [X] BTC
  └─ Cambio 24h: [+/-X%] ← CRÍTICO para anomalía
  └─ Tendencia: [creciendo/cayendo/estable]
- Exchange Netflow 24h: [+/-X] BTC
  └─ Interpretación: [entrada a exchanges = presión venta / salida = holding]

**Anomalía TIER 1:**
[✅ SI / ❌ NO] — Tipo: [EXTREME_ACCUMULATION / ACCUMULATION_STRONG_HOLDING / DISTRIBUTION / EXTREME_DISTRIBUTION / NEUTRAL]
Score Tier 1: [X de 3]

**TIER 2 - Confirmación Macro (LookIntoBitcoin):**
- HODL Waves:
  └─ >1 año: [X%] [EXACTO/ESTIMADO]
  └─ <3 meses: [X%] [EXACTO/ESTIMADO]
  └─ Tendencia reciente: [+/-] en >1 año
- MVRV Z-Score: [X]
  └─ Zona: [verde <3 / amarilla 3-7 / roja >7]
- Pi Cycle: [sin señal / acercándose / cruzando ⚠️]

**Señal Macro:**
[BULLISH / BEARISH / NEUTRAL] — Confianza: [ALTA/MEDIA/BAJA]

**PASO 3 INTEGRADO:**
┌─────────────────────────────────────────────────┐
│ Score Final: [X de 5]                           │
│ Anomalía Detectada: [tipo]                      │
│ Califica para Deep Dive: [✅ SI / ❌ NO]         │
│ Confluencia TIER1 + TIER2: [✅/⚠️/❌]            │
└─────────────────────────────────────────────────┘

<reflection>
¿Los datos de TIER 1 y TIER 2 cuentan la misma historia?
- MVRV Ratio [X] → Zona [X]
- Exchange Reserve Δ [X%] → [acumulación/distribución/neutral]
- HODL >1y [X%] → [holders reteniendo/distribuyendo]
- MVRV Z-Score [X] → [infravalorado/neutral/sobrevalorado]

Conclusión: [CONFIRMACIÓN / DIVERGENCIA / CONTRADICCIÓN]
Si divergencia: [explicar qué métrica contradice]
</reflection>

═══════════════════════════════════════════════════════════════
                    SENTIMIENTO
═══════════════════════════════════════════════════════════════
- Fear & Greed Index: [X] ([Extreme Fear/Fear/Neutral/Greed/Extreme Greed])

═══════════════════════════════════════════════════════════════
                    CALENDARIO ECONÓMICO
═══════════════════════════════════════════════════════════════
**Eventos High Impact (próximos 7 días):**
| Fecha | Hora (ET) | Evento | País | Forecast | Previous |
|-------|-----------|--------|------|----------|----------|
| [X]   | [X]       | [X]    | [X]  | [X]      | [X]      |

**⚠️ Eventos críticos próximas 48h:**
- [Listar si hay FOMC, CPI, NFP, etc.]

═══════════════════════════════════════════════════════════════
                    RESUMEN EJECUTIVO
═══════════════════════════════════════════════════════════════

**Señales Alcistas:**
• [bullet basado en datos observables]
• [bullet basado en datos observables]

**Señales Bajistas:**
• [bullet basado en datos observables]
• [bullet basado en datos observables]

**Sesgo General:** [BULLISH / BEARISH / NEUTRAL / MIXTO]
**Confianza:** [ALTA / MEDIA / BAJA]

**Activos que califican para Deep Dive (score Paso 3 ≥3):**
- BTC: [SÍ/NO] — Score: [X] — Razón: [X]

═══════════════════════════════════════════════════════════════
                    DATOS PENDIENTES / ERRORES
═══════════════════════════════════════════════════════════════
- [ ] [URL que falló + razón]
- [ ] [Dato que requiere login]
- [ ] [Valor estimado vs exacto]
```

---

## Manejo de Errores

### Si CryptoQuant requiere login:
```
[REQUIERE LOGIN] - Intentar:
1. Refrescar página
2. Si persiste, marcar dato como [NO DISPONIBLE - LOGIN]
3. Usar MVRV Z-Score de LookIntoBitcoin como proxy
```

### Si un gráfico está en blanco:
```
1. Esperar 5 segundos adicionales
2. Refrescar página (F5)
3. Si persiste, marcar [GRÁFICO NO CARGÓ]
```

### Si screenshot no captura datos:
```
1. Hacer zoom out (Ctrl + -)
2. Intentar screenshot de área específica
3. Si persiste, marcar [SCREENSHOT INCOMPLETO]
```

### Si tooltip no aparece al hover:
```
1. Intentar click en el punto
2. Buscar panel "Statistics" o "Info" en la página
3. Si no hay datos exactos, usar [ESTIMADO ~X] con valor visual aproximado
```

### Si API retorna 404/error:
```
1. Verificar que la URL esté correcta
2. Si es calendario "nextweek" → normal los fines de semana, OMITIR
3. Para otras APIs, marcar [API ERROR: código]
```

---

## Changelog

| Versión | Fecha | Cambios |
|---------|-------|---------|
| 2.0 | 2025-01-XX | Versión inicial con TIER 1 + TIER 2 |
| **2.1** | **2025-01-25** | **Fixes críticos:** |
| | | - URL MVRV corregida: `/mvrv` → `/mvrv-ratio` |
| | | - Agregado proceso de hover para Exchange Reserve Δ% |
| | | - Agregado proceso de hover para HODL Waves % exactos |
| | | - Agregado fallback para calendario API 404 |
| | | - Agregado CoinGecko como alternativa a CMC |
| | | - Agregado extracción de precio BTC y dominance del header |
| | | - Mejorado manejo de errores con instrucciones específicas |
| | | - Agregado checklist de datos requeridos |
| | | - Mejorada sección de reflection en output |