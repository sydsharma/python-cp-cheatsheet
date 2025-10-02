C# reference for interview coding problems/light competitive programming. Contributions welcome!

## How

Minimal snippets I actually use to solve LeetCode-style problems in C#.

## Why

Strong typing, solid performance, rich stdlib/LINQ, great for interviews.

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
1. [Dutch Flag](#dutch-flag)

# Language Mechanics

## Literals

```csharp
int a = 255; int b = 0b11111111; int c = 0xFF;
long L = 1234567890123L; double d = 1.23; decimal m = 1.23m; bool ok = true;
char ch = 'a'; string s = "hello\n"; object n = null;
int[] arr = new[]{1,2,3};
var list = new List<int>();
var dict = new Dictionary<string,int>();
var set = new HashSet<char>();
```

## Loops

```csharp
for (int i = 0; i < n; i++) {}
for (int i = n - 1; i >= 0; i--) {}
foreach (var x in nums) {}
int i = 0; while (i < n) { i++; }
```

Reverse in-place

```csharp
int l = 0, r = nums.Length - 1;
while (l < r) { (nums[l], nums[r]) = (nums[r], nums[l]); l++; r--; }
```

Ranges

```csharp
for (int i = 0; i < 3; i++) {}
for (int i = 3; i >= 0; i--) {}
```

## Strings

```csharp
int i1 = s.IndexOf('x');
int j1 = s.LastIndexOf('x');
string[] tokens = line.Split(':');
string joined = string.Join(" ", words);
var sb = new StringBuilder(); sb.Append("a").Append(1);
char c0 = s[0];
bool up = char.IsUpper(c0);
bool low = char.IsLower(c0);
bool dig = char.IsDigit(c0);
string t = s.Replace("()", "");
bool st = s.StartsWith("pre"); bool ed = s.EndsWith("suf");
string f = $"My name is {name}, I'm {age}";
```

Manual split by IsLetter

```csharp
List<string> SplitWords(string input){
  var outp = new List<string>();
  int start = -1;
  for(int i=0;i<input.Length;i++){
    char ch = input[i];
    if(char.IsLetter(ch)){ if(start==-1) start=i; }
    else { if(start!=-1){ outp.Add(input.Substring(start, i-start)); start=-1; } }
  }
  if(start!=-1) outp.Add(input.Substring(start));
  return outp;
}
```

## Slicing

```csharp
string sub = s.Substring(2, 2);
int[] subArr = arr[2..5];
```

## Tuple

```csharp
(int first, int second) p = (2, 3);
```

## Sort

```csharp
Array.Sort(nums);
Array.Sort(words, (x,y) => x.Length.CompareTo(y.Length));
list.Sort();
list.Sort((x,y) => x[1].CompareTo(y[1]));

var m = new Dictionary<string,int>();
var e = m.ToList();
e.Sort((a,b) => a.Value.CompareTo(b.Value));
```

Keep original indices

```csharp
var idxVal = nums.Select((v,i) => (i,v)).OrderBy(x => x.v).ToArray();
```

## Hash

```csharp
var ht = new Dictionary<char,int>();
foreach (var ch in s){ ht[ch] = ht.TryGetValue(ch, out var v) ? v+1 : 1; }
```

## Set

```csharp
var st = new HashSet<int>();
st.Add(a); st.Remove(a); bool has = st.Contains(a);
int any = st.First();
```

## List

```csharp
var list = Enumerable.Repeat(0, 5).ToList();
var grid = new List<List<int>>();
grid.Add(new List<int>());
grid[0].Add(1);
list.Reverse();
var joinedList = new List<int>(list1); joinedList.AddRange(list2);
```

## Dict

```csharp
var d = new Dictionary<string,int>();
d["key"] = 1;
int v = d.TryGetValue("key", out var vv) ? vv : 0;
foreach (var k in d.Keys){}
foreach (var (k,val) in d){}
d.TryAdd("k", 0);
d.Remove("k");
```

## BinaryTree

```csharp
class TreeNode{ public int val; public TreeNode left,right; public TreeNode(int v=0, TreeNode l=null, TreeNode r=null){ val=v; left=l; right=r; } }
```

Recursive traversals

```csharp
void Pre(TreeNode n){ if(n==null) return; Visit(n); Pre(n.left); Pre(n.right); }
void In(TreeNode n){ if(n==null) return; In(n.left); Visit(n); In(n.right); }
void Post(TreeNode n){ if(n==null) return; Post(n.left); Post(n.right); Visit(n); }
```

Iterative inorder

```csharp
List<int> Inorder(TreeNode root){
  var outp = new List<int>();
  var st = new Stack<TreeNode>();
  var cur = root;
  while(cur!=null || st.Count>0){
    while(cur!=null){ st.Push(cur); cur=cur.left; }
    cur = st.Pop(); outp.Add(cur.val); cur = cur.right;
  }
  return outp;
}
```

BFS level order

```csharp
List<List<int>> LevelOrder(TreeNode root){
  var res = new List<List<int>>(); if(root==null) return res;
  var q = new Queue<TreeNode>(); q.Enqueue(root);
  while(q.Count>0){
    int sz=q.Count; var lev=new List<int>(sz);
    for(int i=0;i<sz;i++){ var n=q.Dequeue(); lev.Add(n.val); if(n.left!=null) q.Enqueue(n.left); if(n.right!=null) q.Enqueue(n.right); }
    res.Add(lev);
  }
  return res;
}
```

## Graph

Adjacency list and BFS/DFS

```csharp
var g = Enumerable.Range(0, N).Select(_ => new List<int>()).ToArray();
foreach (var e in edges){ g[e[0]].Add(e[1]); g[e[1]].Add(e[0]); }

void Dfs(int u, int p){ foreach(var v in g[u]) if(v!=p) Dfs(v,u); }

List<int> Bfs(int s){ var order=new List<int>(); var vis=new bool[N]; var q=new Queue<int>(); q.Enqueue(s); vis[s]=true; while(q.Count>0){ var u=q.Dequeue(); order.Add(u); foreach(var v in g[u]) if(!vis[v]){ vis[v]=true; q.Enqueue(v);} } return order; }
```

## PriorityQueue

```csharp
var min = new PriorityQueue<int,int>();
min.Enqueue(3, 3); min.Enqueue(1, 1); min.Enqueue(2, 2);
int top = min.Dequeue();

var max = new PriorityQueue<int,int>(Comparer<int>.Create((a,b)=>b.CompareTo(a)));
```

Top K frequent

```csharp
int[] TopKFrequent(int[] nums, int k){
  var cnt = new Dictionary<int,int>(); foreach(var x in nums) cnt[x]=cnt.TryGetValue(x,out var v)? v+1:1;
  var pq = new PriorityQueue<int,int>();
  foreach(var kv in cnt){ pq.Enqueue(kv.Key, kv.Value); if(pq.Count>k) pq.Dequeue(); }
  var res = new List<int>(); while(pq.Count>0) res.Add(pq.Dequeue()); res.Reverse(); return res.ToArray();
}
```

## lambda

```csharp
int best = new[]{a,b}.OrderBy(x => Math.Abs(target - x)).First();
```

## zip

```csharp
foreach (var (a,b) in A.Zip(B)) { }
```

## Random

```csharp
var rng = new Random();
int r = rng.Next(lo, hi);

int[] Shuffle(int[] a){ for(int i=a.Length-1;i>0;i--){ int j=rng.Next(i+1); (a[i],a[j])=(a[j],a[i]); } return a; }
```

## Constants

```csharp
int INF = int.MaxValue; int NINF = int.MinValue;
long LINF = long.MaxValue; long LNINF = long.MinValue;
```

## Ternary

```csharp
int x = cond ? a : b;
```

## Bitwise Operators

```csharp
int andv = (0b1100 & 0b1010);
int orv = (0b1100 | 0b1010);
int xrv = (0b1100 ^ 0b1010);
int shr = (0b1100 >> 2);
int shl = (0b0011 << 2);
uint ushr = (uint.MaxValue >> 1);
```

## For Else

```csharp
bool broken=false; for(int i=0;i<n;i++){ if(cond){ broken=true; break; } } if(!broken){ /* no break */ }
```

## Modulo

```csharp
int Mod(int a,int m){ int r=a % m; return r<0? r+m : r; }
```

## any

```csharp
bool any = nums.Any(x => x > 0);
```

## all

```csharp
bool all = nums.All(x => x >= 0);
```

## Bisect

```csharp
int idx = Array.BinarySearch(arr, target);

int LowerBound(int[] a,int x){ int l=0,r=a.Length; while(l<r){ int m=(l+r)/2; if(a[m] < x) l=m+1; else r=m; } return l; }
int UpperBound(int[] a,int x){ int l=0,r=a.Length; while(l<r){ int m=(l+r)/2; if(a[m] <= x) l=m+1; else r=m; } return l; }
```

## math

```csharp
double p = Math.Pow(a, b) % mod;
long q = Math.DivRem(a, b, out var rem);
```

## iter

```csharp
var it = list.GetEnumerator(); while(it.MoveNext()){ var x = it.Current; }
```

## map

```csharp
var up = list.Select(s => s.ToUpper()).ToList();
```

## filter

```csharp
var over75 = scores.Where(x => x > 75).ToList();
```

## reduce

```csharp
int sum = nums.Aggregate(0, (a,b) => a + b);
```

## Regular Expression

```csharp
string outp = Regex.Replace(s, "[aeiou]", "");
```

## Types

```csharp
var grid = new List<List<int>>();
var adj = new Dictionary<int,List<int>>();
```

## Grids

```csharp
int R = grid.Count, C = grid[0].Count;
int[][] dirs = new[]{ new[]{1,0}, new[]{-1,0}, new[]{0,1}, new[]{0,-1} };
void Dfs(int r,int c){ grid[r][c]=2; foreach(var d in dirs){ int nr=r+d[0], nc=c+d[1]; if(0<=nr && nr<R && 0<=nc && nc<C && grid[nr][nc]==1) Dfs(nr,nc); } }
```

# Collections

## Deque

```csharp
var dq = new LinkedList<int>();
dq.AddFirst(5); dq.AddLast(6); dq.RemoveFirst(); dq.RemoveLast();
```

## Counter

```csharp
var cnt = new Dictionary<char,int>(); foreach(var ch in s){ cnt[ch]=cnt.TryGetValue(ch,out var v)? v+1:1; }
```

Top-K with counter

```csharp
List<int> TopK(int[] nums,int k){ var m=new Dictionary<int,int>(); foreach(var x in nums) m[x]=m.TryGetValue(x,out var v)? v+1:1; return m.OrderByDescending(e=>e.Value).Take(k).Select(e=>e.Key).ToList(); }
```

## Default Dict

```csharp
var dd = new Dictionary<int,List<int>>();
if(!dd.TryGetValue(1, out var lst)){ lst=new List<int>(); dd[1]=lst; }
lst.Add(2);
```

# Algorithms

## General Tips

- Clarify, brute force, optimize, code, test.

## Binary Search

```csharp
int FirstBadVersion(int n, Func<int,bool> IsBad){ int l=1,r=n; while(l<r){ int m=l+(r-l)/2; if(IsBad(m)) r=m; else l=m+1; } return l; }
```

Sqrt template

```csharp
int MySqrt(int x){ if(x<=1) return x; int l=1,r=x; while(l<r){ int m=l+(r-l)/2; if((long)m*m>x) r=m; else l=m+1; } return l-1; }
```

## Binary Search Tree

Complete tree check by index

```csharp
bool IsComplete(TreeNode root){ long total=0, mx=0; void D(TreeNode n,long idx){ if(n==null) return; total++; if(idx>mx) mx=idx; D(n.left, idx*2); D(n.right, idx*2+1); } D(root,1); return total==mx; }
```

Range sum

```csharp
int RangeSumBST(TreeNode root,int L,int R){ if(root==null) return 0; int s=0; void D(TreeNode n){ if(n==null) return; if(L<=n.val && n.val<=R) s+=n.val; if(n.val>L) D(n.left); if(n.val<R) D(n.right); } D(root); return s; }
```

Validate BST (iterative)

```csharp
bool IsValidBST(TreeNode root){ var st=new Stack<TreeNode>(); TreeNode cur=root; int? prev=null; while(cur!=null || st.Count>0){ while(cur!=null){ st.Push(cur); cur=cur.left; } cur=st.Pop(); if(prev!=null && cur.val<=prev) return false; prev=cur.val; cur=cur.right; } return true; }
```

## Topological Sort

```csharp
bool CanFinish(int n, int[][] pre){ var adj=Enumerable.Range(0,n).Select(_=>new List<int>()).ToArray(); var deg=new int[n]; foreach(var e in pre){ adj[e[1]].Add(e[0]); deg[e[0]]++; } var q=new Queue<int>(); for(int i=0;i<n;i++) if(deg[i]==0) q.Enqueue(i); int seen=0; while(q.Count>0){ var u=q.Dequeue(); seen++; foreach(var v in adj[u]) if(--deg[v]==0) q.Enqueue(v); } return seen==n; }
```

## Sliding Window

Longest substring without repeating

```csharp
int LengthOfLongestSubstring(string s){ var last = Enumerable.Repeat(-1,256).ToArray(); int best=0,l=0; for(int r=0;r<s.Length;r++){ int c=s[r]; if(last[c]>=l) l=last[c]+1; last[c]=r; best=Math.Max(best, r-l+1); } return best; }
```

## Greedy

Increasing triplet

```csharp
bool IncreasingTriplet(int[] nums){ int a=int.MaxValue, b=int.MaxValue; foreach(var x in nums){ if(x<=a) a=x; else if(x<=b) b=x; else return true; } return false; }
```

## Tree Tricks

Max ancestor diff

```csharp
int MaxAncestorDiff(TreeNode root){ int ans=0; void D(TreeNode n,int mn,int mx){ if(n==null){ ans=Math.Max(ans, Math.Abs(mx-mn)); return; } D(n.left, Math.Min(mn,n.val), Math.Max(mx,n.val)); D(n.right, Math.Min(mn,n.val), Math.Max(mx,n.val)); } D(root, int.MaxValue, int.MinValue); return ans; }
```

Diameter

```csharp
int DiameterOfBinaryTree(TreeNode root){ int best=0; int Depth(TreeNode n){ if(n==null) return 0; int l=Depth(n.left), r=Depth(n.right); best=Math.Max(best, l+r); return Math.Max(l,r)+1; } Depth(root); return best; }
```

## Anagrams

```csharp
bool IsAnagram(string s,string t){ if(s.Length!=t.Length) return false; var c=new int[26]; foreach(var ch in s) c[ch-'a']++; foreach(var ch in t) if(--c[ch-'a']<0) return false; return true; }
```

Find all anagram indices

```csharp
IList<int> FindAnagrams(string s,string p){ var need=new int[26]; foreach(var ch in p) need[ch-'a']++; var have=new int[26]; var ans=new List<int>(); int m=p.Length; for(int i=0;i<s.Length;i++){ have[s[i]-'a']++; if(i>=m) have[s[i-m]-'a']--; if(need.SequenceEqual(have)) ans.Add(i-m+1); } return ans; }
```

## Dynamic Programming

Coin change

```csharp
int CoinChange(int[] coins,int amount){ int INF=1_000_000_000; var dp=Enumerable.Repeat(INF, amount+1).ToArray(); dp[0]=0; foreach(var c in coins) for(int a=c;a<=amount;a++) dp[a]=Math.Min(dp[a], dp[a-c]+1); return dp[amount]>=INF? -1: dp[amount]; }
```

LCS length

```csharp
int Lcs(string a,string b){ int n=a.Length,m=b.Length; var dp=new int[n+1,m+1]; for(int i=0;i<n;i++) for(int j=0;j<m;j++) dp[i+1,j+1]= a[i]==b[j]? dp[i,j]+1: Math.Max(dp[i,j+1], dp[i+1,j]); return dp[n,m]; }
```

## Cyclic Sort

```csharp
int[] CyclicSort(int[] nums){ int i=0; while(i<nums.Length){ int j=nums[i]-1; if(nums[i]!=nums[j]){ (nums[i],nums[j])=(nums[j],nums[i]); } else i++; } return nums; }
```

## Quick Sort

```csharp
void QuickSort(int[] a){ Sort(a,0,a.Length-1); }
void Sort(int[] a,int l,int r){ if(l>=r) return; int p=Part(a,l,r); Sort(a,l,p-1); Sort(a,p+1,r); }
int Part(int[] a,int l,int r){ int pivot=a[r], i=l; for(int k=l;k<r;k++) if(a[k]<pivot){ (a[k],a[i])=(a[i],a[k]); i++; } (a[r],a[i])=(a[i],a[r]); return i; }
```

## Merge Sort

```csharp
int[] MergeSort(int[] a){ if(a.Length<=1) return a; int m=a.Length/2; var L=MergeSort(a[..m]); var R=MergeSort(a[m..]); return Merge(L,R); }
int[] Merge(int[] L,int[] R){ int i=0,j=0; var res=new int[L.Length+R.Length]; int k=0; while(i<L.Length && j<R.Length) res[k++]= L[i]<=R[j]? L[i++]:R[j++]; while(i<L.Length) res[k++]=L[i++]; while(j<R.Length) res[k++]=R[j++]; return res; }
```

## Merge Arrays

```csharp
int[] MergeKSortedArrays(List<int[]> arrays){ var pq=new PriorityQueue<(int val,int i,int j),int>(); for(int i=0;i<arrays.Count;i++) if(arrays[i].Length>0) pq.Enqueue((arrays[i][0], i, 0), arrays[i][0]); var res=new List<int>(); while(pq.Count>0){ var cur=pq.Dequeue(); res.Add(cur.val); int i=cur.i, j=cur.j+1; if(j<arrays[i].Length) pq.Enqueue((arrays[i][j], i, j), arrays[i][j]); } return res.ToArray(); }
```

## Linked List

```csharp
class ListNode{ public int val; public ListNode next; public ListNode(int v=0,ListNode n=null){ val=v; next=n; } }

ListNode Reverse(ListNode head){ ListNode prev=null,cur=head; while(cur!=null){ var nxt=cur.next; cur.next=prev; prev=cur; cur=nxt; } return prev; }

ListNode MergeTwoLists(ListNode a,ListNode b){ var d=new ListNode(0); var p=d; while(a!=null && b!=null){ if(a.val<b.val){ p.next=a; a=a.next; } else { p.next=b; b=b.next; } p=p.next; } p.next = a??b; return d.next; }
```

## Convert Base

```csharp
string ToHex(int num){ if(num==0) return "0"; uint x = (uint)num; const string idx="0123456789abcdef"; var sb=new StringBuilder(); while(x>0){ int d=(int)(x%16); sb.Append(idx[d]); x/=16; } var arr=sb.ToString().ToCharArray(); Array.Reverse(arr); return new string(arr); }
```

## Parenthesis

Count-only

```csharp
bool IsValidPar(string s){ int c=0; foreach(var ch in s){ if(ch=='(') c++; else if(ch==')'){ c--; if(c<0) return false; } } return c==0; }
```

Stack-based

```csharp
bool IsValid(string s){ var st=new Stack<char>(); var mp=new Dictionary<char,char>{{')','('},{'}','{'},{']','['}}; foreach(var c in s){ if(mp.ContainsValue(c)) st.Push(c); else if(mp.ContainsKey(c)){ if(st.Count==0 || st.Pop()!=mp[c]) return false; } } return st.Count==0; }
```

Remove to make valid

```csharp
string MinRemoveToMakeValid(string s){ var del=new bool[s.Length]; var st=new Stack<int>(); for(int i=0;i<s.Length;i++){ char c=s[i]; if(c=='(') st.Push(i); else if(c==')'){ if(st.Count>0) st.Pop(); else del[i]=true; } } while(st.Count>0) del[st.Pop()]=true; var sb=new StringBuilder(); for(int i=0;i<s.Length;i++) if(!del[i]) sb.Append(s[i]); return sb.ToString(); }
```

## Max Profit Stock

Infinite transactions

```csharp
int MaxProfit(int[] prices){ int t0=0, t1=int.MinValue/4; foreach(var p in prices){ int t0old=t0; t0=Math.Max(t0, t1+p); t1=Math.Max(t1, t0old-p); } return t0; }
```

Single transaction

```csharp
int MaxProfit1(int[] prices){ int t0=0, t1=int.MinValue/4; foreach(var p in prices){ t0=Math.Max(t0, t1+p); t1=Math.Max(t1, -p); } return t0; }
```

K transactions

```csharp
int MaxProfitK(int k, int[] prices){ var t0=new int[k+1]; var t1=Enumerable.Repeat(int.MinValue/4, k+1).ToArray(); foreach(var p in prices){ for(int i=k;i>=1;i--){ t0[i]=Math.Max(t0[i], t1[i]+p); t1[i]=Math.Max(t1[i], t0[i-1]-p); } } return t0[k]; }
```

## Shift Array Right

```csharp
void Rotate(int[] a,int k){ int n=a.Length; k%=n; Rev(a,0,n-1); Rev(a,0,k-1); Rev(a,k,n-1); }
void Rev(int[] a,int l,int r){ while(l<r){ (a[l],a[r])=(a[r],a[l]); l++; r--; } }
```

## Continuous Subarrays with Sum k

```csharp
int SubarraySum(int[] nums,int k){ var mp=new Dictionary<int,int>{{0,1}}; int ans=0,sum=0; foreach(var x in nums){ sum+=x; ans += mp.TryGetValue(sum-k, out var v)? v:0; mp[sum]= mp.TryGetValue(sum, out var vv)? vv+1:1; } return ans; }
```

## Events

```csharp
List<int[]> EmployeeFreeTime(List<List<int[]>> schedule){ var ev=new List<int[]>(); foreach(var e in schedule) foreach(var m in e){ ev.Add(new[]{m[0],1}); ev.Add(new[]{m[1],-1}); } ev.Sort((a,b)=>a[0].CompareTo(b[0])); var itv=new List<int[]>(); int? prev=null; int bal=0; foreach(var e in ev){ int t=e[0], c=e[1]; if(bal==0 && prev!=null && t!=prev) itv.Add(new[]{prev.Value,t}); bal+=c; prev=t; } return itv; }
```

## Merge Meetings

```csharp
List<int[]> Insert(int[][] intervals,int[] newI){ var li=intervals.ToList(); li.Add(newI); li.Sort((a,b)=>a[0].CompareTo(b[0])); var res=new List<int[]> { li[0] }; foreach(var cur in li){ var last=res[^1]; if(cur[0]<=last[1]) last[1]=Math.Max(last[1], cur[1]); else res.Add(cur); } return res; }
```

## Trie

```csharp
class Trie{
  class Node{ public Dictionary<char,Node> ch=new(); public string word; }
  Node root=new();
  public void Add(string s){ var t=root; foreach(var c in s){ t = t.ch.TryGetValue(c, out var nx)? nx: (t.ch[c]=new Node()); } t.word=s; }
  public List<string> MatchPrefix(string p){ var t=root; foreach(var c in p){ if(!t.ch.ContainsKey(c)) return new(); t=t.ch[c]; } var res=new List<string>(); void Collect(Node n){ if(n.word!=null) res.Add(n.word); foreach(var e in n.ch.Values) Collect(e); } Collect(t); return res; }
}
```

Search with '.' wildcard

```csharp
class WordDictionary{
  class N{ public Dictionary<char,N> ch=new(); public bool end; }
  N r=new();
  public void AddWord(string w){ var t=r; foreach(var c in w){ if(!t.ch.ContainsKey(c)) t.ch[c]=new N(); t=t.ch[c]; } t.end=true; }
  public bool Search(string w){ bool D(int i,N n){ if(i==w.Length) return n.end; char c=w[i]; if(c!='.') return n.ch.ContainsKey(c) && D(i+1, n.ch[c]); foreach(var e in n.ch.Values) if(D(i+1,e)) return true; return false; } return D(0,r); }
}
```

## Kadane

```csharp
int MaxSubArray(int[] a){ int best=a[0]; for(int i=1;i<a.Length;i++){ if(a[i-1]>0) a[i]+=a[i-1]; best=Math.Max(best,a[i]); } return best; }
```

## Union Find

```csharp
class DSU{
  int[] p, sz;
  public DSU(int n){ p=new int[n]; sz=new int[n]; for(int i=0;i<n;i++){ p[i]=i; sz[i]=1; } }
  int Find(int x){ if(p[x]!=x) p[x]=Find(p[x]); return p[x]; }
  public bool Union(int a,int b){ int x=Find(a), y=Find(b); if(x==y) return false; if(sz[x]<sz[y]) (x,y)=(y,x); p[y]=x; sz[x]+=sz[y]; return true; }
}
```

## Fast Power

```csharp
double MyPow(double x,long n){ long e=n; if(e<0){ x=1/x; e=-e; } double ans=1; while(e>0){ if((e&1)==1) ans*=x; x*=x; e>>=1; } return ans; }
```

## Fibonacci Golden

```csharp
int Fib(int N){ double g=(1+Math.Sqrt(5))/2.0; return (int)Math.Round(Math.Pow(g,N)/Math.Sqrt(5)); }
```

## Basic Calculator

```csharp
int Calculate(string s){ s+="$"; (long sum,int i) Eval(int i){ var st=new Stack<long>(); char sign='+'; long num=0; while(i<s.Length){ char c=s[i]; if(c==' '){ i++; continue; } if(char.IsDigit(c)){ num=num*10+(c-'0'); i++; continue; } if(c=='('){ var r=Eval(i+1); num=r.sum; i=r.i; c=s[i]; }
    if(!char.IsDigit(c)){
      if(sign=='+') st.Push(num);
      else if(sign=='-') st.Push(-num);
      else if(sign=='*') st.Push(st.Pop()*num);
      else if(sign=='/') st.Push(st.Pop()/num);
      if(c==')') return (st.Sum(x=>x), i+1);
      sign=c; num=0; i++;
    }
  }
  return (int)st.Sum(x=>x);
}
```

## Reverse Polish

```csharp
int EvalRPN(IList<string> tok){ var st=new Stack<int>(); foreach(var c in tok){ if(!"+-/*".Contains(c)){ st.Push(int.Parse(c)); } else { int a=st.Pop(), b=st.Pop(); st.Push(c switch { "+" => b+a, "-" => b-a, "*" => b*a, _ => b/a }); } } return st.Pop(); }
```

## Reservoir Sampling

```csharp
class Picker{ int[] nums; Random rng=new(); public Picker(int[] a){ nums=a; } public int Pick(int target){ int? res=null; int cnt=0; for(int i=0;i<nums.Length;i++){ if(nums[i]==target){ cnt++; int chance=rng.Next(1, cnt+1); if(chance==1) res=i; } } return res??-1; } }
```

## String Subsequence (shortestWay)

```csharp
int ShortestWay(string src,string tgt){ var pos=new Dictionary<char,List<int>>(); for(int i=0;i<src.Length;i++){ char c=src[i]; if(!pos.ContainsKey(c)) pos[c]=new List<int>(); pos[c].Add(i); } int ans=1, idx=-1; foreach(var c in tgt){ if(!pos.ContainsKey(c)) return -1; var arr=pos[c]; int j=arr.BinarySearch(idx); j = j<0 ? ~j : j; if(j==arr.Count){ ans++; idx=arr[0]+1; } else { idx=arr[j]+1; } } return ans; }
```

## Candy Crush (remove duplicates)

```csharp
string RemoveDuplicates(string s,int k){ var st=new Stack<(char ch,int cnt)>(); foreach(var c in s){ if(st.Count>0 && st.Peek().ch==c){ var t=st.Pop(); t.cnt++; if(t.cnt<k) st.Push(t); } else st.Push((c,1)); } var arr=st.Reverse().SelectMany(t=>Enumerable.Repeat(t.ch, t.cnt)).ToArray(); return new string(arr); }
```

## Dutch Flag

```csharp
void SortColors(int[] a){ int p0=0, cur=0, p2=a.Length-1; while(cur<=p2){ if(a[cur]==0){ (a[p0],a[cur])=(a[cur],a[p0]); p0++; cur++; } else if(a[cur]==2){ (a[cur],a[p2])=(a[p2],a[cur]); p2--; } else cur++; } }
```
