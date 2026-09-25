# GTA VI Global Price Index

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22965405.svg)](https://doi.org/10.5281/zenodo.22965405)

What Grand Theft Auto VI costs in **63 markets**: the official Standard and Ultimate Edition prices from the PlayStation Store and the Xbox Store (**103 listings**), converted to US dollars at official reference exchange rates and set against average pay (ILO) and income (World Bank). Collected 2026-09-23; exchange rates of 2026-09-22.

Canonical page, methodology and live table: https://leonidalab.com/data/price-index/

## Findings (Standard Edition, listings where the price includes tax)
- Cheapest: Japan $62.35, India $62.75, South Korea $66.22
- Most expensive: Colombia (Xbox) $106.47, Israel (PlayStation) $105.71, Hungary (PlayStation) $101.42
- Hardest to afford (share of an average month's pay, ILO): India 24.6%, Colombia 21.3%, Ukraine 17.0%

## Files
- `gta6-price-index.csv` - one row per market and store (103 rows)
- `gta6-price-index.json` - the same rows plus every exchange rate used (value, source, date) and column definitions

## Columns
| Column | Meaning |
|---|---|
| country_code, country, region | ISO 3166-1 alpha-2 code, name, region |
| platform, store_code | PlayStation or Xbox; the storefront locale / market code read |
| currency | Currency the store lists in (national, USD or EUR) |
| standard_price, ultimate_price | List prices as shown on the store, local currency |
| standard_usd, ultimate_usd | Local price x fx_usd_per_unit, rounded to cents |
| standard_vs_us_pct | Standard USD price vs the US list price on the same store, % |
| standard_price_final, standard_usd_final | What the buyer pays: the listed price when tax is inside it, listed + tax_rate_pct when a single national rate is added on top, otherwise blank |
| ultimate_premium_pct | Ultimate vs Standard, % |
| standard_share_of_monthly_earnings_pct | standard_usd / earnings_monthly_usd x 100 - only where the ILO figure is from 2021 or later |
| earnings_monthly_usd, earnings_year, earnings_source, earnings_note | ILO average monthly earnings of employees (ILOSTAT DF_EAR_EMTA_SEX_CUR_NB, total, US$ series), latest year, with the ILO's own notes (mean vs median, coverage) |
| standard_share_of_monthly_gni_pct | standard_usd / (gni_per_capita_usd / 12) x 100 |
| gni_per_capita_usd, gni_year | World Bank GNI per capita, Atlas method, current US$ (NY.GNP.PCAP.CD) |
| inflation_pct, inflation_year, high_inflation | World Bank CPI inflation (FP.CPI.TOTL.ZG); high_inflation = above 25% |
| tax_in_listed_price, tax_note, tax_evidence, tax_rate_pct | Whether the listed price includes consumer tax (included / excluded / unverified), with an evidence link |
| on_sale | True if a temporary discount was active (the index records list prices) |
| fx_usd_per_unit, fx_source, fx_date | Exchange rate used and its official source |
| release_utc | Release timestamp in that store listing |
| source_url | The store page or store catalog URL the price was read from |

## Method
- Prices are read directly from each market's official store. Each PlayStation price is checked twice (the store's machine value must equal the displayed price) and every storefront is confirmed to be the real country store, because unknown store codes silently redirect to the US store.
- Exchange rates: ECB euro reference rates, plus the issuing central bank or official source where the ECB publishes none (Argentina BCRA, Colombia TRM, Chile dólar observado, Ukraine NBU, Taiwan CBC; Saudi and UAE pegs). No rate is estimated; where none was available the USD fields are blank.
- Taxes: PlayStation's terms for the Americas say listed prices exclude tax; its terms for Europe, the Middle East, Africa and Oceania say they include it. Xbox catalog prices include tax in most markets. Compare like with like using tax_in_listed_price, or use the *_final columns.

## Caveats
- Pre-launch list prices; stores can change them. Each version is dated.
- US and Canadian prices exclude sales tax, which varies by state/province, so no single after-tax figure exists there.
- Several storefronts price in US dollars, so they match the US price regardless of local purchasing power.
- Pay figures come from national sources collected by the ILO; most are means, some medians (Singapore) or partial coverage (South Korea private sector, Argentina main cities). Indicative, not exact. Figures before 2021 are not used.
- GNI per capita is an average, not a typical wage. Neither the World Bank nor the ILO publishes figures for Taiwan.

## License and citation
CC BY 4.0. Credit **Leonida Lab** with a link to https://leonidalab.com/data/price-index/. ILO and World Bank data are also CC BY 4.0.

> Leonida Lab (2026). GTA VI Global Price Index (Version 2026-09-23) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.22965406

Unofficial. Not affiliated with Rockstar Games, Take-Two Interactive, Sony Interactive Entertainment or Microsoft. No game assets are included.
