alpine headless: [![](https://images.microbadger.com/badges/image/weboaks/node-karma-protractor-chrome:alpine.svg)](https://microbadger.com/images/weboaks/node-karma-protractor-chrome:alpine "alpine headless")   
debian headless: [![](https://images.microbadger.com/badges/image/weboaks/node-karma-protractor-chrome.svg)](https://microbadger.com/images/weboaks/node-karma-protractor-chrome "debian headless")   
xvfb: [![](https://images.microbadger.com/badges/image/weboaks/node-karma-protractor-chrome:headless.svg)](https://microbadger.com/images/weboaks/node-karma-protractor-chrome:headless "Get your own image badge on microbadger.com") 

[![docker stars](https://img.shields.io/docker/stars/weboaks/node-karma-protractor-chrome.svg)](https://hub.docker.com/r/weboaks/node-karma-protractor-chrome/)
[![docker pulls](https://img.shields.io/docker/pulls/weboaks/node-karma-protractor-chrome.svg)](https://hub.docker.com/r/weboaks/node-karma-protractor-chrome/)
[![docker build](https://img.shields.io/docker/build/weboaks/node-karma-protractor-chrome.svg)](https://hub.docker.com/r/weboaks/node-karma-protractor-chrome/)
[![automated build](https://img.shields.io/docker/automated/weboaks/node-karma-protractor-chrome.svg)](https://hub.docker.com/r/weboaks/node-karma-protractor-chrome/)

# Karma and Protractor in a docker container

This image allows to run javascript tests in a headless machine like a CI server.

This image support karma and protractor test under chromium.

Unfortunately, chromium doesn't support container (https://github.com/travis-ci/travis-ci/issues/938), you need to start chromium with --no-sandbox argument to avoid this.

To configure karma and protractor, use this snippets:
### karma:
```javascript
browsers: ['Chromium_no_sandbox'],
customLaunchers: {
  Chromium_no_sandbox: {
    base: 'ChromiumHeadless',
    flags: ['--no-sandbox']
  }
},
```
ChromiumHeadless is available since karma-chrome-launcher@2.2.0, on previous versions use:
```javascript
base: 'Chromium',
flags: ['--no-sandbox', '--headless', '--disable-gpu', '--remote-debugging-port=9222']
```

### protractor:
```javascript
capabilities: {
  'browserName': 'chrome',
  'chromeOptions': {
    'args': ['no-sandbox', 'headless', 'disable-gpu']
  }
},
```
## Headless mode

Chromium recently [added headless support](https://chromium.googlesource.com/chromium/src/+/lkgr/headless/README.md).
If you want to use headless mode use the [![](https://images.microbadger.com/badges/version/weboaks/node-karma-protractor-chrome:headless.svg)](https://microbadger.com/images/weboaks/node-karma-protractor-chrome:headless "Get your own version badge on microbadger.com")  version and follow instructions in this readme.

If you don't want to use the headless  mode, use 
[![](https://images.microbadger.com/badges/version/weboaks/node-karma-protractor-chrome:xvfb.svg)](https://microbadger.com/images/weboaks/node-karma-protractor-chrome:xvfb "Get your own version badge on microbadger.com")
or
[![](https://images.microbadger.com/badges/version/weboaks/node-karma-protractor-chrome.svg)](https://microbadger.com/images/weboaks/node-karma-protractor-chrome "Get your own version badge on microbadger.com") and follow instructions in [that readme](https://github.com/sylvaindumont/docker-node-karma-protractor-chrome/tree/xvfb)

## Alpine Headless
To use alpine instead of debian, follow headless instructions and add this to protractor config :
```
chromeDriver: '/usr/bin/chromedriver',
```


## Gitlab CI

To run karma and protractor on gitlab ci, just use this image, and configure karma and protractor as above.
http://doc.gitlab.com/ce/ci/yaml/README.html#image-and-services

## On Docker Hub
https://hub.docker.com/r/weboaks/node-karma-protractor-chrome/

    docker pull weboaks/node-karma-protractor-chrome
