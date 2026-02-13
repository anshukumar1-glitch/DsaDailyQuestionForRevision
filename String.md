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
