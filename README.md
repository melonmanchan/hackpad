# About Hackpad
Hackpad is a web-based realtime wiki, based on the open source EtherPad collaborative document editor.


The etherpad package is distributed under the Apache License, Version 2.0.

All other packages are redistributed under their original license terms.  See below for a license summary of redistributed software.  More comprehensive license information can be found in the documentation of each package.

This document contains licensing information relating to the use of free and open-source software (FOSS) with or within the Hackpad software.  The authors, licensors, and distributors of the FOSS disclaim all express or implied conditions, representations, and warranties relating to the FOSS and any liability arising from use and distribution of the FOSS.

This document identifies the FOSS packages used in the Hackpad software, the FOSS licenses that Dropbox believes govern those FOSS packages.  While Dropbox has sought to provide complete and accurate licensing information for each FOSS package, Dropbox does not represent or warrant that the licensing information provided herein is correct or error-free.  Recipients of the Hackpad software should investigate the identified FOSS packages to confirm the accuracy of the licensing information provided herein.  Recipients are also encouraged to notify Dropbox of any inaccurate information or errors found in these notices.


# Aalto-specific installation notes

## Step 1. getting the software

You oughta use this fork of Hackpad since it contains some enchancements for running Hackpad inside of a Docker
container in production.

So first, you need to clone this repository.

```sh
    git clone https://github.com/melonmanchan/hackpad
```

Then, cd into the directory and build this repository as a Docker image

```sh
    docker build -t aalto-hackpad .
```

##

## Step 2. Setting up configuration variables

Modify the file under ./etherpad/etc/etherpad.docker.properties with your custom settings.
The rows of particular interest are:

```
    etherpad.superUserEmailAddresses = __email_addresses_with_admin_access__

    topdomains = localhost,localbox.info
    etherpad.canonicalDomain = localhost:9000

```

the topdomains and canonicalDomain variables should be set to whatever the final public URL will be,
for example

```
    topdomains = layersbox.aalto.fi
    etherpad.canonicalDomain = layersbox.aalto.fi

```
## Step 2.1 Setting up the Google registration

First, log in to the google developer console at https://console.developers.google.com

Then, click on 'select a project' and then click on 'Create a project'. Input whatever name you
desire. After a while, you should be redirected to the dashboard of your project. Click on the 'use
Google APIs' tile, then click on the Google+ API under the 'Social APIs'-subsection and enable it.


Next, click on Credentials in the side bar.  Click the 'Create credentials' button and select OAuth
client ID. Select 'Web application' and click the 'Create' button.

It's important to add the correct redirect url in the Restrictions-section. For Hackpad, it's

```
    http://<YOUR_HACKPAD_URL>/ep/account/openid
```

Next, copy the Client ID and Client secret from this very page

After some testing, it seems like setting the googleConsumerKey and googleConsumerSecret in the
properties file does not work for some reason, so your best bet is to open up ./src/e
therpad/pro/google_accounts.js and replace the following lines with your own Google client secret
and id on lines 258-260.

```js
    function clientDetails() {
      return {token_uri :  "https://accounts.google.com/o/oauth2/token",
              auth_uri : "https://accounts.google.com/o/oauth2/auth",
              client_secret: YOUR_API_SECRET_HERE,
              client_id: YOUR_API_ID_HERE};
    }
```

and that should be enough to enable Google authentication for your Hackpad instance!

## Step 2.2. Setting up email authentication

If, like me, you had trouble getting SMTP to play nice with Hackpad, you can use the following handy little script:

https://github.com/melonmanchan/hackpad/mailhack

Follow it's instructions in the README.md for usage.


## Step 3. starting up the container

After building and configuring your instance, start the container with

```sh
    docker run -d -p 9000:9000 -v /path/to/this/repo:/etc/hackpad/src aalto-hackpad
```

------


## Apache License, Version 2.0

solr
http://lucene.apache.org/solr/

smack api
http://www.igniterealtime.org/projects/smack/

gdata java client
https://code.google.com/p/gdata-java-client/

