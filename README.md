# Your next Add-to-Calendar Button
![Add-to-Calendar Button](https://github.com/jekuer/add-to-calendar-button/blob/main/repo_image.png?raw=true)

_A convenient JavaScript snippet, which lets you create beautiful buttons, where people can add events to their calendars._


## Use case // Who this is for

This is for everybody, who wants to include a button at his/her website or app, which enables users to easily add a specific event to their calendars.
It's main goal is to keep this process as easy as possible. Simply define your button configuration via JSON and everything else is automatically generated by the script.
It is for this simple use case. No strings attached.


## Background // Why this repo exists

While building a personal wedding page, I was confronted with the task to include a button, where invited people could save the event to their calendars.
I did not want to build this from scratch (first) and therefore started the usual web research.
Unfortunately, all I found where some extremely outdated code snippets, which did not really fit all the modern systems and calendar tools.
Beside that, there was only the solution by AddEvent.com - all over the place. I was looking at CodePen and all I found where thousands of pens, which basically only included the AddEvent tool.
The problems with AddEvent.com:
* it holds tons of features, which I did not need. I do not want to track my button. I just want it to work.
* it limits the free tier to 50 event adds per month (consider the wedding case - this is way too less).
* it brings some data privacy issues, since you basically send your users to their service.
* the UX/UI is not ideal (imho).
*Bottom line:* Pay for features, which I do not need - at additional privacy "cost" - that made me create this solution (for you).


## DEMO

See [jekuer.github.io/add-to-calendar-button](https://jekuer.github.io/add-to-calendar-button/) for a live demo.


## Features

* Simple and convenient integration of multiple buttons - configure them directly within the HTML code.
* Optimized UX (for desktop and mobile) - adjustable.
* Beautiful UI (the best combined from experts around the world).
* Up-to-date integration of all popular calendars:
  * Google Calendar.
  * Yahoo Calender.
  * Microsoft 365 (and Outlook).
  * Automatically generated iCal/ics files (for all other calendars, like Apple).
* Timed and all-day events.
* Translatable labels and dynamic.
* Well documented code, to easily understand the processes.

![Demo Screenshot](https://github.com/jekuer/add-to-calendar-button/blob/main/demo.gif?raw=true)


## Setup

### Option 1: simple

1. Simply **download** the code from GitHub **or clone** the git repository.
2. Copy the css (atcb.min.css) and js (atcb.min.js) files from the assets (not the "npm_dist"!) folders into your project (the **.min.** files are required, but it is recommended to also copy the raw and map files).
3. Include those files in your project. As usual, the css goes into the <head> (`<link rel="stylesheet" href="./assets/css/atcb.min.css">`), the js into the <body> footer (`<script src="./assets/js/atcb.min.js" defer></script>`). You can also combine them with other files, if you want to.
4. Create your button as can be seen in the "Configuration" section below.
5. That is it. The script takes care of all the rest. :)

### Option 2: npm

1. Requires Node.js, npm, and a project, which builds on it (e.g. React or Angular).
2. Run **`npm install add-to-calendar-button`**.
3. Import the module into your project/component. For example with Angular/React: `import { atcb_init } from 'add-to-calendar-button';`.
4. Init the js after the DOM has been loaded. To determine the right moment and execute, ...
  1. with Angular, you would use `ngAfterViewInit()` with `atcb_init();` (mind that, depending on your app, other hooks might be better); 
  2. with React, you might want to include an event listener like `document.addEventListener('DOMContentLoaded', atcb_init, false);`.
5. Include the css. For example with Angular or React, add the following to the global style.css: `@import 'add-to-calendar-button/assets/css/atcb.min'`;
6. Create your button as can be seen in the "Configuration" section below.
7. That is it. The script takes care of all the rest. :)


## Configuration

A button can be easily created by placing a respective placeholder, wherever you want the button to appear.
(The `style="display:none;"` theoretically is not necessary, but should be used for better compatibility.)
```html
<div class="atcb" style="display:none;">
  (...)
</div>
```
Within this placeholder, you can easily configure the button, by placing a respective JSON structure.
Mind that with Angular, you might need to escape the { with `{{ '{' }}` and } with `{{ '}' }}`; with React it would be `{ '{' }` and `{ '}' }`.

### Minimal structure (required)

```html
<div class="atcb" style="display:none;">
  {
    "name":"Add the title of your event",
    "startDate":"02-21-2022",
    "endDate":"03-24-2022",
    "options":[
      "Google"
    ]
  }
</div>
```

### Full structure (without schema.org markup)

```html
<div class="atcb" style="display:none;">
  {
    "name":"Add the title of your event",
    "description":"A nice description does not hurt",
    "startDate":"02-21-2022",
    "endDate":"03-24-2022",
    "startTime":"10:13",
    "endTime":"17:57",
    "location":"Somewhere over the rainbow",
    "label":"Add to Calendar",
    "options":[
      "Apple",
      "Google",
      "iCal",
      "Microsoft365",
      "Outlook.com",
      "Yahoo"
    ],
    "timeZone":"Europe/Berlin",
    "timeZoneOffset":"+01:00",
    "trigger":"click",
    "iCalFileName":"Reminder-Event"
  }
</div>
```

### Full structure (with schema.org markup)
You can save on the `style="display:none;"`, but mind that you should not use dynamic dates (e.g. "today" or "+1") here!
You can use startTime and endTime in the event block, but it is recommended to rather add it to startDate and endDate with "T" as delimiter here.

```html
<div class="atcb">
  <script type="application/ld+json">
    {
      "event": {
        "@context":"https://schema.org",
        "@type":"Event",
        "name":"Add the title of your event",
        "description":"A nice description does not hurt",
        "startDate":"02-21-2022T10:13",
        "endDate":"03-24-2022T17:57",
        "location":"Somewhere over the rainbow"
      },
      "label":"Add to Calendar",
      "options":[
        "Apple",
        "Google",
        "iCal",
        "Microsoft365",
        "Outlook.com",
        "Yahoo"
      ],
      "timeZone":"Europe/Berlin",
      "timeZoneOffset":"+01:00",
      "trigger":"click",
      "iCalFileName":"Reminder-Event"
    }
  </script>
</div>
```
 

### Important information and hidden features

* The "label" is optional, but enables you to customize the button text. Default: "Add to Calendar".
* Dates need to be formatted as MM-DD-YYYY.
* You can also use the word "today" as date. It will then dynamically use the current day at click.
* Add "+5" at the end of the date to dynamically add 5 days (or any other number). "01-30-2022+12" would generate the 11th of February 2022. This can be interesting, when combined with "today".
* Times need to be formatted as HH:MM.
* Times are optional. If not set, the button generates all-day events.
* 1 option is required. You can add as many as you want. The supported formats are listed above.
* If you want to rename (or translate) a label, use the following schema at the options: optionName + Pipe + yourLabel. "Google|Google Kalender" would generate a Google Calendar option, but label it as "Google Kalender".
* If no timeZone and no timeZoneOffset is provided, the date refers to UTC time.
* You can add a timeZoneOffset or timeZone (TZ name). You can find a list of them at [Wikipedia](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).
* If the timeZoneOffset is set, it will always override the timeZone. It is recommended to only use 1 of them at a time.
* The timeZone might not work in very old browsers, but also considers dynamic changes like summer/winter time.
* timeZoneOffset works with older browsers, but is quite static.
* You can set the trigger to "click". This makes the button open on click at desktop. Otherwise, the default would be to open on hover. On touch devices, this makes no difference.
* If you want to define a specific name for any generated ics file (iCal), you can specify it via the "iCalFileName" option. The default would be "event-to-save-in-my-calendar".
* You can use the option "inline":true in order to make the button appear with inline-block instead of block style.
* If you require line breaks within the description, use `\n` or `<br>`.


## Contributing

Anyone is welcome to contribute, but mind the [guidelines](.github/CONTRIBUTING.md):

* [Bug reports](.github/CONTRIBUTING.md#bugs)
* [Feature requests](.github/CONTRIBUTING.md#features)
* [Pull requests](.github/CONTRIBUTING.md#pull-requests)

IMPORTANT NOTE: Run `npm install` and `npm run build` to create the minified js and css file, its sourcemap files as well as the npm_dist/ folder and content!


## License

The code is available under the [MIT license (with “Commons Clause” License Condition v1.0)](LICENSE.txt).


## Changelog (without bug fixes)

* v1.4 : schema.org support (also changed some keys in the JSON!)
* v1.3 : new license (MIT with “Commons Clause”)
* v1.2 : inline and line break support
* v1.1 : npm functionality
* v1.0 : initial release


## Kudos go to
* [github.com/dudewheresmycode](https://github.com/dudewheresmycodee)
* [uxwing.com](https://uxwing.com)
