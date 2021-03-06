# Adxmi Client to Sever API For Publisher_Version 1.0
****

## DESCRIPITIONS
**Adxmi Client to Sever Api** is a product that designs for our cooperators to get all information of Adxmi offers with a programmatic way.

Here is the general principle of Adxmi Client to Sever API

1. The Api is only accessible by HTTP GET request and returns JSON.
2. The Api is supported only for the publishing partners who have Adxmi account and approved app.



In order to use this api, publishers need to go to our official website (www.adxmi.com) to create an application and get the app_id and app_secret, which are used for Adxmi Api request.

## API Request
### API Request url

>  http://ad.api.yyapi.net/v1/online

### Request Parameter


| Parameter  | Description                                                                                                                           | Type   | Mandatory |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|--------|-----------|
| app_id     | Apply from www.adxmi.com for the application                                                                                          | string | Y         |
| page_size  | Define the number of offers                                                                                                           | int    | Y         |
| os         | The operating system of the device(`ios` or `android`)                                                                                | string | Y         |
| user_id    | Identify the user who completed a task. The server callback can return this value when user completed a task                          | string | N         |
| ip         | The ip address of user                                                                                                                | string | N         |
| os_version | A string representing the os version of the device (eg: 4.2.2)                                                                        | string | N         |
| category   | define the offer category you would like to pull (eg: "SDL,WEB"), seperated by "," , default setting is return all available category | string | N         |
| imei       | IMEI on Android                                                                                                                       | string | N         |
| mac        | Mac Address                                                                                                                           | string | N         |
| device     | The brand of the device                                                                                                               | string | N         |
| androidid  | The Android ID on Android                                                                                                             | string | N         |
| advid      | The Google Advertising ID of user's device                                                                                            | string | N         |
| idfa       | The IDFA on IOS                                                                                                                       | string | N         |
| udid       | The UDID of the device                                                                                                                | string | N         |
| traffic    | The value is `incentive` or `non-incentive`                                                                                           | string | N         |
| carrier    | The carrier of the device                                                                                                             | string | N         |
| nettype    | The net type of the device(`2g`、`2.5g`、`3g`、`4g`、`wifi`)                                                                          | string | N         |
| chn        | Identify the channel which completed a task.                                                                                          | string | N         |


#### Notice
- page_size would like be less than 500 in case of request timeout.
- `ip` is optional. It means the ip address of user. Adxmi server will return corresponding ads accroding to this ip address. If publishers don't set up this value, Adxmi will resolute the ip address from your request


### Offer Category

| category | Description                                                     |
|----------|-----------------------------------------------------------------|
| SDL      | The app that is  listed publicly on store(AppStore/GooglePlay). |
| WEB      | Redirect to a website, then play web games or submit a form.    |
| APK      | Download an APK and install direct.                             |
| DDL      | Redirect to a website to download app direct.                   |

#### Example

>Android:
http://ad.api.yyapi.net/v1/online?app_id=b3a3277b8fdd54bc&page_size=20&user_id=your_user_id&ip=192.173.145.81&os_version=4.0.0&os=android&category=SDL&imei=014318001329861&mac=94d859c88359&device=TCL&androidid=26d3bb70d16d3af2&advid=2ead2362-bdf6-41d3-9b6f-6f54a5564aa1&traffic=incentive&carrier=Chinamobile&nettype=4g&chn=abc123

>iOS:
http://ad.api.yyapi.net/v1/online?app_id=b3a3277b8fdd54bc&page_size=20&user_id=your_user_id&ip=192.173.145.81&os_version=7.1.0&os=ios&category=SDL&mac=94d859c88359&idfa=CA35B56F-884F-4619-A3D9-BF0F2F38948D&udid=bd9fe66c29e3452794833c2b8082c41bbc181414&traffic=incentive&carrier=Chinamobile&nettype=wifi&chn=abc123

### Response Parameter

| Parameter        | Description                                                                                                         | Type   |
|------------------|---------------------------------------------------------------------------------------------------------------------|--------|
| id               | The id of the offer                                                                                                 | string |
| name             | The name of the offer                                                                                               | string |
| package          | The package name of the offer                                                                                       | string |
| adtxt            | The introduction of the offer                                                                                       | string |
| task             | The introduction of how to complete the offer                                                                       | string |
| payout           | The revenue($) of the offer                                                                                         | double |
| point            | The amount of virtual currency that will be earned for completing the offer(exchange rate is set on www.adxmi.com ) | int    |
| cap              | The maximum conversion allowed of the offer                                                                         | int    |
| trackinglink     | The link that is used to track conversion                                                                           | string |
| countries        | The target countries of the offer(empty means global)                                                               | array  |
| os               | The target operating system of the offer(`ios` or `android`)                                                        | string |
| traffic          | The value is `incentive` or `non-incentive`                                                                         | string |
| os_version       | The min os version of the offer                                                                                     | string |
| carrier          | The target carrier of the offer                                                                                     | string |
| device           | The target hardware brand of the offer                                                                              | string |
| nettype          | The target net type of the offer                                                                                    | string |
| preview_url      | The preview url of the offer                                                                                        | string |
| icon_url         | The link to the icon of the offer                                                                                   | string |
| creatives        | The image materials of the offer                                                                                    | array  |
| category         | The category of the offer                                                                                           | string |
| store_label      | The store (AppStore/GooglePlay) label of the offer                                                                  | array  |
| store_rating     | The store (AppStore/GooglePlay) rating of the offer                                                                 | string  |
| size             | The size of the package                                                                                             | string |
| mandatory_device | The mandatory device that offer needs to finish a conversion.`true` means mandatory                                 | array  |

