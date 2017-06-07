# Cross Platform Desktop apps with NodeJS

## Legacy Analysis

### Applets

NPAPI (Technology required for Java applets) is no longer supported in Chrome.
 * https://www.java.com/es/download/faq/chrome.xml

### DirectX & Silverlight

Microsoft confirms that Edge will no longer support ActiveX and Silverlight.
 
https://www.genbeta.com/navegadores/microsoft-confirma-que-edge-dejara-de-soportar-para-activex-y-silverlight

Moving to HTML5 Premium Media

https://blogs.windows.com/msedgedev/2015/07/02/moving-to-html5-premium-media


## Electron

Electron is a desktop application framework from Github. It was built for their text editor Atom, and was originally known as Atom Shell. It allows you to build cross-platform desktop applications using HTML, CSS, and Javascript. Although it was released back in 2013, it has become very popular and is used by a number of startups and large businesses for their applications. Apart from Github’s Atom editor, the other major app using Electron is Slack, the chat application.

In many ways Electron is very similar to NW.js; one of the early contributors to NW.js (Cheng Zhao) is a core contributor to Electron, and works for Github in Beijing. Both frameworks combine Chromium and Node.js to allow you to build cross-platform desktop applications, and both have similar feature sets.

That said, Electron takes a slightly different approach to how applications are initialised, as well as how Chromium is integrated into the framework. To get a better understanding of this, let’s walk through an example of how Electron loads an application. 

## NW.JS (NodeWebKit)

NW.js is a framework for building desktop applications with HTML, CSS, and JavaScript. It was created by Roger Wang at Intel’s Open Source Technology Center in China, and worked by combining the Node.js programming framework with Chromium’s (then) browser engine — Webkit,hence the original name Node Webkit.

By combining Node.js with Chromium, Roger found a way to create applications that could not only load a local web site within an application window, but also could interact with the Operating System via a JavaScript API. This JavaScript API could control visual aspects like window dimensions, toolbar and menu items, as well as provide access to local files on the desktop. These are things that can’t be done with a hosted web site, or even a locally hosted web site.


## Comparison table

