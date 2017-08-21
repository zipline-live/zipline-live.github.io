---
title: zipline-live
description: On premise live trading with zipline
---
# zipline-live with Interactive Brokers TWS
## Install
Assuming you have [Python 2.7](https://www.python.org/) and [virtualenv](https://virtualenv.pypa.io) installed,
you can install zipline-live using `pip`:
```
virtualenv ~/venv-zipline-live
source ~/venv-zipline-live/bin/activate
pip install zipline-live[ib]
```
As zipline-live uses the same executable as zipline, the two projects cannot be
simultaneously installed in the same environment. 

## Create a simple algorithm
Save the following code to `~/zipline-algos/demo.py`. This simple algorithm logs
the AAPL prices.
```py
from zipline.api import order, symbol

import logbook
log = logbook.Logger('algo')

def initialize(context):
    pass


def handle_data(context, data):
    sym = symbol("AAPL")
    log.info("handle_data: last_traded={} price={} OHLC={}/{}/{}/{} Volume={}".format(
        data.current(sym, 'last_traded'),
        data.current(sym, 'price'),
        data.current(sym, 'open'),
        data.current(sym, 'high'),
        data.current(sym, 'low'),
        data.current(sym, 'close'),
        data.current(sym, 'volume')))
```

## Ingest data
```
zipline ingest -b quantopian-quandl
```

## Starting Trader Workstation
Start Interactive Brokers Trader Workstation.

Enable API Clients in Configuration API/Settings by setting 'Enable ActiveX and Socket Clients' and 'Socket Port'.
![TWS API Configuration]({{ "/images/tws_settings.png" | prepend: site.baseurl }} "TWS API Configuration")

## Run!
Start zipline-live with `--broker` and `--broker-uri` specified.
```
zipline run -f ~/zipline-algos/demo.py --broker ib --broker-uri localhost:7496:1232 --bundle quantopian-quandl  --data-frequency minute
```
```
[2017-08-18 15:07:24.850838] INFO: IB Broker: Connecting: localhost:7496:1232
Server Version: 76
TWS Time at connection:20170818 11:07:24 EST
[2017-08-18 15:07:24.973549] ERROR: IB Broker: [504] Not connected
[2017-08-18 15:07:24.977206] INFO: IB Broker: [2104] Market data farm connection is OK:eufarm
[2017-08-18 15:07:24.977584] INFO: IB Broker: [2104] Market data farm connection is OK:usfuture
[2017-08-18 15:07:24.977852] INFO: IB Broker: [2104] Market data farm connection is OK:cashfarm
[2017-08-18 15:07:24.978034] INFO: IB Broker: [2104] Market data farm connection is OK:usfarm.us
[2017-08-18 15:07:24.978198] INFO: IB Broker: [2104] Market data farm connection is OK:usfarm
[2017-08-18 15:07:24.978356] INFO: IB Broker: [2106] HMDS data farm connection is OK:ushmds
[2017-08-18 15:07:25.178885] INFO: IB Broker: Managed accounts: ['********']
[2017-08-18 15:07:25.280132] INFO: IB Broker: Local-Broker Time Skew: 0 days 00:00:01
[2017-08-18 15:07:26.104361] WARNING: Loader: Refusing to download new benchmark data because a download succeeded at 2017-08-18 14:48:52+00:00.
[2017-08-18 15:07:26.288726] INFO: Live Trading: initialization done
[2017-08-18 15:08:00.323263] INFO: algo: handle_data: last_traded=NaT price=nan OHLC=nan/nan/nan/nan Volume=nan
[2017-08-18 15:09:00.471625] INFO: algo: handle_data: last_traded=2017-08-18 15:08:59.457000+00:00 price=158.08 OHLC=158.03/158.3/158.03/158.08 Volume=2019
[2017-08-18 15:10:00.624054] INFO: algo: handle_data: last_traded=2017-08-18 15:09:59.677000+00:00 price=158.12 OHLC=158.08/158.36/158.05/158.12 Volume=2075

```

# Extend
You can extend the demo algorithm to obtain portfolio data or to create orders.
For the list of supported features please see the [features page](/features).
