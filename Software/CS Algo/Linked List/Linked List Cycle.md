- The margin between nodes keeps increasing by 1 until we back to 0
```
    bool hasCycle(ListNode *head) 
    {
        auto slow = head;
        auto fast = head;
        
        while(fast && fast->next)
        {
            slow = slow->next;
            fast = fast->next->next;
            
            if (fast == slow)
            {
                return true;
            }
        }
        
        return false;
    }
```