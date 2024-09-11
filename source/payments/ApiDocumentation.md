# API documentation

## Create Invoice

### Overview

This API is used to create an invoice(order) and query the invoice(order) status.

### Interface URL

```jsx
POST /api/pay/order/create
```

### Request Parameters

| Parameter | Type (Length) | Required | Description | Example |
| --- | --- | --- | --- | --- |
| apiId | string (64) | true | Request identity ID | "1234567890123456" |
| timestamp | long | true | Request timestamp | 1723046412345 |
| sign | string (128) | true | Signature of the request data | "SbMQW2w+7pcjM/A4I..." |
| requestId | string (128) | true | Request number | "123456" |
| description | string (64) | true | Invoice description | Collet VPN fee |
| toAddress | string (42) | true | Recipient account address | "0xA33781f85f20CEE1bACA36e72Afc165bB5CC" |
| orderAmount | string (26) | true | Amount to pay, supports up to two digits come after the decimal place | "99.99" |
| createAt | long | true | Creation time | 1723046412345 |
| closeAt | long | true | Expiration time | 1723046412345 |
| callbackUrl | string (128) | false | Callback URL | "[https://xxxxxxxx](https://xxxxxxxx/)" |
| orderCurrency | string(32) | false | Invoice currency unit, default is USD | USD |
| supportTokens | array | true | Supported token list |  |
| &ensp;&ensp;token | string(32) | true | Currency | USDT |
| &ensp;&ensp;network | string(64) | true | Network | NAL |

### Request Example

```jsx
{
    "apiId": "1234567890123456",
    "timestamp": 1723046412345,
    "sign": "SbMQW2w+7pcjM/A4Invl9u1QMr9GjpIPRfLau82kuQ/2k5CcXTPjaTOq5HQgozxam1MkRwsD8rCmCC7LvPu+Ry8hjYxqrV91wsHXSGI25qNcaHCPLv6s/GPPjqM9sIJUBPbmVVMOfO08ifC0sOniXxplUzeAZbpOvsgjQnEkqIo=",
    "description": "VPN fee",
    "orderAmount": "99.99",
    "closeAt": 1723046412345,
    "requestId": "123456",
    "callbackUrl": "https://xxxxxx",
    "toAddress": "0xA33781f85f20CEE1bAf63aCA36e72Afc165bB5C1",
    "orderCurrency": "USD",
    "supportTokens": [
        {
          "token": "USDT",
          "network": "NAL"
        },
        {
          "token": "USDC",
          "network": "NAL"
        }
    ]
}
```

### Response Parameters

| Parameter | Type (Length) | Description | Example |
| --- | --- | --- | --- |
| timestamp | long | Request timestamp | 1723046412345 |
| sign | string (256) | Signature of the request data | "SbMQW2w+7pcjM/A4I..." |
| requestId | string (128) | Request number | "123456" |
| orderNo | string (128) | Invoice number | "123456789" |
| status | string (32) | Invoice status | "pending" |
| description | string (64) | Invoice description | VPN fee |
| orderLink | string (128) | Cashier link | "[https://xxxxxxxxxx](https://xxxxxxxxxx/)" |
| toAddress | string (42) | Recipient account address | "0xA33781f85f20CEE1bAf63aCA36e72Afc165bB5C1" |
| orderAmount | string (26) | Amount to pay | "99.99" |
| paidAmount | string (26) | Paid amount | "99.99" |
| createAt | long | Creation time | 1723046412345 |
| closeAt | long | Expiration time | 1723046412345 |
| callbackUrl | string (128) | Callback URL | "[https://xxxxxxxx](https://xxxxxxxx/)" |
| orderCurrency | string(32) | Invoice currency unit, default is USD | USD |
| supportTokens | array | Supported token list |  |
| &ensp;&ensp;token | string(32) | Currency | USDT |
| &ensp;&ensp;network | string(64) | Network | NAL |

### Response Example

```jsx
{
  "code": 200,
  "msg": "Operation successful",
  "data": {
    "requestId": "123456",
    "orderNo": "123456789",
    "status": "pending",
    "description": "VPN fee",
    "orderLink": "https://xxxxxxxx",
    "orderAmount": "99.99",
    "paidAmount": "99.99",
    "orderCurrency": "USD",
    "supportTokens": "[{\"token\":\"USDT\",\"network\":\"NAL\"}]",
    "toAddress": "0xA33781f85f20CEE1bAf63aCA36e72Afc165bB5C1",
    "callBackUrl": "https://xxxxxxxx",
    "createAt": 1723046412345,
    "closeAt": 1723046412345,
    "timestamp": 1723046412345,
    "sign": "DoMb7r4KN8mRenV8oG1Snk0waV27z+FhP9m6RS2UnhTWuOFI...."
  }
}
```

