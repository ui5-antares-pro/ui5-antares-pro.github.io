[UI5_CLI_NPM_URL]: https://www.npmjs.com/package/@ui5/cli
[UI5_TOOLING_URL]: https://www.npmjs.com/package/@sap/ux-ui5-tooling
[UI5_CDN_URL]: https://ui5.sap.com
[UI5_ANTARES_PRO_PROXY_URL]: https://www.npmjs.com/package/ui5-antares-pro-proxy

When developing a SAPUI5 application locally, the **UI5 Antares Pro** library can be loaded and used automatically after completing the standard installation and configuration steps. This is true regardless of whether the application is started using one of the following commands:

- [@ui5/cli][UI5_CLI_NPM_URL]
- [@sap/ux-ui5-tooling][UI5_TOOLING_URL]

=== "@ui5/cli"

    ```sh
    ui5 serve
    ```

=== "@sap/ux-ui5-tooling"

    ```sh
    fiori run
    ```

Both approaches internally compile the application and expose it on a local development server. They also typically rely on a configuration file (e.g., ui5.yaml) located at the root of the project (alongside package.json) to proxy backend and UI5 resource requests.

For applications generated using standard SAP generators (such as easy-ui5, SAP Fiori tools, or the Business Application Studio templates), this configuration file will most likely include the `fiori-tools-proxy` middleware. This middleware handles routing of requests during local development.

---

## Role of the fiori-tools-proxy

The `fiori-tools-proxy` middleware is responsible for forwarding certain request paths to external systems, such as:

- The SAPUI5 CDN (for loading standard UI5 libraries)
- Backend systems (e.g., for OData service calls)

A typical configuration looks like this:

```yaml title="ui5.yaml"
specVersion: "4.0"
metadata:
  name: test.ui5.antares.pro.employeeui
type: application
server:
  customMiddleware:
    - name: fiori-tools-proxy
      afterMiddleware: compression
      configuration:
        ignoreCertError: true
        ui5:
          path:
            - /resources
            - /test-resources
          url: https://ui5.sap.com
        backend:
          - path: /sap
            url: https://backend-system:44300
            client: '200'
```

In this setup:

