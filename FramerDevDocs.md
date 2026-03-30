# Framer Plugin Quick Start

## Overview

Framer Plugins are small apps that interact with the editor. They can manipulate the Canvas, insert images, layers, components, or sync with CMS collections. Plugins can have a UI or run entirely in the background.

### Core Features

* **Nodes:** Add or manipulate layers on the Canvas.
* **Components:** Insert and configure Components.
* **CMS:** Sync programmatically with Collections.
* **Assets:** Insert images, SVGs, and other media.

---

## Installation

```bash
npm create framer-plugin@latest
```

* Follows step-by-step setup.
* For existing projects: install `framer-plugin` manually.

### Running a Plugin

```bash
cd your-plugin
npm run dev
```

* Keeps your plugin in development mode with live updates.
* Ensure Node.js is up-to-date.

### Opening in Framer

* Enable **Developer Tools** in Framer settings.
* Open your plugin via **Plugin → Open Development Plugin**.

---

## Publishing

1. Test functionality, UI, and compatibility.
2. Ensure your icon and name are correct.
3. Run `npm run pack` to generate a `.zip`.
4. Submit via the Marketplace dashboard.

Updating: repeat `npm run pack` and upload the new zip.

---

## Key APIs

### Navigation

* `navigateTo(nodeId)` – Jump to a Canvas node, collection item, or code file.
* `zoomIntoView(nodeId)` – Pan and zoom viewport to focus on a node.

### Plugin UI

* `showUI(options)` – Display plugin window.
* `hideUI()` – Hide the plugin.
* `closePlugin()` – Terminate plugin.
* `notify(message)` – Show a notification.
* `setCloseWarning(enabled)` – Ask confirmation before closing.

### User APIs

* `getCurrentUser()` – Returns info about the interacting user.
* Properties: `id`, `name`, `avatarUrl`, `initials`.

### Code File API

* Create, read, update, and manage code files:

  * `createCodeFile()`, `getCodeFile()`, `getCodeFiles()`
  * `setFileContent()`, `rename()`, `remove()`
  * `subscribeToCodeFiles()` and `subscribeToOpenCodeFile()`

### Canvas / Nodes

* Position: `top`, `left`, `right`, `bottom`, `centerX`, `centerY`
* Size: `width`, `height`, `minWidth`, `minHeight`, `maxWidth`, `maxHeight`
* Layout: `stackDirection`, `stackAlignment`, `stackDistribution`, `gridRowCount`, `gridColumnCount`
* Appearance: `backgroundColor`, `backgroundGradient`, `border`, `borderRadius`, `opacity`
* Interactivity: `locked`, `visible`, `zIndex`, `gesture`, `textTruncation`
* Assets: `imageRendering`, `svg`

### CMS

* `getCollections()` – All collections in the project.
* `getActiveCollection()` – Currently selected collection.
* `getActiveManagedCollection()` – Currently active plugin-managed collection.
* Collections can be managed or unmanaged; APIs are consistent across types.



### **Framer Plugin API – Consolidated Reference**

#### **Collections**

* **getManagedCollections()** – Retrieve Collections managed by the current Plugin.

* **Collection** – User-controlled collection (unmanaged).

  * **addFields()** – Create new fields.
  * **addItems()** – Add items.
  * **getFields()** – Fetch all fields.
  * **getItems()** – Retrieve all items.
  * **managedBy** – Returns manager.
  * **readonly** – Whether collection is read-only.
  * **removeFields()** – Remove fields by ID.
  * **removeItems()** – Remove items by ID.
  * **setAsActive()** – Set as active collection.
  * **setFieldOrder()** – Reorder fields by IDs.
  * **setItemOrder()** – Reorder items by IDs.
  * **slugFieldBasedOn** – ID of field slug is based on.
  * **slugFieldName** – Name of field used as slug.
  * **createCollection()** – Add a new CMS collection.

* **CollectionItem** – CMS item in a collection.

  * **fieldData** – Field values.
  * **id** – Unique item ID.
  * **navigateTo()** – Navigate UI to item.
  * **remove()** – Remove item.
  * **setAttributes()** – Update fields.
  * **slug** – Slug value.

* **EnumField & EnumCase** – Enum types.

  * **addCase()**, **cases**, **setCaseOrder()**.
  * **EnumCase** – ID, name, localized name, remove, setAttributes.

