---
authors: 
  - mcroissant
date: 2024-12-18
categories:
  - api
  - cicd
  - yaml
hide:
  - toc
---


# Manipulating YAML and OpenApi specifications with yq

[Yq](https://mikefarah.gitbook.io/yq) is a powerful command-line tool designed to make working with YAML, JSON, and XML files easier and more efficient. it is build to feell a lot like [jq](https://jqlang.github.io/jq/) an other popular cli.

YQ functionalities support YAML, making it an invaluable resource for us developers, DevOps engineers, and data enthusiasts who frequently interact with configuration files or structured data formats. 

With YQ, you can query, manipulate, and transform data in a concise and expressive way, all while maintaining readability. Whether you're automating workflows, debugging configuration issues, or managing complex infrastructure setups, YQ streamlines these tasks, saving you both time and effort. 


<!-- more -->

## General usage of yq with openapi

You can use yq in many ways as YAML gained quite a lot of popularity over json in the last years, obviously the whole container and Kubernetes cluster operation aspects come to mind, but I would like to take a slightly different turn on this and show you a few of the wonders you can do on OpenApi 
specification with this tool.


### list paths
```bash
yq eval '.paths | keys[]' petstore.yml
```


**Output**

```bash
/pets
/pets/{petId}
``` 

### list the servers

``` bash
yq eval '.servers[].url' petstore.yml
```

**Output**
```
http://petstore.swagger.io/v1
```


## More advanced pattern 

### Search 
```bash
yq eval  '.paths[] | select(has("security")) | keys[]' petstore.yml
```

This will return you the secured endpoint list, obviously in this example there are none

### Merge two yamls to add a security scheme

You could leverage this call to apply a security scheme to multiple APIs as part of your CICD, this can come very handy whenever you have additional layers on topc of your API like a Gateway.

```yaml title="security_scheme.yml"
openapi: 3.0.1
components:
  securitySchemes:
    ApiAuth:
      type: apiKey
      in: header
      name: X-API-KEY
```

```bash
yq eval-all 'select(fileIndex == 0) * select(fileIndex == 1)' petstore.yml security_scheme.yml
```


### Applying a security scheme to paths in your API 

```bash
yq eval  '.paths[]+= {"security": [{"ApiAuth":[]}]}' petstore.yml
```

This one will actually add an "ApiAuth" security scheme as well as the security element to your different paths.


### Replace auth in openapi yml

As a final call I leave with this one yq query that took me a bit longer to figure out but that is now part of some of the CI pipeline I use where you can replace an existing security scheme by an other one.

```bash
 yq eval '.paths[] |=    (.. | select(has("security")) | .security[]| .basicAuth |key) = "apiAuth" ' availability.yml
```


## Conclusion

Working with OpenApi specificationisn’t just about designing APIs. There are plenty of occasion where you would like to manipulate the specification. Yq stands out as a reliable, efficient, and flexible tool for these tasks. By incorporating yq into your toolkit, you can simplify your workflows and enhance productivity. 
