# TNCoinTV — Crypto & Markets Chart for Android TV

A free TradingView-style chart app for Android TV / Google TV, in Vietnamese and English.
Watch Bitcoin, altcoins, gold, the S&P 500 and the ASX 200 on the big screen — no account,
no ads, no subscription.

Inspired by the community project [Moon TV](https://moontv.vn/) (a free TradingView-style web
chart with its own buy/sell and altcoin-season indicators). TNCoinTV is a separate, original
app: it does not copy Moon TV's name, data or proprietary indicators — it computes its own
trend table and signals from free public data.

## What you see

- **Overview** — five markets: BTC, Altcoin/BTC ratio, Gold (GC=F), S&P 500, ASX 200. Each
  card shows the closing price, the 7-day change and the trend (Rising / Falling / Sideways),
  plus BTC Dominance and the Fear & Greed Index.
- **Trend & swings** — a 7 / 14 / 30 / 60 / 90 / 180 / 360-day table per market: % change,
  current swing (how many days up/down and by how much), closing low–high range, position
  vs SMA 20/50/200, and market structure (higher highs, lower lows…). Swings are computed
  from closing prices with a per-market reversal threshold, the way Moon TV describes it.
- **Chart** — full-screen candlesticks (Lightweight Charts, Apache-2.0, bundled locally),
  timeframes 1H / 4H / 1D / 1W / 1M, indicators MA 20/50/200, Bollinger Bands, Volume,
  RSI (14) or MACD, candle/line style. Left/Right changes the timeframe, Up/Down changes
  the symbol.
- **Watchlist** — top 20 coins by market cap (CoinGecko) with 24h change and 7-day
  sparklines, plus six ASX blue chips: CBA, BHP, CSL, NAB, WBC, ANZ.
- **Settings** — language (Tiếng Việt / English), currency (USD / AUD / VND), data refresh
  interval (1 / 5 / 15 minutes), about + data-source credits + Buy-me-a-coffee QR.

Remote: Up/Down select, Left/Right changes timeframe (chart) or day range (trend) or
currency (home), OK confirms, Back goes to the previous screen.

## Install

On your Android TV / Google TV (Android 5.0+):

1. **Downloader (easiest):** install the free Downloader app from the Play Store, open it,
   type the code from the release post, press Go, then Install.
   **Downloader code: 1258763**
2. **Send Files to TV:** install the app on your TV and your phone, send the APK from your
   phone, open it with a file manager and Install.
3. **USB:** copy the APK to a FAT32 USB stick, plug it into the TV, open it with a file
   manager and Install.

The app checks GitHub once a day and offers to install new versions on the TV itself.

## Data sources (all free, no key, fetched directly from the TV)

| Data | Source |
|---|---|
| Coin prices, top 250, BTC dominance | CoinGecko public API |
| Crypto candles | Yahoo Finance daily candles (1D/1W/1M), Coinbase Exchange public API, Kraken public OHLC (intraday) |
| SPX, ASX 200, gold, FX rates (AUD/USD, USD/VND) | Yahoo Finance chart API (public, no key) |
| Fear & Greed Index | alternative.me public API |
| Charts | Lightweight Charts v4.2.3 (Apache License 2.0), bundled in the APK |

The Altcoin/BTC ratio is an estimate computed from the top 250 coins on CoinGecko
(excluding stablecoins); its 7-day change is estimated from the 7-day price changes.
Data refreshes at most once a minute; the last good data is cached and shown with its
timestamp when offline.

**VN-Index is not in v1.0.0.** No stable free source was found on 2026-11-14 (Yahoo has no
VN-Index symbol, Stooq returned nothing, FireAnt 404, CafeF serves no data). It will be
added once a stable free source is found — nothing is faked in the meantime.

## Disclaimer

Data is for reference only, not investment advice. Market data can be delayed or
incomplete; indicator signals are context for research, never a guarantee.

## Changelog

### v1.0.0

- First release: Overview (5 markets + dominance + Fear & Greed), Trend & swings table
  (7–360 days), candlestick chart with MA/Bollinger/Volume/RSI/MACD, Watchlist (Top 20
  crypto + 6 ASX blue chips), bilingual VI/EN, currency USD/AUD/VND, auto-update.

## Support

Made by Toan Nguyen In Oz — free for the Vietnamese community in Australia and everywhere.

- ☕ Buy me a coffee: https://buymeacoffee.com/toannguyeninoz
- 💛 PayPal (direct): https://www.paypal.me/ToanNguyen189

## Download

Get the APK from the [latest release](https://github.com/TheodoreNguyenSa/tncointv/releases/latest).
