# List Aliases

This operation lists all existing collection aliases in the specified database.

<div>
    <div style="display: inline-block; background: #026aca; font-size: 0.6em; border-radius: 10px; color: #ffffff; padding: 0.3em 1em;">
        <span>POST</span>
    </div>
    <span style="font-weight: bold;">  http://${MILVUS_URI}/v2/vectordb/aliases/list</span>
</div>

```shell
export MILVUS_URI="localhost:19530"

curl --location --request POST "http://${MILVUS_URI}/v2/vectordb/aliases/list" \
--header "Content-Type: application/json" \
--data-raw '{
    "dbName": "default"
}‘
```
Possible response is similar to the following
```json
{
    "code": 200,
    "data": [
        "bob"
    ]
}
```


## Request

### Parameters

- Header parameters

    | Parameter        | Description                                                                               |
    |------------------|-------------------------------------------------------------------------------------------|
    | `Request-Timeout`  | **integer**<br/>The timeout duration for this operation in seconds. Setting this to None indicates that this operation timeouts when any response arrives or any error occurs.|
    | `Authorization`  | **string**<br/>The authentication token.|

- No query parameters required

- No path parameters required

### Request Body

```json
{
    "dbName": "string"
}
```

| Parameter        | Description                                                                               |
|------------------|-------------------------------------------------------------------------------------------|
| `dbName`  | __string__<br/>The name of an existing database. The value defaults to __default__.  |

## Response

A list of collection aliases. 

### Response Bodies

- Response body if we process your request successfully

```json
{
    "code": "integer",
    "data": [
        {}
    ]
}
```

- Response body if we failed to process your request

```json
{
    "code": integer,
    "message": string
}
```

### Properties

The properties in the returned response are listed in the following table.

| Property | Description                                                                                                                                 |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------|
| `code`   | __integer__<br/>Indicates whether the request succeeds.<br/><ul><li>`200`: The request succeeds.</li><li>Others: Some error occurs.</li></ul> |
| `data` | __array__<br/> |
| `data[]`  | __string__<br/>A list of item objects.  |
| `message`  | __string__<br/>Indicates the possible reason for the reported error. |