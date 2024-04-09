# Revoke Role From User

This operation revokes a privilege granted to the current role.

<div>
    <div style="display: inline-block; background: #026aca; font-size: 0.6em; border-radius: 10px; color: #ffffff; padding: 0.3em 1em;">
        <span>POST</span>
    </div>
    <span style="font-weight: bold;">  http://${MILVUS_URI}/v2/vectordb/users/revoke_role</span>
</div>



> Notes
> To complete this operation, you need to enable authentication on your Milvus instance. For details, refer to [Authenticate User Access](https://milvus.io/docs/authenticate.md).

## Example

```shell
export MILVUS_URI="localhost:19530"

curl --location --request POST "http://${MILVUS_URI}/v2/vectordb/users/revoke_role" \
--header "Content-Type: application/json" \
--data-raw '{
    "roleName": "admin",
    "userName": "milvusAdmin"
}'
```
Possible response is similar to the following.
```json
{
    "code": 200,
    "data": {}
}
```

## Request

### Parameters

- Header parameters

    | Parameter        | Description                                                                               |
    |------------------|-------------------------------------------------------------------------------------------|
    | `Request-Timeout`  | **integer**<br/>The timeout duration for this operation.<br/>Setting this to None indicates that this operation timeouts when any response arrives or any error occurs.|
    | `Authorization`  | **string**<br/>Then authentication token|

- No query parameters required

- No path parameters required

### Request Body

```json
{
    "userName": "string",
    "roleName": "string"
}
```

| Parameter        | Description                                                                               |
|------------------|-------------------------------------------------------------------------------------------|
| `userName` <span style="color:red">*</span> | __string__<br/>The name of the target user. The value should start with a letter and can only contain underline, letters and numbers.  |
| `roleName` <span style="color:red">*</span> | __string__<br/>The name of the target role.  |

## Response

None

### Response Bodies

- Response body if we process your request successfully

```json
{
    "code": "integer",
    "data": {}
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
| `data` | __object__<br/> |
| `message`  | __string__<br/>Indicates the possible reason for the reported error. |