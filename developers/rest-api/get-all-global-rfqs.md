# Get All Global RFQs

### **Get Info about all live and expired RFQs**

GET - Sample Request

<pre><code><strong>GET https://api-six-teal.vercel.app/api/rfq/getAll
</strong>
</code></pre>

Sample Response

```
{
    "status": "success",
    "rfq": [
        {
            "publicKey": "4HnrYyc39pjVPUepEWu9xo3BfueEzJrRgp1ZEXE8AENW",
            "account": {
                "accessManager": null,
                "assetMint": "C6kYXcaRUMqeBF5fhg165RWU7AnpT9z92fvKNoMqjmz6",
                "authority": "6FArwJBMTN6komFv8CKcRjthhM8wNUUzqsPemQ4dzCb4",
                "bestAskAmount": null,
                "bestBidAmount": null,
                "bestAskAddress": null,
                "bestBidAddress": null,
                "canceled": false,
                "confirmedOrder": null,
                "expiry": 1663059201,
                "lastLookApproved": null,
                "legs": "[{\"amount\":\"32\",\"contract\":{\"call\":{}},\"contractAssetAmount\":\"05f5e100\",\"contractQuoteAmount\":\"2191c0\",\"processed\":false,\"expiry\":\"63217bef\",\"id\":\"01\",\"instrument\":{\"option\":{}},\"venue\":{\"psyOptions\":{}},\"buySell\":{\"buy\":{}}},{\"amount\":\"32\",\"contract\":{\"put\":{}},\"contractAssetAmount\":\"05f5e100\",\"contractQuoteAmount\":\"2625a0\",\"processed\":false,\"expiry\":\"63217bef\",\"id\":\"02\",\"instrument\":{\"option\":{}},\"venue\":{\"psyOptions\":{}},\"buySell\":{\"buy\":{}}}]",
                "orderAmount": 1,
                "orderType": "Option",
                "quoteMint": "E6Z6zLzk8MWY3TY8E87mr88FhGowEPJTeMWzkqtL6qkF",
                "settled": false,
                "unixTimestamp": "2022-09-13T02:53:21.000Z"
            }
        },
        {
            "publicKey": "E4WyZaH2R6Qx5GNTWjWPHhe5VJbzFJxEmS67KpHpcVdj",
            "account": {
                "accessManager": null,
                "assetMint": "C6kYXcaRUMqeBF5fhg165RWU7AnpT9z92fvKNoMqjmz6",
                "authority": "BvcmzEF1S97omu7yRh6ZMn1BAydRFFDUG5DWFZrEYFRd",
                "bestAskAmount": null,
                "bestBidAmount": "895440",
                "bestAskAddress": null,
                "bestBidAddress": "CELBkB7KisTkir3TgedLn1qwGPh4w7cGcWmSaSwFv3D4",
                "canceled": false,
                "confirmedOrder": null,
                "expiry": 1662570525,
                "lastLookApproved": null,
                "legs": "[{\"amount\":\"02540be400\",\"contract\":null,\"contractAssetAmount\":null,\"contractQuoteAmount\":null,\"processed\":false,\"expiry\":null,\"id\":\"01\",\"instrument\":{\"spot\":{}},\"venue\":{\"convergence\":{}},\"buySell\":{\"buy\":{}}}]",
                "orderAmount": 10,
                "orderType": "Swap",
                "quoteMint": "E6Z6zLzk8MWY3TY8E87mr88FhGowEPJTeMWzkqtL6qkF",
                "settled": false,
                "unixTimestamp": "2022-09-07T16:08:48.000Z"
            }
        },
        {
            "publicKey": "6dvpbBootFeexJY6PdCg7UW6qVc5V3noEKA6SXySXipg",
            "account": {
                "accessManager": null,
                "assetMint": "C6kYXcaRUMqeBF5fhg165RWU7AnpT9z92fvKNoMqjmz6",
                "authority": "BvcmzEF1S97omu7yRh6ZMn1BAydRFFDUG5DWFZrEYFRd",
                "bestAskAmount": null,
                "bestBidAmount": null,
                "bestAskAddress": null,
                "bestBidAddress": null,
                "canceled": false,
                "confirmedOrder": null,
                "expiry": 1664308160,
                "lastLookApproved": null,
                "legs": "[{\"amount\":\"012a05f200\",\"contract\":null,\"contractAssetAmount\":null,\"contractQuoteAmount\":null,\"processed\":false,\"expiry\":null,\"id\":\"01\",\"instrument\":{\"spot\":{}},\"venue\":{\"convergence\":{}},\"buySell\":{\"buy\":{}}}]",
                "orderAmount": 5,
                "orderType": "Swap",
                "quoteMint": "E6Z6zLzk8MWY3TY8E87mr88FhGowEPJTeMWzkqtL6qkF",
                "settled": false,
                "unixTimestamp": "2022-09-27T18:49:24.000Z"
            }
        },
        {
            "publicKey": "u2bg5v3iyaX21eeXkKTDuKSqQf8yJHBfhW5HANPimoA",
            "account": {
                "accessManager": null,
                "assetMint": "C6kYXcaRUMqeBF5fhg165RWU7AnpT9z92fvKNoMqjmz6",
                "authority": "BvcmzEF1S97omu7yRh6ZMn1BAydRFFDUG5DWFZrEYFRd",
                "bestAskAmount": null,
                "bestBidAmount": "989680",
                "bestAskAddress": null,
                "bestBidAddress": "CELBkB7KisTkir3TgedLn1qwGPh4w7cGcWmSaSwFv3D4",
                "canceled": false,
                "confirmedOrder": null,
                "expiry": 1663105164,
                "lastLookApproved": null,
                "legs": "[{\"amount\":\"174876e800\",\"contract\":null,\"contractAssetAmount\":null,\"contractQuoteAmount\":null,\"processed\":false,\"expiry\":null,\"id\":\"01\",\"instrument\":{\"spot\":{}},\"venue\":{\"convergence\":{}},\"buySell\":{\"buy\":{}}}]",
                "orderAmount": 100,
                "orderType": "Swap",
                "quoteMint": "E6Z6zLzk8MWY3TY8E87mr88FhGowEPJTeMWzkqtL6qkF",
                "settled": false,
                "unixTimestamp": "2022-09-13T20:39:26.000Z"
            }
        },
        {
            "publicKey": "Hhy6RVcDfgrZvtfNdK7GYuYtSJrgpdQs1eynLmdGJ3Dt",
            "account": {
                "accessManager": null,
                "assetMint": "HfRvmfQ8ivX8E3QSbuRhJzabF4zragoQZUAeDG7eFyod",
                "authority": "3KqCTMP528V2hM8yfjGgAxBhsE4crXrkgmL97ryKMzpJ",
                "bestAskAmount": "1e8480",
                "bestBidAmount": "1dc130",
                "bestAskAddress": "EtjKErp7Uz6y8Ww2WDhdSc4Wxvo3zTq5kgFuMUfXgkBD",
                "bestBidAddress": "EtjKErp7Uz6y8Ww2WDhdSc4Wxvo3zTq5kgFuMUfXgkBD",
                "canceled": false,
                "confirmedOrder": {
                    "order": "HHtsJuba3CBgU9P3i3sGbDLXetWNix6nnnwvXf26t9ZN",
                    "quote": {
                        "bid": {}
                    }
                },
                "expiry": 1662640134,
                "lastLookApproved": null,
                "legs": "[{\"amount\":\"0a\",\"contract\":{\"call\":{}},\"contractAssetAmount\":\"0f4240\",\"contractQuoteAmount\":\"64\",\"processed\":true,\"expiry\":\"6319e006\",\"id\":\"00\",\"instrument\":{\"option\":{}},\"venue\":{\"psyOptions\":{}},\"buySell\":{\"sell\":{}}},{\"amount\":\"4c4b40\",\"contract\":null,\"contractAssetAmount\":null,\"contractQuoteAmount\":null,\"processed\":true,\"expiry\":null,\"id\":\"00\",\"instrument\":{\"spot\":{}},\"venue\":{\"convergence\":{}},\"buySell\":{\"sell\":{}}}]",
                "orderAmount": 1,
                "orderType": "Swap",
                "quoteMint": "7X5kun6HvG1F9Sm3izYyhg6AXZUaPpED83oicaPxdd8T",
                "settled": true,
                "unixTimestamp": "2022-09-08T12:23:54.000Z"
            }
        },
        {
            "publicKey": "8UaJpyUzWbQzXPnhmW3WeDp47UAxEFD3YUa86ehqfjsf",
            "account": {
                "accessManager": null,
                "assetMint": "4Wbs4cv4uKgQnpQGXW3sAuyjHraTGRwDV3gEvHmkhLgF",
                "authority": "3KqCTMP528V2hM8yfjGgAxBhsE4crXrkgmL97ryKMzpJ",
                "bestAskAmount": "1e8480",
                "bestBidAmount": "1dc130",
                "bestAskAddress": "2b2RrbpTBzU2BNqjvwXPAUTpzLR2pg2ssKG5GQTDZK11",
                "bestBidAddress": "2b2RrbpTBzU2BNqjvwXPAUTpzLR2pg2ssKG5GQTDZK11",
                "canceled": false,
                "confirmedOrder": {
                    "order": "HfrQKLcTbWGpZ86WEkuYLcdBd5rRwhvYYinY6fGbiFTz",
                    "quote": {
                        "bid": {}
                    }
                },
                "expiry": 1662639171,
                "lastLookApproved": null,
                "legs": "[{\"amount\":\"0a\",\"contract\":{\"call\":{}},\"contractAssetAmount\":\"0f4240\",\"contractQuoteAmount\":\"64\",\"processed\":true,\"expiry\":\"6319dc43\",\"id\":\"00\",\"instrument\":{\"option\":{}},\"venue\":{\"psyOptions\":{}},\"buySell\":{\"sell\":{}}},{\"amount\":\"4c4b40\",\"contract\":null,\"contractAssetAmount\":null,\"contractQuoteAmount\":null,\"processed\":true,\"expiry\":null,\"id\":\"00\",\"instrument\":{\"spot\":{}},\"venue\":{\"convergence\":{}},\"buySell\":{\"sell\":{}}}]",
                "orderAmount": 1,
                "orderType": "Swap",
                "quoteMint": "5cvGWSjLPfE18XkGcVebCr93FSfBfBbcgKYK4Qduv3FT",
                "settled": true,
                "unixTimestamp": "2022-09-08T12:07:51.000Z"
            }
        },
        {
            "publicKey": "3GUmkfSQomCuhUqDuThhyKiWo7tRVZ5Rp2qBKA8GyEWE",
            "account": {
                "accessManager": null,
                "assetMint": "C6kYXcaRUMqeBF5fhg165RWU7AnpT9z92fvKNoMqjmz6",
                "authority": "CELBkB7KisTkir3TgedLn1qwGPh4w7cGcWmSaSwFv3D4",
                "bestAskAmount": "0f4240",
                "bestBidAmount": null,
                "bestAskAddress": "BvcmzEF1S97omu7yRh6ZMn1BAydRFFDUG5DWFZrEYFRd",
                "bestBidAddress": null,
                "canceled": false,
                "confirmedOrder": {
                    "order": "5ZLXxkztG3CSypu6Gc1hYDN3XyG9HrNXEXnPH9jY9osN",
                    "quote": {
                        "ask": {}
                    }
                },
                "expiry": 1663039159,
                "lastLookApproved": null,
                "legs": "[{\"amount\":\"32\",\"contract\":{\"call\":{}},\"contractAssetAmount\":\"05f5e100\",\"contractQuoteAmount\":\"225510\",\"processed\":false,\"expiry\":\"632151bf\",\"id\":\"01\",\"instrument\":{\"option\":{}},\"venue\":{\"psyOptions\":{}},\"buySell\":{\"buy\":{}}},{\"amount\":\"32\",\"contract\":{\"put\":{}},\"contractAssetAmount\":\"05f5e100\",\"contractQuoteAmount\":\"225510\",\"processed\":false,\"expiry\":\"632151bf\",\"id\":\"02\",\"instrument\":{\"option\":{}},\"venue\":{\"psyOptions\":{}},\"buySell\":{\"buy\":{}}}]",
                "orderAmount": 1,
                "orderType": "Option",
                "quoteMint": "E6Z6zLzk8MWY3TY8E87mr88FhGowEPJTeMWzkqtL6qkF",
                "settled": true,
                "unixTimestamp": "2022-09-13T02:19:21.000Z"
            }
        },
        {
            "publicKey": "63mueUUpSknyD1uD71oxoJg8Fe9s67FrGqb7mfYJEtuv",
            "account": {
                "accessManager": null,
                "assetMint": "3Guj453UWqhKqLAWSVBSo5aTHgiWYTby44PxaBC8jjA9",
                "authority": "3KqCTMP528V2hM8yfjGgAxBhsE4crXrkgmL97ryKMzpJ",
                "bestAskAmount": "1e8480",
                "bestBidAmount": "1dc130",
                "bestAskAddress": "EzNHCUsDuyQQzaJ6wKyZvrBA5DPfSdPCTrsa1d72WrWD",
                "bestBidAddress": "EzNHCUsDuyQQzaJ6wKyZvrBA5DPfSdPCTrsa1d72WrWD",
                "canceled": false,
                "confirmedOrder": {
                    "order": "Eh2osnBY7PT7ZBV24ScCudRzX54MNbVQSXa8UAXrtwwx",
                    "quote": {
                        "bid": {}
                    }
                },
                "expiry": 1662577499,
                "lastLookApproved": null,
                "legs": "[{\"amount\":\"0a\",\"contract\":{\"call\":{}},\"contractAssetAmount\":\"0f4240\",\"contractQuoteAmount\":\"64\",\"processed\":true,\"expiry\":\"6318eb5b\",\"id\":\"00\",\"instrument\":{\"option\":{}},\"venue\":{\"psyOptions\":{}},\"buySell\":{\"sell\":{}}},{\"amount\":\"4c4b40\",\"contract\":null,\"contractAssetAmount\":null,\"contractQuoteAmount\":null,\"processed\":true,\"expiry\":null,\"id\":\"00\",\"instrument\":{\"spot\":{}},\"venue\":{\"convergence\":{}},\"buySell\":{\"sell\":{}}}]",
                "orderAmount": 1,
                "orderType": "Swap",
                "quoteMint": "5vfXitLPjcWXn6h5Cqhko7kr65ju3yZtdYaLzpEAXnxd",
                "settled": true,
                "unixTimestamp": "2022-09-07T18:59:58.000Z"
            }
        },
        {
            "publicKey": "DLwCMZC8D7h8bawRJc58jKdqL8btP1ELozqSg9sLnayx",
            "account": {
                "accessManager": null,
                "assetMint": "C6kYXcaRUMqeBF5fhg165RWU7AnpT9z92fvKNoMqjmz6",
                "authority": "A5K2ZeyVDhuMmrydzEQ1tv31X1ydXUFh2vqvDgmtknVN",
                "bestAskAmount": null,
                "bestBidAmount": null,
                "bestAskAddress": null,
                "bestBidAddress": null,
                "canceled": false,
                "confirmedOrder": null,
                "expiry": 1666015084,
                "lastLookApproved": null,
                "legs": "[{\"amount\":\"77359400\",\"contract\":null,\"contractAssetAmount\":null,\"contractQuoteAmount\":null,\"processed\":false,\"expiry\":null,\"id\":\"01\",\"instrument\":{\"spot\":{}},\"venue\":{\"convergence\":{}},\"buySell\":{\"buy\":{}}}]",
                "orderAmount": 2,
                "orderType": "Swap",
                "quoteMint": "E6Z6zLzk8MWY3TY8E87mr88FhGowEPJTeMWzkqtL6qkF",
                "settled": false,
                "unixTimestamp": "2022-10-17T12:58:07.000Z"
            }
        },
        {
            "publicKey": "J5qC9uFRTtjbSrFWcQEcuCAfzak8TrG5G4X2S8djjd9g",
            "account": {
                "accessManager": null,
                "assetMint": "C6kYXcaRUMqeBF5fhg165RWU7AnpT9z92fvKNoMqjmz6",
                "authority": "BvcmzEF1S97omu7yRh6ZMn1BAydRFFDUG5DWFZrEYFRd",
                "bestAskAmount": "0f4240",
                "bestBidAmount": null,
                "bestAskAddress": "CELBkB7KisTkir3TgedLn1qwGPh4w7cGcWmSaSwFv3D4",
                "bestBidAddress": null,
                "canceled": false,
                "confirmedOrder": null,
                "expiry": 1662614635,
                "lastLookApproved": null,
                "legs": "[{\"amount\":\"32\",\"contract\":{\"call\":{}},\"contractAssetAmount\":\"05f5e100\",\"contractQuoteAmount\":\"1dc130\",\"processed\":false,\"expiry\":\"631c0bbf\",\"id\":\"01\",\"instrument\":{\"option\":{}},\"venue\":{\"psyOptions\":{}},\"buySell\":{\"buy\":{}}},{\"amount\":\"32\",\"contract\":{\"put\":{}},\"contractAssetAmount\":\"05f5e100\",\"contractQuoteAmount\":\"1dc130\",\"processed\":false,\"expiry\":\"631c0bbf\",\"id\":\"02\",\"instrument\":{\"option\":{}},\"venue\":{\"psyOptions\":{}},\"buySell\":{\"buy\":{}}}]",
                "orderAmount": 1,
                "orderType": "Option",
                "quoteMint": "E6Z6zLzk8MWY3TY8E87mr88FhGowEPJTeMWzkqtL6qkF",
                "settled": false,
                "unixTimestamp": "2022-09-08T04:23:58.000Z"
            }
        }
    ]
}
```



