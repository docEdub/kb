## docEdub _—_ 08/26/2021

I think I'm hitting a WASM memory grow issue on the Quest 2 with this BabylonJS playground: [https://playground.babylonjs.com/#SY0NY5#5](https://playground.babylonjs.com/#SY0NY5#5 "https://playground.babylonjs.com/#SY0NY5#5") It works fine on desktop Chrome, but in Quest 2 browser it freezes during instrument allocation in the WASM synthesizer I'm using. If I pare down the memory usage a bit, it gets past the initial instrument allocations and works fine, but there seems to be some limit I'm hitting even though the OVR tool reports plenty of memory available overall.

  
![ ](https://cdn.discordapp.com/avatars/363620968146534401/456a50991c4555b83e6bbcb22134800f.webp?size=256)

## yinch _—_ 08/26/2021

I had similar divergence. It appears quest browser mem allocation caps out around 500 mb whereas windows chrome is closer to 2gb

![ ](https://cdn.discordapp.com/avatars/813082266196377683/41243e9b7a3476acf3d085448169848a.webp?size=256)

## docEdub _—_ 08/26/2021

oof

![ ](https://cdn.discordapp.com/avatars/735949862692061246/e63c3551751c47c275a3c423529feb9b.webp?size=256)

## m₂ _—_ 08/26/2021

yep, hit the same issue with Unity + Silk Brush

![](https://cdn.discordapp.com/avatars/813082266196377683/41243e9b7a3476acf3d085448169848a.webp?size=256)@docEdub

oof

![ ](https://cdn.discordapp.com/avatars/363620968146534401/456a50991c4555b83e6bbcb22134800f.webp?size=256)

## yinch _—_ 08/26/2021

[http://clb.confined.space/dump/mem_growth.html](http://clb.confined.space/dump/mem_growth.html "http://clb.confined.space/dump/mem_growth.html")

_[_8:45 PM_]_

You can test it at that link

![](https://cdn.discordapp.com/avatars/363620968146534401/456a50991c4555b83e6bbcb22134800f.webp?size=256)@yinch

[http://clb.confined.space/dump/mem_growth.html](http://clb.confined.space/dump/mem_growth.html "http://clb.confined.space/dump/mem_growth.html")

![ ](https://cdn.discordapp.com/avatars/813082266196377683/41243e9b7a3476acf3d085448169848a.webp?size=256)

## docEdub _—_ 08/26/2021

Thanks, that link let me allocate just shy of 1gb, so I should still have plenty left. I'm not sure what's going on but it's a very consistent issue in the Quest 2 browser. It hits the wall in exactly the same place every time.(edited)

![](https://cdn.discordapp.com/avatars/813082266196377683/41243e9b7a3476acf3d085448169848a.webp?size=256)@docEdub

Thanks, that link let me allocate just shy of 1gb, so I should still have plenty left. I'm not sure what's going on but it's a very consistent issue in the Quest 2 browser. It hits the wall in exactly the same place every time.(edited)

![ ](https://discord.com/assets/6f26ddd1bf59740c536d2274bb834a05.png)

## davehill00 (Oculus) _—_ 08/26/2021

We’ll take a look and see if we can figure out what’s going on. May not get to this til next week though.

August 27, 2021

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ 08/27/2021

@docEdub, @yinch, I've looked at your memory issues a bit.

_[_8:34 AM_]_

First thing to be aware of, Oculus Browser is a 32-bit executable. So 4 GB is a hard limit for memory use of the whole renderer, and Browser uses some of that.

_[_8:35 AM_]_

Second, these WASM allocations are for large _contiguous_ chunks of memory. So you might get access to more memory by asking for more, smaller chunks.

![🙏🏽](https://discord.com/assets/fcf78553740b6d379d28e1092fc293c9.svg)

1

![👍](https://discord.com/assets/08c0a077780263f3df97613e58e71744.svg)

1

_[_8:35 AM_]_

And one request for a larger chunk is more likely to succeed than a small request that you then try to resize.

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ 08/27/2021

The WASM memory limits depend on how your memory is set up. 2GB is a hard limit because of the way we handle pointers. If you need 1-2 GB then you should set WebAssemby.Memory initial to that size, _must be over 1GB._(edited)

_[_8:50 AM_]_

Most other combinations of options end up with a maximum size of 1GB.

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ 08/27/2021

I played around with @docEdub's demo a bit, it would be helpful if you could give me a pointer to where these instrument allocations typically fail, I wasn't sure what I was looking at.

_[_9:00 AM_]_

Hope that helps and makes sense.

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ 08/27/2021

Two more things ... 1. WASM shared memory is less flexible than non-shared when growing: it can only be resized in place. So only request shared memory when you need shared memory. And same as above, if you need a certain amount, it is better to request that size up front. 2. Probably goes without saying, but the more you request, the more likely it is the request will fail. If you can run in up to 1GB, then set initial to whatever you want and maximum as low as possible, up to 1GB. (The maximum will be capped at 1GB.)

_[_9:12 AM_]_

These guidelines may change in the future; let us know if you have feedback.

![](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)@dpc

These guidelines may change in the future; let us know if you have feedback.

![ ](https://cdn.discordapp.com/avatars/735949862692061246/e63c3551751c47c275a3c423529feb9b.webp?size=256)

## m₂ _—_ 08/27/2021

Greatly appreciate the insight. This would be good info to have somewhere in the docs as well if it's not there already.

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ 08/27/2021

Yeah... @davehill00 (Oculus) re: docs ^^^

![👍](https://discord.com/assets/08c0a077780263f3df97613e58e71744.svg)

1

![ ](https://cdn.discordapp.com/avatars/264452965862080512/36e25c8d235c6b14d324e8940e7a035c.webp?size=256)

## Jonathan Hale _—_ 08/27/2021

wonderland engine actually allocates only 500 MB initial memory

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ 08/27/2021

Oh, the bit about OVR tool's memory report... I believe that is telling you about memory _in use._ When you set up WASM Memory or a big ArrayBuffer, etc. the address space for it is _reserved,_ but the operating system hands Browser pages that are zeroed on demand. So there's two quick ways to look at that... The first is `adb shell ps | grep browser` and you'll see output like this:

```
u0_i11        3917 11964 1435992 117780 do_epoll_wait       0 S com.oculus.browser:sandboxed_process0:org.chromium.content.app.SandboxedProcessService0:11
u0_i12        4243 11964 2451636 102440 do_epoll_wait       0 S com.oculus.browser:sandboxed_process0:org.chromium.content.app.SandboxedProcessService0:12
u0_a51       11927   695 1632052 173104 do_epoll_wait       0 S com.oculus.browser
u0_a51       11964   695 1762336  64112 poll_schedule_timeout 0 S com.oculus.browser_zygote
u0_a51       31975   695 1434156 112768 do_epoll_wait       0 S com.oculus.browser:privileged_process1
```

One of the SandboxedProcessService entries is running your page. The fourth column is "virtual size", that's the reserved (including used) memory. So here I'm running the mem_growth sample, it happens to be in SandboxedProcessService0:12, the virtual size is ~2.4 GB even though it's resident size, the fifth column, is ~100 MB.

![](https://cdn.discordapp.com/avatars/264452965862080512/36e25c8d235c6b14d324e8940e7a035c.webp?size=256)Jonathan Hale

wonderland engine actually allocates only 500 MB initial memory

![ ](https://cdn.discordapp.com/avatars/264452965862080512/36e25c8d235c6b14d324e8940e7a035c.webp?size=256)

## Jonathan Hale _—_ 08/27/2021

It's something we can do, because we're designed from the ground up for wasm and hence way more lightweight than Unity and such, but effectively this avoids issues with the tab running out of memory when reloading the page during development. Just a heads up.

_[_9:38 AM_]_

Pardon: 64 MB initial mem, 500 max mem

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ 08/27/2021

Yeah so something like that, use less memory and have a maximum under 1 GB, is the sweet spot.

![👍](https://discord.com/assets/08c0a077780263f3df97613e58e71744.svg)

1

![ ](https://cdn.discordapp.com/avatars/264452965862080512/36e25c8d235c6b14d324e8940e7a035c.webp?size=256)

## Jonathan Hale _—_ 08/27/2021

So OC browser has 31BIT pointers enabled?

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ 08/27/2021

The last bit about understanding address space consumption... The second column is the renderer process ID, so for SandboxedProcessService0:12 in this example the PID is 4243, if you run `adb shell cat /proc/4243/maps` you'll get a dump of the whole 4 GB of memory and some notes about what has allocated what. The naming of these is a bit arcane but you'll see v8 there, you can do some math to work out whether there's sufficient gaps there etc.

![](https://cdn.discordapp.com/avatars/264452965862080512/36e25c8d235c6b14d324e8940e7a035c.webp?size=256)@Jonathan Hale

So OC browser has 31BIT pointers enabled?

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ 08/27/2021

V8 uses tagged pointers, yes.

![👍](https://discord.com/assets/08c0a077780263f3df97613e58e71744.svg)

1

_[_9:46 AM_]_

No doubt you've read about their SMI thing for storing numbers. Although in this case for the memory size limit it might be a specific tag for something else... I would need to do some digging.

![🤔](https://discord.com/assets/263a7f4eeb6f69e46d969fa479188592.svg)

1

![ ](https://cdn.discordapp.com/avatars/277596274239209472/36f892dcea824da1ef6d3de0127f2614.webp?size=256)

## De-Panther _—_ 08/27/2021

very interesting info

![👍](https://discord.com/assets/08c0a077780263f3df97613e58e71744.svg)

1

August 28, 2021

![ ](https://cdn.discordapp.com/avatars/813082266196377683/41243e9b7a3476acf3d085448169848a.webp?size=256)

## docEdub _—_ Yesterday at 11:41 AM

@dpc This is great info! Thank you. I'll investigate on my end a bit more using the `adb` commands and try building a static version of the synthesizer WASM so I can set the initial size using `WebAssemby.Memory`.

![ ](https://discord.com/assets/c09a43a372ba81e3018c3151d4ed4773.png)

## Rik Cabanier (Facebook) _—_ Yesterday at 11:58 AM

Would there be a way to download and release piece of this WASM code? It seems unrealistic to expect all devices to have access to so much free memory

![ ](https://cdn.discordapp.com/avatars/813082266196377683/41243e9b7a3476acf3d085448169848a.webp?size=256)

## docEdub _—_ Yesterday at 1:29 PM

Ya, I can make the WASM available if you want. I don't think the amount of memory needed is large for this WASM, so I don't think the issue I'm having is related to how much free memory is available. I got the static version of the synthesizer WASM built and got it to run on the Quest 2 by linking the WASM with `--initial-memory` and `--max-memory` set to 64mb and 500mb, but I'm now getting no sound out of the synthesizer. I can see it running, but it's not outputting any sound for some reason. I'll ask the synthesizer WASM devs if they know anything about that.(edited)

![ ](https://cdn.discordapp.com/avatars/264452965862080512/36e25c8d235c6b14d324e8940e7a035c.webp?size=256)

## Jonathan Hale _—_ Yesterday at 1:34 PM

@docEdub Maybe stupidly trivial to mention, but just in case: Oculus Browser & Chrome require interaction with the page before permitted to play sound.

![ ](https://cdn.discordapp.com/avatars/813082266196377683/41243e9b7a3476acf3d085448169848a.webp?size=256)

## docEdub _—_ Yesterday at 1:38 PM

Thanks, ya, always good to sanity check, right ![:slight_smile:](https://discord.com/assets/da3651e59d6006dfa5fa07ec3102d1f3.svg) The BabylonJS shows an unmute button for that and after pressing it I can see the AudioContext is running as before so I don't think that's it.

![👍](https://discord.com/assets/08c0a077780263f3df97613e58e71744.svg)

2

![](https://cdn.discordapp.com/avatars/813082266196377683/41243e9b7a3476acf3d085448169848a.webp?size=256)@docEdub

Thanks, ya, always good to sanity check, right ![:slight_smile:](https://discord.com/assets/da3651e59d6006dfa5fa07ec3102d1f3.svg) The BabylonJS shows an unmute button for that and after pressing it I can see the AudioContext is running as before so I don't think that's it.

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ Yesterday at 7:09 PM

Does Chrome (desktop or Android) play audio with the same memory limits?

![](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)@dpc

Does Chrome (desktop or Android) play audio with the same memory limits?

![ ](https://cdn.discordapp.com/avatars/813082266196377683/41243e9b7a3476acf3d085448169848a.webp?size=256)

## docEdub _—_ Yesterday at 7:54 PM

No, the audio quit playing on all platforms

![👍](https://discord.com/assets/08c0a077780263f3df97613e58e71744.svg)

1

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ Yesterday at 10:22 PM

You could do a binary search on Chrome desktop to find the amount of memory it requires. If it is more than 1GB you need to make that your initial size. But if there's a way to reduce the memory use that would be good

![ ](https://cdn.discordapp.com/avatars/813082266196377683/41243e9b7a3476acf3d085448169848a.webp?size=256)

## docEdub _—_ Yesterday at 10:25 PM

This looks to be an issue with the synthesizer WASM's stack size. I've gotten it to work on Quest 2 browser now by increasing the stack size to 4mb, which is probably way more than it needs but it works! I'm fairly certain that the root cause of the errors I was seeing was due to the stack clobbering the heap.

![👍](https://discord.com/assets/08c0a077780263f3df97613e58e71744.svg)

1

![ ](https://cdn.discordapp.com/avatars/473825134277558284/36b84b0228a0c8e801bddd1557d90a4c.webp?size=256)

## dpc _—_ Yesterday at 10:59 PM

Cool, nice find.

[[Csound]]
[[Software Development]]
[[Oculus]]
[[Quest]]
[[Quest 2]]
[[VR]]
[[WASM]]
[[WebXR]]