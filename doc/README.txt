COMP 313/413 Project 2 Report Template

TestList.java and TestIterator.java

	TODO also try with a LinkedList - does it make any difference?

		Yes, it makes a significant difference in performance characteristics. LinkedList and ArrayList have different time complexities for different operations:
		- LinkedList: O(1) for add/remove at ends, O(n) for random access
		- ArrayList: O(1) for random access, O(n) for add/remove at beginning (due to shifting elements)
		The performance differences become very pronounced as the data structure size increases.

TestList.java

	testRemoveObject()

		list.remove(5); // what does this method do?

			list.remove(5) removes the element at INDEX 5 (the 6th element, since indexing starts at 0). 
			It does NOT remove the element with VALUE 5.

		list.remove(Integer.valueOf(5)); // what does this one do?

			list.remove(Integer.valueOf(5)) removes the first occurrence of the element with VALUE 5 from the list. 
			It searches for the object and removes it.

TestIterator.java

	testRemove()

		i.remove(); // what happens if you use list.remove(77)?

			Using list.remove(Integer.valueOf(77)) instead of iterator.remove() would cause a ConcurrentModificationException. 
			This is because modifying a list directly while iterating over it (without using the iterator's remove method) 
			violates the fail-fast behavior of Java collections. The iterator's remove() method is the safe way to remove 
			elements during iteration.

TestPerformance.java

	State how many times the tests were executed for each SIZE (10, 100, 1000 and 10000)
	to get the running time in milliseconds and how the test running times were recorded.

	Each test was run once with 1,000,000 repetitions (REPS = 1000000) for each SIZE.
	Running times were recorded from the Gradle test reports in seconds, then converted to milliseconds.

	SIZE 10
								  #1
        testArrayListAddRemove:  30ms
        testLinkedListAddRemove: 21ms
		testArrayListAccess:     10ms
        testLinkedListAccess:    10ms

	SIZE 100
								  #1
        testArrayListAddRemove:  38ms
        testLinkedListAddRemove: 22ms
		testArrayListAccess:     11ms
        testLinkedListAccess:    19ms

	SIZE 1000
								  #1
        testArrayListAddRemove:  94ms
        testLinkedListAddRemove: 21ms
		testArrayListAccess:     13ms
        testLinkedListAccess:    253ms

	SIZE 10000
								  #1
        testArrayListAddRemove:  1128ms
        testLinkedListAddRemove: 25ms
		testArrayListAccess:     16ms
        testLinkedListAccess:    3514ms

	listAccess - which type of List is better to use, and why?

		ArrayList is significantly better for access operations. ArrayList maintains O(1) constant time access
		regardless of size (10ms-16ms across all sizes), while LinkedList degrades to O(n) linear time
		(10ms for size 10 up to 3514ms for size 10000). For random access, ArrayList is the clear choice.

	listAddRemove - which type of List is better to use, and why?

		LinkedList is significantly better for add/remove operations at the beginning. LinkedList maintains
		O(1) constant time (21-25ms across all sizes) because it only needs to update node references,
		while ArrayList degrades to O(n) linear time (30ms for size 10 up to 1128ms for size 10000)
		because it must shift all subsequent elements. For frequent insertions/deletions at the beginning,
		LinkedList is the clear choice.
