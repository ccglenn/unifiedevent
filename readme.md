# Rapid Response Kit: Building Conferencing and Broadcasting with Twilio. Level: Intermediate. Powered by Twilio - Laravel
[![Build Status](https://travis-ci.org/TwilioDevEd/conference-broadcast-laravel.svg)](https://travis-ci.org/TwilioDevEd/conference-broadcast-laravel)

An example application implementing an disaster response kit that allows an organizer to instantly communicate with volunteers.

[Read the full tutorial](https://www.twilio.com/docs/tutorials/walkthrough/conference-broadcast/php/laravel)!

### Run the application

1. Clone the repository and `cd` into it.
1. Install the application's dependencies with [Composer](https://getcomposer.org/)

   ```bash
   $ composer install
   ```
1. Copy the sample configuration file and edit it to match your configuration.

   ```bash
   $ cp .env.example .env
   ```

  You can find your `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN` under
  your
  [Twilio Account Settings](https://www.twilio.com/user/account/settings).
  You can buy Twilio phone numbers at [Twilio numbers](https://www.twilio.com/user/account/phone-numbers/search)
  `TWILIO_NUMBER` should be set to the phone number you purchased above.
  `TWILIO_RR_NUMBER` should be set to a Twilio number too.
1. Generate an `APP_KEY`:

   ```bash
   $ php artisan key:generate
   ```
1. Expose the application to the wider Internet using [ngrok](https://ngrok.com/)

   ```bash
   $ ngrok http 8000
   ```
   Once you have started ngrok, update your TwiML app's voice URL
   setting to use your ngrok hostname, so it will look something like
   this:

   ```
   http://<your-ngrok-subdomain>.ngrok.io/conference/join
   ```
1. Configure Twilio to call your webhooks
 You will also need to configure Twilio to call your application when calls are received.

 You will need to provision at least one Twilio number with voice capabilities
 so the application's users can participate in conferences. You can buy a number [right
 here](https://www.twilio.com/user/account/phone-numbers/search). Once you have
 a number you need to configure your number to work with your application. Open
 [the number management page](https://www.twilio.com/user/account/phone-numbers/incoming)
 and open a number's configuration by clicking on it.

 Remember that the number where you change the voice webhooks must be the same one you set on
 the `TWILIO_RR_NUMBER` environment variable.

 ![Configure Voice](http://howtodocs.s3.amazonaws.com/twilio-number-config-all-med.gif)

 For this application, you must set the voice webhook of your number to
 something like this:

 ```
 http://<your-ngrok-subdomain>.ngrok.io/conference/join
 ```
 And in this case set the `GET` method on the configuration for this webhook.
1. Run the application using Artisan.

  ```bash
  $ php artisan serve
  ```
  It is `artisan serve` default behaviour to use `http://localhost:8000` when
  the application is run. This means that the ip addresses where your app will be
  reachable on you local machine will vary depending on the operating system.

  The most common scenario, is that your app will be reachable through address
  `http://127.0.0.1:8000`, and this is important because ngrok creates the
  tunnel using only that address. So, if `http://127.0.0.1:8000` is not reachable
  in your local machine when you run the app, you must tell artisan to use this
  address, like this:

  ```bash
  $ php artisan serve --host=127.0.0.1
  ```

### Dependencies

This application uses this Twilio helper library:
* [twilio-php](https://github.com/twilio/twilio-php)

### Run the tests

1. Run at the top-level directory:

   ```bash
   $ phpunit
   ```
   If you don't have phpunit installed on your system, you can follow [this
   instructions](https://phpunit.de/manual/current/en/installation.html) to
   install it.
