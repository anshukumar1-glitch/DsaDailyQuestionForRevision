## Leetcode -3713

```java
class Solution {
    public static boolean checkBalance(int []arr)
    {
         int common=0;
        for(int i=0;i<26;i++){
        if(arr[i]==0)continue;
        if(common==0)
        {
            common=arr[i];
        }
        else if(common!=arr[i])
        {
            return false;
        }
    }
      return true;
    }
    public int longestBalanced(String s) {
        int max=0;
        for(int i=0;i<s.length();i++)
        {
            int[]arr=new int[26];
           for(int j=i;j<s.length();j++)
           {
              char ch=s.charAt(j);
              arr[ch-'a']++;
              if(checkBalance(arr))
              {
                max=Math.max(j-i+1,max);
              }
           }
        }
        return max;
    }
}
```
## Leetcode 921
```java
class Solution {
    public int minAddToMakeValid(String s) {
        Stack<Character>st=new Stack<>();
        int i=0;
        while(i<s.length())
        {
            char ch=s.charAt(i);
            if(st.isEmpty()||ch=='(')
            {
                st.push(ch);
            }
            else if(st.peek()=='('&&ch==')')
            {
                st.pop();
            }
            else{
                st.push(ch);
            }
            i++;
        }
        return st.size();
    }
}
```
## Leetcode 1249  Minimum Remove to Make Valid Parentheses
```java
class Solution {
    public String minRemoveToMakeValid(String s) {
        List<Integer>ls=new ArrayList<>();
        for(int i=0;i<s.length();i++)
        {
            char ch=s.charAt(i);
            if(!Character.isLetter(ch)){
            if(ls.isEmpty()||ch=='(')
            {
                ls.add(i);
            }
            else if(s.charAt(ls.get(ls.size()-1))=='('&&ch==')')
            {
               ls.remove(ls.get(ls.size()-1));
            }
            else{
                ls.add(i);
            }
        }
        }
        StringBuilder sb=new StringBuilder();
        for(int i=0;i<s.length();i++)
        {
            char ch=s.charAt(i);
            if(!ls.contains(i))
            {
                sb.append(ch);
            }
        }
        return sb.toString();
    }
}
```
## 1221. Split a String in Balanced Strings
```java
class Solution {
    public int balancedStringSplit(String s) {
        int count=0;
        int balance=0;
        for(int i=0;i<s.length();i++)
        {
            char ch=s.charAt(i);
            if(ch=='L')
            {
               balance++;
            }
            else{
                balance--;
            }
            if(balance==0)
            {
                count++;
            }
        }
        return count;
    }
}
```
### 1647. Minimum Deletions to Make Character Frequencies Unique
## Intution
 1. Count frequencies.
2. Maintain a Set of used frequencies.
For each frequency:
 - While it is already in the set:
- Decrease frequency by 1
- Count deletion
- Add final frequency to set
This is Greedy.
```java
class Solution {
    public int minDeletions(String s) {
        HashMap<Character,Integer>hm=new HashMap<>();
        for(char ch:s.toCharArray())
        {
            hm.put(ch,hm.getOrDefault(ch,0)+1);
        }
        int count=0;
        Set<Integer>hs=new HashSet<>();
        for(Map.Entry<Character,Integer>it:hm.entrySet())
        {
            char key=it.getKey();
            int val=it.getValue();
            while(hs.contains(val))
            {
               val=val-1;
               count++;
            }
            if(val!=0)
            hs.add(val);
        }
        return count;
    }
}
```
### 2091. Removing Minimum and Maximum From Array
Key Idea Recap (Very Important)
We only care about:
minIndex
maxIndex
n = nums.length
Then we consider 3 strategies:
1️⃣ Delete from front only
2️⃣ Delete from back only
3️⃣ Delete from both sides

