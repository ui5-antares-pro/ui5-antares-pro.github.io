# CreateEntry

[SAPUI5_URL]: https://sapui5.hana.ondemand.com
[UI5_SMARTFORM_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.comp.smartform.SmartForm
[UI5_SIMPLEFORM_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.layout.form.SimpleForm
[UI5_INPUT_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.Input
[UI5_DATEPICKER_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.DatePicker
[UI5_DATETIMEPICKER_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.DateTimePicker
[UI5_TIMEPICKER_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.TimePicker
[UI5_TEXT_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.Text
[UI5_CHECKBOX_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.CheckBox
[UI5_DIALOG_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.Dialog
[UI5_UICOMPONENT_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.core.UIComponent
[UI5_ODATAV2_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.model.odata.v2.ODataModel
[UI5_CONTROLLER_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.core.mvc.Controller

## Overview

The **CreateEntry** class provides a comprehensive, configurable, and reusable framework designed to facilitate the creation of new entities within an [SAPUI5][SAPUI5_URL] application leveraging an OData V2 backend service. It acts as the primary entry point for dynamically generating user interfaces centered around form-based data entry and submission.

This class abstracts and automates the complexities typically associated with building creation dialogs or embedded form components. It handles form generation, user input validation, integration of navigation properties, error handling, and submission workflows seamlessly, significantly reducing the need for repetitive boilerplate code in consuming applications.

The design prioritizes **flexibility** and **extensibility**, allowing developers to customize generated UIs extensively through constructor settings and instance methods, while still benefiting from sensible defaults and rich built-in capabilities.

---

## Key Features

### 1. Automatic UI Generation

- **Dynamic Form Creation**  
  Depending on the consumer's configuration, the class auto-generates a fully functional data entry form within either a modal [dialog][UI5_DIALOG_URL] or an embedded [component][UI5_UICOMPONENT_URL].  

- **Support for Different Form Types**  
  Generates either a [SmartForm][UI5_SMARTFORM_URL] (default) or a [SimpleForm][UI5_SIMPLEFORM_URL], accommodating various application needs and complexity levels.

- **Property Control Generation**  
  Automatically creates appropriate UI controls (e.g., [Input][UI5_INPUT_URL], [DatePicker][UI5_DATEPICKER_URL], [CheckBox][UI5_CHECKBOX_URL]) based on the OData metadata of the target entity’s properties, including handling different data types, such as strings, dates, GUIDs, and booleans.

### 2. Navigation Property Support

- **1:1 Navigation Forms**  
  For single-valued navigation properties, the library generates nested forms enabling data input for related entities inline.  

- **1:N Navigation Tables**  
  For collection-valued navigation properties, it generates tables to manage related entities, supporting add, edit, and delete operations on related rows.

### 3. Validation and Required Field Checks

- **Built-in Validation**  
  Enforces required fields and data type correctness (e.g., date formats, GUID validity) before allowing submission.  

- **Custom Validation Logic**  
  Supports integration of user-defined validation rules, providing flexible pre-submission validation strategies.  

- **Error Messaging**  
  Automatically displays validation error messages with localization support and customizable error text.

### 4. Submission Handling

- **Seamless OData Integration**  
  Submits the new entity via the configured [ODataModel][UI5_ODATAV2_URL], leveraging deferred batch groups for optimized server communication.  

- **Robust Error Handling**  
  Displays detailed error messages extracted from OData error responses or fallback defaults, configurable by the consumer.  

- **Event Notifications**  
  Fires events signaling success or failure of submissions, enabling consuming applications to react accordingly.

### 5. Flexible Configuration

- **Entity Set and Model References**  
  Allows specification of the target EntitySet and references to the [ODataModel][UI5_ODATAV2_URL] and resource (i18n) models used in the consumer app.  

- **Form and Dialog Customization**  
  Supports customized titles, button texts, button types, and content insertion indices.  

- **Property-level Settings**  
  Enables fine-grained control over individual property behavior, such as setting fields as required, readonly, or excluded.  

- **GUID Handling Modes**  
  Provides modes for GUID generation and visibility to control how GUID-type properties are treated in the form.  

- **Date, Time, and Number Formatting**  
  Accepts configuration objects to tailor the formatting of date/time and numeric fields according to user locale or custom patterns.  

- **Content Wrapper Injection**  
  Allows injection of custom UI layouts to wrap generated forms and tables, enabling advanced UI composition scenarios.

---

## Intended Use Case

This class is designed primarily for SAPUI5 applications requiring efficient and standardized entity creation dialogs or embedded entry forms bound to an OData V2 service. It is ideal for enterprise-grade applications where reducing manual UI coding effort, ensuring data integrity through validation, and providing a consistent user experience are critical.

By encapsulating the complexity of OData metadata parsing, control generation, validation, and submission workflows, the **CreateEntry** class empowers developers to focus on business logic and user experience enhancements rather than repetitive UI plumbing.

---

## Benefits to Consumers

- **Reduced Development Time**  
  Eliminates repetitive coding tasks for entity creation forms, accelerating development cycles.  

- **Consistency**  
  Ensures uniform behavior and appearance across entity creation workflows within the application.  

- **Extensibility**  
  Offers rich configuration and extensibility points to cater to unique business requirements.  

- **Localization and Accessibility**  
  Supports i18n models for label generation and error messages, enhancing global usability.  

- **Error Resilience**  
  Built-in, configurable error handling and user feedback mechanisms improve application robustness.

## Constructor

To utilize the functionality provided by this class, it is required to instantiate and initialize the corresponding object prior to its use.

<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Type</th>
      <th>Mandatory</th>
      <th>Default Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>controller</td>
      <td><a href="https://sapui5.hana.ondemand.com/#/api/sap.ui.core.mvc.Controller">Controller</a></td>
      <td>✅ Yes</td>
      <td></td>
      <td>A reference to the controller instance of the consumer application. Used internally to access resources like ODataModel, ResourceModel (i18n), and the owner component.</td>
    </tr>
    <tr>
      <td>entitySet</td>
      <td>string</td>
      <td>✅ Yes</td>
      <td></td>
      <td>Name of the EntitySet within the consumer application's OData service. Must not begin with a slash (/).</td>
    </tr>
    <tr>
      <td>modelRef</td>
      <td>string | <a href="https://sapui5.hana.ondemand.com/#/api/sap.ui.model.odata.v2.ODataModel">ODataModel</a></td>
      <td>❌ No</td>
      <td></td>
      <td>Optional reference to the ODataModel used by the consumer app. If omitted, assumes default unnamed ODataModel from the owner component. Can be a string (model name) or an ODataModel instance.</td>
    </tr>
    <tr>
      <td>resourceModelRef</td>
      <td>string | <a href="https://sapui5.hana.ondemand.com/#/api/sap.ui.model.resource.ResourceModel">ResourceModel</a></td>
      <td>❌ No</td>
      <td></td>
      <td>Optional reference to the resource (i18n) model for generating property labels. Defaults to <strong>i18n</strong> resource model from the owner component. Can be string (model name) or ResourceModel instance.</td>
    </tr>
    <tr>
      <td>deferredGroupId</td>
      <td>string</td>
      <td>❌ No</td>
      <td>ui5AntaresPro</td>
      <td>ID of the deferred group used for OData create operations. Overrides the default group ID <strong>ui5AntaresPro</strong>.</td>
    </tr>
    <tr>
      <td>index</td>
      <td>number</td>
      <td>❌ No</td>
      <td></td>
      <td>Index position of the generated form within the containing dialog or component. Default inserts as the first element.</td>
    </tr>
    <tr>
      <td>dialogTitle</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized title</td>
      <td>Custom title for the generated dialog. Overrides the default localized title based on operation.</td>
    </tr>
    <tr>
      <td>formType</td>
      <td>FormType</td>
      <td>❌ No</td>
      <td>SmartForm</td>
      <td>Type of form to generate (SmartForm or SimpleForm). Defaults to SmartForm.</td>
    </tr>
    <tr>
      <td>formTitle</td>
      <td>string</td>
      <td>❌ No</td>
      <td></td>
      <td>Title displayed above the generated form. Defaults to none.</td>
    </tr>
    <tr>
      <td>submitButtonText</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized text</td>
      <td>Text on the submit button in the dialog. Defaults to localized text.</td>
    </tr>
    <tr>
      <td>submitButtonType</td>
      <td><a href="https://sapui5.hana.ondemand.com/#/api/sap.m.ButtonType">ButtonType</a></td>
      <td>❌ No</td>
      <td>Emphasized</td>
      <td>Button type of the submit button. Defaults to Emphasized.</td>
    </tr>
    <tr>
      <td>closeButtonText</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized text</td>
      <td>Text on the close button in the dialog. Defaults to localized text.</td>
    </tr>
    <tr>
      <td>closeButtonType</td>
      <td><a href="https://sapui5.hana.ondemand.com/#/api/sap.m.ButtonType">ButtonType</a></td>
      <td>❌ No</td>
      <td>Default</td>
      <td>Button type of the close button. Defaults to Default.</td>
    </tr>
    <tr>
      <td>keyEnforcementEnabled</td>
      <td>boolean</td>
      <td>❌ No</td>
      <td>true</td>
      <td>Enables enforcement of key properties in the form. If true (default), all key properties are included and positioned on top. Set to false to exclude or reorder keys.</td>
    </tr>
    <tr>
      <td>metadataLabelEnabled</td>
      <td>boolean</td>
      <td>❌ No</td>
      <td>false</td>
      <td>Enables label generation based on OData metadata. If true, extracts labels from <strong>annotations (@Common.Text)</strong> or <strong>sap-label</strong> property extension.</td>
    </tr>
    <tr>
      <td>guidGenerationMode</td>
      <td>GuidMode</td>
      <td>❌ No</td>
      <td>Key</td>
      <td>Controls GUID generation for <code>Edm.Guid</code> properties. Options: All, Key, NonKey, None. Defaults to Key.</td>
    </tr>
    <tr>
      <td>guidVisibilityMode</td>
      <td>GuidMode</td>
      <td>❌ No</td>
      <td>NonKey</td>
      <td>Controls visibility of <code>Edm.Guid</code> properties in form. Options: All, Key, NonKey, None. Defaults to NonKey.</td>
    </tr>
    <tr>
      <td>requiredPropertyError</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized error message</td>
      <td>Custom error message when required fields are missing on submission (only for SimpleForm). Supports <code>{property}</code> placeholder.</td>
    </tr>
    <tr>
      <td>validationErrorMessage</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized error message</td>
      <td>Custom error message for validation failure upon submission in a MessageBox.</td>
    </tr>
    <tr>
      <td>selectRowError</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized error message</td>
      <td>Error message when an operation is attempted without selecting a row in a table for navigation properties.</td>
    </tr>
    <tr>
      <td>showErrorMessageBox</td>
      <td>boolean</td>
      <td>❌ No</td>
      <td>true</td>
      <td>Whether to show an error MessageBox on submission errors. Defaults to true.</td>
    </tr>
    <tr>
      <td>booleanFalseByDefault</td>
      <td>boolean</td>
      <td>❌ No</td>
      <td>true</td>
      <td>If true (default), <code>Edm.Boolean</code> properties initialize to false on new entities if no value set; otherwise null.</td>
    </tr>
    <tr>
      <td>autoCloseOnSuccess</td>
      <td>boolean</td>
      <td>❌ No</td>
      <td>true</td>
      <td>Controls if dialog auto-closes after successful submission. Defaults to true.</td>
    </tr>
    <tr>
      <td>dateTimeSettings</td>
      <td>DateTimeSettings</td>
      <td>❌ No</td>
      <td></td>
      <td>Settings for date, time, and datetime controls formatting patterns, based on OData type mapping and locale.</td>
    </tr>
    <tr>
      <td>numberSettings</td>
      <td>NumberSettings</td>
      <td>❌ No</td>
      <td></td>
      <td>Settings for numeric formatting: decimal separator, grouping separator, grouping size, and grouping enabled flag.</td>
    </tr>
    <tr>
      <td>contentWrapper</td>
      <td>ContentWrapper</td>
      <td>❌ No</td>
      <td></td>
      <td>Custom layout wrapper for generated content. Defaults to Dialog or VBox depending on context.</td>
    </tr>
    <tr>
      <td>propertySettings</td>
      <td>PropertySettings[]</td>
      <td>❌ No</td>
      <td>—</td>
      <td>Entity-specific configuration for individual properties to mark them required, readonly, or excluded from form/table.</td>
    </tr>
    <tr>
      <td>propertyOrder</td>
      <td>string[]</td>
      <td>❌ No</td>
      <td>—</td>
      <td>Custom order for displaying properties in the form. Properties not listed appear afterwards in metadata order.</td>
    </tr>
  </tbody>
</table>
