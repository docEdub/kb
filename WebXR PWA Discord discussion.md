https://discord.com/channels/758943204715659264/758943204715659267/880713151564378143

---

![ ](https://cdn.discordapp.com/avatars/715739649867251745/9126c750742c29b5d7f7ff8d9b0a20a2.webp?size=256)

## lancelumix _—_ 08/27/2021

Has anyone tried to package a WebXR application in an APK ? I found this older thread on Reddit: [https://www.reddit.com/r/WebVR/comments/dd8ah6/how_to_publish_webvr_games_as_native_apps/](https://www.reddit.com/r/WebVR/comments/dd8ah6/how_to_publish_webvr_games_as_native_apps/ "https://www.reddit.com/r/WebVR/comments/dd8ah6/how_to_publish_webvr_games_as_native_apps/")

reddit

[r/WebVR - How to publish WebVR games as Native apps?](https://www.reddit.com/r/WebVR/comments/dd8ah6/how_to_publish_webvr_games_as_native_apps/)

5 votes and 16 comments so far on Reddit

![](https://cdn.discordapp.com/avatars/715739649867251745/9126c750742c29b5d7f7ff8d9b0a20a2.webp?size=256)@lancelumix

Has anyone tried to package a WebXR application in an APK ? I found this older thread on Reddit: [https://www.reddit.com/r/WebVR/comments/dd8ah6/how_to_publish_webvr_games_as_native_apps/](https://www.reddit.com/r/WebVR/comments/dd8ah6/how_to_publish_webvr_games_as_native_apps/ "https://www.reddit.com/r/WebVR/comments/dd8ah6/how_to_publish_webvr_games_as_native_apps/")

![ ](https://cdn.discordapp.com/avatars/269572981792047106/00642f29f3db932f0c93c9c583e9cedb.webp?size=256)

## slt _—_ 08/27/2021

[https://www.npmjs.com/package/cordova-plugin-aframe](https://www.npmjs.com/package/cordova-plugin-aframe "https://www.npmjs.com/package/cordova-plugin-aframe") There is this old project that add aframe inside a cordova app (cordova being a wrapper that convert a Web app into a mobile app)

npm

[cordova-plugin-aframe](https://www.npmjs.com/package/cordova-plugin-aframe)

A-Frame for Cordova

[![](https://images-ext-1.discordapp.net/external/2wk8OcHCn611djWAWkrbos0ZdT46qDFw0Q3s_CuGp0E/https/static.npmjs.com/338e4905a2684ca96e08c7780fc68412.png?width=160&height=84)](https://static.npmjs.com/338e4905a2684ca96e08c7780fc68412.png)

![ ](https://cdn.discordapp.com/avatars/277596274239209472/36f892dcea824da1ef6d3de0127f2614.webp?size=256)

## De-Panther _—_ 08/27/2021

Look into PWA. Both Android Play Store and Microsoft Windows Store should support PWA as store apps now.

_[_9:46 AM_]_

[https://www.pwabuilder.com/](https://www.pwabuilder.com/ "https://www.pwabuilder.com/")

[PWABuilder](https://www.pwabuilder.com/)

All the tools you need to build and deploy your Progressive Web Apps.

![ ](https://cdn.discordapp.com/avatars/264452965862080512/36e25c8d235c6b14d324e8940e7a035c.webp?size=256)

## Jonathan Hale _—_ 08/27/2021

PWAs work great, wonderland will be releasing one-click PWA support with next version.

![👀](https://discord.com/assets/4c5a77a89716352686f590a6f014770c.svg)

2

![vrwow](https://cdn.discordapp.com/emojis/759884776151842858.png?v=1)

1

![ ](https://cdn.discordapp.com/avatars/277596274239209472/36f892dcea824da1ef6d3de0127f2614.webp?size=256)

## De-Panther _—_ 08/27/2021

I implemented PWA install button in Worlds Demolisher. Didn't get to use the Quest in the last month or so. Did they implemented PWA yet?

![ ](https://cdn.discordapp.com/avatars/498273781589213185/0e0ebe15a861a936959c02edac0334b4.webp?size=256)

## shaw _—_ 08/27/2021

non trivial

_[_1:20 PM_]_

We have a WebXR pseudo polyfill we shipped for a client

_[_1:21 PM_]_

Using capacitor, which is an offshoot of cordova

_[_1:21 PM_]_

But real WebXR requires you to compile chrome with a flag off ![:cry:](https://discord.com/assets/f6d30507f4baee759bc9d7e5c0d3ba4f.svg)

_[_1:21 PM_]_

So WebXR currently is only supported in Chrome, not Android browser apps (i.e. webviews in apps)

_[_1:21 PM_]_

[https://bai.dev/projects/webxr-electron-apr2021.html](https://bai.dev/projects/webxr-electron-apr2021.html "https://bai.dev/projects/webxr-electron-apr2021.html")

[Electron + WebXR](https://bai.dev/projects/webxr-electron-apr2021.html)

How to ship immersive WebXR experiences as native apps

[![](https://images-ext-1.discordapp.net/external/xMG71UuxrMQD5acWBPVNr0NtQiC7zbzuFTI_62pn5ZM/https/bai.dev/images/articles/webxr-electron-apr2021/electron-webxr-twitter-white.png?width=800&height=400)](https://bai.dev/images/articles/webxr-electron-apr2021/electron-webxr-twitter-white.png)

_[_1:22 PM_]_

Bai was able to get this running with Electron, similar but different process

_[_1:22 PM_]_

And it should be possible but non-trivial to compile Cordova, Capacitor, etc with WebXR support(edited)

_[_1:24 PM_]_

@slt @lancelumix In the meantime people are just emulating the API and driving with native ARKit and such, and we have a plugin that demonstrates most of this that can get you started: [https://github.com/XRFoundation/native-xr-for-web](https://github.com/XRFoundation/native-xr-for-web "https://github.com/XRFoundation/native-xr-for-web")(edited)

![](https://cdn.discordapp.com/avatars/715739649867251745/9126c750742c29b5d7f7ff8d9b0a20a2.webp?size=256)@lancelumix

Has anyone tried to package a WebXR application in an APK ? I found this older thread on Reddit: [https://www.reddit.com/r/WebVR/comments/dd8ah6/how_to_publish_webvr_games_as_native_apps/](https://www.reddit.com/r/WebVR/comments/dd8ah6/how_to_publish_webvr_games_as_native_apps/ "https://www.reddit.com/r/WebVR/comments/dd8ah6/how_to_publish_webvr_games_as_native_apps/")

![ ](https://cdn.discordapp.com/avatars/548176959293751338/97eae6b93a9003a1261be3afac388332.webp?size=256)

## Michael Vogt _—_ 08/27/2021

Here you can package a PWA to a TWA (trusted web app) for the play store. Don't know about App store. [https://www.pwabuilder.com/](https://www.pwabuilder.com/ "https://www.pwabuilder.com/")(edited)

[PWABuilder](https://www.pwabuilder.com/)

All the tools you need to build and deploy your Progressive Web Apps.

_[_4:18 PM_]_

Did this with my AR app earlier this year. Worked like a charm.

![ ](https://cdn.discordapp.com/avatars/715739649867251745/9126c750742c29b5d7f7ff8d9b0a20a2.webp?size=256)

## lancelumix _—_ 08/27/2021

Amazing thanks you @Michael Vogt @shaw @De-Panther @slt @Jonathan Hale

![🙂](https://discord.com/assets/da3651e59d6006dfa5fa07ec3102d1f3.svg)

2

![](https://cdn.discordapp.com/avatars/715739649867251745/9126c750742c29b5d7f7ff8d9b0a20a2.webp?size=256)@lancelumix

Amazing thanks you @Michael Vogt @shaw @De-Panther @slt @Jonathan Hale

![ ](https://cdn.discordapp.com/avatars/498273781589213185/0e0ebe15a861a936959c02edac0334b4.webp?size=256)

## shaw _—_ 08/27/2021

NP, @Michael Vogt 's solution is the easiest

![ ](https://cdn.discordapp.com/avatars/548176959293751338/97eae6b93a9003a1261be3afac388332.webp?size=256)

## Michael Vogt _—_ 08/27/2021

The only problem is, that the use of WebXR isn't recognized automatically and added to the Android manifest. So the app is also offered to devices that aren't compatible. Maybe I would use the cli that's used by PWABuilder instead (don't remember the name...) next time and add this to the Android manifest manually.

![ ](https://cdn.discordapp.com/avatars/548176959293751338/97eae6b93a9003a1261be3afac388332.webp?size=256)

## Michael Vogt _—_ 08/27/2021

Found it: [https://github.com/GoogleChromeLabs/bubblewrap](https://github.com/GoogleChromeLabs/bubblewrap "https://github.com/GoogleChromeLabs/bubblewrap")

GitHub

[GitHub - GoogleChromeLabs/bubblewrap: Bubblewrap is a Command Line ...](https://github.com/GoogleChromeLabs/bubblewrap)

Bubblewrap is a Command Line Interface (CLI) that helps developers to create a Project for an Android application that launches an existing Progressive Web App (PWAs) using a Trusted Web Activity. ...

[[Discord]]
[[PWA]]
[[WebXR]]