```java
class Solution {
    public int minimumDeletions(int[] nums) {
        int minIndex=0;
        int maxIndex=0;
        for(int i=0;i<nums.length;i++)
        {
            if(nums[minIndex]>nums[i])
            {
                minIndex=i;
            }
        }
        for(int i=0;i<nums.length;i++)
        {
             if(nums[maxIndex]<nums[i])
            {
                maxIndex=i;
            }
        }
        int left=Math.min(minIndex,maxIndex);
        int right=Math.max(minIndex,maxIndex);
        int deleteFromFront=right+1;
        int deleteFromBack=nums.length-left;
        int deleteFromBoth=(left+1)+(nums.length-right);

        int ans=Math.min(deleteFromFront,Math.min(deleteFromBack,deleteFromBoth));
        return ans;
    }
}
```
### 1423. Maximum Points You Can Obtain from Cards
```java
class Solution {
    public int maxScore(int[] cardPoints, int k) {
        int[]prefix=new int[cardPoints.length];
        int []suffix=new int[cardPoints.length];
        prefix[0]=cardPoints[0];
        int n=cardPoints.length;
        suffix[n-1]=cardPoints[n-1];
        for(int i=1;i<n;i++)
        {
            prefix[i]=prefix[i-1]+cardPoints[i];
        }
        for(int i=n-2;i>=0;i--)
        {
            suffix[i]=suffix[i+1]+cardPoints[i];
        }

        int max=0;
        for(int i=0;i<=k;i++)
        {
            int left=0;
            int right=0;
            if(i>0)
            {
              left=prefix[i-1];
            }
            if(k-i>0)
            {
                right=suffix[n-(k-i)];
            }
            max=Math.max((left+right),max);
        }
        return max;
    }
}
```
Core Idea:-
You must take exactly k cards.
If you take:
i cards from the left
then you must take k - i cards from the right
Because:
total cards taken = k
i (left) + (k - i) (right) = k
The Loop
for (int i = 0; i <= k; i++)

This loop tries all possible distributions of cards.
If k = 3, the loop runs like this:
i (left)	k - i (right)
0	3
1	2
2	1
3	0

So we check:
0 left + 3 right
1 left + 2 right
2 left + 1 right
3 left + 0 right
This guarantees we don’t miss any possible valid combination.

### 2379. Minimum Recolors to Get K Consecutive Black Blocks
```java
class Solution {
    public int minimumRecolors(String arr, int k) {
       //Handling if the the colour exist
       int count=0;
       for(int i=0;i<arr.length();i++)
       {
        char ch=arr.charAt(i);
        if(count==k)
        {
            return 0;
        }
        if(ch=='B')
        {
            count++;
        }
        else{
            count=0;
        }
       } 
       int i=0;
       int j=0;
       count=0;
       int min=Integer.MAX_VALUE;
       while(j<arr.length())
       {
          char ch=arr.charAt(j);
           if(ch=='W')
          {
            count++;
          }
          while(j-i+1>k)
          {
            if(arr.charAt(i)=='W'){
            count--;
            }
            i++;
          }
          if(j-i+1==k)
          {
            min=Math.min(count,min);
          }
          System.out.println(min+",i="+i+",j="+j);
          j++;
       }
       return min;
    }
}
```

### 724. Find Pivot Index
Given an array of integers nums, calculate the pivot index of this array.
The pivot index is the index where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to the index's right.
If the index is on the left edge of the array, then the left sum is 0 because there are no elements to the left. This also applies to the right edge of the array.
Return the leftmost pivot index. If no such index exists, return -1.

```java
class Solution {
    public int pivotIndex(int[] nums) {
        int psum[]=new int[nums.length];
        psum[0]=nums[0];
        int n=nums.length;
        for(int i=1;i<n;i++)
        {
         psum[i]=psum[i-1]+nums[i];
        }
        if(psum[n-1]-psum[0]==0)
        {
            return 0;
        }
        for(int i=1;i<n;i++)
        {
            if(psum[i-1]==psum[n-1]-psum[i])
            {
                return i;
            }
        }
        if(psum[n-1]==0)
        {
            return n-1;
        }
        return -1;
    }
}
```
### LeetCode 438. and also like count no of occurences of geeksforgeeks(2 questions)
Correct Sliding Window Behavior
You correctly:
Decrease frequency when expanding window
Decrease count only when frequency hits 0
When window size == k:
If count == 0 → valid anagram
Restore frequency when shrinking window
Increase count when needed
This logic is correct.
```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer>ls=new ArrayList<>();
        int i=0;
        int j=0;
        Map<Character,Integer>hm=new HashMap<>();
        for(char ch:p.toCharArray())
        {
            hm.put(ch,hm.getOrDefault(ch,0)+1);
        }
         int count=hm.size();
        int k=p.length();
        while(j<s.length())
        {
           char cur=s.charAt(j);
           if(hm.containsKey(cur))
           {
            hm.put(cur,hm.get(cur)-1);
            if(hm.get(cur)==0)
            {
                count--;
            }
           }
           if(j-i+1<p.length())
           {
            j++;
           }
           else if(j-i+1==k)
           {
            if(count==0)
            {
                ls.add(i);
            }
            char ch=s.charAt(i);
            if(hm.containsKey(ch))
            {
                hm.put(ch,hm.get(ch)+1);
                if(hm.get(ch)==1)
                {
                    count++;
                }
            }
            i++;
            j++;
           }

        }
        return ls;
    }
}
```
### Leetcode 567 is also similar to previous one rememeber that.

