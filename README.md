# URQL

## USMART Resource Query Language

### Introduction

The **U**SMART **R**esource **Q**uery **L**anguage (URQL) allows you to search
for specific records within an API resource. We've based URQL loosely on 
[RQL](https://github.com/persvr/rql).

#### URQL Rules

The URQL grammar is based around standard URI delimiters. The standard rules for
encoding strings with URL encoding (%xx) are observed. URQL also supersets FIQL.
Therefore we can write a query that finds resources with a "price" property below
10 with a "lt" operator using FIQL syntax:

    price=lt=10

Which is identical (and sugar for call operator syntax known as the normalized form):

    lt(price,10)

One can combine conditions with multiple operators with "&":

    foo=3&price=lt=10

Is the same as:

    eq(foo,3)&lt(price,10)

Which is also the same as:

    and(eq(foo,3),lt(price,10))

The | operator can be used to indicate an "or" operation. We can also use paranthesis
to group expressions. For example:

    (foo=3|foo=bar)&price=lt=10

Which is the same as:

    and(or(eq(foo,3),eq(foo,bar)),lt(price,10))

Values in queries can be strings (using URL encoding), numbers, booleans, null, undefined,
and dates (in ISO UTC format without colon encoding). We can also denote arrays
with paranthesis enclosed, comma separated values. For example to find the objects
where foo can be the number 3, the string bar, the boolean true, or the date for the
first day of the century we could write an array with the "in" operator:

    foo=in=(3,bar,true,2000-01-01T00:00:00Z)

We can also explicitly specify primitive types in queries. To explicitly specify a string "3",
we can do:

    foo=string:3


Another common operator is sort. We can use the sort operator to sort by a specified property.
To sort by foo in ascending order:

	price=lt=10&sort(+foo)

We can also do multiple property sorts. To sort by price in ascending order and rating in descending order:

    sort(+price,-rating)

### Query operators

#### Filter query

- `eq(property,value) ` - Filters for objects where the specified property's value is equal to the provided value
  
    https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&eq(speed,10)
- `in(property,(valueA,valueB,...)) ` - Filters for objects where the specified property's value is in the comma-separated array of values
  
    https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&in(type,(A,B))
- `lt(property,value) ` - Filters for objects where the specified property's value is less than the provided value
  
    https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&lt(speed,10)
- `le(property,value,interval,,start_of_interval) ` - Filters for objects where the specified property's value is less than or equal to the provided value, can also accept date_math: (property,value,-1M,M)
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&le(speed,10)
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&le(timestamp,2019-06-01)
- `gt(property,value) ` - Filters for objects where the specified property's value is greater than the provided value
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&gt(speed,10)
- `ge(property,value,interval,start_of_interval) ` - Filters for objects where the specified property's value is greater than or equal to the provided value, can also accept date_math: (property,value,-1M,M)
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&ge(timestamp,2019-06-01)
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&ge(speed,10)
  
- `exists(property) ` - Filters for objects where the specified property's value is not null or []
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&exists(speed)

#### Freetext query

- `re(property,value) ` - Filters for objects where the specified property's value is in the regular expression value

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&re(model,Isa.*)

- `match(property,valueA valueB ...) ` - Matches objects where the specified property's value contains any of the provided, space separated, values (ordered by number of words matching)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&match(model,Isacco)

- `matchphrase(property,valueA valueB ...)) ` - Matches objects where the specified property's value contains the exact phrase made up of comma-separated values
- `matchphrase(property,valueA valueB ...,slopFactor)) ` - Matches objects where the specified property's value contains the comma-separated values in the order specified, but they may be separated by the slopFactor number of other words

#### Aggregation query

- `value_count(property)` - Count the number of occurrences of a property

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&value_count(model)

- `sum(property)` - Sum all values of this property

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&sum(speed)

- `avg(property)` - Calculate the average value of this property

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&avg(speed)

- `min(property)` - Find the minimum value of this property
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&min(speed)
  
- `max(property)` - Find the maximum value of this property
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&max(speed)

- `stats(property)` - Get a full statistical breakdown for this property (value_count, sum, avg, min, max)
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&stats(speed)

- `aggregate(groupingPropertyA,groupingPropertyB,...,operation(property),limit)` - aggregate values of a property grouped by one or more other properties; for 'operation' use value_count, sum, avg, min, max; if multiple operations are required, provide them in a comma separate list enclosed by brackets; to limit number of returned aggregate rows to top X set 'limit' to an integer (default value is 100000)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&aggregate(type,value_count(speed))


#### Special Operations

- `date_histogram(date_field_name, interval, ...operation(property))` - date_histogram is a special operation that can be used inside an aggregation. It is native to elasticSearch: (https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-bucket-datehistogram-aggregation.html, "ElasticSearch Date_Histogram"), operation can be any of the above^

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&date_histogram(timestamp,day,value_count(speed))

- `serial_diff( integer )` - serial_diff can be a secondary operation used inside a date_histogram after one the above is used. This will use the value produced by the prior operation to create a difference in values. More information here:(https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-pipeline-serialdiff-aggregation.html, "ElasticSearch Serial_Differencing")

#### Spatial query
- `withinBoundingBox(geometryProperty,(minX,maxX,minY,maxY)) ` - Filters for objects where the specified geometry property's coordinates fall completely within the bounding box as defined by minimum and maximum X and Y values

#### Combining queries

- `and(query,query,...) ` - Applies all the given queries
- `or(query,query,...) ` - The union of the given queries

#### Sorting, selecting return values and paging

- `sort(+|-propertyA,+|-propertyB,...) ` - Sorts by the given property/properties in order specified by the prefix (+ for ascending, - for descending)
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(100,0)&select(timestamp,speed)&sort(+speed)
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(100,0)&select(timestamp,speed)&sort(-speed)
- `select(property,property,...) ` - Trims each object down to the set of properties defined in the arguments

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(100,0)&select(timestamp,speed)

- `limit(numberOfRecords,offset) ` - Returns the given range of objects from the result set (numberOfRecords = how many records should be returned, offset = how many records should be skipped; to return a stream of all records call 'limit(-1)'.) The 'limit' operator can only be used for the first 10,000 records (you chose limit and offset)
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(100,0)

### Others
- `format(ouputFormat) ` - Sets the output format - valid values are 'json' (default) and 'csv' (comma separated text file).
- `cache=true ` - Turn on cache option for this query
### More Examples
TODO