## Invoice query

### Overview

Query Invoice details by orderNo

### Interface URL

```jsx
POST /api/pay/order/getByOrderNo
```

### Request Parameters

| Parameter | Type (Length) | Required | Description | Example |
| --- | --- | --- | --- | --- |
| apiId | string (64) | true | Request identity ID | "1234567890123456" |
| timestamp | long | true | Request timestamp | 1723046412345 |
| sign | string (256) | true | Signature of the request data | "SbMQW2w+7pcjM/A4I..." |
| orderNo | string (128) | true | Invoice number | "123456789" |

### Request Example

```jsx
{
  "apiId": "1234567890123456",
  "timestamp": 1723046412345,
  "sign": "SbMQW2w+7pcjM/A4I...",
  "orderNo": "123456789"
}
```

### Response Parameters

| Parameter | Type (Length) | Description | Example |
| --- | --- | --- | --- |
| timestamp | long | Request timestamp | 1723046412345 |
| sign | string (256) | Signature of the request data | "SbMQW2w+7pcjM/A4I..." |
| requestId | string (128) | Request number | "123456" |
| orderNo | string (128) | Invoice number | "123456789" |
| status | string (32) | Invoice status | "pending" |
| description | string (64) | Invoice description | collect VPN fee |
| orderLink | string (128) | Cashier link | "[https://xxxxxxxxxx](https://xxxxxxxxxx/)" |
| toAddress | string (42) | Recipient account address | "00xA33781f85f20CEE1bAf63aCA36e72Afc165bB5C1" |
| fromAddress | string (42) | Send address | "0xcdF9b03791e8bA913Ee81bA626f06xxx9e2C35ff" |
| orderAmount | string (26) | Amount to pay | "99.99" |
| paidAmount | string (26) | Paid amount | "99.99" |
| createAt | long | Creation time | 1723046412345 |
| closeAt | long | Expiration time | 1723046412345 |
| callbackUrl | string (128) | Callback URL | "[https://xxxxxxxx](https://xxxxxxxx/)" |
| orderCurrency | string(32) | Invoice currency unit, default is USD | USD |
| supportTokens | array | Supported token list |  |
| &ensp;&ensp;token | string(32) | Currency | USDT |
| &ensp;&ensp;network | string(64) | Network | NAL |

### Response Example

```json
{
  "code": 200,
  "msg": "Operation successful",
  "data": {
    "requestId": "123456",
    "orderNo": "123456789",
    "status": "pending",
    "description": "VPN fee",
    "orderLink": "https://xxxxxxxx",
    "orderAmount": "99.99",
    "paidAmount": "99.99",
    "orderCurrency": "USDT",
    "supportTokens": "[{\"token\":\"USDT\",\"network\":\"NAL\"}]",
    "toAddress": "0xA33781f85f20CEE1bAf63aCA36e72Afc165bB5C1",
    "fromAddress": "0xcdF9b03791e8bA913Ee81bA626f06xxx9e2C35ff",
    "callBackUrl": "https://xxxxxxxx",
    "createAt": 1723046412345,
    "closeAt": 1723046412345,
    "timestamp": 1723046412345,
    "sign": "DoMb7r4KN8mRenV8oG1Snk0waV27z+FhP9m6RS2UnhTWuOFI...."
  }
}

```

## Signature Regulation

### Regulation

1. All interfaces require signature to access, and all returned results will also be signed.
2. Request parameters must be sorted in ascending order by key before signing.
3. Request parameters must include `apiId`, `timestamp`, and `sign` fields. Response results will always include `timestamp` and `sign` fields.
4. The RSA asymmetric encryption algorithm and SHA-256 hashing algorithm are used for digital signatures.

### Example

Consider the following request for querying an order:

**Request Parameters**

```json
{
  "apiId": "123456",
  "timestamp": 1723046412345,
  "orderNo": "123456789"
}

```

**Sorted Parameters**

```json
{
  "apiId": "123456",
  "orderNo": "123456789",
  "timestamp": 1723046412345
}

```

**Sorting Code Implementation**

```java
public static String getSortedData(JSONObject jsonObject) {
    List<String> keys = new ArrayList<>(jsonObject.keySet());
    StringBuilder sb = new StringBuilder();
    Collections.sort(keys);
    for (String key : keys) {
        sb.append(jsonObject.get(key));
    }
    return sb.toString();
}

```

The resulting string: `"1234561234567891723046412345"`.

**Sign the Data**

