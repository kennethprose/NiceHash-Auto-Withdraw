| :warning: WARNING          |
|:---------------------------|
| I was already moving away from NiceHash and Ethereum's switch to proof of stake was the final nail in the coffin. I will no longer be using or maintaining this project. Feel free to fork this repo if you are somehow still profitable with mining.|

# NiceHash-Auto-Withdraw

It is highly recommended that you do not keep any significant amount of cryptocurrency on an exchange. Crypto exchanges have a long history of getting hacked with the victim being you, the user. However, repeatedly logging into NiceHash to transfer your crypto to a safer location can be quite annoying, especially as your mining operations grow. This script utilizes the NiceHash API to monitor your balance and transfer your crypto to a specified wallet after you hit a specified threshold.

## Installation

---

Acquire the necessary files by downloading the [latest release](https://github.com/kennethprose/NiceHash-Auto-Withdraw/releases). Save and extract the files to a directory of your choosing.

## Configuration

---

1. Open the NiceHash [API key](https://www.nicehash.com/my/settings/keys) settings. Take note of your organization id located at the top of the page. (Ex. 01234567-0123-0123-0123-012345678900)

2. Create an API key. You can make the App Name whatever you want. I recommend changing the API permissions to only allow "View balances, wallet activities and deposit addresses" and "Withdraw funds" as this is all that is required for the script to function. Take note of the "API Key Code" (public key) and the "API Secret Key Code" (private key). Make sure you complete the process of activating the new API key.

3. If you already have a withdrawal address configured, you can skip this step. Open the [withdrawal address](https://www.nicehash.com/my/settings/withdraw-addresses) settings and create a new withdrawal address. Make sure to set the currency to BTC. Enter the withdrawal address and double check it. You will not be able to recover your crypto if you send it to the wrong address.

4. Navigate to the NiceHash [API page](https://www.nicehash.com/docs/rest/get-main-api-v2-accounting-withdrawalAddresses). Make sure you are on the "/main/api/v2/accounting/withdrawalAddresses" endpoint and click "Try it out." Select BTC for the currency and then click "Get." Look through the response for your desired withdrawal address. It will be labeled "address". Scroll up and take note of the associated "id." This is your withdrawal address id.

    NOTE: Your withdrawal address and your withdrawal address id are not the same. Make sure you take note of the id.

5. Finally, take all of the information you have gathered so far...

    - organization id
    - public key
    - private key
    - withdrawal address id

    ... and enter these values into the `config.json` file. Also set the minimum balance value in the config file to your desired amount (Can not be less than 0.0005).

    Save the file and you are done with configuration.

## Usage

---

To run the script, just navigate to the directory where you installed the files and run the python file:

```
python WithdrawScript.py
```

or

```
python3 WithdrawScript.py
```

## Cron

---

If you would like to run this script on your own schedule using [crontab](https://www.hostinger.com/tutorials/cron-job), you can pass '--cron' as a command line argument. Passing this argument will suppress the automatic 4 hour loop, and the script will only execute once.

You can use [Crontab Generator](https://crontab-generator.org/) to quickly generate a custom crontab command.

**Note:** Crontab runs in your home directory by default. If you saved the script to a different directory, you will have to tell cron to change directories before running the script.

Ex:

```
* */4 * * * cd /home/[USER]/AutoWithdraw && python3 WithdrawScript.py --cron >/dev/null 2>&1
```

## License

---

Distributed under the MIT License. See `LICENSE.txt` for more information.
