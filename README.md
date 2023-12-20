# Alfresco Repository JavaScript Root Object for RenditionService2

This repository addon is designed to address the absence of the renditionService2 JavaScript Root Object in the current [Repository JavaScript API](https://docs.alfresco.com/content-services/latest/develop/reference/repo-root-objects-ref/), a component introduced in Alfresco 7.0 to replace the deprecated `renditionService`. The implementation provided by this project allows seamless integration and utilization of the `renditionService2 in your Repository JavaScript scripts.

## Building

To build the project, use the default Maven command:

```bash
mvn clean package
```

## Deploying

Deploy the compiled JAR file, named `script-rendition-service-2-1.0.0.jar`, by copying it to the `$TOMCAT_DIR/webapps/alfresco/WEB-INF/lib` folder.

## Using

After successful deployment, leverage the following methods within your Repository JavaScript code:

```javascript
// Find all renditions for a given ScriptNode document 
var renditions = renditionService2.getRenditions(document);
renditions.forEach(function(rendition) {
  logger.log(rendition);
});

// Get a single rendition by name
logger.log(renditionService2.getRenditionByName(document, "pdf"));

// This method is executed asynchronously, no result is available
renditionService2.render(document, "pdf");
```

## Workaround

If this addon is not applied, you can still access the `RenditionService2` Spring bean from Repository JavaScript code using the `Packages` approach:

```javascript
var context = Packages.org.springframework.web.context.ContextLoader.getCurrentWebApplicationContext();
nodeRef = new Packages.org.alfresco.service.cmr.repository.NodeRef('workspace://SpacesStore/' + document.getId());
var RenditionService2 = context.getBean('renditionService2', Packages.org.alfresco.repo.rendition2.RenditionService2Impl);
logger.log(RenditionService2.getRenditions(nodeRef));
```

This workaround allows you to access the functionality of `RenditionService2` even without applying the addon.