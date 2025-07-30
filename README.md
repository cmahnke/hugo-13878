# Hugo GitHub Issue #13878

Details: <https://github.com/gohugoio/hugo/issues/13878>

Description: Failed to to resolve media type for remote resource in 0.148.2

## Instructions

Clone this branch of the repository and build the site.

```text
git clone --single-branch -b hugo-github-issue-13878 https://github.com/jmooring/hugo-testing hugo-github-issue-13878
cd hugo-github-issue-13878
hugo server
```


# Updated Version

The bug wasn't about reolving the resource, but it's about a difference in template resolution in 0.148.1 and 0.148.2.

Both exaples need to be run in `exampleSite`:

```
cd exampleSite
```

```
$ hugo-0.148.1 --themesDir ../.. --printUnusedTemplates --logLevel=debug 
Start building sites … 
hugo v0.148.1-98ba786f2f5dca0866f47ab79f394370bcb77d2f+extended darwin/arm64 BuildDate=2025-07-11T12:56:21Z

INFO  static: syncing static files to / duration 790.75µs
INFO  build:  step process substep collect files 1 files_total 1 pages_total 1 resources_total 0 duration 1.753792ms
INFO  build:  step process duration 1.796833ms
INFO  build:  step assemble duration 865.417µs
WARN  Executing _markup/_render-link.html with .Destination 'https://gdpr-info.eu/art-6-gdpr/'
ERROR .Err: Unable to get remote resource https://query.wikidata.org/sparql?query=SELECT+%3Fitem+%3FitemLabel+%3FofficialWebsite+%3FofficialBlog+%3FonlineDatabaseURL+WHERE+%7B%0A++++++%3Fitem+wdt%3AP856+%3Chttps%3A%2F%2Fgdpr-info.eu%2Fart-6-gdpr%2F%3E+.+SERVICE+wikibase%3Alabel+%7B+bd%3AserviceParam+wikibase%3Alanguage+%22%5BAUTO_LANGUAGE%5D%2Cen%22+.+%7D%0A++++++OPTIONAL+%7B+%3Fitem+wdt%3AP856+%3FofficialWebsite+.+%7D+OPTIONAL+%7B+%3Fitem+wdt%3AP1581+%3FofficialBlog+.+%7D+OPTIONAL+%7B+%3Fitem+wdt%3AP1316+%3FonlineDatabaseURL+.+%7D%0A++++%7D: template: _markup/_render-link.html:15:25: executing "_markup/_render-link.html" at <resources.GetRemote>: error calling GetRemote: failed to resolve media type for remote resource "https://query.wikidata.org/sparql?query=SELECT+%3Fitem+%3FitemLabel+%3FofficialWebsite+%3FofficialBlog+%3FonlineDatabaseURL+WHERE+%7B%0A++++++%3Fitem+wdt%3AP856+%3Chttps%3A%2F%2Fgdpr-info.eu%2Fart-6-gdpr%2F%3E+.+SERVICE+wikibase%3Alabel+%7B+bd%3AserviceParam+wikibase%3Alanguage+%22%5BAUTO_LANGUAGE%5D%2Cen%22+.+%7D%0A++++++OPTIONAL+%7B+%3Fitem+wdt%3AP856+%3FofficialWebsite+.+%7D+OPTIONAL+%7B+%3Fitem+wdt%3AP1581+%3FofficialBlog+.+%7D+OPTIONAL+%7B+%3Fitem+wdt%3AP1316+%3FonlineDatabaseURL+.+%7D%0A++++%7D"
INFO  build:  step render substep pages site en outputFormat html duration 4.667667ms
INFO  build:  step render pages 1 content 1 duration 4.688042ms
INFO  build:  step render deferred count 0 duration 250ns
INFO  build:  step postProcess duration 1.875µs
INFO  build:  duration 7.659375ms
Total in 25 ms
Error: error building site: logged 1 error(s)
```


```
$ hugo --themesDir ../.. --printUnusedTemplates --logLevel=debug 
Start building sites … 
hugo v0.148.2+extended+withdeploy darwin/arm64 BuildDate=2025-07-27T12:43:24Z VendorInfo=brew

WARN  skipping template file "/Users/cmahnke/projects/projektemacher/hugo-13878/layouts/_default/_markup/_render-link.html": unrecognized render hook template
INFO  static: syncing static files to / duration 270.042µs
INFO  build:  step process substep collect files 1 files_total 1 pages_total 1 resources_total 0 duration 212.542µs
INFO  build:  step process duration 251.583µs
INFO  build:  step assemble duration 168.583µs
INFO  build:  step render substep pages site en outputFormat html duration 1.746542ms
INFO  build:  step render pages 1 content 1 duration 1.765625ms
INFO  build:  step render deferred count 0 duration 459ns
INFO  build:  step postProcess duration 1.834µs
INFO  build:  duration 2.316167ms

                  │ EN 
──────────────────┼────
 Pages            │  1 
 Paginator pages  │  0 
 Non-page files   │  0 
 Static files     │  1 
 Processed images │  0 
 Aliases          │  0 
 Cleaned          │  0 

Total in 12 ms
```

