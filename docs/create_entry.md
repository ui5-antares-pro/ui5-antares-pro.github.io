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
      <td>Instance of the consuming application's controller. Used internally to access models (ODataModel, ResourceModel) and the owner component context.</td>
    </tr>
    <tr>
      <td>entitySet</td>
      <td>string</td>
      <td>✅ Yes</td>
      <td></td>
      <td>Exact name of the OData EntitySet to operate on, as defined in the service metadata. Must not include leading slash.</td>
    </tr>
    <tr>
      <td>modelRef</td>
      <td>string | <a href="https://sapui5.hana.ondemand.com/#/api/sap.ui.model.odata.v2.ODataModel">ODataModel</a></td>
      <td>❌ No</td>
      <td></td>
      <td>Reference to the ODataModel instance or its name in the consuming app. If omitted, defaults to the unnamed ODataModel from the owner component.</td>
    </tr>
    <tr>
      <td>resourceModelRef</td>
      <td>string | <a href="https://sapui5.hana.ondemand.com/#/api/sap.ui.model.resource.ResourceModel">ResourceModel</a></td>
      <td>❌ No</td>
      <td>i18n</td>
      <td>Reference to the resource (i18n) model for label generation, either by name or instance. Defaults to <code>i18n</code> resource model from owner component.</td>
    </tr>
    <tr>
      <td>deferredGroupId</td>
      <td>string</td>
      <td>❌ No</td>
      <td>ui5AntaresPro</td>
      <td>OData deferred batch group ID to be used for create operations, overriding the default <code>ui5AntaresPro</code>.</td>
    </tr>
    <tr>
      <td>index</td>
      <td>number</td>
      <td>❌ No</td>
      <td></td>
      <td>Insertion position index for the generated form within its parent container. Defaults to insertion as the first element if unspecified.</td>
    </tr>
    <tr>
      <td>dialogTitle</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized title</td>
      <td>Overrides the default localized title of the generated dialog with a custom string.</td>
    </tr>
    <tr>
      <td>formType</td>
      <td>FormType</td>
      <td>❌ No</td>
      <td>SmartForm</td>
      <td>Specifies the form variant to generate: <code>SmartForm</code> or <code>SimpleForm</code>. Defaults to <code>SmartForm</code>.</td>
    </tr>
    <tr>
      <td>formTitle</td>
      <td>string</td>
      <td>❌ No</td>
      <td></td>
      <td>Optional title text displayed above the generated form. No title is shown by default.</td>
    </tr>
    <tr>
      <td>submitButtonText</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized text</td>
      <td>Text label for the submit button in the dialog. Defaults to localized standard text.</td>
    </tr>
    <tr>
      <td>submitButtonType</td>
      <td><a href="https://sapui5.hana.ondemand.com/#/api/sap.m.ButtonType">ButtonType</a></td>
      <td>❌ No</td>
      <td>Emphasized</td>
      <td>Visual type of the submit button control. Defaults to <code>Emphasized</code>.</td>
    </tr>
    <tr>
      <td>closeButtonText</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized text</td>
      <td>Text label for the dialog close button. Defaults to localized standard text.</td>
    </tr>
    <tr>
      <td>closeButtonType</td>
      <td><a href="https://sapui5.hana.ondemand.com/#/api/sap.m.ButtonType">ButtonType</a></td>
      <td>❌ No</td>
      <td>Default</td>
      <td>Visual type of the close button control. Defaults to <code>Default</code>.</td>
    </tr>
    <tr>
      <td>keyEnforcementEnabled</td>
      <td>boolean</td>
      <td>❌ No</td>
      <td>true</td>
      <td>If enabled, key properties are enforced by including and positioning them at the top of the form. Disable to exclude or reorder key fields.</td>
    </tr>
    <tr>
      <td>metadataLabelEnabled</td>
      <td>boolean</td>
      <td>❌ No</td>
      <td>false</td>
      <td>Enable automatic label generation from OData metadata annotations (<code>@Common.Text</code>) or <code>sap-label</code> property extensions.</td>
    </tr>
    <tr>
      <td>guidGenerationMode</td>
      <td>GuidMode</td>
      <td>❌ No</td>
      <td>Key</td>
      <td>Determines which <code>Edm.Guid</code> properties receive generated GUID values on entity creation. Options: All, Key, NonKey, None.</td>
    </tr>
    <tr>
      <td>guidVisibilityMode</td>
      <td>GuidMode</td>
      <td>❌ No</td>
      <td>NonKey</td>
      <td>Controls visibility of <code>Edm.Guid</code> properties in the form. Options: All, Key, NonKey, None.</td>
    </tr>
    <tr>
      <td>requiredPropertyError</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized error message</td>
      <td>Custom error message shown when required fields are empty. Triggers on form submission, when the user leaves the input field (focus out), or presses enter. Only applies to <code>SimpleForm</code>. Supports <code>{property}</code> placeholder.</td>
    </tr>
    <tr>
      <td>validationErrorMessage</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized error message</td>
      <td>Error message displayed in a MessageBox when form validation fails on submit.</td>
    </tr>
    <tr>
      <td>selectRowError</td>
      <td>string</td>
      <td>❌ No</td>
      <td>Localized error message</td>
      <td>Message shown when a navigation operation requires row selection but none is selected in the table.</td>
    </tr>
    <tr>
      <td>showErrorMessageBox</td>
      <td>boolean</td>
      <td>❌ No</td>
      <td>true</td>
      <td>Flag to enable or disable display of error MessageBox on submission errors. Defaults to enabled (<code>true</code>).</td>
    </tr>
    <tr>
      <td>booleanFalseByDefault</td>
      <td>boolean</td>
      <td>❌ No</td>
      <td>true</td>
      <td>If true, <code>Edm.Boolean</code> properties default to <code>false</code> on new entities if no initial value is set; otherwise they remain <code>null</code>.</td>
    </tr>
    <tr>
      <td>autoCloseOnSuccess</td>
      <td>boolean</td>
      <td>❌ No</td>
      <td>true</td>
      <td>Determines whether the dialog closes automatically after a successful submission. Defaults to <code>true</code>.</td>
    </tr>
    <tr>
      <td>dateTimeSettings</td>
      <td>DateTimeSettings</td>
      <td>❌ No</td>
      <td></td>
      <td>Configuration allowing consumers to define formatting patterns for date, time, and datetime properties. If not specified, formatting defaults to the user’s locale settings based on OData types.</td>
    </tr>
    <tr>
      <td>numberSettings</td>
      <td>NumberSettings</td>
      <td>❌ No</td>
      <td></td>
      <td>Settings for numeric formatting including decimal separator, grouping separator, grouping size, and grouping enablement.</td>
    </tr>
    <tr>
      <td>contentWrapper</td>
      <td>ContentWrapper</td>
      <td>❌ No</td>
      <td></td>
      <td>Custom layout container wrapping the generated content. Defaults to standard Dialog or VBox container depending on context.</td>
    </tr>
    <tr>
      <td>propertySettings</td>
      <td>PropertySettings[]</td>
      <td>❌ No</td>
      <td></td>
      <td>Array of property-level configurations to mark individual properties as required, read-only, or excluded from the form or table.</td>
    </tr>
    <tr>
      <td>propertyOrder</td>
      <td>string[]</td>
      <td>❌ No</td>
      <td></td>
      <td>Custom sequence of property names to define display order in the form. Properties that are not listed in this array follow the metadata order.</td>
    </tr>
    <tr>
      <td>navigationProperties</td>
      <td>NavigationProperty[]</td>
      <td>❌ No</td>
      <td></td>
      <td>
        Array of navigation property configurations to be included within the generated dialog or component. The library supports both <strong>1:1</strong> and <strong>1:N</strong> cardinalities: for <strong>1:1</strong> associations, it generates an additional form representing the target entity; for <strong>1:N</strong> associations, it creates a table displaying the related entities. Each navigation property should be an instance of <code>ui5.antares.pro.v2.metadata.NavigationProperty</code>, where its specific settings are defined during instantiation.
      </td>
    </tr>
    <tr>
      <td>validationLogics</td>
      <td>ValidationLogic[]</td>
      <td>❌ No</td>
      <td></td>
      <td>
        Collection of validation logic instances executed prior to entity submission to enforce complex business or data integrity rules on user input. Each <code>ui5.antares.pro.v2.validation.ValidationLogic</code> instance encapsulates a particular validation rule, configured via its constructor. This enables modular, reusable, and composable validation checks that minimize data entry errors and improve UX consistency.
      </td>
    </tr>
    <tr>
      <td>valueLists</td>
      <td>ValueList[]</td>
      <td>❌ No</td>
      <td></td>
      <td>
        Definitions of value help dialogs applied to <code>Edm.String</code> or <code>Edm.Guid</code> typed properties. Managed through instances of the <code>ui5.antares.pro.v2.valuelist.ValueList</code> class, consumers specify the target entity set for lookup, properties to display, and filter/search behavior. The library internally manages selection and filtering logic based on this configuration, providing consistent and flexible value help UI integration.
      </td>
    </tr>
    <tr>
      <td>formLayout</td>
      <td>FormLayout</td>
      <td>❌ No</td>
      <td></td>
      <td>
        Enables overriding the default form layout used within the generated dialog or component. By default, a standard form layout is applied; specifying a custom <code>FormLayout</code> instance allows consumers to define alternate visual structures and arrangement of form elements, facilitating tailored UX designs to meet specific project requirements.
      </td>
    </tr>
    <tr>
      <td>customElements</td>
      <td>CustomElement[]</td>
      <td>❌ No</td>
      <td></td>
      <td>
        Allows the injection of custom SAPUI5 controls to replace the default controls generated automatically for specific entity properties. Each <code>ui5.antares.pro.v2.custom.CustomElement</code> instance specifies the property to override and the control to insert (e.g., a slider instead of an input field). When provided, the library skips default generation for that property, enabling advanced UI customization while maintaining integration with the form lifecycle.
      </td>
    </tr>
    <tr>
      <td>customContents</td>
      <td>CustomContent[]</td>
      <td>❌ No</td>
      <td></td>
      <td>
        Additional custom SAPUI5 controls to be added anywhere within the generated dialog or component's UI. These controls must be wrapped in <code>ui5.antares.pro.v2.custom.CustomContent</code> instances, which specify placement and grouping. The consumer is responsible for managing the lifecycle, event handling, and behavior of these controls. The library solely handles positioning, allowing flexible extension of the generated UI without losing control over custom elements.
      </td>
    </tr>    
  </tbody>
</table>

