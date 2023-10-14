# COLLECTIONS VS COLLECTIONS:
- Collection is an interface with ``LIST``, ``SET`` AND ``QUEUE`` child interface.
- Collections is a utility ``class`` in util package.
- All Methods are ``static`` in nature in Collections Class.

# ENUM SET
- specialized implementation of the Set interface.
- null objects are not allowed in it.
- Fail-Safe iterator is used internally, So no concurrent Modification Exception
- All Methods of ENUM SET uses Bitwise operations.

## Types of ENUM SET:
- Regular EnumSet: uses a single long object to store the elements at each index
  - long value is 64 bits so it can store up to 64 elements.
- Jumbo Set: Array of Long Elements to store the ENUM SET.


# BLOCKING QUEUE:
- It is an interface added in **1.5JDK**
- It does not allow null values
- It is thread-safe in nature
- All methods use atomic in nature and use internal locks.

## Array Blocking Queue:
- Size is fixed in nature
- FIFO Nature
- Implements Serializable Interface.

## Linked Blocking Queue:
- Size is not fixed
- Dynamic allocation of Nodes
- Implements Blocking Queue Interface and **Abstract Queue**
  
