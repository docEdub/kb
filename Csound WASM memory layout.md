## Notes
Csound uses the LLVM `wasm-ld` linker without the `--stack-first` argument, so the WASM memory is layed out from left to right like so...

```
|  Csound code  |  Plugin code  |  Stack  |  Heap  |
```

The stack and the heap start at the same address with the stack expanding to the left towards the code sections, and the heap expanding to the right into the browser's memory. This is why the stack pointer and the heaper pointer in `Csound/wasm/browser/src/module.js` can both point to the same address. They expand in opposite directions.

The stack can not grow. If it gets too large it overwrites the code sections which is very bad.

The heap is grown automatically by the browser as needed. To make growing the heap take less CPU, use the `maximum` argument when calling `WebAssembly.Memory(...)`.

---

## Links
- [[Oculus Quest WASM memory Discord discussion]]
- [https://github.com/WebAssembly/tool-conventions/DynamicLinking.md](https://github.com/WebAssembly/tool-conventions/blob/08bacbed7d0daff49808370cd93b6a6f0c962d76/DynamicLinking.md)
- https://github.com/rustwasm/team/issues/81
- [https://github.com/llvm-mirror/lld/wasm/Writer.cpp:578](https://github.com/llvm-mirror/lld/blob/9ca9c36542ba3466b42a52cae5166b22c0124bf0/wasm/Writer.cpp#L578-L649)