* **ManagedCollection** – Plugin-controlled collection.

  * **createManagedCollection()**, **addItems()**, **getFields()**, **getItemIds()**, **removeItems()**, **setAsActive()**, **setFields()**, **setItemOrder()**.

#### **Localization API**

* **getActiveLocale()**, **getDefaultLocale()**, **getLocales()**, **getLocalizationGroups()**, **setLocalizationData()**.
* **Locale** – code, fallbackLocaleId, id, name, slug.
* **LocalizationGroup** – id, name, sources, statusByLocale, supportsExcludedStatus, type.
* **LocalizationSource** – id, name, type, value, valueByLocale.
* **LocalizationValue** – lastEdited, readonly, status, value, warning.

#### **Settings API**

* Redirects: **addRedirects()**, **getRedirects()**, **removeRedirects()**, **setRedirectOrder()**.
* **Redirect** – expandToAllLocales, from, id, remove(), setAttributes(), to.

#### **Permissions**

* **isAllowedTo()**, **subscribeToIsAllowedTo()**, **useIsAllowedTo()**.

#### **Modes**

* **mode** – Current plugin mode. Available modes:

  * **code**, **image**, **canvas**, **editImage**, **collection**, **localization**, **configureManagedCollection**, **syncManagedCollection**.

#### **Project**

* **getProjectInfo()**, **getPublishInfo()**.

#### **Selection**

* **getSelection()**, **setSelection(nodeIds)**, **subscribeToSelection(callback)**.

#### **Assets**

* **addImage()**, **setImage()**, **uploadImage()**, **uploadImages()**, **uploadFile()**, **uploadFiles()**, **addSvg()**.

#### **Components**

* **addComponentInstance({url, attributes})**, **addDetachedComponentLayers({url, layout, attributes})**.

#### **Text**

* **getText()**, **setText()**, **addText()**, **subscribeToText(callback)**.

#### **Custom Code**

* **setCustomCode(options)**, **getCustomCode()**, **subscribeToCustomCode(callback)**.
* Locations: **headStart**, **headEnd**, **bodyStart**, **bodyEnd**.

#### **Data Storage**

* **getPluginData(key)**, **setPluginData(key, value)**, **getPluginDataKeys()**.

#### **Styles**

* **createColorStyle(attributes)**, **getColorStyle(id)**, **getColorStyles()**, **subscribeToColorStyles(callback)**, **createTextStyle(attributes)**, **getTextStyle(id)**, **getTextStyles()**, **subscribeToTextStyles(callback)**.

#### **Fonts**

* **getFont(family)**, **getFonts()**.

#### **Nodes**

* Low-level node operations:

  * **createFrameNode(attributes)**, **cloneNode(nodeId)**, **removeNode(nodeId)**, **getCanvasRoot()**, **subscribeToCanvasRoot(callback)**, **getNode(nodeId)**, **getParent(nodeId)**, **getChildren(nodeId)**, **getRect(nodeId)**, **setAttributes(nodeId, attributes)**, **setParent(nodeId, parentId)**, **getNodesWithType(type)**, **getNodesWithAttribute(attribute)**, **getNodesWithAttributeSet(attribute)**, **node.navigateTo(opts)**.

#### **Interface & UI**

* **framer.showUI({options})**, **framer.hideUI()**, **framer.closePlugin(message, options)**.
* Notifications: **framer.notify(message, options)**.
* Menus: **framer.setMenu(menu)**, **framer.showContextMenu(menu, options)**.
* Color tokens: `--framer-color-*` variables.
* Dark/Light mode detection via `document.body.dataset.framerTheme`.
* Built-in CSS classes: **framer-button-primary**, **framer-divider**.

#### **Plugin Architecture**

* Runs in iframe, React-based template.
* Floating window by default; can run headless with toast notifications.
* Supports async operations and traits for safe property access.

#### **CMS Plugin Concepts**

* Managed vs unmanaged collections.
* Adding/updating fields and items.
* Reference fields via slugs or IDs.
* Markdown support for formattedText fields.
* Array type supports gallery fields (currently single image).
* Plugin data can store metadata like last sync.

#### **Localization Plugin Concepts**

* Supports localization mode.
* Can read/write Locales, Groups, Sources.
* Supports status toggling and localized content updates during collection updates.




### **Permissions**

* Plugins can only perform actions allowed by the user’s granular project permissions.
* **Recommended APIs:**

  * React: `useIsAllowedTo`
  * Vanilla JS: `subscribeToIsAllowedTo`
