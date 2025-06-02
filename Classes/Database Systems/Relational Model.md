
| **Attributes** | **Attributes** |
| -------------- | -------------- |
| *Touples*      | *Touples*      |
| *...*          | *...*          |

$\text{Attributes} = A_1 ... A_n$    
$R = (A_1 ... A_n) \rightarrow \text{Relation Schema}$ *can be unordered*

$r(R) \rightarrow \text{relation instance "r" over schema R}$ 

element *t* of r is a touple

Entities (Primary Keys, Attributes)
- **Entities includes relationships** (merge with the same key if they are unique)
- *1 to Many = 1 ID will suffice*
- *Many to Many = you need both IDs*

## Attributes
- **Domain** - allowed values for attributes
- **Indivisible** - attributes should be "atomic"

*null = unknown = no specification*

## Database
### Database Schema
- logical structure of a database

### Database Instance
- snapshot at a given time

## Keys
- $K\subset R$ 
- K is a **superkey** of R if it can identify a touple
	- superkey K is a **candidate key** if K is *minimal* (least amount of attributes to identify an item/object)
	- **composite key** means using two or more keys to identify and item/object
- K is a **foreign key** if it acts as a constraint (value in one must appear in the other)
	- Referencing
	- Referenced

