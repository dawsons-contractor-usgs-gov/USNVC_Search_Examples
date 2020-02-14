## USNVC (United States National Vegetation Classification) API Query Examples

This document shows some basic query examples for using the USNVC API



The api endpoint  **/api/v1/usnvc/units**  allows for specific queries to be submitted.  

The *pagesize* parameter sets the maximum number of results returned by the query. 

The *offset* parameter is used to implement paging within the result set.

The *q* parameter is where the query is typed in. 

Sample queries are:

A query will find all items with a Database Code of 'CEGL006190'
* {'match': {'data.Identifiers.Database Code':'CEGL006190' }}
 
 
This query searches the Conservation Status Rank, or Description for G1G2 
* {'multi_match':{'query':'G1G2','fields':['data.Conservation Status.*Rank', '*Description']}}

The query below will return results where Black and Pine are found in the Translated Name or Colloquial Name. Note that the 
words do not need to be in the order given. 

* {'multi_match': {'query': 'Black Pine', 'fields': ['data.Overview.Translated Name','data.Overview.Colloquial Name'], 'operator': 'And'}}

Examples of searching on a Scientific Name

(partial name)
* {'match_phrase': {'data.Overview.Scientific Name':'Pinus rigida' }}
* {'match_phrase': {'data.Overview.Scientific Name':'Pinus contorta var. murrayana'}}

(full Scientific Name)
* {'match_phrase': {'data.Overview.Scientific Name':'Pinus rigida / (Quercus ilicifolia) / Aronia melanocarpa / Deschampsia flexuosa Woodland' }}


Where this query will only return results where the Translated Name contains the phrase 'Black Pine' 

* {'match_phrase': {'data.Overview.Translated Name':'Black Pine'}}

These queries will find the results that contain the indicated phrase the Floristics field"

 * {'match_phrase': {'data.Vegetation.Floristics':'open mixture of pines'}} 
 * {'match_phrase': {'data.Vegetation.Floristics':'Graminoids dominate the herbaceous stratum'}}

To find all items with a given parent_id

* {'match': {'data.Hierarchy.parent_id':'871069' }}


A few notes about processing an existing result set via a program or script run against the API:
  
* Near the bottom of each result item returned is a uri field that can be used to access the individual item.
  
* There is an array of ancestors and if applicable an array of children that can be traversed. The numbers in the array each refer to a specific item. 
No example provided because to do this manually you would use the identifier endpoint (see below)for each item 
  
  

The api endpoint **/api/v1/usnvc/units/{identifier}** retrieves an individual item. The Identifier is used to drill down to a specific 
item. Generally this would be an item retrieved as part of more general query. The item number represents that specific unit in the data store, and has no meaning other than being a unique identifier. 

The queries are performed with an ElasticSearch DSL.  More information about the query syntax can be found
at [Elastic Search Query Language](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html)
