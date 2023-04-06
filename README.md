**Stock Dashboard Application**

The Stock Dashboard Application is a web application that helps users track their favorite stocks and provides the latest news to make informed investing decisions. The application is built using Streamlit, a Python library for creating data-driven apps, and integrates several data sources, including yfinance, Alpha Vantage, and StockNews.

**Installation**

To run the application, you need to have Python 3.7 or later installed on your system. 

**Usage**

To launch the application, run the following command from the project directory:

streamlit run app.py
The application will launch in your web browser at http://localhost:8501.

Once the application is launched, you can enter the ticker symbol of your favorite stock and select the start and end dates for the historical data you want to analyze. The application retrieves the data using the Yahoo Finance API and displays the stock price and volume traded as line charts.

You can also view the pricing movements and historical pricing data for the selected stock, as well as the balance sheet, income statement, and cashflow statement using the Alpha Vantage API. Additionally, you can view the latest news for the selected stock using the StockNews API.

**Contributing**

If you would like to contribute to the project, please fork the repository and create a pull request. We welcome contributions of all types, including bug fixes, new features, and documentation improvements.

**Acknowledgments**

This project was inspired by the many great resources and tools available for analyzing stock data. We would like to thank the creators and contributors of Streamlit, yfinance, Alpha Vantage, and StockNews for making this project possible.
