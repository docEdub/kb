## Building instructions from Steven Yi's Discord reply (with some fixes) ...
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

---

[[Csound]]
[[Software Development]]
[[WASM]]