# API Documentation

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
| callbackUrl | string (128) | false | Callback URL | "https://xxxxxxxx/" |
| currency | string (32) | false | Currency (default: USDT) | USDT |
| network | string (64) | false | Network (default: NAL) | NAL |

### Request Example

```jsx
{
    "apiId": "1234567890123456",
    "timestamp": 1723046412345,
    "sign": "SbMQW2w+7pcjM/A4Invl9u1QMr9GjpIPRfLau82kuQ/2k5CcXTPjaTOq5HQgozxam1MkRwsD8rCmCC7LvPu+Ry8hjYxqrV91wsHXSGI25qNcaHCPLv6s/GPPjqM9sIJUBPbmVVMOfO08ifC0sOniXxplUzeAZbpOvsgjQnEkqIo=",
    "description": "VPN fee",
    "amount": "99.99",
    "closeAt": 1723046412345,
    "requestId": "123456",
    "callbackUrl": "https://xxxxxx",
    "currency": "USDT",
    "network": "NAL",
    "toAddress": "0xA33781f85f20CEE1bAf63aCA36e72Afc165bB5C1"
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
| orderLink | string (128) | Cashier link | "https://xxxxxxxxxx/" |
| toAddress | string (42) | Recipient account address | "0xA33781f85f20CEE1bAf63aCA36e72Afc165bB5C1" |
| orderAmount | string (26) | Amount to pay | "99.99" |
| paidAmount | string (26) | Paid amount | "99.99" |
| createAt | long | Creation time | 1723046412345 |
| closeAt | long | Expiration time | 1723046412345 |
| callbackUrl | string (128) | Callback URL | "https://xxxxxxxx/" |
| currency | string (32) | Currency (default: USDT) | USDT |
| network | string (64) | Network (default: NAL) | NAL |

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
    "currency": "USDT",
    "network": "NAL",
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
| orderLink | string (128) | Cashier link | "https://xxxxxxxxxx/" |
| toAddress | string (42) | Recipient account address | "00xA33781f85f20CEE1bAf63aCA36e72Afc165bB5C1" |
| fromAddress | string (42) | Send address | "0xcdF9b03791e8bA913Ee81bA626f06xxx9e2C35ff" |
| orderAmount | string (26) | Amount to pay | "99.99" |
| paidAmount | string (26) | Paid amount | "99.99" |
| createAt | long | Creation time | 1723046412345 |
| closeAt | long | Expiration time | 1723046412345 |
| callbackUrl | string (128) | Callback URL | "https://xxxxxxxx/" |
| currency | string (32) | Currency (default: USDT) | USDT |
| network | string (64) | Network (default: NAL) | NAL |

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
    "orderLink": "<https://xxxxxxxx>",
    "orderAmount": "99.99",
    "paidAmount": "99.99",
    "currency": "USDT",
    "network": "NAL",
    "toAddress": "0xA33781f85f20CEE1bAf63aCA36e72Afc165bB5C1",
    "fromAddress": "0xcdF9b03791e8bA913Ee81bA626f06xxx9e2C35ff",
    "callBackUrl": "<https://xxxxxxxx>",
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
| USDT |

## Order Status List

| Status | Description |
| --- | --- |
| pending | Wait for payment |
| confirming | Confirming the payment result |
| confirmed | Payment received |
| closed | Closed |
| failed | Failed |

## Error Codes

Success code is 200. Below are some related error codes:

| Error Code | Meaning |
| --- | --- |
| 900000 | Invalid wallet address |
| 900001 | Signature failed |
| 900002 | Timestamp expired |
| 900003 | Invalid account, please configure it in the Developer Center first |
| 900004 | Duplicate request |
| 900005 | Order does not exist |