* `isAllowedTo` checks permissions but shouldn’t be relied on for reactive state.
* Multiple permissions can be checked simultaneously; methods on class instances can be referenced with `ClassName.method`.
* Attempting a disallowed method throws `FramerPluginError` and shows a toast with required permissions.
* Test permissions by inviting a secondary Framer user to your project.

---

### **Components**

* **Insert Component Instances:**

```js
const instance = await framer.addComponentInstance({ url: "https://framer.com/m/framer/Video.js" })
```

* **Set attributes on instances:**

```js
framer.addComponentInstance({ url, attributes: { width: "900px", height: "600px" } })
```

* **Set component controls:**

```js
selection.setAttributes({ controls: { radius: 10 } })
```

* **Upload images for controls:**

```js
const image = await framer.uploadImage({ image: "https://example.com/image.png", altText: "Alt Text" })
selection.setAttributes({ controls: { image } })
```

* **Detached Layers:**

```js
const frame = await framer.addDetachedComponentLayers({ url, attributes: { title: user.name }, layout: true })
```

* **Module URLs:** Components have unique URLs; remove `@` suffix to always point to the latest version.

---

### **Assets (Images & Files)**

* **Add Images:**

```js
await framer.addImage({ image: "https://example.com/image.png", name: "My image", altText: "Alt description" })
```

* **Set Image on selection:**

```js
await framer.setImage({ image: "https://example.com/image.png", altText: "Alt Description" })
```

* **Upload for later use:**

```js
const image = await framer.uploadImage({ image: "https://example.com/image.png" })
await framer.createFrameNode({ backgroundImage: image })
```

* **SVGs:**

```js
await framer.addSVG({ svg: "<svg>...</svg>", name: "framer.svg" })
```

* **Files:**

```js
const uploadedFile = await framer.uploadFile({ file: "https://example.com/video.mp4", name: "Example Video" })
```

---

### **Styles (Color, Text, Fonts)**

* **Color Styles:**

```js
const colorStyle = await framer.createColorStyle({ name: "My Cool Color", light: "rgba(242,59,57,1)", dark: "rgba(120,22,11,1)" })
```

* **Text Styles:**

```js
const textStyle = await framer.createTextStyle({ name: "Heading", fontSize: "30px", lineHeight: "1.6em" })
```

* **Breakpoints:** Scale text attributes across widths. Max 4 breakpoints.
* **Fonts:** Ensure variants belong to the same family.

```js
const font = await framer.getFont("Open Sans", { weight: 400 })
```

---

### **Nodes**

* **Types:** `FrameNode`, `TextNode`, `SVGNode`, `CodeComponentNode`, `UnknownNode`
* **Selection & Query:**

```js
const selection = await framer.getSelection()
const node = await framer.getNode("some-node-id")
```

* **Traits:** Check node type or support for attributes:
  `isFrameNode`, `isTextNode`, `supportsPosition`, `supportsBackgroundGradient`, etc.
* **Replicas:** Inherit from primary nodes until overridden.
* **Children & Parents:** `getChildren()`, `getParent()`
* **Async handling example:**

```js
const [state, setState] = useState(null)
useEffect(() => {
  let active = true
  async function run() {
    const parentNode = selection[0]
    const [children, parentRect] = await Promise.all([parentNode.getChildren(), parentNode.getRect()])
    setState({ parent: parentNode, child: children[0], parentRect, childRect: await children[0].getRect() })
  }
  run()
  return () => { active = false }
}, [selection])
```

---

### **Data**

* **Store global project data:**

```js
await framer.setPluginData("key", "value")
const data = await framer.getPluginData("key")
```

* **Store data on nodes:**

```js
await node.setPluginData("key", "value")
const keys = await node.getPluginDataKeys()
```

* **Remove data:** Set value to `null` for deletion.
* **User-specific data:** Use `localStorage` or `sessionStorage`; sandboxed per user.




### 1. **OAuth in Framer Plugins**

* Web flows using `window.opener.postMessage` **won’t work** in the Framer desktop app.
* Use a **backend as a temporary token store**. Plugin polls backend with a unique read key.
* **Cloudflare Workers** are perfect: free tier, simple deployment, serverless.

**Steps:**

