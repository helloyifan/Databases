#The Relational Model

Idea: All information is organized in (flat) relations

Features
* simple and clean data model
* powerful and declarative query/update languages
* semantic integrity constraints
* data independence


* **database** = set of named relations/tables
* **relations** = has a set of named attributes/columns
* **attribules** - has a type/domain
* **tuple/row** = has a value for each attribute
 
##Formal Definition

Universe : a set of atomic values D with equality (=)
Domain: a name D with a set of values dom(D) in D
Relations/Schema:has a name R set of distinct attribute names A and a set of domain names (doen't have to be distinct) R(A1:D1...
- instance: a fininte relation.

Database/Schema: a fine set of uniquely named relations
- instance: a relation Ri for each Ri

Intention of a relation: the associated relation schema
Extension of a relation: the associated set of tuples

##Relational Model Properties

Relational Schema's have named and typed attributes
Relational instances are finite

Properties of a relation
1. based on (finite set theory) 
  - attribute ordering is not necessary
  - value oriented: tuples identified by attribute values
  - instance has a set semantics: no ordering among tuples, no duplicate tuples
2. all attribute values are atomic
3. degree: number of attributes in a schema
4. cardinality: number of tuples in a instance

##Relations vs SQL Tables

Discrepancies
1. semantics of instance
  - relations are set of tuples
  - tables are multisets of tuples
2. unknown valuse: SQL data model defines a particular value null

##Integrity Constraints

A relational schema captures only the strucutre of relations

Idea: Extend relational/database schema with rules called constraints. An instance is only valid if it satisfies all schema constraints

Reasons to use constaints
- ensure data entry/modifications respects database design
- protect data from bugs in applications

##Types of Integrity Constraints

Tuple level
- domain restrictions
- attribute comparisons

Relation-level
- function dependcies 
- key constaints: a statement that a certain minimal subset of the fields of a relation is a unique identifier for a tuple.
 - super key: a set of attributes for which no pair of distinct tuples in the realtion will ever agree on the corresponding values
 - candidate key: a minimal superkey ( a minimal set of attributes that uniquely identifies a tuple_
 - primary ley: a designated candidate key

Primary key is a Candidate key which in turn is a Super key

Database-level
- Inclusion dependencies
- Foreign key: primary key of one relation apprearing as an attribute of another relation
- Referential Integrity: a tuple with a non null value for a foreign kew that does not match the priary key value of a tuple in the reference relation is not allowed
