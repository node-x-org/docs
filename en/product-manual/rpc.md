---
description: API Call Documentation (RPC Proxy Service)
---

# RPC

<p align="right"><a href="https://docs.node-x.xyz/chan-pin-shou-ce/rpc">中文</a></p>

## 💻 API Call Documentation (RPC Proxy Service)

### 🎯 Interface Overview

This API interface is used to proxy calls to a specific Remote Procedure Call (RPC) service.

> **Note:** This interface is only accessible after the service has been purchased and payment has been initiated.

### 🚀 Interface Details

| Attribute        | Value          |
| ---------------- | -------------- |
| **HTTP Method**  | `POST`         |
| **Request Path** | `/rpc/{chain}` |

#### Path Parameters

| Parameter   | Type     | Description                                                                                             | Example            |
| ----------- | -------- | ------------------------------------------------------------------------------------------------------- | ------------------ |
| **`chain`** | `String` | **Required**. The name of the purchased RPC service (e.g., `ethereum-mainnet`, `polygon-mumbai`, etc.). | `ethereum-mainnet` |

***

### 🔑 Header Parameters (Authentication)

| Header Name         | Type     | Description                                                                                                                                                                                  |
| ------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`X-PAYER-TOKEN`** | `String` | **Required**. The **`token` value** returned after successfully purchasing the RPC service. This token is mandatory for authentication and billing. **Please ensure it is stored securely.** |

***

### 📄 Request Body (`rawBody`)

| Parameter     | Type     | Description                                                                                                                                                      |
| ------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`rawBody`** | `String` | **Required**. The raw request body used to invoke a specific RPC method. The content must dynamically follow the underlying RPC specifications (e.g., JSON-RPC). |

#### `rawBody` Example (for Ethereum JSON-RPC)

To retrieve the latest block number (`eth_blockNumber`), the `rawBody` content is:

```json
{
    "jsonrpc": "2.0",
    "method": "eth_blockNumber",
    "params": [],
    "id": 1
}
```

❌ 錯誤處理

| **HTTP Status Code**   | **Error Reason**       | **Description**                                                                         |
| ---------------------- | ---------------------- | --------------------------------------------------------------------------------------- |
| `402 PAYMENT_REQUIRED` | Authentication Failed  | Payment required for access.                                                            |
| `404 Not Found`        | Resource Not Found     | The `chain` name in the request path is invalid.                                        |
| `400 Bad Request`      | Invalid Request Format | `rawBody` is malformed, or the underlying RPC service failed to validate parameters.    |
| `5xx` Series           | Server Error           | May indicate an internal service error or failure to connect to the target RPC service. |
