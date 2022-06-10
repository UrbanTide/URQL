# URQL

## Examples

#### Filter query
- `eq(property,value) ` -eq(speed,10)
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&eq(speed,10)


- `in(property,(valueA,valueB,...)) ` in(type,(A,B))
  
    https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&in(type,(A,B))


- `lt(property,value)  ` le(speed,10)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&le(speed,10)
  

- `gt(property,value)  ` gt(speed,10)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&gt(speed,10)


- `ge(property,value)  ` ge(speed,10)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&ge(speed,10)


- `ne(property,value)  ` ne(speed,10)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&ne(speed,10)


- `exists(property)  ` exists(speed)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&exists(speed)


- `match(property,value)  ` match(model,Isacco)
  
  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&match(model,Isacco)


- `re(property,value)  ` re(model,Isa.*)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&re(model,Isa.*)


- `value_count(property)  ` value_count(model)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&value_count(model)


- `sum(property)  ` sum(speed)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&sum(speed)


- `avg(property)  ` avg(speed)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&avg(speed)


- `min(property)  ` min(speed)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&min(speed)


- `max(property)  ` max(speed)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&max(speed)


- `stats(property)  ` stats(speed)

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&stats(speed)


- `aggregate(groupingPropertyA,groupingPropertyB,...,operation(property),limit)  ` aggregate(type,value_count(speed))

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&aggregate(type,value_count(speed))



- `date_histogram(date_field_name, interval, ...operation(property))  ` date_histogram(timestamp,day,value_count(speed))

  https://api.usmart.io/org/28ccd497-7cad-4470-bd17-721d5cbbd6ef/ebaa48b2-d69f-4092-b3bc-cd3913dfba97/latest/urql?limit(10,0)&date_histogram(timestamp,day,value_count(speed))
  



