# binance-crypto-trading-bot

> A cryptocurrency trading bot that automates long and short trades on a bunch of USDT pairs. It uses a simple strategy using fractal indicator combined with Alligator indicator (exponential moving averages) from Bill Williams.

## Warning

**This bot is not intended to make anyone rich or make money. Its main purpose is educational and learn about the binance API, websockets, some candlestick or signal processing and Telegram chatbot among others.**

**Use it at your own risk. I am not responsible for any loss incurred directly or indirectly by using this code. Please read [disclaimer](#disclaimer) before using this code.**

## Main features

- The bot works with a bunch of USDT pairs that can be modified at _variables.py_ file.
- Use of Binance API in order to obtain past candlestick price information.
- Use of websockets in order to retrieve real-time candlestick data from Binance.
- The default timeframe is 5 minute candlestick, the user can change it to their preference.
- Default x5 margin leverage, the user can change the leverage to their preference.
- Candlestick processing and indicator calculations on real-time.
- Use of Telegram bot API.
- Real-time communication between the trading bot and the Telegram bot about recent trades, graphics, overall user position and more.
- Wallet simulation so the user can test the bot without investing real money or creating a Binance account.

## Trading bot

### Some constants that can be changed

- `RSI_PERIOD = 14`: The period of RSI calculation (RSI not used by default, but the user can use it to check for market conditions)
- `INIT_USDT = 1000`: Initial USDT amount to invest
- `INIT_BNB = 10`: Initial BNB amount to pay fees

- `MAX_CURRENT_CRYPTOS = 20`: Stop buying if this number of positions are open. Also, it will be invested the current USDT divided by `MAX_CURRENT_CRYPTOS` on each trade.
- `MIN_USDT = 200`: Stop buying if this amount of current USDT is reached

- `RRRATIO = 1.5`: Risk Reward Ratio for the target price calculation
- `LEVERAGE = 5`: Leverage for margin trading
- `MAKERFEERATE = 0.00018`: The percentage (per one) of maker fee
- `TAKERFEERATE = 0.00036`: The percentage (per one) of taker fee

## Telegram bot

### Commands

Most commands are flexible, so the bot may understand a command that is not perfectly typed.

#### `/start`

Start the conversation with the bot. It is necessary to start the bot with this command, so it will internally check wether the user has access and start sending the trades.

#### `thresholds of <pair>`

Show the sell limit and stop loss thresholds calculated by the trading bot.

#### `trade <ID1, ID2, ...>`

Show a candlestick graph that indicates the buy instant, the sell limit and stop loss prices and surrounding candlesticks that include the sell instant if it has sold.

#### `open positions`

Show which positions are currently open. It shows the trade ID for each open position.

#### `today summary / new summary`

Summary of all the trades that have been made during the day.

- `nWin`: number of positive trades
- `nLoss`: number of negative trades
- `money win`: how many USDT have been earnt
- `money loss`: how many USDT have been lost because of negative trades
- `average money win`: average USDT earnt per positive trade
- `average money lost`: average loss per negative trade
- `money earnt`: total USDT earnt without fees (`money win` - `money lost`)
- `bnb`: total BNB spent on fees
- `profit after fees`: pretty self explainatory (`money earnt` - `bnb`\*actual BNBUSDT price)

#### `summary`

The same as the daily summary but since the first time the bot has runned (or the log has been cleared).

#### `random`

Gives a random fact in case you are sad after all the losses.

## Some results and examples

### Trading bot examples

- `White line`: when the trade has been opened
- `Red line`: stop loss price
- `Green line`: target price

Note that for long trades, the green line is above the red line. For short trades, the red line is the one above.

<div style='display: flex; gap: 20px;'>
<img width="402" height="291" src='examples/chart3.png'>
<img width="402" height="291" src='examples/chart4.png'>
<img width="402" height="291" src='examples/chart1.png'>
<img width="402" height="291" src='examples/chart6.png'>
<img width="402" height="291" src='examples/chart7.png'>
<img width="402" height="291" src='examples/chart5.png'>
<img width="402" height="291" src='examples/chart8.png'>
<img width="402" height="291" src='examples/chart2.png'>
<img width="402" height="291" src='examples/chart9.png'>
<img width="402" height="291" src='examples/chart10.png'>
</div>

It can be seen how not all the trades are positive. More trade examples can be found in examples directory (around 1000 past trades). If anyone is interested in contributing, it can study the examples in order to see when the strategy fails and make improvements.

### Telegram bot examples

In the examples, a initial 1000 USDT is used, with a maximum 20 active pairs, that is 50 USDT per trade. The trades with a green light indicates buy actions, the ones with red lights sell actions. They are not related with a positive or negative trade. If a sell action has a total USDT higher than 50, it indicates a positive trade in this case. Some screenshots use a x5 leverage and some others x1, as indicated in the trading messages.

<div style='display: flex; gap: 20px;'>
<img width="282" height="500" src='examples/sc1.jpg'>
<img width="282" height="500" src='examples/sc3.jpg'>
<img width="282" height="500" src='examples/sc2.jpg'>
<img width="282" height="500" src='examples/sc5.jpg'>
<img width="282" height="500" src='examples/sc4.jpg'>
</div>

## Set up

### Install Python dependencies

Run the following line in the terminal: `pip install -r requirements.txt`.

You may create a `virtualenv` to execute this project, to know more about how to install and create virtualenvs visit [virtualenv](https://docs.python.org/3/library/venv.html).

### Create Telegram bot token

Skip this step if you only intend to use the bot without Telegram communication.

- Create a Telegram Account
- Start a new conversation with the [botfather](https://telegram.me/botfather)
- Send `/newbot` to create a new Telegram bot
- When asked, enter a name for the bot
- Give the Telegram bot a unique username. Note that the bot name must end with the word "bot" (case-insensitive)
- Save the Telegram bot's access token
- Put the access token in a new file called _token.txt_ in the same directory

Configure user ID

- Run _telegram_bot.py_ in the console
- Start a new conversation with the bot
- It will message us that the access is denegated, but will give us what our user ID is
- Go at the top of _telegram_bot.py_ file and change `USER = None` by the user that the bot has sent us. This way is secure that the bot can only interact with you.

### How to run the bot

- Run _telegram_bot.py_ in one console
- Run _crypto_bot_EMA.py_ in other console
- That's it! Now you can see the trades in the console or interact with the Telegram bot

## Authors

This project is created and maintained by David Pujalte.

## Disclaimer

This project is for informational and educational purposes only. The user must not use the project or anything related to it as investment, financial or other advice.

There is not any warranty that the information and materials contained in this project are accurate.

**USE AT YOUR OWN RISK!**

Under any circumstances will the author of the project be held responsible or liable in any way for claims, damages, losses, expenses, costs, or liabilities watsoever, including, without limitation, any direct or indirect damages for loss of profits.
