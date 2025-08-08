This section documents the core capabilities, configuration options, and behaviors that are shared across all **Entry classes** in the library — namely [**`CreateEntry`**](create_entry.md), [**`UpdateEntry`**](update_entry.md), [**`DeleteEntry`**](delete_entry.md), and [**`DisplayEntry`**](display_entry.md).

The features described here represent the foundational functionality of the **UI5 Antares Pro** library when working with OData V2 models for creating, updating, deleting, or displaying entity data. These capabilities include parameter configurations, UI generation rules, validation mechanisms, value help integration, and extensibility points.

!!! tip "Availability Notice"

    While these features form the common base for all Entry classes, certain capabilities may not be applicable to every class. For example, features related to editable forms may not apply to read-only classes such as [**`DeleteEntry`**](delete_entry.md) or [**`DisplayEntry`**](display_entry.md). Where applicable, such limitations are explicitly noted in the description of each feature.

!!! note "Example Usage Note"

    In the examples provided throughout this section, the [**`CreateEntry`**](create_entry.md) class is used to demonstrate configuration and behavior. However, the same configuration principles apply to the other Entry classes, provided the respective feature is supported in that class.