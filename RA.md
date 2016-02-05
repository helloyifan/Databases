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
-result schema has all the attributes of E1 **and** all attributes of E2
