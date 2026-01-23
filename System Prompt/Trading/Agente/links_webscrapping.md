# Solicitud: Recolección de Datos de Trading

Necesito que visites las siguientes URLs de análisis cripto. Como muchas usan gráficos interactivos (canvas, SVG, JS), **tomá screenshot de cada página** y luego extraé los datos visibles del screenshot para generar el informe.

## Proceso para cada URL

1. Navegá a la URL
2. Esperá que cargue completamente (3-5 segundos)
3. Tomá screenshot de la zona principal con datos
4. Extraé los valores numéricos visibles en el screenshot
5. Si no podés leer un valor, marcalo como [NO VISIBLE EN SCREENSHOT]

---

## PARTE 1: URLs AUTOMÁTICAS (visitá estas)

**Derivados (Coinglass):**
1. https://www.coinglass.com/pro/futures/LiquidationHeatMap
2. https://www.coinglass.com/pro/futures/LiquidationMap
3. https://www.coinglass.com/pro/futures/OpenInterest
4. https://www.coinglass.com/FundingRate
5. https://www.coinglass.com/LongShortRatio
6. https://www.coinglass.com/pro/futures/hyperliquid-long-short-ratio

**On-Chain (CryptoQuant):**
7. https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-netflow-total
8. https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-reserve

**On-Chain (LookIntoBitcoin):**
9. https://www.lookintobitcoin.com/charts/hodl-waves/
10. https://www.lookintobitcoin.com/charts/mvrv-zscore/
11. https://www.lookintobitcoin.com/charts/pi-cycle-top-indicator/

**Complementarios:**
12. https://alternative.me/crypto/fear-and-greed-index/

---

## PARTE 2: DATOS MANUALES (los agrego yo)

Estos sitios están bloqueados para scraping automático. Voy a pegar los datos manualmente al final:

- **Calendario Económico:** (eventos de alto impacto esta semana)
- **Glassnode LTH/SOPR:** (requiere suscripción paga - omitir)

### Datos de CoinMarketCap API (Global Metrics)

```
BTC Dominance: 59.23%
BTC Dominance 24h Change: +0.04%
ETH Dominance: 11.77%
Total Market Cap: $3.00T
Total Market Cap 24h Change: +0.22%
Total Volume 24h: $101.1B
Volume 24h Change: -19.94%
DeFi Market Cap: $69.5B
DeFi Volume 24h Change: -21.66%
Stablecoin Market Cap: $285.7B
Stablecoin Volume 24h Change: -15.54%
Derivatives Volume 24h: $773B
Derivatives Volume 24h Change: -32.06%
Active Cryptocurrencies: 8,968
Active Exchanges: 917
```

---

## Qué necesito de cada fuente

**Coinglass:**
- Liquidation Heatmap: zonas de liquidez arriba/abajo del precio actual, colores intensos = mayor concentración
- Liquidation Map: barras de liquidez longs (verde) vs shorts (rojo), valores en millones
- Open Interest: OI total en billions y cambio % 24h
- Funding Rate: funding actual de BTC (valor decimal, ej: 0.0045%)
- Long/Short Ratio: ratio global y de top traders
- Hyperliquid L/S: posicionamiento en Hyperliquid

**CryptoQuant:**
- Exchange Netflow: valor en BTC, positivo = entrada, negativo = salida
- Exchange Reserve: tendencia de la curva

**LookIntoBitcoin:**
- HODL Waves: % aproximado en bandas de colores (>1 año vs <3 meses)
- MVRV Z-Score: valor numérico y zona de color (verde/amarillo/rojo)
- Pi Cycle: si las dos líneas (111 DMA y 350 DMA x2) están cerca o cruzándose

**Complementarios:**
- Fear & Greed: número (0-100) y clasificación

---

## Formato del informe

```
# Informe de Datos — Trading POD
Fecha/Hora UTC: [timestamp]

## MERCADO GLOBAL (CoinMarketCap API)
- BTC Dominance: [X%] ([+/-X%] 24h)
- ETH Dominance: [X%]
- Total Market Cap: $[X]T ([+/-X%] 24h)
- Total Volume 24h: $[X]B ([+/-X%] 24h)
- Derivatives Volume 24h: $[X]B ([+/-X%] 24h)
- Stablecoin Market Cap: $[X]B

## DERIVADOS (Coinglass)
- Liquidation Heatmap: Liquidez concentrada en $[X] (arriba) / $[X] (abajo)
- Liquidation Map: Longs $[X]M / Shorts $[X]M
- Open Interest: $[X]B ([+/-X%] 24h)
- Funding BTC: [X%]
- L/S Ratio: Global [X%/X%] / Top Traders [X:1]
- Hyperliquid L/S: [X:1 o datos visibles]

## ON-CHAIN
- Exchange Netflow 24h: [+/-X] BTC — [entrada/salida]
- Exchange Reserve: [creciendo/cayendo/estable]
- HODL Waves: >1y [X%] / <3m [X%]
- MVRV Z-Score: [X] — [zona verde/amarilla/roja]
- Pi Cycle: [sin señal/acercándose/cruzando]

## COMPLEMENTARIOS
- Fear & Greed: [X] ([clasificación])

## DATOS PENDIENTES
- Calendario económico: [PENDIENTE - agregar manualmente]

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
- El BTC Dominance aparece en el header de Coinglass (ej: "Dominance: BTC 57.6%")
- Si una página requiere login y no tenés sesión activa, marcá [REQUIERE LOGIN]
- Si un dato no es visible ni en screenshot, marcá [NO DISPONIBLE]
- Esto es para mi análisis personal de trading