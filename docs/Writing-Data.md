# Writing Data (Live Tracking)

The HTTP API is the primary means of writing data, by sending POST requests to `https://your-domain.local/write`.

livetracking.io is based on the time series database [InfluxDB](https://github.com/influxdata/influxdb). Each user comes with their own database. Only the user can write to his own database. The database name is the same as the user name.

If you want to learn more about the InfluxDB HTTP API, you can read the [official documentation](https://docs.influxdata.com/influxdb/).

## [POST] /write

When writing points, you must specify an existing database in the `db` query parameter. The database name is the username.

The example below writes a single point to the `test` database. The data consist of the measurement `samples`, the field key value with a field `hr_bpm` of `145`, and the timestamp in nanoseconds `1434055562000000000`. 

```
curl -u "test:test1234" "https://your-domain.local/write?db=test" \
  --data-binary 'samples hr_bpm=145 1434055562000000000'
```

The body of the POST - InfluxDB call this the Line Protocol - contains the time-series data that you wish to store. InfluxDB requires a measurement name. Always use the name: `samples`

Field keys are required and are always strings, and, by default, field values are floats.

The timestamp - supplied at the end of the line in Unix time in **nanoseconds** since January 1, 1970 UTC - is optional. If you do not specify a timestamp the server’s local nanosecond timestamp in Unix epoch is used. Anything that has to do with time is always UTC. They can adjust the precision by parameter.

### Query String Parameters

#### db=database

Required! The database name is the username.

#### precision=[ns,u,ms,s,m,h]

Optional. Sets the precision for the supplied Unix time values. The HTTP API assumes that timestamps are in nanoseconds if you do not specify precision.

* ns = nanoseconds
* u = microsecond
* ms = milliseconds
* s = seconds _(A good precision for live tracking)_
* m = minutes
* h = hours

**Examples:**

Write a point to the database test with a timestamp in nanoseconds (default):

```
curl -u "test:test1234" 'https://your-domain.local/write?db=test' \
  --data-binary 'samples hr_bpm=145 1465934559000000000' 
```

Write a point to the database test with a timestamp in seconds:

```
curl -u "test:test1234" 'https://your-domain.local/write?db=test&precision=s' \
  --data-binary 'samples hr_bpm=145 1463683075' 
```

### Syntax

```
<measurement> <field_key>=<field_value>[,<field_key>=<field_value>] [<timestamp>]
```

Always use the measurement name: `samples`
Note the spaces and comma.

The fields are explained in the following.

### Field Keys

If you missed something, please contact me.

#### dur_s

Duration in seconds.

#### dist_km

Distance in kilometers.

#### lat

Latitude in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees) (DD).

#### lng

Longitude in decimal degrees (DD).

#### acc_m

GPS accuracy in meters.

#### bearing

Bearing in degrees.

#### battery

Charging state of the battery. Indication in percent.

#### gsm_signal

GSM radio signal in percent.

#### temp_c

Temperature in degrees Celsius.

#### spd_kph

Speed in kilometers per hour.

#### alt_m

Altitude / Elevation in meters.

#### hr_bpm

Heart rate beats per minute.

#### cad_rpm

Cadence in revolutions per minute.

#### pwr_w

Power in watts.

#### pwr_w_l

Power of the left leg in watts.

#### pwr_w_r

Power of the right leg in watts.


### Writing multiple samples

Post multiple samples at the same time by separating each sample with a new line. 

**Examples:**

```
curl -u "test:test1234" 'https://your-domain.local/write?db=test&precision=s' \
--data-binary 'samples hr_bpm=123,pwr_w=1234 1463683075
samples hr_bpm=111,pwr_w=999 1463683076
samples hr_bpm=99,pwr_w=456 1463683080' 
```