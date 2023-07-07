---
title: StatsForecast ⚡️
---

::: {.cell 0=‘h’ 1=‘i’ 2=‘d’ 3=‘e’}

<details>
<summary>Code</summary>

``` python
%load_ext autoreload
%autoreload 2
```

</details>

:::

::: {.cell 0=‘h’ 1=‘i’ 2=‘d’ 3=‘e’}

<details>
<summary>Code</summary>

``` python
import warnings
warnings.simplefilter('ignore')

import logging
logging.getLogger('statsforecast').setLevel(logging.ERROR)
```

</details>

:::

> StatsForecast offers a collection of popular univariate time series
> forecasting models optimized for high performance and scalability.

## Installation {#installation}

You can install `StatsForecast` with:

``` python
pip install statsforecast
```

or

``` python
conda install -c conda-forge statsforecast
```

Vist our [Installation
Guide](./docs/getting-started/0_Installation.ipynb) for further
instructions.

## Quick Start {#quick-start}

**Minimal Example**

``` python
from statsforecast import StatsForecast
from statsforecast.models import AutoARIMA

sf = StatsForecast(
    models = [AutoARIMA(season_length = 12)],
    freq = 'M'
)

sf.fit(df)
sf.predict(h=12, level=[95])
```

**Get Started with this [quick
guide](../nbs/docs/getting-started/1_Getting_Started_short.ipynb).**

**Follow this [end-to-end
walkthrough](../nbs/docs/getting-started/2_Getting_Started_complete.ipynb)
for best practices.**

## Why? {#why}

Current Python alternatives for statistical models are slow, inaccurate
and don’t scale well. So we created a library that can be used to
forecast in production environments or as benchmarks. `StatsForecast`
includes an extensive battery of models that can efficiently fit
millions of time series.

## Features {#features}

-   Fastest and most accurate implementations of `AutoARIMA`, `AutoETS`,
    `AutoCES`, `MSTL` and `Theta` in Python.
-   Out-of-the-box compatibility with Spark, Dask, and Ray.
-   Probabilistic Forecasting and Confidence Intervals.
-   Support for exogenous Variables and static covariates.
-   Anomaly Detection.
-   Familiar sklearn syntax: `.fit` and `.predict`.

## Highlights {#highlights}

-   Inclusion of `exogenous variables` and `prediction intervals` for
    ARIMA.
