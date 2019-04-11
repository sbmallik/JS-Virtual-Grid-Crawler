# JavaScript Virtual Grid Sitemap Crawler

### Quickly collect screenshots of all your website pages and responsive viewports.

### To Install:

* ```$ git clone git@github.com:applitools/JS-Virtual-Grid-Crawler.git```
* ```$ npm install```

### To Run:

```
$ node crawler.js --help

Usage: crawler [options]

Options:
  -V, --version                 output the version number
  -u --url [url]                Add the site URL you want to generate a sitemap for. e.g. -u https://www.seleniumconf.com
  -s --sitemap [sitemap]        Use an already existing sitemap file. e.g. -s "/path/to/sitemap.xml" Note: This overrides the -u arg
  -m, --sitemapUrl [sitemapUrl  Specify a sitemap URL. e.g. -m https://www.example.com/sitemap.xml
  -b, --browsers [browsers]     Add the MAX number of browsers to run concurrently. e.g. -b 10. Note: Be careful with this!
  -k --key [key]                Set your Applitools API Key. e.g. -k yourLongAPIKeyyyyy
  -v --serverUrl [serverUrl]    Set your Applitools on-prem or private cloud server URL. (Default: https://eyes.applitools.com). e.g. -v https://youreyes.applitools.com
  --no-grid                     Disable the Visual Grid and run locally only (Default: false). e.g. --no-grid
  --log                         Enable Applitools Debug Logs (Default: false). e.g. --log
  --headless                    Run Chrome headless (Default: false). e.g. --headless
  --no-fullPage                 Disable Full Page Screenshot (Default: full page). e.g. --no-fullPage
  -U --URL [URL]                Add a single web URL you want to capture images for. e.g. -U https://www.google.com
  -a --appName [appName]        Override your appName. e.g. -a MyApp
  -t --testName [testName]      Override your testName. e.g. -t MyTest
  -l --level [level]            Set your Match Level "Layout2, Content, Strict, Exact" (Default: Strict). e.g. -l Layout2
  -h, --help                    output usage information
```

### Examples:

* Set an environment variable for your Applitools API Key. e.g. export APPLITOOLS_API_KEY="Your_API_KEY"

* Generate Sitemap and Run: `$ node crawler.js -u https://www.seleniumconf.com`
* Use a sitemap.xml URL and Run: `$ node crawler.js -m https://slack.com/sitemap.xml -b 20 --headless`
* Use existing sitemap.xml and Run: `$ node crawler.js -s ./sitemaps/www.seleniumconf.com.xml`
* Use a self made sitemap and Run: `$ node crawler.js -s ./sitemaps/random-sitemap.xml`
* Open 20 browsers concurrently (default: 10): `$ node crawler.js -s ./sitemaps/www.primerica.com.xml -b 20`
   * The max browsers by default is 10. However, if the sitemap.xml only has 5 links, then only 5 browsers will open.
   * ***Be careful with this value***. Opening too many browsers might kill your machine. Leave it at the default (10) and tweak this value slightly until you know the ideal number your machine can handle.
* Disable Visual Grid and Run locally: `$ node crawler.js -s ./sitemaps/www.seleniumconf.com.xml --no-grid`
* Enable Applitools Debug logs: `$ node crawler.js -s ./sitemaps/www.seleniumconf.com.xml --log`
* Run Chrome Headless: `$ node crawler.js -s ./sitemaps/www.seleniumconf.com.xml --headless`
* Overides: Set API Key and On-Prem/Private Cloud Server URL and Run: `$ node crawler.js -u https://seleniumconf.com -k YourApiKey -v https://youreyes.applitools.com`
* Crawl a single URL: `$ node crawler.js -U https://www.google.com`
* Crawl a single URL and set a App and Test Name: `$ node crawler.js -U https://www.google.com -a Google -t HomePage`
* Disable Full Page Screenshot: `$ node crawler.js -s ./sitemaps/www.seleniumconf.com.xml --no-fullPage`

### Notes:

* Quit during mid-execution:
   * ctrl-c only once and wait! This should put you in the FINALLY block to kill the execution and close all browsers. Repeated ctrl-c might break out of the his block and leave zombie browsers running on your pc which you'll have to manually kill. 

### Current VG Hardcoded Options:

```
browsersInfo: [
   { width: 1200, height: 800, name: 'firefox' },
   { width: 1200, height: 800, name: 'ie' },
   { width: 1200, height: 800, name: 'edge' },
   { width: 1200, height: 800, name: 'chrome' },
   { deviceName: 'iPhone X', screenOrientation: 'portrait' },
   { deviceName: 'iPad',     screenOrientation: 'portrait' },
   { deviceName: 'Nexus 7',  screenOrientation: 'portrait' },
   { deviceName: 'Pixel 2',  screenOrientation: 'portrait' }
]
```

### ToDos:

* Create configuration file to pass in the virtual grid configurations.
* Multithread/process the sitemap creation to speed it up.
* Clean/Dry the code. Split methods into classes.
* Add additional checks/actions to a sitemap. e.g: 
```
   <url>
      <loc>https://www.seleniumconf.com/</loc>
      <action>driver.findElement(By.tagName('button')).click();</action>
      <check>eyes.checkElementBy(By.css("div.section"), null, "Example")</check>
   </url>
```