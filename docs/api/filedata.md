### Get realtime and historical data

This endpoint returns historical data about the solar station. For realtime data, you must choose both start and end dates for the day you want to query. E.g.: assuming May 4th 2020 is today, you can query realtime data by setting `startTime` to `2020-05-04 00:00:00` and `endTime` to `2020-05-04 23:59:59`.

The intervals the Hoymiles devices use for reporting data alternates between 15 and 60 minutes. There are up to 64 entries in the response JSON for the day you want to query. Each entry in the top-most `data` field represents a day.

- URL: ``
- Method: **POST**
- Headers:
  - Authorization
- Params:
  - **cycle**: string (valid values are: day, week, month, year, total)
  - **endTime**: string (formatted as YYYY-MM-DD HH:mm:ss)
  - **interval**: int (don't know, in doubt use 0)
  - **startTime**: string (formatted as YYYY-MM-DD HH:mm:ss)
  - **stationId**: string (station ID int as string)
- Response:
```json
{
    "status": "0",
    "message": "success",
    "data": [
        {
            "date": "YYYY-MM-DD",
            "data": [
                [
                    "float",
                    "bool",
                    "int",
                    "timestamp",
                    "YYYY-MM-DD HH:mm",
                    "int",
                    "bool",
                    "int"
                ]
            ],
            "isFile": "int as string"
        }
    ]
}
```

As you can see, there's a data field for each day entry in the response. It's an array inside an array, and, as written above, a day can have up to 64 data entries. Using pseudo-code, each entry for the array can be represented as:

- `entry`:
  - **power**: float
  - unknown: bool
  - **station id**: int
  - **entry date**: int, unix timestamp
  - **entry date**: string, formatted as YYYY-MM-DD HH:mm
  - **report interval**: int
  - unknown: bool (probably related to sunlight)
  - **energy generated (accumulated)**: int

If the date you're querying refers to historical data (i.e. past dates), the `data` field will return a link to a JSON file containing the historical data for the day specified.

The link to the JSON file has the following format: `https://station-data.hoymiles.com/{stationId}/{year}/{month}/{day}/{stationId}.json`. The file contains an array of arrays, just like as querying for realtime data, and it follows the same format as specified above.