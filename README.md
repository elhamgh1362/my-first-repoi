# my-first-repoi
just testing github
import requests
import matplotlib.pyplot as pl
from datetime import datetime

def fetch_btc_history():
    url = "https://api.coingecko.com/api/v3/coins/bitcoin/market_chart"
    params = {"vs_currency": "usd", "days": "7"}
    response = requests.get(url, params=params)
    data = response.json()
    return data["prices"]

def plot_prices(prices):
    dates = [datetime.fromtimestamp(p[0]/1000) for p in prices]
    values = [p[1] for p in prices]

    plt.figure(figsize=(10, 5))
    plt.plot(dates, values, label='BTC Price (USD)', color='orange')
    plt.title("Bitcoin Price - Last 7 Days")
    plt.xlabel("Date")
    plt.ylabel("Price in USD")
    plt.grid(True)
    plt.legend()
    plt.tight_layout()
    plt.savefig("btc_price_chart.png")
    plt.show()

if name == "main":
    print("📊 Fetching BTC data...")
    prices = fetch_btc_history()
    print("✅ Data fetched. Plotting chart...")
    plot_prices(prices)