- All requests to `/resources` and `/test-resources` are forwarded to the SAPUI5 CDN at [https://ui5.sap.com][UI5_CDN_URL].
- All requests to `/sap` are forwarded to the defined backend system.

This setup works perfectly for loading standard SAPUI5 libraries like sap.m, sap.ui.core, etc.

---

## The Problem: Custom Library Conflicts with the Proxy

When the **UI5 Antares Pro** library is added as a dependency and built using ui5 build, its content is emitted into the `/resources` directory. This means that locally, after a successful build, the library is available under:

- **/resources/ui5/antares/pro/**

For example:

- /resources/ui5/antares/pro/library.js
- /resources/ui5/antares/pro/v2/entry/CreateEntry.js
- /resources/ui5/antares/pro/v2/component/create/Component.js

However, due to the way the `fiori-tools-proxy` is configured, all requests to `/resources` are blindly forwarded to the UI5 CDN — including those that actually target the **UI5 Antares Pro** library. This leads to the development server attempting to fetch:

- https://ui5.sap.com/resources/ui5/antares/pro/library.js

…which results in a **404 Not Found** error, because UI5 Antares Pro is a **custom** library and **does not exist on the SAPUI5 CDN**.

This causes the application to break locally since the required library files cannot be resolved, even though they exist within the build output of the project itself.

### Solution 1 (Recommended): Using the UI5 Antares Pro Proxy Package

UI5 Antares Pro provides an additional NPM package designed specifically to enable smooth local testing of SAPUI5 applications that use the library. This package is called **ui5-antares-pro-proxy** and serves as a custom middleware for the UI5 tooling.

The main purpose of this middleware is to take over the **UI5 resource request handling** from the default `fiori-tools-proxy` and ensure that:  

1. **Standard SAPUI5 library requests** are still forwarded to the **SAPUI5 CDN** at [https://ui5.sap.com][UI5_CDN_URL] or custom CDN url that can be configured by the consumer.  
2. **UI5 Antares Pro resources** are always loaded from the **local development environment**, ensuring that the library functions without 404 errors during local development.

!!! danger "Attention"

    While this proxy fully manages the UI5 resource routing, it does **not** provide backend request handling. This means that requests to your backend system (e.g., `/sap/opu/odata/...`) must **still be handled** by the `fiori-tools-proxy` middleware in your `ui5.yaml` configuration.

The **ui5-antares-pro-proxy** middleware is added to the same YAML configuration file that controls the UI5 tooling (ui5 serve or fiori run). It works seamlessly alongside other middleware definitions.

Further installation and configuration instructions for **ui5-antares-pro-proxy** can be found in the official package documentation: [ui5-antares-pro-proxy][UI5_ANTARES_PRO_PROXY_URL]

### Solution 2: Removing the `ui5` Block from `fiori-tools-proxy`

Another possible solution is to remove the `ui5` block from the **fiori-tools-proxy** configuration in the `ui5.yaml` file used by the UI5 tooling (`ui5 serve` or `fiori run`) to run the application.

Once this block is removed, the **fiori-tools-proxy** will automatically load the UI5 resources from [https://ui5.sap.com][UI5_CDN_URL] using the version specified in the `manifest.json` file under:

"sap.ui5" → "dependencies" → "minUI5Version"

**Advantages**

- **Fastest solution** to implement.
- No additional packages or complex configuration required.

**Disadvantages**

- The UI5 CDN URL or the UI5 version **cannot** be changed via the `fiori-tools-proxy` configuration anymore.
- Any change to the UI5 version must be made in the `manifest.json` file instead.

=== "Before"

    ```yaml title="ui5.yaml" hl_lines="11-15"
    specVersion: "4.0"
    metadata:
      name: your.app.name
    type: application
    server:
      customMiddleware:   
        - name: fiori-tools-proxy
          afterMiddleware: compression
          configuration:
            ignoreCertError: true
            ui5:                             # ❌ REMOVE THIS BLOCK
              path:
                - /resources
                - /test-resources
              url: https://ui5.sap.com
            backend:
              - path: /sap
                url: https://your.backend.url
                client: '200'
    ```

=== "After"

    ```yaml title="ui5.yaml"
    specVersion: "4.0"
    metadata:
      name: your.app.name
    type: application
    server:
      customMiddleware:   
        - name: fiori-tools-proxy
          afterMiddleware: compression
          configuration:
            ignoreCertError: true
            backend:
              - path: /sap
                url: https://your.backend.url
                client: '200'
    ```

### Solution 3: Changing the `/resources` path in `ui5` block of `fiori-tools-proxy`

Modify the `/resources` path in the `ui5` block of `fiori-tools-proxy` so that it does not conflict with the UI5 Antares Pro resource path (`/resources/ui5/antares/pro/...`).

This solution requires changes in both `ui5.yaml` and `index.html` files.

=== "Before"

    ```yaml title="ui5.yaml" hl_lines="13"
    specVersion: "4.0"
    metadata:
      name: your.app.name
    type: application
    server:
      customMiddleware:   
        - name: fiori-tools-proxy
          afterMiddleware: compression
          configuration:
            ignoreCertError: true
            ui5:                             
              path:
                - /resources # Change the path
                - /test-resources
              url: https://ui5.sap.com
            backend:
              - path: /sap
                url: https://your.backend.url
                client: '200'
    ```

=== "After"

    ```yaml title="ui5.yaml" hl_lines="13"
    specVersion: "4.0"
    metadata:
      name: your.app.name
    type: application
    server:
      customMiddleware:   
        - name: fiori-tools-proxy
          afterMiddleware: compression
          configuration:
            ignoreCertError: true
            ui5:                             
              path:
                - /ui5-resources
                - /test-resources
              url: https://ui5.sap.com            
            backend:
              - path: /sap
                url: https://your.backend.url
                client: '200'
    ```

Modify the `src` attribute of the script in `index.html` file of your application. The UI5 resources are loaded from the specified address in this attribute. It must match to the path specified in `ui5` block of `fiori-tools-proxy` configuration.

!!! danger "Attention"

    When deploying the application, you must revert the `index.html` change. If not reverted, the deployed app will fail to load UI5 resources because it will attempt to fetch them via the modified path.

=== "Before"

    ```html title="index.html" hl_lines="15"
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <title>Your App</title>
        <style>
            html, body, body > div, #container, #container-uiarea {
                height: 100%;
            }
        </style>
        <script
            id="sap-ui-bootstrap"
            src="resources/sap-ui-core.js" <!-- change the path as in the fiori-tools-proxy configuration -->
            data-sap-ui-theme="sap_horizon"
            data-sap-ui-resourceroots='{
                "your.app.namespace": "./"
            }'
            data-sap-ui-oninit="module:sap/ui/core/ComponentSupport"
            data-sap-ui-compatVersion="edge"
            data-sap-ui-async="true"
            data-sap-ui-frameOptions="trusted"
        ></script>
    </head>
    <body class="sapUiBody sapUiSizeCompact" id="content">
        <div
            data-sap-ui-component
            data-name="your.app.namespace"
            data-id="container"
            data-settings='{"id" : "your.app.namespace"}'
            data-handle-validation="true"
        ></div>
    </body>
    </html>
    ```

=== "After"

    ```html title="index.html" hl_lines="15"
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <title>Your App</title>
        <style>
            html, body, body > div, #container, #container-uiarea {
                height: 100%;
            }
        </style>
        <script
            id="sap-ui-bootstrap"
            src="ui5-resources/sap-ui-core.js"
            data-sap-ui-theme="sap_horizon"
            data-sap-ui-resourceroots='{
                "your.app.namespace": "./"
            }'
            data-sap-ui-oninit="module:sap/ui/core/ComponentSupport"
            data-sap-ui-compatVersion="edge"
            data-sap-ui-async="true"
            data-sap-ui-frameOptions="trusted"
        ></script>
    </head>
    <body class="sapUiBody sapUiSizeCompact" id="content">
        <div
            data-sap-ui-component
            data-name="your.app.namespace"
            data-id="container"
            data-settings='{"id" : "your.app.namespace"}'
            data-handle-validation="true"
        ></div>
    </body>
    </html>
    ```