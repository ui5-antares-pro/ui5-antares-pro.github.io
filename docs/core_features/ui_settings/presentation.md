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