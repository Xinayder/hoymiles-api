### List all inverter error codes

This endpoint returns the list of all possible error codes for a Hoymiles micro inverter.

- URL: `/zhgf-core/api/0/alarmManage/viewAllErrCode`
- Method: **POST**
- Headers:
  - Authorization
  - language
    - Set to `en-US` otherwise it will return a list of error codes in Chinese
- Params:
  - **all**: string (valid values are: All)
- Response:
```json
{
    "status": "0",
    "message": "success",
    "data": {
        "0": "Offline",
        "100": "UNKNOW",
        "1510": "Island",
        "1511": "GFDI",
        "1831": "Remote shutdown",
        "1512": "Hardware failure - code:12",
        "1832": "Remote lock",
        "1513": "Hardware failure - code:13",
        "1514": "Hardware failure - code:14",
        "1515": "Grid Overvoltage",
        "1516": "Error Code-16",
        "1520": "Firmware broken",
        "151": "Error Code-01",
        "152": "Error Code-02",
        "120": "STANDBY",
        "153": "Error Code-03",
        "154": "Error Code-04",
        "155": "PV Input Overvoltage/Undervoltage",
        "156": "Hardware failure - code:06",
        "157": "Over temperature",
        "158": "Grid Overvoltage/Undervoltage",
        "190": "Microinverter is suspected of being stolen",
        "159": "Grid Overfrequency/Underfrequency"
    }
}
```