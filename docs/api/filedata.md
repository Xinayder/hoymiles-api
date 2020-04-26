### Get realtime and historical data

This endpoint returns historical data about the solar station. For realtime data, you must choose both start and end dates for the day you want to query. E.g.: assuming May 4th 2020 is today, you can query realtime data by setting `startTime` to `2020-05-04 00:00:00` and `endTime` to `2020-05-04 23:59:59`.

The intervals the Hoymiles devices use for reporting data alternates between 15 and 60 minutes. There are up to 64 entries in the response JSON for the day you want to query. Each entry in the top-most `data` field represents a day.

- URL: `/zhgf-core/api/0/liveStationMiPortApi/fileData`
- Method: **POST**
- Headers:
  - Authorization
- Params:
  - _cycle_: string (valid values are: day, week, month, year, total)
  - **endTime**: string (formatted as YYYY-MM-DD HH:mm:ss)
  - _interval_: int (don't know, in doubt use 0)
  - **startTime**: string (formatted as YYYY-MM-DD HH:mm:ss)
  - **stationId**: string (station ID int as string)
  - _type_: int (default: 2; valid values: 2, 5)
    - If the type parameter is `5`, the response JSON is [different](#detailed-response).
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

> - **data**:
>  - **0**: power (float)
>  - **1**: ? (bool)
>  - **2**: station id (int)
>  - **3**: report date (unix timestamp)
>  - **4**: report date (YYYY-MM-DD HH:mm)
>  - **5**: report interval (int)
>  - **6**: ? (bool)
>  - **7**: energy generated, accumulated (int)

If the date you're querying refers to historical data (i.e. past dates), the `data` field will return a link to a JSON file containing the historical data for the day specified.

The link to the JSON file has the following format: `https://station-data.hoymiles.com/{stationId}/{year}/{month}/{day}/{stationId}.json`. The file contains an array of arrays, just like as querying for realtime data, and it follows the same format as specified above.

### Detailed response
When the `type` parameter is present, the response JSON format changes slightly, including details such as grid frequency and voltage, solar panel voltage and current, among others. If querying for historical data, the JSON file URL follows the format above, with the exception that the `{stationId}` parameter prepending the `.json` extension is replaced by a `S` (capital S).

> - **lastOne** (last data reported):
>  - **(panel ID; starts with 1)**:
>    - **YYYY-MM-DD HH:mm**:
>      - **0**: panel voltage (float)
>      - **1**: panel current (float)
>      - **2**: grid voltage (float)
>      - **3**: grid frequency (float)
>      - **4**: panel temperature (float)
>      - **5**: panel power (float)
>      - **6**: generated energy, accumulated (int)
>      - **7**: report date (YYYY-MM-DD HH:mm)
>      - **8**: MI port (int)
>      - **9**: connected (int)
>      - **10**: ? (int)
>      - **11**: report date (timestamp with milliseconds)
>
> - **exportPowerData**:
>  - **(panel index)**:
>    - **0**: MI_serial_number-panel_index (string)
>    - **1**: report date (YYYY-MM-DD)
>    - **2**: generated energy, accumulated (int)
>
> - **manyData**:
>  - same as **lastOne**, but with each report as a separate entry