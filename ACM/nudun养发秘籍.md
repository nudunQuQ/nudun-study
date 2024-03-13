[TOC]

# 基础模版

## 初始格式

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef double db;
template<class T>inline void MAX(T &a,T b){if(b>a)a=b;}
template<class T>inline void MIN(T &a,T b){if(b<a)a=b;}
template<class T>inline void rd(T &x){
	x=0;char o,f=1;
	while(o=getchar(),o<48)if(o=='-')f=-f;
	do x=(x<<3)+(x<<1)+(o^48);
	while(o=getchar(),o>47);
	x*=f;
}

int main(){
#ifndef ONLINE_JUDGE
//	freopen("nudun.in","r",stdin);
//	freopen("nudun.out","w",stdout);
#endif
	
	return 0;
}
```

## 备用知识

### 关键字

y1

/*

/tmp/compiler_pmwm__ms/src:18:8: 错误：‘int y1’被重新声明为不同意义的符号 int x1,y1,x2,y2,ans;        ^~ In file included from /usr/include/features.h:424,                 from /usr/include/x86_64-linux-gnu/c++/8/bits/os_defines.h:39,                 from /usr/include/x86_64-linux-gnu/c++/8/bits/c++config.h:508,                 from /usr/include/c++/8/cassert:43,                 from /usr/include/x86_64-linux-gnu/c++/8/bits/stdc++.h:33,                 from /tmp/compiler_pmwm__ms/src:1: /usr/include/x86_64-linux-gnu/bits/mathcalls.h:221:1: 附注：previous declaration ‘double y1(double)’ __MATHCALL (y1,, (_Mdouble_)); ^~~~~~~~~~ /tmp/compiler_pmwm__ms/src: 在函数‘int main()’中: /tmp/compiler_pmwm__ms/src:44:9: 错误：invalid conversion from ‘double (*)(double) throw ()’ {aka ‘double (*)(double)’} to ‘int’ [-fpermissive]  dfs(x1,y1);         ^~ /tmp/compiler_pmwm__ms/src:23:20: 附注：  初始化‘void dfs(int, int)’的实参 2 void dfs(int x,int y){                ~~~~^ /tmp/compiler_pmwm__ms/src: In instantiation of ‘void rd(T&) [with T = double(double)]’: /tmp/compiler_pmwm__ms/src:37:14:   required from here /tmp/compiler_pmwm__ms/src:8:3: 错误：向只读形参‘x’赋值  x=0;char o,f=1;  ~^~ /tmp/compiler_pmwm__ms/src:10:9: 错误：操作数类型‘double(double)’和‘int’对双目‘operator<<’而言无效  do x=(x<<3)+(x<<1)+(o^48);       ~~^~~~ /tmp/compiler_pmwm__ms/src:10:16: 错误：操作数类型‘double(double)’和‘int’对双目‘operator<<’而言无效  do x=(x<<3)+(x<<1)+(o^48);              ~~^~~~ /tmp/compiler_pmwm__ms/src:12:3: 错误：操作数类型‘double(double)’和‘char’对双目‘operator*’而言无效  x*=f;  ~^~~ /tmp/compiler_pmwm__ms/src:12:3: 错误：在求‘operator*=(double(double), char)’值时

*/

### 优先级

| 优先级 | 符号 | 方向 |
| :--- | ---- | ---- |
| 1    | **!  ~** | **右到左** |
| 2    | ***  /  %** | 左到右 |
| 3    | **+  -** | 左到右 |
| 4 | **<<  >>** | 左到右 |
| 5 | **>  >=  <  <=** | 左到右 |
| 6 | **==  !=** | 左到右 |
| 7 | **&** | 左到右 |
| 8 | **^** | 左到右 |
| 9 | **\|** | 左到右 |
| 10 | **&&** | 左到右 |
| 11 | **\|\|** | 左到右 |
| 12 | **?** | **右到左** |
| 13 | **=**  （各种赋值） | **右到左** |

**!  ~**      *** / %**      **+ -**      **<< >>**        **> >= < <=**        **== !=**        **&**    **^**    **\|**        **&&**    **\|\|**      **?**      **=**

## 二进制

二进制下1的个数

二进制下1的个数为奇数的数的个数//范围为[0,n]

```cpp
template<class T>inline int cnt_1(T n){
	int cnt=0;
	while(n)cnt++,n=n&(n-1);
	return cnt;
}
template<class T>inline T cnt_1_odd(T n){
	if(n&1)return (n+1)>>1;
	return (n>>1)+(cnt_1(n)&1);
}
```

x的lowbit（二进制下最小的1）：x&-x

​	**x-(x&-x)**等价于**x&(x-1)**

集合中非公共的1：sum_and[S] ^ sum_or[S]（用于吉司机线段树**区间按位取与/或**）

枚举x的非0子集

```cpp
for(int i=x;i;i=(i-1)&x)
```

枚举x的子集

```cpp
for(int i=x;;i=(i-1)&x){
	
	if(!i)break;
}
```





## 基数排序

给int范围内的非负整数排序，建议 n>=$10^5$

```cpp
void Sort(int n,int *A){
	static const int M=1e6+5,S=16,P=(1<<S)-1;
	static int cnt[1<<S],B[M];
	memset(cnt,0,sizeof(cnt));
	for(int i=1;i<=n;i++)cnt[A[i]&P]++;
	for(int i=1;i<=P;i++)cnt[i]+=cnt[i-1];
	for(int i=n;i>=1;i--)B[cnt[A[i]&P]--]=A[i];
	memset(cnt,0,sizeof(cnt));
	for(int i=1;i<=n;i++)cnt[B[i]>>S]++;
	for(int i=1;i<=P;i++)cnt[i]+=cnt[i-1];
	for(int i=n;i>=1;i--)A[cnt[B[i]>>S]--]=B[i];
}
```





# 数据结构

## 树状数组*

## 线段树*

### 动态开点+线段树合并

关于线段树合并的复杂度：

假设刚开始**所有线段树上**共有x（一般是$n*\log{n}$左右）个节点，合并两棵线段树的复杂度是它们的交集部分。

合并的时候每到达一个点都意味着有两个点变成了一个点，少了一个点，这时用了O(1)的时间。

每少一个点都是O(1)，那么少掉x个点也就是O(x)。

所以，线段树无论怎么合并复杂度都不会超过O(x)，不超过update的复杂度。

代码：使用标记永久化的写法，支持线段树合并（加法运算），区间加法，单点查询。

```cpp
const int M=2e5+5;
const int S=40;
int LLL=1,RRR=M-5;
int trid,rt[M],ls[M*S],rs[M*S],tag[M*S];
void update(int &x,int a,int b,int v,int l=LLL,int r=RRR){
	if(r<a||l>b)return;
	if(!x)x=++trid;
	if(a<=l&&r<=b){
		tag[x]+=v;
		return;
	}
	int mid=l+r>>1;
	update(ls[x],a,b,v,l,mid);
	update(rs[x],a,b,v,mid+1,r);
}
int merge(int x,int y){
	if(!x||!y)return x|y;
	tag[x]+=tag[y];
	ls[x]=merge(ls[x],ls[y]);
	rs[x]=merge(rs[x],rs[y]);
	return x;
}
int query(int x,int pos,int l=LLL,int r=RRR){
	if(r<pos||l>pos||!x)return 0;
	int mid=l+r>>1;
	return tag[x]+query(ls[x],pos,l,mid)+query(rs[x],pos,mid+1,r);
}
```

### 标记永久化

关于一般标记永久化的写法：

一、区间修改单点查询

修改：1，对于返回节点，修改永久化标记的值；2，对于路径上其它节点，没有变化

查询：1，对于叶子结点，贡献该点的值和永久化标记的值；2，对于路径上其它节点，贡献永久化标记的值

二、区间修改区间查询

修改：1，对于返回节点，修改永久化标记的值；2，对于路径上其它节点，维护该点的值（该值不考虑永久化标记）

查询：1，对于返回节点，贡献该点的值和永久化标记的值；2，对于路径上其它节点，贡献永久化标记的值

已知用途：为动态开点线段树节省空间

//不能区间修改区间查询？

//可用于主席树的修改，线段树合并，二维线段树？

## 主席树*

## 吉司机线段树

线段树上一个没有次大值的点的更新只需要O(1)，一个关键点会使O(log(n))个祖先结点存在次大值，即消除一个关键点的复杂度是O(log(n))，而每次修改最多生成O(log(n))个关键点，所以修改的复杂度是O(log(n)^2))。

（BZOJ4695）维护一个序列，支持下面几种操作

1 L R v ：给区间[L,R]加上一个数v

2 L R v ：把区间[L,R]中小于v的数变成v

3 L R v ：把区间[L,R]中大于v的数变成v

4 L R ：求区间[L,R]的和

5 L R ：求区间[L,R]的最大值

6 L R ：求区间[L,R]的最小值

时间复杂度  $O(nlog^2{n})$

```cpp
const int M=5e5+5;
const ll INF=1e18;
int n,q,A[M];
int len[M<<2],cmx[M<<2],cmi[M<<2];
ll sum[M<<2],mx[M<<2],mx2[M<<2],mi[M<<2],mi2[M<<2];
ll lazy_mx[M<<2],lazy_mi[M<<2],lazy_add[M<<2];

