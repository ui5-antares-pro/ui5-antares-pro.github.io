This section describes the user interface–related configuration options available for the Entry classes — [CreateEntry](../../create_entry.md), [UpdateEntry](../../update_entry.md), [DeleteEntry](../../delete_entry.md), and [DisplayEntry](../../display_entry.md).  

These options allow consumers to control various aspects of the generated UI, including dialog titles, button text and behavior, and other presentation-related settings.  

Some configuration options may not be applicable to all Entry classes. Such limitations are clearly mentioned in the description of each feature.

Configurations can be applied in two ways:

- **In the constructor** of the Entry class.
- **Via getter/setter methods** through an instance of an Entry class.

!!! note

    All examples in this section use the **CreateEntry** class for demonstration purposes. The same configuration applies to other Entry classes as long as the specific feature is supported.

## Form Position (index)

![number](https://img.shields.io/badge/Type-number-blue?style=flat-square)

By default, the Entry classes place the generated form as the first element within the dialog or embedded component. This position can be adjusted using the **`index`** configuration, allowing consumers to determine where the form should appear in relation to other generated content.

This feature is especially useful when multiple navigation properties are configured, each producing its own table or form inside the same container. Additionally, `ui5.antares.pro.v2.metadata.NavigationProperty` instances can also define an **`index`** to control the placement of their generated content.

<style>
  /* On small screens, stack the divs vertically */
  @media (max-width: 600px) {
    .responsive-flex {
      flex-direction: column !important;
      gap: 0px !important; /* smaller gap for stacked layout */
    }
  }
</style>

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

![string](https://img.shields.io/badge/Type-string-blue?style=flat-square)

![Localized Text](https://img.shields.io/badge/Default%20Value-Localized%20Text-orange?style=flat-square)

In dialog mode, the Entry classes generate a dialog with a default title composed of localized text and the associated `EntitySet` name. This default title ensures clarity for end users, but consumers can easily override it using the `dialogTitle` configuration.

This feature is especially useful when the default title is too generic or when you want to provide a more descriptive, user-friendly title in the dialog header.

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
          <td style="text-align:center;">❌ No</td>
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

---

## Form Title (formTitle)

![string](https://img.shields.io/badge/Type-string-blue?style=flat-square)

The `formTitle` property defines the title displayed above the generated form. By default, no title is shown. This property allows you to set a clear and descriptive heading, improving the visual structure and user experience of the form.

A custom `formTitle` is particularly helpful when forms are part of a larger UI and need to convey context or purpose to the end user.

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
          <th style="width: 25%;">Returns</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 25%;"><code>getFormTitle()</code></td>
          <td style="width: 25%;"><code>string | undefined</code></td>
          <td>Returns the current form title. If no title is set, returns <code>undefined</code>.</td>
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
          <td style="width: 30%;"><code>setFormTitle(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>string</code></td>
          <td>✅ Yes</td>
          <td>Sets a custom title for the form.</td>
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
                formTitle: "Product Details" // Set a custom form title
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
                    formTitle: "Product Details" // Set a custom form title
                });
            }
        });
    });
    ```

---

## Form Type (formType)

![FormType](https://img.shields.io/badge/Type-FormType-blue?style=flat-square)

![SmartForm](https://img.shields.io/badge/Default%20Value-SmartForm-orange?style=flat-square)

Determines the type of form generated for the specified `EntitySet`. 
By default, the library creates a [SmartForm](https://sapui5.hana.ondemand.com/#/api/sap.ui.comp.smartform.SmartForm), which is metadata-driven and supports advanced features such as smart fields, annotations, and automatic OData integration.

This property allows consumers to switch to a [SimpleForm](https://sapui5.hana.ondemand.com/#/api/sap.ui.layout.form.SimpleForm) when a simpler, less metadata-heavy layout is desired. `SimpleForm` offers more control over layout and content, making it suitable for custom UI scenarios or when metadata is incomplete.

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
          <td style="width: 25%;"><code>getFormType()</code></td>
          <td><code>FormType</code></td>
          <td>Returns the current form type. If not explicitly set, returns the default value <code>"SmartForm"</code>.</td>
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
          <td style="width: 25%;"><code>setFormType(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>FormType</code></td>
          <td>✅ Yes</td>
          <td>Sets the type of form to generate. Must be either <code>"SmartForm"</code> or <code>"SimpleForm"</code>.</td>
        </tr>
      </tbody>
    </table>

### FormType Values

<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>SmartForm</code></td>
      <td>Generates a <a href="https://sapui5.hana.ondemand.com/#/api/sap.ui.comp.smartform.SmartForm" target="_blank" rel="noopener">SmartForm</a> using OData metadata to automatically create fields, labels, and layout.</td>
    </tr>
    <tr>
      <td><code>SimpleForm</code></td>
      <td>Generates a <a href="https://sapui5.hana.ondemand.com/#/api/sap.ui.layout.form.SimpleForm" target="_blank" rel="noopener">SimpleForm</a>, offering more flexibility for custom layouts and manual field creation.</td>
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
                formType: "SimpleForm" // Switch to SimpleForm
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
                    formType: "SimpleForm" // Switch to SimpleForm
                });
            }
        });
    });
    ```

