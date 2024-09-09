# Custom Page Loading Indicator <!-- omit in toc -->

A subtle animation at the bottom of the page just above the footer element indicates to the user that the page is busy fetching data from a database or web service. This repo allows you to customise the standard loader bar, use a spinner from the library of [Spinners](https://github.com/stadium-software/spinners) or define a custom loader in CSS. 

https://github.com/user-attachments/assets/39fa9bca-d127-43f4-accc-10275cce312d

# Version
Initial 1.0

# Setup

## Application Setup
1. Check the *Enable Style Sheet* checkbox in the application properties

## Global Script
1. Create a Global Script called "PageLoader"
2. Add the input parameters below to the Global Script
   1. Type
3. Drag a *JavaScript* action into the script
4. Add the Javascript below into the JavaScript code property
```javascript
/* Stadium Script v1.0 https://github.com/stadium-software/page-loader */
let classname = ~.Parameters.Input.Type;
if (!classname) { 
    console.error("The 'Type' parameter is required");
    return false;
}
let container = document.querySelector("#busy-indicator");
let indicator = container.querySelector(".busy-indicator");
let inner = indicator.querySelector(".busy-indicator-inner");
if (!inner) {
    inner = document.createElement("div");
} else {
    inner.setAttribute("class", "");
}
container.classList.remove("stadium-spinner");
if (classname.startsWith("spinner-type-")) container.classList.add("stadium-spinner");
inner.classList.add("busy-indicator-inner", classname);
indicator.appendChild(inner);
container.appendChild(indicator);
```

## Page.Load
1. Drag the "PageLoader" script into the **first position (!!)** in the Page.Load event handler
2. Provide a value for the script *Type* input parameter
   1. page-loader-classic-bar (or just 'classic-bar'): Customise the standard Stadium bar loader
   2. page-loader-icon: Add an animated icon (or choose one from the [list below](#icons)) and place it somewhere on the screen
   3. page-loader-custom: Animate your own icon
   4. spinner-type-X: [Use any Spinner](#using-a-spinner) from the [Spinners](https://github.com/stadium-software/spinners) repo (see [Using a Spinner](#using-a-spinner))
3. Use the variables in the [*page-loader-variables.css*](page-loader-variables.css) file to customise the loader ([see below](#page-loader-customisations))

## CSS
The CSS below is required for the correct functioning of the module. Some elements can be [customised](#customising-css) using a variables CSS file. 

1. Create a folder called "CSS" inside of your Embedded Files in your application
2. Drag the two CSS files from this repo [*page-loader-variables.css*](page-loader-variables.css) and [*page-loader.css*](page-loader.css) into that folder
3. Paste the link tags below into the *head* property of your application
```html
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/page-loader.css">
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/page-loader-variables.css">
``` 

### CSS Upgrading
To upgrade the CSS in this module, follow the [steps outlined in this repo](https://github.com/stadium-software/samples-upgrading)

## Page Loader Customisations
1. Open the CSS file called [*page-loader-variables.css*](page-loader-variables.css) from this repo
2. Adjust the variables in the *:root* element as you see fit
3. Overwrite the file in the CSS folder of your application with the customised file

## Icons
Use any of these icons to customise the 'page-loader-icon' or the 'page-loader-custom' option ([see above](#pageload)). Alternatively, [create your own base64 encoded image](#base64-encoded-images)

<img src="icons/icon-84.svg">

```css
url("data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwLjI0OSAwLjAwNDUgNTQuMzk0OSA0NS43MjI2IiB3aWR0aD0iNTQuMzk1IiBoZWlnaHQ9IjQ1LjcyMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4NCjxzdHlsZT4NCgkJI3RvcCB7DQoJCQlhbmltYXRpb246IGNvbG9yMSAxcyBpbmZpbml0ZSBsaW5lYXI7DQoJCX0NCgkJI21pZGRsZSB7DQoJCQlhbmltYXRpb246IGNvbG9yMiAxcyBpbmZpbml0ZSBsaW5lYXI7DQoJCX0NCgkJI2JvdHRvbSB7DQoJCQlhbmltYXRpb246IGNvbG9yMyAxcyBpbmZpbml0ZSBsaW5lYXI7DQoJCX0NCgkJQGtleWZyYW1lcyBjb2xvcjEgew0KCQkgIDAlIHsNCgkJCWZpbGw6I2ZmZmZmZjsNCgkJICB9DQoJCSAgMzMlIHsNCgkJCWZpbGw6I2RkZGRkZDsNCgkJICB9DQoJCSAgNjYlIHsNCgkJCWZpbGw6IzE4MTgxODsNCgkJICB9DQoJCSAgMTAwJSB7DQoJCQlmaWxsOiNmZmZmZmY7DQoJCSAgfQ0KCQl9DQoJCUBrZXlmcmFtZXMgY29sb3IyIHsNCgkJICAwJSB7DQoJCQlmaWxsOiNkZGRkZGQ7DQoJCSAgfQ0KCQkgIDMzJSB7DQoJCQlmaWxsOiMxODE4MTg7DQoJCSAgfQ0KCQkgIDY2JSB7DQoJCQlmaWxsOiNmZmZmZmY7DQoJCSAgfQ0KCQkgIDEwMCUgew0KCQkJZmlsbDojZGRkZGRkOw0KCQkgIH0NCgkJfQ0KCQlAa2V5ZnJhbWVzIGNvbG9yMyB7DQoJCSAgMCUgew0KCQkJZmlsbDojMTgxODE4Ow0KCQkgIH0NCgkJICAzMyUgew0KCQkJZmlsbDojZmZmZmZmOw0KCQkgIH0NCgkJICA2NiUgew0KCQkJZmlsbDojZGRkZGRkOw0KCQkgIH0NCgkJICAxMDAlIHsNCgkJCWZpbGw6IzE4MTgxODsNCgkJICB9DQoJCX0NCgk8L3N0eWxlPg0KICA8cGF0aCBpZD0ibWlkZGxlIiBmaWxsPSIjZGRkZGRkIiBkPSJNIDU0LjYzNyAyOC43NjMgTCA1NC42MzcgMTYuNjc5IEMgNTQuNjM3IDEzLjI0OCA1MS44NjYgMTEuNzQ2IDUxLjg2NiAxMS43NDYgQyA1MS44NjYgMTEuNzQ2IDUyLjc3IDEyLjI1NyA1Mi43NyAxMy4yMDUgQyA1Mi43NyAxNC4xNTQgNTEuOCAxNC43MTUgNTEuOCAxNC43MTUgTCAzNy4wNjcgMjIuNzc2IEwgMzcuMDY3IDIyLjk2NSBMIDUxLjcwNiAzMC45MjQgQyA1Mi44MjMgMzEuNTQ5IDUyLjc3MSAzMi40MzYgNTIuNzcxIDMyLjQzNiBDIDUyLjc3MSAzMy4zNSA1MS43MDYgMzQuMDk4IDUxLjcwNiAzNC4wOTggQyA1NC45MyAzMi4wMTQgNTQuNjM3IDI4Ljc2MyA1NC42MzcgMjguNzYzIiBzdHlsZT0iYW5pbWF0aW9uLWR1cmF0aW9uOiAxczsgYW5pbWF0aW9uLWl0ZXJhdGlvbi1jb3VudDogaW5maW5pdGU7IGFuaW1hdGlvbi1uYW1lOiBjb2xvcjI7IGFuaW1hdGlvbi10aW1pbmctZnVuY3Rpb246IGxpbmVhcjsiLz4NCiAgPHBhdGggaWQ9InRvcCIgZmlsbD0iI2ZmZmZmZiIgZD0iTSAzNy4wNyAyMi44NzMgTCA1LjA0OSA1LjQwMyBDIDUuMDQ5IDUuNDAzIDAuNDg5IDMuMDUzIDAuMjQ5IDAuMDEzIEwgMjMuODU5IDAuMDEzIEMgMjMuODU5IDAuMDEzIDI3LjM4OSAtMC4wOTcgMjkuODE3IDAuNDczIEMgMjkuODE3IDAuNDczIDMyLjEyOSAwLjkwMyAzMy44MTcgMS44MjMgTCA1MS41MDcgMTEuNDkzIEMgNTEuNTA3IDExLjQ5MyA1Mi44OTcgMTIuMTczIDUyLjg5NyAxMy4zMDMgQyA1Mi44OTkgMTMuMzAzIDUzLjAyOCAxNC4xODMgNTEuNTA4IDE1LjAxMyBDIDUwLjAzOCAxNS44MjUgMzcuOTMyIDIyLjQwNCAzNy4xMTIgMjIuODQ5IiBzdHlsZT0iYW5pbWF0aW9uLWR1cmF0aW9uOiAxczsgYW5pbWF0aW9uLWl0ZXJhdGlvbi1jb3VudDogaW5maW5pdGU7IGFuaW1hdGlvbi1uYW1lOiBjb2xvcjE7IGFuaW1hdGlvbi10aW1pbmctZnVuY3Rpb246IGxpbmVhcjsiLz4NCiAgPHBhdGggaWQ9ImJvdHRvbSIgZmlsbD0iIzE4MTgxOCIgZD0iTSAzNy4wNjYgMjIuODczIEMgMzcuMDY2IDIyLjg3MyA0OS45ODIgMjkuODk0IDUxLjUwNSAzMC43MjcgQyA1My4wMjggMzEuNTU3IDUyLjg5IDMyLjQzOCA1Mi44OSAzMi40MzggQyA1Mi44OSAzMy41NjEgNTEuNTA1IDM0LjI1IDUxLjUwNSAzNC4yNSBMIDMzLjgxNiA0My45MTEgQyAzMi4xMyA0NC44MzEgMjkuODIgNDUuMjY1IDI5LjgyIDQ1LjI2NSBDIDI3LjM4OCA0NS44MyAyMy44NTMgNDUuNzE4IDIzLjg1MyA0NS43MTggTCAwLjI1IDQ1LjcxOCBDIDAuNDkxIDQyLjY3OSA1LjA0NCA0MC4zMzMgNS4wNDQgNDAuMzMzIEwgMzcuMDY2IDIyLjg3MyBaIiBzdHlsZT0iYW5pbWF0aW9uLWR1cmF0aW9uOiAxczsgYW5pbWF0aW9uLWl0ZXJhdGlvbi1jb3VudDogaW5maW5pdGU7IGFuaW1hdGlvbi1uYW1lOiBjb2xvcjM7IGFuaW1hdGlvbi10aW1pbmctZnVuY3Rpb246IGxpbmVhcjsiLz4NCjwvc3ZnPg==")
```

<img src="icons/icon-85.svg">

```css
url("data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwLjI0OSAxLjAwNDUgNTQuMzk0OSA0NS43MjI2IiB3aWR0aD0iNTQuMzk1IiBoZWlnaHQ9IjQ1LjcyMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4NCgk8c3R5bGU+DQoJCSN0b3Agew0KCQkJYW5pbWF0aW9uOiBjb2xvcjEgM3MgaW5maW5pdGUgbGluZWFyOw0KCQl9DQoJCSNtaWRkbGUgew0KCQkJYW5pbWF0aW9uOiBjb2xvcjIgM3MgaW5maW5pdGUgbGluZWFyOw0KCQl9DQoJCSNib3R0b20gew0KCQkJYW5pbWF0aW9uOiBjb2xvcjMgM3MgaW5maW5pdGUgbGluZWFyOw0KCQl9DQoJCUBrZXlmcmFtZXMgY29sb3IxIHsNCgkJICAwJSB7DQoJCQlmaWxsOiNGQUI1MEQ7DQoJCSAgfQ0KCQkgIDMzJSB7DQoJCQlmaWxsOiNFQzY4MDc7DQoJCSAgfQ0KCQkgIDY2JSB7DQoJCQlmaWxsOiMwMTAyMDI7DQoJCSAgfQ0KCQkgIDEwMCUgew0KCQkJZmlsbDojRkFCNTBEOw0KCQkgIH0NCgkJfQ0KCQlAa2V5ZnJhbWVzIGNvbG9yMiB7DQoJCSAgMCUgew0KCQkJZmlsbDojRUM2ODA3Ow0KCQkgIH0NCgkJICAzMyUgew0KCQkJZmlsbDojMDEwMjAyOw0KCQkgIH0NCgkJICA2NiUgew0KCQkJZmlsbDojRkFCNTBEOw0KCQkgIH0NCgkJICAxMDAlIHsNCgkJCWZpbGw6I0VDNjgwNzsNCgkJICB9DQoJCX0NCgkJQGtleWZyYW1lcyBjb2xvcjMgew0KCQkgIDAlIHsNCgkJCWZpbGw6IzAxMDIwMjsNCgkJICB9DQoJCSAgMzMlIHsNCgkJCWZpbGw6I0ZBQjUwRDsNCgkJICB9DQoJCSAgNjYlIHsNCgkJCWZpbGw6I0VDNjgwNzsNCgkJICB9DQoJCSAgMTAwJSB7DQoJCQlmaWxsOiMwMTAyMDI7DQoJCSAgfQ0KCQl9DQoJPC9zdHlsZT4NCg0KICA8cGF0aCBpZD0ibWlkZGxlIiBmaWxsPSIjRUM2ODA3IiBkPSJNIDU0LjYzNyAyOS43NjMgTCA1NC42MzcgMTcuNjc5IEMgNTQuNjM3IDE0LjI0OCA1MS44NjYgMTIuNzQ2IDUxLjg2NiAxMi43NDYgQyA1MS44NjYgMTIuNzQ2IDUyLjc3IDEzLjI1NyA1Mi43NyAxNC4yMDUgQyA1Mi43NyAxNS4xNTQgNTEuOCAxNS43MTUgNTEuOCAxNS43MTUgTCAzNy4wNjcgMjMuNzc2IEwgMzcuMDY3IDIzLjk2NSBMIDUxLjcwNiAzMS45MjQgQyA1Mi44MjMgMzIuNTQ5IDUyLjc3MSAzMy40MzYgNTIuNzcxIDMzLjQzNiBDIDUyLjc3MSAzNC4zNSA1MS43MDYgMzUuMDk4IDUxLjcwNiAzNS4wOTggQyA1NC45MyAzMy4wMTQgNTQuNjM3IDI5Ljc2MyA1NC42MzcgMjkuNzYzIiBzdHlsZT0iYW5pbWF0aW9uLWR1cmF0aW9uOiA0czsgYW5pbWF0aW9uLWl0ZXJhdGlvbi1jb3VudDogaW5maW5pdGU7IGFuaW1hdGlvbi1uYW1lOiBjb2xvcjI7IGFuaW1hdGlvbi10aW1pbmctZnVuY3Rpb246IGxpbmVhcjsiLz4NCiAgPHBhdGggaWQ9InRvcCIgZmlsbD0iI0ZBQjUwRCIgZD0iTSAzNy4wNyAyMy44NzMgTCA1LjA0OSA2LjQwMyBDIDUuMDQ5IDYuNDAzIDAuNDg5IDQuMDUzIDAuMjQ5IDEuMDEzIEwgMjMuODU5IDEuMDEzIEMgMjMuODU5IDEuMDEzIDI3LjM4OSAwLjkwMyAyOS44MTcgMS40NzMgQyAyOS44MTcgMS40NzMgMzIuMTI5IDEuOTAzIDMzLjgxNyAyLjgyMyBMIDUxLjUwNyAxMi40OTMgQyA1MS41MDcgMTIuNDkzIDUyLjg5NyAxMy4xNzMgNTIuODk3IDE0LjMwMyBDIDUyLjg5OSAxNC4zMDMgNTMuMDI4IDE1LjE4MyA1MS41MDggMTYuMDEzIEMgNTAuMDM4IDE2LjgyNSAzNy45MzIgMjMuNDA0IDM3LjExMiAyMy44NDkiIHN0eWxlPSJhbmltYXRpb24tZHVyYXRpb246IDRzOyBhbmltYXRpb24taXRlcmF0aW9uLWNvdW50OiBpbmZpbml0ZTsgYW5pbWF0aW9uLW5hbWU6IGNvbG9yMTsgYW5pbWF0aW9uLXRpbWluZy1mdW5jdGlvbjogbGluZWFyOyIvPg0KICA8cGF0aCBpZD0iYm90dG9tIiBmaWxsPSIjMDEwMjAyIiBkPSJNIDM3LjA2NiAyMy44NzMgQyAzNy4wNjYgMjMuODczIDQ5Ljk4MiAzMC44OTQgNTEuNTA1IDMxLjcyNyBDIDUzLjAyOCAzMi41NTcgNTIuODkgMzMuNDM4IDUyLjg5IDMzLjQzOCBDIDUyLjg5IDM0LjU2MSA1MS41MDUgMzUuMjUgNTEuNTA1IDM1LjI1IEwgMzMuODE2IDQ0LjkxMSBDIDMyLjEzIDQ1LjgzMSAyOS44MiA0Ni4yNjUgMjkuODIgNDYuMjY1IEMgMjcuMzg4IDQ2LjgzIDIzLjg1MyA0Ni43MTggMjMuODUzIDQ2LjcxOCBMIDAuMjUgNDYuNzE4IEMgMC40OTEgNDMuNjc5IDUuMDQ0IDQxLjMzMyA1LjA0NCA0MS4zMzMgTCAzNy4wNjYgMjMuODczIFoiIHN0eWxlPSJhbmltYXRpb24tZHVyYXRpb246IDRzOyBhbmltYXRpb24taXRlcmF0aW9uLWNvdW50OiBpbmZpbml0ZTsgYW5pbWF0aW9uLW5hbWU6IGNvbG9yMzsgYW5pbWF0aW9uLXRpbWluZy1mdW5jdGlvbjogbGluZWFyOyIvPg0KPC9zdmc+")
```

## Base64 Encoded Images
To display icons, this module uses Base64 encoded image strings. Using this method has the advantage that images do not have to be included in the application as separate files as they are directly inserted into the CSS stylesheet

**Base64 Encoding**
1. Some icon sites (e.g. https://icones.js.org/collection/all) provide this as a standard download option (select "Data Url" from the option buttons in this example)
2. Any image can also be converted to a Base64 encoded string in a number of sites (e.g. https://base64.guru/ - choose "Data URI" or "CSS Background" from the "Output options" dropdown)

## Using a Spinner
Spinners cover the entire page while any party of it is loading. This makes it very obvious to the users that the page is loading and also prevents them from interacting with the UI. To use a Spinner:

1. Include both [Spinners](https://github.com/stadium-software/spinners) CSS files in the CSS folder in the EmbeddedFiles in your application
2. Paste the link tags below into the *head* property of your application
```html
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/spinners.css">
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/spinners-variables.css">
```
3. Follow the instructions in the [Page.Load](#pageload) section

## Working with Stadium Repos
Stadium Repos are not static. They change as additional features are added and bugs are fixed. Using the right method to work with Stadium Repos allows for upgrading them in a controlled manner. How to use and update application repos is described here 

[Working with Stadium Repos](https://github.com/stadium-software/samples-upgrading)
