# Solicitud: Recolección de Datos de Trading - v2.0

Necesito que visites las siguientes URLs de análisis cripto. Como muchas usan gráficos interactivos (canvas, SVG, JS), **tomá screenshot de cada página** y luego extraé los datos visibles del screenshot para generar el informe.

## Proceso para cada URL

1. Navegá a la URL
2. Esperá que cargue completamente (3-5 segundos)
3. Tomá screenshot de la zona principal con datos
4. Extraé los valores numéricos visibles en el screenshot
5. Si no podés leer un valor, marcalo como [NO VISIBLE EN SCREENSHOT]

---

## PARTE 1: URLs AUTOMÁTICAS (visitá estas)

### Derivados (Coinglass)
1. https://www.coinglass.com/pro/futures/LiquidationHeatMap
2. https://www.coinglass.com/pro/futures/LiquidationMap
3. https://www.coinglass.com/pro/futures/OpenInterest
4. https://www.coinglass.com/FundingRate
5. https://www.coinglass.com/LongShortRatio
6. https://www.coinglass.com/pro/futures/hyperliquid-long-short-ratio

### On-Chain TIER 1 - CryptoQuant (señales primarias, refresh ~1h)
7. https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-netflow-total
8. https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-reserve
9. **https://cryptoquant.com/asset/btc/chart/market-indicator/mvrv** ← CRÍTICO para Paso 3

### On-Chain TIER 2 - LookIntoBitcoin (confirmación macro, refresh ~24h)
10. https://www.lookintobitcoin.com/charts/hodl-waves/
11. https://www.lookintobitcoin.com/charts/mvrv-zscore/
12. https://www.lookintobitcoin.com/charts/pi-cycle-top-indicator/

### Complementarios
13. https://alternative.me/crypto/fear-and-greed-index/

---

## PARTE 2: DATOS MANUALES (los agrego yo)

Estos sitios están bloqueados para scraping automático:

### Calendario Económico (API gratuita, sin key)
```
GET https://nfs.faireconomy.media/ff_calendar_thisweek.json
GET https://nfs.faireconomy.media/ff_calendar_nextweek.json
```
Filtrar por `"impact": "High"`

### CoinMarketCap Global Metrics (requiere API key)
```
GET https://pro-api.coinmarketcap.com/v1/global-metrics/quotes/latest
Header: X-CMC_PRO_API_KEY: [TU_KEY]
```

### Glassnode LTH/SOPR
❌ Requiere suscripción paga — omitir (usamos CryptoQuant MVRV + LookIntoBitcoin como proxy)

---

## Qué necesito de cada fuente

### Coinglass
| Página | Datos a extraer |
|--------|-----------------|
| Liquidation Heatmap | Zonas de liquidez arriba/abajo del precio, colores brillantes = alta concentración |
| Liquidation Map | Barras longs (verde) vs shorts (rojo), valores en millones |
| Open Interest | OI total en billions + cambio % 24h |
| Funding Rate | Funding BTC (valor decimal, ej: 0.0045%) |
| Long/Short Ratio | Ratio global + top traders |
| Hyperliquid L/S | Posicionamiento en Hyperliquid |

### CryptoQuant (TIER 1)
| Página | Datos a extraer |
|--------|-----------------|
| Exchange Netflow | Valor en BTC (+entrada / -salida) |
| Exchange Reserve | Valor actual + cambio % 24h + tendencia visual |
| **MVRV Ratio** | **Valor numérico actual (ej: 1.85) — CRÍTICO** |

### LookIntoBitcoin (TIER 2)
| Página | Datos a extraer |
|--------|-----------------|
| HODL Waves | % banda >1 año + % banda <3 meses |
| MVRV Z-Score | Valor numérico + zona de color (verde/amarillo/rojo) |
| Pi Cycle | Estado de las líneas (sin señal/acercándose/cruzando) |

### Complementarios
| Página | Datos a extraer |
|--------|-----------------|
| Fear & Greed | Número (0-100) + clasificación |

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
# Informe de Datos — Trading POD v2.0
Fecha/Hora UTC: [timestamp]
Precio BTC: $[X]

═══════════════════════════════════════════════════════════════
                    MERCADO GLOBAL
═══════════════════════════════════════════════════════════════
**CoinMarketCap API:**
- BTC Dominance: [X%] ([+/-X%] 24h)
- ETH Dominance: [X%]
- Total Market Cap: $[X]T ([+/-X%] 24h)
- Total Volume 24h: $[X]B ([+/-X%] 24h)
- Derivatives Volume 24h: $[X]B ([+/-X%] 24h)
- Stablecoin Market Cap: $[X]B