---

## Submit Button Text (submitButtonText)

![string](https://img.shields.io/badge/Type-string-blue?style=flat-square)

![Localized Text](https://img.shields.io/badge/Default%20Value-Localized%20Text-orange?style=flat-square)

Text displayed on the submit button within the generated dialog. A default localized text is provided by the library based on the current language. This property allows the consumer to override the button text.

!!! note

    The submit button is not generated when using the **DisplayEntry** class. Additionally, the library **will not generate** any button in the `Component Mode` regardless of which Entry class is utilized.

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
          <td style="text-align:center;">❌ No</td>
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
          <td style="width: 25%;"><code>getSubmitButtonText()</code></td>
          <td><code>string</code></td>
          <td>Returns the current submit button text. If not explicitly set, returns the default localized text.</td>
        </tr>
      </tbody>
    </table>

=== "Setter"

    <table>
      <thead>
        <tr>
          <th style="width: 35%;">Method</th>
          <th>Parameter</th>
          <th>Type</th>
          <th>Mandatory</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 35%;"><code>setSubmitButtonText(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>string</code></td>
          <td>✅ Yes</td>
          <td>Sets a custom text for the submit button, overriding the default localized text.</td>
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
                submitButtonText: "Send Data" // Override the submit button text
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
                    submitButtonText: "Send Data" // Override the submit button text
                });
            }
        });
    });
    ```

---

## Submit Button Type (submitButtonType)

![ButtonType](https://img.shields.io/badge/Type-ButtonType-blue?style=flat-square)

![Emphasized](https://img.shields.io/badge/Default%20Value-Emphasized-orange?style=flat-square)

[Button Type](https://sapui5.hana.ondemand.com/#/api/sap.m.ButtonType) of the submit button in the generated dialog. Defaults to **Emphasized**. This property allows the consumer to configure a different button type.

!!! note

    The submit button is not generated when using the **DisplayEntry** class. Additionally, the library **will not generate** any button in the `Component Mode` regardless of which Entry class is utilized.

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
          <td style="text-align:center;">❌ No</td>
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
          <th style="width: 25%;">Returns</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 25%;"><code>getSubmitButtonType()</code></td>
          <td style="width: 25%;"><a href="https://sapui5.hana.ondemand.com/#/api/sap.m.ButtonType">ButtonType</a></td>
          <td>Returns the current submit button type. If not explicitly set, returns the default value <code>Emphasized</code>.</td>
        </tr>
      </tbody>
    </table>

=== "Setter"

    <table>
      <thead>
        <tr>
          <th style="width: 30%;">Method</th>
          <th>Parameter</th>
          <th style="width: 10%;">Type</th>
          <th>Mandatory</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 30%;"><code>setSubmitButtonType(newValue)</code></td>
          <td><code>newValue</code></td>
          <td style="width: 10%;"><a href="https://sapui5.hana.ondemand.com/#/api/sap.m.ButtonType">ButtonType</a></td>
          <td>✅ Yes</td>
          <td>Sets a custom button type for the submit button, overriding the default <code>Emphasized</code> type.</td>
        </tr>
      </tbody>
    </table>

### Example

=== "TypeScript"

    ```ts linenums="1" hl_lines="17" title="Main.controller.ts"
    import Controller from "sap/ui/core/mvc/Controller";
    import CreateEntry from "ui5/antares/pro/v2/entry/CreateEntry"; // Import the class
    import ButtonType from "sap/m/ButtonType"; // Import the ButtonType enum

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
                submitButtonType: ButtonType.Reject // Override the submit button type
            });
        }
    }
    ```

=== "JavaScript"

    ```js linenums="1" hl_lines="17" title="Main.controller.js"
    sap.ui.define([
        "sap/ui/core/mvc/Controller",
        "ui5/antares/pro/v2/entry/CreateEntry", // Import the class
        "sap/m/ButtonType" // Import the ButtonType enum
    ], (Controller, CreateEntry, ButtonType) => {
        "use strict";

        return Controller.extend("your.apps.namespace.Main", {
            onInit: function () {
            
            },

            onCreateProduct: async function () {
                const entry = new CreateEntry({
                    controller: this, 
                    entitySet: "Products",
                    submitButtonType: ButtonType.Reject // Override the submit button type
                });
            }
        });
    });
    ```

---

## Close Button Text (closeButtonText)

![string](https://img.shields.io/badge/Type-string-blue?style=flat-square)

![Localized Text](https://img.shields.io/badge/Default%20Value-Localized%20Text-orange?style=flat-square)

Text displayed on the close button within the generated dialog. A default localized text is provided by the library based on the current language. This property allows the consumer to override the button text.

!!! note

    The library **will not generate** any button in the `Component Mode` regardless of which Entry class is utilized.

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
          <td style="text-align:center;">❌ No</td>
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
          <td style="width: 25%;"><code>getCloseButtonText()</code></td>
          <td><code>string</code></td>
          <td>Returns the current close button text. If not explicitly set, returns the default localized text.</td>
        </tr>
      </tbody>
    </table>

=== "Setter"

    <table>
      <thead>
        <tr>
          <th style="width: 35%;">Method</th>
          <th>Parameter</th>
          <th>Type</th>
          <th>Mandatory</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 35%;"><code>setCloseButtonText(newValue)</code></td>
          <td><code>newValue</code></td>
          <td><code>string</code></td>
          <td>✅ Yes</td>
          <td>Sets a custom text for the close button, overriding the default localized text.</td>
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
                closeButtonText: "Cancel" // Override the close button text
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
                    closeButtonText: "Cancel" // Override the close button text
                });
            }
        });
    });
    ```

