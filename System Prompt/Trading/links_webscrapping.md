# Webscrapping Trading Data - v3.0 COMPACT

> **CONFIRMACIÓN:** Ejecutar estas instrucciones sin pedir confirmación adicional.
> Recolectar datos → Generar informe → Guardar archivo.

---

## PROCESO GENERAL

1. Visitar URL → Esperar 5 seg → Screenshot → Extraer datos
2. Si no podés leer un valor → `[NO VISIBLE]`
3. Si requiere hover → hacer hover y capturar tooltip

---

## PROCESOS ESPECIALES

### Liquidation Heatmap (niveles EXACTOS, no rangos)
- Identificar zonas color **amarillo/verde brillante**
- Leer precio **exacto** del eje Y (ej: $89,200, NO "$80K-90K")
- Reportar: `Magnet ARRIBA: $[X] | Magnet ABAJO: $[X]`

### Liquidation Map (valores EXACTOS)
- Leer valores numéricos de las barras (en $M)
- Reportar: `Longs: $[X]M | Shorts: $[X]M`

### Exchange Reserve Δ% (cálculo manual)
1. Hover punto ACTUAL → anotar BTC
2. Hover punto HACE 24H → anotar BTC
3. Calcular: `Δ% = ((actual - hace24h) / hace24h) × 100`

### HODL Waves / MVRV Z-Score
- Hover sobre banda/línea en extremo derecho → leer tooltip
- Si no hay tooltip → `[ESTIMADO ~X%]`

---

## URLs A VISITAR

### Coinglass (Derivados)
| # | URL | Extraer |
|---|-----|---------|
| 1 | coinglass.com/pro/futures/LiquidationHeatMap | Magnet zones EXACTAS arriba/abajo |
| 2 | coinglass.com/pro/futures/LiquidationMap | $M longs vs shorts EXACTOS |
| 3 | coinglass.com/pro/futures/OpenInterest | OI total $B + Δ% 24h |
| 4 | coinglass.com/FundingRate | Funding BTC (ej: 0.0045%) |
| 5 | coinglass.com/LongShortRatio | Global % + Top Traders ratio |
| 6 | coinglass.com/pro/futures/Hyperliquid/HyperliquidLongShortRatio | Ratio L/S Hyperliquid |

**BONUS del header:** Precio BTC + BTC Dominance %

### CryptoQuant (TIER 1 On-Chain)
| # | URL | Extraer |
|---|-----|---------|
| 7 | cryptoquant.com/asset/btc/chart/exchange-flows/exchange-netflow-total | Netflow 24h en BTC (+/-) |
| 8 | cryptoquant.com/asset/btc/chart/exchange-flows/exchange-reserve | Reserve BTC + **Δ% 24h calculado** |
| 9 | cryptoquant.com/asset/btc/chart/market-indicator/mvrv-ratio | **MVRV Ratio (CRÍTICO)** |

### LookIntoBitcoin (TIER 2 Macro)
| # | URL | Extraer |
|---|-----|---------|
| 10 | lookintobitcoin.com/charts/hodl-waves/ | % banda >1 año + <3 meses |
| 11 | lookintobitcoin.com/charts/mvrv-zscore/ | Valor + zona color |
| 12 | lookintobitcoin.com/charts/pi-cycle-top-indicator/ | ¿Líneas cruzando? |

### Complementarios
| # | URL | Extraer |
|---|-----|---------|
| 13 | alternative.me/crypto/fear-and-greed-index/ | Número 0-100 + clasificación |

---

## FORMATO OUTPUT

```markdown
# Trading Data Report
Fecha/Hora UTC: [timestamp]
Precio BTC: $[X] | Dominance: [X%]

## DERIVADOS (Coinglass)
- Magnet ARRIBA: $[exacto] | ABAJO: $[exacto]
- Liquidations: Longs $[X]M / Shorts $[X]M
- OI: $[X]B ([+/-X%] 24h)
- Funding BTC: [X%]
- L/S Global: [X%/X%] | Top Traders: [X:1]
- Hyperliquid L/S: [X:1]

## ON-CHAIN TIER 1 (CryptoQuant)
- MVRV Ratio: [X] → Zona: [Acc/Neutral/Dist]
- Exchange Reserve: [X] BTC | Δ24h: [+/-X%]
  └─ (actual: [X] vs hace24h: [X])
- Netflow 24h: [+/-X] BTC

## ON-CHAIN TIER 2 (LookIntoBitcoin)
- HODL >1y: [X%] | <3m: [X%]
- MVRV Z-Score: [X] → Zona: [verde/amarilla/roja]
- Pi Cycle: [sin señal/cruzando]

## SENTIMIENTO
- Fear & Greed: [X] ([clasificación])

## ERRORES/PENDIENTES
- [Listar si hubo problemas]
```

---

## ERRORES COMUNES

| Problema | Solución |
|----------|----------|
| Requiere login | Marcar `[LOGIN REQUERIDO]` |
| Gráfico en blanco | Esperar 5s + refresh |
| Tooltip no aparece | Click en punto o estimar con `[ESTIMADO]` |
| Heatmap sin zonas claras | `[SIN MAGNET DEFINIDO]` |