| Operation                 | Data Structure Used     | Reason for Choosing the DS                                                                                   |
| ------------------------- | ----------------------- | ------------------------------------------------------------------------------------------------------------ |
| Insert Word               | **Linked List**         | Allows dynamic memory growth and efficient insertion at end or any position without shifting elements.       |
| Undo / Redo               | **Stack**               | LIFO behavior perfectly represents undo/redo actions: last action done is the first to be reversed.          |
| Display Text (FIFO order) | **Queue**               | Queue provides natural first-in-first-out traversal, matching normal left-to-right reading order.            |
| Edit History Log          | **Queue**               | Keeps history in the exact order events happened—FIFO ensures chronological display.                         |
| Delete First Word         | **Queue + Linked List** | Queue logic fits deletion of the earliest (first) word; linked list pointer update makes deletion efficient. |
| Replace Word              | **Linked List**         | Allows traversal and modification of each node’s word directly.                                              |
| Word Statistics           | **Linked List**         | Easy linear scanning to compute longest, shortest, and average length.                                       |