FacebookSDK.framework
https://developers.facebook.com/docs/ios/

GoogleToolbox
https://code.google.com/p/google-toolbox-for-mac/

OCMock
https://github.com/erikdoe/ocmock/blob/master/Source/License.txt

## MIT and MIT-Style Licenses

bililiteRange.js
https://github.com/dwachss/bililiteRange

handlebars.js
https://github.com/wycats/handlebars.js/blob/master/LICENSE

html5shiv
https://code.google.com/p/html5shiv/

i18next
http://i18next.com/

JQuery
http://jquery.com/

JQueryUI
http://jqueryui.com/

jquery.ajaxqueue.js
http://www.onemoretake.com/2009/10/11/ajaxqueue-and-jquery-1-3/

jquery.autocomplete.js
http://bassistance.de/jquery-plugins/jquery-plugin-autocomplete/

jquery.ba-dotimeout.min.js
http://benalman.com/projects/jquery-dotimeout-plugin/

jquery.color.js
https://github.com/jquery/jquery-color

jquery.contextMenu.js
https://github.com/medialize/jQuery-contextMenu

jquery.customSelect.js
https://github.com/adamcoulombe/jquery.customSelect

jquery.embedly.js
https://github.com/embedly/embedly-jquery

jquery.handsontable.js
http://handsontable.com/

jquery.placeholder.js
https://github.com/mathiasbynens/jquery-placeholder

jquery.sendkeys.js
https://github.com/dwachss/bililiteRange

jquery.tablesorter.js
http://tablesorter.com/docs/

jquery.textcomplete.min.js
https://github.com/yuku-t/jquery-textcomplete/

jquery.tinysort.js
http://tinysort.sjeiti.com/

jquery.ui.position.js
http://jqueryui.com/

jquery.ui.touch-punch.min.js
http://touchpunch.furf.com/

jquery.validate.js
http://bassistance.de/jquery-plugins/jquery-plugin-validation/

jquery.transition.js
https://github.com/louisremi/jquery.transition.js/

less-1.4.1.min.js
http://www.lesscss.org/

LESS Hat
http://LESSHat.com/

pagedown
https://code.google.com/p/pagedown/source/browse/LICENSE.txt

require.js
http://github.com/jrburke/requirejs

selectivizr-min.js
http://selectivizr.com/

simplewebrtc.bundle.js
https://github.com/HenrikJoreteg/SimpleWebRTC

socket.io.js
https://github.com/LearnBoost/socket.io-client

ACE Syntax Highlighter (tokenizer.js)
http://ace.c9.io/

to-markdown
https://github.com/domchristie/to-markdown

unicode.js
http://xregexp.com

MBProgressHUD
https://github.com/jdg/MBProgressHUD

WebViewJavascriptBridge
https://github.com/marcuswestin/WebViewJavascriptBridge/blob/master/LICENSE

JavaScript Pretty Date
http://ejohn.org/blog/javascript-pretty-date/

JSON Framework
https://code.google.com/p/json-framework/

Emoji One Non-Artwork
https://github.com/Ranks/emojione

ZeroClipboard
https://github.com/zeroclipboard/zeroclipboard

## BSD and BSD-Style Licenses

java-apns
https://github.com/notnoop/java-apns

glue sprite generator
https://github.com/jorgebastida/glue

NSAttributedString+DDHTML
https://github.com/dbowen/NSAttributedString-DDHTML/

RNCachingURLProtocol
https://github.com/rnapier/RNCachingURLProtocol

Sente Testing Kit
http://www.quantum-step.com/download/sources/mystep/OCUnit/SourceCode/SenTestingKit/OpenSourceLicense.html

ASIHTTPRequest
http://allseeing-i.com/ASIHTTPRequest/

## Other Licenses

jquery.autoresize.js
https://github.com/warpech/jQuery.fn.autoResize

vocaro.com UIImage Resize
https://gist.github.com/benilovj/2009030

Emoji One Artwork
https://github.com/Ranks/emojione
