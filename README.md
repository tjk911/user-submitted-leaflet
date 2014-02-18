User-submitted Leaflet map
===========
This is a WIP, combining @courieressig's ["Tabletop to Leaflet"](https://github.com/csessig86/tabletop_to_leaflet) and @mapbox's ["Geo for Google Docs"](https://github.com/mapbox/geo-googledocs) into a single entity.

It's a responsive mapping tool that allows users to submit locations, and with one click, geocode said locations to a leaflet-based map.

* @courieressig's original tool relied on Bootstrap, this has been tweaked to run on Foundation instead. 
* @mapbox's original script also looped and created additional columns with each geocode, this has been fixed. 
* @mapbox's original script also included a geo_accuracy column, this has been removed as it wasn't being used by Tabletop to Leaflet.

To do list/broken stuff
===========
* Styling has to be fixed, and most of the original files from @courieressig's tool is still there

* Update readme to combine both @courieressig and @mapbox's scripts

* Update readme to provide more leaflet styling/plugin info

* Create examples

* Debug having too many columns/sources (should be some silly error on my end, temporarily ignored by removing references).

Setting up Tabletop
===========
* Create a Google Docs spreadsheet, and ensure that anyone who has the link can view it

* On the menu bar, click "Insert > Form" and create the relevant form, making sure that address fields are asked (address, state, zip)

* Address fields can be a single question or split separately, it doesn't matter

* Return to the spreadsheet, rename the headers to one-word lowercase words/titles

* Open up the js/script.js or js/script_cluster.js file and add your spreadsheet ID as a value to the spreadsheetKey key in the initializeTabletopObject. This is on line 19 of the file.
	```initializeTabletopObject('0Aq-sgqQU9ojidFR6aG9rS3ZpRElkdFNPVDFDenhGMnc');```

Setting up Leaflet
===========
* The data will then be sent to the startUpLeafet function. We will loop through the data and create variables for each column in the spreadsheet. In the js/script.js file, change lines 45 through 49 to match with the column names in your Google spreadsheet. NOTE: your numbers may be off by a few lines if you have more or less columns than the example table:
	```javascript
	var dataOne = tabletopData[num].brewery;
	var dataTwo = tabletopData[num].address;
	var dataThree = tabletopData[num].city;
	var dataFour = tabletopData[num].phone;
	var dataFive = tabletopData[num].website;
	```

* Similarily, we will scroll down to lines 63 to 70 (again, your numbers may be off) and change the text in popup variable to the names of your columns. So change 'Address', 'City', etc. to the appropriate column names:
	```javascript
	var popup = "<div class=popup_box" + "id=" + num + ">";
    popup += "<div class='popup_box_header'><strong>" + dataOne + "</strong></div>";
    popup += "<hr />";
    popup += "<strong>Address:</strong> " + dataTwo + "<br />";
    popup += "<strong>City:</strong> " + dataThree + "<br />";
    popup += "<strong>Phone:</strong> " + dataFour + "<br />";
    popup += "<strong>Website:</strong> " + dataFive + "<br />";
    popup += "</div>";
    ```

* Quick note, lines 1-6 from script.js and script_cluster.js defines the initial location and zoom level. I use [iTouchMap](http://itouchmap.com/latlong.html) to get a starting point's Lat/Long.

Geocode installation
===========

* Copy the source of geocode.js (located in js/geocode.js)
* Open your spreadsheet and go to tools > script editor
* Replace the content in the text box with the copied source from mapbox.js
* Set the name of this script to geo
* Go to file > save and close the popup window
* Refresh your spreadsheet and you will see a new menu called Geo added after Help on the menu bar

Geocode usage
===========
* Highlight/select the relevant cells, they can be a single cell or multiple cells
* Click "Geo" and select "Geocode Addresses" and choose an API, MapQuest requires no API key while the others (Yahoo & Cicero) requires one
* Note, please abide by MapQuest's [ToS here](https://developer.mapquest.com/web/products/open/geocoding-service)
* Two additional columns titled longitude and latitude should be created with the relevant data
* If the columns already exist, it should be updated/filled instead of created


Below is the readme info from @courieressig and @mapbox that has yet to be adapted over.


```
Tabletop to Leaflet
===========
* [Live demo](http://wcfcourier.com/app/special/tabletop_to_leaflet)

* Uses [Tabletop.js](http://builtbybalance.com/Tabletop/) and a [Google Spreadsheet](https://docs.google.com/spreadsheet/pub?key=0As3JvOeYDO50dF9NWWRiaTdqNmdKQ1lCY3dpdDhZU3c&output=html) to feed data to a [Leaflet](http://leafletjs.com/) map template.

* The map template is responsive, meaning it works on screens both big and small.

* Besides Tabletop.js and Leaflet, the template utilizes the [Bootstrap](http://twitter.github.io/bootstrap/) framework.

* H/T to [Chris Keller](https://twitter.com/ChrisLKeller) for his work on his [Tabletop to DataTables template](https://github.com/chrislkeller/datafeed_to_datatables).

* For more information, check out my [blog post](http://csessig.wordpress.com/2013/05/08/creating-responsive-maps-with-leaflet-google-docs/).


Styling the map
===========
* This example uses plain blue markers provided by Leaflet but plenty of options are available. For more, visit [their website](http://leafletjs.com/reference.html).

* You also style the map's sidebar, header, buttons, etc. using the css/style.css file. Here's an example using a [black template](http://wcfcourier.com/app/special/wloo_history/).


Plugins
===========
* You can also use [Leaflet plugins](http://leafletjs.com/plugins.html‎) with the map. One example is the [Leaflet.markercluster plugin](https://github.com/Leaflet/Leaflet.markercluster), which clusters markers that are close together. You can see an example of this with the "index_cluster.html" file. A live example can be viewed by [clicking here](http://wcfcourier.com/app/special/tabletop_to_leaflet/index_cluster.html).



```