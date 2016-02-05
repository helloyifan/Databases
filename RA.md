#Relation Algebra

The relational algebra consists of a set of operators

Relation algebra is closed
- each operator takes as input zero or more relations
- ech operator defines a single output realtion in terms of its input relation(s)
- relational operators can be compsed to form expressions that define new relations in terms of existing relations

Notations
R - relation name
E - relational algebra expression+

##Selection (σ)

σcondition(E)
- result schema: same as E's
 - preseves all columns

-real instance: subset of E's tuples that satisfy the condition
 - Filters some rows

##Projection (π)

- πattributes(E)
- result schema: only the specified attributes
 - filters some columns

- result instance: could have as amany tuples as E except that dupicates are eliminated (*)
 - preserves all rows


## Rename: (p)

Rename: p(R(F), E)
F - list of terms of the form oldname -> new name

- result schema: E's schema with columns renamed according to F 
- result instance : same as E's
- remebers the result as R for future expressions

rename: p(Movies(title ->name, actor->performer), Film)

##Product (x)

Product: E1 x E2
- result schema has all the attributes of E1 **and** all attributes of E2
- result instance: includes one tuple for every pair of tuples (one from each expression result) in E1 and E2
- sometimes called cross product or Cartesian prodcut
- renaming is needed when E1 and E2 have comon attributes


##Joins

###Condition join E1 ⋈ condition E2
- equivalent to σ condition(E1 x E2)
- special case: equijoin -> textbook
- eg Proj ⋈ (RespEmp = EmpNO) Emp

###Natural Join E1 ⋈ E2
- equivalent to π...(σ ...(E1 x E2))
- the result of E1 ⋈ E2 can be formed by the following steps

1. form the cross-product of E1 and E2 renaming duplicate attributes
2. eliminate from the cross-product and tuples that do not have matching values for all pair of attributes common to schemas E1 and E2
3. Project out douplicate attributes

- If no attributes in common, this is just a product
 
#Set-Based Relational Operators

**Union Compatible**: two relations are union-compatible if they have the same # of attributes and each attribute must be from the same domain


- Union (R \union S)
 - Schemas of R and S must be "union compatible"
 - Result includes all tuples that appear either in R or in S or in both

- Difference (R - S)
 - Schemas of R and S must be "union compatible"

- Intersection (R \intersection S)
 - Schemas of R and S must be "union compatible"
 - Result includes all tuples that appear in both R and S

- Union Compatible
 - same number of fields
 - 'corresponding' (left to right) fields have the same type
 
##Relational Division

X/s = πA(X) πA((πA(X)xS)   X) //This is obviously wrong but slides are wrong too

##Relational Completeness

Definition (Relationally Complete)
A query languages that is at least as expressive as relational algebra is said to be relationally complete

- The following languages are all erlatiobally complete
 - safe relational calculus
 - relational algebra
 - sql

- Sql has additional expressive power because it captures duplicate tuoesm unknown values, aggregation, ordering....
