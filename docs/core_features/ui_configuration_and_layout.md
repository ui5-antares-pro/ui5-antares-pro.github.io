This section describes the user interface–related configuration options available for the Entry classes — [CreateEntry](../create_entry.md), [UpdateEntry](../update_entry.md), [DeleteEntry](../delete_entry.md), and [DisplayEntry](../display_entry.md).  

These options allow consumers to control various aspects of the generated UI, including dialog titles, button text and behavior, layout structures, and other presentation-related settings.  

Some configuration options may not be applicable to all Entry classes. Such limitations are clearly mentioned in the description of each feature.

Configurations can be applied in two ways:

- **In the constructor** of the Entry class.
- **Via getter/setter methods** through an instance of an Entry class.

!!! note

    All examples in this section use the **CreateEntry** class for demonstration purposes. The same configuration applies to other Entry classes as long as the specific feature is supported.

## Form Position (index)

![number](https://img.shields.io/badge/number-blue?style=flat-square)

By default, the Entry classes place the generated form as the first element within the dialog or embedded component. This position can be adjusted using the **`index`** configuration, allowing consumers to determine where the form should appear in relation to other generated content.

This feature is especially useful when multiple navigation properties are configured, each producing its own table or form inside the same container. Additionally, `ui5.antares.pro.v2.metadata.NavigationProperty` instances can also define an **`index`** to control the placement of their generated content.

<div style="display: flex; gap: 20px; align-items: flex-start;">

  <table>
    <thead>
      <tr>
        <th>Entry Class</th>
        <th>Supported</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><a href="../../create_entry">CreateEntry</a></td>
        <td style="text-align:center;">✅ Yes</td>
      </tr>
      <tr>
        <td><a href="../../update_entry">UpdateEntry</a></td>
        <td style="text-align:center;">✅ Yes</td>
      </tr>
      <tr>
        <td><a href="../../delete_entry">DeleteEntry</a></td>
        <td style="text-align:center;">✅ Yes</td>
      </tr>
      <tr>
        <td><a href="../../display_entry">DisplayEntry</a></td>
        <td style="text-align:center;">✅ Yes</td>
      </tr>
    </tbody>
  </table>

  <table>
    <thead>
      <tr>
        <th>Mode</th>
        <th>Supported</th>
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
          <td style="width: 25%;"><code>getIndex()</code></td>
          <td><code>number</code></td>
          <td>Current index of the generated form; supports negative values to control its position in the dialog or component.</td>
        </tr>
      </tbody>
    </table>

=== "Setter"

    <table>
      <thead>
        <tr>
          <th style="width: 25%;">Method</th>
          <th>Parameter</th>
          <th>Type</th>
          <th>Mandatory</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 25%;"><code>setIndex(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>number</code></td>
          <td>✅ Yes</td>
          <td>Sets the index for the generated form; supports negative values for relative positioning.</td>
        </tr>
      </tbody>
    </table>

### Example

=== "TypeScript"

    ```ts linenums="1" hl_lines="17 22" title="Main.controller.ts"
    import Controller from "sap/ui/core/mvc/Controller";
    import CreateEntry from "ui5/antares/pro/v2/entry/CreateEntry"; // Import the class
    import NavigationProperty from "ui5/antares/pro/v2/metadata/NavigationProperty"; // Import the class

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
                index: 1 // Position the form after the navigation property content
            });
            
            entry.addNavigationProperty(new NavigationProperty({
                name: "toSupplier",
                index: 0 // Position the navigation property content before the main form
            }));
        }
    }
    ```

=== "JavaScript"

    ```js linenums="1" hl_lines="17 22" title="Main.controller.js"
    sap.ui.define([
        "sap/ui/core/mvc/Controller",
        "ui5/antares/pro/v2/entry/CreateEntry", // Import the class
        "ui5/antares/pro/v2/metadata/NavigationProperty" // Import the class
    ], (Controller, CreateEntry, NavigationProperty) => {
        "use strict";

        return Controller.extend("your.apps.namespace.Main", {
            onInit: function () {

            },

            onCreateProduct: async function () {
                const entry = new CreateEntry({
                    controller: this, 
                    entitySet: "Products",
                    index: 1 // Position the form after the navigation property content
                });

                entry.addNavigationProperty(new NavigationProperty({
                    name: "toSupplier",
                    index: 0 // Position the navigation property content before the main form
                }));
            }
        });
    });
    ```

---

## Dialog Title (dialogTitle)

![string](https://img.shields.io/badge/string-blue?style=flat-square)

In dialog mode, the Entry classes generate a dialog with a default title composed of localized text and the associated `EntitySet` name. This default title ensures clarity for end users, but consumers can easily override it using the `dialogTitle` configuration.

This feature is especially useful when the default title is too generic or when you want to provide a more descriptive, user-friendly title in the dialog header.

<div style="display: flex; gap: 20px; align-items: flex-start;">

  <table>
     <thead>
        <tr>
           <th>Entry Class</th>
           <th>Supported</th>
        </tr>
     </thead>
     <tbody>
        <tr>
           <td><a href="../../create_entry">CreateEntry</a></td>
           <td style="text-align:center;">✅ Yes</td>
        </tr>
        <tr>
           <td><a href="../../update_entry">UpdateEntry</a></td>
           <td style="text-align:center;">✅ Yes</td>
        </tr>
        <tr>
           <td><a href="../../delete_entry">DeleteEntry</a></td>
           <td style="text-align:center;">✅ Yes</td>
        </tr>
        <tr>
           <td><a href="../../display_entry">DisplayEntry</a></td>
           <td style="text-align:center;">✅ Yes</td>
        </tr>
     </tbody>
  </table>

  <table>
    <thead>
      <tr>
        <th>Mode</th>
        <th>Supported</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Dialog Mode</td>
        <td style="text-align:center;">✅ Yes</td>
      </tr>
      <tr>
        <td>Component Mode</td>
        <td style="text-align:center;">❌ No</td>
      </tr>
    </tbody>
  </table>  

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
          <td style="width: 25%;"><code>getDialogTitle()</code></td>
          <td><code>string</code></td>
          <td>Returns the current dialog title. If not explicitly set, returns the generated default title.</td>
        </tr>
      </tbody>
    </table>

=== "Setter"

    <table>
      <thead>
        <tr>
          <th style="width: 25%;">Method</th>
          <th>Parameter</th>
          <th>Type</th>
          <th>Mandatory</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 25%;"><code>setDialogTitle(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>string</code></td>
          <td>✅ Yes</td>
          <td>Sets a custom title for the dialog, replacing the generated default title.</td>
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
                dialogTitle: "Create New Product" // Override the default dialog title
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
                    dialogTitle: "Create New Product" // Override the default dialog title
                });
            }
        });
    });
    ```