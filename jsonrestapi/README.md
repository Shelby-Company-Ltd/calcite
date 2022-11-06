# JSON REST API Adapter

JSON REST API `model.json` files should be of the following format:

```json
{
  "version": "1.0",
  "defaultSchema": "PRICES",
  "schemas": [
    {
      "name": "PRICES",
      "type": "custom",
      "factory": "org.apache.calcite.adapter.jsonrestapi.JsonRestApiSchemaFactory",
      "operand": {
        "url": "https://api.coingecko.com/api/v3/coins/simple/price",
        "parameters": [
          "ids",
          "vs_currencies",
          "include_market_cap",
          "include_24hr_vol",
          "include_24hr_change",
          "include_last_updated_at",
          "precision"
        ],
        "requiredParameters": [
          "ids",
          "vs_currencies"
        ]
      },
      "columns": [
        "price"
      ]
    }
  ]
}
```

The `ApiData` class will use any filters against the `parameters` fields to modify the API request URL, effectively
pre-filtering the data. The `ApiData` class will then validate that all required parameters are present in the final
request URL.
