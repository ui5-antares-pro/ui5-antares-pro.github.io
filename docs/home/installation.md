[NODEJS_URL]: https://nodejs.org
[NPMJS_URL]: https://www.npmjs.com
[UI5_CLI_URL]: https://sap.github.io/ui5-tooling/v4
[SAPUI5_VERSIONS_URL]: https://sapui5.hana.ondemand.com/versionoverview.html
[APPROUTER_URL]: https://help.sap.com/docs/btp/sap-business-technology-platform/application-router?locale=en-US

This page provides detailed installation and configuration instructions for the **UI5 Antares Pro** library.

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

- `1.120.x`
- `1.136.x`

While `x` refers to the latest patch available in each version series, it is likely that earlier patch versions within the same major version will also be compatible. However, users are encouraged to validate compatibility in their respective environments.

### Tag-Based Release System

To ensure clarity and flexibility in installation, **UI5 Antares Pro** utilizes **npm dist-tags** to distinguish releases by their target SAPUI5 version. The latest version of the library compatible with each supported SAPUI5 release will be tagged accordingly:

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

## Installation Steps

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