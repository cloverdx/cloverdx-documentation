<!-- Administration > Configuration > Server configuration > Branding of CloverDX Server -->

### Branding of CloverDX Server

**CloverDX Server** offers an option to customize the look and feel of the following pages, allowing you to align them with your organization’s branding:

- **Login** page at `https://[host]/clover/login`
- **Home** page at `https://[host]/clover/home`
- **Data Apps catalog** page at `https://[host]/clover/data-app#/catalog`
- Individual published data apps at `https://[host]/data-app#/app/`

You can modify the following:

- **UI messages**: Customize labels, captions, tooltips, and other user-facing text.
- **CSS styling**: Apply custom styles to alter the appearance.
- **Images**: Replace default images with your own visuals.
- **Additional customization**: Implement advanced modifications using custom JavaScript code.
> [!NOTE]
> For organizations seeking to customize the **CloverDX Server Console** itself (**https://[host]/clover/gui/login.jsf**) to match their branding guidelines, a different approach is required due to the underlying technologies. Contact your CloverDX account manager to discuss whitelabeling and branding options for the **CloverDX Server Console**.

#### Basic branding steps

1. **Download an example branding file**: Obtain a `cloverdx.webapps.branding.{version}.zip` file from the **Other resources** section on the CloverDX support portal: [https://support.cloverdx.com/downloads](https://support.cloverdx.com/downloads).
2. **Edit branding files:** Modify the files within the downloaded `.zip` archive according to your branding needs.
3. **Set configuration property:** Add the [`webapps.branding.resourceFilePath`](list-of-properties.md#lop-dataapp-branding-resourcefilepath) configuration property into the CloverDX configuration file and point it to the path of your edited `.zip` file. Make sure to restart CloverDX Server for the change to take effect.
> [!NOTE]
> On Windows OS, use either forward slashes or double backslashes in the path to the branding file, e.g.:
>
> `webapps.branding.resourceFilePath=C:/path/to/cloverdx.webapps.branding.6.5.0.zip`
>
> `webapps.branding.resourceFilePath=C:\\path\\to\\cloverdx.webapps.branding.6.5.0.zip`

#### Branding file structure

```
--data-apps
   |-- "app.css"
   |-- "app.js"
   |-- "images"
   |-- "messages.json"
--login
   |-- "app.css"
   |-- "app.js"
   |-- "images"
   |-- "messages.json"
|-- "images"
   |-- "favicon.png"
-- "messages.json"
```

#### Resource locations

##### UI messages

Modify the following files to redefine the values of UI messages (labels, captions, tooltips, etc.). Optionally, keep only the modified messages and delete the rest to leverage default messages for unchanged elements.

- `<cloverdx.webapps.branding.zip>/messages.json`: to modify messages globally in **Login**, **Home** and **Data Apps** pages.
- `<cloverdx.webapps.branding.zip>/data-apps/messages.json`: to modify **Data Apps** pages.
- `<cloverdx.webapps.branding.zip>/login/messages.json`: to modify **Login** and **Home** pages.

##### UI styling

Replace the default **favicon** with your custom icon by placing it at:

- `<cloverdx.webapps.branding.zip>/images/favicon.png`

##### CSS styles

Modify or add custom CSS styles:

- `<cloverdx.webapps.branding.zip>/data-app/app.css`: to modify **Data Apps** pages.
- `<cloverdx.webapps.branding.zip>/login/app.css`: to modify **Login** and **Home** pages.

To hide all default images, add the following code to the `app.css` file:

```css
.cloverdx-brand {
   display: none !important;
}
```

##### Images

Add your custom images to:

- `<cloverdx.webapps.branding.zip>/data-app/images`: for images used in **Data Apps** pages.
- `<cloverdx.webapps.branding.zip>/login/images`: for images used in **Login** and **Home** pages.
- `<cloverdx.webapps.branding.zip>/images`: to update the **favicon** image.

These images will be accessible via URLs like:

- `/SERVER_CONTEXT/data-app/resource/branding/data-app/PATH_TO_IMAGE` (e.g., `/clover/data-app/resource/branding/data-app/images/image.png`).
- `/SERVER_CONTEXT/login/resource/branding/login/PATH_TO_IMAGE` (e.g., `/clover/login/resource/branding/login/images/image.png`).

##### Custom JavaScript

Implement complex modifications that go beyond CSS capabilities using custom JavaScript code:

- `<cloverdx.webapps.branding.zip>/data-app/app.js`: to modify **Data Apps** pages.
- `<cloverdx.webapps.branding.zip>/login/app.js`: to modify **Login** and **Home** pages.

For example, the following code will add a custom element (footer) to the bottom of the page:

```js
window.addEventListener("load", function() {
    const dataAppEl = this.document.querySelector(".content");
    const newEl = document.createElement("div");
    newEl.innerHTML = "Copyright © 2024 My Company, All rights reserved.";
    newEl.id = "footer";
    dataAppEl.parentNode.insertBefore(newEl, dataAppEl.nextSibling);
}, false);
```
