# Solicitud: Recolección de Datos de Trading

Necesito que visites las siguientes URLs de análisis cripto, extraigas los datos clave visibles en cada una, y me generes un informe consolidado en markdown que pueda copiar y pegar en otro chat.

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
17. https://www.tradingview.com/economic-calendar/

## Qué necesito de cada fuente

**Coinglass:**
- Liquidation Heatmap: zonas de liquidez arriba/abajo del precio, volumen en cada zona
- Liquidation Map: liquidez total longs vs shorts
- Open Interest: OI total y cambio 24h
- Funding Rate: funding actual de BTC
- Long/Short Ratio: ratio global y de top traders
- Top Trader Positions: posición neta
- BTC Dominance: % actual

**Glassnode:**
- LTH Supply: cantidad y tendencia
- SOPR: valor actual
- Net Position Change: acumulación o distribución

**CryptoQuant:**
- Exchange Netflow: entrada/salida neta 24h
- Exchange Reserve: tendencia

**LookIntoBitcoin:**
- HODL Waves: % en bandas >1 año y <3 meses
- MVRV Z-Score: valor y zona
- Pi Cycle: estado actual

**Complementarios:**
- Fear & Greed: valor y clasificación
- Calendario: próximos eventos de alto impacto

## Formato del informe

Generá el informe con este formato:

```
# Informe de Datos — Trading POD
Fecha/Hora UTC: [timestamp]

## DERIVADOS
- Liquidation Heatmap: [datos]
- Liquidation Map: Longs $[X]M / Shorts $[X]M
- Open Interest: $[X]B ([+/-X%] 24h)
- Funding BTC: [X%]
- L/S Ratio: Global [X:1] / Top Traders [X:1]
- BTC Dominance: [X%]

## ON-CHAIN
- LTH Supply: [X] BTC — [acumulando/distribuyendo]
- LTH-SOPR: [X]
- LTH Net Change: [+/-X] BTC
- Exchange Netflow 24h: [+/-X] BTC
- Exchange Reserve: [tendencia]
- HODL Waves >1y: [X%] / <3m: [X%]
- MVRV Z-Score: [X] — [zona]
- Pi Cycle: [estado]

## COMPLEMENTARIOS
- Fear & Greed: [X] ([clasificación])
- Eventos próximos: [lista]

## RESUMEN
Señales alcistas: [bullets]
Señales bajistas: [bullets]
Sesgo general: [BULLISH/BEARISH/NEUTRAL]
```

## Notas
- Si alguna página requiere login, marcá [REQUIERE LOGIN]
- Si un dato no carga, marcá [NO DISPONIBLE]
- Esto es para mi análisis personal de trading