void up(int p){
	int ls=p<<1,rs=p<<1|1;
	sum[p]=sum[ls]+sum[rs];
	if(mx[ls]>mx[rs]){
		mx[p]=mx[ls];
		mx2[p]=max(mx2[ls],mx[rs]);
		cmx[p]=cmx[ls];
	}
	else if(mx[ls]<mx[rs]){
		mx[p]=mx[rs];
		mx2[p]=max(mx2[rs],mx[ls]);
		cmx[p]=cmx[rs];
	}
	else{
		mx[p]=mx[ls];
		mx2[p]=max(mx2[ls],mx2[rs]);
		cmx[p]=cmx[ls]+cmx[rs];
	}
	if(mi[ls]<mi[rs]){
		mi[p]=mi[ls];
		mi2[p]=min(mi2[ls],mi[rs]);
		cmi[p]=cmi[ls];
	}
	else if(mi[ls]>mi[rs]){
		mi[p]=mi[rs];
		mi2[p]=min(mi2[rs],mi[ls]);
		cmi[p]=cmi[rs];
	}
	else{
		mi[p]=mi[ls];
		mi2[p]=min(mi2[ls],mi2[rs]);
		cmi[p]=cmi[ls]+cmi[rs];
	}
}
void build(int l=1,int r=n,int p=1){
	len[p]=r-l+1;
	lazy_mx[p]=lazy_mi[p]=lazy_add[p]=0;
	if(l==r){
		cmx[p]=cmi[p]=1;
		sum[p]=mx[p]=mi[p]=A[l];
		mx2[p]=-INF;
		mi2[p]=INF;
		return;
	}
	int mid=l+r>>1;
	build(l,mid,p<<1);
	build(mid+1,r,p<<1|1);
	up(p);
}
void cal_max(int p,ll v){
	lazy_mx[p]+=v;
	if(cmx[p]==len[p])mi[p]+=v;
	else if(cmx[p]+cmi[p]==len[p])mi2[p]+=v;
	mx[p]+=v;
	sum[p]+=1ll*v*cmx[p];
}
void cal_min(int p,ll v){
	lazy_mi[p]+=v;
	if(cmi[p]==len[p])mx[p]+=v;
	else if(cmi[p]+cmx[p]==len[p])mx2[p]+=v;
	mi[p]+=v;
	sum[p]+=1ll*v*cmi[p];
}
void cal_add(int p,ll v){
	lazy_add[p]+=v;
	mx[p]+=v;
	mi[p]+=v;
	if(mx2[p]!=-INF)mx2[p]+=v;
	if(mi2[p]!=INF)mi2[p]+=v;
	sum[p]+=1ll*v*len[p];
}
void down(int p){
	int ls=p<<1,rs=p<<1|1;
	if(lazy_mx[p]){
		if(mx[ls]>mx[rs])cal_max(ls,lazy_mx[p]);
		else if(mx[ls]<mx[rs])cal_max(rs,lazy_mx[p]);
		else cal_max(ls,lazy_mx[p]),cal_max(rs,lazy_mx[p]);
		lazy_mx[p]=0;
	}
	if(lazy_mi[p]){
		if(mi[ls]<mi[rs])cal_min(ls,lazy_mi[p]);
		else if(mi[ls]>mi[rs])cal_min(rs,lazy_mi[p]);
		else cal_min(ls,lazy_mi[p]),cal_min(rs,lazy_mi[p]);
		lazy_mi[p]=0;
	}
	if(lazy_add[p]){
		cal_add(ls,lazy_add[p]);
		cal_add(rs,lazy_add[p]);
		lazy_add[p]=0;
	}
}
void update_max(int a,int b,ll v,int l=1,int r=n,int p=1){
	if(r<a||l>b||v<=mi[p])return;
	if(a<=l&&r<=b&&v<mi2[p]){
		cal_min(p,v-mi[p]);
		return;
	}
	down(p);
	int mid=l+r>>1;
	update_max(a,b,v,l,mid,p<<1);
	update_max(a,b,v,mid+1,r,p<<1|1);
	up(p);
}
void update_min(int a,int b,ll v,int l=1,int r=n,int p=1){
	if(r<a||l>b||v>=mx[p])return;
	if(a<=l&&r<=b&&v>mx2[p]){
		cal_max(p,v-mx[p]);
		return;
	}
	down(p);
	int mid=l+r>>1;
	update_min(a,b,v,l,mid,p<<1);
	update_min(a,b,v,mid+1,r,p<<1|1);
	up(p);
}
void update_add(int a,int b,ll v,int l=1,int r=n,int p=1){
	if(r<a||l>b)return;
	if(a<=l&&r<=b){
		cal_add(p,v);
		return;
	}
	down(p);
	int mid=l+r>>1;
	update_add(a,b,v,l,mid,p<<1);
	update_add(a,b,v,mid+1,r,p<<1|1);
	up(p);
}
ll query_max(int a,int b,int l=1,int r=n,int p=1){
	if(r<a||l>b)return -INF;
	if(a<=l&&r<=b)return mx[p];
	down(p);
	int mid=l+r>>1;
	return max(query_max(a,b,l,mid,p<<1),query_max(a,b,mid+1,r,p<<1|1));
}
ll query_min(int a,int b,int l=1,int r=n,int p=1){
	if(r<a||l>b)return INF;
	if(a<=l&&r<=b)return mi[p];
	down(p);
	int mid=l+r>>1;
	return min(query_min(a,b,l,mid,p<<1),query_min(a,b,mid+1,r,p<<1|1));
}
ll query_sum(int a,int b,int l=1,int r=n,int p=1){
	if(r<a||l>b)return 0;
	if(a<=l&&r<=b)return sum[p];
	down(p);
	int mid=l+r>>1;
	return query_sum(a,b,l,mid,p<<1)+query_sum(a,b,mid+1,r,p<<1|1);
}
int main(){
#ifndef ONLINE_JUDGE
//	freopen("nudun.in","r",stdin);
//	freopen("nudun.out","w",stdout);
#endif
	rd(n);
	for(int i=1;i<=n;i++)rd(A[i]);
	build();
	rd(q);
	while(q--){
		int op,a,b,v;
		rd(op),rd(a),rd(b);
		if(0);
		else if(op==1)rd(v),update_add(a,b,v);
		else if(op==2)rd(v),update_max(a,b,v);
		else if(op==3)rd(v),update_min(a,b,v);
		else if(op==4)printf("%lld\n",query_sum(a,b));
		else if(op==5)printf("%lld\n",query_max(a,b));
		else if(op==6)printf("%lld\n",query_min(a,b));
	}
	return 0;
}
```



## 李超线段树*

## 可撤销并查集*

## ST表*

## 分块*

## 莫队

### 普通莫队

给定长度为n的序列，m次询问，求区间 $[l,r]$ 之间有多少种不同的数字 P1972

```cpp
const int M=1e6+5;
const int S=sqrt(M);
int n,m,res,A[M],cnt[M],ans[M];
struct node{
	int l,r,id;
	bool operator <(const node &A)const{
		if(l/S!=A.l/S)return l/S<A.l/S;
		if((l/S)&1)return r<A.r;
		return r>A.r;
	}
}B[M];
void insert(int x){
	if(++cnt[x]==1)res++;
}
void erase(int x){
	if(--cnt[x]==0)res--;
}
int main(){
#ifndef ONLINE_JUDGE
//	freopen("nudun.in","r",stdin);
//	freopen("nudun.out","w",stdout);
#endif
	rd(n);
	for(int i=1;i<=n;i++)rd(A[i]);
	rd(m);
	for(int i=1;i<=m;i++){
		rd(B[i].l),rd(B[i].r);
		B[i].id=i;
	}
	sort(B+1,B+1+m);
	int l=1,r=0;
	for(int i=1;i<=m;i++){
		while(r<B[i].r)insert(A[++r]);
		while(l>B[i].l)insert(A[--l]);
		while(r>B[i].r)erase(A[r--]);
		while(l<B[i].l)erase(A[l++]);
		ans[B[i].id]=res;
	}
	for(int i=1;i<=m;i++)printf("%d\n",ans[i]);
	return 0;
}
```

### 带修莫队*

### 树上待修莫队

uoj58 糖果公园

$n$个节点的树，$m$种颜色，$q$个询问。
树上每个节点有一个颜色，每种颜色有一个权值。
第$i$次遍历到某种颜色的点，该点的价值乘上对应的数值。
$0$ $x$ $y$ : 把$x$点的颜色改为$y$。
$1$ $x$ $y$ : 查询遍历$x$到$y$路径的总价值。

思路：利用树的括号序将查询的一条链转化成括号序的一个区间，再在括号序的区间上用待修莫队求解。

1.（**关键点：括号序**）一个点的括号序分别是dfs过程中进入和退出的时候标记得到的，每个点会被标记两次，分别记为L[i]和R[i]。

2.（**关键点：区间上一个点出现次数的奇偶**）括号序的一个区间对应一段连续的时间。假设L[a]<L[b]，考虑从进入a到进入b的过程，即区间[L[a],L[b]]。

如果b在a的子树中，那么在a到b的路径上的点都会被标记了进入，却没有标记退出，而不在a到b的路径上的点要么没有被标记，要么被同时标记了进入和退出。

结论：**a到b的路径上的点为区间[L[a],L[b]]中出现一次的点**。

如果b不在a的子树中，那么a的子树内的点会被标记两次，a到lca的路径上的点（不包含lca）会被标记了退出，b到lca的路径上的点（不包含lca）会被标记了进入，而其它点要么没有被标记，要么被同时标记了进入和退出。

结论：**a到b的路径上的点为**区间[L[a],L[b]]中出现一次的点加a和lca，即**区间[R[a],L[b]]中出现一次的点和lca**。

3.（**关键点：只考虑出现奇数次的点的贡献**）将查询的链转化为区间，用带修莫队离线处理区间，维护区间里点出现的次数，当一个点出现奇数次时加入贡献，一个点出现偶数次时撤销贡献。

4.块的大小是$\sqrt[3]{n*q} $，最后就是树剖+排序+待修莫队的复杂度$O(n^{5/3})$。

```cpp
const int M=1e5+5;
const int S=2000;
int head[M],nxt[M<<1],to[M<<1],tot;
void add_edge(int a,int b){
	nxt[++tot]=head[a];
	to[tot]=b;
	head[a]=tot;
}
int n,m,q,A[M],B[M],C[M];
int fa[M],deep[M],sz[M],son[M];
int dfsid,top[M],idL[M],idR[M],reid[M<<1];
void dfs(int x,int f){
	fa[x]=f;
	deep[x]=deep[f]+1;
	sz[x]=1;
	son[x]=0;
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(y==f)continue;
		dfs(y,x);
		sz[x]+=sz[y];
		if(sz[y]>sz[son[x]])son[x]=y;
	}
}
void chain(int x,int t){
	top[x]=t;
	reid[idL[x]=++dfsid]=x;
	if(son[x])chain(son[x],t);
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(y==fa[x]||y==son[x])continue;
		chain(y,y);
	}
	reid[idR[x]=++dfsid]=x;
}
int LCA(int x,int y){
	while(top[x]!=top[y]){
		if(deep[top[x]]<deep[top[y]])swap(x,y);
		x=fa[top[x]];
	}
	return deep[x]<deep[y]?x:y;
}
struct node{
	int l,r,t,lca,id;
	bool operator <(const node &A)const{
		if(l/S!=A.l/S)return l/S<A.l/S;
		if(r/S!=A.r/S){
			if(l/S&1)return r/S<A.r/S;
			return r/S>A.r/S;
		}
		if(r/S&1)return t<A.t;
		return t>A.t;
	}
}Q[M];
int op0,op1,pos[M],old_v[M],new_v[M],mark[M],cnt[M];
ll res,ans[M];
void add(int x){
	mark[x]^=1;
	if(mark[x])res+=1ll*B[A[x]]*C[++cnt[A[x]]];
	else res-=1ll*B[A[x]]*C[cnt[A[x]]--];
}
int main(){
#ifndef ONLINE_JUDGE
//	freopen("nudun.in","r",stdin);
//	freopen("nudun.out","w",stdout);
#endif
	rd(n),rd(m),rd(q);
	for(int i=1;i<=m;i++)rd(B[i]);
	for(int i=1;i<=n;i++)rd(C[i]);
	for(int i=1;i<n;i++){
		int a,b;
		rd(a),rd(b);
		add_edge(a,b);
		add_edge(b,a);
	}
	for(int i=1;i<=n;i++)rd(A[i]);
	dfs(1,0);
	chain(1,1);
	for(int i=1;i<=q;i++){
		int op,a,b;
		rd(op),rd(a),rd(b);
		if(!op){
			pos[++op0]=a,old_v[op0]=A[a],new_v[op0]=A[a]=b;
		}
		else{
			if(idL[a]>idL[b])swap(a,b);
			if(idL[b]<idR[a])Q[++op1]=(node){idL[a],idL[b],op0,0,i};
			else Q[++op1]=(node){idR[a],idL[b],op0,LCA(a,b),i};
		}
	}
	sort(Q+1,Q+1+op1);
	int now=op0,l=Q[1].l,r=l-1;/*detail*/
	for(int i=1;i<=op1;i++){
		int L=Q[i].l,R=Q[i].r,t=Q[i].t,lca=Q[i].lca,id=Q[i].id;
		while(r<R)add(reid[++r]);
		while(l>L)add(reid[--l]);
		while(r>R)add(reid[r--]);
		while(l<L)add(reid[l++]);
		while(now<t){
			now++;
			if(mark[pos[now]]){/*must*/
				add(pos[now]);
				A[pos[now]]=new_v[now];
				add(pos[now]);
			}
			else A[pos[now]]=new_v[now];
		}
		while(now>t){
			if(mark[pos[now]]){/*must*/
				add(pos[now]);
				A[pos[now]]=old_v[now];
				add(pos[now]);
			}
			else A[pos[now]]=old_v[now];
			now--;
		}
		if(lca)add(lca);
		ans[id]=res;
		if(lca)add(lca);
	}
	for(int i=1;i<=q;i++)if(ans[i])printf("%lld\n",ans[i]);
	return 0;
}
```



### 回滚莫队*

### 二次离线莫队*

## 线段树分治*

## CDQ分治*

## 整体二分*

## Splay Tree*

## Link Cut Tree*

## 支持任意删除的堆

代码一：精简版本

```cpp
struct Queue{
	priority_queue<int>A,B;
	void push(int x){A.push(x);}
	void pop(int x){
		B.push(x);
		while(!B.empty()&&A.top()==B.top())A.pop(),B.pop();
	}
	int top(){return A.top();}
};
```

代码二：完整版本

```cpp
struct Queue{
	priority_queue<int>A,B;
	void push(int x){
		A.push(x);
	}
	void pop(int x){
		B.push(x);
		while(!A.empty()&&!B.empty()&&A.top()==B.top())A.pop(),B.pop();
	}
	void pop(){
		if(A.empty())return;
		A.pop();
		while(!A.empty()&&!B.empty()&&A.top()==B.top())A.pop(),B.pop();
	}
	int top(){
		if(A.empty())return -1e9;
		else return A.top();
	}
	void clear(){
		while(!A.empty())A.pop();
		while(!B.empty())B.pop();
	}
	bool empty(){
		return A.empty();
	}
};
```



## 哈希表实现map

代码一：STL版本

```cpp
unordered_map<int,int>mp;
```

代码二：手写版本（int->int）

```cpp
struct hash_map{
	static const int M=1e6+5;
	static const int S=1;//注意空间溢出
	int tot,head[M],key[M*S],value[M*S],nxt[M*S];
	int Hash(int x){
		if(x<0)x=-x;
		return x%(M-1)+1;
	}
	int& operator [](int x){
		int pos=Hash(x);
		for(int i=head[pos];i;i=nxt[i])
			if(key[i]==x)return value[i];
		key[++tot]=x,value[tot]=0,nxt[tot]=head[pos],head[pos]=tot;
		return value[tot];
	}
};
```

代码三：手写版本（整数->所有类型）

```cpp
template<class KEY,class VALUE>struct hash_map{
	static const int M=1e6+5;
	static const int S=1;//注意空间溢出
	int tot,head[M],nxt[M*S];
	KEY key[M*S];
	VALUE value[M*S];
	int Hash(KEY x){
		if(x<0)x=-x;
		return x%(M-1)+1;
	}
	VALUE& operator [](KEY x){
		int pos=Hash(x);
		for(int i=head[pos];i;i=nxt[i])
			if(key[i]==x)return value[i];
		key[++tot]=x,nxt[tot]=head[pos],head[pos]=tot;
		value[tot]=0;//根据类型初始化
		return value[tot];
	}
};
```

## 思想收集

用线段树合并优化树形dp

### WQS二分

（模板题：求恰好有k条特定边的最小生成树 https://www.luogu.com.cn/problem/P2619）

应用条件：

1. 在一定限制下，求恰好选 k 个特定物品的最小代价（最大价值）
2. 选择物品的代价（价值）随 k 变化的曲线是凸函数

做法：

二分一个 v ，通过让特定物品的代价加上 v（价值减上 v ）来控制选择的特定物品的数量，再根据选择的数量与 k 比较来调整 v 。

最后的答案要加减 k * v 。

### tfw乱搞栈_qwq

给一个长为n的序列，m次操作，对于每次操作：
1 x v ：在[x,n]区间上加上 v 
2 v ：在序列末尾添加一个数 v ，n++
3 ：查询整个序列的最大值

（可以用维护差值来实现相同的功能）

```cpp
struct tfw_stack{
	static const int M=1e6+5;
	int n,sum,fa[M],L[M],val[M],lazy[M];
	tfw_stack(){
		n=sum=0;
	}
	int getfa(int x){
		return fa[x]==x?x:fa[x]=getfa(fa[x]);
	}
	void update(int x,int v){
		x=getfa(x);
		val[x]+=v;
		lazy[x]+=v;
		sum+=v;
		while(L[x]&&val[x]+lazy[L[x]]>=val[L[x]]){
			int y=L[x];
			val[x]+=lazy[y];
			lazy[x]+=lazy[y];
			fa[y]=x;
			L[x]=L[y];
		}
	}
	void push(int v){
		n++;
		fa[n]=n,L[n]=n-1;
		val[n]=lazy[n]=0;
		update(n,v-sum);
	}
	int top(){
		return val[getfa(1)];
	}
};
```





# 树论

## 树链剖分+LCA

```cpp
const int M=1e5+5;
int head[M],nxt[M<<1],to[M<<1],tot;
int dfsid,fa[M],deep[M],sz[M],son[M],top[M],dfn[M],reid[M];
void add_edge(int a,int b){
	nxt[++tot]=head[a];
	to[tot]=b;
	head[a]=tot;
}
void dfs(int x,int f){
	fa[x]=f;
	deep[x]=deep[f]+1;
	sz[x]=1;
	son[x]=0;
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(y==f)continue;
		dfs(y,x);
		sz[x]+=sz[y];
		if(sz[y]>sz[son[x]])son[x]=y;
	}
}
void chain(int x,int t){
	top[x]=t;
	reid[dfn[x]=++dfsid]=x;
	if(son[x])chain(son[x],t);
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(y==fa[x]||y==son[x])continue;
		chain(y,y);
	}
}
int LCA(int x,int y){
	while(top[x]!=top[y]){
		if(deep[top[x]]<deep[top[y]])swap(x,y);
		x=fa[top[x]];
	}
	return deep[x]<deep[y]?x:y;
}
```

## 树上倍增+LCA*

## DSU on tree

```cpp
const int M=1e5+5;
int n,A[M],cnt[M],mxcnt;
ll ans[M],sum;
int head[M],nxt[M<<1],to[M<<1],tot;
void add_edge(int a,int b){
	nxt[++tot]=head[a];
	to[tot]=b;
	head[a]=tot;
}
int fa[M],sz[M],son[M];
void dfs(int x,int f){
	fa[x]=f;
	sz[x]=1;
	son[x]=0;
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(y==f)continue;
		dfs(y,x);
		sz[x]+=sz[y];
		if(sz[y]>sz[son[x]])son[x]=y;
	}
}
void insert(int val,int sign){
	cnt[val]+=sign;
	if(sign>0){
		if(cnt[val]>mxcnt)mxcnt=cnt[val],sum=val;
		else if(cnt[val]==mxcnt)sum+=val;
	}
	else mxcnt=sum=0;
}
void rdfs(int x,int sign){
	insert(A[x],sign);
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(y==fa[x])continue;
		rdfs(y,sign);
	}
}
void dsu(int x){
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(y==fa[x]||y==son[x])continue;
		dsu(y);
		rdfs(y,-1);
	}
	if(son[x])dsu(son[x]);
	insert(A[x],1);
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(y==fa[x]||y==son[x])continue;
		rdfs(y,1);
	}
	ans[x]=sum;
}
int main(){
#ifndef ONLINE_JUDGE
//	freopen("nudun.in","r",stdin);
//	freopen("nudun.out","w",stdout);
#endif
	rd(n);
	for(int i=1;i<=n;i++)rd(A[i]);
	for(int i=1;i<n;i++){
		int a,b;
		rd(a),rd(b);
		add_edge(a,b);
		add_edge(b,a);
	}
	dfs(1,0);
	dsu(1);
	for(int i=1;i<=n;i++)printf("%lld%c",ans[i],i==n?'\n':' ');
	return 0;
}
```

## 点分治*

## 树上差分

要求：先修改后查询，且修改的是一条路径。

树上的差分，一个点的权值就是其子树的差分值之和再加其初始值。

修改从a到b的路径只需差分值在a和b处加（插入），在lca和fa[lca]处减（撤销）。

dfs遍历时从下往上更新，每个节点合并其每个子节点的累计差分值，得出该点的权值。





# 图论

哈密顿回路（点的回路），欧拉回路（边的回路）

## 最短路*

## 差分约束*

## 二分图

### 二分图最大匹配

匈牙利算法 P3386

二分图左边n个点，右边m个点，e条边，求二分图最大匹配

```cpp
const int M=505<<1;
const int N=5e4+5;
int head[M],nxt[N],to[N],tot;
void add_edge(int a,int b){
	nxt[++tot]=head[a];
	to[tot]=b;
	head[a]=tot;
}
int n,m,e;
int mark[M],match[M];
bool dfs(int x){
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(mark[y])continue;
		mark[y]=1;
		if(!match[y]||dfs(match[y])){
			match[x]=y;
			match[y]=x;
			return 1;
		}
	}
	return 0;
}
int main(){
#ifndef ONLINE_JUDGE
//	freopen("nudun.in","r",stdin);
//	freopen("nudun.out","w",stdout);
#endif
	rd(n),rd(m),rd(e);
	while(e--){
		int a,b;rd(a),rd(b);
		add_edge(a,n+b);
	}
	int ans=0;
	for(int i=1;i<=n;i++)if(!match[i]){
		memset(mark,0,sizeof(mark));
		ans+=dfs(i);
	}
	printf("%d\n",ans);
	return 0;
}
```

### 二分图最小点覆盖

定义：选出最少的点，满足每条边至少有一个端点被选

算法：二分图中，最小点覆盖 = 最大匹配，数值上相等

### 二分图最小边覆盖

定义：选出最少的边，满足每个点至少有一条边被选

算法：二分图中，最小边覆盖 = 总点数 - 最大匹配

### 二分图最大独立集

定义：选出最多的点，满足两两之间没有边相连

算法：最大独立集 = 点数 - 最小顶点覆盖，两者恰为补集。

### 二分图最大团

定义：选出最多的点，满足二分图两侧的点对之间都有边相连

算法：二分图中，最大团 = 补图的最大独立集

### DAG最大权闭合子图

定义：有向无环图中，找出权值和最大的一个集合，满足集合内所有边都连向点集内的边（点权可以为负）

算法：建立（源点，正权点，对应权值）、（正权点，负权点，INF）、（负权点，汇点，对应权值的绝对值）的网络，

​			最大权闭合子图 = 正权点权值之和 - 最小割

### DAG最小不相交路径覆盖

定义：有向无环图中，找出最少的路径，使得这些路径经过了所有的点，且每一条路径经过的顶点各不相同

算法：把原图中的点 V 拆成两个点 Vx 和 Vy ，对于原图中的边 A->B ，在新图中建立一条 Ax->By 的边

​			那么，最小不相交路径覆盖 = 原图的点数 - 新图的最大匹配

### DAG最小可相交路径覆盖

定义：有向无环图中，找出最少的路径，使得这些路径经过了所有的点，路径可以相交

算法：先用floyd求出原图的传递闭包：如果a到b有路， 那么就添加一条从a到b的边。然后就转化成了最小不相交路径覆盖问题

### DAG最大独立集

定义：选出最多的点，满足两两之间没有边相连

算法：有向无环图中，最大独立集 = 最小不相交路径覆盖

### DAG最长反链

定义：选出最多的点，满足两两之间没有路径相连

算法：有向无环图中，最长反链 = 最小可相交路径覆盖

## 最大流

### dinic

分层用bfs，增广用dfs，复杂度$O(n^{2}∗m)$

```cpp
const int SIZE=1e5+5;
const int inf=(1ll<<31)-1;
int head[SIZE],nxt[SIZE<<1],to[SIZE<<1],flow[SIZE<<1],tot;
void add_edge(int a,int b,int c){
	nxt[++tot]=head[a];
	to[tot]=b;
	flow[tot]=c;
	head[a]=tot;
}
void add(int a,int b,int c){
	add_edge(a,b,c);
	add_edge(b,a,0);
}
int n,m,S,T;
int Q[SIZE],deep[SIZE],cur[SIZE];
int bfs(int sz=T){
	for(int i=0;i<=sz;i++)deep[i]=0;
	for(int i=0;i<=sz;i++)cur[i]=head[i];
	int l=1,r=0;
	deep[Q[++r]=S]=1;
	while(l<=r){
		int x=Q[l++];
		for(int i=head[x];i;i=nxt[i]){
			int y=to[i];
			if(!deep[y]&&flow[i])
				deep[Q[++r]=y]=deep[x]+1;
		}
	}
	return deep[T]>0;
}
int dfs(int x=S,int lim=inf){
	if(x==T||!lim)return lim;
	int res=0;
	for(int &i=cur[x];i;i=nxt[i]){
		int y=to[i];
		if(deep[y]==deep[x]+1){
			int f=dfs(y,min(lim,flow[i]));
			res+=f;
			lim-=f;
			flow[i]-=f;
			flow[i^1]+=f;
			if(!lim)break;
		}
	}
	return res;
}
int main(){
#ifndef ONLINE_JUDGE
//	freopen("nudun.in","r",stdin);
//	freopen("nudun.out","w",stdout);
#endif
	memset(head,0,sizeof(head));
	tot=1;//important
	rd(n),rd(m),rd(S),rd(T);
	for(int i=1;i<=m;i++){
		int a,b,c;
		rd(a),rd(b),rd(c);
		add(a,b,c);
	}
	ll mxflow=0;
	while(bfs(n))mxflow+=dfs();
	printf("%lld\n",mxflow);
	return 0;
}
```

其它算法

Ford-Fulkerson：不分层直接dfs，复杂度$O(n*m*f)$

Edmonds-Karp：不分层直接bfs，复杂度$O(n∗m^{2})$

MPLA：分层和增广都用bfs，复杂度$O(n∗m^{2})$

MPM：？？？

#### ISAP*

（距离标号最短增广路）

#### 预流推进

复杂度$O(n^{2}∗m)$，还不如dinic。。。

```cpp
int n,m,S,T,H[SIZE];
ll keep[SIZE];
ll max_flow(int sz=T){
	for(int i=1;i<=sz;i++)H[i]=keep[i]=0;
	for(int i=head[S];i;i=nxt[i]){
		int y=to[i],f=flow[i];
		keep[y]+=f;
		keep[S]-=f;
		flow[i]-=f;
		flow[i^1]+=f;
	}
	H[S]=sz;
	int Qsz=1,Esz;
	while(Qsz){
		Qsz=0;
		for(int x=1;x<=sz;x++)if(x!=S&&x!=T&&keep[x]){
			Qsz++,Esz=0;
			for(int i=head[x];i;i=nxt[i]){
				int y=to[i];
				if(H[x]>H[y]&&flow[i]){
					int f=min(keep[x],1ll*flow[i]);
					keep[y]+=f;
					keep[x]-=f;
					flow[i]-=f;
					flow[i^1]+=f;
					Esz++;
				}
			}
			if(!Esz){
				int mi=1e9;
				for(int i=head[x];i;i=nxt[i])
					if(flow[i])MIN(mi,H[to[i]]);
				H[x]=mi+1;
			}
		}
	}
	return keep[T];
}
```

#### 最高标号预流推进

复杂度$O(n^{2}\sqrt{m})$，经典版本数据随机情况下不比dinic慢

```cpp
const int SIZE=1e5+5;
const int inf=1e9;//can't be (1ll<<31)-1
int head[SIZE],nxt[SIZE<<1],to[SIZE<<1],flow[SIZE<<1],tot;
void add_edge(int a,int b,int c){
	nxt[++tot]=head[a];
	to[tot]=b;
	flow[tot]=c;
	head[a]=tot;
}
void add(int a,int b,int c){
	add_edge(a,b,c);
	add_edge(b,a,0);
}
int n,m,S,T,h[SIZE],e[SIZE],mark[SIZE],gap[SIZE<<1];
struct cmp{
	bool operator ()(int a,int b)const{
		return h[a]<h[b];
	}
};
priority_queue<int,vector<int>,cmp>Q;
bool bfs(int sz){
	static int Q[SIZE];
	for(int i=1;i<=sz;i++)h[i]=inf;
	int r=0,l=1;
	h[Q[++r]=T]=0;
	while(l<=r){
		int x=Q[l++];
		for(int i=head[x];i;i=nxt[i]){
			int y=to[i];
			if(h[y]==inf&&flow[i^1])
				h[Q[++r]=y]=h[x]+1;
		}
	}
	return h[S]!=inf;
}
void push(int x){
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(h[x]==h[y]+1&&flow[i]){
			int f=min(e[x],flow[i]);
			e[y]+=f;
			e[x]-=f;
			flow[i]-=f;
			flow[i^1]+=f;
			if(y!=S&&y!=T&&!mark[y]){
				Q.push(y);mark[y]=1;
			}
			if(!e[x])break;
		}
	}
}
void relabel(int x){
	h[x]=inf;
	for(int i=head[x];i;i=nxt[i]){
		int y=to[i];
		if(flow[i])MIN(h[x],h[y]+1);
	}
}
int hlpp(int sz=T){
	if(!bfs(sz))return 0;
	h[S]=sz;
	for(int i=1;i<=sz;i++)e[i]=mark[i]=0;
	for(int i=0;i<=2*sz;i++)gap[i]=0;
	for(int i=1;i<=sz;i++)if(h[i]!=inf)gap[h[i]]++;
	for(int i=head[S];i;i=nxt[i]){
		int y=to[i],f=flow[i];
		e[y]+=f;
		e[S]-=f;
		flow[i]-=f;
		flow[i^1]+=f;
		if(f&&y!=S&&y!=T&&!mark[y]){
			Q.push(y);mark[y]=1;
		}
	}
	while(!Q.empty()){
		int x=Q.top();
		Q.pop();mark[x]=0;
		push(x);
		if(e[x]){
			gap[h[x]]--;
			if(!gap[h[x]])for(int i=1;i<=sz;i++)
				if(i!=S&&i!=T&&h[x]<h[i]&&h[i]<=sz)h[i]=sz+1;
			relabel(x);
			gap[h[x]]++;
			Q.push(x);mark[x]=1;
		}
	}
	return e[T];
}
int main(){
#ifndef ONLINE_JUDGE
//	freopen("nudun.in","r",stdin);
//	freopen("nudun.out","w",stdout);
#endif
	memset(head,0,sizeof(head));
	tot=1;//important
	rd(n),rd(m),rd(S),rd(T);
	for(int i=1;i<=m;i++){
		int a,b,c;
		rd(a),rd(b),rd(c);
		add(a,b,c);
	}
	printf("%d\n",hlpp(n));
	return 0;
}
```

## 最小割模型

1，求**最大权闭合子图**：求图G的一个点集的最大点权和，满足点集内所有点的出边都指向点集内的点（允许点权带负）。

原问题等价于**给定一些二元组，选了a就必须选择b**

将原问题转化为最小割问题，初态为选了所有的a，没选所有的b，初始答案为a的权值和

S向a点连容量为val[a]的边，b点向T连容量为-val[b]的边，a向b连容量为inf的边，求最大流

最终答案为 **a的权值和 - 最小割**

2，

原问题等价于**给定一些二元组，选了a就不能选择b**

将原问题转化为最小割问题，初态为选了所有的点，初始答案为所有点的权值和

S向a点连容量为val[a]的边，b点向T连容量为val[b]的边，a向b连容量为inf的边，求最大流

最终答案为 **所有点的权值和 - 最小割**

## 费用流

```cpp
const int SIZE=5e4+5;
const int inf=(1ll<<31)-1;
const ll INF=1e18;
int head[SIZE],nxt[SIZE<<1],to[SIZE<<1],flow[SIZE<<1],cost[SIZE<<1],tot;
void add_edge(int a,int b,int c,int d){
	nxt[++tot]=head[a];
	to[tot]=b;
	flow[tot]=c;
	cost[tot]=d;
	head[a]=tot;
}
void add(int a,int b,int c,int d){
	add_edge(a,b,c,d);
	add_edge(b,a,0,-d);
}
int n,m,S,T;
int Q[SIZE],mark[SIZE],lim[SIZE],pre[SIZE],lst[SIZE];
ll dis[SIZE],mxflow,micost;
bool SPFA(int sz){
	for(int i=1;i<=sz;i++)dis[i]=INF,lim[i]=inf,mark[i]=0;
	int l=0,r=0;
	Q[r=r%sz+1]=S;
	dis[S]=0;
	pre[T]=0;
	while(l!=r){
		int x=Q[l=l%sz+1];
		mark[x]=0;
		for(int i=head[x];i;i=nxt[i]){
			int y=to[i];
			if(flow[i]&&dis[x]+cost[i]<dis[y]){
				dis[y]=dis[x]+cost[i];
				pre[y]=x;
				lst[y]=i;
				lim[y]=min(lim[x],flow[i]);
				if(!mark[y]){
					Q[r=r%sz+1]=y;
					mark[y]=1;
				}
			}
		}
	}
	return pre[T]>0;
}
void MCMF(int sz=T){
	while(SPFA(sz)){
		mxflow+=lim[T];
		micost+=1ll*lim[T]*dis[T];
		for(int i=T;i!=S;i=pre[i]){
			flow[lst[i]]-=lim[T];
			flow[lst[i]^1]+=lim[T];
		}
	}
}
int main(){
#ifndef ONLINE_JUDGE
//	freopen("nudun.in","r",stdin);
//	freopen("nudun.out","w",stdout);
#endif
	memset(head,0,sizeof(head));
	tot=1;
	rd(n),rd(m),rd(S),rd(T);
	for(int i=1;i<=m;i++){
		int a,b,c,d;
		rd(a),rd(b),rd(c),rd(d);
		add(a,b,c,d);
	}
	MCMF(n);
	printf("%lld %lld\n",mxflow,micost);
	return 0;
}
```

### 关于网络流建图

选a必选b：求最大权闭合子图，转化为最小割模型，最后是否选则就看是否与S联通

选a不选b：转化为最小割模型，最后选了a则a与S联通，选了b则b不与S联通

二分图a和b至少选一个：a和b连边，求二分图最小点覆盖=二分图最大匹配

每个点只能经过若干次：把每个点拆为入点和出点，把点可以经过的最大次数作为点内部的流量，经过点的作用作为点内部的费用

多选一（多选多）：每个选择关系新建一个点x，x向每个选项连一条流量为1的边，源点（或其它）向x连一条流量为选择次数的边

## Prufer序列

一个n个节点的树可以用 n-2 个 [1,n] 之间的数数表示，这些数形成的序列叫 Prufer 序列，树与序列一一对应

无根树转化为 Prufer 序列：

每次将编号最小的度为1的点删除，记录与那个点相连的另外一个点，重复以上步骤直至只剩下两个点

Prufer 序列转化为无根树：

每次将点集中未被使用的编号最小的没出现在 Prufer 序列中的元素与 Prufer 序列第一个元素连边，再删除 Prufer 序列的第一个元素，重复以上步骤直至点集中只剩两个点，最后给这两个点连边

Prufer 序列的性质：

1. Caylay 公式：n 个点的无根完全图的生成树有 $n^{n-2}$ 种
2. 对于每个点，prufer 序列上出现的次数 = 度数$-1$（度数 = 出现次数$+1$）
3. n 个节点的有根树有 $n^{n-1}$ 种
4. n 个节点的度依次为 $d_1,d_2,...,d_n$ 的树共有 $\frac{(n-2)!}{\prod_{i=1}^{n}{(d_i-1)!}}$ 个
5. n 个点 m 条边的无向图，有 k 个联通块，加 k-1 条边使整个图联通的方案数为 $n^{k-2}\prod_{i=1}^{k}{s_i}$（其中 $s_i$ 为每个连通块的大小）

## 矩阵树定理*

## 斯坦纳树*





# 数学

## 整除分块

```cpp
for(int l=1,r;l<=n;l=r+1){
	r=n/(n/l);
    
}
```

## 线性筛*

### 筛质数*

### 莫比乌斯系数*

### 欧拉筛*

## 判质数

朴素算法$O(\sqrt{n})$

```cpp
bool is_prime(int n){
	if(n<=3)return n>1;
	if(n%2==0||n%3==0)return 0;
	for(int i=5;i*i<=n;i+=6)if(n%i==0||n%(i+2)==0)return 0;
	return 1;
}
```

### Miller_Rabin

**费马小定理**的逆否命题：若$a^{n-1}\not\equiv1(mod\ n)$，则$n$不为质数

**二次探测定理**的逆否命题：若$x^2\equiv1(mod\ n)$的解不为$x\equiv1$或$x\equiv{n-1}$，则$n$不为质数

```cpp
inline ll mul(ll a,ll b,ll mod){
	return (__int128)a*b%mod;
}
inline ll pow(ll a,ll b,ll mod){
	ll res=1;
	while(b){
		if(b&1)res=mul(res,a,mod);
		a=mul(a,a,mod);
		b>>=1;
	}
	return res;
}
bool miller_rabin(ll x,ll n){
	ll a=n-1,b=0;
	while(!(a&1))a>>=1,b++;
	x=pow(x,a,n);
	if(x==1)return 1;
	while(b--){
		if(x==n-1)return 1;
		x=mul(x,x,n);
	}
	return 0;
}
bool is_prime(ll n){
	if(n==1)return 0;
	static int num[]={2,3,5,7,13,29,37,89};
	for(int i=0;i<8;i++)if(n==num[i])return 1;
	for(int i=0;i<8;i++)if(!miller_rabin(num[i],n))return 0;
	return 1;
}
```

## 杂项

### 拉格朗日四平方数和定理

**结论：任意一个非负整数可以表示为四个整数的平方和**

有一个特殊的数字**169**,它分别可以表示成1,2,3,4个正平方数的和

1. 169 = 13 * 13
2. 169 = 12 * 12 + 5 * 5
3. 169 = 10 * 10 + 8 * 8 + 2 * 2 + 1 * 1
4. 169 = 12 * 12 + 4 * 4 + 2 * 2 + 2 * 2 + 1 * 1

**推论：任意一个大于169的数字都能表示成5个正平方数的和**

证明：令y=x-169（x>169）

根据拉格朗日四平方数和定理，y可以表示为1到4个正平方数的和

而169可以根据y的情况任意拆分成1到4个正平方数的和

所以x=y+169则一定可以表示成5个正平方数的和



# 字符串

## KMP

```cpp
const int M=1e6+5;
int nxt[M];
void get_nxt(char B[]){
	int m=strlen(B+1);
	nxt[1]=0;
	for(int i=2;i<=m;i++){
		int now=nxt[i-1];
		while(now&&B[i]!=B[now+1])now=nxt[now];
		nxt[i]=now+(B[i]==B[now+1]);
	}
}
int KMP(char A[],char B[]){
	int n=strlen(A+1);
	int m=strlen(B+1);
	int now=0,cnt=0;
	for(int i=1;i<=n;i++){
		while(now&&A[i]!=B[now+1])now=nxt[now];
		now+=A[i]==B[now+1];
		if(now==m){
//			return i-m+1;
			cnt++;
			now=nxt[now];
		}
	}
	return cnt;
}
```





# DP

## 未命名优化

1.如果dp'[i]表示最大值的最小值为i时的最大元素个数（首目标最大化元素个数，次目标最小化元素最大值），

将dp方程转化为dp[i]表示选了i个元素时最大元素的最小值，

那么合并dp[a] [?]和dp[b] [?]即为dp[a]数组和dp[b]数组做归并排序。

可用multiset+启发式合并维护归并排序。

## 计数dp*

## 仙人掌dp*

## dp套dp*

## 动态dp*

## 插头dp*



