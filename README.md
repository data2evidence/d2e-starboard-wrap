# 🌯 starboard-wrap
A small library that wraps a Starboard Notebook iframe in the parent webpage.

## What?

A starboard notebook runtime should always run in a sandboxed iFrame on a different domain. This makes sure any code in the notebook can't take over the webpage that contains it.

The webpage talks to the notebook runtime in the iFrame using `postMessage`. This package provides an easy-to-use custom HTML element that facilitates this communication.

## Example

```html
<div id="mount-point"></div>

<script type="module">
    import {StarboardEmbed} from "../dist/index.js"
    const mount = document.querySelector("#mount-point");

    const el = new StarboardEmbed({
        notebookContent: "# %% [javascript]\n3+5\n",
        src: "https://unpkg.com/starboard-notebook@0.9.1/dist/index.html"
    });

    el.style.width = "100%";
    mount.appendChild(el);
</script>
```

Or

```html
<script src="/dist/index.iife.js" defer></script>

<starboard-embed>

<script type="starboard">
# %% [javascript]
3+5
</script>
<iframe src="https://unpkg.com/starboard-notebook@0.9.1/dist/index.html" style="width: 100%"></iframe>

</starboard-embed>
```

> ⚠️ Never use the second approach (the one with the `<script>` tag inside the `starboard-embed` element) for notebooks you did not author yourself! It makes cross site scripting (XSS) trivial. Its intended use is for embedding small notebooks in a blogpost, not for use in applications with user-generated content.

## Changelog

### 0.3.0
* Renamed the custom element to `StarboardEmbed` with HTML tag `starboard-embed`.
* The custom element longer extends `IFrameHTMLElement`, instead it will look for an iframe child node or create one if it doesn't exist. This means that the Safari polyfill is no longer required, and pages containing a notebook in an iframe will load faster as the iframe can start loading before the main page's Javascript has been run.
* You can now embed the notebook's content in a script tag inside the `starboard-embed` element.
* `sendMessage()` function now buffers messages until the notebook ready signal has been received.