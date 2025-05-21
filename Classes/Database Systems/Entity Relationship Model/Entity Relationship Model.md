## ER Diagram
Consists of:
1. **Entity Set** - *stores* a set of *objects or items* (represented by a *rectangle*)
2. **Attribute** - describes a *property of an entity* (represented as an *oval*)
3. **Relationship** - defines relationships between entities (represented as a *diamond*)

![[Entity Relationship Model-1.webp]]

**Entities**: *Student* and *Class*
**Attributes**:
1. Student: *NRIC (Primary Key), Name, DoB*
2. Class: *Number (Primary Key), Name, Location*
**Relationship**: *Enrolled in*

### Self-referencing Relationship
There can be an edge case where a **Relationship** points to an **Entity** that *points back* to the  **Relationship**

![[Entity Relationship Model-2.webp]]


### Tertiary Relationship
When a **Relationship** involves more than two **Entities**
![[Entity Relationship Model-3.webp]]

You can read this **ER Diagram** as:
1. Given an article and a book, they can only be published by 1 publisher.
2. Given an article and a publisher, the article can only appeared one book (published by that publisher).
3. Given a book and a publisher, the book may contain many different articles.