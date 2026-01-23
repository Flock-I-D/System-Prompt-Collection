# Solicitud: Recolección de Datos de Trading

Necesito que visites las siguientes URLs de análisis cripto. Como muchas usan gráficos interactivos (canvas, SVG, JS), **tomá screenshot de cada página** y luego extraé los datos visibles del screenshot para generar el informe.

## Proceso para cada URL

1. Navegá a la URL
2. Esperá que cargue completamente (3-5 segundos)
3. Tomá screenshot de la zona principal con datos
4. Extraé los valores numéricos visibles en el screenshot
5. Si no podés leer un valor, marcalo como [NO VISIBLE EN SCREENSHOT]

---

## URLs a visitar

**Derivados (Coinglass):**
1. https://www.coinglass.com/pro/futures/LiquidationHeatMap
2. https://www.coinglass.com/pro/futures/LiquidationMap
3. https://www.coinglass.com/pro/futures/OpenInterest
4. https://www.coinglass.com/FundingRate
5. https://www.coinglass.com/LongShortRatio
6. https://www.coinglass.com/pro/futures/TopTraderPositions
7. https://www.coinglass.com/pro/futures/BitcoinDominance

**On-Chain (Glassnode):**
8. https://studio.glassnode.com/metrics?a=BTC&m=supply.LthSum
9. https://studio.glassnode.com/metrics?a=BTC&m=indicators.Sopr
10. https://studio.glassnode.com/metrics?a=BTC&m=supply.LthNetChange

**On-Chain (CryptoQuant):**
11. https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-netflow-total
12. https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-reserve

**On-Chain (LookIntoBitcoin):**
13. https://www.lookintobitcoin.com/charts/hodl-waves/
14. https://www.lookintobitcoin.com/charts/mvrv-zscore/
15. https://www.lookintobitcoin.com/charts/pi-cycle-top-indicator/

**Complementarios:**
16. https://alternative.me/crypto/fear-and-greed-index/
17. https://www.investing.com/economic-calendar/

---

## Qué necesito de cada fuente

**Coinglass:**
- Liquidation Heatmap: zonas de liquidez arriba/abajo del precio actual, colores intensos = mayor concentración
- Liquidation Map: barras de liquidez longs (verde) vs shorts (rojo), valores en millones
- Open Interest: OI total en billions y cambio % 24h
- Funding Rate: funding actual de BTC (valor decimal, ej: 0.0045%)
- Long/Short Ratio: ratio global y de top traders
- Top Trader Positions: posición neta (net long o net short)
- BTC Dominance: % actual

**Glassnode:**
- LTH Supply: valor en BTC y dirección de la curva (subiendo/bajando)
- SOPR: valor actual (arriba o abajo de 1)
- Net Position Change: barras verdes (acumulación) o rojas (distribución)

**CryptoQuant:**
- Exchange Netflow: valor en BTC, positivo = entrada, negativo = salida
- Exchange Reserve: tendencia de la curva

**LookIntoBitcoin:**
- HODL Waves: % aproximado en bandas de colores (>1 año vs <3 meses)
- MVRV Z-Score: valor numérico y zona de color (verde/amarillo/rojo)
- Pi Cycle: si las dos líneas (111 DMA y 350 DMA x2) están cerca o cruzándose

**Complementarios:**
- Fear & Greed: número (0-100) y clasificación (Extreme Fear/Fear/Neutral/Greed/Extreme Greed)
- Calendario Investing.com: eventos de esta semana con impacto alto (3 toros rojos)

---

## Formato del informe

```
# Informe de Datos — Trading POD
Fecha/Hora UTC: [timestamp]

## DERIVADOS
- Liquidation Heatmap: Liquidez concentrada en $[X] (arriba) / $[X] (abajo)
- Liquidation Map: Longs $[X]M / Shorts $[X]M
- Open Interest: $[X]B ([+/-X%] 24h)
- Funding BTC: [X%]
- L/S Ratio: Global [X%/X%] / Top Traders [X:1]
- Top Traders: [Net Long/Net Short]
- BTC Dominance: [X%]

## ON-CHAIN
- LTH Supply: [X] BTC — [subiendo/bajando/lateral]
- LTH-SOPR: [X] — [arriba/abajo de 1]
- LTH Net Change: [acumulación/distribución]
- Exchange Netflow 24h: [+/-X] BTC — [entrada/salida]
- Exchange Reserve: [creciendo/cayendo/estable]
- HODL Waves: >1y [X%] / <3m [X%]
- MVRV Z-Score: [X] — [zona verde/amarilla/roja]
- Pi Cycle: [sin señal/acercándose/cruzando]

## COMPLEMENTARIOS
- Fear & Greed: [X] ([clasificación])
- Eventos próximos alto impacto:
  - [Evento] - [Fecha/Hora]
  - [Evento] - [Fecha/Hora]

## RESUMEN
Señales alcistas:
- [bullet]
- [bullet]

Señales bajistas:
- [bullet]
- [bullet]

Sesgo general: [BULLISH/BEARISH/NEUTRAL/MIXTO]
Confianza: [Alta/Media/Baja]
```

---

## Notas importantes
- Usá screenshots para extraer datos de gráficos JS/canvas/SVG
- Si una página requiere login y no tenés sesión activa, marcá [REQUIERE LOGIN]
- Si un dato no es visible ni en screenshot, marcá [NO DISPONIBLE]
- Priorizá valores numéricos exactos cuando sean legibles
- Esto es para mi análisis personal de trading