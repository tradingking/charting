# Facilities for Data Visualization

## Content

1.  Frontend for visualizing data: `app/`
2.  Streaming server to feed data from raw data source: `server/`
3.  Supporting facilities like history writer: `support/`
4.  Stub scripts and fake data to mock real data source: `stub/`

## How to Demo

### Environment

* Prepare python 3.5+
* `pip install sanic pika`

### Start services

* start influxdb `https://docs.influxdata.com/chronograf/v1.4/introduction/getting-started`
* start web server `cd app && python -m http.server`
* start streaming server and point to influxdb `python server/server.py --host 127.0.0.1 --port 8086 --db coin`

### View history data

* prepare history data `./stub/prepare_hist.sh`
* Open `http://127.0.0.1:8000?config=plot1`
* (View history data)
* Data format: exchange,code,type,freq,time,last,open,high,low,bid,offer,vol

### Feed stub live data

`stub/publish.sh`

### Configure plot

* Modify plot1.json or create new one (and refer it in query parameters)

## Design

### Data flow

```mermaid
graph LR;
    id1((Lean)) --> influxdb;
    influxdb --> server;
    server -- websocket --> frontend;

    style id1 stroke-dasharray: 5, 5
```