1. Create developer account and app at your OAuth provider.
2. Get `CLIENT_ID` and `CLIENT_SECRET`.
3. Setup backend:

   * Clone example repo.
   * Set `.dev.vars` with environment variables.
   * Run locally (`npm install` → `npm run bootstrap` → `npm run dev`).
4. Poll backend from your plugin with `readKey`.
5. Store returned tokens in `localStorage`.
6. Make authorized API calls using `Bearer` headers.

**Key tip:** Never commit `CLIENT_SECRET`. Always serve over HTTPS.

---

### 2. **Drag & Drop**

* Use `framer.makeDraggable()` for raw HTML elements.
* Or `Draggable` component for React-friendly setup.
* Supports: `image`, `svg`, `componentInstance`, `detachedComponentLayers`.

Example snippet:

```js
<Draggable data={{ type: "svg", svg: mySVG }}>
  <button onClick={() => framer.addSVG({ svg: mySVG })}>Drag me</button>
</Draggable>
```

---

### 3. **Custom Code**

* Inject scripts via `framer.setCustomCode({ html, location })`.
* Locations: `headStart`, `headEnd`, `bodyStart`, `bodyEnd`.
* Detect if users disabled your code with `framer.getCustomCode()`.

---

### 4. **CORS for Plugins**

* Plugins run on `*.plugins.framercdn.com` domains.
* **Allow both production and version-specific domains**.
* Don’t hardcode version IDs or use `*` with credentials.
* Dynamic origin check:

