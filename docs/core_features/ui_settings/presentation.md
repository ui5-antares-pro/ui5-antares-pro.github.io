[UI5_INPUT_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.Input
[UI5_DATEPICKER_URL]: https://sapui5.hana.ondemand.com/#/api/sap.m.DatePicker

This section describes the user interface–related configuration options available for the Entry classes — [CreateEntry](../../create_entry.md), [UpdateEntry](../../update_entry.md), [DeleteEntry](../../delete_entry.md), and [DisplayEntry](../../display_entry.md).  

These options allow consumers to control various aspects of the generated UI, including rendering order, visibilities for properties of `Edm.Guid` type. 

Some configuration options may not be applicable to all Entry classes. Such limitations are clearly mentioned in the description of each feature.

Configurations can be applied in two ways:

- **In the constructor** of the Entry class.
- **Via getter/setter methods** through an instance of an Entry class.

!!! note

    All examples in this section use the **CreateEntry** class for demonstration purposes. The same configuration applies to other Entry classes as long as the specific feature is supported.

---

## Key Enforcement (keyEnforcementEnabled)

![boolean](https://img.shields.io/badge/Type-boolean-blue?style=flat-square)

![true](https://img.shields.io/badge/Default%20Value-true-orange?style=flat-square)

When **`keyEnforcementEnabled`** is set to `true` (default), all key properties defined in the OData metadata are:

1. Always included in the generated form.
2. Automatically positioned at the top of the form.

This ensures that essential identifying fields are always visible and prioritized for the end user.  
If you want to **exclude key properties** or **change their position**, you must explicitly set this flag to `false`.

<div class="responsive-flex" style="display: flex; gap: 50px; align-items: flex-start;">

  <div>
    <h4>Entry Class Availability</h4>
    <table>
       <thead>
          <tr>
             <th>Entry Class</th>
             <th>Available</th>
          </tr>
       </thead>
       <tbody>
          <tr>
             <td><a href="../../../create_entry">CreateEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
          <tr>
             <td><a href="../../../update_entry">UpdateEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
          <tr>
             <td><a href="../../../delete_entry">DeleteEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
          <tr>
             <td><a href="../../../display_entry">DisplayEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
       </tbody>
    </table>
  </div>

  <div>
    <h4>Implementation Mode Availability</h4>
    <table>
      <thead>
        <tr>
          <th>Mode</th>
          <th>Available</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Dialog Mode</td>
          <td style="text-align:center;">✅ Yes</td>
        </tr>
        <tr>
          <td>Component Mode</td>
          <td style="text-align:center;">✅ Yes</td>
        </tr>
      </tbody>
    </table>
  </div>  

</div>

---

=== "Getter"

    <table>
      <thead>
        <tr>
          <th style="width: 30%;">Method</th>
          <th>Returns</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 30%;"><code>getKeyEnforcementEnabled()</code></td>
          <td><code>boolean</code></td>
          <td>Returns whether key enforcement is enabled. Defaults to <code>true</code>.</td>
        </tr>
      </tbody>
    </table>

=== "Setter"

    <table>
      <thead>
        <tr>
          <th style="width: 32%;">Method</th>
          <th>Parameter</th>
          <th>Type</th>
          <th>Mandatory</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 32%;"><code>setKeyEnforcementEnabled(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>boolean</code></td>
          <td>✅ Yes</td>
          <td>Enables or disables the enforcement of key properties in the generated form.</td>
        </tr>
      </tbody>
    </table>

### Example

=== "TypeScript"

    ```ts linenums="1" hl_lines="16" title="Main.controller.ts"
    import Controller from "sap/ui/core/mvc/Controller";
    import CreateEntry from "ui5/antares/pro/v2/entry/CreateEntry"; // Import the class

    /**
     * @namespace your.apps.namespace
     */
    export default class Main extends Controller {
        public onInit() {
        
        }

        public async onCreateProduct() {
            const entry = new CreateEntry({
                controller: this, 
                entitySet: "Products",
                keyEnforcementEnabled: false // Allow excluding or reordering key properties
            });
        }
    }
    ```

=== "JavaScript"

    ```js linenums="1" hl_lines="16" title="Main.controller.js"
    sap.ui.define([
        "sap/ui/core/mvc/Controller",
        "ui5/antares/pro/v2/entry/CreateEntry" // Import the class
    ], (Controller, CreateEntry) => {
        "use strict";

        return Controller.extend("your.apps.namespace.Main", {
            onInit: function () {
            
            },

            onCreateProduct: async function () {
                const entry = new CreateEntry({
                    controller: this, 
                    entitySet: "Products",
                    keyEnforcementEnabled: false // Allow excluding or reordering key properties
                });
            }
        });
    });
    ```

---

## Property Order (propertyOrder)

![string[]](https://img.shields.io/badge/Type-string[]-blue?style=flat-square)

By default, property controls (e.g., [Input][UI5_INPUT_URL], [DatePicker][UI5_DATEPICKER_URL]) are rendered in the order they appear in the OData metadata.  
The **`propertyOrder`** feature allows you to define a custom display sequence by listing property names in the desired order.

The **first** property in the array will be rendered first in the form, followed by the next, and so on.

!!! note

    If [keyEnforcementEnabled](#key-enforcement-keyenforcementenabled) is set to `true`, key properties are always displayed first, regardless of their position in this array.

<div class="responsive-flex" style="display: flex; gap: 50px; align-items: flex-start;">

  <div>
    <h4>Entry Class Availability</h4>
    <table>
       <thead>
          <tr>
             <th>Entry Class</th>
             <th>Available</th>
          </tr>
       </thead>
       <tbody>
          <tr>
             <td><a href="../../../create_entry">CreateEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
          <tr>
             <td><a href="../../../update_entry">UpdateEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
          <tr>
             <td><a href="../../../delete_entry">DeleteEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
          <tr>
             <td><a href="../../../display_entry">DisplayEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
       </tbody>
    </table>
  </div>

  <div>
    <h4>Implementation Mode Availability</h4>
    <table>
      <thead>
        <tr>
          <th>Mode</th>
          <th>Available</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Dialog Mode</td>
          <td style="text-align:center;">✅ Yes</td>
        </tr>
        <tr>
          <td>Component Mode</td>
          <td style="text-align:center;">✅ Yes</td>
        </tr>
      </tbody>
    </table>
  </div>  

</div>

---

=== "Getter"

    <table>
      <thead>
        <tr>
          <th style="width: 25%;">Method</th>
          <th>Returns</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 25%;"><code>getPropertyOrder()</code></td>
          <td><code>string[]</code></td>
          <td>Returns the current property order. If not explicitly set, returns an empty array.</td>
        </tr>
      </tbody>
    </table>

=== "Setter"

    <table>
      <thead>
        <tr>
          <th style="width: 30%;">Method</th>
          <th>Parameter</th>
          <th>Type</th>
          <th>Mandatory</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 30%;"><code>setPropertyOrder(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>string[]</code></td>
          <td>✅ Yes</td>
          <td>Sets a custom property order for rendering fields in the generated form.</td>
        </tr>
      </tbody>
    </table>

### Example

=== "TypeScript"

    ```ts linenums="1" hl_lines="16-20" title="Main.controller.ts"
    import Controller from "sap/ui/core/mvc/Controller";
    import CreateEntry from "ui5/antares/pro/v2/entry/CreateEntry"; // Import the class

    /**
     * @namespace your.apps.namespace
     */
    export default class Main extends Controller {
        public onInit() {
        
        }

        public async onCreateProduct() {
            const entry = new CreateEntry({
                controller: this, 
                entitySet: "Products",
                propertyOrder: [
                    "ProductID",   // First field
                    "ProductName", // Second field
                    "Category"     // Third field
                ]
            });
        }
    }
    ```

=== "JavaScript"

    ```js linenums="1" hl_lines="16-20" title="Main.controller.js"
    sap.ui.define([
        "sap/ui/core/mvc/Controller",
        "ui5/antares/pro/v2/entry/CreateEntry" // Import the class
    ], (Controller, CreateEntry) => {
        "use strict";

        return Controller.extend("your.apps.namespace.Main", {
            onInit: function () {
            
            },

            onCreateProduct: async function () {
                const entry = new CreateEntry({
                    controller: this, 
                    entitySet: "Products",
                    propertyOrder: [
                        "ProductID",   // First field
                        "ProductName", // Second field
                        "Category"     // Third field
                    ]
                });
            }
        });
    });
    ```

---

## Guid Visibility Mode (guidVisibilityMode)

![GuidMode](https://img.shields.io/badge/Type-GuidMode-blue?style=flat-square) 

![NonKey](https://img.shields.io/badge/Default%20Value-NonKey-orange?style=flat-square)

Controls the visibility of properties with **Edm.Guid** type in the generated form.

**Supported modes**:

- **All** – Displays all **Edm.Guid** properties.  
- **Key** – Displays only key **Edm.Guid** properties.  
- **NonKey** – Displays only non-key **Edm.Guid** properties.  
- **None** – Hides all **Edm.Guid** properties.  

!!! note

    If [keyEnforcementEnabled](#key-enforcement-keyenforcementenabled) is set to `true`, all key properties (including **Edm.Guid**) are always displayed first in the form, even if `guidVisibilityMode` is set to hide them.

<div class="responsive-flex" style="display: flex; gap: 50px; align-items: flex-start;">

  <div>
    <h4>Entry Class Availability</h4>
    <table>
       <thead>
          <tr>
             <th>Entry Class</th>
             <th>Available</th>
          </tr>
       </thead>
       <tbody>
          <tr>
             <td><a href="../../../create_entry">CreateEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
          <tr>
             <td><a href="../../../update_entry">UpdateEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
          <tr>
             <td><a href="../../../delete_entry">DeleteEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
          <tr>
             <td><a href="../../../display_entry">DisplayEntry</a></td>
             <td style="text-align:center;">✅ Yes</td>
          </tr>
       </tbody>
    </table>
  </div>

  <div>
    <h4>Implementation Mode Availability</h4>
    <table>
      <thead>
        <tr>
          <th>Mode</th>
          <th>Available</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Dialog Mode</td>
          <td style="text-align:center;">✅ Yes</td>
        </tr>
        <tr>
          <td>Component Mode</td>
          <td style="text-align:center;">✅ Yes</td>
        </tr>
      </tbody>
    </table>
  </div>  

</div>

---

=== "Getter"

    <table>
      <thead>
        <tr>
          <th style="width: 30%;">Method</th>
          <th>Returns</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 30%;"><code>getGuidVisibilityMode()</code></td>
          <td><code>GuidMode</code></td>
          <td>Returns the current visibility mode for **Edm.Guid** properties.</td>
        </tr>
      </tbody>
    </table>

=== "Setter"

    <table>
      <thead>
        <tr>
          <th style="width: 30%;">Method</th>
          <th>Parameter</th>
          <th>Type</th>
          <th>Mandatory</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 30%;"><code>setGuidVisibilityMode(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>GuidMode</code></td>
          <td>✅ Yes</td>
          <td>Sets the visibility mode for **Edm.Guid** properties.</td>
        </tr>
      </tbody>
    </table>

### GuidMode Values

<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>All</code></td>
      <td>Show <strong>all</strong> properties with type <code>Edm.Guid</code>, regardless of whether they are key or non-key fields.</td>
    </tr>
    <tr>
      <td><code>Key</code></td>
      <td>Show only those <code>Edm.Guid</code> properties that are <strong>keys</strong> in the entity.</td>
    </tr>
    <tr>
      <td><code>NonKey</code></td>
      <td>Show only <code>Edm.Guid</code> properties that are <strong>not</strong> keys (e.g., foreign keys, reference IDs).</td>
    </tr>
    <tr>
      <td><code>None</code></td>
      <td>Hide <strong>all</strong> <code>Edm.Guid</code> properties from the generated form.</td>
    </tr>
  </tbody>
</table>

### Example

=== "TypeScript"

    ```ts linenums="1" hl_lines="16" title="Main.controller.ts"
    import Controller from "sap/ui/core/mvc/Controller";
    import CreateEntry from "ui5/antares/pro/v2/entry/CreateEntry"; // Import the class

    /**
     * @namespace your.apps.namespace
     */
    export default class Main extends Controller {
        public onInit() {
        
        }

        public async onCreateProduct() {
            const entry = new CreateEntry({
                controller: this, 
                entitySet: "Products",
                guidVisibilityMode: "All"
            });
        }
    }
    ```

=== "JavaScript"

    ```js linenums="1" hl_lines="16" title="Main.controller.js"
    sap.ui.define([
        "sap/ui/core/mvc/Controller",
        "ui5/antares/pro/v2/entry/CreateEntry" // Import the class
    ], (Controller, CreateEntry) => {
        "use strict";

        return Controller.extend("your.apps.namespace.Main", {
            onInit: function () {
            
            },

            onCreateProduct: async function () {
                const entry = new CreateEntry({
                    controller: this, 
                    entitySet: "Products",
                    guidVisibilityMode: "All"
                });
            }
        });
    });
    ```

---

## Property Settings (propertySettings)

![PropertySettings[]](https://img.shields.io/badge/Type-PropertySettings[]-blue?style=flat-square)

Entity-specific configuration for individual properties belonging to the specified **EntitySet**. This array allows consumers to define property-level behaviors, such as marking fields as **required**, **readonly**, or **excluded** from the generated form or table.

<h4>Entry Class Availability</h4>
<table>
   <thead>
      <tr>
         <th>Property</th>
         <th><a href="../../../create_entry">CreateEntry</a></th>
         <th><a href="../../../update_entry">UpdateEntry</a></th>
         <th><a href="../../../delete_entry">DeleteEntry</a></th>
         <th><a href="../../../display_entry">DisplayEntry</a></th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>label</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
      </tr>
      <tr>
         <td>required</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">❌ No</td>
         <td style="text-align:center;">❌ No</td>
      </tr>
      <tr>
         <td>readonly</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">❌ No</td>
         <td style="text-align:center;">❌ No</td>
      </tr>
      <tr>
         <td>excluded</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
      </tr>
      <tr>
         <td>textInEditModeSource</td>
         <td style="text-align:center;">✅ Yes*</td>
         <td style="text-align:center;">✅ Yes*</td>
         <td style="text-align:center;">❌ No</td>
         <td style="text-align:center;">❌ No</td>
      </tr>
      <tr>
         <td>layoutData</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
         <td style="text-align:center;">✅ Yes</td>
      </tr>
   </tbody>
</table>
<p><small>*Requires <code>formType</code> to be <strong>SmartForm</strong></small></p>

<h4>Implementation Mode Availability</h4>
<table>
   <thead>
      <tr>
         <th>Mode</th>
         <th>Available</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>Dialog Mode</td>
         <td style="text-align:center;">✅ Yes</td>
      </tr>
      <tr>
         <td>Component Mode</td>
         <td style="text-align:center;">✅ Yes</td>
      </tr>
   </tbody>
</table>

### PropertySettings Type

<table>
   <thead>
      <tr>
         <th style="width: 25%;">Property</th>
         <th style="width: 25%;">Type</th>
         <th>Mandatory</th>
         <th>Description</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td style="width: 25%;"><code>name</code></td>
         <td style="width: 25%;"><code>string</code></td>
         <td>✅ Yes</td>
         <td>The technical name of the property in the entity.</td>
      </tr>
      <tr>
         <td style="width: 25%;"><code>label</code></td>
         <td style="width: 25%;"><code>string</code></td>
         <td>❌ No</td>
         <td>Consumer-defined label for the property. If not provided, the library tries to derive it in the following order:<br><br>1. Metadata labels (if <code>metadataLabelEnabled</code> is true in the Entry class).<br>2. ResourceModel (i18n) labels based on naming conventions.<br>3. Generated from the property’s naming style (camelCase, CONSTANT_CASE).</td>
      </tr>
      <tr>
         <td style="width: 25%;"><code>required</code></td>
         <td style="width: 25%;"><code>boolean</code></td>
         <td>❌ No</td>
         <td>Marks the property as required.</td>
      </tr>
      <tr>
         <td style="width: 25%;"><code>readonly</code></td>
         <td style="width: 25%;"><code>boolean</code></td>
         <td>❌ No</td>
         <td>Marks the property as read-only.</td>
      </tr>
      <tr>
         <td style="width: 25%;"><code>excluded</code></td>
         <td style="width: 25%;"><code>boolean</code></td>
         <td>❌ No</td>
         <td>Excludes the property from rendering in the generated UI.</td>
      </tr>
      <tr>
         <td style="width: 25%;"><code>textInEditModeSource</code></td>
         <td style="width: 25%;"><a href="https://sapui5.hana.ondemand.com/#/api/sap.ui.comp.smartfield.TextInEditModeSource">TextInEditModeSource</a></td>
         <td>❌ No</td>
         <td>Source of display text in edit mode. Only applies when <code>formType</code> is <code>SmartForm</code>.</td>
      </tr>
      <tr>
         <td style="width: 25%;"><code>layoutData</code></td>
         <td style="width: 25%;"><a href="https://sapui5.hana.ondemand.com/#/api/sap.ui.core.LayoutData">LayoutData</a></td>
         <td>❌ No</td>
         <td>Layout data applied to the generated control.</td>
      </tr>
   </tbody>
</table>

---

=== "Getter"

    <table>
      <thead>
        <tr>
          <th style="width: 30%;">Method</th>
          <th style="width: 28%;">Returns</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 30%;"><code>getPropertySettings()</code></td>
          <td style="width: 28%;"><code>PropertySettings[]</code></td>
          <td>Returns the current property settings array.</td>
        </tr>
      </tbody>
    </table>

=== "Setter"

    <table>
      <thead>
        <tr>
          <th style="width: 30%;">Method</th>
          <th>Parameter</th>
          <th style="width: 25%;">Type</th>
          <th>Mandatory</th>
          <th style="width: 25%;">Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 30%;"><code>setPropertySettings(newValue)</code></td>
          <td><code>newValue</code></td>
          <td style="width: 25%;"><code>PropertySettings[]</code></td>
          <td>✅ Yes</td>
          <td style="width: 25%;">Sets the property settings for the generated form or table.</td>
        </tr>
      </tbody>
    </table>

### Example

=== "TypeScript"

    ```ts linenums="1" hl_lines="16-20" title="Main.controller.ts"
    import Controller from "sap/ui/core/mvc/Controller";
    import CreateEntry from "ui5/antares/pro/v2/entry/CreateEntry"; // Import the class

    /**
     * @namespace your.apps.namespace
     */
    export default class Main extends Controller {
        public onInit() {
        
        }

        public async onCreateProduct() {
            const entry = new CreateEntry({
                controller: this, 
                entitySet: "Products",
                propertySettings: [
                    { name: "ProductID", required: true },
                    { name: "ProductName", label: "Product Name" },
                    { name: "Category", readonly: true }
                ]
            });
        }
    }
    ```

=== "JavaScript"

    ```js linenums="1" hl_lines="16-20" title="Main.controller.js"
    sap.ui.define([
        "sap/ui/core/mvc/Controller",
        "ui5/antares/pro/v2/entry/CreateEntry" // Import the class
    ], (Controller, CreateEntry) => {
        "use strict";

        return Controller.extend("your.apps.namespace.Main", {
            onInit: function () {
            
            },

            onCreateProduct: async function () {
                const entry = new CreateEntry({
                    controller: this, 
                    entitySet: "Products",
                    propertySettings: [
                        { name: "ProductID", required: true },
                        { name: "ProductName", label: "Product Name" },
                        { name: "Category", readonly: true }
                    ]                    
                });
            }
        });
    });
    ```