# Querying Data (Live Tracking)

To perform a query send a GET request to the `https://your-domain.local/query` endpoint, set the URL parameter `db` as the target database, and set the URL parameter `q` as your query. 

livetracking.io is based on the time series database [InfluxDB](https://github.com/influxdata/influxdb). Each user comes with their own database. The database name is the same as the user name.

If you want to learn more about the InfluxDB HTTP API, you can read the [official documentation](https://docs.influxdata.com/influxdb/).

## [GET] /query

The example below uses the HTTP API to query the same database that you encountered in [Writing Data](Writing-Data).

The user `public` with password `livetracking` always has read access to all data.

```
curl -u "public:livetracking" -G 'https://your-domain.local/query?db=test' \
  --data-urlencode 'q=SELECT * FROM samples'
```

InfluxDB returns JSON. The results of your query appear in the "results" array. If an error occurs, InfluxDB sets an "error" key with an explanation of the error. 

### Query String Parameters

#### db=database

Required! The database name is the username.

#### q=query

Required! 

**Syntax:**

```
SELECT <field_key>[,<field_key>] FROM <measurement_name> [WHERE_clause]
```

Always use the measurement name: `samples`
Note the spaces and comma.

Field keys are the same as when [writing data](Writing-Data).

A detailed description of the syntax used can be found in the [InfluxDB Help](https://docs.influxdata.com/influxdb/v1.7/query_language/data_exploration/).

Example to see data from the last 10 minutes:

```
SELECT * FROM samples WHERE time > now() - 10m
```


#### epoch=[h,m,s,ms,u,ns]

Optional. Everything is stored and reported in UTC. By default, timestamps are returned in [RFC3339](https://tools.ietf.org/html/rfc3339) UTC and have **nanosecond precision**, for example `2016-08-12T20:15:14.318570484Z`. If you want timestamps in Unix epoch format include in your request the query string parameter `epoch`.

* ns = nanoseconds
* u = microsecond
* ms = milliseconds
* s = seconds (A good precision for live tracking)
* m = minutes
* h = hours

For example, get epoch in seconds with:

```
curl -u "public:livetracking" -G 'https://your-domain.local/query' \
  --data-urlencode 'db=test'
  --data-urlencode 'epoch=s'
  --data-urlencode 'q=SELECT * FROM samples'
```

