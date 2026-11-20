# PRATAMA SCREENING

Static market screener for GitHub Pages. No Python server, build tools, or TradingView dependency. Files in this folder can be uploaded directly to the root of a GitHub repository.

## Publish on GitHub Pages

1. Create a GitHub repository, for example `pratama-screening`.
2. Upload `index.html`, `styles.css`, `app.js`, and this README to the repository root.
3. Open **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/(root)`, then save.
4. Open the Pages URL GitHub shows after deployment.
5. In the site, click **Data & API**, enter a Twelve Data API key, then choose **Simpan & sambungkan**.

Crypto uses Binance's public market data endpoints and does not need a key. Stocks and XAU/USD use Twelve Data. The key is saved only in the browser's local storage and is not embedded in these files. Anyone using a public deployment must enter their own API key. Never commit a personal key into this repository.

## Markets and timeframes

- Indonesia stocks: BBCA, BBRI, BMRI, TLKM, ASII, ANTM, GOTO, BREN · D1.
- US stocks: AAPL, MSFT, NVDA, AMZN, GOOGL, META, TSLA, AMD · D1.
- Crypto: BTC, ETH, BNB, SOL, XRP against USDT · M15.
- XAU/USD: M5 only, for the requested scalping workflow.

The screener calculates EMA 9/21, RSI 14, and ATR 14 from returned candles. Click an instrument row to select it in the built-in canvas candlestick chart. The chart overlays EMA 9/21 and the active entry, stop, and target levels. Live ticks update the active candle; new M5/M15 candles are created at interval boundaries. WebSocket connections retry after disconnect. Auto update is enabled by default: if an individual symbol receives no stream tick for 45 seconds, the site refreshes one stale symbol's latest price through the provider API at most once every 30 seconds, rotating through the current market list. This is a fallback; the provider's entitlement and delay still determine how current the returned price is. No charting library or TradingView component is used.

When EMA/RSI conditions produce BUY or SELL, the entry reference is the latest feed price. The indicative stop is 1.5 × ATR(14) from entry and the target is 3 × ATR(14), a nominal 1:2 risk/reward distance before spread and execution costs. WAIT shows no trade levels. ATR is a volatility measure derived from true range, which includes the current high/low and previous close. These are example rule-based levels, not personalized trade instructions. See [True Range formula](https://chartschool.stockcharts.com/table-of-contents/technical-indicators-and-overlays/technical-indicators/true-range).

Price, chart, and signal rows remain empty when a provider cannot return data; the page never substitutes generated/demo prices.

The REST fallback checks only one stale instrument every 30 seconds. Twelve Data documents the `/price` endpoint at one API credit per symbol, so fallback may use up to two API credits per minute while the stream is stale. The WebSocket remains the primary feed and does not trigger this REST fallback when ticks keep arriving.

## Real-time and licensing notes

Real-time availability depends on the data provider, account plan, symbol, exchange, and market-data permissions. Twelve Data documents real-time WebSocket quotes, while its current stock-market listing identifies Indonesia as EOD/delayed on its international coverage. Public IDX display also has licensing restrictions: the IDX terms say internet display of real-time IDX data is restricted to authorized users, and public display without that access is to be delayed/EOD. Therefore this site labels the Indonesia feed as provider/delay-dependent and does not claim public IDX real-time data. Arrange an authorized real-time feed and user access with IDX or a licensed vendor if that is required.

Binance crypto streaming is real-time exchange data for those Binance spot pairs, not a consolidated price across all crypto exchanges. XAU/USD is the provider's gold spot quote and may differ from a broker's CFD quote. Real-time updates require an active WebSocket subscription and available provider quota/entitlements. A static GitHub Pages site cannot keep provider API credentials secret from the browser user; the key is stored locally per browser, not included in the public site files.

Sinyal bersifat informasional, bukan rekomendasi atau jaminan hasil trading. Perhatikan spread, slippage, jam perdagangan, lisensi data, dan risiko.
