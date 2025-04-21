# quick-backtest

**quick-backtest** is a lightweight Python framework for backtesting quantitative trading strategies. It simplifies the process of data ingestion, strategy simulation, risk management, and performance analysis, allowing you to validate and iterate on your ideas quickly.

## Features

- **Data Ingestion**: Load historical price data from CSV files or APIs (e.g., Yahoo Finance, Alpha Vantage).
- **Strategy Interface**: Define custom trading strategies by implementing entry and exit signals in a clear API.
- **Portfolio Simulation**: Simulate orders, position sizing, transaction costs, slippage, and capital allocation.
- **Performance Metrics**: Automatically compute key statistics including total return, Sharpe ratio, maximum drawdown, and drawdown duration.
- **Reporting**: Generate interactive backtest reports and visualizations using Plotly or Matplotlib.
- **Extensible Architecture**: Modular design to plug in new data sources, risk models, and execution engines.

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/aldozhang/quick-backtest.git
   cd quick-backtest
   ```

2. Create and activate a virtual environment:

   ```bash
   python3 -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

## Quick Start

1. **Prepare Data**  
   Place your historical price data in the `data/` directory as CSV files with columns: `date, open, high, low, close, volume`.

2. **Define a Strategy**  
   Create a Python file in `strategies/` inheriting from `BaseStrategy` and implement the `generate_signals()` method.

   ```python
   from quick_backtest import BaseStrategy

   class MovingAverageCrossStrategy(BaseStrategy):
       def generate_signals(self, data):
           # Example: simple moving average crossover
           data['ma_short'] = data['close'].rolling(20).mean()
           data['ma_long'] = data['close'].rolling(50).mean()
           data['signal'] = (data['ma_short'] > data['ma_long']).astype(int)
           return data
   ```

3. **Run Backtest**  
   Execute the backtest with your chosen strategy:

   ```bash
   python run_backtest.py --strategy strategies/moving_average_cross.py --data data/SPY.csv
   ```

4. **View Report**  
   After completion, view the generated HTML report in `reports/`.

## Project Structure

```
quick-backtest/
├── data/                  # Historical CSV data files
├── reports/               # Generated backtest reports
├── strategies/            # Custom strategy implementations
├── quick_backtest/        # Core framework modules
│   ├── __init__.py
│   ├── backtester.py      # Engine to run simulations
│   ├── metrics.py         # Performance metrics calculations
│   └── base_strategy.py   # BaseStrategy class definition
├── run_backtest.py        # CLI entry point for running backtests
├── requirements.txt       # Python dependencies
└── README.md              # Project overview and instructions
```

## Contributing

Contributions, issues, and feature requests are welcome! Please open an issue or submit a pull request.

## License

This project is licensed under the MIT License.