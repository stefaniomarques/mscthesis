# Data Sources

Raw data files are not redistributed in this repository. All series are public and can
be retrieved directly from the sources below.

| Variable | Source | Notes |
|---|---|---|
| Residential gas demand (GWh) | CSO / Gas Networks Ireland | Metered, billing-derived volumes |
| Gas price index | CSO Consumer Price Index (2015=100) | |
| Electricity price index | CSO Consumer Price Index (2015=100) | |
| Real household consumption | CSO Quarterly National Accounts | Constant prices, not seasonally adjusted |
| Cumulative BER certificates | CSO Domestic Building Energy Ratings, Table 1 | |
| Heating degree days | Met Éireann | Base 15.5°C |

The R package [`csodata`](https://github.com/JosieMac/csodata) provides programmatic
access to most CSO tables used here, including table `EBQ02` (domestic BER ratings by
energy band), referenced in the thesis as a candidate variable for future work.

All series cover 2014 Q1–2024 Q4 (N = 44 quarterly observations).
