# TrueWallet Class

Unoffical TrueMoney Wallet API Class for PHP.

```php
// Login with Credentials. (You will need OTP for the first time.)
$tw = new TrueWallet($username, $password);
print_r($tw->RequestLoginOTP());
print_r($tw->SubmitLoginOTP($otp_code, $mobile_number, $otp_reference));
print_r($tw->access_token); // Access Token
print_r($tw->reference_token); // Reference Token

// Login with Credentials and Reference Token.
$tw = new TrueWallet($username, $password, $reference_token);
print_r($tw->Login());
print_r($tw->access_token); // Access Token

// Login with Access Token.
$tw = new TrueWallet($access_token);

```

```php
// Example Usage with Transaction History.
$transactions = $tw->getTransaction(50); // Fetch last 50 transactions. (within the last 30 days)
foreach ($transactions["data"]["activities"] as $report) {
	// Fetch transaction details.
	print_r($tw->GetTransactionReport($report["report_id"]));
}
```

*Warning: If you upgrade from version 1.x.x, please recheck on these functions as new endpoints may break your code!*

GetProfile(), GetBalance(), DraftTransferP2P(), ConfirmTransferP2P()

---

## Support Me?

If you like my project, consider donating me. Thank you! <3

[ [Donate with Paypal](https://paypal.me/likecyber) or [Donate with PromptPay](https://promptpay.io/0913147533) ]

Paypal: likecyber.unlimit@gmail.com

PromptPay: 091-314-7533 (Thiranat Mahattanobon)

BTC Address: 3ASp8h7zo1exHJ2ZGNbEdu5kahY5XoNerN

ETH Address: 0x7d0068B8ba02F18e79abdFC5e33B94830A6c93fA

BCH Address: bitcoincash:qpa0dkuq3mwdy2ja0w4ujkjs29jrdy8qlugt5hjvef

## Installation

It is pretty simple to utilize this class, you just need to require it.

```php
require_once("TrueWallet.class.php");
```

## Initialization

Simple initialization with Login Credentials/Login Credentials + Reference Token/Access Token.

```php
$tw = new TrueWallet($username, $password); // Login Credentials
$tw = new TrueWallet($username, $password, $reference_token); // Login Credentials + Reference Token
$tw = new TrueWallet($access_token); // Access Token

```
## Functions

### [function setCredentials ($username, $password, $reference_token = null, $type = null)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L55-L62)

You can set Login Credentials with this function.

Email or Mobile Number can be used as Username. PIN can be used as Password as well.

### [function setAccessToken ($access_token)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L64-L66)

You can set Access Token with this function.

### [function setReferenceToken ($reference_token)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L68-L70)

You can set Reference Token with this function.

### [function RequestLoginOTP ()](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L108-L121)

You can request for Login OTP with this function. Login Credentials are required.

This function will automatically fill $mobile_number and $otp_reference parameters for SubmitLoginOTP() function.

### [function SubmitLoginOTP ($otp_code, $mobile_number = null, $otp_reference = null)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L123-L144)

You can submit Login OTP with this function. $mobile_number and $otp_reference parameters are required.

### [function Login ()](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L146-L162)

You can login without OTP with this function. Login Credentials and Reference Token are required.

### [function Logout ()](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L164-L167)

You can logout with this function. this function will destroy Access Token session.

### [function GetProfile ()](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L169-L174)

You can get your Profile information with this function.

### [function GetBalance ()](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L176-L181)

You can get your current wallet balance with this function.

### [function GetTransaction ($limit = 50, $start_date = null, $end_date = null)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L183-L195)

You can fetch your transaction(s) with this function. $start_date and $end_date parameters are needed to be "Y-m-d" format.

### [function GetTransactionReport ($report_id)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L197-L202)

You can fetch your transaction report with this function. $report_id parameter is required.

### [function TopupCashcard ($cashcard)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L204-L207)

You can topup your wallet balance with this function. $cashcard parameter is required.

### [function DraftTransferP2P ($mobile_number, $amount)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L209-L220)

You can draft P2P transfer transaction with this function.

This function will automatically fill $draft_transaction_id and $reference_key parameters for ConfirmTransferP2P() function.

### [function ConfirmTransferP2P ($personal_message = "", $wait_processing = true, $draft_transaction_id = null, $reference_key = null)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L222-L266)

You can process P2P transfer with this function. $draft_transaction_id and $reference_key parameters are required.

$draft_transaction_id and $reference_key can be set to NULL if you did perform DraftTransferP2P() function before.

If you set $wait_processing to TRUE, it will check for transaction status to be completed before continue.

### [function GetDetailTransferP2P ($transaction_id = null)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L268-L276)

You can get your P2P transfer details with this function. $transaction_id is required.

$transaction_id can be set to NULL if you did perform GetDetailTransferP2P() function before.

### [function DraftBuyCashcard ($amount, $mobile_number)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L278-L287)

You can draft Buy Cashcard with this function. $amount and $mobile_number are required.

Cashcard E-Pin will be sent as SMS to input $mobile_number.

This function will automatically fill $draft_transaction_id, $mobile_number and $otp_reference parameters for ConfirmBuyCashcard() function.

### [function ConfirmBuyCashcard ($otp_code, $wait_processing = true, $draft_transaction_id = null, $mobile_number = null, $otp_reference = null)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L289-L324)

You can process Buy Cashcard with this function. $draft_transaction_id, $mobile_number and $otp_reference parameters are required.

$draft_transaction_id, $mobile_number and $otp_reference can be set to NULL if you did perform DraftBuyCashcard() function before.

If you set $wait_processing to TRUE, it will check for transaction status to be completed before continue.

### [function GetDetailBuyCashcard ($transaction_id = null)](https://github.com/likecyber/php-truewallet-class/blob/master/TrueWallet.class.php#L326-L332)

You can get your Buy Cashcard details with this function. $transaction_id is required.

$transaction_id can be set to NULL if you did perform ConfirmBuyCashcard() function before.

---

## Useful Variables
These variables can be used if you need them.

- (string) $this->response : Plain body Response from Curl execution.
- (int) $this->http_code : HTTP Code from Curl execution.

- (string) $this->access_token : You can take Access Token from this variable.
- (string) $this->reference_token : You can take Reference Token from this variable.

- (array) $this->curl_options : Allow you to set extra Curl Options. (You can modify this variable.)
- (int) $this->device_id : Allow you to change device_id parameter. (You can modify this variable.)
- (int) $this->mobile_tracking : Allow you to change mobile_tracking parameter. (You can modify this variable.)

---

### Note
- CURLOPT_TIMEOUT can be set with $this->curl_options.
- CURLOPT_SSL_VERIFYPEER can be turn off with $this->curl_options.
- It is best to combine $this->http_code to check for the status of API.
- $this->request()  will automatically json_decode if possible.
- GetTransaction() function will fetch last 50 transactions within the last 30 days by default.
- If you set $wait_processing to TRUE, it will check for transaction status to be completed 10 times with 1 second delay.

---

## Licenses

TrueWallet Class is 100% free and open-source.

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.

Copyright 2018-2019 Likecyber

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---

Special thanks to @Noxturnix for original gen-wallet-signature.py script.

https://gist.github.com/Noxturnix/2333671ffe093386b477c2edca323cbf
