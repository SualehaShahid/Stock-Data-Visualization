#Importing dependencies 
import streamlit as st
import pandas as pd
import numpy as np
import yfinance as yf
import plotly.express as px
import base64
from alpha_vantage.fundamentaldata import FundamentalData
from stocknews import StockNews

#Designing Streamlit Webapplication
st.title("Stock Dashboard ")
st.write("This app helps you track your favourite stocks. Also provide latest NEWS for better investing decisions")
ticker = st.sidebar.text_input('Write Ticker of your favourite stock:', value='', max_chars=5)
start_date=st.sidebar.date_input("Select starting date:")
end_date=st.sidebar.date_input("Select ending date:")

#Retrieving the Data
try:
    data = yf.download(ticker, start=start_date, end=end_date)
    historical_data = yf.Ticker(ticker).history(start=start_date, end=end_date)
    
    #Plotting Data
    fig1 = px.line(data, x=data.index, y=data['Adj Close'], title = ticker)
    st.plotly_chart(fig1)
    
    # Plotting Volume Traded
    fig2 = px.line(data, x=data.index, y=data['Volume'], title='Volume Traded for ' + ticker)
    st.plotly_chart(fig2)

    #Creating tabs
    price_data, historical_price_data, fundamental_data, news = st.tabs(['Price Data', 'Historical Price Data', 'Fundamental Data', 'News'])

    with price_data:
        st.header('Pricing Movements')
        data2= data
        data2['%Change']= data['Adj Close']/data['Adj Close'].shift(1)
        data2.dropna(inplace=True)
        st.write(data2)
        annual_return = data2['%Change'].mean()*252/1000
        st.write(f'The annual return is {annual_return:.2%}')
        risk = np.std(data2['%Change'])*np.sqrt(252)
        st.write(f'The annualized risk is {risk:.2%}')
        st.write('The risk adjusted return is ', annual_return/risk, '%')
        csv = data.to_csv(index=False)
        b64 = base64.b64encode(csv.encode()).decode()
        href = f'<a href="data:file/csv;base64,{b64}" download="{ticker}_data.csv">Download Historical Data as CSV</a>'
        st.markdown(href, unsafe_allow_html=True)

        
    with historical_price_data:
        st.header('Historical Pricing Data')
        st.write(historical_data)

    with fundamental_data:
        key = 'CO6OKR1CBA7O5C47'
        fd = FundamentalData(key, output_format= 'pandas')
        st.subheader('Balance Sheet')
        balance_sheet = fd.get_balance_sheet_annual(ticker)[0]
        bs = balance_sheet.T[2:]
        bs.columns = list(balance_sheet.T.iloc[0])
        st.write(bs)
        st.subheader('Income Statement')
        income_statement = fd.get_income_statement_annual(ticker)[0]
        is1 = income_statement.T[2:]
        is1.columns = list(income_statement.T.iloc[0])
        st.write(is1)
        st.subheader('Cashflow Statement')
        cash_flow = fd.get_cash_flow_annual(ticker)[0]
        cf = cash_flow.T[2:]
        cf.columns = list(cash_flow.T.iloc[0])
        st.write(cf)

    with news:
        st.header(f"What's going for {ticker} ?")
        sn = StockNews(ticker, save_news=False)
        df_news = sn.read_rss()
        for i in range(10):
            st.subheader(f'News{i+1}')
            st.write(df_news['published'][i])
            st.write(df_news['title'][i])
            st.write(df_news['summary'][i])
            title_sentiment = df_news['sentiment_title'][i]
            st.write(f'Title Sentiment{title_sentiment}')
            news_sentiment = df_news['sentiment_summary'][i]
            st.write(f'News Sentiment {news_sentiment}')
except Exception as e:
    st.write(f"Error: {e}")
    st.write("Please Enter a ticker symbol.")
