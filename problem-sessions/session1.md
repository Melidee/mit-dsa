### Order functions by asymptotic behavior
- set 0
    - 1: n, 2: root(n), 3:n+root(n)
    - 2, {1, 3}
- set a
    - inputs
        - log(n)^2019
        - n^2 log(n)^2019
        - n^3
        - 2.019^n
        - n log n
    - guess
        - f5 f2 f3 f4
    - actual
        - f1 f5 f2 f3 f4
- set b
    - inputs
        - 2^n
        - n^3
        - choose(n, n/2)
        - n!
        - choose(n, 3)
    - guess
        - f2, f1, {f3, f4, f5}
    - guess2
        - f2 f1, {f3, f5}, f4
    - guess3
        - f4, f2, f1, {f3, f5}
        - n!/((n/2)!(n)!)
        - 1/(n^n)
    - actual
        - {f2, f5}, f3, f1, f4
    - notes
    - (log n)^a < o(n^b)
    - o(n) = O(n) - Theta(n)
        - little o is strict comparison in every case
    - n choose k
        - n!/(k!(n-k)!)
        - how many combinations of k items from n things
        - how many combinations of 5 cards from a 52 card deck

### Black box abstraction
- public interface without knowledge of internals
- not a concrete implementation
- Sequence interface
    - ordered, indexed collection of data
    - extrinsic order
        - doesnt matter what item is, just how they are ordered
        - 1st thing, nth thing, last thing
    - four operations in constant time
        - insert first |Seq, T| => ()
        - insert last |Seq, T| => ()
        - delete first |Seq| => T
        - delete last |Seq| => T
```py
"""
delete the first element and store it
delete the last element and store it
insert the last element in the first position
insert the first element in the last position

constant time (constant number of operations)
"""
def swap_ends(D: Seq):
    first = delete_first(D)
    last = delete_last(D)
    insert_first(D, last)
    insert_last(D, first)
```
```py
"""
k times, delete the first element and push it to the back of the sequence

O(k) time, performs constant time operations k times
"""
def shift_left(D: Seq, k: int):
    for i in range(k):
        item = delete_first(D)
        insert_last(D, item)
"""
delete first element and insert it last, if k != 0 shift_left(k-1)
"""
def shift_left(D: Seq, k: int):
    if k > 0:
        item = delete_first(D)
        insert_last(D, item)
        shift_left(D, k-1)
```
### data structures
```py
"""
make an array dynamic on both ends
if inserting at the front allocate new space and place the array shifted so that there is extra space at the front, 
do the same allocation technique at the back
"""
```
### programming problem
```py
"""
find the center node of the list
reverse the list starting from the center node
"""
def reorder_students(L):
    """
    3 Input: L | linked list with head L.head and size L.size
    4 Output: None |
    5 This function should modify list L to reverse its last half.
    6 Your solution should NOT instantiate:
    7 - any additional linked list nodes
    8 - any other non-constant-sized data structures
    """
    ptr = L.head
    for i in L.size // 2:
        ptr = ptr.next
    ptr.next = reverse_list(ptr.next)

def reverse_list(L):
    if L.head == None:
        return
    head = L.head
    next_node = ptr.next
    head.next = None
    while next_node != None:
        last = head
        head = next_node
        next_node = head.next
        head.next = last
    return head
```