═══════════════════════════════════════════════════════════════
                    DERIVADOS (Coinglass)
═══════════════════════════════════════════════════════════════
**Liquidez:**
- Heatmap: Concentración arriba en $[X] / abajo en $[X]
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
  └─ Cambio 24h: [+/-X%]
  └─ Tendencia: [creciendo/cayendo/estable]
- Exchange Netflow 24h: [+/-X] BTC
  └─ Interpretación: [entrada/salida de exchanges]

**Anomalía TIER 1:**
[✅ SI / ❌ NO] — Tipo: [ACCUMULATION_STRONG_HOLDING / DISTRIBUTION / NEUTRAL]
Score Tier 1: [X de 5]

**TIER 2 - Confirmación Macro (LookIntoBitcoin):**
- HODL Waves:
  └─ >1 año: [X%]
  └─ <3 meses: [X%]
  └─ Tendencia 7d: [+/-X%] en >1 año
- MVRV Z-Score: [X]
  └─ Zona: [verde <3 / amarilla 3-7 / roja >7]
- Pi Cycle: [sin señal/acercándose/cruzando]

**Señal Macro:**
[BULLISH / BEARISH / NEUTRAL] — Confianza: [ALTA/MEDIA/BAJA]

**PASO 3 INTEGRADO:**
Score Final: [X de 5]
Anomalía Detectada: [tipo]
Califica para Deep Dive: [✅ SI (score ≥3) / ❌ NO]
Confluencia TIER1 + TIER2: [✅ Confirmada / ⚠️ Divergente / ❌ Contradictoria]

<reflection>
¿Los datos de TIER 1 y TIER 2 cuentan la misma historia?
- Si MVRV <1.5 + Reserve ↓ PERO HODL >1y cayendo → DIVERGENCIA (bajar confianza)
- Si MVRV >3.0 + Reserve ↑ Y HODL >1y cayendo → CONFIRMACIÓN (subir confianza)
</reflection>

═══════════════════════════════════════════════════════════════
                    COMPLEMENTARIOS
═══════════════════════════════════════════════════════════════
- Fear & Greed: [X] ([clasificación])

═══════════════════════════════════════════════════════════════
                    CALENDARIO ECONÓMICO
═══════════════════════════════════════════════════════════════
**Eventos High Impact (próximos 7 días):**
| Fecha | Hora UTC | Evento | Moneda | Impacto Esperado |
|-------|----------|--------|--------|------------------|
| [X] | [X] | [X] | [X] | [X] |

═══════════════════════════════════════════════════════════════
                    RESUMEN EJECUTIVO
═══════════════════════════════════════════════════════════════

**Señales Alcistas:**
- [bullet basado en datos]
- [bullet basado en datos]

**Señales Bajistas:**
- [bullet basado en datos]
- [bullet basado en datos]

**Sesgo General:** [BULLISH/BEARISH/NEUTRAL/MIXTO]
**Confianza:** [ALTA/MEDIA/BAJA]

**Activos que califican para Deep Dive (score Paso 3 ≥3):**
- BTC: [SÍ/NO] — Score: [X]

═══════════════════════════════════════════════════════════════
                    DATOS PENDIENTES / ERRORES
═══════════════════════════════════════════════════════════════
- [Listar URLs que fallaron o requieren login]
```

---

## Notas de Implementación

### Prioridades de Extracción
1. **CRÍTICO:** MVRV Ratio de CryptoQuant (sin esto, Paso 3 no funciona)
2. **CRÍTICO:** Exchange Reserve cambio 24h
3. **IMPORTANTE:** HODL Waves >1 año
4. **IMPORTANTE:** Liquidation Heatmap magnet zones

### Manejo de Errores
- Si CryptoQuant requiere login → marcá `[REQUIERE LOGIN]`
- Si un gráfico está en blanco → esperá 5 segundos más y retry
- Si screenshot no captura datos → marcá `[SCREENSHOT INCOMPLETO]`
- BTC Dominance aparece en header de Coinglass (ej: "Dominance: BTC 57.6%")

### Changelog vs v1.0
| Aspecto | v1.0 | v2.0 |
|---------|------|------|
| Paso 3 fuente | "Glassnode (omitir)" | CryptoQuant MVRV + Reserve |
| Estructura | Flat | TIER 1 (1h) + TIER 2 (24h) |
| Thresholds | ❌ No definidos | ✅ Tabla con scores |
| Lag compensation | ❌ No | ✅ TIER 1 intraday, TIER 2 macro |
| Reflection | ❌ Ausente | ✅ Validación de confluencia |
| Output format | Bullets sueltos | Score estructurado + anomaly type |