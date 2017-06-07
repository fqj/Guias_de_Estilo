5. Start with a fast first load

Progressive Web Apps should start fast and be usable immediately. In its current state, our Weather App starts quickly, but it's not useable. There's no data. We could make an AJAX request to get that data, but that results in an extra request and makes the initial load longer. Instead, provide real data in the first load.

Inject the weather forecast data
For this code lab, we'll simulate the server injecting the weather forecast directly into the JavaScript, but in a production app, the latest weather forecast data would be injected by the server based on the IP address geo-location of the user.

The code already contains the data that we're going to inject. It's the initialWeatherForecast that we used in the previous step.

Differentiating the first run
But, how do we know when to display this information, which may not be relevant on future loads when the weather app is pulled from the cache? When the user loads the app on subsequent visits, they may have changed cities, so we need to load the information for those cities, not necessarily the first city they ever looked up.

User preferences, like the list of cities a user has subscribed to, should be stored locally using IndexedDB or another fast storage mechanism. To simplify this code lab as much as possible, we've used localStorage, which is not ideal for production apps because it is a blocking, synchronous storage mechanism that is potentially very slow on some devices.

Extra Credit: Replace localStorage implementation with idb, check out localForage as a simple wrapper to idb.

First, let's add the code required to save user preferences. Find the following TODO comment in your code.

  // TODO add saveSelectedCities function here
And add the following code below the comment.

  // Save list of cities to localStorage.
  app.saveSelectedCities = function() {
    var selectedCities = JSON.stringify(app.selectedCities);
    localStorage.selectedCities = selectedCities;
  };
Next, let's add the startup code to check if the user has any saved cities and render those, or use the injected data. Find the following comment:

  // TODO add startup code here
And add the following code below this comment:

/************************************************************************
   *
   * Code required to start the app
   *
   * NOTE: To simplify this codelab, we've used localStorage.
   *   localStorage is a synchronous API and has serious performance
   *   implications. It should not be used in production applications!
   *   Instead, check out IDB (https://www.npmjs.com/package/idb) or
   *   SimpleDB (https://gist.github.com/inexorabletash/c8069c042b734519680c)
   ************************************************************************/

  app.selectedCities = localStorage.selectedCities;
  if (app.selectedCities) {
    app.selectedCities = JSON.parse(app.selectedCities);
    app.selectedCities.forEach(function(city) {
      app.getForecast(city.key, city.label);
    });
  } else {
    /* The user is using the app for the first time, or the user has not
     * saved any cities, so show the user some fake data. A real app in this
     * scenario could guess the user's location via IP lookup and then inject
     * that data into the page.
     */
    app.updateForecastCard(initialWeatherForecast);
    app.selectedCities = [
      {key: initialWeatherForecast.key, label: initialWeatherForecast.label}
    ];
    app.saveSelectedCities();
  }
The startup code checks if there are any cities saved in local storage. If so, then it parses the local storage data and then displays a forecast card for each of the saved cities. Else, the startup code just uses the fake forecast data and saves that as the default city.

Save the selected cities
Finally, you need to modify the "add city" button handler to save the selected city to local storage.

Update your butAddCity click handler so that it matches the following code:

document.getElementById('butAddCity').addEventListener('click', function() {
    // Add the newly selected city
    var select = document.getElementById('selectCityToAdd');
    var selected = select.options[select.selectedIndex];
    var key = selected.value;
    var label = selected.textContent;
    if (!app.selectedCities) {
      app.selectedCities = [];
    }
    app.getForecast(key, label);
    app.selectedCities.push({key: key, label: label});
    app.saveSelectedCities();
    app.toggleAddDialog(false);
  });
The new additions are the initialization of app.selectedCities if it doesn't exist, and the calls to app.selectedCities.push() and app.saveSelectedCities().

Test it out
When first run, your app should immediately show the user the forecast from initialWeatherForecast.
Add a new city (by clicking the + icon on the upper right) and verify that two cards are shown.
Refresh the browser and verify that the app loads both forecasts and shows the latest information.
TRY IT

