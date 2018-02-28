# Handshake API description


## End points
---
### REST Endpoints
- 	/Settings
-	/Network
-	/IO_configuration
-	/IO_State

## Settings
---
## Network
---
## IO_configuration
---
## IO_State
---
Endpoint controls the physical ports of the hs-8io-eth. There are 8 ports availble,
numbered from 0 to 7. 

state actions can be on individual ports or all ports at once

Quering the state of the ports return the realtime value of the port.

Ports that are configured as input will return the value that is connected to it on `get` request, ports configured
as output will return the last value written to the port on a `get` request.

a `patch` request will only affected ports that are configured as output, if a `patch` request is executed on a single
port configured as output this will be noted in the repsonse

### URL
/IO_State/
/IO_State/:portnumber/


### Methods 
`GET`, `PATCH`

## Model
---
## Examples
---
### Example 1: Get status of single port
---
Returns the status of port 4, configured as input

#### url `/IO_State/:portnumber`
#### method `GET`
#### response status `200`
#### headers `none`

#### response:

```json
{
    "direction" : "input",
    "state"     :   true
}
```

#### sample call:

```
curl -X GET \
http://ipadress/IO_State/4 \
 -H 'cache-control: no-cache' \
```

### Example 2: Get status of single port
---
Returns the status of port 6, configured as output. 

#### url 
`/IO_State/:portnumber`
#### method 
`GET`
#### response status 
`200`
#### headers 
`none`

#### response:

```json
{
    "direction" : "output",
    "state"     :   true,
}
```

#### sample call:

```
curl -X GET \
http://ipadress/IO_State/2 \
 -H 'cache-control: no-cache' \
```
### Example 3: Get status of ports
---
Returns the statu

#### url 
`/IO_State/`
#### method 
`GET`
#### response status 
`200`
#### headers 
`none`

#### response:

```json
{
    "state"     :   0x4b
}
```

#### sample call:

```
curl -X GET \
http://ipadress/IO_State/ \
 -H 'cache-control: no-cache' \
```

### Example 4: set single port
---
make the output of port 5 high, configured as output

#### url 
`/IO_State/:portnumber`
#### method 
`PATCH`
#### response status 
`200`
#### headers 
`state`

#### response:

```json
{
    "result"    :   "succes"
}
```

#### sample call:

```
curl -X PATCH \
http://ipadress/IO_State/5?state=true \
 -H 'cache-control: no-cache' \
```
### Example 5: clear single port
---
make the output of port 2 low, configured as input

#### url 
`/IO_State/:portnumber`
#### method 
`PATCH`
#### response status 
`200`
#### headers 
`state`

#### response:

```json
{
    "result"    :   "error"
    "direction" :   "input"
}
```

#### sample call:

```
curl -X PATCH \
http://ipadress/IO_State/2?state=false \
 -H 'cache-control: no-cache' \
 
 ### Example 6: update state of multiple ports
---
update multiple ports at once, ports configured as input won't 
be affected,and will also not generated in error. in this example port 7 is configured as input, and the state is true

#### url 
`/IO_State/`
#### method 
`PATCH`
#### response status 
`200`
#### headers 
`state`

#### response:

```json
{
    "result"    :   "succes"
    "state"     :   0xba
}
```

#### sample call:

```
curl -X PATCH \
http://ipadress/IO_State?state=0x3a \
 -H 'cache-control: no-cache' \
```

