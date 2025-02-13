# build standalone
All abap2UI5 artifacts are combined into a single HTTP handler implementation. This approach makes your app completely independent of the rest of the system or any other abap2UI5 installation.

#### Installation

1. Create a new HTTP handler in your system.
2. Copy & paste the handler class from this repository.
3. Add your abap2UI5 app as a local class and start it via your new HTTP endpoint.
4. Alternatively, pull this repository using abapGit.

#### Persistence
To avoid any side effects with other abap2UI5 installations, this version uses the table z2ui5_t_99 for persistence. You can either pull this repository or manually create the following table in your system:
```cds
@EndUserText.label : 'abap2ui5 standalone'
@AbapCatalog.enhancement.category : #NOT_EXTENSIBLE
@AbapCatalog.tableCategory : #TRANSPARENT
@AbapCatalog.deliveryClass : #A
@AbapCatalog.dataMaintenance : #RESTRICTED
define table z2ui5_t_99 {
  key mandt         : mandt not null;
  key id            : abap.char(32) not null;
  id_prev           : abap.char(32);
  id_prev_app       : abap.char(32);
  id_prev_app_stack : abap.char(32);
  timestampl        : timestampl;
  uname             : abap.char(20);
  data              : abap.string(0);

}
```

#### Info
* HTTP API: `/sap/bc/z2ui5standalone?sap-client=001&app_start=z2ui5_cl_my_standalone_app`
* Credits: Created with and powered by the fantastic tool [abapmerge](https://github.com/larshp/abapmerge)
