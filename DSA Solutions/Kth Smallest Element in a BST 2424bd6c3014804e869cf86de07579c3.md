# Kth Smallest Element in a BST

Difficulty: medium
 : Yes
: August 1, 2025
Problem: bfs, binary search tree, stack/queue

Perform an inorder traversal of the BST and add the values to a queue. Since inorder traversal of a BST produces values in ascending order, the smallest elements will be at the front of the queue and the largest at the back. To find the kth smallest element, pop k values from the queue and return the last popped value as the answer.