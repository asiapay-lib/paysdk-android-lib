![paydollar2](https://user-images.githubusercontent.com/57220911/68009559-4000a480-fca8-11e9-8ed1-545a4b6e4cfd.png)

#### PayDollar is a global payment gateway that accepts payments from more than 200 countries.The PaySDK ensures payment is authorised by 3DS 2.0

- [Features](#features)
- [Requirements](#requirements)
- [Integration](#integration)



## Features

- Direct Client Side Connection
- Client Post through Browser Side Connection
- Payment via Alipay


## Requirements

- minSdkVersion 19


## Integration

#### Step 1

Merchant need to integrate certificate. This certificate will be provided when merchant apply for the SDK service from [PayDollar Dashboard](https://www.paydollar.com/b2c2/eng/merchant/index.jsp).

Add `paysdk.properties` and set value of certificate.

e.g
sdk_rsa_publickey=GDJDFGHJHFGJHGJAQEF6H57F6JKNP489TFNKGH9874HNFDKLH98YHJVH78E67JNJVH98DFJJKDH099FDJKF

<!--img width="406" alt="Screenshot 2019-11-07 at 7 01 41 PM" src="https://user-images.githubusercontent.com/57219745/68393070-29b78480-0191-11ea-923a-19445f25fe52.png"-->

#### Step 2

Add `paydollarsdk-release.aar` in project lib folder and add below code in grade file

     repositories {
        flatDir {
          dirs 'libs'
      }
       }

Add below line in the dependencies to project’s gradle file

```implementation(name: 'paydollarsdk-release', ext: 'aar')```

#### Step 3

Instantiate PaySDK class with context.

<!--##### Java -->

```PaySDK paySDK = new PaySDK(getApplicationContext());```

OR

You can also pass the SDK public key at the initialize process

```PaySDK paySDK = new PaySDK(getApplicationContext(),sdkPublicKey)```

<!--##### Kotlin

You can also implement same in Kotlin.

```var paySDK: PaySDK = PaySDK(applicationContext)```
-->

### Payment method 

Creating PayData for payment and process.


#### WebView Payment
```
                PayData payData = new PayData();
                payData.setChannel(EnvBase.PayChannel.WEBVIEW);
                payData.setEnvType(EnvBase.EnvType.SANDBOX);
                payData.setAmount("10");
                payData.setPayGate(EnvBase.PayGate.PAYDOLLAR);
                payData.setCurrCode(EnvBase.Currency.HKD);
                payData.setPayType(EnvBase.PayType.NORMAL_PAYMENT);
                payData.setOrderRef("abcde12345");
                payData.setPayMethod("VISA");
                payData.setLang(EnvBase.Language.ENGLISH);
                payData.setMerchantId("1");
                payData.setRemark(" ");
                paySDK.setRequestData(payData);
                paySDK.process();

```

#### Direct Payment
```
                PayData payData = new PayData();
                payData.setChannel(EnvBase.PayChannel.DIRECT);
                payData.setEnvType(EnvBase.EnvType.SANDBOX);
                payData.setAmount("10");
                payData.setPayGate(EnvBase.PayGate.PAYDOLLAR);
                payData.setCurrCode(EnvBase.Currency.HKD);
                payData.setPayType(EnvBase.PayType.NORMAL_PAYMENT);
                payData.setOrderRef("abcde12345");
                payData.setPayMethod("VISA");
                payData.setLang(EnvBase.Language.ENGLISH);
                payData.setMerchantId("1");


                CardDetails cardDetails=new CardDetails();
                cardDetails.setCardNo("1234567890123456");
                cardDetails.setEpMonth("01");
                cardDetails.setEpYear("2020");
                cardDetails.setSecurityCode("123");
                cardDetails.setCardHolder("abc abc");
                payData.setCardDetails(cardDetails);
                payData.setRemark("");
                paySDK.setRequestData(payData);
                paySDK.process();

```

#### Payment via AliPay
```
                PayData payData = new PayData();
                payData.setChannel(EnvBase.PayChannel.DIRECT);
                payData.setEnvType(EnvBase.EnvType.SANDBOX);
                payData.setAmount("10");
                payData.setPayGate(EnvBase.PayGate.PAYDOLLAR);
                payData.setCurrCode(EnvBase.Currency.HKD);
                payData.setPayType(EnvBase.PayType.NORMAL_PAYMENT);
                payData.setOrderRef("abcde12345");
                payData.setPayMethod("ALIPAYHKAPP");
                //payData.setPayMethod("ALIPAYCNAPP");
                //payData.setPayMethod("ALIPAYAPP");
                payData.setLang(EnvBase.Language.ENGLISH);
                payData.setMerchantId("1");
                payData.setRemark(" ");
                paySDK.setRequestData(payData);

                paySDK.process();

```

#### Payment via WeChat
```
                PayData payData = new PayData();
                payData.setChannel(EnvBase.PayChannel.DIRECT);
                payData.setEnvType(EnvBase.EnvType.SANDBOX);
                payData.setAmount("10");
                payData.setPayGate(EnvBase.PayGate.PAYDOLLAR);
                payData.setCurrCode(EnvBase.Currency.HKD);
                payData.setPayType(EnvBase.PayType.NORMAL_PAYMENT);
                payData.setOrderRef("abcde12345");
                payData.setPayMethod("WECHATPAY");
                payData.setLang(EnvBase.Language.ENGLISH);
                payData.setMerchantId("1");
                payData.setRemark(" ");
                paySDK.setRequestData(payData);

                paySDK.process();

```

### Payment response

```
               paySDK.responseHandler(new PaymentResponse() {
                    @Override
                    public void getResponse(PayResult payResult) {

                        Toast.makeText(AuthActivity.this, payResult.getErrMsg(), Toast.LENGTH_SHORT).show();
                    }

                    @Override
                    public void onError(Data data) {

                        Toast.makeText(AuthActivity.this,data.getError(),Toast.LENGTH_SHORT).show();
                    }
                });
```
For detailed description kindly follow [PayDollar Guide](http://paydollar.com/pdf/op/enpdintguide.pdf).
                
                


