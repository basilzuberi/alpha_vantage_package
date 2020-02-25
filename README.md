# alpha_vantage_package

A new Flutter package for using alpha vantage api.

You will need your own API key from https://www.alphavantage.co/ (it's free) to use stocks other than MSFT

This was refactored and updated from the original source: https://github.com/jcmelend/flutter_alpha_vantage_api so credits to the maker.

For more information about how the JSON is layed out, visit https://www.alphavantage.co/documentation/

## Getting Started

For help getting started with Flutter, view our online [documentation](https://flutter.io/).

For help on editing package code, view the [documentation](https://flutter.io/developing-packages/).

## Usage

Add the following import statement where you need to use this package libraries:
import 'package:alpha_vantage_package/alpha_vantage_package.dart';

There are four libraries to use to call Alpha Vantage rest api:
TimeSeries.dart, SectorPerformances.dart, ForeignExchange.dart, CryptoCurrencies.dart,
and TechnicalIndicators.dart.

Example:

```Dart

import 'package:flutter_test/flutter_test.dart';

import 'package:flutter_alpha_vantage_package/alpha_vantage_package.dart';

void main() async {


  test('Intraday', () async {
    final timeSeries = new TimeSeries("YourAlphaVantageAPIKey");
    //get the hourly time series for Microsoft with to-the-minute updates. You can change this.
    JSONObject json = await timeSeries.getIntraday("MSFT");
    var data = json.getJSONMap()["Time Series (1min)"];

    //convert to map to get specific data like the amount during lcose
    var data2 = Map<String, dynamic>.from(data);
    data2.forEach((k,v) => print(v["4. close"]));

     //Use get method to search entire json for key for stock
    expect(json.get("2. Symbol"), "MSFT");

    // Use map to find stock symbol
    expect(json.getJSONMap()["Meta Data"]["2. Symbol"], "MSFT");
    print(json.getJSONMap());


  });

  test('Intraday', () async {
    final technicalIndicator = new TechnicalIndicators("YourAlphaVantageAPIKey");
    //get SMA for microsoft
    JSONObject json = await technicalIndicator.getSMA("MSFT");

    // Use get method to search entire json for key for stock
    expect(json.get("1: Symbol"), "MSFT");

    // Use map to find stock symbol
    expect(json.getJSONMap()["Meta Data"]["1: Symbol"], "MSFT");
    print(json.getJSONMap());
  });
}
```

