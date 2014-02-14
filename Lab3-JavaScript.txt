//Weather Display

function Execute() {
    var myOptions1 = {
        zoom: 3,
        center: new google.maps.LatLng(20.5937, 78.9629),
        mapTypeId: google.maps.MapTypeId.ROADMAP
    };
    var map = new google.maps.Map(document.getElementById("map_weather"), myOptions1);
    var weather = new google.maps.weather.WeatherLayer({
        temperatureUnits: google.maps.weather.TemperatureUnit.DEGREE //Temperature unit can also be changed to FAHRENHEIT by using the keyword "FAHRENHEIT"
    });
    weather.setMap(map);
    var cloud = new google.maps.weather.CloudLayer();
    cloud.setMap(map); 
}            

//Navgator Display


function Navigator(){
var elevator;
var myOptions = {
    zoom: 6,
    mapTypeId: 'terrain'
};
//var map_geo = new google.maps.Map(document.getElementById("map_geo"), myOptions);
    map = new google.maps.Map($('#map_geo')[0], myOptions);
var markers = [];

  if(navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(function(position) {
      var pos = new google.maps.LatLng(position.coords.latitude,
                                       position.coords.longitude);

      var infowindow = new google.maps.InfoWindow({
        map: map,
        position: pos,
        content: 'Location found using HTML5.'
      });

      map.setCenter(pos);
    }, function() {
      handleNoGeolocation(true);
    });
  } else {    
    handleNoGeolocation(false);
  }
}

//Direction Display

var directionDisplay;
var directionsService = new google.maps.DirectionsService();    
var map2;
var Source;
var dest;

function initialize()
{
    var Source = document.getElementById("i1").value;
    var dest = document.getElementById("i2").value;
    if(Source==""&& Destination=="")
    {
        
    }
else
{
    document.getElementById("map_view").hidden = false;
    directionsDisplay = new google.maps.DirectionsRenderer();        
    var center = new google.maps.LatLng(0, 0);     
    var myOptions =
    {
            zoom:7,
            mapTypeId: google.maps.MapTypeId.ROADMAP,
            center: center
    }
    map2 = new google.maps.Map(document.getElementById("map_view"), myOptions);
    directionsDisplay.setMap(map2);

    var request =
    {
            origin:Source,
            destination:dest,
            travelMode: google.maps.DirectionsTravelMode.DRIVING         
    };
    directionsService.route(request, function(response, status)
    {
            if (status == google.maps.DirectionsStatus.OK) 
            {
            directionsDisplay.setDirections(response);         
            }
    });
}
}

var button = document.getElementById('button');

var onClick = function() { 
    initialize();
};

button.addEventListener('click', onClick, false);

var clbutton = document.getElementById('clbutton');

var onClClick=function(){
    document.getElementById("map_view").hidden = true;
    document.getElementById("i1").value="";
    document.getElementById("i2").value="";
   
};

clbutton.addEventListener('click', onClClick, false);

//Navigator Display
var Nbutton = document.getElementById('Nbutton');
var onClick = function() { 
    document.getElementById("map_geo").hidden = false;
    Navigator();
};
Nbutton.addEventListener('click', onClick, false);

var onClClick=function(){
    document.getElementById("map_geo").hidden = true;    
   
};

Nclbutton.addEventListener('click', onClClick, false);


//Weather Display

var Wbutton = document.getElementById('Wbutton');
var onClick = function() { 
    document.getElementById("map_weather").hidden = false;
    Execute();
};
Wbutton.addEventListener('click', onClick, false);

var onClClick=function(){
    document.getElementById("map_weather").hidden = true;     
   
};

Wclbutton.addEventListener('click', onClClick, false);


