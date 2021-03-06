---
uid: AssetsSearchAPI
---

# Assets Search API
The assets search API allows you to search for your assets with search criteria.

***
## `Get Assets by Search Criteria` 
Returns an array of assets that meet the search criteria.

### Searchable Properties
Assets can be searched on the following asset properties:

- Id
- Name
- Description
- Attributes
  - Name
  - Description
  - Value
- Asset Type Name
- AssetTypeId
- Measurement Mapping Name

Search criteria can be chained together using an **AND**. See examples below. 


### Request 
```text 

GET api/v1-preview/Tenants/{tenantId}/Namespaces/{namespaceId}/Assets?skip={skip}&count={count}&query={queryString} 

```

### Parameters  
`string tenantId` 

The tenant identifier

`string namespaceId` 

The namespace identifier

[Optional] `int skip` 

An optional parameter representing the zero-based offset of the first asset to retrieve. If not specified, a default value of 0 is used.

[Optional] `int count` 

An optional parameter representing the maximum number of assets to retrieve. If not specified, a default value of 100 is used.

`string queryString`
The asset query string.Search strings are not case-sensitive.

### Response 
The response includes a status code and an array of assets matching the search criteria.

| Status Code | Body Type | Description |
|--|--|--|
| 200 OK | Asset list | A list of assets matching the search criteria. An empty array is returned if there are no matching assets. |
| 204 OK | empty | No assets match your search criteria. |
| 400 Bad Request | error | The request is not valid. See the response body for additional details. |
| 403 Forbidden | error | You are not authorized to view the requested asset. |

### Example Asset Queries

| Query String                   | Description                                                  |
| ------------------------------ | ------------------------------------------------------------ |
| Id:Id1                         | Returns the asset with ID equal to **Id1**.                  |
| Id:Id*                         | Returns all assets with ID matching **id*** wildcard. |
| Name:Name1                     | Returns all asset with a friendly name equal to **Name1**. |
| Id:Id AND Name:Name1           | Returns all assets with ID matching the **id*** wildcard and with a friendly name equal to **Name1**. |
| Description:floor1*            | Returns all assets with a description that starts with **floor1**. |
| Metadata/Name:Building*      | Returns all assets with at least one metadatum description that contains the string **Building**. |
| Metadata/Description:heater* | Returns all assets with at least one metadatum description that starts with **heater**. |
| Metadata/Value:123           | Returns all assets with at least one metadatum that equals **123**. |
| Id:X* AND Metadata/Name:B*   | Returns all assets with ID starting with **X** and containing at least one metadatum with a name that starts with a **B**. |
| AssetTypeId:HeaterTypeId | Returns all assets with AssetTypeId matching HeaterTypeId |
| AssetTypeName:HeaterTypeName | Returns all assets whose Name field of the AssetType matches HeaterTypeName |
| Measurements/Name:WindMeasure | Returns all assets with the measurement name **WindMeasure**. |


