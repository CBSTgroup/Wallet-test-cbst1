---
description: >-
  This endpoint allows generation of disposable ONE-TIME use LNURLs. This is
  good for controlling how often and when users can withdraw from a wallet. Upon
  successful withdrawal, the LNURL is invalid
---

# Disposable LNURL-withdraw

{% api-method method="get" host="https://api.lnpay.co/v1/wallet" path="/:wallet\_key/lnurl/withdraw" %}
{% api-method-summary %}
GetWalletLnurlWithdraw
{% endapi-method-summary %}

{% api-method-description %}
Generate a disposable LNURL-withdraw link. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="wallet\_key" type="string" required=true %}
wal\_ for server side  
waka\_ for client side
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="passThru" type="string" required=false %}
base64 encoded json of data to use in webhooks, etc
{% endapi-method-parameter %}

{% api-method-parameter name="memo" type="string" required=false %}
memo for the invoice
{% endapi-method-parameter %}

{% api-method-parameter name="num\_satoshis" type="integer" required=false %}
Max number of satoshis this LNURL is good for.   
  
If blank max wallet balance is used
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
LNURL generated
{% endapi-method-response-example-description %}

```text
{
    "lnurl":"LNURL1DP68GURN8GHJ7MRWWPSHJTNRDUHHVVF0W4EK2U30WASKCMR9WSHHWC2LFACXUM35DDR5736ZF4HXVS6VGEV8GU6YDE49GC30D3H82UNV94C8YMMRV4EHX0M0W36R66MGD95KS4JGFADRS4ZRFEXK2SN2FFUXUSMHFA98XDZ8D3T9SDECWVHR43"
    "ott":"Y4J9"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Note: These LNURLs are ONE-TIME use. This is to prevent repeated access to the wallet.

the `ott` is a One-Time-Token that is encoded in the LNURL and saved by the wallet to verify
{% endhint %}

{% tabs %}
{% tab title="curl" %}
```bash
curl -u sak_XXXXXXX: \
"https://api.lnpay.co/v1/wallet/wal_XXXXXXX/lnurl/withdraw?num_satoshis=3"
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
LNPay.Initialize('pak_O0iUMxk8kK_qUzkT4YKFvp1ZsUtp');

let lnurlParams = {"num_satoshis":12,"memo":"SatsBack!"};
let myWallet = new LNPayWallet('wa_Opnn4kGOGBMnfCLFXtsDnjTb');
myWallet.getLnurl(lnurlParams,
    function(result) {
      console.log(result);
    }
);
```
{% endtab %}

{% tab title="Python" %}
```python
lnpay_py.initialize('pak_O0iUMxk8kK_qUzkT4YKFvp1ZsUtp')
from lnpay_py.wallet import LNPayWallet

my_wallet = LNPayWallet('wa_Opnn4kGOGBMnfCLFXtsDnjTb')
lnurl_params = {
    'num_satoshis': 1,
    'memo': 'SatsBack!'
}
lnurl_link = my_wallet.get_lnurl(lnurl_params)
print(lnurl_link)
```
{% endtab %}
{% endtabs %}

