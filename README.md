# Crypto Token Correlation Heatmap

This project analyzes the correlation and volatility of crypto tokens using price data from the CoinGecko Pro API. It provides tools to fetch historical price data, compute correlations, visualize heatmaps, and assess token volatility.

## Features

- Fetch historical price data for multiple tokens from CoinGecko Pro API
- Clean and align time series data for accurate analysis
- Compute and visualize token correlation heatmaps
- Calculate and display token volatility (standard deviation of log returns)
- Save and load processed data for reproducible analysis

## Setup

1. **Clone the repository**  
   Download or clone this project to your local machine.

2. **Install dependencies**  
   Run the following command to install required Python libraries:
   ```
   pip install requests pandas numpy matplotlib seaborn python-dotenv joblib
   ```

3. **API Key**  
   - Sign up for [CoinGecko Pro](https://www.coingecko.com/en/api/pro) and get your API key.
   - Create a `.env` file in the project root:
     ```
     GECKO_API=your_api_key_here
     ```

## Usage

1. **Fetch and Save Token Prices**  
   Run the notebook `01_data.ipynb` to fetch price data for your chosen tokens and save the cleaned DataFrame:
   - Enter token IDs (e.g., `bitcoin,ethereum,solana`) when prompted.
   - Data is saved to `Database/df_prices.joblib`.

2. **Analyze Correlation and Volatility**  
   Open `token_correlation.ipynb` to:
   - Load the saved DataFrame
   - Plot the correlation heatmap
   - Compute and display volatility for each token

## Example

```python
# Load saved prices
import joblib
df_prices = joblib.load("Database/df_prices.joblib")

# Drop missing values
df_prices_clean = df_prices.dropna()

# Correlation heatmap
import seaborn as sns
import matplotlib.pyplot as plt
corr = df_prices_clean.corr()
sns.heatmap(corr, annot=True, cmap='coolwarm')
plt.title("Token Correlation Heatmap")
plt.show()

# Volatility
import numpy as np
returns = df_prices_clean.pct_change().apply(lambda x: np.log1p(x))
volatility = returns.std()
print(volatility)
```

## Notes

- Data alignment is crucial: only timestamps present for all tokens are used.
- For best results, use tokens with high liquidity and trading volume.
- The project is designed for educational and research purposes.

## License

MIT License

## Author

Ruth Arogundade