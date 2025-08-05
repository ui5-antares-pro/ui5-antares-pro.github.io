# UI5 Antares Pro

[UI5_ANTARES_PRO_URL]: https://ui5-antares-pro.github.io
[UI5_ANTARES_URL]: https://ui5-antares.github.io
[TYPESCRIPT_URL]: https://www.typescriptlang.org
[SAPUI5_URL]: https://sapui5.hana.ondemand.com
[SAPUI5_VERSIONS_URL]: https://sapui5.hana.ondemand.com/versionoverview.html
[UI5_LICENSE_URL]: https://tools.hana.ondemand.com/developer-license-3_2.txt
[UI5_COMPONENT_CONTAINER_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.core.ComponentContainer
[UI5_DIALOG_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.Dialog
[UI5_V2_ODATA_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.model.odata.v2.ODataModel
[UI5_ANTARES_PRO_LICENSE_URL]: https://github.com/hasanciftci26/ui5-antares-pro/blob/master/LICENSE
[NODEJS_URL]: https://nodejs.org
[NPMJS_URL]: https://www.npmjs.com
[UI5_CLI_URL]: https://sap.github.io/ui5-tooling/v4
[UI5_CLI_NPM_URL]: https://www.npmjs.com/package/@ui5/cli
[UI5_TOOLING_URL]: https://www.npmjs.com/package/@sap/ux-ui5-tooling
[APPROUTER_URL]: https://help.sap.com/docs/btp/sap-business-technology-platform/application-router?locale=en-US
[UI5_CDN_URL]: https://ui5.sap.com

!!! info  

	**UI5 Antares Pro** is the successor of the [UI5 Antares][UI5_ANTARES_URL] library, completely rebuilt from the ground up with a renewed code base to ensure higher code quality, better maintainability, and enhanced performance.
	It adds advanced capabilities such as comprehensive navigation handling and improved flexibility for robust SAPUI5 apps.

**UI5 Antares Pro** is a modular [SAPUI5][SAPUI5_URL] library designed to standardize and accelerate the implementation of CRUD operations for OData EntitySets in enterprise applications.

Leveraging the OData model defined in the consuming application, the library dynamically generates UI elements such as dialogs, forms, and tables. Full lifecycle handling is provided, including data binding, submission, and error management. Support is also included for custom validation logic, which can be implemented by the consumer as needed.

!!! danger "Attention" 

	The library currently supports only [sap.ui.model.odata.v2.ODataModel][UI5_V2_ODATA_URL]. Support for OData v4 is not yet available.

## License and Usage Notice

!!! danger "Attention"

	This library leverages standard classes and components provided by the [SAPUI5][SAPUI5_URL] framework without modifying or redistributing SAPUI5 source code. SAPUI5 is licensed under the [SAP Developer License][UI5_LICENSE_URL]. Users of **UI5 Antares Pro** are responsible for reviewing and complying with the terms and conditions of the [SAP Developer License][UI5_LICENSE_URL].

	Careful attention must be paid to the licensing restrictions when integrating **UI5 Antares Pro** in projects that include SAPUI5 dependencies.

	This project is licensed under the Apache License 2.0 - see the [LICENSE][UI5_ANTARES_PRO_LICENSE_URL] file for details.	

## Integration Modes

Two integration modes are supported:

- **Dialog Mode**  
  A ready-to-use [sap.m.Dialog][UI5_DIALOG_URL] is generated with embedded form and table components for rapid deployment.

- **Component Mode**  
  A reusable UI component is exposed, which can be integrated via [sap.ui.core.ComponentContainer][UI5_COMPONENT_CONTAINER_URL]. This allows the consumer to position and style the component freely within the application layout while benefiting from the same functionality.

## Compatibility

UI5 Antares Pro is developed using [TypeScript][TYPESCRIPT_URL] and is fully compatible with both JavaScript-based and TypeScript-based SAPUI5 applications.

## Benefits

UI5 Antares Pro promotes consistency, reusability, and reduced development effort across SAPUI5-based projects, making it a valuable foundation for scalable and maintainable enterprise UI development.

### Core Features

- **Auto Dialog Generation**  
  Automatically generates fully functional dialogs with forms and tables based on OData metadata.

- **Reusable Components**  
  Provides library components that can be integrated flexibly within different UI layouts.

- **ValueList Support**  
  Advanced filter and value help dialogs for improved data selection experience.

- **ValidationLogic Integration**  
  Built-in support for complex validation rules and custom validator functions.

- **Navigation (Association) Handling**  
  Handles 1-N and 1-1 OData associations gracefully with auto-generated tables and navigation properties.

- **Lifecycle Management**  
  Manages data binding, submission, error handling, and UI refresh cycles seamlessly.

- **TypeScript-Based**  
  Developed in TypeScript for improved maintainability and type safety.

## Prerequisites

Before installing and using **UI5 Antares Pro**, ensure that the following tools are available in your development environment:

- **[Node.js][NODEJS_URL]**  
  Required to run the UI5 tooling and package scripts.

- **[npm][NPMJS_URL]** (Node Package Manager)  
  Used for managing dependencies and building the project.

- **[UI5 CLI][UI5_CLI_URL]** (Version 4 or higher)  
  Must be installed either globally or locally in your project.  
  This tool is essential for building and serving SAPUI5 projects using the UI5 Tooling ecosystem.

To verify that all required tools are installed correctly, run the following commands:

```sh
node -v && npm -v
v22.15.0
10.9.2
```

=== "Locally installed UI5 Tooling"

    ```sh
    npx ui5 -v
    4.0.15
    ```

=== "Globally installed UI5 Tooling"

    ```sh
    ui5 -v
    4.0.15
    ```

## Versioning Strategy

**UI5 Antares Pro** adheres to a versioning strategy that aligns closely with officially supported **[SAPUI5][SAPUI5_VERSIONS_URL]** long-term maintenance (LTS) releases. Since the library builds upon and depends on standard SAPUI5 components without any modifications, compatibility is strictly maintained with specific SAPUI5 versions.

### Supported SAPUI5 Versions

The library officially supports the following **SAPUI5 LTS versions**:

- `1.108.x`
- `1.120.x`
- `1.136.x`

While `x` refers to the latest patch available in each version series, it is likely that earlier patch versions within the same major version will also be compatible. However, users are encouraged to validate compatibility in their respective environments.

### Tag-Based Release System

To ensure clarity and flexibility in installation, **UI5 Antares Pro** utilizes **npm dist-tags** to distinguish releases by their target SAPUI5 version. The latest version of the library compatible with each supported SAPUI5 release will be tagged accordingly:

- `ui5-1.108.x-latest`
- `ui5-1.120.x-latest`
- `ui5-1.136.x-latest`

!!! tip "Recommended"

    Always install the library using one of the official tags to ensure alignment with your SAPUI5 runtime version.

    ```sh
    # Example: Install the latest version for SAPUI5 1.136.x
    npm install ui5-antares-pro@ui5-1.136.x-latest
    ```

### Upgrades and Future LTS Support

Whenever SAP releases a new patch within any of the supported versions, **UI5 Antares Pro** will be updated accordingly and published under a new incremental version while preserving the appropriate tag.

When SAP introduces a new LTS version, **UI5 Antares Pro** will evaluate and incorporate support for it, including issuing a corresponding tag (e.g., `ui5-1.148.x-latest`), following the same structured release process.

!!! info "Why this matters"
    This strategy ensures that consumers have precise control over compatibility, stability, and upgrade paths while benefiting from the latest improvements in both SAPUI5 and **UI5 Antares Pro**.

### Version Mapping

The table below shows the relationship between the supported **SAPUI5 LTS versions** and their corresponding **UI5 Antares Pro** release tags:

<table>
  <thead>
    <tr>
      <th>SAPUI5 Version</th>
      <th>UI5 Antares Pro Tag</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>1.108.x</code></td>
      <td><code>ui5-1.108.x-latest</code></td>
      <td>Latest compatible release for 1.108.x</td>
    </tr>
    <tr>
      <td><code>1.120.x</code></td>
      <td><code>ui5-1.120.x-latest</code></td>
      <td>Latest compatible release for 1.120.x</td>
    </tr>
    <tr>
      <td><code>1.136.x</code></td>
      <td><code>ui5-1.136.x-latest</code></td>
      <td>Latest compatible release for 1.136.x</td>
    </tr>
  </tbody>
</table>

!!! tip "Installation Example"

    ```sh
    # Install Antares Pro for SAPUI5 1.120.x
    npm install ui5-antares-pro@ui5-1.120.x-latest
    ```

!!! note "Future Support"

    When SAP releases a new LTS version (e.g., 1.148.x), a corresponding tag (e.g., `ui5-1.148.x-latest`) will be introduced.

## Installation

Follow the steps below to install and configure **UI5 Antares Pro** in your SAPUI5 application.

---

### 1. Install via NPM

Run the following command in the root directory of your UI5 app (where the `package.json` is located):

```sh
npm install ui5-antares-pro@ui5-1.136.x-latest
```

!!! info "Tag Selection"

    Replace `ui5-1.136.x-latest` with the tag that matches your SAPUI5 version. Available tags:
    
    - `ui5-1.136.x-latest`
    - `ui5-1.120.x-latest`
    - `ui5-1.108.x-latest`

---

### 2. Add the Library to `manifest.json` (Dependencies)

Add the library to the `"sap.ui5"."dependencies"."libs"` section:

```json title="manifest.json" hl_lines="11"
{
  ...
  "sap.ui5": {
    ...
    "dependencies": {
      ...
      "libs": {
        "sap.m": {},
        "sap.ui.core": {},
        ...
        "ui5.antares.pro": {}
      }
    }
  }
}
```

---

### 3. Configure Resource Roots

Add the following entry to the `"sap.ui5"."resourceRoots"` section in your `manifest.json`:

```json title="manifest.json" hl_lines="6"
{
  ...
  "sap.ui5": {
    ...
    "resourceRoots": {
      "ui5.antares.pro": "./resources/ui5/antares/pro"
    }
  }
}
```

---

### 4. (Optional) Enable Reuse Components (Component Mode)

If you wish to use the provided reusable components (`create`, `update`, `delete`, `display`), follow these two steps:

#### a. Add Component Dependencies

Include them under `"sap.ui5"."dependencies"."components"`:

```json title="manifest.json"
{
  ...
  "sap.ui5": {
    ...
    "dependencies": {
      ...
      "components": {
        "ui5.antares.pro.v2.component.create": {
          "lazy": false
        },
        "ui5.antares.pro.v2.component.update": {
          "lazy": false
        },
        "ui5.antares.pro.v2.component.delete": {
          "lazy": false
        },
        "ui5.antares.pro.v2.component.display": {
          "lazy": false
        }
      }      
    }
  }
}
```

#### b. Define Component Usages

Add entries under `"sap.ui5"."componentUsages"`:

```json title="manifest.json"
{
  ...
  "sap.ui5": {
    ...
    "componentUsages": {
      "ui5AntaresProCreateEntry": {
        "name": "ui5.antares.pro.v2.component.create"
      },
      "ui5AntaresProUpdateEntry": {
        "name": "ui5.antares.pro.v2.component.update"
      },
      "ui5AntaresProDeleteEntry": {
        "name": "ui5.antares.pro.v2.component.delete"
      },
      "ui5AntaresProDisplayEntry": {
        "name": "ui5.antares.pro.v2.component.display"
      }
    }    
  }
}
```

!!! tip "Component Container Integration"

    The `componentUsages` keys (e.g., `ui5AntaresProCreateEntry`) can be used as the `usage` attribute in the `ComponentContainer`.

---

### 5. Adjust Build Script

To ensure the library is included during the build, add the `--all` flag to your build script in `package.json`:

```json title="package.json" hl_lines="4"
{
  ...
  "scripts": {
    "build": "ui5 build --all --config=ui5.yaml --clean-dest --dest dist"
  }  
}
```

---

### 6. Configure Deployment (ui5-task-zipper)

To ensure the library is included during deployment, set `includeDependencies: true` in your `ui5.yaml` or corresponding build configuration:

```yaml title="ui5-deploy.yaml" hl_lines="7"
...
builder:
  customTasks:
    - name: ui5-task-zipper
      afterTask: generateCachebusterInfo
      configuration:
        includeDependencies: true
```

!!! note

    This configuration is essential for deploying the library alongside your app.

### 7. (Optional) TypeScript Configuration

If your SAPUI5 application is developed using **TypeScript**, you must inform the compiler about the types provided by **UI5 Antares Pro**.  
To do this, add the library to the `"types"` array in your `tsconfig.json` file:

```json title="tsconfig.json" hl_lines="6"
{
  "compilerOptions": {
    ...
    "types": [
      "@sapui5/types", 
      "ui5-antares-pro"
    ]
  }
}
```

This step ensures that TypeScript can correctly resolve type definitions from both SAPUI5 and **UI5 Antares Pro**, enabling type checking, IntelliSense, and autocompletion throughout your project.

### 8. (Optional) BTP Deployment Configuration (`xs-app.json`)

If your application is deployed to the **SAP BTP environment**, it will typically include an `xs-app.json` file to configure route handling for the [Standalone or Managed AppRouter][APPROUTER_URL].

By default, SAP’s UI5 project generator includes the following route in the `routes` section:

```json title="xs-app.json"
{
  "welcomeFile": "/index.html",
  "authenticationMethod": "route",
  "routes": [
    ...
    {
      "source": "^/resources/(.*)$",
      "target": "/resources/$1",
      "authenticationType": "none",
      "destination": "ui5"
    }  
  ]
}
```

This configuration forwards requests to `/resources/` to the **SAPUI5 CDN** via the `ui5` destination.  
However, the **UI5 Antares Pro** library is not hosted on the SAPUI5 CDN — it resides in the **HTML5 Application Repository** of your deployed application.

To make the library available, you must add the following route to the `xs-app.json` of your **UI5 application**:

!!! danger "Attention"

    The route highlighted below must be added before the `/resources/` route which is forwarding requests to the `ui5` destination.

```json title="xs-app.json" hl_lines="6-11"
{
  "welcomeFile": "/index.html",
  "authenticationMethod": "route",
  "routes": [
    ...
    {
      "source": "^/resources/ui5/antares/pro/(.*)$",
      "target": "/resources/ui5/antares/pro/$1",
      "service": "html5-apps-repo-rt",
      "authenticationType": "xsuaa"
    },
    {
      "source": "^/resources/(.*)$",
      "target": "/resources/$1",
      "authenticationType": "none",
      "destination": "ui5"
    },
    {
      "source": "^/test-resources/(.*)$",
      "target": "/test-resources/$1",
      "authenticationType": "none",
      "destination": "ui5"
    },
    {
      "source": "^(.*)$",
      "target": "$1",
      "service": "html5-apps-repo-rt",
      "authenticationType": "xsuaa"
    }      
  ]
}
```

!!! note

    If you're using a **Standalone AppRouter**, ensure this configuration is added to the `xs-app.json` of the **UI5 application itself**, _not_ the AppRouter's `xs-app.json`.

This route ensures that requests for **UI5 Antares Pro** resources are served from the HTML5 repository where the app is deployed.

## Local Testing

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

### Role of the fiori-tools-proxy

The `fiori-tools-proxy` middleware is responsible for forwarding certain request paths to external systems, such as:

- The SAPUI5 CDN (for loading standard UI5 libraries)
- Backend systems (e.g., for OData service calls)

A typical configuration looks like this:

```yaml title="ui5.yaml"
specVersion: "3.1"
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

### The Problem: Custom Library Conflicts with the Proxy

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