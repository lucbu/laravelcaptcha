# LaravelCaptcha

## Installation

Install with composer :

```
composer require lucbu\laravelcaptcha
```

Just add 
```
'Lucbu\LaravelCaptcha\CaptchaServiceProvider',
``` 
in the array `providers` in the file `config\app.php`.

Publish the package using the command `php artisan vendor:publish`

## Configuration

In the file `config\lucbu-laravelcaptcha.php` their is some parameters you can configurate:

 * length: The length of the captcha (should be an integer)
 * listForbidden: list of letters that won't appear in captcha
 * icon-play: Path to icon image used to display the clicking button to hear the sounds of letters
 * icon-update: Path to icon image used to update the captcha
 * background-color: color of the captcha background (use red green blue notation ['red' => $red, 'green' => $green, 'blue' => $blue])
 * text-color: color of the captcha text (use red green blue notation)
 * grid: Is there a grid behind the letters?
 * grid: Is there random lines on the captcha?
 * width: width of the captcha image;
 * height: height of the captcha image
 * sessionKey: the key used to store the captcha in Session Variable
 * default_language: the language in case we don't find the sounds for the locale

## Usage

In the form view, just use the following code :
```
@include('lucbu-laravelcaptcha::captcha')
```

You can validate the fields that has to be fulfill with captcha with the rule `lucbularavelcaptcha` :

```
public function rules() {
    return [
        'captcha' => 'required|lucbularavelcaptcha:is_caseSensitive'
    ];
}
```

You can set the parameters is_caseSensitive as 'true' or 'false', the validation will take care or not of matching the case (false by default).

You can generate a captcha in a controller like this :

```
<?php namespace App\Http\Controllers;

use Lucbu\LaravelCaptcha\Services\Captcha;

class ExampleController {
    public function exampleFunction(){
        Captcha::generateCaptcha();
    }
}
```

The function will create the captcha and store into the session variable.

You can also get just the image using the route `lucbu.laravelcaptcha.image` or the sound with the route `lucbu.laravelcaptcha.sound`.

The player used to play the sound is based on HTML5. (`<audio>` tag)