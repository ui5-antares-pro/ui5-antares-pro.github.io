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