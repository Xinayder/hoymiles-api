### Login

By looking at their website, the API endpoint for logging in requires a username, password and a UUID. The UUID is used to identify the client logging in, although at each login, the UUID changes. The password is a simple MD5 hash of the account's password, there's no salt or other crypto functions such as scrypt or bcrypt. 

On a successful login, the response returns an authentication token, used for querying realtime data from Hoymiles devices.

Request:

- URL: `/permission/system/0/admin/login`
- Method: **POST**
- Headers: N/A
- Params:
  - userName: string
  - password: string (MD5 hash)
  - uniqueId: UUID (without dashes)

Response:
- Wrong login:
```json
    {
        "status": "1", 
        "message": "wrong account or password",
        "data": ""
    }
```

- Correct login:
```json
  {
      "status": "0",
      "message": "success",
      "data": {
          "organizationType": "int as string",
          "userInfo": "string",
          "agreeGdpr": null,
          "loginType": "int as string",
          "isOZhou": "string",
          "companyName": "string",
          "organCountryName": "string",
          "isPlatformManager": "int as string",
          "userInfoFullName": "string",
          "userId": "int as string",
          "userLoginType": "int as string",
          "token": "string"
      }
  }
```

