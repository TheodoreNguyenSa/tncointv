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
   **Downloader code: 1435616** (v1.0.4 — mã cũ 1258763 chỉ còn v1.0.0).
2. **Send Files to TV:** install the app on your TV and your phone, send the APK from your
   phone, open it with a file manager and Install.
3. **USB:** copy the APK to a FAT32 USB stick, plug it into the TV, open it with a file
   manager and Install.

The app checks GitHub once a day and offers to install new versions on the TV itself.

## Data sources (all free, no key, fetched directly from the TV)

| Data | Source |
|---|---|
| Coin prices, top 250, BTC dominance | CoinGecko public API |
| Crypto candles | Yahoo Finance daily candles (1D/1W/1M), Coinbase Exchange public API, Kraken public OHLC (intraday), CoinGecko public OHLC as a last resort for coins the others don't carry (e.g. USDE) |
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

### v1.0.4 (published 2026-11-18 — Downloader code: 1435616)

Audit fixes from Astra (Xingchi API) code review of v1.0.3 — 4 small bugs, ~30 lines. Includes all v1.0.3 fixes below.

- **Offline refresh no longer lies:** a failed refresh used to stamp "Dữ liệu lúc <giờ vừa refresh>" on stale data. Now if every source fails, the old timestamp is kept and the status says "Mất mạng — hiển thị dữ liệu cũ lúc…" (uses the `offline` string that was already written but never used). Partial failures still count as a refresh.
- **Candles refresh in-session:** the candle cache had no expiry, so a chart opened once never got new candles until the app restarted. The cache is now cleared after every successful refresh.
- **Fast coin switching shows the new coin at once:** changing coins mid-load used to leave the old coin in the header until the old request finished. The header now clears to "Đang tải…" immediately.
- **Compact numbers follow the language:** English mode now shows "1.77B ₫" / "42.6M" instead of the Vietnamese "1,77 tỷ ₫" / "42,6 tr".
- **About screen shows the right version:** the in-app version string was still hardcoded "v1.0.3" — now "v1.0.4" (found during the TV check).

### v1.0.3 (staged 2026-11-14, not yet published — Downloader code TBD)

Fixes the layout bugs found on the real TV in v1.0.2 (1920×1080, currency
VND). Includes all v1.0.1/v1.0.2 fixes below.

- **VND numbers no longer break the header:** long values are compacted —
  1.772.380.152 ₫ shows as "1,77 tỷ ₫", 42.600.308.736 volume as
  "42,6 tỷ" (≥ 1 triệu → "tr", ≥ 1 tỷ → "tỷ"). USD/AUD formatting is
  unchanged, small VND values still write out in full ("3.831 ₫"). The
  header is now non-wrapping (OHLC side ellipsises) and the price font
  shrinks if the row still overflows — the header stays on one line in
  every currency.
- **Black title bar gone:** the app now runs fullscreen with no title bar
  (same as GameHub), giving the chart back the ~95px the bar used to eat.
- **No more overlapping axis labels:** the volume overlay's price scale is
  hidden (its "5000.00" used to draw on top of the candle scale's
  "80000.00"); the volume bars still render in the bottom margin.
- **Oscillator time axis hidden:** the RSI/MACD pane shared the main
  chart's time range but drew its own Aug–Nov axis — it no longer does.

### v1.0.2 (staged 2026-11-14, not yet published — Downloader code TBD)

Chart-screen redesign from the user-approved mockup v3 — includes all v1.0.1
fixes below.

- **Layout fits the TV:** overscan-safe padding (~48px sides, 36px bottom)
  replaces the old 18/28/12px, which let the TV crop the bottom hint line
  mid-text. Compact header (symbol + price + change pill + OHLC on one
  line, smaller text), symbol strip + timeframe pills in one compact row,
  chart taking ~70% of the height (~80% when the oscillator is off),
  slim 120px oscillator strip.
- **Remote control that actually works:** real focus zones on the chart
  screen — symbol strip → timeframe row → control buttons — with a visible
  gold focus ring. UP/DOWN moves between zones, LEFT/RIGHT moves within a
  zone (timeframe switches live), OK activates. The symbol strip shows all
  symbols (markets + top-20 coins, scrolls to the focused one) instead of
  blindly cycling ~25 instruments. The bottom buttons (Indicators, Chart
  type, Buy me a coffee, Back) are reachable by remote for the first time —
  before, there was no key path to them at all.
- **Buy me a coffee is a real function:** a "Buy me a coffee" button on the
  home menu and on the chart control row opens a screen with the QR large
  (buymeacoffee.com/toannguyeninoz); BACK returns to where you came from.
  (It used to live only in Settings → About.)
- **Readability kept from v1.0.1:** outlined candle bodies, brighter chart
  text/grid, thicker MA lines.

### v1.0.1 (staged 2026-11-14, not yet published — Downloader code TBD)

- **Coins with no candles anywhere now load:** new CoinGecko OHLC fallback (last in the
  chain) for watchlist coins that have no Coinbase product, no Yahoo ticker and no Kraken
  pair — USDE (Ethena) was the reported case, returning 404 on every source before.
- **No more stale chart under a new title:** a failed load (and switching coins) now
  clears the old candles, volume and last-price label immediately, and the oscillator
  pane hides so the main pane takes the full height instead of leaving an empty area.
  A load requested while another is in flight is queued instead of dropped.
- **Plain-language errors:** a failed chart now says which coin has no candle data
  ("Chưa có dữ liệu nến cho USDE") instead of raw "coinbase: HTTP 404 | yahoo: HTTP 404"
  (technical detail stays in the log only).
- **More readable chart:** outlined candle bodies, brighter chart text/grid, thicker MA
  lines — easier to read from the couch.

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