```java
public static String sign(String data, PrivateKey privateKey) throws Exception {
    byte[] keyBytes = privateKey.getEncoded();
    PKCS8EncodedKeySpec keySpec = new PKCS8EncodedKeySpec(keyBytes);
    KeyFactory keyFactory = KeyFactory.getInstance("RSA");
    PrivateKey key = keyFactory.generatePrivate(keySpec);
    Signature signature = Signature.getInstance("SHA256withRSA");
    signature.initSign(key);
    signature.update(data.getBytes());
    return new String(Base64.encodeBase64(signature.sign()));
}

```

Include the signed result in the `sign` field and send the final request:

```json
{
  "apiId": "123456",
  "timestamp": 1723046412345,
  "sign": "SbMQW2w+7pcjM/A4I...",
  "orderNo": "123456789"
}

```

**Verify Signature**

```java
public static boolean verify(String srcData, PublicKey publicKey, String sign) throws Exception {
    byte[] keyBytes = publicKey.getEncoded();
    X509EncodedKeySpec keySpec = new X509EncodedKeySpec(keyBytes);
    KeyFactory keyFactory = KeyFactory.getInstance("RSA");
    PublicKey key = keyFactory.generatePublic(keySpec);
    Signature signature = Signature.getInstance("SHA256withRSA");
    signature.initVerify(key);
    signature.update(srcData.getBytes());
    return signature.verify(Base64.decodeBase64(sign.getBytes()));
}

```

## Currency List

| Currency |
| --- |
| USDT(NAL) |
| USDC(NAL) |
| USDT(ETHEREUM) |
| USDC(ETHEREUM) |

## Order Status List

| Status | Description |
| --- | --- |
| pending | Wait for payment |
| confirming | Confirming the payment result |
| confirmed | Payment received |
| closed | Closed |
| failed | Failed |

## Error Codes

Success code is 200. Below are some business-related error codes:

| Error Code | Meaning |
| --- | --- |
| 900000 | Invalid wallet address |
| 900001 | Signature failed |
| 900002 | Timestamp expired |
| 900003 | Invalid account, please configure it in the Developer Center first |
| 900004 | Duplicate request |
| 900005 | Order does not exist |
| 900006 | Unsupported orderCurrency |
| 900007 | Token or network error |

## Asynchronous Notification API

When an Invoice(order) status changes, **Nal Pay** will notify the caller by sending a request to the `callbackUrl` provided by the caller. Below are the request parameters and the notification details.

### Notification Request Parameters

| Name | Type (Length) | Description | Example |
| --- | --- | --- | --- |
| requestId | string (128) | Request identity ID | "123456" |
| timestamp | long | Request timestamp | 1723046412345 |
| sign | string (256) | Signature of the request data | "SbMQW2w+7pcjM/A4I..." |
| orderNo | string (128) | Invoice number | "123456789" |
| status | string (32) | Invoice status | "confirmed" |
| orderAmount | string (26) | Invoice amount | "99.99" |
| paidAmount | string (26) | Payment amount received | "99.99" |
| currency | string (32) | Payment currency | "USDT" |
| network | string (64) | Blockchain network | "NAL" |
| receiveAt | long | Payment received timestamp | 1723046412345 |
| toAddress | string (42) | Receiving account address | "0xcdF9b03791e8bA913Ee81bA626f06xxx9e2C35ff" |
| fromAddress | string (42) | Sending account address | "0xcdF9b03791e8bA913Ee81bA626f06xxx9e2C35ff" |
| createAt | long | Invoice creation timestamp | 1723046412345 |
| closeAt | long | Invoice close timestamp | 1723046412345 |

### Example Notification Request

```json
{
    "requestId": "123456",
    "orderNo": "123456789",
    "status": "pending",
    "orderAmount": "99.99",
    "paidAmount": "99.99",
    "currency": "USDT",
    "network": "NAL",
    "toAddress": "0xcdF9b03791e8bA913Ee81bA626f06xxx9e2C35ff",
    "fromAddress": "0xcdF9b03791e8bA913Ee81bA626f06xxx9e2C35ff",
    "createAt": 1723046412345,
    "closeAt": 1723046412345,
    "timestamp": 1723046412345,
    "sign": "DoMb7r4KN8mRenV8oG1Snk0waV27z+FhP9m6RS2UnhTWuOFI...."
}

```

### Response

| Name | Type | Description |
| --- | --- | --- |
| code | int | Status code (200 = success) |
| msg | string | Message (if any) |

Example Response:

```json
{
  "code": 200,
  "msg": ""
}

```

### Retry Mechanism

We use RocketMQ for retry handling, with the default retry count set to 18 times. Please implement idempotency protection. The retry intervals are as follows: 

1s, 5s, 10s, 30s, 1 minute, 2 minutes, 3 minutes, 4 minutes, 5 minutes, 6 minutes, 7 minutes, 8 minutes, 9 minutes, 10 minutes, 20 minutes, 30 minutes, 1 hour, and 2 hours.