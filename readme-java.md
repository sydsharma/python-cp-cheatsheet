Java reference for interview coding problems/light competitive programming. Contributions welcome!

## How

Minimal snippets I actually use to solve LeetCode-style problems in Java.

## Why

Predictable performance, strong typing, rich stdlib, great for interviews.

[Language Mechanics](#language-mechanics)

1. [Literals](#literals)
1. [Loops](#loops)
1. [Strings](#strings)
1. [Slicing](#slicing)
1. [Tuples](#tuple)
1. [Sort](#sort)
1. [Hash](#hash)
1. [Set](#set)
1. [List](#list)
1. [Dict](#dict)
1. [Binary Tree](#binarytree)
1. [PriorityQueue](#priorityqueue)
1. [lambda](#lambda)
1. [zip](#zip)
1. [Random](#random)
1. [Constants](#constants)
1. [Ternary Condition](#ternary)
1. [Bitwise operators](#bitwise-operators)
1. [For Else](#for-else)
1. [Modulo](#modulo)
1. [any](#any)
1. [all](#all)
1. [bisect](#bisect)
1. [math](#math)
1. [iter](#iter)
1. [map](#map)
1. [filter](#filter)
1. [reduce](#reduce)
1. [regular expression](#regular-expression)
1. [Types](#types)
1. [Grids](#grids)

[Collections](#collections)

1. [Deque](#deque)
1. [Counter](#counter)
1. [Default Dict](#default-dict)

[Algorithms](#algorithms)

1. [General Tips](#general-tips)
1. [Binary Search](#binary-search)
1. [Topological Sort](#topological-sort)
1. [Sliding Window](#sliding-window)
1. [Tree Tricks](#tree-tricks)
1. [Binary Search Tree](#binary-search-tree)
1. [Anagrams](#anagrams)
1. [Dynamic Programming](#dynamic-programming)
1. [Cyclic Sort](#cyclic-sort)
1. [Quick Sort](#quick-sort)
1. [Merge Sort](#merge-sort)
1. [Merge K Sorted Arrays](#merge-arrays)
1. [Linked List](#linked-list)
1. [Convert Base](#convert-base)
1. [Parenthesis](#parenthesis)
1. [Max Profit Stock](#max-profit-stock)
1. [Shift Array Right](#shift-array-right)
1. [Continuous Subarrays with Sum k](#continuous-subarrays-with-sum-k)
1. [Events](#events)
1. [Merge Meetings](#merge-meetings)
1. [Trie](#trie)
1. [Kadane's Algorithm - Max subarray sum](#kadane)
1. [Union Find/DSU](#union-find)
1. [Fast Power](#fast-power)
1. [Fibonacci Golden](#fibonacci-golden)
1. [Basic Calculator](#basic-calculator)
1. [Reverse Polish](#reverse-polish)
1. [Reservoir Sampling](#reservoir-sampling)
1. [Candy Crush](#candy-crush)

# Language Mechanics

## Literals

```java
int a = 255; int b = 0b11111111; int c = 0xFF;
long L = 1234567890123L; double d = 1.23; boolean ok = true;
char ch = 'a'; String s = "hello\n"; Object n = null;
int[] arr = {1,2,3};
List<Integer> list = new ArrayList<>();
Map<String,Integer> map = new HashMap<>();
Set<Character> set = new HashSet<>();
```

## Loops

```java
for (int i = 0; i < n; i++) {}
for (int i = n - 1; i >= 0; i--) {}
for (int x : nums) {}
int i = 0; while (i < n) { i++; }
```

Reverse in-place

```java
int l = 0, r = nums.length - 1;
while (l < r) { int tmp = nums[l]; nums[l] = nums[r]; nums[r] = tmp; l++; r--; }
```

Ranges

```java
for (int i = 0; i < 3; i++) {}
for (int i = 3; i >= 0; i--) {}
```

## Strings

```java
int i = s.indexOf('x');
int j = s.lastIndexOf('x');
String[] tokens = l.split(":");
String joined = String.join(" ", listOfWords);
StringBuilder sb = new StringBuilder(); sb.append("a").append(1);
char c = s.charAt(0);
boolean up = Character.isUpperCase(c);
boolean low = Character.isLowerCase(c);
boolean dig = Character.isDigit(c);
String t = s.replace("()", "");
boolean st = s.startsWith("pre"); boolean ed = s.endsWith("suf");
String f = String.format("My name is %s, I'm %d", "John", 36);
```

Manual split by isLetter

```java
List<String> splitWords(String input) {
  List<String> out = new ArrayList<>();
  int start = -1;
  for (int i = 0; i < input.length(); i++) {
    char ch = input.charAt(i);
    if (Character.isLetter(ch)) { if (start == -1) start = i; }
    else { if (start != -1) { out.add(input.substring(start, i)); start = -1; } }
  }
  if (start != -1) out.add(input.substring(start));
  return out;
}
```

## Slicing

```java
String sub = s.substring(2, 4);
int[] subArr = Arrays.copyOfRange(arr, 2, 5);
```

## Tuple

```java
record Pair<A,B>(A first, B second) {}
Pair<Integer,Integer> p = new Pair<>(2,3);
```

## Sort

```java
Arrays.sort(nums);
Arrays.sort(nums, 0, k);
Arrays.sort(words, Comparator.comparingInt(String::length));
Collections.sort(list); // natural
list.sort((x,y) -> x[1] - y[1]);
list.sort(Comparator.comparing((int[] a) -> a[1]).thenComparing(a -> a[0]));

Map<String,Integer> m = new HashMap<>();
List<Map.Entry<String,Integer>> e = new ArrayList<>(m.entrySet());
e.sort(Map.Entry.comparingByValue());
```

Keep original indices

```java
int n = nums.length;
int[][] idxVal = new int[n][2];
for (int i = 0; i < n; i++) { idxVal[i][0] = i; idxVal[i][1] = nums[i]; }
Arrays.sort(idxVal, Comparator.comparingInt(a -> a[1]));
```

## Hash

```java
Map<Character,Integer> ht = new HashMap<>();
for (char ch : s.toCharArray()) ht.put(ch, ht.getOrDefault(ch, 0) + 1);
```

## Set

```java
Set<Integer> st = new HashSet<>();
st.add(a); st.remove(a); boolean has = st.contains(a);
Integer any = st.iterator().next();
```

## List

```java
List<Integer> list = new ArrayList<>(Collections.nCopies(5, 0));
List<List<Integer>> grid = new ArrayList<>();
grid.add(new ArrayList<>());
grid.get(0).add(1);
Collections.reverse(list);
List<Object> joinedList = new ArrayList<>(); joinedList.addAll(list1); joinedList.addAll(list2);
```

## Dict

```java
Map<String,Integer> d = new HashMap<>();
d.put("key", 1);
int v = d.getOrDefault("key", 0);
for (String k : d.keySet()) {}
for (var ent : d.entrySet()) { String k = ent.getKey(); int val = ent.getValue(); }
d.computeIfAbsent("k", kk -> 0);
d.remove("k");
```

## BinaryTree

```java
class TreeNode { int val; TreeNode left, right; TreeNode(){} TreeNode(int v){val=v;} }
```

Recursive traversals

```java
void pre(TreeNode n){ if(n==null) return; visit(n); pre(n.left); pre(n.right); }
void in(TreeNode n){ if(n==null) return; in(n.left); visit(n); in(n.right); }
void post(TreeNode n){ if(n==null) return; post(n.left); post(n.right); visit(n); }
```

Iterative inorder

```java
List<Integer> inorder(TreeNode root){
  List<Integer> out = new ArrayList<>();
  Deque<TreeNode> st = new ArrayDeque<>(); TreeNode cur = root;
  while (cur != null || !st.isEmpty()) { while (cur != null) { st.push(cur); cur = cur.left; }
    cur = st.pop(); out.add(cur.val); cur = cur.right; }
  return out;
}
```

BFS level order

```java
List<List<Integer>> levelOrder(TreeNode root){
  List<List<Integer>> res = new ArrayList<>(); if(root==null) return res;
  Deque<TreeNode> q = new ArrayDeque<>(); q.add(root);
  while(!q.isEmpty()){
    int sz = q.size(); List<Integer> lev = new ArrayList<>(sz);
    for(int i=0;i<sz;i++){ TreeNode n = q.poll(); lev.add(n.val);
      if(n.left!=null) q.add(n.left); if(n.right!=null) q.add(n.right);
    }
    res.add(lev);
  }
  return res;
}
```

## Graph

Adjacency list and BFS/DFS

```java
List<List<Integer>> g = new ArrayList<>();
for(int i=0;i<N;i++) g.add(new ArrayList<>());
for(int[] e : edges){ g.get(e[0]).add(e[1]); g.get(e[1]).add(e[0]); }

void dfs(int u, int p){ for(int v : g.get(u)) if(v!=p) dfs(v, u); }

List<Integer> bfs(int s){
  List<Integer> order = new ArrayList<>(); boolean[] vis = new boolean[N];
  Deque<Integer> q = new ArrayDeque<>(); q.add(s); vis[s]=true;
  while(!q.isEmpty()){ int u=q.poll(); order.add(u);
    for(int v: g.get(u)) if(!vis[v]){ vis[v]=true; q.add(v);} }
  return order;
}
```

## PriorityQueue

```java
PriorityQueue<Integer> min = new PriorityQueue<>();
PriorityQueue<Integer> max = new PriorityQueue<>(Comparator.reverseOrder());

int[] three = Arrays.stream(nums).boxed()
  .sorted(Comparator.reverseOrder()).limit(3).mapToInt(x->x).toArray();

PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[0]));
```

Top K frequent

```java
int[] topKFrequent(int[] nums, int k){
  Map<Integer,Integer> cnt = new HashMap<>();
  for(int x: nums) cnt.put(x, cnt.getOrDefault(x,0)+1);
  PriorityQueue<Map.Entry<Integer,Integer>> pq =
    new PriorityQueue<>(Map.Entry.comparingByValue());
  for(var e: cnt.entrySet()){ pq.offer(e); if(pq.size()>k) pq.poll(); }
  int[] res = new int[pq.size()]; int i=0; while(!pq.isEmpty()) res[i++]=pq.poll().getKey();
  return res;
}
```

## Lambda

```java
int best = Arrays.stream(new int[]{a,b}).boxed()
  .min(Comparator.comparingInt(x -> Math.abs(target - x))).get();
```

## Zip

```java
for (int i = 0; i < Math.min(A.size(), B.size()); i++) {
  var a = A.get(i); var b = B.get(i);
}
```

Rotate matrix using transpose+reverse

```java
void rotate(int[][] m){ int n=m.length; for(int i=0;i<n;i++) for(int j=i+1;j<n;j++){int t=m[i][j];m[i][j]=m[j][i];m[j][i]=t;} for(int i=0;i<n;i++) for(int l=0,r=n-1;l<r;l++,r--){int t=m[i][l];m[i][l]=m[i][r];m[i][r]=t;} }
```

## Random

```java
int r = ThreadLocalRandom.current().nextInt(lo, hi); // [lo,hi)
Collections.shuffle(list);
```

## Constants

```java
int INF = Integer.MAX_VALUE; int NINF = Integer.MIN_VALUE;
long LINF = Long.MAX_VALUE; long LNINF = Long.MIN_VALUE;
```

## Ternary

```java
int x = cond ? a : b;
```

## Bitwise Operators

```java
int andv = (0b1100 & 0b1010);
int orv = (0b1100 | 0b1010);
int xrv = (0b1100 ^ 0b1010);
int shr = (0b1100 >> 2);
int shl = (0b0011 << 2);
int ushr = (-1 >>> 1);
```

## For Else

```java
boolean broken = false;
for(int i=0;i<n;i++){ if(cond){ broken=true; break; } }
if(!broken){ /* no break */ }
```

## Modulo

```java
int mod(int a, int m){ int r = a % m; return r < 0 ? r + m : r; }
```

## Any

```java
boolean any = Arrays.stream(nums).anyMatch(x -> x > 0);
```

## All

```java
boolean all = Arrays.stream(nums).allMatch(x -> x >= 0);
```

## Bisect

```java
int idx = Arrays.binarySearch(arr, target); // >=0 found; else (-(ins)-1)

int lowerBound(int[] a, int x){ int l=0,r=a.length; while(l<r){ int m=(l+r)/2; if(a[m] < x) l=m+1; else r=m; } return l; }
int upperBound(int[] a, int x){ int l=0,r=a.length; while(l<r){ int m=(l+r)/2; if(a[m] <= x) l=m+1; else r=m; } return l; }
```

## Math

```java
long p = (long) (Math.pow(a, b)) % mod;
long q = Math.floorDiv(a, b); long rem = Math.floorMod(a, b);
```

## iter

```java
Iterator<Integer> it = list.iterator();
while(it.hasNext()){ int x = it.next(); }
```

## Map

```java
List<String> up = list.stream().map(String::toUpperCase).toList();
```

## Filter

```java
List<Integer> over75 = scores.stream().filter(x -> x > 75).toList();
```

## Reduce

```java
int sum = Arrays.stream(nums).reduce(0, Integer::sum);
```

## Regular Expression

```java
String out = s.replaceAll("[aeiou]", "");
```

## Types

```java
List<List<Integer>> grid = new ArrayList<>();
Map<Integer,List<Integer>> adj = new HashMap<>();
```

## Grids

```java
int R = grid.length, C = grid[0].length;
int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
void dfs(int r,int c){ grid[r][c]=2; for(int[] d:dirs){int nr=r+d[0], nc=c+d[1]; if(0<=nr&&nr<R&&0<=nc&&nc<C && grid[nr][nc]==1) dfs(nr,nc);} }
```

# Collections

## Deque

```java
Deque<Integer> dq = new ArrayDeque<>();
dq.addFirst(5); dq.addLast(6); dq.removeFirst(); dq.removeLast();
```

## Counter

```java
int[] cnt = new int[26];
for(char ch : s.toCharArray()) cnt[ch - 'a']++;
```

Top-K with counter

```java
List<Integer> topK(int[] nums, int k){
  Map<Integer,Integer> map = new HashMap<>(); for(int x:nums) map.put(x, map.getOrDefault(x,0)+1);
  return map.entrySet().stream()
    .sorted((a,b)->b.getValue()-a.getValue()).limit(k)
    .map(Map.Entry::getKey).toList();
}
```

## Default Dict

```java
Map<Integer,List<Integer>> dd = new HashMap<>();
dd.computeIfAbsent(1, z -> new ArrayList<>()).add(2);
```

# Algorithms

## General Tips

- Clarify, brute force, optimize, code, test.

## Binary Search

```java
int firstBadVersion(int n){
  int l=1,r=n;
  while(l<r){ int m=l+(r-l)/2; if(isBad(m)) r=m; else l=m+1; }
  return l;
}
```

Sqrt template

```java
int mySqrt(int x){
  if(x<=1) return x; int l=1,r=x; while(l<r){ int m=l+(r-l)/2; if((long)m*m>x) r=m; else l=m+1; } return l-1;
}
```

## Binary Search Tree

Complete tree check by index

```java
boolean isComplete(TreeNode root){
  long[] total = {0}, mx = {Long.MIN_VALUE};
  dfs(root,1,total,mx); return total[0]==mx[0];
}
void dfs(TreeNode n,long idx,long[] total,long[] mx){ if(n==null) return; total[0]++; mx[0]=Math.max(mx[0],idx); dfs(n.left,idx*2,total,mx); dfs(n.right,idx*2+1,total,mx); }
```

Range sum

```java
int rangeSumBST(TreeNode root, int L, int R){ if(root==null) return 0; int s=0; if(L<=root.val && root.val<=R) s+=root.val; if(root.val>L) s+=rangeSumBST(root.left,L,R); if(root.val<R) s+=rangeSumBST(root.right,L,R); return s; }
```

Validate BST (iterative)

```java
boolean isValidBST(TreeNode root){
  Deque<TreeNode> st = new ArrayDeque<>(); TreeNode cur=root; Long prev=null;
  while(cur!=null || !st.isEmpty()){
    while(cur!=null){ st.push(cur); cur=cur.left; }
    cur=st.pop(); if(prev!=null && cur.val<=prev) return false; prev=(long)cur.val; cur=cur.right;
  }
  return true;
}
```

## Topological Sort

```java
boolean canFinish(int n, int[][] pre){
  List<List<Integer>> adj = new ArrayList<>(); for(int i=0;i<n;i++) adj.add(new ArrayList<>());
  int[] deg = new int[n];
  for(int[] e: pre){ adj.get(e[1]).add(e[0]); deg[e[0]]++; }
  Deque<Integer> q = new ArrayDeque<>(); for(int i=0;i<n;i++) if(deg[i]==0) q.add(i);
  int seen=0; while(!q.isEmpty()){ int u=q.poll(); seen++; for(int v: adj.get(u)) if(--deg[v]==0) q.add(v); }
  return seen==n;
}
```

Alien dictionary

```java
String alienOrder(String[] words){
  Set<Character> nodes = new HashSet<>(); for(String w:words) for(char c:w.toCharArray()) nodes.add(c);
  Map<Character,List<Character>> adj = new HashMap<>(); Map<Character,Integer> deg = new HashMap<>();
  for(char c:nodes){ adj.put(c,new ArrayList<>()); deg.put(c,0); }
  for(int i=0;i+1<words.length;i++){
    String a=words[i], b=words[i+1];
    int m=Math.min(a.length(), b.length()); boolean diff=false;
    for(int j=0;j<m;j++) if(a.charAt(j)!=b.charAt(j)){ char u=a.charAt(j), v=b.charAt(j); adj.get(u).add(v); deg.put(v,deg.get(v)+1); diff=true; break; }
    if(!diff && a.length()>b.length()) return "";
  }
  Deque<Character> q = new ArrayDeque<>(); for(var e:deg.entrySet()) if(e.getValue()==0) q.add(e.getKey());
  StringBuilder sb=new StringBuilder(); while(!q.isEmpty()){ char u=q.poll(); sb.append(u); for(char v: adj.get(u)){ deg.put(v,deg.get(v)-1); if(deg.get(v)==0) q.add(v);} }
  return sb.length()==nodes.size()? sb.toString() : "";
}
```

## Sliding Window

Template

```java
int lengthOfLongestSubstring(String s){
  int[] last = new int[256]; Arrays.fill(last, -1);
  int best=0, l=0; for(int r=0;r<s.length();r++){ char c=s.charAt(r); if(last[c]>=l) l=last[c]+1; last[c]=r; best=Math.max(best, r-l+1); } return best;
}
```

Fruits into baskets (2 types)

```java
int totalFruit(int[] f){
  Map<Integer,Integer> cnt=new HashMap<>(); int l=0,ans=0;
  for(int r=0;r<f.length;r++){ cnt.put(f[r], cnt.getOrDefault(f[r],0)+1);
    while(cnt.size()>2){ int x=f[l++]; cnt.put(x,cnt.get(x)-1); if(cnt.get(x)==0) cnt.remove(x); }
    ans=Math.max(ans,r-l+1);
  } return ans;
}
```

## Greedy (sample)

Increasing triplet

```java
boolean increasingTriplet(int[] nums){
  int a=Integer.MAX_VALUE, b=Integer.MAX_VALUE; for(int x:nums){ if(x<=a) a=x; else if(x<=b) b=x; else return true; } return false;
}
```

## Tree Tricks

Max ancestor diff

```java
int maxAncestorDiff(TreeNode root){
  int[] ans={0};
  dfs(root, Integer.MAX_VALUE, Integer.MIN_VALUE, ans); return ans[0];
}
void dfs(TreeNode n,int mn,int mx,int[] ans){ if(n==null){ ans[0]=Math.max(ans[0], Math.abs(mx-mn)); return; } dfs(n.left, Math.min(mn,n.val), Math.max(mx,n.val), ans); dfs(n.right, Math.min(mn,n.val), Math.max(mx,n.val), ans); }
```

Diameter

```java
int diameterOfBinaryTree(TreeNode root){ int[] best={0}; depth(root,best); return best[0]; }
int depth(TreeNode n,int[] best){ if(n==null) return 0; int l=depth(n.left,best), r=depth(n.right,best); best[0]=Math.max(best[0], l+r); return Math.max(l,r)+1; }
```

## Anagrams

```java
boolean isAnagram(String s, String t){ if(s.length()!=t.length()) return false; int[] c=new int[26]; for(char ch:s.toCharArray()) c[ch-'a']++; for(char ch:t.toCharArray()) if(--c[ch-'a']<0) return false; return true; }
```

Find all anagram indices (sliding window)

```java
List<Integer> findAnagrams(String s, String p){
  int[] need=new int[26]; for(char ch:p.toCharArray()) need[ch-'a']++;
  int[] have=new int[26]; List<Integer> ans=new ArrayList<>(); int m=p.length();
  for(int i=0;i<s.length();i++){
    have[s.charAt(i)-'a']++;
    if(i>=m) have[s.charAt(i-m)-'a']--;
    if(Arrays.equals(need, have)) ans.add(i-m+1);
  } return ans;
}
```

## Dynamic Programming

Coin change

```java
int coinChange(int[] coins, int amount){ int INF=1_000_000_000; int[] dp=new int[amount+1]; Arrays.fill(dp, INF); dp[0]=0; for(int c:coins) for(int a=c;a<=amount;a++) dp[a]=Math.min(dp[a], dp[a-c]+1); return dp[amount]>=INF?-1:dp[amount]; }
```

LCS length

```java
int lcs(String a, String b){ int n=a.length(), m=b.length(); int[][] dp=new int[n+1][m+1]; for(int i=0;i<n;i++) for(int j=0;j<m;j++) dp[i+1][j+1]=a.charAt(i)==b.charAt(j)?dp[i][j]+1:Math.max(dp[i][j+1], dp[i+1][j]); return dp[n][m]; }
```

## Cyclic Sort

```java
int[] cyclicSort(int[] nums){ int i=0; while(i<nums.length){ int j=nums[i]-1; if(nums[i]!=nums[j]){ int t=nums[i]; nums[i]=nums[j]; nums[j]=t; } else i++; } return nums; }
```

## Quick Sort

```java
void quickSort(int[] a){ sort(a,0,a.length-1); }
void sort(int[] a,int l,int r){ if(l>=r) return; int p=part(a,l,r); sort(a,l,p-1); sort(a,p+1,r); }
int part(int[] a,int l,int r){ int pivot=a[r], i=l; for(int k=l;k<r;k++) if(a[k]<pivot){ int t=a[k]; a[k]=a[i]; a[i]=t; i++; } int t=a[r]; a[r]=a[i]; a[i]=t; return i; }
```

## Merge Sort

```java
int[] mergeSort(int[] a){ if(a.length<=1) return a; int m=a.length/2; int[] L=mergeSort(Arrays.copyOfRange(a,0,m)); int[] R=mergeSort(Arrays.copyOfRange(a,m,a.length)); return merge(L,R); }
int[] merge(int[] L,int[] R){ int i=0,j=0; int[] res=new int[L.length+R.length]; int k=0; while(i<L.length && j<R.length) res[k++]= L[i]<=R[j]? L[i++]:R[j++]; while(i<L.length) res[k++]=L[i++]; while(j<R.length) res[k++]=R[j++]; return res; }
```

## Merge Arrays

```java
int[] mergeKSortedArrays(List<int[]> arrays){ PriorityQueue<int[]> pq=new PriorityQueue<>(Comparator.comparingInt(a->a[0])); for(int i=0;i<arrays.size();i++) if(arrays.get(i).length>0) pq.add(new int[]{arrays.get(i)[0], i, 0}); List<Integer> res=new ArrayList<>(); while(!pq.isEmpty()){ int[] cur=pq.poll(); res.add(cur[0]); int i=cur[1], j=cur[2]+1; if(j<arrays.get(i).length) pq.add(new int[]{arrays.get(i)[j], i, j}); } return res.stream().mapToInt(x->x).toArray(); }
```

Merge K Lists (LeetCode ListNode)

```java
ListNode mergeKLists(ListNode[] lists){ PriorityQueue<ListNode> pq=new PriorityQueue<>(Comparator.comparingInt(n->n.val)); for(ListNode node:lists) if(node!=null) pq.add(node); ListNode dummy=new ListNode(0), cur=dummy; while(!pq.isEmpty()){ ListNode n=pq.poll(); cur.next=n; cur=cur.next; if(n.next!=null) pq.add(n.next); } return dummy.next; }
```

## Linked List

Reverse

```java
ListNode reverse(ListNode head){ ListNode prev=null,cur=head; while(cur!=null){ ListNode nxt=cur.next; cur.next=prev; prev=cur; cur=nxt; } return prev; }
```

Merge two lists

```java
ListNode mergeTwoLists(ListNode a, ListNode b){ ListNode d=new ListNode(0), p=d; while(a!=null && b!=null){ if(a.val<b.val){ p.next=a; a=a.next; } else { p.next=b; b=b.next; } p=p.next; } p.next = (a!=null? a:b); return d.next; }
```

## Convert Base

```java
String toHex(int num){ if(num==0) return "0"; long x=num<0? (num & 0xffffffffL): num; char[] idx="0123456789abcdef".toCharArray(); StringBuilder sb=new StringBuilder(); while(x>0){ int d=(int)(x%16); sb.append(idx[d]); x/=16; } return sb.reverse().toString(); }
```

## Parenthesis

Count-only

```java
boolean isValidPar(String s){ int c=0; for(char ch:s.toCharArray()){ if(ch=='(') c++; else if(ch==')'){ c--; if(c<0) return false; } } return c==0; }
```

Stack-based

```java
boolean isValid(String s){ Deque<Character> st=new ArrayDeque<>(); Map<Character,Character> mp=Map.of(')', '(', '}', '{', ']', '['); for(char c: s.toCharArray()){ if(mp.containsValue(c)) st.push(c); else if(mp.containsKey(c)){ if(st.isEmpty() || st.pop()!=mp.get(c)) return false; } } return st.isEmpty(); }
```

Remove to make valid

```java
String minRemoveToMakeValid(String s){ StringBuilder sb=new StringBuilder(s); Deque<Integer> st=new ArrayDeque<>(); boolean[] del=new boolean[s.length()]; for(int i=0;i<s.length();i++){ char c=s.charAt(i); if(c=='(') st.push(i); else if(c==')'){ if(!st.isEmpty()) st.pop(); else del[i]=true; } } while(!st.isEmpty()) del[st.pop()]=true; StringBuilder ans=new StringBuilder(); for(int i=0;i<s.length();i++) if(!del[i]) ans.append(s.charAt(i)); return ans.toString(); }
```

## Max Profit Stock

Infinite transactions

```java
int maxProfit(int[] prices){ int t0=0, t1=Integer.MIN_VALUE; for(int p:prices){ int t0old=t0; t0=Math.max(t0, t1+p); t1=Math.max(t1, t0old-p); } return t0; }
```

Single transaction

```java
int maxProfit1(int[] prices){ int t0=0, t1=Integer.MIN_VALUE; for(int p:prices){ t0=Math.max(t0, t1+p); t1=Math.max(t1, -p); } return t0; }
```

K transactions

```java
int maxProfitK(int k, int[] prices){ int n=prices.length; int[] t0=new int[k+1], t1=new int[k+1]; Arrays.fill(t1, Integer.MIN_VALUE/4); for(int p:prices){ for(int i=k;i>=1;i--){ t0[i]=Math.max(t0[i], t1[i]+p); t1[i]=Math.max(t1[i], t0[i-1]-p); } } return t0[k]; }
```

## Shift Array Right

```java
void rotate(int[] a, int k){ int n=a.length; k%=n; rev(a,0,n-1); rev(a,0,k-1); rev(a,k,n-1); }
void rev(int[] a,int l,int r){ while(l<r){ int t=a[l]; a[l]=a[r]; a[r]=t; l++; r--; } }
```

## Continuous Subarrays with Sum k

```java
int subarraySum(int[] nums, int k){ Map<Integer,Integer> mp=new HashMap<>(); mp.put(0,1); int ans=0,sum=0; for(int x:nums){ sum+=x; ans+= mp.getOrDefault(sum-k,0); mp.put(sum, mp.getOrDefault(sum,0)+1); } return ans; }
```

## Events

```java
List<int[]> employeeFreeTime(List<List<int[]>> schedule){ List<int[]> ev=new ArrayList<>(); for(var e:schedule) for(int[] m:e){ ev.add(new int[]{m[0],1}); ev.add(new int[]{m[1],-1}); } ev.sort(Comparator.comparingInt(a->a[0])); List<int[]> itv=new ArrayList<>(); Integer prev=null; int bal=0; for(int[] e:ev){ int t=e[0], c=e[1]; if(bal==0 && prev!=null && t!=prev) itv.add(new int[]{prev,t}); bal+=c; prev=t; } return itv; }
```

## Merge Meetings

```java
List<int[]> insert(int[][] intervals, int[] newI){ List<int[]> li=new ArrayList<>(Arrays.asList(intervals)); li.add(newI); li.sort(Comparator.comparingInt(a->a[0])); List<int[]> res=new ArrayList<>(); res.add(li.get(0)); for(int[] cur: li){ int[] last=res.get(res.size()-1); if(cur[0]<=last[1]) last[1]=Math.max(last[1], cur[1]); else res.add(cur); } return res; }
```

## Trie

```java
class Trie{
  static class Node{ Map<Character,Node> ch=new HashMap<>(); String word; }
  Node root=new Node();
  void add(String s){ Node t=root; for(char c:s.toCharArray()){ t=t.ch.computeIfAbsent(c,k->new Node()); } t.word=s; }
  List<String> matchPrefix(String p){ Node t=root; for(char c:p.toCharArray()){ if(!t.ch.containsKey(c)) return List.of(); t=t.ch.get(c);} List<String> res=new ArrayList<>(); collect(t,res); return res; }
  void collect(Node n,List<String> out){ if(n.word!=null) out.add(n.word); for(var e:n.ch.values()) collect(e,out); }
}
```

Search with '.' wildcard

```java
class WordDictionary{
  static class N{ Map<Character,N> ch=new HashMap<>(); boolean end; }
  N r=new N();
  void addWord(String w){ N t=r; for(char c:w.toCharArray()) t=t.ch.computeIfAbsent(c,k->new N()); t.end=true; }
  boolean search(String w){ return dfs(w,0,r); }
  boolean dfs(String w,int i,N n){ if(i==w.length()) return n.end; char c=w.charAt(i); if(c!='.') return n.ch.containsKey(c) && dfs(w,i+1,n.ch.get(c)); for(var e:n.ch.values()) if(dfs(w,i+1,e)) return true; return false; }
}
```

## Kadane

```java
int maxSubArray(int[] a){ int best=a[0]; for(int i=1;i<a.length;i++){ if(a[i-1]>0) a[i]+=a[i-1]; best=Math.max(best,a[i]); } return best; }
```

## Union Find

```java
class DSU{
  int[] p, sz;
  DSU(int n){ p=new int[n]; sz=new int[n]; for(int i=0;i<n;i++){ p[i]=i; sz[i]=1; } }
  int find(int x){ if(p[x]!=x) p[x]=find(p[x]); return p[x]; }
  boolean union(int a,int b){ int x=find(a), y=find(b); if(x==y) return false; if(sz[x]<sz[y]){ int t=x; x=y; y=t; } p[y]=x; sz[x]+=sz[y]; return true; }
}
```

## Fast Power

```java
double myPow(double x, int n){ long e=n; if(e<0){ x=1/x; e=-e; } double ans=1; while(e>0){ if((e&1)==1) ans*=x; x*=x; e>>=1; } return ans; }
```

## Fibonacci Golden

```java
int fib(int N){ double g=(1+Math.sqrt(5))/2.0; return (int)Math.round((Math.pow(g,N))/Math.sqrt(5)); }
```

## Basic Calculator

```java
int calculate(String s){ s=s+"$"; return (int)eval(new ArrayDeque<>(), s, 0)[0]; }
long[] eval(Deque<Long> st, String s, int i){ long num=0; char sign='+'; while(i<s.length()){ char c=s.charAt(i); if(c==' '){ i++; continue; } if(Character.isDigit(c)){ num=num*10+(c-'0'); i++; continue; } if(c=='('){ long[] r=eval(new ArrayDeque<>(), s, i+1); num=r[0]; i=(int)r[1]; c=s.charAt(i); }
  if(!Character.isDigit(c)){
    if(sign=='+') st.push(num);
    else if(sign=='-') st.push(-num);
    else if(sign=='*') st.push(st.pop()*num);
    else if(sign=='/') st.push(st.pop()/num);
    if(c==')') return new long[]{ st.stream().mapToLong(x->x).sum(), i+1 };
    sign=c; num=0; i++;
  }
 }
 return new long[]{ st.stream().mapToLong(x->x).sum(), i };
}
```

## Reverse Polish

```java
int evalRPN(List<String> tok){ Deque<Integer> st=new ArrayDeque<>(); for(String c: tok){ if(!"+-/*".contains(c)){ st.push(Integer.parseInt(c)); } else { int a=st.pop(), b=st.pop(); switch(c){ case "+": st.push(b+a); break; case "-": st.push(b-a); break; case "*": st.push(b*a); break; default: st.push(b/a); } } } return st.pop(); }
```

## Reservoir Sampling

```java
class Picker{ int[] nums; Picker(int[] a){ nums=a; } int pick(int target){ Integer res=null; int cnt=0; for(int i=0;i<nums.length;i++){ if(nums[i]==target){ cnt++; int chance=ThreadLocalRandom.current().nextInt(1, cnt+1); if(chance==1) res=i; } } return res; } }
```

## String Subsequence (shortestWay)

```java
int shortestWay(String src, String tgt){ Map<Character,List<Integer>> pos=new HashMap<>(); for(int i=0;i<src.length();i++) pos.computeIfAbsent(src.charAt(i),k->new ArrayList<>()).add(i); int ans=1, i=-1; for(char c: tgt.toCharArray()){ if(!pos.containsKey(c)) return -1; List<Integer> p=pos.get(c); int j=Collections.binarySearch(p, i); j = j<0 ? -j-1 : j; if(j==p.size()){ ans++; i=p.get(0)+1; } else { i=p.get(j)+1; } } return ans; }
```

## Candy Crush (remove duplicates)

```java
String removeDuplicates(String s, int k){ Deque<int[]> st=new ArrayDeque<>(); for(char c: s.toCharArray()){ if(!st.isEmpty() && st.peek()[0]==c){ st.peek()[1]++; if(st.peek()[1]==k) st.pop(); } else st.push(new int[]{c,1}); } StringBuilder sb=new StringBuilder(); while(!st.isEmpty()){ int[] t=st.removeLast(); for(int i=0;i<t[1];i++) sb.append((char)t[0]); } return sb.toString(); }
```

## Dutch Flag

```java
void sortColors(int[] a){ int p0=0, cur=0, p2=a.length-1; while(cur<=p2){ if(a[cur]==0){ int t=a[p0]; a[p0]=a[cur]; a[cur]=t; p0++; cur++; } else if(a[cur]==2){ int t=a[cur]; a[cur]=a[p2]; a[p2]=t; p2--; } else cur++; } }
```
