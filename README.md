# nbpfcrudgen-derby_sample_mod-wildfly-with-theme_selector

A final working project generated with Primefaces Crud Generator.
 
Used: 
Wildfly server.
Database  mysql named derby_sample_mod.

At generated web app with Primefaces Crud Generator i have added functionality to  select a Theme at runtime to change the look of Web app.

So i added at web.xml the following context-param:

<context-param>
        <param-name>primefaces.THEME</param-name>
        <param-value>#{userSettingsBean.theme.name}</param-value>
    </context-param>

into source java i added also a package named: management.themes that contain:

Theme.java
ThemeConverter.java
UserSettingsBean.java (SessionScoped). So the selected Theme  remains stored 
 for the whole session of the user.

Into webpages at dir web/resources i added a dir named images/themes that contain 
the thumbails of Themes.
So when the user try to change the Theme at runtime, it can select it with a image
 of resulting theme selected.

 Also into  WEB-INF/include/entity/ for each entity (customer, discountCode, manufacturer, 
microMarket, product, productCode,purchaseOrder, warehouse) into files:
 Create.xhtml, Edit.xhtml, View.xhtml i modified the following code:

For the Customer entity:
                <h:panelGroup id="display" rendered="#{customerController.selected != null}">
                    <p:panelGrid columns="2" columnClasses="column">

and added : at columnClasses another class named ui-widget-header.

so finally the code modified result:
<h:panelGroup id="display" rendered="#{customerController.selected != null}">
                    <p:panelGrid columns="2" columnClasses="column ui-widget-header">

Obviously for other entities it is necessary to change the name of the controller accordingly.

With this last modify i resolved the problem of labels of field at left side of pages:
 Create.xhtml, Edit.xhtml, View.xhtml, where the names of the labels were not visible.


The  columnClasses="column ui-widget-header" resolved the problem.



Important: for run the netbeans project, resolve the  dependencies: 
from project right click and select properties/lib.

Into libs add the primefaces-6.1.jar and all-themes-1.0.10.jar (download from primefaces web site).

For the persistence, control the  <jta-data-sorce> name if your db is configurated  into wildfly
 with same name:
into project the persitence.xml contains:
 <jta-data-source>java:/jboss/datasources/MySQLDS</jta-data-source>


