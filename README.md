# ServiceNow-Catalog-Experience
A collection of Service Portal Widgets to enhance the ServiceNow Catalog Experience

## Muli-Page Catalog Item

🟡 Warning: Use at your own risk. This feature uses a Service Portal specific g_form hack to circumvent mandatory variables and therefore may pose risk for future upgrades. If you are intent on a multi-page catalog item solution, this one is fairly low risk compared to other mainstream solutions.

[![Multi-Page Catalog Item Video](http://img.youtube.com/vi/F3gYalVybbM/0.jpg)](http://www.youtube.com/watch?v=F3gYalVybbM "Multi-Page Catalog Item")

A common requirement for Service Catalog is the ability to support multi-step or multi-page Catalog Items.  The proposed solution typically involves recommending Order Guides (less than ideal portal implementation), cloning the Catalog Form widget (a moderate to high risk idea), or one of many solutions that nest the Catalog Form Widget which typically has a large, risky code base.  This specific implementation achieves the same multi-page experience via Catalog Item containers with a number of advantages over other typical solutions:

### Advantages

#### No Mandatory Variable Issues

Mandatory variables introduce a number of issues that generally require a complex code base to juggle the issue with the inability of g_form.setVisible to hide variables that are mandatory. This solution circumvents the issue with a g_form hack that directly sets container visibility to false which ignores the child variable mandatory checks. Ideally, ServiceNow would implement a standard g_form method for container visibility that provided this functionality.  In absense, this hack provides the desired outcome in just a few lines of code.

#### Support for Multi Row Variable Sets

A common issue with container based multi-page Catalog solutions is that Catalog treats Multi-Row Variable Sets as a container.  Without a separate data model, it would not be possible to have additional fields on the same page as a Multi-Row Variable Set.  This solution provides that data model in the form of a Sections related list on every Catalog Item.  This makes it possible to associate multiple containers with a single page.  Through these simple data definitions, this widget framework is able to manage what would normally take extensive Client Script or UI Policy logic.

#### Bring Your Own Widget

The logic for this solution is almost entirely contained in the `CatalogItemNavigator` Angular Provider. This standard API means you can bring your own widget to the party without having to clone, copy, and manage the container logic.  Don't like the look and feel provided in the reference implementation?  Go crazy building your own on top of the shared API service.

### Disadvantages

#### Non-Standard Methods

This solution, like most multi-page Catalog Item solutions, requires the use of non-standard API calls. In particular, this method hooks into the g_form events in Service Portal to get access to the g_form instance variable and also uses a g_form hack by accessing the field's \_isVisible internal property to bypass the variable mandatory checks when hiding containers.  It's worth noting that most solutions require access to more non-standard features than this solution.

## Installation

1. Download the Update Set XML from Releases
2. Upload the Update Set XML to your Instance
3. Commit the Update Set to install the application
4. You can add a Page Route map or use any technique desired to direct Catalog Items to the `cc_cat_item` Service Portal page or create your own widgets and pages to customize to your needs
