# webinos nfc API #

**Service Type**: http://webinos.org/api/nfc

The main concept of nfc API is to provide access to the device's Near Field Communication (NFC) capabilities.


## Installation ##

To install the nfc API you will need to npm the node module inside the webinos pzp.

For end users, you can simply open a command prompt in the root of your webinos-pzp and do: 

	npm install https://github.com/webinos/webinos-api-nfc.git

For developers that want to tweak the API, you should fork this repository and clone your fork inside the node_module of your pzp.

	cd node_modules
	git clone https://github.com/<your GitHub account>/webinos-api-nfc.git
	cd webinos-api-nfc
	npm install


## Getting a reference to the service ##

To discover the service you will have to search for the "http://webinos.org/api/nfc" type. Example:

	var serviceType = "http://webinos.org/api/nfc";
	webinos.discovery.findServices( new ServiceType(serviceType), 
		{ 
			onFound: serviceFoundFn, 
			onError: handleErrorFn
		}
	);
	function serviceFoundFn(service){
		// Do something with the service
	};
	function handleErrorFn(error){
		// Notify user
		console.log(error.message);
	}

Alternatively you can use the webinos dashboard to allow the user choose the nfc API to use. Example:
 	
	webinos.dashboard.open({
         module:'explorer',
	     data:{
         	service:[
            	'http://webinos.org/api/nfc'
         	],
            select:"services"
         }
     }).onAction(function successFn(data){
		  if (data.result.length > 0){
			// User selected some services
		  }
	 });

## Methods ##

Once you have a reference to an instance of a service you can use the following methods:

###textRecord(text, lang)

This method creates an NDEF record from a string

###uriRecord(uri)

This method creates an NDEF record from a URI


###mimeRecord(mimeType, data)

This method creates an NDEF record from a MIME type and a byte array representing data of that type

###addTextTypeListener(listener, success, fail)

This is a method for registering a call back for NFC tags with NDEF text records.

###addUriTypeListener(scheme, listener, success, fail)

This is a method for registering a call back for NFC tags with NDEF URI records.

###addMimeTypeListener(mimeType, listener, success, fail)

This is a method for registering a call back for NFC tags with NDEF MIME content records with a specific MIME type, e.g. "text/vcard", which is used for an electronic equivalent of a business card.This is a method for registering a call back for NFC tags with NDEF URI records.

###shareTag(message, success, fail)

This is a method for setting a device into a sharing mode for pushing an NDEF message to another NDEF device.

###unshareTag(success, fail)

This method is used after the shareTag method, and sets the device back to the default mode in which it listens for the presence of NFC tags.


## Links ##

- [Specifications](http://dev.webinos.org/specifications/api/nfc.html)
- [Examples](https://github.com/webinos/webinos-api-nfc/wiki/Examples)

