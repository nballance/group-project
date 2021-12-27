Distributed Serverless Workflow for Crytpocurrency price movements

Set up a distributed serverless workflow to automatically detect when jumps/drops occur very rapidly in tracked cryptocurrencies. Will send out a SMS alert to the subscriber so they can determine whether they want to buy/sell more actively monitor.

CloudWatch Events, every minute the tracked cryptocurrencies data will be pulled. CloudWatch Events will trigger a lambda function which will pull data from the Yahoo Finance API 

Lambda (ClockHandler),

Yahoo Finance API, query this for fetching the last known price for the cryptocurrency. Can use the python API (yfinance), install via pip install yfinance

After fetching the last known Sticker price, then update the StockState Dynamo D table

Then the ClockHandler lambda will calculate the change in % and insert into the cryptocurrency ticker table. 

Use dyanamo db stream to see if it surpasses the user-set cadence value.

Fetch all users that care about cryptocurrency ticker and percent combo from the WatchList Dynamo DB table and send out a notification`


