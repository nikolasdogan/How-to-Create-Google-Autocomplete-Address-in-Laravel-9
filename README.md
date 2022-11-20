# How-to-Create-Google-Autocomplete-Address-in-Laravel-9

Laravel Google autocomplete address tutorial, with the help of this comprehensive guide,
you will find out how to create and implement a google autocomplete address in laravel with
the use of google address API.

The autocomplete is a robust places library, which referred to the JavaScript maps API.
The autocomplete mechanism is employed in the web and mobile applications to integrate the
Google maps search field’s type-ahead search behavior.

Google autocomplete address helps you display the complete address such as longitude,
latitude, country, state, city, and zip code. Not just that, you can dynamically
place or add the marker’s location using the google map in laravel.

Let us check out systematically how to integrate google autocomplete address in laravel.

###  Implementation of Google Autocomplete Address in Laravel 9 Example  ###

Step 1: Create Laravel Project
Step 2: Arrange Google Place API Key
Step 3: Create Controller
Step 4: Create Route
Step 5: Set up Blade View
Step 6: Incorporate Google Autocomplete Adress Script
Step 7: Test Laravel App


Create Laravel Project
Initialize the first step with laravel application installation, hence open console and execute the following command:
|--------------------------------------------------------------------------
| composer create-project --prefer-dist laravel/laravel laravel-google-autocomplete-app
|--------------------------------------------------------------------------

Get Google Place API Key
This tutorial is incomplete if you don’t have Google place API key, so visit cloud.google.com and get the place google api key.

Create Controller
Subsequently, run the below command, it will generate a new controller.

|--------------------------------------------------------------------------
| php artisan make:controller AutoAddressController
|--------------------------------------------------------------------------

After that, head over to app/controllers/AutoAddressController.php file and add the given below code:


***************************************************************************
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
class AutoAddressController extends Controller
{
    public function googleAutoAddress()
    {
    	return view('welcome');
    }
}
****************************************************************************

Inside this controller we declared the logic to set the blade view template name inside the googleAutoAddress() method.

Create Route
Then, to load the lade view template we need to define a route with GET method, the route method takes controller
where we declared the method also name the route which will become the address to make the request.

Next, open routes/web.php file likewise update the following code.
***************************************************************************
<?php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\AutoAddressController;
/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
|
*/
Route::get('auto-complete-address', [AutoAddressController::class, 'googleAutoAddress']);

****************************************************************************

Set up Blade View
Now comes the time when you need to define the autocomplete address form in laravel blade view,
therefore open resources/views/welcome.blade.php file and update the following code within the template:

<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Laravel Google Autocomplete Address Example</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
    <script src="https://code.jquery.com/jquery-3.4.1.js"></script>
</head>
<body>
    <div class="container mt-5">
        <h2>Implement Google Autocomplete Address in Laravel 8</h2>
        <div class="form-group">
            <label>Location/City/Address</label>
            <input type="text" name="autocomplete" id="autocomplete" class="form-control" placeholder="Choose Location">
        </div>
        <div class="form-group" id="latitudeArea">
            <label>Latitude</label>
            <input type="text" id="latitude" name="latitude" class="form-control">
        </div>
        <div class="form-group" id="longtitudeArea">
            <label>Longitude</label>
            <input type="text" name="longitude" id="longitude" class="form-control">
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
    </div>
</body>
</html>

****************************************************************************

Incorporate Google Autocomplete Adress Script
Finally, you have to define the Google Autocomplete Address script, wherefore insert the given JavaScript code before the closed body HTML tag:

<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
<script type="text/javascript"
    src="https://maps.google.com/maps/api/js?key=Your_Google_Key=places&callback=initAutocomplete"></script>
<script>
    $(document).ready(function () {
        $("#latitudeArea").addClass("d-none");
        $("#longtitudeArea").addClass("d-none");
    });
</script>
<script>
    google.maps.event.addDomListener(window, 'load', initialize);
    function initialize() {
        var input = document.getElementById('autocomplete');
        var autocomplete = new google.maps.places.Autocomplete(input);
        autocomplete.addListener('place_changed', function () {
            var place = autocomplete.getPlace();
            $('#latitude').val(place.geometry['location'].lat());
            $('#longitude').val(place.geometry['location'].lng());
            $("#latitudeArea").removeClass("d-none");
            $("#longtitudeArea").removeClass("d-none");
        });
    }
</script>
JavaScript
Here is the final example of conjugated code:

<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Laravel Google Autocomplete Address Example</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
    <script src="https://code.jquery.com/jquery-3.4.1.js"></script>
</head>
<body>
    <div class="container mt-5">
        <h2>Implement Google Autocomplete Address in Laravel 8</h2>
        <div class="form-group">
            <label>Location/City/Address</label>
            <input type="text" name="autocomplete" id="autocomplete" class="form-control" placeholder="Choose Location">
        </div>
        <div class="form-group" id="latitudeArea">
            <label>Latitude</label>
            <input type="text" id="latitude" name="latitude" class="form-control">
        </div>
        <div class="form-group" id="longtitudeArea">
            <label>Longitude</label>
            <input type="text" name="longitude" id="longitude" class="form-control">
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
    <script type="text/javascript"
        src="https://maps.google.com/maps/api/js?key=Your_Google_Key=places&callback=initAutocomplete"></script>
    <script>
        $(document).ready(function () {
            $("#latitudeArea").addClass("d-none");
            $("#longtitudeArea").addClass("d-none");
        });
    </script>
    <script>
        google.maps.event.addDomListener(window, 'load', initialize);
        function initialize() {
            var input = document.getElementById('autocomplete');
            var autocomplete = new google.maps.places.Autocomplete(input);
            autocomplete.addListener('place_changed', function () {
                var place = autocomplete.getPlace();
                $('#latitude').val(place.geometry['location'].lat());
                $('#longitude').val(place.geometry['location'].lng());
                $("#latitudeArea").removeClass("d-none");
                $("#longtitudeArea").removeClass("d-none");
            });
        }
    </script>
</body>
</html>

-------------------------------------------------------------------------------------------
PHP

Test Laravel App
Next, start the laravel project using artisan command inside the terminal:

php artisan serve

Now, you can check the result on the browser with the following URL:

http://127.0.0.1:8000/auto-complete-address
