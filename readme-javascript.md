JavaScript reference for interview coding problems/light competitive programming. Contributions welcome!

## How

Minimal snippets I actually use to solve LeetCode-style problems in JavaScript.

## Why

Fast iteration, expressive syntax, rich built-ins, works well for interviews.

[Language Mechanics](#language-mechanics)

1. [Literals](#literals)
1. [Loops](#loops)
1. [Strings](#strings)
1. [Slicing](#slicing)
1. [Tuple](#tuple)
1. [Sort](#sort)
1. [Hash](#hash)
1. [Set](#set)
1. [List](#list)
1. [Dict](#dict)
1. [Binary Tree](#binary-tree)
1. [Graph](#graph)
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
1. [regex](#regular-expression)
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
1. [Kadane's Algorithm](#kadane)
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

```js
const a = 255; const b = 0b11111111; const c = 0xFF;
const big = 12345678901234567890n; // BigInt
const d = 1.23; const ok = true;
const ch = 'a'; const s = "hello\n";
const n = null; const u = undefined;
const arr = [1, 2, 3];
const obj = { key: 1 };
const set = new Set(['a', 'b']);
const map = new Map([["k", 1]]);
```

## Loops

```js
for (let i = 0; i < n; i++) {}
for (let i = n - 1; i >= 0; i--) {}
for (const x of nums) {}
let i = 0; while (i < n) { i++; }
```

Reverse in-place

```js
let l = 0, r = nums.length - 1;
while (l < r) { [nums[l], nums[r]] = [nums[r], nums[l]]; l++; r--; }
```

Ranges

```js
for (let i = 0; i < 3; i++) {}
for (let i = 3; i >= 0; i--) {}
```

## Strings

```js
const i = s.indexOf('x');
const j = s.lastIndexOf('x');
const tokens = line.split(":");
const joined = ["a", "b"].join(" ");
const c0 = s.charAt(0);
const up = c0 === c0.toUpperCase();
const low = c0 === c0.toLowerCase();
const dig = /\d/.test(c0);
const t = s.replaceAll("()", "");
const st = s.startsWith("pre"); const ed = s.endsWith("suf");
const f = `My name is ${name}, I'm ${age}`;
```

Manual split by isLetter

```js
function splitWords(input) {
  const out = [];
  let start = -1;
  for (let i = 0; i < input.length; i++) {
    const ch = input[i];
    if (/[A-Za-z]/.test(ch)) { if (start === -1) start = i; }
    else { if (start !== -1) { out.push(input.slice(start, i)); start = -1; } }
  }
  if (start !== -1) out.push(input.slice(start));
  return out;
}
```

## Slicing

```js
const sub = s.slice(2, 4);
const subArr = arr.slice(2, 5);
```

## Tuple

```js
const pair = [2, 3]; // or { first: 2, second: 3 }
```

## Sort

```js
nums.sort((a, b) => a - b);
nums.slice(0, k).sort((a, b) => a - b);
words.sort((a, b) => a.length - b.length);
list.sort((a, b) => a[1] - b[1]);
list.sort((a, b) => a[1] - b[1] || a[0] - b[0]);

const m = new Map(Object.entries({ a: 2, b: 1 }));
const e = Array.from(m.entries()).sort((x, y) => x[1] - y[1]);
```

Keep original indices

```js
const idxVal = nums.map((v, i) => [i, v]).sort((a, b) => a[1] - b[1]);
```

## Hash

```js
const ht = new Map();
for (const ch of s) ht.set(ch, (ht.get(ch) || 0) + 1);
```

## Set

```js
const st = new Set();
st.add(a); st.delete(a); const has = st.has(a);
const any = st.values().next().value;
```

## List

```js
const list = Array(5).fill(0);
const grid = Array.from({ length: 2 }, () => []);
grid[0].push(1);
list.reverse();
const joinedList = [...list1, ...list2];
```

## Dict

```js
const d = new Map();
d.set("key", 1);
const v = d.get("key") ?? 0;
for (const k of d.keys()) {}
for (const [k, val] of d.entries()) {}
if (!d.has("k")) d.set("k", 0);
d.delete("k");
```

## Binary Tree

```js
class TreeNode { constructor(val = 0, left = null, right = null) { this.val = val; this.left = left; this.right = right; } }
```

Recursive traversals

```js
function pre(n){ if(!n) return; visit(n); pre(n.left); pre(n.right); }
function ino(n){ if(!n) return; ino(n.left); visit(n); ino(n.right); }
function post(n){ if(!n) return; post(n.left); post(n.right); visit(n); }
```

Iterative inorder

```js
function inorder(root){
  const out = [], st = [];
  let cur = root;
  while (cur || st.length) {
    while (cur) { st.push(cur); cur = cur.left; }
    cur = st.pop(); out.push(cur.val); cur = cur.right;
  }
  return out;
}
```

BFS level order

```js
function levelOrder(root){
  const res = []; if (!root) return res;
  const q = [root];
  while (q.length) {
    const sz = q.length, lev = [];
    for (let i = 0; i < sz; i++) {
      const n = q.shift(); lev.push(n.val);
      if (n.left) q.push(n.left); if (n.right) q.push(n.right);
    }
    res.push(lev);
  }
  return res;
}
```
## Graph

Adjacency list and BFS/DFS

```js
const g = Array.from({ length: N }, () => []);
for (const [u, v] of edges) { g[u].push(v); g[v].push(u); }

function dfs(u, p){ for (const v of g[u]) if (v !== p) dfs(v, u); }

function bfs(s){
  const order = [], vis = Array(N).fill(false);
  const q = [s]; vis[s] = true;
  for (let qi = 0; qi < q.length; qi++){
    const u = q[qi]; order.push(u);
    for (const v of g[u]) if (!vis[v]){ vis[v] = true; q.push(v); }
  }
  return order;
}
```

## PriorityQueue

```js
class MinHeap {
  constructor(cmp = (a, b) => a - b) { this.a = []; this.cmp = cmp; }
  size(){ return this.a.length; }
  peek(){ return this.a[0]; }
  push(x){ this.a.push(x); this._siftUp(this.a.length - 1); }
  pop(){ const a = this.a; if (a.length === 0) return undefined; const top = a[0]; const x = a.pop(); if (a.length){ a[0] = x; this._siftDown(0); } return top; }
  _siftUp(i){ const a = this.a; while (i){ const p = (i - 1) >> 1; if (this.cmp(a[i], a[p]) < 0){ [a[i], a[p]] = [a[p], a[i]]; i = p; } else break; } }
  _siftDown(i){ const a = this.a; for(;;){ let l = i * 2 + 1, r = l + 1, m = i; if (l < a.length && this.cmp(a[l], a[m]) < 0) m = l; if (r < a.length && this.cmp(a[r], a[m]) < 0) m = r; if (m !== i){ [a[i], a[m]] = [a[m], a[i]]; i = m; } else break; } }
}
```

Top K frequent

```js
function topKFrequent(nums, k){
  const cnt = new Map(); for (const x of nums) cnt.set(x, (cnt.get(x) || 0) + 1);
  const pq = new MinHeap((a, b) => a[1] - b[1]);
  for (const e of cnt.entries()){ pq.push(e); if (pq.size() > k) pq.pop(); }
  const res = []; while (pq.size()) res.push(pq.pop()[0]);
  return res.reverse();
}
```
## lambda

```js
const best = [a, b].reduce((p, x) => Math.abs(target - x) < Math.abs(target - p) ? x : p);
```

## zip

```js
for (let i = 0; i < Math.min(A.length, B.length); i++) {
  const a = A[i], b = B[i];
}
```

Rotate matrix using transpose+reverse

```js
function rotate(m){ const n = m.length; for(let i=0;i<n;i++) for(let j=i+1;j<n;j++){ const t=m[i][j]; m[i][j]=m[j][i]; m[j][i]=t; } for(let i=0;i<n;i++) m[i].reverse(); }
```

## Random

```js
const r = Math.floor(Math.random() * (hi - lo)) + lo; // [lo,hi)
// Fisher-Yates
function shuffle(a){ for(let i=a.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [a[i],a[j]]=[a[j],a[i]]; } return a; }
```

## Constants

```js
const INF = Number.POSITIVE_INFINITY; const NINF = Number.NEGATIVE_INFINITY;
const MAXI = Number.MAX_SAFE_INTEGER; const MINI = Number.MIN_SAFE_INTEGER;
```

## Ternary

```js
const x = cond ? a : b;
```

## Bitwise Operators

```js
const andv = (0b1100 & 0b1010);
const orv = (0b1100 | 0b1010);
const xrv = (0b1100 ^ 0b1010);
const shr = (0b1100 >> 2);
const shl = (0b0011 << 2);
const ushr = (-1 >>> 1);
```

## For Else

```js
let broken = false;
for(let i=0;i<n;i++){ if(cond){ broken = true; break; } }
if(!broken){ /* no break */ }
```

## Modulo

```js
function mod(a, m){ const r = a % m; return r < 0 ? r + m : r; }
```

## any

```js
const any = nums.some(x => x > 0);
```

## all

```js
const all = nums.every(x => x >= 0);
```

## Bisect

```js
function lowerBound(a, x){ let l=0,r=a.length; while(l<r){ const m=(l+r)>>1; if(a[m] < x) l=m+1; else r=m; } return l; }
function upperBound(a, x){ let l=0,r=a.length; while(l<r){ const m=(l+r)>>1; if(a[m] <= x) l=m+1; else r=m; } return l; }
```

## Math

```js
const p = (BigInt(a) ** BigInt(b)) % BigInt(mod);
const q = Math.trunc(a / b); const rem = ((a % b) + b) % b;
```

## iter

```js
for (const x of list) {}
const it = list[Symbol.iterator](); it.next();
```

## Map

```js
const up = list.map(s => s.toUpperCase());
```

## Filter

```js
const over75 = scores.filter(x => x > 75);
```

## Reduce

```js
const sum = nums.reduce((a, b) => a + b, 0);
```

## Regular Expression

```js
const out = s.replace(/[aeiou]/g, "");
```

## Types

```js
const grid = Array.from({ length: R }, () => Array(C).fill(0));
const adj = new Map(); // Map<number, number[]>
```

## Grids

```js
const R = grid.length, C = grid[0].length;
const dirs = [[1,0],[-1,0],[0,1],[0,-1]];
function dfs(r,c){ grid[r][c]=2; for(const [dr,dc] of dirs){ const nr=r+dr,nc=c+dc; if(0<=nr&&nr<R&&0<=nc&&nc<C&&grid[nr][nc]===1) dfs(nr,nc); } }
```

# Collections

## Deque

```js
const dq = [];
dq.unshift(5); dq.push(6); dq.shift(); dq.pop();
```

## Counter

```js
const cnt = new Map();
for (const ch of s) cnt.set(ch, (cnt.get(ch) || 0) + 1);
```

Top-K with counter

```js
function topK(nums, k){
  const m = new Map(); for (const x of nums) m.set(x, (m.get(x) || 0) + 1);
  return Array.from(m.entries()).sort((a,b)=>b[1]-a[1]).slice(0,k).map(e=>e[0]);
}
```

## Default Dict

```js
function getOrInit(map, key, init){ if(!map.has(key)) map.set(key, init()); return map.get(key); }
const dd = new Map(); getOrInit(dd, 1, () => []).push(2);
```
# Algorithms

## General Tips

- Clarify, brute force, optimize, code, test.

## Binary Search

```js
function firstBadVersion(n, isBad){
  let l=1, r=n;
  while(l<r){ const m = l + ((r-l)>>1); if(isBad(m)) r=m; else l=m+1; }
  return l;
}
```

Sqrt template

```js
function mySqrt(x){ if(x<=1) return x; let l=1,r=x; while(l<r){ const m=l+((r-l)>>1); if(m*m>x) r=m; else l=m+1; } return l-1; }
```

## Binary Search Tree

Complete tree check by index

```js
function isComplete(root){ let total=0n, mx=0n; (function dfs(n, idx){ if(!n) return; total++; if(idx>mx) mx=idx; dfs(n.left, idx*2n); dfs(n.right, idx*2n+1n); })(root, 1n); return total===mx; }
```

Range sum

```js
function rangeSumBST(root, L, R){ if(!root) return 0; let s=0; const dfs=(n)=>{ if(!n) return; if(L<=n.val && n.val<=R) s+=n.val; if(n.val>L) dfs(n.left); if(n.val<R) dfs(n.right); }; dfs(root); return s; }
```

Validate BST (iterative)

```js
function isValidBST(root){ const st=[]; let cur=root, prev=null; while(cur||st.length){ while(cur){ st.push(cur); cur=cur.left; } cur=st.pop(); if(prev!==null && cur.val<=prev) return false; prev=cur.val; cur=cur.right; } return true; }
```

## Topological Sort

```js
function canFinish(n, pre){ const adj=Array.from({length:n},()=>[]), deg=Array(n).fill(0); for(const [a,b] of pre){ adj[b].push(a); deg[a]++; } const q=[]; for(let i=0;i<n;i++) if(deg[i]===0) q.push(i); for(let qi=0; qi<q.length; qi++){ const u=q[qi]; for(const v of adj[u]) if(--deg[v]===0) q.push(v); } return q.length===n; }
```

Alien dictionary

```js
function alienOrder(words){ const nodes=new Set(words.join("")); const adj=new Map(), deg=new Map(); for(const c of nodes){ adj.set(c, []); deg.set(c, 0); }
  for(let i=0;i+1<words.length;i++){
    const a=words[i], b=words[i+1]; const m=Math.min(a.length,b.length); let diff=false;
    for(let j=0;j<m;j++) if(a[j]!==b[j]){ adj.get(a[j]).push(b[j]); deg.set(b[j], deg.get(b[j])+1); diff=true; break; }
    if(!diff && a.length>b.length) return "";
  }
  const q=[...Array.from(deg.entries()).filter(([,d])=>d===0).map(([c])=>c)]; let out="";
  for(let qi=0; qi<q.length; qi++){ const u=q[qi]; out+=u; for(const v of adj.get(u)){ deg.set(v, deg.get(v)-1); if(deg.get(v)===0) q.push(v); } }
  return out.length===nodes.size? out : "";
}
```
## Convert Base

```js
function toHex(num){ if(num===0) return "0"; if(num<0) num = 2**32 + num; const idx="0123456789abcdef"; let s=""; while(num>0){ const d = num % 16; s = idx[d] + s; num = Math.floor(num/16); } return s; }
```

## Parenthesis

Count-only

```js
function isValidPar(s){ let c=0; for(const ch of s){ if(ch==='(') c++; else if(ch===')'){ c--; if(c<0) return false; } } return c===0; }
```

Stack-based

```js
function isValid(s){ const st=[], mp=new Map([[")","("],["}","{"],["]","["]]); for(const c of s){ if([...mp.values()].includes(c)) st.push(c); else if(mp.has(c)){ if(!st.length || st.pop()!==mp.get(c)) return false; } } return st.length===0; }
```

Remove to make valid

```js
function minRemoveToMakeValid(s){ const st=[], del=Array(s.length).fill(false); for(let i=0;i<s.length;i++){ const c=s[i]; if(c==='(') st.push(i); else if(c===')'){ if(st.length) st.pop(); else del[i]=true; } } while(st.length) del[st.pop()]=true; let ans=""; for(let i=0;i<s.length;i++) if(!del[i]) ans+=s[i]; return ans; }
```

## Max Profit Stock

Infinite transactions

```js
function maxProfit(prices){ let t0=0, t1=-Infinity; for(const p of prices){ const t0old=t0; t0=Math.max(t0, t1+p); t1=Math.max(t1, t0old-p); } return t0; }
```

Single transaction

```js
function maxProfit1(prices){ let t0=0, t1=-Infinity; for(const p of prices){ t0=Math.max(t0, t1+p); t1=Math.max(t1, -p); } return t0; }
```

K transactions

```js
function maxProfitK(k, prices){ const t0=Array(k+1).fill(0), t1=Array(k+1).fill(-1e15); for(const p of prices){ for(let i=k;i>=1;i--){ t0[i]=Math.max(t0[i], t1[i]+p); t1[i]=Math.max(t1[i], t0[i-1]-p); } } return t0[k]; }
```

## Shift Array Right

```js
function rotate(a,k){ const n=a.length; k%=n; rev(a,0,n-1); rev(a,0,k-1); rev(a,k,n-1); }
function rev(a,l,r){ while(l<r){ [a[l],a[r]]=[a[r],a[l]]; l++; r--; } }
```

## Continuous Subarrays with Sum k

```js
function subarraySum(nums,k){ const mp=new Map([[0,1]]); let ans=0,sum=0; for(const x of nums){ sum+=x; ans+= mp.get(sum-k)||0; mp.set(sum, (mp.get(sum)||0)+1); } return ans; }
```

## Events

```js
function employeeFreeTime(schedule){ const ev=[]; for(const e of schedule) for(const m of e){ ev.push([m.start,1]); ev.push([m.end,-1]); } ev.sort((a,b)=>a[0]-b[0]); const itv=[]; let prev=null, bal=0; for(const [t,c] of ev){ if(bal===0 && prev!==null && t!==prev) itv.push([prev,t]); bal+=c; prev=t; } return itv; }
```

## Merge Meetings

```js
function insert(intervals, newI){ const li=intervals.slice(); li.push(newI); li.sort((a,b)=>a[0]-b[0]); const res=[li[0]]; for(const cur of li){ const last=res[res.length-1]; if(cur[0]<=last[1]) last[1]=Math.max(last[1], cur[1]); else res.push(cur); } return res; }
```

## Trie

```js
class Trie{
  constructor(){ this.root = {}; }
  addWord(s){ let t=this.root; for(const c of s){ if(!t[c]) t[c]={}; t=t[c]; } t['#']=s; }
  matchPrefix(s, t){ if(!t) t=this.root; for(const c of s){ if(!t[c]) return []; t=t[c]; } const out=[]; const rec = (node)=>{ for(const k in node){ if(k==='#') out.push(node[k]); else rec(node[k]); } }; rec(t); return out; }
  hasWord(s){ let t=this.root; for(const c of s){ if(!t[c]) return false; t=t[c]; } return true; }
}
```

Search with '.' wildcard

```js
class WordDictionary{
  constructor(){ this.r={}; }
  addWord(w){ let t=this.r; for(const c of w){ if(!t[c]) t[c]={}; t=t[c]; } t['$']=true; }
  search(w){ const dfs=(i,n)=>{ if(i===w.length) return !!n['$']; const c=w[i]; if(c!=='.') return n[c] && dfs(i+1, n[c]); for(const k in n) if(k!=='$' && dfs(i+1, n[k])) return true; return false; }; return dfs(0,this.r); }
}
```

## Kadane

```js
function maxSubArray(a){ let best=a[0]; for(let i=1;i<a.length;i++){ if(a[i-1]>0) a[i]+=a[i-1]; best=Math.max(best,a[i]); } return best; }
```

## Union Find

```js
class DSU{
  constructor(n){ this.p=Array(n).fill(0).map((_,i)=>i); this.sz=Array(n).fill(1); }
  find(x){ if(this.p[x]!==x) this.p[x]=this.find(this.p[x]); return this.p[x]; }
  union(a,b){ let x=this.find(a), y=this.find(b); if(x===y) return false; if(this.sz[x]<this.sz[y]) [x,y]=[y,x]; this.p[y]=x; this.sz[x]+=this.sz[y]; return true; }
}
```

## Fast Power

```js
function myPow(x, n){ let e=BigInt(n), xb=Number.isInteger(x)? BigInt(x): x; if(e<0n){ xb = 1/Number(xb); e=-e; }
  let ans=1; let base=Number(xb);
  while(e>0n){ if((e&1n)===1n) ans*=base; base*=base; e>>=1n; } return ans; }
```

## Fibonacci Golden

```js
function fib(N){ const g=(1+Math.sqrt(5))/2; return Math.round((g**N)/Math.sqrt(5)); }
```

## Basic Calculator

```js
function calculate(s){ s+='$'; function evalAt(i){ const st=[]; let sign='+', num=0; while(i<s.length){ const c=s[i]; if(c===' '){ i++; continue; } if(c>='0'&&c<='9'){ num=num*10+(c.charCodeAt(0)-48); i++; continue; } if(c==='('){ const r=evalAt(i+1); num=r[0]; i=r[1]; }
      if(!(c>='0'&&c<='9')){ if(sign==='+') st.push(num); else if(sign==='-') st.push(-num); else if(sign==='*') st.push(st.pop()*num); else if(sign==='/') st.push((st.pop()/num)|0);
        if(c===')') return [st.reduce((a,b)=>a+b,0), i+1]; sign=c; num=0; i++; }
    }
    return [st.reduce((a,b)=>a+b,0), i]; }
  return evalAt(0)[0]; }
```

## Reverse Polish

```js
function evalRPN(tok){ const st=[]; for(const c of tok){ if(!'+-/*'.includes(c)) st.push(Number(c)); else { const a=st.pop(), b=st.pop(); switch(c){ case '+': st.push(b+a); break; case '-': st.push(b-a); break; case '*': st.push(b*a); break; default: st.push((b/a)|0); } } } return st.pop(); }
```

## Reservoir Sampling

```js
class Picker{ constructor(nums){ this.nums=nums; } pick(target){ let res=null, cnt=0; for(let i=0;i<this.nums.length;i++){ if(this.nums[i]===target){ cnt++; const chance = Math.floor(Math.random()*cnt)+1; if(chance===1) res=i; } } return res; } }
```

## String Subsequence (shortestWay)

```js
function shortestWay(src, tgt){ const pos=new Map(); for(let i=0;i<src.length;i++){ const c=src[i]; if(!pos.has(c)) pos.set(c, []); pos.get(c).push(i); }
  let ans=1, i=-1; for(const c of tgt){ if(!pos.has(c)) return -1; const arr=pos.get(c); let j=lowerBound(arr, i); if(j===arr.length){ ans++; i=arr[0]+1; } else { i=arr[j]+1; } }
  return ans;
  function lowerBound(a, x){ let l=0,r=a.length; while(l<r){ const m=(l+r)>>1; if(a[m] < x) l=m+1; else r=m; } return l; }
}
```

## Candy Crush (remove duplicates)

```js
function removeDuplicates(s,k){ const st=[]; for(const c of s){ if(st.length && st[st.length-1][0]===c){ st[st.length-1][1]++; if(st[st.length-1][1]===k) st.pop(); } else st.push([c,1]); } let ans=""; for(const [ch, cnt] of st) ans+=ch.repeat(cnt); return ans; }
```

## Dutch Flag

```js
function sortColors(a){ let p0=0, cur=0, p2=a.length-1; while(cur<=p2){ if(a[cur]===0){ [a[p0],a[cur]]=[a[cur],a[p0]]; p0++; cur++; } else if(a[cur]===2){ [a[cur],a[p2]]=[a[p2],a[cur]]; p2--; } else cur++; } }
```