#### Notice
- "cap" will be 0 if there is no limit.
- "countries" will be an empty array if the offer is global.

#### Example

```javascript
{
    "offers": [
        {
            "id": "780480625520939008",
            "name": "Slot & Party Free Casino Slots",
            "payout": 3.5,
            "point": 350,
            "cap": 0,
            "preview_url": "https://play.google.com/store/apps/details?id=com.multislot.multislot",
            "countries": [
                "GB",
                "US"
            ],
            "store_label": [
                "Game",
                "Casino"
            ],
            "store_rating": "3.9",
            "os": "android",
            "task": "Install the application and play for a few minutes",
            "traffic": "incentive",
            "os_version": "",
            "carrier": "",
            "nettype": "",
            "creatives": [
                {
                    "mime": "image/jpeg",
                    "width": "512",
                    "height": "288",
                    "url": "http://img2.ymcdn.net/creative/1512/24/832e7b83e3f22a9e-unnamed.jpg"
                },
                {
                    "url": "http://img2.ymcdn.net/creative/1512/24/fca80868554bd30c-unnamed.jpg",
                    "mime": "image/jpeg",
                    "width": "512",
                    "height": "288"
                }
            ],
            "size": "45M",
            "device": [],
            "mandatory_device": {
                "imei": false,
                "mac": false,
                "andid": false,
                "advid": false,
                "idfa": false,
                "udid": false
            },
            "icon_url": "http://img2.ymcdn.net/creative/1512/24/1b91231add2d8d7d-unnamed.jpg",
            "adtxt": "Slot &amp; Party – is the BEST CHOICE and #1 multi-player slot machine game! It&#39;s EASY to play together with your friends and win in EACH AND EVERY SPIN, not only from the casino, but also from friends and other players who play with you in the same slot table.  Download now, GET FREE COINS &amp; YOUR SPECIAL BONUS! Start playing to have fun and excitement with your friends, anytime, anywhere! •\tPlay with your friends and win Jackpots in each and every spin •\tExciting Bonuses, Mini-Games, Free spins, Gifts •\tVIP club with Special Offers &amp; Bonuses •\tUnlock amazing Slots with high quality sounds and effects •\tSend and receive gifts from your friends •\tAccessible anytime, anywhere   •\t100% FREE to download and play! Terms of the service:  http://multi-slots-server.com/flash/Doc/Terms%20of%20Service.htm  This product is for entertainment purposes only. The results are based on luck and the choices of the players, and Slot &amp; Party does not interfere in any way. This application service is not endorsed ",
            "package": "com.multislot.multislot",
            "category": "SDL",
            "trackinglink": "http://ad.api.yyapi.net/aos/v1/eff?s=1,3,b3a3277b8fdd54bc,E9MQ4zTTAq,1,ye8V4YI.TtcdaOrELc0aqh7DqRIAiNTzYWXl8c8uThOfcQNzC.qUSGBQgI0TTi8R3Db3yXLhF.apsYNHLLRtarihBJwOx93gZoYWr94-PTeynGwRgbNWF-3aRA242z5k9B5wuK8R9x9Z0P4b9k.ivml3BX0WHxpqpG30rfv9eawRK7X6I0KPXgwp6I4BoBdmWfts0HYvK2JchdF.,BS7n2zLVZyfIL8E9zl5bPSnIipxaClfqTtZNJimzb0DHxQ6R35ZF-7nUU7C3PWW2tI4xyQ__"
        }
    ]
}
```

## Common Error Response

| Key         | Description                                                                                                                                               |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| {"c":-3003} | missing required parameters                                                                                                                               |
| {"c":-1002} | app_id not exists                                                                                                                                         |
| {"c":-1202} | app didn't pass the verification                                                                                                                          |
| {"c":-1004} | app not match device_type                                                                                                                                 |
| {"c":-1300} | app_secret not match app_id                                                                                                                               |
| {"c":-1403} | Application didn't pass the verification or publisher didn't turn on the "Live" button for the application in "ADs Settings" - "Ad Units" of ADXMI Panel. |
| {"c":-2103} | offer not exists                                                                                                                                          |
| {"c":-2221} | offer not running                                                                                                                                         |
| {"c":-3212} | country mismatch                                                                                                                                          |
