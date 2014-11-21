Laravel Country Lookup by IP Address
======================================

Laravel package to lookup the country associated with an IPv4 address. Creates and populates a local database table, 
so there are no external requests being made during runtime.

This product includes GeoLite data created by MaxMind, available from
<a href="http://www.maxmind.com">http://www.maxmind.com</a>. The updated free downloadable database is released the
first Tuesday of each month. I'll attempt to ensure to update this package each time.

How to Install
--------------
Require the package with composer.
```bash
composer require "smalldogs/ip2country:dev-master"
```

Create and populate the database lookup table.
```bash
php artisan migrate --package="smalldogs/ip2country"
```

How to Use
----------

```php
// Returns the 2 letter country code for the user, eg: 'US'
$myCountryCode = Ip2Country::get();

// Returns the full name of the country, eg: 'United States'
$myCountryName = Ip2Country::getFull();

// Get the country for someone other than user on the page
$someonesIpAddress = '192.168.0.1';
$someonesCountryCode = Ip2Country::get($someonesIpAddress);
```

Configuration
-------------
By default, if the IP address is not found in the lookup table, it will return 'US' as a country code, and 'United 
States' as a country name. You can customize this in the config.

```bash
php artisan config:publish smalldogs/ip2country
```

Then navigate to <code>app/config/packages/smalldogs/ip2country/config.php</code>.
```php
return array(
    // If IP address is not found, what country is returned
    'default_country_code' => 'US',
    'default_country_name' => 'United States'
);

````
If you don't want anything returned if the IP address is not found, simply set each of these to <code>=> null</code>