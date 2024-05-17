This is a Telegram bot that tracks the transactions of added Ethereum (ETH) and Binance Coin (BNB) wallets and sends notifications whenever a new transaction occurs. The bot uses the Etherscan and BSCscan APIs to gather information about transactions, and CoinGecko to fetch the current prices of ETH and BNB.

## Commands

- `/start` shows a welcome message and instructions on how to use the bot.
- `/add` adds a new wallet to track transactions for. The wallet address must be provided in the correct format (starting with '0x' for ETH wallets and 'bnb' for BNB wallets), otherwise the bot will prompt the user to correct it. The added wallets are saved in a JSON file for persistence.
- `/remove` removes a wallet from the list of tracked wallets. The user must provide the wallet address in the correct format.
- `/list` shows the list of currently tracked wallets.

## Features

- Logging: the bot prompts every transaction and errors.
- Format check: the bot checks that the wallet address provided by the user is in the correct format before adding it to the list of tracked wallets.

## Requirements

To run the bot, you'll need to have Python 3.6 or later installed on your system, along with the following Python libraries:

- `requests` (for making HTTP requests to the APIs)
- `web3` (for interacting with the Ethereum blockchain)

You'll also need to obtain API keys for Etherscan and BSCscan, as well as a Telegram bot token. These can be obtained by following the instructions on the respective websites.

## Installation

1. Clone this repository: `git clone https://github.com/cankatx/crypto-wallet-tracker.git`
2. Install the required packages: `pip install -r requirements.txt`
3. Replace the following placeholders in the `main.py` file with your API keys and bot token:

    ```python
    ETHERSCAN_API_KEY = '<your_etherscan_api_key>'
    BSCSCAN_API_KEY = '<your_bscscan_api_key>'
    TELEGRAM_BOT_TOKEN = '<your_telegram_bot_token>'
    TELEGRAM_CHAT_ID = '<your_telegram_chat_id>'
    ```
4. Start the bot: `python main.py`

## Telegram chat ID

#### Find your ChatID with bot

To get your ChatID go into Telegram and send a chat message to your newly created bot (it will not respond). Once you have initiated a chat with your bot, then enter the following URL into your browser:

```
https://api.telegram.org/bot{BOTTOKEN_FROM_BOTFATHER}/getUpdates
```

The above URL should produce JSON output for your bot, including the ChatID. Paste your ChatID into your config.toml file.

An example of the JSON output is as follows:

```

{"ok":true,"result":[{"update_id":111111111,
"message":{"message_id":4,"from":{"id":222222222,"is_bot":false,"first_name":"TestUser","last_name":"","username":"TestUSer","language_code":"en-US"},"chat":{"id":000000000,"first_name":"TestUser","last_name":"","username":"TestUser","type":"private"},"date":1533900000,"text":"Hello"}}]}
```

In the example above, "chat":{"id":000000000 is what you are looking for, and specifically the id which in this example is 000000000.

#### Group chat ID

Assume the bot name is my_bot.

1- Add the bot to the group.
Go to the group, click on group name, click on Add members, in the searchbox search for your bot like this: @my_bot, select your bot and click add.

2- Send a dummy message to the bot.
You can use this example: /my_id @my_bot
(I tried a few messages, not all the messages work. The example above works fine. Maybe the message should start with /)

3- Go to following url: https://api.telegram.org/botXXX:YYYY/getUpdates
replace XXX:YYYY with your bot token

4- Look for "chat":{"id":-zzzzzzzzzz,
-zzzzzzzzzz is your chat id (with the negative sign).

5- Testing: You can test sending a message to the group with a curl:

```
curl -X POST "https://api.telegram.org/botXXX:YYYY/sendMessage" -d "chat_id=-zzzzzzzzzz&text=my sample text"
```

If you miss step 2, there would be no update for the group you are looking for. Also if there are multiple groups, you can look for the group name in the response ("title":"group_name").


## Reference

Group chat ID: https://stackoverflow.com/questions/32423837/telegram-bot-how-to-get-a-group-chat-id

## Disclaimer

This bot is provided for educational purposes only and should not be used as financial advice. The bot does not have access to your wallet.
