[UI5_DIALOG_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.Dialog
[UI5_UICOMPONENT_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.core.UIComponent
[UI5_SMARTFORM_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.comp.smartform.SmartForm
[UI5_SIMPLEFORM_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.layout.form.SimpleForm
[UI5_INPUT_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.Input
[UI5_DATEPICKER_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.DatePicker
[UI5_DATETIMEPICKER_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.DateTimePicker
[UI5_TIMEPICKER_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.TimePicker
[UI5_CHECKBOX_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.CheckBox
[UI5_ODATAV2_URL]: https://sapui5.hana.ondemand.com/#/api/sap.ui.model.odata.v2.ODataModel

## 1. Automatic UI Generation

- **Dynamic Form Creation**  
  Depending on the consumer's configuration, the class auto-generates a fully functional data entry form within either a modal [dialog][UI5_DIALOG_URL] or an embedded [component][UI5_UICOMPONENT_URL].  

- **Support for Different Form Types**  
  Generates either a [SmartForm][UI5_SMARTFORM_URL] (default) or a [SimpleForm][UI5_SIMPLEFORM_URL], accommodating various application needs and complexity levels.

- **Property Control Generation**  
  Automatically creates appropriate UI controls (e.g., [Input][UI5_INPUT_URL], [DatePicker][UI5_DATEPICKER_URL], [CheckBox][UI5_CHECKBOX_URL]) based on the OData metadata of the target entity’s properties, including handling different data types, such as strings, dates, GUIDs, and booleans.

## 2. Navigation Property Support

- **1:1 Navigation Forms**  
  For single-valued navigation properties, the library generates nested forms enabling data input for related entities inline.  

- **1:N Navigation Tables**  
  For collection-valued navigation properties, it generates tables to manage related entities, supporting add, edit, and delete operations on related rows.

## 3. Validation and Required Field Checks

- **Built-in Validation**  
  Enforces required fields and data type correctness (e.g., date formats, GUID validity) before allowing submission.  

- **Custom Validation Logic**  
  Supports integration of user-defined validation rules, providing flexible pre-submission validation strategies.  

- **Error Messaging**  
  Automatically displays validation error messages with localization support and customizable error text.

## 4. Submission Handling

- **Seamless OData Integration**  
  Submits the new entity via the configured [ODataModel][UI5_ODATAV2_URL], leveraging deferred batch groups for optimized server communication.  

- **Robust Error Handling**  
  Displays detailed error messages extracted from OData error responses or fallback defaults, configurable by the consumer.  

- **Event Notifications**  
  Fires events signaling success or failure of submissions, enabling consuming applications to react accordingly.

## 5. Flexible Configuration

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