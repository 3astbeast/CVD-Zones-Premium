<p align="center">
  <img src="https://avatars.githubusercontent.com/u/209633456?v=4" width="160" alt="RedTail Indicators Logo"/>
</p>

<h1 align="center">CVD Zones Premium</h1>

<p align="center">
  <b>A Cumulative Volume Delta heatmap indicator for NinjaTrader 8.</b><br>
  Renders a thermal overlay on price candles showing where buying and selling volume concentrates across price levels.
</p>

<p align="center">
  <a href="https://buymeacoffee.com/dmwyzlxstj">
    <img src="https://img.shields.io/badge/☕_Buy_Me_a_Coffee-FFDD00?style=flat-square&logo=buy-me-a-coffee&logoColor=black" alt="Buy Me a Coffee"/>
  </a>
</p>

---

<p align="center">
  <img src="https://raw.githubusercontent.com/3astbeast/CVD-Zones-Premium/refs/heads/main/MGC_2Minute_20260405_162452.png" width="800" alt="RedTail Toolbar Screenshot"/>
</p>

---

## Credit

Original TradingView Pine Script by **[B3AR_Trades](https://www.tradingview.com/u/B3AR_Trades/)**. NinjaTrader 8 conversion by **[@_hawkeye_13](https://twitter.com/_hawkeye_13)** (RedTail Indicators).

---

## Overview

CVD Zones Premium splits each bar's volume into estimated buy and sell components using the bar's OHLC range, then distributes the delta across 62 price bins spanning a configurable lookback range. Each bin is color-mapped to a thermal gradient — bullish delta glows in one color, bearish in another, with intensity proportional to the magnitude. The result is a heatmap painted directly on the candle area showing where volume-weighted buying or selling pressure is concentrated at each price level.

---

## CVD Settings

**Profile Depth** — Controls the lookback period for the volume delta calculation. Shallow uses 100 bars for a fast, reactive heatmap. Balanced (default) uses 300 bars for a broader picture. Deep uses 600 bars for a longer-term view.

**CVD Mode** — Two calculation modes:
- **Net CVD** — Buy volume minus sell volume at each price bin. Shows directional pressure — positive bins glow bullish, negative bins glow bearish.
- **Cumulative CVD** — Buy volume plus sell volume. Shows total activity concentration regardless of direction, with color determined by whether the close is above or below each bin.

**Threshold %** — Filters out bars where the absolute buy/sell imbalance is below this percentage of the maximum imbalance in the lookback range (default: 35%). Reduces noise from low-conviction bars.

**Volume-Weighted Midpoint** — When enabled, assigns each bar's volume to HLC/3 instead of close price, producing a smoother distribution that better represents where volume actually transacted.

**Normalization Approximation** — An alternative normalization method that divides the period's total CVD evenly across bins for a more uniform gradient spread.

---

## Heatmap Display

**Thermal Sensitivity** — Controls the gradient curve:
- **High Contrast** — Only the strongest bins glow, weaker bins stay dark. Best for identifying major imbalance zones.
- **Balanced** — Moderate gradient range.
- **Smooth** — Full gradient from zero to max. Every bin gets some color.

**Gradient Normalization** — Linear (default) or Logarithmic. Logarithmic compresses the range so that moderate-volume bins show more color relative to the peak.

**Heatmap Opacity** — 0 (fully opaque) to 100 (fully transparent). Default: 50%.

**Hide Active Candle** — Clears heatmap bins that overlap the candle's open, close, midpoint, and HLC/3 prices, so the candle body remains readable through the heatmap.

---

## Color Themes

Seven built-in themes with curated bullish/bearish color pairs:

- **Traditional** — Green / Red
- **Modern** — Cyan / Red (default)
- **Heatwave** — Orange / Purple
- **Stealth** — Teal / Pink
- **Aurora** — Green / Indigo
- **Magma** — Pink-white / Deep red
- **Plasma** — Orange / Violet

Plus a **Custom** theme option where you set your own bullish and bearish colors.

---

## Companion Indicator

The companion indicator (CVDZonesPremiumCompanion) mirrors the CVD heatmap onto charts running different bar types for the same instrument. This solves a common problem: you compute the CVD heatmap on a time-based chart (e.g., 5-minute) but trade on a tick or range chart — the companion brings the heatmap to your trading chart without recomputing.

**How It Works**
- Add CVDZonesPremium to any chart (your "source" chart)
- Add CVDZonesPremiumCompanion to a different chart for the same instrument (your "trading" chart)
- The companion discovers the source automatically via a static ConcurrentDictionary registry — no manual linking, no data series configuration
- Set the companion's Source Timeframe Type and Value to match the source chart's bar period

**Cross-Chart Alignment**
- Source bars are aligned onto the companion chart using timestamps, not bar indices
- This means bar types can differ completely — tick charts, range charts, Renko, minute charts — the companion handles the mapping correctly

**Inherited Settings**
- Theme colors, CVD mode, sensitivity, gradient normalization, and opacity are inherited from the source indicator automatically
- Optional opacity override on the companion if you want different transparency on different charts

**Status Label**
- An optional status label in the top-right corner shows connection state: green checkmark when connected, red message with troubleshooting guidance when searching

---

## Installation

Both `.cs` files must be installed — the companion depends on types defined in the main indicator.

1. Download both `CVDZonesPremium.cs` and `CVDZonesPremiumCompanion.cs`
2. Copy both files to `Documents\NinjaTrader 8\bin\Custom\Indicators`
3. Open NinjaTrader (if not already open)
4. In Control Center, go to **New → NinjaScript Editor**
5. Click the **Compile** button — both indicators will compile together
6. Add CVDZonesPremium to your source chart, then add CVDZonesPremiumCompanion to any other chart for the same instrument

---

## Part of the RedTail Indicators Suite

This indicator is part of the [RedTail Indicators](https://github.com/3astbeast/RedTailIndicators) collection — free NinjaTrader 8 tools built for futures traders who demand precision.

---

<p align="center">
  <a href="https://buymeacoffee.com/dmwyzlxstj">
    <img src="https://img.shields.io/badge/☕_Buy_Me_a_Coffee-Support_My_Work-FFDD00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black" alt="Buy Me a Coffee"/>
  </a>
</p>
