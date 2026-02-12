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
