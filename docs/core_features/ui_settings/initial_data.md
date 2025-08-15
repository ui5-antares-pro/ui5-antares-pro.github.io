This section describes the **initial data–related configuration options** that control the default values assigned to specific property types when an Entry class — [CreateEntry](../../create_entry.md), [UpdateEntry](../../update_entry.md), [DeleteEntry](../../delete_entry.md), and [DisplayEntry](../../display_entry.md) — instance is created.  

These options allow the consumer to define how properties of certain EDM types should be pre-filled if no explicit values are provided in the initial data. This helps prevent unintended `null` values in newly created entities and ensures consistency in default data handling.

Two key behaviors are supported:

- **Guid Generation Mode**  
  Automatically generates random GUID values for properties of type `Edm.Guid` if no value is provided.
  
- **Initial Boolean Values**  
  Sets `false` as the default value for properties of type `Edm.Boolean` if no value is provided. Without this option, such properties would default to `null`.

Configurations can be applied in two ways:

- **In the constructor** of the Entry class.  
- **Via getter/setter methods** through an instance of an Entry class.

!!! note

    All examples in this section use the **CreateEntry** class for demonstration purposes. The same configuration applies to other Entry classes as long as the specific feature is supported.

---

## Guid Generation Mode (guidGenerationMode)

![GuidMode](https://img.shields.io/badge/Type-GuidMode-blue?style=flat-square) 

![Key](https://img.shields.io/badge/Default%20Value-Key-orange?style=flat-square)

Controls the way **Edm.Guid** properties are automatically populated when creating a new entry.

**Supported modes**:

- **All** – Generates random GUID values for all **Edm.Guid** properties.  
- **Key** – Generates random GUID values only for key **Edm.Guid** properties.  
- **NonKey** – Generates random GUID values only for non-key **Edm.Guid** properties.  
- **None** – Does not generate any GUID values automatically (properties will remain `null` unless explicitly set).

!!! note

    - Initial data can only be set by the consumer via the **`run`** method of the Entry class instance or Component instance. If the consumer sets initial data for `Edm.Guid` properties explicitly, the library will not generate any random guid values for those properties. 
    - This feature is **fully supported** by [CreateEntry](../../create_entry.md) but only **partially supported** by [UpdateEntry](../../update_entry.md). In `UpdateEntry`, GUID generation applies **only** when the consumer adds a navigation property with **1:N cardinality**. In this case, the application will generate a table for that navigation property, including a create button for adding child entities to an existing parent entity in update mode.  
    - [DeleteEntry](../../delete_entry.md) and [DisplayEntry](../../display_entry.md) do **not** support this feature.

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
             <td style="text-align:center;">⚠️ Partial</td>
          </tr>
          <tr>
             <td><a href="../../../delete_entry">DeleteEntry</a></td>
             <td style="text-align:center;">❌ No</td>
          </tr>
          <tr>
             <td><a href="../../../display_entry">DisplayEntry</a></td>
             <td style="text-align:center;">❌ No</td>
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
          <td style="width: 30%;"><code>getGuidGenerationMode()</code></td>
          <td><code>GuidMode</code></td>
          <td>Returns the current GUID generation mode for <code>Edm.Guid</code> properties.</td>
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
          <td style="width: 30%;"><code>setGuidGenerationMode(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>GuidMode</code></td>
          <td>✅ Yes</td>
          <td>Sets the GUID generation mode for <code>Edm.Guid</code> properties.</td>
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
      <td>Generate random GUID values for <strong>all</strong> <code>Edm.Guid</code> properties, regardless of whether they are key or non-key fields.</td>
    </tr>
    <tr>
      <td><code>Key</code></td>
      <td>Generate random GUID values only for <strong>key</strong> <code>Edm.Guid</code> properties.</td>
    </tr>
    <tr>
      <td><code>NonKey</code></td>
      <td>Generate random GUID values only for <code>Edm.Guid</code> properties that are <strong>not</strong> keys.</td>
    </tr>
    <tr>
      <td><code>None</code></td>
      <td>Do not generate any GUID values automatically.</td>
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
                guidGenerationMode: "All"
            });

            entry.run(); // Initial data is applied here
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
                    guidGenerationMode: "All"
                });

                entry.run(); // Initial data is applied here
            }
        });
    });
    ```

---

## Initial Boolean Values (booleanFalseByDefault)

![boolean](https://img.shields.io/badge/Type-boolean-blue?style=flat-square) 

![true](https://img.shields.io/badge/Default%20Value-true-orange?style=flat-square)

Specifies whether properties of type **Edm.Boolean** should default to `false` when no value is provided in the initial data.

When enabled (`true`), all **Edm.Boolean** properties without explicitly set values will be initialized with `false` instead of `null`. This ensures more predictable behavior in forms and avoids unintended `null` states.

!!! note

    - Initial data can only be set by the consumer via the **`run`** method of the Entry class instance or Component instance. If the consumer sets initial data for `Edm.Boolean` properties explicitly, the library **will not set** the value `false` for those properties. 
    - This feature is **fully supported** by [CreateEntry](../../create_entry.md) but only **partially supported** by [UpdateEntry](../../update_entry.md). In `UpdateEntry`, initial boolean values apply **only** when the consumer adds a navigation property with **1:N cardinality**. In this case, the application will generate a table for that navigation property, including a create button for adding child entities to an existing parent entity in update mode.  
    - [DeleteEntry](../../delete_entry.md) and [DisplayEntry](../../display_entry.md) do **not** support this feature.

---

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
             <td style="text-align:center;">⚠️ Partial</td>
          </tr>
          <tr>
             <td><a href="../../../delete_entry">DeleteEntry</a></td>
             <td style="text-align:center;">❌ No</td>
          </tr>
          <tr>
             <td><a href="../../../display_entry">DisplayEntry</a></td>
             <td style="text-align:center;">❌ No</td>
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
          <td style="width: 30%;"><code>getBooleanFalseByDefault()</code></td>
          <td><code>boolean</code></td>
          <td>Returns whether **Edm.Boolean** properties default to <code>false</code> in initial data.</td>
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
          <td style="width: 32%;"><code>setBooleanFalseByDefault(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>boolean</code></td>
          <td>✅ Yes</td>
          <td>Sets whether **Edm.Boolean** properties default to <code>false</code> in initial data.</td>
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
                booleanFalseByDefault: false // Library will not set any value for booleans
            });

            entry.run(); // Apply initial data
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
                    booleanFalseByDefault: false // Library will not set any value for booleans
                });

                entry.run(); // Apply initial data
            }
        });
    });
    ```