-   20x
    [faster](https://github.com/Nixtla/statsforecast/tree/main/experiments/arima)
    than `pmdarima`.
-   1.5x faster than `R`.
-   500x faster than `Prophet`.
-   4x
    [faster](https://github.com/Nixtla/statsforecast/tree/main/experiments/ets)
    than `statsmodels`.
-   Compiled to high performance machine code through
    [`numba`](https://numba.pydata.org/).
-   1,000,000 series in [30
    min](https://github.com/Nixtla/statsforecast/tree/main/experiments/ray)
    with [ray](https://github.com/ray-project/ray).
-   Replace FB-Prophet in two lines of code and gain speed and accuracy.
    Check the experiments
    [here](https://github.com/Nixtla/statsforecast/tree/main/experiments/arima_prophet_adapter).
-   Fit 10 benchmark models on **1,000,000** series in [under **5
    min**](https://github.com/Nixtla/statsforecast/tree/main/experiments/benchmarks_at_scale).

Missing something? Please open an issue or write us in
[![Slack](https://img.shields.io/badge/Slack-4A154B?&logo=slack&logoColor=white.png)](https://join.slack.com/t/nixtlaworkspace/shared_invite/zt-135dssye9-fWTzMpv2WBthq8NK0Yvu6A)

## Examples and Guides {#examples-and-guides}

📚 [End to End
Walkthrough](https://nixtla.github.io/statsforecast/docs/getting-started/getting_started_complete.html):
Model training, evaluation and selection for multiple time series

🔎 [Anomaly
Detection](https://nixtla.github.io/statsforecast/docs/tutorials/anomalydetection.html):
detect anomalies for time series using in-sample prediction intervals.

👩‍🔬 [Cross
Validation](https://nixtla.github.io/statsforecast/docs/tutorials/crossvalidation.html):
robust model’s performance evaluation.

❄️ [Multiple
Seasonalities](https://nixtla.github.io/statsforecast/docs/tutorials/multipleseasonalities.html):
how to forecast data with multiple seasonalities using an MSTL.

🔌 [Predict Demand
Peaks](https://nixtla.github.io/statsforecast/docs/tutorials/electricitypeakforecasting.html):
electricity load forecasting for detecting daily peaks and reducing
electric bills.

📈 [Intermittent
Demand](https://nixtla.github.io/statsforecast/docs/tutorials/intermittentdata.html):
forecast series with very few non-zero observations.

🌡️ [Exogenous
Regressors](https://nixtla.github.io/statsforecast/docs/how-to-guides/exogenous.html):
like weather or prices

## Models {#models}

### Automatic Forecasting {#automatic-forecasting}

Automatic forecasting tools search for the best parameters and select
the best possible model for a group of time series. These tools are
useful for large collections of univariate time series.

| Model                                                                              | Point Forecast | Probabilistic Forecast | Insample fitted values | Probabilistic fitted values |
|:-----------------------------|:---------:|:---------:|:---------:|:---------:|
| [AutoARIMA](https://nixtla.github.io/statsforecast/src/core/models.html#autoarima) |       ✅       |           ✅           |           ✅           |             ✅              |
| [AutoETS](https://nixtla.github.io/statsforecast/src/core/models.html#autoets)     |       ✅       |           ✅           |           ✅           |             ✅              |
| [AutoCES](https://nixtla.github.io/statsforecast/src/core/models.html#autoces)     |       ✅       |           ✅           |           ✅           |             ✅              |
| [AutoTheta](https://nixtla.github.io/statsforecast/src/core/models.html#autotheta) |       ✅       |           ✅           |           ✅           |             ✅              |

## ARIMA Family {#arima-family}

These models exploit the existing autocorrelations in the time series.

| Model                                                                                        | Point Forecast | Probabilistic Forecast | Insample fitted values | Probabilistic fitted values |
|:-----------------------------|:---------:|:---------:|:---------:|:---------:|
| [ARIMA](https://nixtla.github.io/statsforecast/src/core/models.html#arima)                   |       ✅       |           ✅           |           ✅           |             ✅              |
| [AutoRegressive](https://nixtla.github.io/statsforecast/src/core/models.html#autoregressive) |       ✅       |           ✅           |           ✅           |             ✅              |

### Theta Family {#theta-family}

Fit two theta lines to a deseasonalized time series, using different
techniques to obtain and combine the two theta lines to produce the
final forecasts.

| Model                                                                                                      | Point Forecast | Probabilistic Forecast | Insample fitted values | Probabilistic fitted values |
|:-----------------------------|:---------:|:---------:|:---------:|:---------:|
| [Theta](https://nixtla.github.io/statsforecast/src/core/models.html#theta)                                 |       ✅       |           ✅           |           ✅           |             ✅              |
| [OptimizedTheta](https://nixtla.github.io/statsforecast/src/core/models.html#optimizedtheta)               |       ✅       |           ✅           |           ✅           |             ✅              |
| [DynamicTheta](https://nixtla.github.io/statsforecast/src/core/models.html#dynamictheta)                   |       ✅       |           ✅           |           ✅           |             ✅              |
| [DynamicOptimizedTheta](https://nixtla.github.io/statsforecast/src/core/models.html#dynamicoptimizedtheta) |       ✅       |           ✅           |           ✅           |             ✅              |

### Multiple Seasonalities {#multiple-seasonalities}

Suited for signals with more than one clear seasonality. Useful for
low-frequency data like electricity and logs.

| Model                                                                    | Point Forecast | Probabilistic Forecast | Insample fitted values | Probabilistic fitted values |
|:-----------------------------|:---------:|:---------:|:---------:|:---------:|
| [MSTL](https://nixtla.github.io/statsforecast/src/core/models.html#mstl) |       ✅       |           ✅           |           ✅           |             ✅              |

### GARCH and ARCH Models {#garch-and-arch-models}

Suited for modeling time series that exhibit non-constant volatility
over time. The ARCH model is a particular case of GARCH.

| Model                                                                      | Point Forecast | Probabilistic Forecast | Insample fitted values | Probabilistic fitted values |
|:-----------------------------|:---------:|:---------:|:---------:|:---------:|
| [GARCH](https://nixtla.github.io/statsforecast/src/core/models.html#garch) |       ✅       |           ✅           |           ✅           |             ✅              |
| [ARCH](https://nixtla.github.io/statsforecast/src/core/models.html#arch)   |       ✅       |           ✅           |           ✅           |             ✅              |

### Baseline Models {#baseline-models}

Classical models for establishing baseline.

| Model                                                                                                      | Point Forecast | Probabilistic Forecast | Insample fitted values | Probabilistic fitted values |
|:-----------------------------|:---------:|:---------:|:---------:|:---------:|
| [HistoricAverage](https://nixtla.github.io/statsforecast/src/core/models.html#historicaverage)             |       ✅       |           ✅           |           ✅           |             ✅              |
| [Naive](https://nixtla.github.io/statsforecast/src/core/models.html#naive)                                 |       ✅       |           ✅           |           ✅           |             ✅              |
| [RandomWalkWithDrift](https://nixtla.github.io/statsforecast/src/core/models.html#randomwalkwithdrift)     |       ✅       |           ✅           |           ✅           |             ✅              |
| [SeasonalNaive](https://nixtla.github.io/statsforecast/src/core/models.html#seasonalnaive)                 |       ✅       |           ✅           |           ✅           |             ✅              |
| [WindowAverage](https://nixtla.github.io/statsforecast/src/core/models.html#windowaverage)                 |       ✅       |                        |                        |                             |
| [SeasonalWindowAverage](https://nixtla.github.io/statsforecast/src/core/models.html#seasonalwindowaverage) |       ✅       |                        |                        |                             |

### Exponential Smoothing {#exponential-smoothing}

Uses a weighted average of all past observations where the weights
decrease exponentially into the past. Suitable for data with clear trend
and/or seasonality. Use the `SimpleExponential` family for data with no
clear trend or seasonality.

| Model                                                                                                                                      | Point Forecast | Probabilistic Forecast | Insample fitted values | Probabilistic fitted values |
|:-----------------------------|:---------:|:---------:|:---------:|:---------:|
| [SimpleExponentialSmoothing](https://nixtla.github.io/statsforecast/src/core/models.html#simpleexponentialsmoothing)                       |       ✅       |                        |                        |                             |
| [SimpleExponentialSmoothingOptimized](https://nixtla.github.io/statsforecast/src/core/models.html#simpleexponentialsmoothingoptimized)     |       ✅       |                        |                        |                             |
| [SeasonalExponentialSmoothing](https://nixtla.github.io/statsforecast/src/core/models.html#seasonalexponentialsmoothing)                   |       ✅       |                        |                        |                             |
| [SeasonalExponentialSmoothingOptimized](https://nixtla.github.io/statsforecast/src/core/models.html#seasonalexponentialsmoothingoptimized) |       ✅       |                        |                        |                             |
| [Holt](https://nixtla.github.io/statsforecast/src/core/models.html#holt)                                                                   |       ✅       |           ✅           |           ✅           |             ✅              |
| [HoltWinters](https://nixtla.github.io/statsforecast/src/core/models.html#holtwinters)                                                     |       ✅       |           ✅           |           ✅           |             ✅              |

### Sparse or Inttermitent {#sparse-or-inttermitent}

Suited for series with very few non-zero observations

| Model                                                                                            | Point Forecast | Probabilistic Forecast | Insample fitted values | Probabilistic fitted values |
|:-----------------------------|:---------:|:---------:|:---------:|:---------:|
| [ADIDA](https://nixtla.github.io/statsforecast/src/core/models.html#adida)                       |       ✅       |                        |                        |                             |
| [CrostonClassic](https://nixtla.github.io/statsforecast/src/core/models.html#crostonclassic)     |       ✅       |                        |                        |                             |
| [CrostonOptimized](https://nixtla.github.io/statsforecast/src/core/models.html#crostonoptimized) |       ✅       |                        |                        |                             |
| [CrostonSBA](https://nixtla.github.io/statsforecast/src/core/models.html#crostonsba)             |       ✅       |                        |                        |                             |
| [IMAPA](https://nixtla.github.io/statsforecast/src/core/models.html#imapa)                       |       ✅       |                        |                        |                             |
| [TSB](https://nixtla.github.io/statsforecast/src/core/models.html#tsb)                           |       ✅       |                        |                        |                             |

## How to contribute {#how-to-contribute}

See
[CONTRIBUTING.md](https://github.com/Nixtla/statsforecast/blob/main/CONTRIBUTING.md).

## Citing {#citing}

``` bibtex
@misc{garza2022statsforecast,
    author={Federico Garza, Max Mergenthaler Canseco, Cristian Challú, Kin G. Olivares},
    title = {{StatsForecast}: Lightning fast forecasting with statistical and econometric models},
    year={2022},
    howpublished={{PyCon} Salt Lake City, Utah, US 2022},
    url={https://github.com/Nixtla/statsforecast}
}
```

