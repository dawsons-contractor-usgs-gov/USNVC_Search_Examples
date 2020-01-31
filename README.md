## USNVC (United States National Vegetation Classification) API Query Examples

This document shows some basic query examples for using the USNVC API

The queries are performed with an ElasticSearch DSL.  More information about the query syntax can be found
at [Elastic Search Query Language](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html)


The api endpoint  **/api/v1/usnvc/units**  allows for specific queries to be submitted.  

The *pagesize* parameter sets the maximum number of results returned by the query. 

The *offset* parameter is used to implement paging within the result set.

The *q* parameter is where the query is typed in. 

Sample queries are:

* {'match': {'data.Identifiers.Database Code':'CEGL006190' }}
 
* {'multi_match':{'query':'G1G2','fields':['data.Conservation Status.*Rank', '*Description']}}

* {'multi_match': {'query': 'Black Pine', 'fields': ['data.Overview.Translated Name'], 'operator': 'And'}}

* {'match_phrase': {'data.Overview.Translated Name':'Black Pine'}}

Note that at the bottom of the individual result set the specific row_id is returned, as well as a uri to retrieve 
the specific item. 

The api endpoint **/api/v1/usnvc/units/{identifier}** retrieves an individual item. The Identifier is used to drill down to a specific 
item. Generally this would be an item retrieved as part of more general query. The item number represents that specific unit in the data store, and has no meaning other than being a unique identifier. 