## Current build and publish instructions using npm
This works with node 14.16.0 and npm 7.22.0
- Clone Csound from https://github.com/docEdub/csound.git.
	```
	git clone https://github.com/docEdub/csound.git -b webaudio-csound+/docEdub
	```
- Install Node and NPM.
- Install nix. See https://nixos.org/download.html. The curl command works fine on Mac.
- `cd wasm`
- `npm build`
	- Builds the `csound-wasm` module which is libcsound compiled to WASM.
- `npm link`??? I used to do `yarn link` here. Is `npm link` is the same?
- `cd browser`
- `npm link @doc.e.dub/csound-wasm-bin`. (See previous note about `yarn link`).
	- Tells NPM to use the local version of `csound-wasm` rather than the on on npmjs.com.
- `npm run build:release:prod`
- `npm login --publish`
	- U: `doc.e.dub`
	- P: `...........`
	- Email: `andy@docEdub.com`
- `npm publish`

---

I haven't tried it yet, but the old `yarn` commands might work again now that the `npm` version is updated to 7.22.0. `yarn publish` kept failing with something like "Symbolic links are not allowed" but that might have been because of an old version of `npm`???

---

## Old building instructions from Steven Yi's Discord reply (with some fixes) ...
1. download yarn
2. download nix (https://nixos.org/download.html, the curl command works fine on mac)
3. cd wasm
4. yarn build (builds the csound-wasm module, which is just libcsound compiled to wasm)
5. yarn link
6. cd browser
7. yarn link "@csound/wasm-bin" (tells to use the local version of csound-wasm rather than the one on npm)
8. yarn build (build the csound-browser module)

## Notes

- If the `yarn link` command fails in the wasm folder, saying it's already linked and it needs to be unlinked, just delete `~/.yarn/@csound/wasm` and `~/.config/yarn/link/@csound/wasm` from the filesystem instead of trying to figure out where it was linked originally.

- To build a static WASM, change the wasm folder's package.json `build` script to `"build": "bash ./scripts/compile.static.sh",` and find/replace `@csound/wasm-bin/lib/csound.dylib.wasm.z` with `@csound/wasm-bin/lib/csound.wasm.z`.
	- I couldn't get the static build to play any sound for some reason. I didn't investigate because I got the dynamic/plugin version working in the Quest 2 browser.
---

[[Csound]]
[[Software Development]]
[[WASM]]