<table class="aligncenter" style="border-color: #a6a6a6; color: #ffffff;" border="1" width="100%" cellspacing="0" cellpadding="3">
<thead>
<tr style="height: 33px; background-color: #f0f0f0; color: #000000;">
<td style="text-align: left; height: 33px;" width="40%">&nbsp;</td>
<td style="text-align: center; height: 33px;" width="30%"><strong>NW.js 0.20.2</strong></td>
<td style="text-align: center; height: 33px;" width="30%"><strong>Electron&nbsp;v1.4.15</strong></td>
</tr>
</thead>
<tbody>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Project inception</td>
<td style="text-align: center; height: 33px;">2011</td>
<td style="text-align: center; height: 33px;">2013</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">Corporate Sponsor</td>
<td style="text-align: center; height: 33px;">Intel</td>
<td style="text-align: center; height: 33px;">GitHub</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Licensing</td>
<td style="text-align: center; height: 33px;" colspan="2" width="30%">Open Source, MIT License</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Browser Runtime</td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #beebc1;" width="30%"><a href="https://www.chromium.org/Home" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://www.chromium.org/Home', 'Chromium']);">Chromium</a></td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #fa9393;" width="30%"><a href="https://github.com/atom/libchromiumcontent" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://github.com/atom/libchromiumcontent', 'libchromiumcontent']);">libchromiumcontent</a></td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Node.js Version</td>
<td style="height: 33px; text-align: center; background-color: #beebc1;">&nbsp;6.3.0</td>
<td style="height: 33px; text-align: center; background-color: #fff27a;">6.1.0</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Chromium Version</td>
<td style="height: 33px; text-align: center; background-color: #beebc1;">52.0.2743.82</td>
<td style="height: 33px; text-align: center; background-color: #fff27a;">51.0.2704.106</td>
</tr>
<tr style="height: 37px;">
<td style="text-align: left; height: 37px;" width="40%">Entry Point</td>
<td style="width: 30%; text-align: center; height: 37px; background-color: #beebc1;" width="30%">HTML or JavaScript<sup>4</sup></td>
<td style="width: 30%; text-align: center; height: 37px; background-color: #fff27a;" width="30%">JavaScript</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Bare Distribution Size</td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #fff27a;" width="30%">139MB&nbsp;<span class="smaller">(52MB zipped)</span></td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #beebc1;" width="30%">125MB&nbsp;<span class="smaller">(45MB zipped)</span></td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Windows Platform Support</td>
<td style="width: 30%; height: 33px; text-align: center;" colspan="2" width="30%">Windows 7+&nbsp;<span class="smaller">(x86 and x64)</span></td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px; padding-left: 30px;" width="40%">Windows XP Support</td>
<td style="width: 30%; height: 33px; text-align: center; background-color: #beebc1;" width="30%">In LTS version (0.14.x)</td>
<td style="width: 30%; height: 33px; text-align: center; background-color: #fa9393;" width="30%">No</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Mac Platform Support</td>
<td style="width: 30%; height: 33px; text-align: center;" colspan="2" width="30%">Mac OS X.9&nbsp;+</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px; padding-left: 30px;" width="40%">Mac OS X.6</td>
<td style="width: 30%; height: 33px; text-align: center; background-color: #beebc1;" width="30%">In LTS version (0.14.x)</td>
<td style="width: 30%; height: 33px; text-align: center; background-color: #fa9393;" width="30%">&nbsp;No</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Architecture Support</td>
<td style="width: 30%; height: 33px; text-align: center;" colspan="2" width="30%">32bit <span class="smaller">(Win)</span>, 64bit <span class="smaller">(Win/Mac)</span> &amp; arm <span class="smaller">(limited)</span></td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Chrome Apps Support</td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #beebc1;" width="30%">Yes</td>
<td style="width: 30%; height: 33px; text-align: center; background-color: #fa9393;" width="30%">No</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">Support of chrome.* APIs</td>
<td style="text-align: center; height: 33px; background-color: #beebc1;">Yes</td>
<td style="text-align: center; height: 33px; background-color: #fa9393;">No</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Plugin Support</td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #beebc1;" width="30%">NaCL, Pepper</td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #fff27a;" width="30%">Pepper</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Adobe Flash Support</td>
<td style="width: 30%; text-align: center; height: 33px;" colspan="2" width="30%">via Pepper Plugin</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Mac App Store Support</td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #ffffff;" colspan="2" width="30%">Yes</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Windows App Store Support</td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #beebc1;" width="30%">Yes</td>
<td style="height: 33px; width: 30%; text-align: center; background-color: #fff27a;" width="30%">Windows 10+ (<a href="https://github.com/felixrieseberg/electron-windows-store" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://github.com/felixrieseberg/electron-windows-store', 'details']);">details</a>)</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">App signing</td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #beebc1;" colspan="2" width="30%">Yes</td>
</tr>
<tr style="height: 37px;">
<td style="text-align: left; height: 37px;" width="40%">Source Code Protection</td>
<td style="width: 30%; text-align: center; height: 37px; background-color: #beebc1;" width="30%">V8 Snapshot<sup>1</sup></td>
<td style="width: 30%; height: 37px; text-align: center; background-color: #fff27a;" width="30%">ASAR Archive Support<sup>2</sup></td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Auto-update</td>
<td style="width: 30%; height: 33px; text-align: center; background-color: #fff27a;" width="30%"><span class="smaller">Unclear (<a href="https://github.com/edjafarov/node-webkit-updater" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://github.com/edjafarov/node-webkit-updater', 'module']);">module</a>)</span></td>
<td style="width: 30%; height: 33px; text-align: center; background-color: #beebc1;" width="30%">Mac/Win <span class="smaller">(thru <a href="https://github.com/squirrel/squirrel.windows" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://github.com/squirrel/squirrel.windows', 'Squirrel']);">Squirrel</a>)</span></td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Crash Reporting</td>
<td style="width: 30%; text-align: center; height: 33px; background-color: #fa9393;" width="30%">No</td>
<td style="width: 30%; height: 33px; text-align: center; background-color: #beebc1;" width="30%">Yes</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;" width="40%">Kiosk Mode</td>
<td style="text-align: center; height: 33px;" colspan="2" width="30%">Partial <span class="smaller">(Buggy on Mac<sup>5</sup>)</span></td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">PDF Viewer</td>
<td style="text-align: center; height: 33px; background-color: #beebc1;">&nbsp;Yes</td>
<td style="height: 33px; text-align: center; background-color: #fff27a;">Using <a href="http://mozilla.github.io/pdf.js/" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'http://mozilla.github.io/pdf.js/', 'pdf.js']);">pdf.js</a></td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">Native Node Module Support</td>
<td style="text-align: center; height: 33px;" colspan="2">Yes&nbsp;</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">SSL Client Certificate</td>
<td style="text-align: center; height: 33px; background-color: #beebc1;">Yes</td>
<td style="text-align: center; height: 33px; background-color: #fff27a;">Partial (<a href="https://github.com/hokein/electron-sample-apps/tree/master/client-certificate" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://github.com/hokein/electron-sample-apps/tree/master/client-certificate', 'details']);">details</a>)</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">Print Preview</td>
<td style="text-align: center; height: 33px; background-color: #beebc1;">Yes</td>
<td style="text-align: center; height: 33px; background-color: #fa9393;">No</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">DevTools Extension Support</td>
<td style="height: 33px; text-align: center;" colspan="2">Yes</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">Debugging</td>
<td style="text-align: center; height: 33px;">DevTools + extensions</td>
<td style="text-align: center; height: 33px;">Dedicated <a href="http://electron.atom.io/devtron/" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'http://electron.atom.io/devtron/', 'Devtron']);">Devtron</a>&nbsp;Module</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">Integration Testing</td>
<td style="text-align: center; height: 33px;">ChromeDriver &amp; WebDriver</td>
<td style="text-align: center; height: 33px;">Dedicated <a href="http://electron.atom.io/spectron/" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'http://electron.atom.io/spectron/', 'Spectron']);">Spectron</a> Module</td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">Windows Installer</td>
<td style="text-align: center; height: 33px;">Yes <span class="smaller">(<a href="https://github.com/nwjs/nw-builder" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://github.com/nwjs/nw-builder', 'nw-builder']);">nw-builder</a>)</span></td>
<td style="text-align: center; height: 33px;">Yes <span class="smaller">(<a href="https://github.com/atom/grunt-electron-installer" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://github.com/atom/grunt-electron-installer', 'external module']);">external module</a>)</span></td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">html5test.com Score</td>
<td style="text-align: center; height: 33px;" colspan="2">492</td>
</tr>
<tr style="height: 37px;">
<td style="text-align: left; height: 37px;">Octane 2.0 Score<sup>3</sup></td>
<td style="text-align: center; height: 37px;">27205</td>
<td style="text-align: center; height: 37px;">27343</td>
</tr>
<tr style="height: 54px;">
<td style="text-align: left; height: 54px;">Issue Resolution Time<sup>6</sup></td>
<td style="text-align: center; height: 54px; background-color: #fa9393;"><img class="alignnone" src="http://isitmaintained.com/badge/resolution/nwjs/nw.js.svg" alt="" width="135" height="20"></td>
<td style="text-align: center; height: 54px; background-color: #beebc1;"><img class="alignnone" src="http://isitmaintained.com/badge/resolution/electron/electron.svg" alt="" width="128" height="20"></td>
</tr>
<tr style="height: 53px;">
<td style="text-align: left; height: 53px;">Open Issues<sup>6</sup></td>
<td style="text-align: center; height: 53px; background-color: #fa9393;"><img class="alignnone" src="http://isitmaintained.com/badge/open/nwjs/nw.js.svg" alt="" width="113" height="20"></td>
<td style="text-align: center; height: 53px; background-color: #beebc1;"><img class="alignnone" src="http://isitmaintained.com/badge/open/electron/electron.svg" alt="" width="106" height="20"></td>
</tr>
<tr style="height: 60px;">
<td style="text-align: left; height: 60px;">GitHub Trends</td>
<td style="height: 60px; text-align: center;"><iframe width="110px" height="20px" src="http://ghbtns.com/github-btn.html?user=nwjs&amp;repo=nw.js&amp;type=watch&amp;count=true&amp;v=2" frameborder="0" scrolling="0"></iframe> <iframe width="110px" height="20px" src="http://ghbtns.com/github-btn.html?user=nwjs&amp;repo=nw.js&amp;type=star&amp;count=true&amp;v=2" frameborder="0" scrolling="0"></iframe> <iframe width="110px" height="20px" src="http://ghbtns.com/github-btn.html?user=nwjs&amp;repo=nw.js&amp;type=fork&amp;count=true&amp;v=2" frameborder="0" scrolling="0"></iframe></td>
<td style="height: 60px; text-align: center;"><iframe width="110px" height="20px" src="http://ghbtns.com/github-btn.html?user=electron&amp;repo=electron&amp;type=watch&amp;count=true&amp;v=2" frameborder="0" scrolling="0"></iframe> <iframe width="110px" height="20px" src="http://ghbtns.com/github-btn.html?user=electron&amp;repo=electron&amp;type=star&amp;count=true&amp;v=2" frameborder="0" scrolling="0"></iframe> <iframe width="110px" height="20px" src="http://ghbtns.com/github-btn.html?user=electron&amp;repo=electron&amp;type=fork&amp;count=true&amp;v=2" frameborder="0" scrolling="0"></iframe></td>
</tr>
<tr style="height: 33px;">
<td style="text-align: left; height: 33px;">Open Codecs/Containers</td>
<td style="text-align: center; height: 33px;" colspan="2">Vorbis, Theora, Opus, VP8, VP9, PCM, Ogg, WebM, WAV</td>
</tr>
<tr style="height: 37px;">
<td style="text-align: left; height: 37px;">Licensed Codecs</td>
<td style="height: 37px; text-align: center;" colspan="2">MP3, MP4, H.264, AAC</td>
</tr>
</tbody>
</table>

1. Beware that this results in a 30% performance hit.
2. This is a very weak protection. It’s basically a TAR archive of all the project files. The Electron team decided against support for V8 snapshots. See details here.
3. Higher is better. Tests performed on Apple MacBook Pro Retina (Yosemite)
4. This can be done by using the “node-main” instruction in the package.json file or (in version 0.13 and above) through the Chrome Apps manifest file. 
5. Kiosk mode is enabled upstream by Chromium. If you would like the Chromium team to improve kiosk mode support on Mac, please vote for it.
6. Data from isitmaintained.com: NW.js, Electron.

Source: http://tangiblejs.com/posts/nw-js-and-electron-compared-2016-edition

Some of the applications using NW.js and Electron out there today include:
- Slack, the group chat application
- Gitter, another chat application, for developers
- Atom, Github’s IDE
- Microsoft’s Visual Studio Code, a cross-platform IDE
- Facebook’s Nuclide, a fork of Atom tailored for Facebook’s technologies
- Docker’s Kitematic, a GUI for Docker containers
- SoundNode — SoundCloud for desktop

# Conclusion



# Sources

* [http://tangiblejs.com/posts/nw-js-and-electron-compared-2016-edition](http://tangiblejs.com/posts/nw-js-and-electron-compared-2016-edition)

* [https://www.xplatform.rocks/2016/02/09/nw-js-vs-electron/](https://www.xplatform.rocks/2016/02/09/nw-js-vs-electron/)

* [https://medium.com/@paulbjensen/building-cross-platform-desktop-applications-with-electron-and-nw-js-e1fc93ae3bff#.dzp1c52mg](https://medium.com/@paulbjensen/building-cross-platform-desktop-applications-with-electron-and-nw-js-e1fc93ae3bff#.dzp1c52mg)