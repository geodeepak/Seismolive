ObsPy 0.9.0 ([changelog](https://github.com/obspy/obspy/releases/tag/0.9.0)) offers (amongst many other things) two major new features: support for the [FDSN webservices](http://www.fdsn.org/webservices/) and the [FDSN StationXML](http://www.fdsn.org/xml/station/) format. This guide is intended to ease the transition for users to the new version. This will be necessary for many people as the IRIS datacenter [shut down](http://www.iris.edu/dms/nodes/dmc/news/2013/03/new-fdsn-web-services-and-retirement-of-deprecated-services/) its old webservices so existing codes needs to be adjusted accordingly.

 - [TL;DR (short summary)](Migration-to-ObsPy-0.9.0#tldr)
 - [Detailed notes on FDSN/StationXML changes](Migration-to-ObsPy-0.9.0#detailed-changes)
   - [FDSN Webservices](Migration-to-ObsPy-0.9.0#fdsn-webservices)
   - [StationXML](Migration-to-ObsPy-0.9.0#stationxml)

# TL;DR (Summary)

The old obspy.iris client does not work anymore - so instead of this:

```python
from obspy.iris import Client
from obspy import UTCDateTime

t1 = UTCDateTime("2010-02-27T06:30:00.000")
t2 = UTCDateTime("2010-02-27T07:30:00.000")

client = Client()

st = client.getWaveform("IU", "ANMO", "00", "BHZ", t1, t2)
cat = client.getEvents(starttime=t1, endtime=t2,
                       minmag=6.7)
# This saves a RESP file to disc.  
client.saveResponse("resp.txt", "IU", "ANMO", "", "*",
                    t1, t2, format="RESP") 
st.simulate(seedresp={"filename": "resp.text", "units": "VEL"}) 
```

do this:

```python
from obspy.fdsn import Client
from obspy import UTCDateTime

t1 = UTCDateTime("2010-02-27T06:30:00.000")
t2 = UTCDateTime("2010-02-27T07:30:00.000")

client = Client("IRIS")

st = client.get_waveforms("IU", "ANMO", "00", "BHZ", t1, t2)
cat = client.get_events(starttime=t1, endtime=t2, minmagnitude=3)
# The FDSN webservices return StationXML metadata.
inv = client.get_stations(starttime=t1, endtime=t2, network="IU",
                          station="ANMO", location="00", channel="BHZ",
                          level="response")

# Instrument correction directly from StationXML without the need for temporary
# files.
st.attach_response(inv)
st.remove_response(output="VEL", water_level=..., pre_filt=..., ...)

# If you only care about instrument correction this can also be simplified.
st = client.get_waveforms("IU", "ANMO", "00", "BHZ", t1, t2, attach_response=True)
st.remove_response(output="VEL")

```

# Detailed Changes
## FDSN Webservices

Usage of the new webservices is quite similiar to the existing ObsPy clients. The client should work for all datacenters implementing the FDSN webservice standard.

Full details are specified in the  [docs](http://docs.obspy.org/packages/obspy.fdsn.html).

### Client Initialization

Upon initialization the Client must be told the datacenter endpoint.

```python
from obspy.fdsn import Client

# It defaults to the IRIS FDSN implementation.
c = Client()
# ObsPy is aware of a number of implementations and provides convenient 
# mappings.
c = Client("USGS")
# The base URL of a given endpoint can also be given.
c = Client("http://ws.resif.fr")
```

The currently available mappings are available in the docstring of the `Client` class and also in the [obspy.fdsn documentation](http://docs.obspy.org/packages/obspy.fdsn.html). **If you know of any other public FDSN implementations please let us know.**

```python
In [4]: Client?
...
    :param base_url: Base URL of FDSN web service compatible server
        (e.g. "http://service.iris.edu") or key string for recognized
        server (one of 'IRIS', 'NCEDC', 'RESIF', 'USGS')
...
```

### Service Discovery

Different datacenters may provide different services, the `Client` discovers what services are available for any given endpoint.

```python
>>> print c
FDSN Webservice Client (base url: http://service.iris.edu)
Available Services: 'dataselect' (v1.0.0), 'event' (v1.0.8), 'station' (v1.0.9),
	'available_event_contributors', 'available_event_catalogs'

Use e.g. client.help('dataselect') for the
parameter description of the individual services
or client.help() for parameter description of
all webservices.
```

The different services can also have different capabilities. Use the `client.help()` method to query for details.
```python
>>> c.help("event")
Parameter description for the 'event' service (v1.0.8) of 
	'http://service.iris.edu':
The service offers the following non-standard parameters:
    magtype (str)
        type of Magnitude used to test minimum and maximum limits (case
        insensitive)
    originid (int)
        Retrieve an event based on the unique origin ID numbers assigned by
        the IRIS DMC
WARNING: The service does not offer the following standard parameters: 
	magnitudetype
Available catalogs: ANF, UofW, NEIC PDE, ISC, TEST, GCMT
Available contributors: NEIC PDE-W, ANF, University of Washington, 
	GCMT-Q, NEIC PDE-Q, UNKNOWN, NEIC ALERT, ISC, NEIC PDE-M, GCMT
```

### Data Download

Once a client has been initialized, data downloading works as always. The `get_waveforms()`, `get_stations()`, and `get_events()` methods are described in detail in the [module's documentation](http://docs.obspy.org/packages/obspy.fdsn.html).

## StationXML

The [obspy.station](http://docs.obspy.org/packages/obspy.station.html)  module takes care of dealing with StationXML. The new `read_inventory()` top-level function reads StationXML files to `Inventory` objects:

```python
from obspy import read_inventory

inv = read_inventory("TA.Z52A.xml")

# The format detection uses the StationXML XSD schema. As very many files 
# out in the wild currently do not yet adhere to the standard ObsPy is not 
# able to correctly deduce the format. Thus forcing the format is a good idea.
inv = read_inventory("TA.Z52A.xml", format="stationxml")
```

You can print it to get an idea of what it contains.
```
>>> print inv
Inventory created at 2013-12-02T05:55:15.000000Z
    Created by: IRIS WEB SERVICE: fdsnws-station | version: 1.0.7
        http://service.iris.edu/fdsnws/station/1/query?...
    Sending institution: IRIS-DMC (IRIS-DMC)
    Contains:
        Networks (1):
            TA
        Stations (1):
            TA.Z52A (Williamson, GA, USA)
        Channels (3):
            TA.Z52A..BHE, TA.Z52A..BHN, TA.Z52A..BHZ
```

The [inventory class](http://docs.obspy.org/master/packages/autogen/obspy.station.inventory.Inventory.html#obspy.station.inventory.Inventory) It is a hierarchical structure, starting with a list of [networks](http://docs.obspy.org/master/packages/autogen/obspy.station.network.Network.html#obspy.station.network.Network), each containing a list of [stations](http://docs.obspy.org/master/packages/autogen/obspy.station.station.Station.html#obspy.station.station.Station) which again each contains a list of [channels](http://docs.obspy.org/master/packages/autogen/obspy.station.channel.Channel.html#obspy.station.channel.Channel). The [responses](http://docs.obspy.org/master/packages/autogen/obspy.station.response.html#module-obspy.station.response) are attached to the channels.

```python
>>> net = inv[0]
>>> net
<obspy.station.network.Network at 0x10ac50e10>

>>> sta = net[0]
>>> print sta
Station Z52A (Williamson, GA, USA)
    Station Code: Z52A
    Channel Count: 40/40 (Selected/Total)
    2012-04-11T00:00:00.000000Z - 2599-12-31T23:59:59.000000Z
    Access: open
    Latitude: 33.19, Longitude: -84.42, Elevation: 252.0 m
    Available Channels:
            Z52A..BHE, Z52A..BHN, Z52A..BHZ

>>> cha = sta[0]
>>> print cha
Channel 'BHE', Location ''
    Timerange: 2012-04-11T00:00:00.000000Z - 2599-12-31T23:59:59.000000Z
    Latitude: 33.19, Longitude: -84.42, Elevation: 252.0 m, Local Depth: 0.0 m
    Azimuth: 90.00 degrees from north, clockwise
    Dip: 0.00 degrees down from horizontal
    Channel types: GEOPHYSICAL
    Sampling Rate: 40.00 Hz
    Sensor: Guralp CMG3T/Quanterra 330 Linear Phase Composite
    Response information available

>>> print cha.response
Channel Response
    From M/S (velocity in meters per second) to COUNTS (digital counts)
    Overall Sensitivity: 6.30907e+08 defined at 0.200 Hz
    3 stages:
        Stage 1: PolesZerosResponseStage from M/S to V, gain: 1504.20
        Stage 2: CoefficientsTypeResponseStage from V to COUNTS, gain: 419430.00
        Stage 3: CoefficientsTypeResponseStage from COUNTS to COUNTS, gain: 1.00
```

#### Dealing with the Instrument Response

The [get\_evalresp\_response()](http://docs.obspy.org/master/packages/autogen/obspy.station.response.Response.get_evalresp_response.html#obspy.station.response.Response.get_evalresp_response) method will call some functions within evalresp to generate the response.

```python
resp_ob = cha.response
response, freqs = resp_ob.get_evalresp_response(0.1, 16384, output="VEL")
```

Some convenience methods to perform an instrument correction on `Stream` and `Trace` objects are available and most users will want to use those. The [attach\_response()](http://docs.obspy.org/master/packages/autogen/obspy.core.stream.Stream.attach_response.html?highlight=attach_response#obspy.core.stream.Stream.attach_response) method will attach matching responses to each Trace if they are available within the inventory object. The [remove\_response()](http://docs.obspy.org/master/packages/autogen/obspy.core.trace.Trace.remove_response.html?highlight=remove_response#obspy.core.trace.Trace.remove_response) method deconvolves the instrument response in-place. As always see the docs for a full list of options and a more detailed explanation.

```python
st = read("...")
inv = read_inventory("...")
st.attach_response(inv)
st.remove_response(output="VEL", water_level=..., pre_filt=..., ...)
```