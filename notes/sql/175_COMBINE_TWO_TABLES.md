# Combine Two tables

```SQL
SELECT P.firstName, P.lastName, A.city, A.state --  select cols u want
From person P -- alias the table name by giving char after table name 
LEFT JOIN Address A  -- merge tables to include null values as well 
ON P.personId = A.personId -- define relationship

-- example if you wanted values that DID not have null

ON P.personId = A.personId where city is not null -- you can also do this to drop non null values
```

