First Steps
===========

Hi, to introduce you the Tago features, let’s start with a hands on example. In this example, let’s create a full ecosystem that communicates with an emergency power generator localized in Chicago, Il.

The following real-time information will be obtained:

* Fuel level
* Oil pressure
* Battery level
* Running hours
* Location

Also, we will setup actions that will be triggered when some variables reach a defined value. In this case, Tago will send an SMS to the operating manager when the Fuel level is lower than 10%.

Let's do this!

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube.com/watch?v=TChfKm8CJac" frameborder="0" allowfullscreen></iframe>

Creating bucket
---------------

Bucket is your storage tool; all data received from your devices or subscriptions are stored here. You may create as many buckets as you wish. Let’s create one for the Power generator device.

First, access the Tago Admin and click on Data on the sidebar. Then, click on Add new bucket blue button.

.. raw:: html

	<img src="https://tago.io/assets/img/screenshot/create_bucket_1.png" alt="" width="800" height="600">

Now, enter with the bucket name and description. You can edit the fields later if needed.

.. raw:: html

	<img src="https://tago.io/assets/img/screenshot/create_bucket_2.png" alt="" width="800" height="600">

Great! You created your bucket! It should be something like this:

.. raw:: html

	<img src="https://tago.io/assets/img/screenshot/create_bucket_3.png" alt="" width="800" height="600">

.. raw:: html

	<small>Tip: We have APIs to create devices and anything else that is shown here. You may check the full API documentation if you want to build automated scripts.</small>

.. code-block:: javascript

	export default function OptionFactory (variable) {
	    const option_identifiable = Object.create({}, {
	        id: {
	            get: function() {
	                if (this.bucket && this.device) {
	                    return this.variable + this.bucket.id + this.device.id;
	                } else{
	                    return this.variable + this.counter;
	                }
	            }
	        }
	    });

	    return _.assign(Object.create(option_identifiable), variable);
	}

Sending data
------------

Sending data from a device to Tago system is very easy. Tago API is RESTful.

Basically, when you are sending data to Tago, you are writing on its database. So, you only need to POST the data in the route https://api.tago.io/data and use a device token in the header.

All API responses are in JSON format. Also, you can send your data in the JSON format. Some types of data are available.

The variable structure is:

* variable - string - required
* value - string/int/float - required
* unit - string - required
* type - string
* time - string/js_dateformat
* location - string/geojson
* Here is one example:

.. code-block:: json

	{ 'value': 32, 'variable': 'fuel_level', 'unit': '%' }

Now, let’s send this variable using curl and httpie. We will need the device token created in the earlier step.

curl
^^^^

Idk Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

httpie
^^^^^^

It was very easy, right? We may even have an SDK for your language for simple plug-and-play. Check out our [Github page](https://github.com/tago-io).

This is an example using node.js. You can copy the code from our github page.
