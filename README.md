sapui5-easyfunctionmodules
===============================
A Module to easily call an sap function module from javascript code

This small module allows you to call an SAP function module from javascript. 
It also supports a very simple interface to mock these function calls.


Usage is very simple:
-------------------

```
// instantiate the caller
var caller = new FunctionModuleCaller('/path/to/sicf/node/in/your/backend/');

// Call function Z_MY_FUNCTION on the backend giving it some parameters
caller.call('Z_MY_FUNCTION', {	IM_PARAM: 'value1', 
								TA_PARAM: [{PROP1:'VAL1'},
								           {PROP1:'VAL2'}
											]
},
function(oBeData){
	//this function is called with the data returned from the backend
});
```


How does it work?
-------------------
The library makes an http call to the url given. In order for this to work with an
sap system, you need to install a custom sicf handler. 

The handler will handle the http calls and call the corresponding function module on the system.

This library was designed to work with the json adapter from Cesar Martin:  

http://scn.sap.com/community/abap/connectivity/blog/2013/03/05/json-adapter-for-abap-function-modules

https://github.com/cesar-sap/abap_fm_json/blob/master/README.md  


Why?
-------------------
Some systems have a lot of function modules already developed and wrapping them in Odata services would
be a prohibitive amount of work. On the other hand, it is also common that the gateway is the backend server (and not a separate instance).
On these systems, it makes a lot of sense to call the function modules directly.


How to use ?
-------------------
Get the code either by cloning this repo or downloading the zip file.

Create an ui5 project with this code under WebContent and upload it to your backend sap server. Suppose it is called Z_EASY_FMS

In the project you want to use this library, you should first .require the file:

```
jQuery.sap.registerModulePath('easyfunctionmodules','/sap/bc/ui5_ui5/sap/Z_EASY_FMS/js/');
jQuery.sap.require('easyfunctionmodules.FunctionModuleCaller');
```

Now you can easily call the function. Check index.html for a complete example


Mocking calls
-------------------
Sometimes it is very usefull to mock a function call altogether: automated testing, complete independence between frontend/backend development.

This library also makes it very simple to mock a function call. Check index.html for an example.
