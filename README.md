# Risk, Return, Diversification, and Trend-Following Strategies: Evidence from U.S. Technology and Kazakhstan-Related Equities

An independent quantitative finance research project comparing selected U.S. technology and Kazakhstan-related equities using Python.

## Project Overview

This project examines the historical return, risk, correlation, and diversification characteristics of six selected equities. It also compares moving-average trend-following strategies with a Buy & Hold benchmark and evaluates simplified transaction-cost scenarios.

The findings apply to the selected securities and sample periods. They should not be interpreted as conclusions about the entire U.S. or Kazakhstan stock markets.

## Research Question

> How did the selected U.S. technology and Kazakhstan-related equities differ in return, risk, diversification, and moving-average strategy performance during the periods analyzed?

## Author

**Zhanbota Erlan**  
National Physics and Mathematics School (FIZMAT)  
Almaty, Kazakhstan

## Securities Analyzed

| Yahoo Finance ticker | Security | Exchange and security type | Quote currency |
|---|---|---|---|
| AAPL | Apple | Nasdaq common stock | USD |
| MSFT | Microsoft | Nasdaq common stock | USD |
| NVDA | NVIDIA | Nasdaq common stock | USD |
| KSPI | Kaspi.kz | Nasdaq American Depositary Shares (ADS), each representing one common share | USD |
| HSBK.IL | Halyk Bank | London Stock Exchange GDR, each representing 40 common shares | USD |
| KAP.IL | Kazatomprom | London Stock Exchange GDR, each representing one ordinary share | USD |

The `.IL` tickers are the Yahoo Finance identifiers used in the notebook; the London-listed instruments trade under the symbols HSBK and KAP. Instrument details are available from the [Kaspi.kz SEC filing](https://www.sec.gov/Archives/edgar/data/1985487/000095017024049512/kspi-20231231.htm), [London Stock Exchange Halyk Bank profile](https://www.londonstockexchange.com/stock/HSBK/jsc-halyk-bank/company-page), and [London Stock Exchange Kazatomprom profile](https://www.londonstockexchange.com/stock/KAP/joint-stock-company-national-atomic-company-kazatomprom/trade-recap?lang=en).

## Data and Sample Periods

Historical daily price data were obtained from Yahoo Finance using the `yfinance` Python library.

* AAPL, MSFT, NVDA, HSBK.IL, and KAP.IL: requested from 1 January 2020 to 1 January 2025.
* KSPI: requested from 19 January 2024 to 1 January 2025.
* Matched portfolio comparison: 22 January 2024 to 31 December 2024, with **235 matched daily-return observations**.

Daily returns were calculated for each security first. The resulting return series were then aligned by date, and dates without observations for all six securities were excluded from the matched sample. Therefore, 235 refers to matched **return observations**, not price observations.

The current notebook does not explicitly set the `auto_adjust` parameter in `yf.download()`. As a result, adjustment behavior may depend on the installed `yfinance` version. The data retrieval date is also not recorded in the notebook.

## Methodology

The analysis includes:

* Daily returns, annualized arithmetic returns, and volatility
* Pearson correlation and diversification ratios
* Equal-weighted portfolios
* Cumulative returns and maximum drawdowns
* Formal Sharpe ratios
* MA20, MA50, MA100, and MA200 strategies compared with Buy & Hold
* One-way transaction-cost scenarios of 0, 10, and 25 basis points

Because weights are equal, each portfolio's daily return is the simple average of its three components' returns, which implies daily rebalancing to equal weights. Portfolio calculations do not include the transaction costs of this rebalancing.

Moving-average signals are lagged by one trading day. Strategy evaluation begins after the MA200 warm-up period. Because KSPI's available data begin in January 2024, its post-MA200 evaluation period is only about two months; its longer-window strategy results are therefore exploratory. The annual strategy summary also requires corrected warm-up filtering before those results can be reported.

The current notebook uses a fixed annual risk-free-rate input of 4.97%, converted to a daily rate by compounding. The source and reference date for this input are not documented. The strategy backtest assigns zero return to cash positions while subtracting the risk-free rate in Sharpe calculations, which may affect strategy Sharpe estimates.

## Matched-Sample Portfolio Results

| Measure | U.S. Technology Portfolio | Kazakhstan-Related Portfolio |
|---|---:|---:|
| Annualized arithmetic return | 46.86% | 19.95% |
| Annualized volatility | 25.32% | 20.99% |
| Cumulative return | 50.21% | 18.01% |
| Maximum drawdown | −16.99% | −12.32% |
| Average pairwise correlation | 0.391 | 0.116 |
| Diversification ratio | 1.266 | 1.541 |

These results describe the two equal-weighted portfolios over the matched 2024 sample. During this period, the U.S. portfolio had higher realized return and volatility, while the Kazakhstan-related portfolio had lower average pairwise correlation and a higher diversification ratio.

The Sharpe ratios reported in the notebook are 1.659 for the U.S. portfolio and 0.720 for the Kazakhstan-related portfolio. They use the fixed 4.97% annual risk-free-rate input described above.

## Limitations

* The study covers six selected securities, not either country's entire stock market.
* The U.S. group contains only technology companies, while the Kazakhstan-related group spans multiple sectors.
* KSPI's post-MA200 strategy period is very short.
* Transaction-cost scenarios are simplified and do not fully model bid-ask spreads, slippage, taxes, or equal-weight rebalancing costs.
* The annual strategy robustness results require corrected warm-up filtering.
* Historical performance does not predict future results.

## Future Work

Potential extensions include expanding the sample, adding sector-matched comparisons or market indices, lengthening the common sample period, and recalculating the annual and downside strategy analyses after correcting warm-up handling. More realistic transaction-cost and cash-return assumptions could also be examined.

## Repository Structure

```text
US-Kazakhstan-Stock-Analysis/
├── README.md
├── LICENSE
├── paper.pdf
├── Stock_Market_Analysis-2.ipynb
├── requirements.txt
└── figures/


## How to Run

1. Clone or download this repository.
2. Install the required packages:

   ~~~bash
   pip install -r requirements.txt
   ~~~

3. Open the notebook:

   ~~~bash
   jupyter notebook Stock_Market_Analysis-2.ipynb
   ~~~

An internet connection is required to run the notebook’s Yahoo Finance data-download cells.

## Acknowledgements

Historical market data were retrieved from Yahoo Finance using the `yfinance` Python library. This project also uses the open-source Python libraries pandas, NumPy, and Matplotlib. The author thanks the developers and maintainers of these tools.

## Citation

If you reference this project, please cite it as:

> Erlan, Z. (2026). *Risk, Return, Diversification, and Trend-Following Strategies: Evidence from U.S. Technology and Kazakhstan-Related Equities*. Independent Research Project, National Physics and Mathematics School.

## License

See `LICENSE` for the terms of use.