```js
const PLUGIN_ID = "yourPluginId";

function getCorsHeaders(request) {
  const origin = request.headers.get("origin");
  if (!origin) return {};
  const pattern = new RegExp(`^https://${PLUGIN_ID}(-[a-zA-Z0-9]+)?\\.plugins\\.framercdn\\.com$`);
  if (!pattern.test(origin)) return {};
  return {
    "Access-Control-Allow-Origin": origin,
    "Access-Control-Allow-Methods": "GET, POST, PUT, PATCH, DELETE, OPTIONS",
    "Access-Control-Allow-Headers": "Content-Type, Authorization",
    "Access-Control-Allow-Credentials": "true",
  };
}
```

---

### 5. **Server API**

* Automate Framer project updates from **any server**.
* Uses **WebSockets**, not REST.
* Core methods:

  ```js
  const framer = await connect(projectUrl, process.env.FRAMER_API_KEY);
  const changes = await framer.getChangedPaths();
  const preview = await framer.publish();
  await framer.deploy(preview.deployment.id);
  await framer.disconnect();
  ```
* Useful for syncing Notion, Slack, or REST APIs to Framer CMS automatically.

---

### ⚡ Practical Notes

* **Environment handling:** switch URLs dynamically between `localhost` and production.
* **Token refresh:** implement auto-refresh when OAuth tokens expire.
* **Loading states & error handling:** essential for smooth UX.



### **1. Fetch**

* **Purpose:** Grab dynamic API data and use it in your Framer site without writing a full backend.
* **Use cases:** Location-based content, live inventory, login state, personalized data.
* **Best practice:** If data can be static, stick to the CMS or hardcoded values for SEO; use Fetch only for truly dynamic data.
* **Security:** For API keys, don’t expose them on the frontend—use a small backend (Cloudflare Worker, Val Town) as a proxy.
* **CORS:** Make sure your endpoint allows your Framer site to access it.

---

### **2. Code Components**

* **Purpose:** Extend Framer with React components.
* **Core idea:** Everything is React 18 compatible, live-previewed in the editor.
* **Examples:** Buttons, forms, animated SVGs, canvas rendering.
* **Sharing:** Each component has a unique URL. Add `@framerDisableUnlink` to prevent designers from accidentally unlinking your component.

---

### **3. Auto-Sizing**

* **Purpose:** Let Framer decide component size based on content or let designers set fixed sizes.
* **Settings:** `auto`, `fixed`, `any`, `any-prefer-fixed` (width & height independently).
* **Dynamic sizing:** Use `useLayoutEffect` or `useMeasuredSize` for content-driven layouts.

---

### **4. Property Controls**

* **Purpose:** Let designers tweak props visually in the properties panel.
* **Types:** Boolean, Color, String, Number, Array, Object, File, Date, Enum, Link, Cursor, Padding, Border, BoxShadow, Font, etc.
* **Best practice:** Use `defaultProps` to avoid errors. Hide controls conditionally with a `hidden` function. Add descriptions to explain usage.
* **Complex controls:** Arrays for repeatable content, ComponentInstance for linking components, Object for grouped settings.

---

### **5. Overrides**

* **Purpose:** Temporarily override Layer or Component props with React logic.
* **Current trend:** Many use cases for Overrides are now better served with Fetch or Code Components.

---

### **6. Custom Site Code**

* **Purpose:** Add scripts, HTML, structured data, or tracking across pages.
* **Tip:** Use sparingly—every added script can affect performance.

---

💡 **TL;DR for fast action:**

* **Static content:** use CMS/hardcode.
* **Dynamic content/API:** Fetch via a backend proxy.
* **Custom UI logic:** Code Components.
* **Designer-facing props:** Property Controls.
* **One-off tweaks:** Overrides.
* **Global scripts:** Custom Site Code.

---

If you want, I can make you a **tiny “cheat sheet”** that shows exactly **which Framer feature to use for every real-world scenario**, so you never have to wade through all this documentation again. That will save you a ton of time when building your projects.

Do you want me to make that cheat sheet?







Got it—you’ve basically dumped Framer’s developer docs on Code Components, Overrides, and Fetch. Here’s the concise breakdown and key points you actually need if you’re building dynamic Framer sites or experimenting with custom functionality:

---

### **1. Render Context**

* **`RenderTarget`**: Detect where your component is shown.

  ```ts
  import { RenderTarget } from "framer";
  const isOnCanvas = RenderTarget.current() === RenderTarget.canvas;
  ```
* **`useIsStaticRenderer`**: For animations, ensures component doesn’t animate during export (prevents tiling/Canvas lag).

---

### **2. Localization**

* Use `useLocaleInfo()` to get/set locales.

  ```ts
  const { activeLocale, locales, setLocale } = useLocaleInfo();
  ```
* Typically used with `<select>` or custom UI for switching languages.

---

### **3. Property Controls**

* Let users change props through Framer UI.

  ```ts
  import { addPropertyControls, ControlType } from "framer";
  addPropertyControls(Button, { tint: { type: ControlType.Color } });
  ```

---

### **4. Framer Motion**

* Full `framer-motion` API is available. Import as usual:

  ```ts
  import { motion, animate } from "framer-motion";
  ```

---

### **5. Code Overrides**

* Small functions to modify layers dynamically.
* Must use React 18 patterns (`forwardRef`, etc.)
* **Common use cases**:

  * Custom IDs & data attributes:

    ```ts
    export function withTags(Component) {
      return forwardRef((props, ref) => <Component ref={ref} {...props} id="SomeID" />);
    }
    ```
  * Click tracking:

    ```ts
    export function withButtonTracking(Component) {
      return forwardRef((props, ref) => {
        const handleClick = () => { fetch("api.example.com/tracking/button"); props?.onClick?.(); };
        return <Component ref={ref} {...props} onClick={handleClick} />;
      });
    }
    ```
  * Text replacement:

    ```ts
    export function withText(Component) {
      return forwardRef((props, ref) => <Component ref={ref} {...props} text="Hello World" />);
    }
    ```
  * Counter example:

    ```ts
    import { createStore } from "https://framer.com/m/framer/store.js@^1.0.0";
    const useStore = createStore({ count: 0 });
    ```

---

### **6. Fetch**

* Fetch allows API calls without full backend code.
* Works best for dynamic/personalized data (inventory, location, login state).
* Needs JSON object returns.
* Secure tokens should be handled in a backend worker (Cloudflare Workers, Val Town, Hono).
* Examples:

  * Simple GET endpoint.
  * API wrapper to preprocess data and set CORS headers.

---

### **7. When to Use What**

| Feature          | Use Case                                                     |
| ---------------- | ------------------------------------------------------------ |
| Code Components  | Full interactivity or dynamic UI inside Framer               |
| Code Overrides   | Layer-level tweaks (props, click tracking, text replacement) |
| Fetch            | Pull live or dynamic data from APIs                          |
| Custom Site Code | Tracking scripts, structured data, HTML injection            |
| Plugins          | Extend editor capabilities, automate repetitive tasks        |

---

### **8. Important Tips**

* Don’t override core classes (`className`) unless you merge.
* If building complex logic or apps, go with a **normal React app** instead of forcing Framer.
* State management inside Framer is limited—risk of conflicts with built-in component control.
