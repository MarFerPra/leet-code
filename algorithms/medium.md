##### Add Two Numbers

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int extra = 0, sum = 0, val1 = 0, val2 = 0;

        ListNode auxNode = new ListNode(0);
        ListNode u = l1;
        ListNode v = l2;

        ListNode currentNode = auxNode;

        while( u != null || v != null){
            val1 = (u != null) ? u.val : 0;
            val2 = (v != null) ? v.val : 0;

            sum = val1 + val2 + extra;
            extra = sum / 10;
            sum = sum % 10;

            currentNode.next = new ListNode(sum);
            currentNode = currentNode.next;

            u = (u != null) ? u.next : null;
            v = (v != null) ? v.next : null;
        }

        if(extra > 0){
            currentNode.next = new ListNode(extra);
        }

        return auxNode.next;

    }
}
```


##### Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

```
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        String currentSolution = "", bestSolution = "";
        Character currentChar;
        Map<Character, Integer> charsUsed = new HashMap<Character, Integer>();

        for(int i = 0; i < s.length(); i++){
            currentChar = s.charAt(i);

            if(charsUsed.containsKey(currentChar)){

                if(currentSolution.length() > bestSolution.length()){
                    bestSolution = currentSolution;
                }

                int index = currentSolution.indexOf(currentChar);

                currentSolution = currentSolution.substring(index+1);
                currentSolution += Character.toString(currentChar);

                charsUsed.put(currentChar, 0);

            } else {
                currentSolution += Character.toString(currentChar);
                charsUsed.put(currentChar, 0);

            }

        }

        if(currentSolution.length() > bestSolution.length()){
            bestSolution = currentSolution;
        }

        return bestSolution.length();
    }
}
```
