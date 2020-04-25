### Search organizations

This endpoint returns the list of organizations associated with the user currently logged in.

- URL: `/permission/api/0/permission/organization/searchOrganizations`
- Method: **POST**
- Headers:
  - Authorization
- Params: `{}`
- Response:
```json
{
    "status": "0",
    "message": "success",
    "data": [
        {
            "id": int,
            "parentId": int,
            "parentIds": "comma-separated list of ints as string",
            "type": "int as string",
            "name": "string",
            "master": "string",
            "phone": "string"
        }
    ]
}
```