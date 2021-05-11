# Catalog API Demo App

This is a sample command line application providing examples of common Catalog API interactions.

## Assumptions

This README assumes you are using Maven to build and run Java code. If you are
not using Maven, the app should still work, but you will need to follow your
existing build/execution steps.

## STEP 1: Get a Personal Access Token

To execute the examples in this demo, you'll need a personal access token from
Square. If you already have one, you can use it for this demo. If you don't
already have one (or want to use a different one) you can generate a new access
token:

1. Visit the Developer Dashboard at https://developer.squareup.com/apps
2. Click "+" under Applications to create a new application.
3. Create an application with the name "Catalog API Demo".
4. Click on the application you have just created, and navigate to "Credentials"
5. Copy the Access Token on that page and save it to an
  environment variable:
   
   `export SQPAT={{ YOUR NEW ACCESS TOKEN }}`

## STEP 2: Compile the demo

The `src` directory should contain everything you need to compile and run the
demo app. To build `catalog-api-demo`:

```bash
mvn compile
```

## STEP 3: List the available examples

To confirm the demo is runnable, use the `-list-examples` flag to see all
the available examples:

```bash
mvn -q exec:java "-Dexec.args=-list-examples"
```

For simplicity, here is a list of available examples and their description:

| Example Name  | Description |
| ------------- | ------------- |
| create_item  | Create an item, then retrieve it  |
| delete_all_items  | Delete ALL items. This is a destructive action and cannot be undone  |
| apply_tax_to_all_items   | Applies a selected tax to all items  |
| deduplicate_taxes  | Merge identical taxes (same name, percentage, and inclusion type)  |
| delete_category  | Create a category with three items, then delete the category and items  |
| list_categories  | List all categories  |
| list_discounts  | List all discounts  |
| location_specific_price  | Create an item with a location-specific price. Must have at least 2 locations to run this example  |
| search_items  | Search for items  |
| retrieve_catalog_object  | Retrieve a catalog object by ID  |
| globally_enable_items  | Make all items available at all locations |
| clone_catalog  | Clones catalog objects from one merchant account to another  |


## Execute an Example

Source code for each of the examples is listed under
`src/main/java/com/squareup/catalog/demo/example/`.

Running an example has the following syntax:

```bash
mvn -q exec:java "-Dexec.args={{ example name }} -token {{ accessToken }}"
```

For example:
```bash
mvn -q exec:java "-Dexec.args=create_item -token $SQPAT"
```

By default, the example will use the sandbox environment: https://connect.squareupsandbox.com/

In order to use the production environment, use the `-env` flag with the `production` argument:
```bash
mvn -q exec:java "-Dexec.args=create_item -token $SQPAT -env production"
```

In order to use a different/custom URL, use the `-base-url` flag with your custom URL and omit the `-env` flag.


## Cleanup an Example

Some examples create items and other catalog objects in your merchant catalog. You can
cleanup the objects created by an example using the `-cleanup` flag.

Note that the cleanup code will delete items and other objects by name, and as such may
delete items with the same name that were not created by the example. 

For example:
```bash
mvn -q exec:java "-Dexec.args=create_item -token $SQPAT -cleanup"
```
