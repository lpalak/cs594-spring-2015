Stock Analysis

*Data Science Question:* To predict the behaviour of certain stocks and do sentiment analysis on the user's tweets

Problem: 	How to gather the historical data i.e. Stock prices 

Solution: 	Use yahoo query language (yql) to get the historical stocks price from  yahoo finance api

Example:	https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20csv%20where%20url%3D%27http%3A%2F%2Fichart.finance.yahoo.com%2Ftable.csv%3Fs%3DGOOG%26a%3D1%26b%3D1%26c%3D2015%26d%3D4%26e%3D28%26f%3D2015%26g%3Dd%27&format=json&diagnostics=true&callback=

File:		stock_quotes.py

Above code will get google stock data for 3 months

/----------------------------------/
Problem: How to gather the user's tweets for stocks.

Solution: Use StockTwits API to get the json data.

Example:	https://api.stocktwits.com/api/2/streams/symbol/GOOG.json.

File:		stock_sentiments.py

This will return the latest 30 messages in json format.


/----------------------------------/

Problem: How to do the sentiment analysis

Solution: Use MongDB's Map/Reduce feature for grouping of user's twits. Use python's TextBlob library to get the sentiments of each twits.

Example: 

for i in data:
        testimonial = TextBlob(i)
        if testimonial.sentiment.subjectivity > 0.3:
            buyCount += 1
        else:
            sellCount += 1

    total = buyCount+sellCount
    buyPercent = (buyCount*100)/total
    sellPercent = (sellCount*100)/total
	
File:		stock_analysis.py
	
Read all the records from DB, and based on the subjectivity  i.e. less than 0.3 in our case, then the sentiment is negative else positive. Save this in DB as well
