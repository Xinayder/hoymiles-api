### List countries

This endpoint returns a list of countries, probably for using it in the web UI. It also provides useful information such as 2 letter country codes.

- URL: `/zhgf-core/api/0/address2/getAddress`
- Method: **POST**
- Headers:
  - Authorization
- Params:
  - **pid**: int (don't know what this is, maybe it's parent id, in doubt use 0)
- Response:
```json
{
    "status": "0",
    "message": "success",
    "data": [
        {
            "id": "int",
            "pid": "int",
            "nameCn": "string",
            "nameEn": "string",
            "postcode": "string",
            "level": "int",
            "child": null,
            "fullNameCn": null,
            "fullNameEn": null,
        }
    ]
}
```