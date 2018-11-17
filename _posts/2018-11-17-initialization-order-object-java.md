---
published: false
---
@@java
\#java

## The correct order of initialisation is:

- Static variable initialisers and static initialisation blocks, in textual order, if the class hasn't been previously initialised.
- The super() call in the constructor, whether explicit or implicit.
- Instance variable initialisers and instance initialisation blocks, in textual order.
- Remaining body of constructor after super().
