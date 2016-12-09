#SnaapDog 

##SnaapDog enables an open collaboration between seekers, finders, and shelters to get roaming dogs home

![landing view](front-end/SnaapDogApp/www/img/landing.png "Landing Page")


### Users will be able to:
* Create an alert for their lost pet and notify others in a set radius - tagged with description key words
* Upload a picture of a roaming dog and insert into the database as a sighting - tagged with key words
* Connect with each other without revealing personal contact information

<!-- Visit here: [Portfolio](http://) -->

###Requirements `npm install` once pulled


##Built with:
	- Html
	- CSS
	- Javascript
	- jQuery 
	- Bootstrap
  - Ionic Framework
  - Mongo

## What you won't see in the code:
### Ionic really starts in the terminal:
```
$ npm install -g ionic
$ ionic lib update
$ ionic start myapp [template]
```
###We used the tabs template.

###End of setup, now to see the app!
```
$ ionic serve [options] 
```           
###We used -l as the option, which tests on multiple screen sizes and platform types.
####https://ionicframework.com/docs/v2/cli/serve/  for more information.


##Sample Code
### Geolocation:

```javascript
.controller('mainCtrl', function($scope, $rootScope, $cordovaGeolocation, $ionicLoading, $ionicPlatform, fromDB, myLocation) {
  $ionicPlatform.ready(function() {
    $ionicLoading.show({
      template: '<ion-spinner icon="bubbles"></ion-spinner><br/>Finding your location'
    });
    // $ionicLoading.hide();
  });
  var markers = [];
  var myLoc = {};
  var map; 

  fromDB.strayEntries().then(function success(rspns) {
    var entries = rspns.data.docs;
    $rootScope.stray_entries = entries;
    $scope.totalEntries = $rootScope.stray_entries.length;
    console.log($rootScope.stray_entries);
  }, function fail(rspns) {
    console.log(rspns);
  })
  .then(function success(rspns) {
    myLocation.locate().then(function success(rspns) {
      var lat = rspns.coords.latitude;
      var lng = rspns.coords.longitude;
      myLoc = new google.maps.LatLng(lat, lng);
      map = new google.maps.Map(document.getElementById('map'), {
        center: myLoc,
        zoom: 8
      });
      $ionicLoading.hide();
    }, function fail(rspns) {
      console.log(rspns);
    })
    .then(function success(rspns) {
      for (var i = 0; i < $rootScope.stray_entries.length; i++) {
        placeMarkers($rootScope.stray_entries[i], map);
      }
    }, function fail(rspns) {
      console.log(rspns);u
    });
  }, function fail(rspns) {
    console.log(rspns);
  });
```
### Using states to route: even with inner menus:
```
  $stateProvider
   .state('tabs', {
      url: "/tabs",
      abstract: true,
      templateUrl: "templates/tabs.html",
      controller: 'TabsCtrl'
    })

   .state('landing', {
    url: '/landing',
    templateUrl: 'templates/landing.html',
    controller: 'LogInCtrl'
  })

   .state('tabs.dash', {
    url: '/dash',
    views: {
      'tab-dash': {
        templateUrl: 'templates/tab-dash.html',
        controller: 'TabsCtrl'
      }
    }
  })


  .state('tabs.chats', {
      url: '/tabs/chats',
      views: {
        'tab-chats': {
          templateUrl: 'templates/tab-chats.html',
          controller: 'TabsCtrl'
        }
      }
    })

  .state('tabs.chat-detail', {
      url: '/tabs/chats/:chatId',
      views: {
        'tab-chats': {
          templateUrl: 'templates/chat-detail.html',
          controller: 'TabsCtrl'
        }
      }
    })

  .state('tabs.account', {
    url: '/tabs/account',
    views: {
      'tab-account': {
        templateUrl: 'templates/tab-account.html',
        controller: 'TabsCtrl'
      }
    }
  })
  .state('tabs.listing', {
    url: '/listing',
    views: {
      'tab-listing': {
        templateUrl: 'templates/tab-listing.html',
        controller: 'listingCtrl'
      }
    }
  })

  .state('tabs.snaap', {
    url: '/snaap',
    views: {
      'tab-main': {
        templateUrl: 'templates/tab-snaap.html',
        controller: 'snaapCtrl'
      }
    }
  })

  .state('tabs.post', {
    url: '/post',
    views: {
      'tab-post': {
        templateUrl: 'templates/tab-post.html',
        controller: 'postCtrl'
      }
    }
  })
  

  .state('camera', {
    url: '/camera',
    templateUrl: 'templates/camera.html',
    controller: 'snaapCtrl'
  })

```

####Early stages of site
![Alt text](img/ScreenShot1.png "Early stages of site")

<!-- add a video of interaction with the site -->

##Future Add-ons
- Links to more current projects.
- Ability for visitors to send messages directly from the site to me.
- An enhanced UX/UI design that encourages more visitors.


