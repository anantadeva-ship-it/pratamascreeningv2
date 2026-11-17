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

The screener calculates EMA 9/21 and RSI 14 from returned candles. Price and signal rows remain empty when a provider cannot return data; the page never substitutes generated/demo prices.

## Real-time and licensing notes

Real-time availability depends on the data provider, account plan, symbol, exchange, and market-data permissions. Twelve Data documents real-time WebSocket quotes, while its current stock-market listing identifies Indonesia as EOD/delayed on its international coverage. Public IDX display also has licensing restrictions: the IDX terms say internet display of real-time IDX data is restricted to authorized users, and public display without that access is to be delayed/EOD. Therefore this site labels the Indonesia feed as provider/delay-dependent and does not claim public IDX real-time data. Arrange an authorized real-time feed and user access with IDX or a licensed vendor if that is required.

Binance crypto streaming is real-time exchange data for those Binance spot pairs, not a consolidated price across all crypto exchanges. XAU/USD is the provider's gold spot quote and may differ from a broker's CFD quote. A static GitHub Pages site cannot keep provider API credentials secret from the browser user; the key is stored locally per browser, not included in the public site files.

Sinyal bersifat informasional, bukan rekomendasi atau jaminan hasil trading. Perhatikan spread, slippage, jam perdagangan, lisensi data, dan risiko.
