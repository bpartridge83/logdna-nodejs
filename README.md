<p align="center">
  <a href="https://app.logdna.com">
    <img height="95" width="201" src="https://raw.githubusercontent.com/logdna/artwork/master/logo%2Bnode.png">
  </a>
  <p align="center">Node.js library for logging to <a href="https://app.logdna.com">LogDNA</a></p>
</p>

[![Build Status](https://travis-ci.org/logdna/nodejs.svg?branch=master)](https://travis-ci.org/logdna/nodejs)

===

* **[Install](#install)**
* **[Setup](#setup)**
* **[Usage](#usage)**
* **[API](#api)**
* **[Winston Transport](#winston-transport)**
* **[License](#license)**


## Install

```javascript
$ npm install logdna
```

## Setup
```javascript
var Logger = require('logdna');
var options = {
    hostname: myHostname,
    ip: ipAddress,
    mac: macAddress,
    app: appName
};
var logger = Logger.create(apikey, options);
```
_**Required**_ - *(String)* - max length 32 chars
* [LogDNA API Key](https://app.logdna.com/manage/profile) 
* Hostname
* MAC Address
* IP Address

## Usage

After initial setup, logging is as easy as:
```javascript
// Simplest use case
logger.log('My Sample Log Line');

// Add a custom level
logger.log('My Sample Log Line', 'MyCustomLevel');

// Include an App name with this specific log
logger.log('My Sample Log Line', { level: 'Warn', app: 'myAppName'});
```

For more options, this module also offers:
```javascript
// We support the following six levels
logger.info('My Sample Log Line');
logger.warn('My Sample Log Line');
logger.debug('My Sample Log Line');
logger.error('My Sample Log Line');
logger.fatal('My Sample Log Line');

// Functions above also accept additional options
logger.trace('My Sample Log Line', { app: 'myAppName'});
```

## API

### create(key, [options])

#### key

_**Required**_  
Type: `String`  
Values: `YourAPIKey`   
Max Length: `32`  

The [LogDNA API Key](https://app.logdna.com/manage/profile) associated with your account.

#### options

##### hostname

_**Required**_  
Type: `String`  
Default: `''`  
Values: `YourCustomHostname`  
Max Length: `32`  

The default hostname passed along with every log sent through this instance.

##### mac

_**Required**_  
Type: `String`  
Default: `''`  
Values: `C0:FF:EE:C0:FF:EE`  

The default MAC Address passed along with every log sent through this instance.

##### ip

_**Required**_  
Type: `String`  
Default: `''`  
Values: `10.0.0.1`

The default IP Address passed along with every log sent through this instance.

##### timeout

_**Optional**_  
Type: `Integer`  
Default: `30000`  
Max Value: `100000`

The length of the timeout on the POST request that is sent to LogDNA.

##### level

_**Optional**_  
Type: `String`  
Default: `''`  
Values: `Debug`, `Trace`, `Info`, `Warn`, `Error`, `Fatal`, `YourCustomLevel`  
Max Length: `32`

The default level passed along with every log sent through this instance.

##### app

_**Optional**_  
Type: `String`  
Default: `''`  
Values: `YourCustomApp`  
Max Length: `32`

The default app passed along with every log sent through this instance.

### log(line, [options])

#### line

_**Required**_  
Type: `String`  
Default: `''`  
Max Length: `32000`

The line which will be sent to the LogDNA system.

#### options

##### level

_**Optional**_  
Type: `String`  
Default: `''`  
Values: `Debug`, `Trace`, `Info`, `Warn`, `Error`, `Fatal`, `YourCustomLevel`  
Max Length: `32`

The level passed along with this log line.

##### app

_**Optional**_  
Type: `String`  
Default: `''`  
Values: `YourCustomApp`  
Max Length: `32`

The app passed along with this log line.


## Winston Transport

This module also provides a transport object, which can be added to winston using:

```javascript
var winston = require('winston');
var options = {
    key: apikey,
    hostname: myHostname,
    ip: ipAddress,
    mac: macAddress,
    app: appName
};
winston.add(winston.transports.Logdna, options);
```

## License

MIT © [LogDNA](https://logdna.com/)
