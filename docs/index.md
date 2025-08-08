[UI5_ANTARES_URL]: https://ui5-antares.github.io
[SAPUI5_URL]: https://sapui5.hana.ondemand.com
[UI5_V2_ODATA_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.model.odata.v2.ODataModel
[UI5_COMPONENT_CONTAINER_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.core.ComponentContainer
[UI5_DIALOG_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.Dialog
[TYPESCRIPT_URL]: https://www.typescriptlang.org

**UI5 Antares Pro** is a modular [SAPUI5][SAPUI5_URL] library designed to standardize and accelerate the implementation of CRUD operations for OData EntitySets in enterprise applications.

Leveraging the OData model defined in the consuming application, the library dynamically generates UI elements such as dialogs, forms, and tables. Full lifecycle handling is provided, including data binding, submission, and error management. Support is also included for custom validation logic, which can be implemented by the consumer as needed.

!!! danger "Attention" 

	The library currently supports only [sap.ui.model.odata.v2.ODataModel][UI5_V2_ODATA_URL]. Support for OData v4 is not yet available.

!!! info  

	**UI5 Antares Pro** is the successor of the [UI5 Antares][UI5_ANTARES_URL] library, completely rebuilt from the ground up with a renewed code base to ensure higher code quality, better maintainability, and enhanced performance.
	It adds advanced capabilities such as comprehensive navigation handling and improved flexibility for robust SAPUI5 apps.

---

## Integration Modes

Two integration modes are supported:

- **Dialog Mode**  
  A ready-to-use [sap.m.Dialog][UI5_DIALOG_URL] is generated with embedded form and table components for rapid deployment.

- **Component Mode**  
  A reusable UI component is exposed, which can be integrated via [sap.ui.core.ComponentContainer][UI5_COMPONENT_CONTAINER_URL]. This allows the consumer to position and style the component freely within the application layout while benefiting from the same functionality.

---

## Core Features

UI5 Antares Pro promotes consistency, reusability, and reduced development effort across SAPUI5-based projects, making it a valuable foundation for scalable and maintainable enterprise UI development.

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

---

## Compatibility

UI5 Antares Pro is developed using [TypeScript][TYPESCRIPT_URL] and is fully compatible with both JavaScript-based and TypeScript-based SAPUI5 applications.

---

## Change Log

Please see [Change Log](./change_log.md).