---

## Close Button Type (closeButtonType)

![ButtonType](https://img.shields.io/badge/Type-ButtonType-blue?style=flat-square)

![Default](https://img.shields.io/badge/Default%20Value-Default-orange?style=flat-square)

[Button Type](https://sapui5.hana.ondemand.com/#/api/sap.m.ButtonType) of the close button in the generated dialog. Defaults to **Default**. This property allows the consumer to configure a different button type.

!!! note

    The library **will not generate** any button in the `Component Mode` regardless of which Entry class is utilized.

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
          <td style="text-align:center;">❌ No</td>
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
          <th style="width: 25%;">Returns</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 25%;"><code>getCloseButtonType()</code></td>
          <td style="width: 25%;"><a href="https://sapui5.hana.ondemand.com/#/api/sap.m.ButtonType">ButtonType</a></td>
          <td>Returns the current close button type. If not explicitly set, returns the default value <code>Default</code>.</td>
        </tr>
      </tbody>
    </table>

=== "Setter"

    <table>
      <thead>
        <tr>
          <th style="width: 30%;">Method</th>
          <th>Parameter</th>
          <th style="width: 10%;">Type</th>
          <th>Mandatory</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="width: 30%;"><code>setCloseButtonType(newValue)</code></td>
          <td><code>newValue</code></td>
          <td style="width: 10%;"><a href="https://sapui5.hana.ondemand.com/#/api/sap.m.ButtonType">ButtonType</a></td>
          <td>✅ Yes</td>
          <td>Sets a custom button type for the close button, overriding the default <code>Default</code> type.</td>
        </tr>
      </tbody>
    </table>

### Example

=== "TypeScript"

    ```ts linenums="1" hl_lines="17" title="Main.controller.ts"
    import Controller from "sap/ui/core/mvc/Controller";
    import CreateEntry from "ui5/antares/pro/v2/entry/CreateEntry"; // Import the class
    import ButtonType from "sap/m/ButtonType"; // Import the ButtonType enum

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
                closeButtonType: ButtonType.Reject // Override the close button type
            });
        }
    }
    ```

=== "JavaScript"

    ```js linenums="1" hl_lines="17" title="Main.controller.js"
    sap.ui.define([
        "sap/ui/core/mvc/Controller",
        "ui5/antares/pro/v2/entry/CreateEntry", // Import the class
        "sap/m/ButtonType" // Import the ButtonType enum
    ], (Controller, CreateEntry, ButtonType) => {
        "use strict";

        return Controller.extend("your.apps.namespace.Main", {
            onInit: function () {
            
            },

            onCreateProduct: async function () {
                const entry = new CreateEntry({
                    controller: this, 
                    entitySet: "Products",
                    closeButtonType: ButtonType.Reject // Override the close button type
                });
            }
        });
    });
    ```