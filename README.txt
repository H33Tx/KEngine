# KEngine - Katana PHP Engine
Simple - Extensive - Fast
If you have any questions regarding this engine, themes, plugins
or anything related to it, open an issue or join the Discord!

Join our Discord: https://discord.gg/uahG2fKVvg
Visit our Website: https://h33t.moe and https://treacherouswaters.org
Donate <3 https://ko-fi.com/saintly or https://paypal.me/WOLFRAMEdev

# What is the KEngine?
The KEngine is a PHP framework made for primarily our projects.
It is intended to run all of our projects as "themes" instead
of completely new frameworks for each of our project. As we are
familiar with it, development will go much smoother and faster
with it than before.

# Requirements
PHP 5.3 to 7.4, 8.x is not supported.

# Installation
You need to install required node_modules. Do so with `npm install`
or download `node_modules.zip` in the "releases"-tab.

For development, run `npx tailwindcss -o ./dist/output.css --watch`
and force refresh page when making changes to the templates.

# Documentation
For installation, see the paragraph above.

## Important Variables
(array)     $config // Contents of `config.php`, see below
                    // Smarty & PHP
(bool)      $logged // Is user logged in? Smarty & PHP
(string)    ROOT    // Root-directory of your installation
                    // Ends with a slash. PHP only
(array)     $theme  // Holds all data about your theme
                    // PHP only
(string)    $timeZone   // Timezone Name of server. Smarty & PHP
(float)     $version    // Version of installed KEngine instance.
                    // Smarty only

## Config
The central config-file for KEngine is `config.php`. Anything
inside the `$config`-variable will be assigned to smarty, thus
being accessible in the `.tpl`-files. Since we make use of
the PHPRouter (see docs below), setting the URL correctly is
essential for everything to run. The default config comes with
some data, but you can edit most of it to your liking.
However, this is what you CAN NOT remove:
$config
|- debug
|- url
|- theme
|- path
|- -- langs
|- -- plugins
|- smarty
|- -- template
|- -- config
|- -- compile
|- -- cache

## Database
KEngine uses SleekDB by default and comes shipped with it. However,
to use it, you need the `SleekDB` plugin - load order is important!
You *could* use MySQL, but as of now, there's no plugin (yet).

## Router
This software makes use of the `PHPRouter`. You can define routes
in the `routes.php` file in your theme by adding a new array to
the `$customRoutes` with following structure:
Array(
    Type,
    Request,
    File
);
For example, a GET-request for the index would look like this:
`["get", "/", "views/index.php"]`
... or read the official documentation: https://phprouter.com

## Autoload
This file is kind of the core of KEngine.
Structure:
- Creates session
- Starts Timer [1]
- Sets `$error` to `false`
//- Checks if a `.installed`-file exists (not in use in v1.0.0)
- Sets `$logged` to `false`
- Requires config-variables
- Activates debug-mode (if `true` in config)
- Requires functions
- Creates `$parsedown` (Parsedown)
- Creates `$purifier` (HTMLPurifier)
- Creates `$smarty` (Smarty)
- Checks for salt
- Checks if `info.php` for theme exists and requires it
- Gets all the plugins in the array-order ASC from the theme
- Assigns smarty variables

[1] You can record how fast your page loads. In your `views/*.php`
-file include `system/files/timer.stop.php` - this assigns the
time it took to load everything in miliseconds to the Smarty vari-
able `{$rendertime}`.

## Themes
Creating themes is actually like creating a new software - but
without having to write the complete back-end, just a few handlers
and frontend-files. In this example, we will use the `euphoria`-theme:
Euphoria
|- info.php         - Holds all of your themes information, config, etc.
|- routes.php       - As mentioned earlier, this defines the web-routes
|- api/             - Holds all of your PHP API-files
|- -- index.php
|- pages/           - Holds the page-contents of your templates
|- -- index.tpl
|- parts/           - Holds parts of your templates
|- -- foot.tpl
|- -- footer.tpl
|- -- head.tpl
|- -- header.tpl
|- views/           - Holds your PHP Handlers (e.g. index.php)
|- -- index.php

## Functions
Some of the core-functions from the `functions.php`-file.
- clean($data)  // Completely sanitizes $data
- cat($data)    // Turns "This is CooL" to "this-is-cool", for URLs
- namba($data)  // Files $data for numbers and returns only them
- now()         // Returns timestamp of current time d-m-Y H:i:s
- jd($data)     // json_decode() but in short
- je($data)     // json_encode() but in short with pretty print
- rdash($data)  // Replaces dashes with spaces
- ps($data)     // Used for __DIR__, replaces slashes with / or \
                // Depends on platform
- genUuid()     // Generates Unique user id
- genToken()    // Generates a token that *should* be used for sessions
- formatBytes($data)    // Formats bytes to MB, KB, etc.
- rmrf($dir)    // Completely gets rid of a directory. USE WITH CAUTION!
- formatDate($data) // Formats timestamp from now() to a readable date
- timeAgo($data)    // takes timestamp from now() and returns how much
                // passed since then
- str_contains($hay, $needle)   // An implementation of the PHP 8.x
                // function str_contains for PHP 7.x and lower
- shorten($data, $max)  // Shortens given data to a length of $max and
                // if longer, returns cut-off string with appended "..."
- titlify($a, $b, $c)   // Takes three variables and turns them to one,
                // Useful for pagetitle-generation
- startsWith($data, $search)    // Checks if $data starts with $search
                // Returns `true` if yes, `false` if no

# Credits
- PHP (developed on 7.4)
- TailwindCSS (by default)
- Snowbite (Tailwind framework)
- HTMLPurifier
- SleekDB
- Smarty
- Parsedown
- PHPRouter

# Contributors
ForsakenMaiden @s-vhs
Saintly2k @saintly2k