---
title: "算法笔记"
tags: [ "Algorithm", "Note", "Cpp"]
description: "使用C++，包括一些基础算法：排序，搜索，字符串，STL，树，图，求质数等"
date: 2022-04-14
slug: "algorithm-note"
---

## 基础算法

### 排序

#### 快速排序
```cpp
void quicksort(int L, int R){
	if(L >= R) return;
	int i = L - 1, j = R + 1, mid = a[L + R >> 1];
	while(i < j){
		do i++; while(a[i] < mid);
		do j--; while(a[j] > mid);
		if(i < j) swap(a[i], a[j]);
	}
	quicksort(L, j);
	quicksort(j + 1, R);
}
```

#### 归并排序
```cpp
void mergesort(int L, int R) {
	if (L >= R) return;
	int mid = (L + R) >> 1;
	mergesort(L, mid);
	mergesort(mid + 1, R);
	int i = L, j = mid + 1, t = L;
	while (i <= mid && j <= R) {
		if (in[i] <= in[j]) temp[t++] = in[i++];
		else temp[t++] = in[j++];
	}
	while (i <= mid) temp[t++] = in[i++];
	while (j <= R)temp[t++] = in[j++];
	for (int k = L; k <= R; ++k) in[k] = temp[k];
}
```

#### 插入排序
```cpp
void insertsort(int l, int r){
	for(int i = l; i <= r; ++i){
		int t = a[i];
		int k = i;
		while(a[k - 1] > t){
			a[k] = a[k - 1];
			k--;
		}
		a[k] = t;
	}
}
```

#### 堆排序
- 宏定义
```cpp
#define	F (u >> 1)
#define Ls (u << 1)
#define Rs (u << 1 | 1)
```
- 上推操作
```cpp
void up(int u){
	while(F && tr[u] < tr[F]){
		heap_swap(u, F);
		u >>= 1;
	}
}
```
- 下推操作
```cpp
void down(int u){
	int t = u;
	if(Ls <= cnt && tr[Ls] < tr[t]) t = Ls;
	if(Rs <= cnt && tr[Rs] < tr[t]) t = Rs;
	if(u != t){
		swap(tr[u], tr[t]);
		down(t);
	}
}
```
- 初始化
```cpp
cnt = n;
for(int i = n / 2; i ; --i) down(i);
```
- 输出
```cpp
while(m--){
	cout << tr[1] << " ";
	tr[1] = tr[cnt--];
	down(1);
}
```

---
### 二分

#### 易懂版本
```cpp
int binary_search(int arr[], int l, int r, int x)
{
	int mid;
	while (l <= r)
    {
        mid = l + r >> 1;
		if(arr[mid] == x) return mid;
        else if(arr[mid] > x) r = mid - 1;
        else l = mid + 1;
    }
    return -1;
}
```

#### 高效版本
- 注：
  - 若if-else部分l = mid，则mid需要加1 
  - 否则若if-else部分l = mid + 1，则mid不需要加1 
  - 若`check(mid)==true`时设置`r = mid`，则查找出的可能存在结果的区间为`[left，mid)`
  - 相反，若`check(mid)==true`时设置`l = mid`，则查找出的可能存在结果的区间为`(mid, right]`
- 这两个都是可能存在结果的范围，是否实际存在需要再加if判断


> 左边界
- 分割区间为[left, mid][mid + 1, right]
```cpp
int bsearch_left(int l, int r)
{
    while (l < r)
    {
        int mid = l + r >> 1;
        if (check(mid)) r = mid;
        else l = mid + 1;
    }
    return l;
}
```

> 右边界
- 分割区间为[left, mid - 1][mid, right]
```cpp
int bsearch_right(int l, int r)
{
    while (l < r)
    {
        int mid = l + r + 1 >> 1;
        if (check(mid)) l = mid;
        else r = mid - 1;
    }
    return l;
}
```

---
### 三分
- 选取L, R中点为mid
- 选取mid, R中点为mmid
- 比较mid和mmid
- 推断l, r接下来为哪个点
  - 例：函数最值点：
```cpp
void fun(double l, double r) {
	while (r - l > 0.000001) {
		double mid = (l + r) / 2;
		double mmid = (mid + r) / 2;
		if (f(mid) > f(mmid)) r = mmid;//mmid < mid,mmid一定在最值右边，mid无法确定
		//mmid > mid, mid一定在最值左边， mmid无法确定
		else l = mid;
	}
	printf("%.5lf\n", r);
}
```

---
### 高精度

#### 预处理
```cpp
for (int i = a.size() - 1; i >= 0; i -- ) A.push_back(a[i] - '0');
for (int i = b.size() - 1; i >= 0; i -- ) B.push_back(b[i] - '0');
```

#### 高精加
```cpp
vector<int> add(vector<int> &A, vector<int> &B)
{
    if (A.size() < B.size()) return add(B, A);

    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size(); i ++ )
    {
        t += A[i];
        if (i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }

    if (t) C.push_back(t);
    return C;
}
```

#### 高精减
```cpp
bool cmp(vector<int> &A, vector<int> &B)
{
    if (A.size() != B.size()) return A.size() > B.size();

    for (int i = A.size() - 1; i >= 0; i -- )
        if (A[i] != B[i])
            return A[i] > B[i];

    return true;
}

vector<int> sub(vector<int> &A, vector<int> &B)
{
    vector<int> C;
    for (int i = 0, t = 0; i < A.size(); i ++ )
    {
        t = A[i] - t;
        if (i < B.size()) t -= B[i];
        C.push_back((t + 10) % 10);
        if (t < 0) t = 1;
        else t = 0;
    }

    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}
```

#### 高精乘

```cpp
vector<int> mul(vector<int> &A, int b)
{
    vector<int> C;

    int t = 0;
    for (int i = 0; i < A.size() || t; i ++ )
    {
        if (i < A.size()) t += A[i] * b;
        C.push_back(t % 10);
        t /= 10;
    }

    while (C.size() > 1 && C.back() == 0) C.pop_back();

    return C;
}

```

#### 高精除

```cpp
vector<int> div(vector<int> &A, int b, int &r)
{
    vector<int> C;
    r = 0;
    for (int i = A.size() - 1; i >= 0; i -- )
    {
        r = r * 10 + A[i];
        C.push_back(r / b);
        r %= b;
    }
    reverse(C.begin(), C.end());
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}
```

---
### 位运算

- `num & 1 == 1`为奇数
- `num & 1 == 0`为偶数
- 快速去重
- 两个相同的数`^`会抵消
- `0 ^ num <=> num`
```cpp
int num = a[0];
for(int i = 1; i < n; ++i){
	num ^= a[i + 1];
}
```
- 或`|`所有数会将其二进制上为1的位置标记
- sum = 100010
- x = 100100
- sum | x = 100110


---
### 欧几里得求最大公约数算法

```cpp
int gcd(int a, int b){
    return b ? gcd(b , a % b) : a;
}
```

---
### 数学
- `floor()`向下取整
- `ceil()`向上取整
- `1GB` = `1024MB`
- `1MB` = `1024KB`
- `1KB` = `1024B` = `1024Byte`
- `1Byte` = `8bit`
- 求逆元
  - 在模p意义下除以x等价于乘以x的逆元：x^(p-2)^

***[返回目录](#目录)***

---
---
## 快读
```cpp
inline int read() {
	int x = 0, f = 1;
	char c = getchar();
	while (c < '0' || c > '9') {
		if (c == '-') f = -1;
		c = getchar();
	}
	while (c >= '0' && c <= '9') {
		x = (x << 3) + (x << 1) + (c ^ 48);
		c = getchar();
	}
	return x * f;
}
```
***[返回目录](#目录)***

---
---
## 二维差分
给定一个二维数组，要求对面积进行加减c，求最后的二维数组
- 将原数组差分化
- 统一操作
- 输出数组
- 由差分和前缀和的关系可知，差分数组计算（0，0）的前缀和即可化成原数组，原数组可以在本身位置标记一个数转化成差分数组，所以先将原数组化为差分数组，差分数组a[i][j]代表从（i，j)位置到（n，m）位置的所有数字都+a[i][j]，最后将差分数组还原为原数组，只需统计一下前缀和即可
```cpp
int b[N][N];

void insert(int x1, int y1, int x2, int y2, int c) {
	b[x1][y1] += c;
	b[x2 + 1][y1] -= c;
	b[x1][y2 + 1] -= c;
	b[x2 + 1][y2 + 1] += c;
}

int main() {
	int n, m, q;
	int x1, x2, y1, y2, c;
	cin >> n >> m >> q;
	for (int i = 1; i <= n; ++i)//读入二维数组
		for (int j = 1; j <= m; ++j) {
			cin >> c;
			insert(i, j, i, j, c);//差分处理
		}

	for (int i = 0; i < q; ++i) {//进行操作
		cin >> x1 >> y1 >> x2 >> y2 >> c;
		insert(x1, y1, x2, y2, c);
	}

	for (int i = 1; i <= n; ++i) {
		for (int j = 1; j <= m; ++j) {//输出
			b[i][j] += b[i - 1][j] + b[i][j - 1] - b[i - 1][j - 1];
			cout << b[i][j] << " ";
		}
		puts("");
	}
}
```
***[返回目录](#目录)***

---
---
## 双指针
[最长连续不重复子序列](https://www.acwing.com/problem/content/801/)
一个指针`i`在前一个指针`j`在后锁定区间长度，同时计算这个区间内有无重复元素，若有则`j++`，否则`i++`
```cpp
int main()
{
	int n;
	cin >> n;
	for(int i = 0; i < n; ++i) cin >> a[i];
	
	int j = 0, i = 0, ans = 0;
	while(i < n){
		cnt[a[i]]++;
		while(cnt[a[i]] > 1 && j <= i){
			cnt[a[j]]--;
			j++;
		}
		ans = max(ans, i - j + 1);
		i++;
	}
	cout << ans << endl;
	return 0;
}
```
***[返回目录](#目录)***

---
---
## DP

### 背包DP
- 公式为f[i][j] = max(f[i][j], f[i - 1][j - v[i]] + w[i]]);意义为取i个物品容量不超过j的最大价值，因为只有i和i-1两层需要使用，可以通过控制遍历顺序来达到使用不同两层价值的目的，上一层为`j-v[i]`<当前层`j`，所以从大到小遍历，同时防止越界，j遍历到v[i]就停止。
#### [01背包](https://www.acwing.com/problem/content/2/)
```cpp
int v[N], w[N], f[N];

int main(){
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; i ++ ) cin >> v[i] >> w[i];
    
    for (int i = 1; i <= n; i ++ )
        for (int j = m; j >= v[i]; j -- )
            f[j] = max(f[j], f[j - v[i]] + w[i]);
            
    cout << f[m] << endl;
}
```

#### 完全背包
```cpp
int v[N], w[N], dp[N];

int main()
{
    int n, m;
    cin >> n >> m;
    
    for (int i = 1; i <= n; i ++ ) cin >> v[i] >> w[i];
    
    for (int i = 1; i <= n; i ++ )
        for (int j = v[i]; j <= m; j ++ )
            dp[j] = max(dp[j], dp[j - v[i]] + w[i]);
            
    cout << dp[m] << endl;
}
```
***[返回目录](#目录)***

### 线性DP

#### 最长上升子序列
- 定义f[i]代表以第i个数结尾的最长上升子序列的长度，则f[i] = max(f[j]) + 1;`j = 0 ~ i - 1`也就是前`1 ~ i - 1`中的最长的子序列长度加一，同时为了保证是上升序列，要加上a[i] > a[j]的条件
```cpp
int a[N], f[N];

int main(){
    int n;
    cin >> n;
    for (int i = 1; i <= n; i ++ ) cin >> a[i];

    for (int i = 1; i <= n; i ++ ){
        f[i] = 1;
        for (int j = 1; j < i; j ++ )
            if(a[j] < a[i]) f[i] = max(f[j] + 1, f[i]);
    }

    int ans = 0;
    for (int i = 1; i <= n; i ++ ) ans = max(f[i], ans);

    cout << ans << endl;
    return 0;
}
```

#### 最长公共子序列
```cpp
char a[N], b[N];
int f[N][N];

int main(){
    int n, m;
    cin >> n >> m >> a + 1 >> b + 1;
    for (int i = 1; i <= n; i ++ )
        for (int j = 1; j <= m; j ++ ){
            f[i][j] = max(f[i][j -1], f[i - 1][j]);
            if(a[i] == b[j]) f[i][j] = max(f[i][j], f[i - 1][j - 1] + 1);
        }
            
    cout << f[n][m] << endl;
    return 0;
}
```
***[返回目录](#目录)***

### 树状DP
- [没有上司的舞会](https://www.luogu.com.cn/problem/P1352)
```cpp
void dfs(int u) {
	for (int i = head[u]; i != -1; i = ne[i]) {
		int v = to[i];
		dfs(v);//先搜索到叶子
		dp[u][0] += max(dp[v][1], dp[v][0]);//由子节点向上dp，按照题意更改
		dp[u][1] += dp[v][0];
	}
}

int main() {
	int n, v, u, root;
	cin >> n;
	for (int i = 1; i <= n; ++i) cin >> dp[i][1];

	memset(head, -1, sizeof head);
	for (int i = 1; i < n; ++i) {
		cin >> v >> u;
		add(u, v);
		in[v]++;
	}
	for (int i = 1; i <= n; ++i)
		if (!in[i]) {
			root = i;
			break;
		}
	dfs(root);//从根向下dp
	cout << max(dp[root][1], dp[root][0]) << endl;//将dp结果取最大值
	return 0;
}
```

***[返回目录](#目录)***

--- 
---
## 数据结构

### 树状数组

#### 求父节点与子节点距离
- x + lowbit(x)能查找父节点
- x - lowbit(x)能查找同级的上一个子节点，若为最后一个节点，则x变为0
- 查找同级下一个子节点为x + (lowbit(x) >> 1)
```cpp
#define lowbit(x) (x & (-x))
```

#### 更新数组
```cpp
void update(int x, int value) {
	a[x] += value;
	while (x <= n) {
		tree[x] += value;//当前节点更新
		x += lowbit(x);//找下一个父节点
	}
}
```

#### 前缀和
```cpp
int getsum(int x){
    int ans = 0;
    while(x > 0){
        ans += tree[x];
        x -= lowbit(x);
    }
    return ans;
}
```

#### 找到区间最大值
```cpp
void update(int x) {
	while (x <= n) {
		tree[x] = a[x];//初始化
		for (int i = 1; i < lowbit(x); i <<= 1)//遍历lowbit(x)范围所有节点
			tree[x] = max(tree[x], tree[x - i]);//更新
		x += lowbit(x);//找到下一个父节点
	}
}
void query(int l, int r){
	int ans = 0;//初始化
	while(l <= r){
		ans = max(a[r], ans);//更新最大值
		r--;//找到邻近的点
		for(;l <= r - lowbit(r); r -= lowbit(r))//遍历子节点更新最大值
			ans = max(tree[r], ans);
	}
	cout << ans << endl;//输出答案
}
int main(){
	for (int i = 1; i <= n; ++i){
		cin >> a[i];
		update(i);
	}
}
```

***[返回目录](#目录)***

### ST表
- ST表可实现O(nlogn)的建立，O(1)的查找区间最值
#### 查询
```cpp
int query(int l, int r){
	int k = log2(r - l + 1);
	return max(a[l][k], a[r - (1 << k) + 1][k]);//两个方向取最大值，因为k不一定覆盖整个区间
}
```

#### 建立
- a[i][j]表示从i开始，总个数为$2^j$大小的区间的最大值，因此每个区间的递推公式可写成`a[i][j]=max(a[i][j - 1], a[i + (1 << (j - 1))][j - 1])`
```cpp
for(int i = 1; i <= n; ++i) scanf("%d", &a[i][0]);
	
for(int i = 1; i <= sum; ++i)//sum为总数所占的二进制位数
	for(int j = 1; j + (1 << i) - 1 <= n; ++j)
		a[j][i] = max(a[j][i - 1], a[j + (1 << (i - 1))][i - 1]);
```
***[返回目录](#目录)***

### 线段树

#### 豪华define套餐
```cpp
#define Start 1, 1, n
#define Mid (l + r >> 1)
#define Ls (u << 1)
#define Rs (u << 1 | 1)
#define Lson Ls, l, Mid
#define Rson Rs, Mid + 1, r
```

#### 建立
` 初始化每个值为1
```cpp
void build(int u, int l, int r) {
	tree[u] = 1;
	if (l == r) return;
	int mid = l + r >> 1;
	build(u << 1, l, mid);
	build(u << 1 | 1, mid + 1, r);
}
```
- 初始化每个值为0，每个叶子为arr数组
```cpp
void build(int u, int l, int r) {
	if (l == r) tree[u] = { l, r, arr[r] };
	else {
		tree[u] = { l, r };
		int mid = l + r >> 1;
		build(u << 1, l, mid);
		build(u << 1 | 1, mid + 1, r);
		push_up(u);
	}
}
```

#### 更新父节点
- 可根据线段树的需求更改子结点与父节点的关系
- 父节点为子节点相乘
```cpp
void push_up(int u) {
	tree[u] = (tree[u << 1] * tree[u << 1 | 1]) % M;
}
```
- 父节点是子节点的最大值
```cpp
void push_up(int u) {
	tree[u].v = max(tree[u << 1].v, tree[u << 1 | 1].v);
}
```

#### 变更值
```cpp
void update(int u, int x, int v) {
	if (tree[u].l == tree[u].r) tree[u].v = max(tree[u].v, v);//找到叶子节点，更新子节点
	else {
		int mid = tree[u].l + tree[u].r >> 1;
		if (x <= mid) update(u << 1, x, v);
		else update(u << 1 | 1, x, v);
		push_up(u);//子节点更新完毕，更新父节点
	}
}
```

#### 查询区间值
```cpp
int query(int u, int l, int r) {
	if (l <= tree[u].l && tree[u].r <= r) return tree[u].v;//当前区间为所招区间的子区间
	int mid = tree[u].l + tree[u].r >> 1;
	int v = 0;
	if (l <= mid) v = query(u << 1, l, r);//当前区间有交集
	if (r > mid) v = max(v, query(u << 1 | 1, l, r));
	return v;
}
```

#### 区间添加
```cpp
int a[N];
LL tr[N * 4], lazy[N * 4];

void push_down(int u, int l, int r) {//下传函数
	lazy[u << 1] += lazy[u];//子节点打上懒标记
	lazy[u << 1 | 1] += lazy[u];
	tr[u << 1] += lazy[u] * (Mid - l + 1);//子节点添加值
	tr[u << 1 | 1] += lazy[u] * (r - Mid);
	lazy[u] = 0;//重设懒标记
}

void add(int u, int l, int r, int x, int y, int k) {//区间添加
	if (x <= l && r <= y) {//找到目标区间的子区间
		tr[u] += k * (r - l + 1);//将此区间的总和加上k * 区间长度
		lazy[u] += k;//添加懒标记
		return;
	}
	push_down(u, l, r);//没找到目标区间，将懒标记下传
	if (x <= Mid) add(Lson, x, y, k);
	if (y >= Mid + 1) add(Rson, x, y, k);
	push_up(u);//子节点统计完成，将此节点更新
}

LL query(int u, int l, int r, int x, int y) {
	if (x <= l && r <= y) return tr[u];
	push_down(u, l, r);//由于添加了懒标记，在统计前要将标记下传
	LL v = 0;
	if (x <= Mid) v += query(Lson, x, y);
	if (y >= Mid + 1) v += query(Rson, x, y);
	return v;
}
```

#### 区间加和乘混合
- 将计数操作统一到加的lazy数组，如果出现查询操作，先乘后加
```cpp
int a[N], p;
LL tr[N * 4], lazy[N * 4], lazymul[N * 4];

void push_up(int u) {
	tr[u] = (tr[Ls] + tr[Rs]) % p;//
}

void push_down(int u, int l, int r) {
	lazymul[Ls] = (lazymul[u] * lazymul[Ls]) % p;
	lazymul[Rs] = (lazymul[u] * lazymul[Rs]) % p;
	lazy[Ls] = (lazy[Ls] * lazymul[u] + lazy[u]) % p;
	lazy[Rs] = (lazy[Rs] * lazymul[u] + lazy[u]) % p;
	tr[Ls] = (tr[Ls] * lazymul[u] + (Mid - l + 1) * lazy[u]) % p;
	tr[Rs] = (tr[Rs] * lazymul[u] + (r - Mid) * lazy[u]) % p;
	lazy[u] = 0;
	lazymul[u] = 1;
}

void build(int u, int l, int r) {
	lazymul[u] = 1;
	if (l == r) {
		tr[u] = a[r];
		return;
	}
	build(Lson);
	build(Rson);
	push_up(u);
	tr[u] %= p;//直接取余
}

void add(int u, int l, int r, int x, int y, int k) {
	if (x <= l && r <= y) {
		tr[u] = (tr[u] + k * (r - l + 1)) % p;
		lazy[u] = (lazy[u] + k) % p;
		return;
	}
	push_down(u, l, r);
	if (x <= Mid) add(Lson, x, y, k);
	if (y >= Mid + 1) add(Rson, x, y, k);
	push_up(u);
}

void mul(int u, int l, int r, int x, int y, int k) {
	if (x <= l && r <= y) {
		tr[u] = (tr[u] * k) % p;
		lazymul[u] = (lazymul[u] * k) % p;
		lazy[u] = (lazy[u] * k) % p;
		return;
	}
	push_down(u, l, r);
	if (x <= Mid) mul(Lson, x, y, k);
	if (y >= Mid + 1) mul(Rson, x, y, k);
	push_up(u);
}

LL query(int u, int l, int r, int x, int y) {
	if (x <= l && r <= y) return tr[u];
	push_down(u, l, r);
	LL v = 0;
	if (x <= Mid) v += query(Lson, x, y);
	if (y >= Mid + 1) v += query(Rson, x, y);
	return v % p;
}

int main() {
	int n, m, op, x, y, k;
	cin >> n >> m >> p;
	for (int i = 1; i <= n; ++i) cin >> a[i];
	build(Start);
	for (int i = 1; i <= m; ++i) {
		cin >> op >> x >> y;
		if (op == 1) {
			cin >> k;
			mul(Start, x, y, k);
		}	
		else if (op == 2) {
			cin >> k;
			add(Start, x, y, k);
		}
		else cout << query(Start, x, y) << endl;
	}
	return 0;
}
```

***[返回目录](#目录)***

### 最小生成树

- prim算法
  - 适用于稠密图
```cpp
int prim() {
	int res = 0;
	memset(dis, 0x3f, sizeof dis);
	
	for(int i = 0; i < n; ++i) {
		int u = -1;
		
		for(int j = 1; j <= n; ++j)
			if(!st[j] && (u == -1 || dis[u] > dis[j]))
				u = j;
		
		if(i && dis[u] == INF) return INF;
		
		if(i) res += dis[u];
		st[u] = true;
		
		for(int j = 1; j <= n; ++j) dis[j] = min(dis[j], edge[u][j]);
	}
	
	return res;
}
```

- kruskal算法
  - 适用于稀疏图
```cpp
int kruskal(){
	sort(edge + 1, edge + 1 + m);
	
	for(int i = 1; i <= n; ++i) a[i] = i;
	
	int res = 0, cnt = 0;
	for(int i = 1; i <= m; ++i){
		int u = edge[i].u, v = edge[i].v, w = edge[i].w;
		int fu = find(u), fv = find(v);
		if(fu != fv){
			a[fu] = fv;
			res += w;
			cnt++;
		}
		if(cnt == n - 1) return res;
	}
	return INF;
}
```

***[返回目录](#目录)***

### Trie字典树
- 使用一个足够长的字符表`[N][字符种类](N为所有字符串总长度)`存储字符串，在每次查找时顺着字符表向下遍历，如果到字符串末尾，返回字符表此处是否存在字符
```cpp
int trie[N][30], cnt[N], idx;
//trie建立字符表，cnt统计此编号下字符串数目，idx在出现新字符串时会标记走过的路径为编号
char str[N];

int query(){
    int f = 0;
    for(int i = 0; str[i]; ++i){
        int t = str[i] - 'a';
        if(!trie[f][t]) return 0;//该序号下没找到该字符，返回0
        f = trie[f][t];//找下一个编号
    }
    return cnt[f];//返回该编号的字符串个数
}

void insert(){
    int f = 0;//从第一层开始找
    for(int i = 0; str[i]; ++i){
        int t = str[i] - 'a';
        if(!trie[f][t]) trie[f][t] = ++idx;//此层不匹配，去idx + 1层新建一个序号
        f = trie[f][t];//移动到下一层
    }
    cnt[f]++;//该序号次数加一
}
```

***[返回目录](#目录)***

### 二叉排序树
- 若左子树非空，则左子树上所有节点的值均小于根节点的值
- 若右子树非空，则右子树上所有节点的值均大于根节点的值
- 左右子树也是一棵二叉排序树
```cpp
typedef struct node{
	int val;
	node *l, *r;
}tree;

tree* find(tree* root,const int& x){
	if(root->val > x && root->l){
		return find(root->l, x);
	}else if(root->val < x && root->r){
		return find(root->r, x);
	}
	return root;
}

tree* find(tree *root, const int &x, tree *&parent){
	if(root->val > x && root->l){
		parent = root;
		return find(root->l, x, parent);
	}else if(root->val < x && root->r){
		parent = root;
		return find(root->r, x, parent);
	}
	return root;
}

tree* create(int arr[], int len){
	tree* root = nullptr;
	for(int i = 0; i < len; ++i){
		tree* newNode = new tree;
		newNode->val = arr[i];
		newNode->l = nullptr;
		newNode->r = nullptr;
		
		if(root == nullptr){
			root = newNode;
			continue;
		}
		
		tree* cur = find(root, arr[i]);
		
		if(cur->val < arr[i]){
			cur->r = newNode;
		}
		else if(cur->val > arr[i]){
			cur->l = newNode;
		}
		else{
			puts("create error");
		}
	}
	return root;
}

void print(tree* root){
	if(root->l) print(root->l);
	cout << root->val << " ";
	if(root->r) print(root->r);
}

void del(tree *root,const int& x){
	tree *parent = nullptr;
	tree *cur = find(root, x, parent);
	if(cur->l && cur->r){
		tree *p_last = cur;
		tree *p = cur->l;
		while(p->r){
			p_last = p;
			p = p->r;
		}
		if(p_last == cur){
			cur->val = cur->l->val;
			cur->l = cur->l->l;
		}
		else{
			cur->val = p->val;
			p_last->r = p->l;
		}
		delete p;
		return;
	}
	else if(cur->l){
		if(parent == nullptr) root = cur->l;
		else if(parent->l == cur) parent->l = cur->l;
		else parent->r = cur->l;
	}
	else if(cur->r){
		if(parent == nullptr) root = cur->r;
		else if(parent->l == cur) parent->l = cur->r;
		else parent->r = cur->r;
	}
	else{
		if(parent == nullptr) root = nullptr;
		else if(parent->l == cur) parent->l = nullptr;
		else parent->r = nullptr;
	}
	delete cur;
}
```


***[返回目录](#目录)***

### 栈

#### 栈的应用

[表达式求值](https://www.acwing.com/problem/content/3305/)
```cpp
#include <stack>
#include <unordered_map>

stack <int> num;
stack <char> op;

void eval() {
	auto b = num.top(); num.pop();
	auto a = num.top(); num.pop();
	auto c = op.top(); op.pop();
	switch (c) {
	case '+': a += b; break;
	case '-': a -= b; break;
	case '*': a *= b; break;
	case '/': a /= b; break;
	}
	num.push(a);
}

int main() {
	unordered_map<char, int> pr{ {'+', 1}, {'-', 1}, {'*', 2}, {'/', 2} };
	string s;
	cin >> s;
	for (int i = 0; i < s.length(); ++i) {
		auto c = s[i];
		if (isdigit(c)) {
			int x = 0, j = i;
			while (j < s.length() && isdigit(s[j]))
				x = x * 10 + s[j++] - '0';
			i = j - 1;
			num.push(x);
		}
		else if (c == '(') op.push(c);
		else if (c == ')') {
			while (op.top() != '(') eval();
			op.pop();
		}
		else {
			while (!op.empty() && op.top() != '(' && pr[op.top()] >= pr[c]) eval();
			op.push(c);
		}
	}
	while (!op.empty()) eval();
	cout << num.top() << endl;
	return 0;
}
```
***[返回目录](#目录)***

### 链表

#### 建立

- 单向链表
```cpp
typedef struct s{
	int data;
	s* next;
}num;

num* create(int n){
	num *head, *tail, *p;
	p = (num*)malloc(sizeof(num));
	p->next = NULL;
	head = tail = p;
	while(n--){
		p = (num*)malloc(sizeof(num));
		cin >> p->data;
		p->next = NULL;
		tail->next = p;
		tail = p;
	}
	return head;
}
```

- 双向链表
```cpp
typedef struct s{
	int data;
	s *next, *last;
}num;

num* create(int n){
	num *head, *tail, *p;
	head = tail = NULL;
	while(n--){
		p = (num*)malloc(sizeof(num));
		cin >> p->data;
		p->next = NULL;
		if(!head){
			head = tail = p;
			p->last = NULL;
		}
		else{
			tail->next = p;
			p->last = tail;
			tail = p;
		}
	}
	return head;
}
```

- 循环链表
```cpp
typedef struct s{
	int data;
	s* next;
}num;

num* create(int n){
	num *head, *tail, *p;
	head = tail = NULL;
	while(n--){
		p = (num*)malloc(sizeof(num));
		cin >> p->data;
		if(!head){
			head = tail = p;
			p->next = p;
		}
		else{
			p->next = head;
			tail->next = p;
			tail = p;
		}
	}
	return head;
}
```

#### 输出
```cpp
void print(num* head){
	num* p = head->next;
	while(p){
		cout << p->data << " ";
		p = p->next;
	}
}
```

#### 删除
```cpp
void del(num* q){
	q->next = q->next->next;
}
```

#### 查找
```cpp
void find(num* head, int k){
	num* p = head;
	while(p->data != k) p = p->next;
	cout << p->data;
}
```
***[返回目录](#目录)***

---
---
## STL
### map & vector梦幻联动
```cpp
map <vector<int>, int> m;

vector <pair<int, vector<int>>> v;

// 合起来
map [v] ++;

// 还能排序
sort(v.begin(), v.end());
//按照pair原则，先排第一位int，再排第二位vector
//排序vector按照每个元素字典序排序
```

### lower_bound
- 返回第一个大于等于查找值的位置
- `lower_bound(begin, end, key);`

### upper_bound
- 返回第一个大于查找值的位置
- `upper_bound(begin, end, key);`

### string
- `substr(起始下标， 长度(不写为到结尾))`

### next_permutation
- 进行下一次全排列（包括string）
- `next_permutation(数组首地址，数组尾地址)`

***[返回目录](#目录)***

---
---
## 欧氏筛
- 每次使用最小质因子去除合数
- 当`i % prime[j] != 0`时，`prime[j]`小于`i`的最小质因子，`prime[j] * i`的最小质因子为`prime[j]`
- 当`i % prime[j] == 0`时，`prime[j]`等于`i`的最小质因子，`prime[j] * i`的最小质因子为`prime[j]`，当`j++`时`prime[j] * i`的最小质因子为`prime[j - 1]`，不符合算法条件，所以`break`
```cpp
int st[N], prime[N], cnt;

void solve(int n) {
	for (int i = 2; i <= n; ++i) {
		if (!st[i]) prime[cnt++] = i;
		for(int j = 0; prime[j] <= n / i; ++j){
			st[prime[j] * i] = true;
			if(i % prime[j] == 0) break;
		}
	}
}
```
***[返回目录](#目录)***

---
---
## 快速幂
```cpp
LL ksm(LL base, LL power, LL mod) {
	LL res = 1;
	while (power) {
		if (power & 1) res = res * base % mod;
		base = base * base % mod;
		power >>= 1;
	}
	return res;
}
```
***[返回目录](#目录)***

---
---
## 滑动窗口
```cpp
int a[N], q[N];//a[N]存储数据，q[N]存储单调数列在数据数列中位置,同时控制数列为递增/减数列,以及数列大小
int  n, k;
cin >> n >> k;
for (int i = 1; i <= n; i ++ ) cin >> a[i];
```
- 输出每次窗口最小值
```cpp
int head = 1, tail = 0;
for (int i = 1; i <= n; i ++ ){
    if(head <= tail && i - q[head] + 1 > k) head++;//如果最后一个数字大于窗口大小，将数字弹出
    while(head <= tail && a[q[tail]] >= a[i]) tail--;//维持窗口为递增数列,注意等号
    q[++tail] = i;
    if(i >= k) cout << a[q[head]] << " ";//头部为数列最小值
}
cout << endl;
```
- 输出每次窗口最大值
```cpp
head = 1;tail = 0;
for (int i = 1; i <= n; i ++ ){
    if(head <= tail && i - q[head] + 1 > k) head++;//如果最后一个数字大于窗口大小，将数字弹出
    while(head <= tail && a[q[tail]] <= a[i]) tail--;//维持窗口为递减数列，注意等号
    q[++tail] = i;
    if(i >= k) cout << a[q[head]] << " ";//头部为数列最大值
}
cout << endl;
```
***[返回目录](#目录)***

---
---
## 字符串

### 字符串哈希
- 作用
  将字符串转化为一串长数字，便于比较两个字符串是否相等
- 计算
  - 单hash法
	*其中prime要选择较大的质数*
  `hash[i] = hash[i - 1] * prime + idx[s[i]] % M;`
  - 双hash法
  `hash1[i] = hash1[i - 1] * prime + idx[s[i]] % M1;`
  `hash2[i] = hash2[i - 1] * prime + idx[s[i]] % M2;`
	- 如果hash1[n]相同且hash2[n]相同，则极大概率为同一字符串
- 计算
  - base为进制数，取131
```cpp
ULL Hash(char *str, ULL base){
	ULL ans = 0;
	for(int i = 0; i < str[i]; ++i)
		ans = base * ans + (ULL)str[i];
	return ans;
}
```
- 获取区间hash值
```cpp
ULL get(ULL h[], int l, int r){
	return h[r] - h[l - 1] * p[r - l + 1];
}
```

#### 快速比较子串
- [字符串哈希](#https://www.acwing.com/activity/content/problem/content/891/) 
```cpp
const int N = 1e5 + 10, P = 131;

unsigned long long p[N], a[N];
int n, m;
char s[N];

unsigned long long get(int l, int r){
	return a[r] - a[l - 1] * p[r - l + 1];//截取子串哈希值
}

int main() {
	scanf("%d%d%s", &n, &m, s + 1);
	p[0] = 1;
	for(int i = 1; i <= n; ++i){
		a[i] = a[i - 1] * P + s[i];//mod为unsigned long long可自然溢出
		p[i] = p[i - 1] * P;//计算每个数乘了多少
	}
	
	while(m--){
		int l1, r1, l2, r2;
		cin >> l1 >> r1 >> l2 >> r2;
		if(get(l1, r1) == get(l2, r2)) puts("Yes");
		else puts("No");
	}
	return 0;
}
```
***[返回目录](#目录)***

### KMP
- 快速查找子串位置的优化算法

#### 时间复杂度
- O(m + n)

#### next 数组含义
- next 数组代表当前位置下，子串中相同前后缀的最长长度，如果匹配失败，这个长度将作为可回溯的位置
- 例如：
	```text
	下标 i:		0	1 	2	3	4	5	6	7
	文本串 s：	1	2	3	4	1	2	7	8
	模式串 p：	1	2	3	4	1	2	3	6
	next数组：	-1	-1	-1	-1	0	1	2	0
	```
  - 该算法的模拟过程
    - 在匹配过程中，当 `i = 6` 时, 此时模式串中 `j = 5`，发现 `s[i] != p[j + 1]` 不匹配，此时进行回溯，发现对应的 `next` 值为 1，所以模式串回溯到下标为 1 的位置进行继续匹配
  - 该算法的原理
    - 因为对于`文本串 s`中已经匹配的子串 `123412`,我们可以发现**该子串的后缀**和**模式串的前缀**存在共同的部分，即子串 `123412`中的后缀 `12`， 所以我们的模式串只要从 `12` 的位置，即`模式串p`中下标为 1 的位置继续匹配即可，不需要从头开始匹配，而在具体实现中，我们根据计算出的 `next` 数组就可以跳转到该位置
  - 如何计算这个共同部分的长度，也就是 `next` 数组？
    - 我们可以使用双指针来计算，`i` 指针用于遍历字符串，`j` 指针用于计算有多长字符串匹配
    - 此处计算也用到了上面字符串匹配的思想，当匹配成功时，`i`和 `j` 同时 `+1` ，当匹配失败时 `p[i] != p[j + 1]`，此时的子串为 `p[0]~p[j]`，对于该子串，我们也会发现有前后缀共同的部分，我们可以利用 `next[j]` 跳转到共同部分的下标, 此时的 `j < i`，并且我们已经计算好了 `i` 之前的 next 数组，我们就可以直接利用 next 数组来计算 `j` 的位置，即 `j = next[j]`，节省了从头开始匹配的时间。
  
#### 创建next数组
```cpp
//经过跳转到字符串中间，减少了从头开始匹配的时间，next数组标记当前字符串匹配失败后应该返回的上一位置
for(int i = 2, j = 0; i <= n; ++i){
	//原数组下标为1~n, i与j + 1错开一位，防止自己和自己匹配，所以i从2开始
    while(j && p[i] != p[j + 1]) j = ne[j];
	//如果下一位不匹配就返回到j的上一个匹配成功的字符串的位置
	//例如ABCDABD
	//i和j+1在位置7且不相同，则j将会返回到位置2继续尝试
	//因为下一位第3位仍然不匹配，所以再次返回到上一位第0位
    if(p[i] == p[j + 1]) j++;//如果匹配成功j将会++
    ne[i] = j;//此时j位置就是最长的匹配长度
}
```

#### 输出子串位置
```cpp
for(int i = 1, j = 0; i <= m; ++i){//这里从1开始为了i和j + 1重合起点
    while(j && s[i] != p[j + 1]) j = ne[j];//如果匹配失败，j返回上一个节点
    if(s[i] == p[j + 1]) j++;//匹配成功，j++
    if(j == n){//完全成功
        cout << i - n << " ";//输出位置
        j = ne[j];//返回上一位置，因为next数组表示当前位置与前缀的最大子串长度，当前位置可能是下一p子串的中间点
    }
}
```

#### java实现
此处实现中，数组起始位置为 0, j 起始位置为 -1
```java
class Solution {
    public int strStr(String haystack, String needle) {
        char[] s = haystack.toCharArray();
        char[] p = needle.toCharArray();
        int[] next = new int[p.length];
        int j = -1;
        next[0] = j; 
		// 初始化模式串中第 0 个位置应该回溯到 -1 的位置
        for(int i = 1; i < p.length; i++){
            while (j > -1 && p[i] != p[j + 1]) j = next[j]; 
			// 当下一个字符串不匹配时，并且可以回溯（j > -1），就回溯到上一个匹配成功的位置
            if(p[i] == p[j + 1]) j++; 
			// 当下一个字符串匹配时，j++
            next[i] = j; 
			// 标记当前位置 i 字符串匹配成功的位置为 j
        }

        j = -1;
        for(int i = 0; i < s.length; i++){ 
			// 注意此处的 i 变为 0，因为要匹配的是 s 文本串，从头开始匹配
            while (j > -1 && s[i] != p[j + 1]) j = next[j];
            if(s[i] == p[j + 1]) j++;
            if(j == p.length - 1){ 
				// 匹配成功，返回位置
                return i - p.length + 1;
            }
        }
        return -1;
    }
}
```

#### 应用
- 查找前后缀相同的所有子串
  - 例如`abadefaba`的`aba`和`a`
  - 原理：以上为例，next为`001000123`，则回溯后回到第三位，因为前缀的aba和后缀的aba相同，则第三位的a可视为最后一位的a，即子串数加一
```cpp
int main() {
	string s;
	while (cin >> s) {
		s = 'x' + s;
		memset(ne, 0, sizeof ne);
		for (int i = 2, j = 0; i < s.length(); ++i) {
			while (j && s[i] != s[j + 1]) j = ne[j];
			if (s[i] == s[j + 1]) j++;
			ne[i] = j;
		}
		
		vector <int> v;
		for (int i = s.length() - 1; i > 0; i = ne[i]) v.push_back(i);
		for (int i = v.size() - 1; i >= 0; --i) cout << v[i] << " ";
		puts("");
	}
	return 0;
}
```
- 查找字符串是否有循环节
  - 例：abcabcabc
  - 原理：若有循环节，则从循环节开始next会累加，如上例的next:`000123456`，可得`len - ne[len]`为循环节长度
```cpp
int main() {
	while (scanf("%s", s + 1) != EOF) {
		if (s[1] == '.') break;
		memset(ne, 0, sizeof ne);
		int len = strlen(s + 1);
		for (int i = 2, j = 0; i <= len; ++i) {
			while (j && s[i] != s[j + 1]) j = ne[j];
			if (s[i] == s[j + 1]) j++;
			ne[i] = j;
		}

		if (len % (len - ne[len]) == 0) printf("%d\n", len / (len - ne[len]));
		else printf("1\n");
	}
	return 0;
}
```
***[返回目录](#目录)***

### manacher求回文串

- 初始化字符串
```cpp
str += '^';
for(int i = 0; i < s.length(); ++i){
	str += '#';
	str += s[i];
}
str += '#';
str += '@';
```

- 求回文串
  - 设回文为`dacadbebdacad`, `mid`为`e`，`r`为`12`，`i`为右边的`c`
  - 先判断当前字符是否在大回文串里，是则获取对称位置的c的半径是多少，半径最大不能超过大回文串（否则不保证是回文），如果不是，取半径为1
  - 再一点点判断是否是回文串
  - 然后更新mid和r
```cpp
int len = str.length() - 1;
int r = 0, mid = 0, ans = 0;
for(int i = 1; i <= len; ++i){
	range[i] = r > i ? min(range[(mid << 1) - i], r - i) : 1;
	while(str[i + range[i]] == str[i - range[i]]) range[i]++;
	if(i + range[i] > r){
		r = i + range[i];
		mid = i;
	}
	ans = max(ans, range[i] - 1);
}
```

---
---
## 图论

### 建图
- vector存法
```cpp
for(int i = 0; i < m; ++i){
		int u, v;
		cin >> u >> v;
		t.push_back({u, v});
	}
	sort(t.begin(), t.end());
	for(auto c : t) e[c.x].push_back(c.y);
```

- 链式前向星
  - 起点大于0
  - `to[i]`为边`i`的终点,`we[i]`为边权,`next[i]`为起点为`i`的下一个边的下标编号
  - `head[i]`为边`i`的起点
```cpp
int head[N], to[M], we[M], ne[M], idx;

void add(int u, int v, int w){
	to[idx] = v;
	we[idx] = w;
	ne[idx] = head[u];
	head[u] = idx++;
}

void print(){
	for(int j = 1; j <= n; ++j)
		for(int i = head[u]; i != -1; i = ne[i])
			cout << j << " " << to[i] << " " << we[i] << endl;
			//起点，终点，边权
}
```
***[返回目录](#目录)***

### 遍历图
- dfs
```cpp
void dfs(int k){
	cout << k << " ";
	st[k] = true;
	for(auto c : v[k]){
		if(!st[c])
			dfs(c);
	}
}
int dfs(int u) {
	int count = 1;
	for (int i = 0; i < n; i++) {
		if (flag[i] == 0 && graph[u][i] == 1) {
			flag[i] = 1;
			count += dfs(i);
			flag[i] = 0;
		}
	}
	return count;
}
```

- bfs
```cpp
void bfs(int k){
	st[k] = true;
	cout << k << " ";
	queue <int> q;
	q.push(k);
	while(!q.empty()){
		int x = q.front();
		q.pop();
		for(auto c : v[x]){
			if(!st[c]){
				cout << c << " ";
				st[c] = true;
				q.push(c);
			}
		}
	}
}
```
***[返回目录](#目录)***

### 最短路
#### Dijkstra算法

[Dijkstra算法Ⅰ](https://www.acwing.com/problem/content/851/)
map数组存储边，dist数组存储从1到各个点的最短路径，st标记是否成为最短路
```cpp
int dijkstra()
{
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;

    for (int i = 0; i < n - 1; i ++ )
    {
        int t = -1;
        for (int j = 1; j <= n; j ++ )
            if (!st[j] && (t == -1 || dist[t] > dist[j]))
                t = j;

        for (int j = 1; j <= n; j ++ )
            dist[j] = min(dist[j], dist[t] + w[t][j]);

        st[t] = true;
    }

    if (dist[n] == 0x3f3f3f3f) return -1;
    return dist[n];
}
```

#### Floyd算法

操作后`d[i][j]`为最短路
```cpp
void floyd(){
    for(int k = 1; k <= n; ++k)
        for(int i = 1; i <= n; ++i)
            for(int j = 1; j <= n; ++j)
                dis[i][j] = min(dis[i][j], dis[i][k] + dis[k][j]);
}
```

- bellman-ford算法
  - 可求负权路
  - 第一层循环遍历k次(最多经过k条边)(若为无限制则遍历n次)
  - 第二层循环遍历所有边，更新最小长度
```cpp
void bellman_ford(){
    memset(dist, 0x3f, sizeof dist);

    dist[1] = 0;
    for(int i = 0; i < k; ++i){
        memcpy(last, dist, sizeof dist);
        for(int j = 1; j <= m; ++j){
            auto e = edge[j];
            dist[e.v] = min(dist[e.v], last[e.u] + e.w);
        }
    }
}
```
- 输出
```cpp
if(dist[n] > 0x3f3f3f3f / 2) cout << "impossible" << endl;
else cout << dist[n] << endl;
```

#### spfa算法
  - bellman-ford队列优化版
```cpp
int spfa(){
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;

    queue<int> q;
    q.push(1);
    st[1] = true;
    while(!q.empty()){
        int t = q.front();
        q.pop();
        st[t] = false;
        for(int i = head[t]; i != -1; i = ne[i]){
            int j = to[i];
            if(dist[j] > dist[t] + w[i]){
                dist[j] = dist[t] + w[i];
                if(!st[j]){
                    q.push(j);
                    st[j] = true;
                }
            }
        }
    }

    return dist[n];
}
```
```cpp
if(t == 0x3f3f3f3f) cout << "impossible" << endl;
else cout << t << endl;
```
- 计算负环
```cpp
int spfa(){
    queue<int> q;
    for(int i = 1; i <= n; ++i) {
        q.push(i);
        st[i] = true;
    }

    while(!q.empty()){
        int t = q.front();
        q.pop();
        st[t] = false;
        for(int i = head[t]; i != -1; i = ne[i]){
            int j = to[i];
            if(dist[j] > dist[t] + w[i]){
                dist[j] = dist[t] + w[i];
                cnt[j] = cnt[t] + 1;
                if(cnt[j] >= n) return true;
                if(!st[j]){
                    q.push(j);
                    st[j] = true;
                }
            }
        }
    }

    return false;
}
```
***[返回目录](#目录)***

### 分层图
  - 在图中可以选k条边进行操作，得到不同结果
  - 比如可以选k条边为代价为0
- 建边时多建k层的图，每层之间用权值为0的边连接，再跑一边最短路算法，最后遍历k层终点取最小值即为答案
```cpp
for (int j = 1; j <= k; j++) {
		add(u + j * n, v + j * n, w);
		add(v + j * n, u + j * n, w);
		add(u + j * n - n, v + j * n, 0);
		add(v + j * n - n, u + j * n, 0);
}
```

***[返回目录](#目录)***

### 二分图

#### 染色法判断
- 遍历所有点寻找未染色的点开始dfs
- 从一个点开始向其他点染色，如果未染色就染不一样的颜色，如果有颜色，判断颜色是否不同
```cpp
bool dfs(int u, int c) {
    col[u] = c;
    for (int i = head[u]; i != -1; i = ne[i]) {
        int v = to[i];
        if (!col[v]) {
            if (!dfs(v, 3 - c)) return false;
        } 
        else if (col[v] == c) return false;
    }
    return true;
}

int main() {
    int n, m, u, v;
    cin >> n >> m;
    memset(head, -1, sizeof head);
    for (int i = 1; i <= m; ++i) {
        cin >> u >> v;
        add(u, v);
        add(v, u);
    }

    bool flag = true;
    for (int i = 1; i <= n; ++i) {
        if (!col[i]) {
            if (!dfs(i, 1)) {
                flag = false;
                break;
            }
        }
    }

    cout << (flag ? "Yes" : "No") << endl;
    return 0;
}
```

#### 匈牙利算法
- 求二分图内最多有多少边连接左右图独立（未被其他边连接）两个点
- 遍历左图的所有点
- 每次初始化所有点未走过
- 从每个点开始dfs
- 若未走过的右图点没有匹配的左图点，标记为匹配
- 若有匹配的左图点，从该左图点开始dfs，查找该左图点是否有另外点可配对
```cpp
bool find(int u){
    for(int i = head[u]; i != -1; i = ne[i]){
        int v = to[i];
        if(!st[v]){
            st[v] = true;
            if(match[v] == 0 || find(match[v])){
                match[v] = u;
                return true;
            }
        }
    }
    return false;
}

int main(){
    int m, u, v;
    scanf("%d%d%d", &n1, &n2, &m);

    memset(head, -1, sizeof head);
    for(int i = 1; i <= m; ++i){
        scanf("%d%d", &u, &v);
        add(u, v);
    }

    int res = 0;
    for(int i = 1; i <= n1; ++i){
        memset(st, 0, sizeof st);
        if(find(i)) res++;
    }

    printf("%d\n", res);
    return 0;
}
```
---
---

## 数论

### 欧拉函数
- 整数唯一分解定理
若`n>1`则 $$n=p_1^{α_1}p_2^{α_2}...p_k^{α_k}$$ 其中p~1~≤p~2~≤…≤p~m~皆素数
若`d`是`n`的正因数，则 $$d=p_1^{β_1}p_2^{β_2}...p_k^{β_k}$$ 其中α~i~≥β~i~(i = 1, 2, 3, ..., k)

- 求欧拉函数
$$f(n)=n(1-\frac{1}{p_1})(1-\frac{1}{p_2})...(1-\frac{1}{p_k})$$(p~i~是n的质因子)
	- 证明：
    	- n为质数时，$f(n) = n-1$
    	- n非质数时，$f(n) = n-\frac{n}{p_1}-\frac{n}{p_2}...-\frac{n}{p_k}+\frac{n}{p_1p_2}+\frac{n}{p_2p_3}...+\frac{n}{p_{k-1}p_k}-\frac{n}{p_1p_2p_3}-\frac{n}{p_2p_3p_4}...$（去除所有p~i~倍数的数，加上p~i~p~i+1~倍数的数(被多删了一次)，减去p~i~p~i+1~p~i+2~倍数的数(被上一步取消删除操作了)，反复操作直到$\frac{n}{p_1p_2...p_k}$)
    	- 整理可得$f(n)=n(1-\frac{1}{p_1})(1-\frac{1}{p_2})...(1-\frac{1}{p_k})$
```cpp
int oula(int x) {
	int res = x;
	for (int i = 2; i <= x / i; ++i) {
		if (x % i == 0) {
			res = res / i * (i - 1);
			while (x % i == 0) x /= i;
		}
	}

	if (x > 1) res = res / x * (x - 1);
	return res;
}
```

***[返回目录](#目录)***

### 线性筛欧拉函数
- 推导
  - 当n为质数时，f(n)显然为`n-1`
  - 当n为非质数时，n可由`i * prime[j]`得来，`i * prime[j]`的质因子比`i`多了一项`prime[j]`
    - 当`i % prime[j] != 0`时，`i`中不包含`prime[j]`，所以$$euler[i * prime[j]] = (i * prime[j])(1-\frac{1}{p_1})(1-\frac{1}{p_2})...(1-\frac{1}{prime[j]})$$ $$ = euler[i] *  (1-\frac{1}{prime[j]}) * prime[j]$$ $$ = euler[i] * (prime[j] - 1) $$
  - 当`i % prime[j] == 0`时，`i`中包含`prime[j]`，所以$$euler[i * prime[j]] = (i * prime[j])(1-\frac{1}{p_1})(1-\frac{1}{p_2})...(1-\frac{1}{prime[j]})$$ $$ = euler[i] * prime[j]$$
```cpp
void get_euler(int n){
    euler[1] = 1;
    for(int i = 2; i <= n; ++i){
        if(!st[i]){
            prime[cnt++] = i;
            euler[i] = i - 1;
        }
        for(int j = 0; prime[j] <= n / i; ++j){
            int t = prime[j] * i;
            st[t] = true;
            if(i % prime[j] == 0){
                euler[t] = euler[i] * prime[j];
                break;
            }
            euler[t] = euler[i] * (prime[j] - 1);
        }
    }
}
```
***[返回目录](#目录)***

### 扩展欧几里得算法
- 给定两个非零的整数a、b，求$ax + by = gcd(a,b)$的整数解，其中gcd(a,b)表示a和b的最大公约数
- 可算出x, y的一对值
- 当b为0时，a为最大公约数，即取`x=1` `y=0`
- 当b不为0时，设$b * y + (a mod b) * x = d$，则原式可变为$$b * y + (a - \lfloor \frac{a}{b} \rfloor * b) * x = d$$提取公因式可得$$a * x + b * (y - \lfloor \frac{a}{b} \rfloor * x) = d$$
- 由上式可得递归函数

- 求得方程为$ax_0 + by_0 = gcd(a,b)$
- 可变形为$a(x_0 + k * \frac{b}{gcd(a, b)}) + b(y_0 + k * \frac{-a}{gcd(a, b)}) = gcd(a,b)$
- 因为$\frac{b}{gcd(a, b)}$为整数，所以x,y都为整数解
- x的通解为$x = x_0 + k * \frac{b}{gcd(a, b)}$
- y的通解为$y = y_0 + k * \frac{-a}{gcd(a, b)}$
```cpp
int exgcd(int a, int b, int &x, int &y){
	if(!b){
		x = 1, y = 0;
		return a;
	}
	int d = exgcd(b, a % b, y, x);
	y -= a / b * x;
	return d;
}
```
***[返回目录](#目录)***

### 求逆元
- 当p为质数时，x的逆元为x^p-2^，可以用快速幂求得
- 求线性逆元时，递推式为`inv[i] = (mod - mod / i) * inv[mod % i] % mod`
- 当p不是质数时，x的逆元用扩展欧几里得求得
  - $\frac{a}{x} = a*x^{-1}(mod p)$
  - $x * x^{-1} = 1(modp)$
  - $x*x^{-1}-k*p=1$(x和p互质)（gcd(x, p) == 1)

### 中国剩余定理
- 原定理：待补充
- 扩展版：[表达整数的奇怪方式](https://www.acwing.com/problem/content/206/)
- 证明
  - 设前两个式子为$$x \equiv m_1(mod a_1)$$$$x \equiv m_2(mod a_2)$$
  - 则可变形为$$x=k_1*a_1+m_1$$ $$x=k_2*a_2+m_2$$
  - 两式相减可得$$k_1*a_1 + k_2*(-a_2) = m_2-m_1$$ 此时$k_1k_2$相当于扩欧的x，y，若$\frac{m_2 - m_1}{gcd(a_1,a_2)}$有整数解(即$m_2-m_1$是$gcd(a_1,a_2)$的整数倍)则$k_1k_2$有解
  - 将$a_1a_2k'_1k'_2$代入扩欧可算出$$k'_1 * a_1 + k'_2 * a_2 = gcd(a_1, a_2)$$
  - 则$k_1=k'_1*\frac{m_2-m_1}{gcd(a_1, a_2)}$ $k_2=k'_2*\frac{m_2-m_1}{gcd(a_1, a_2)}$
  - 又由通解可得①$k''=k_1 + k*\frac{a_2}{gcd(a_1, a_2)}$
  - 要使得$k_1k_2$最小，就要让$k_1mod\frac{a_2}{gcd(a_1, a_2)}$
  - 此时算出最小的$k_1$，②$x=k_1*a_1+m_1$
  - 将①代入②可得$x=(k_1 + k*\frac{a_2}{gcd(a_1, a_2)})*a_1+m_1$，即$$x=k*\frac{a_1a_2}{gcd(a_1, a_2)}+k_1*a_1 + m_1$$
  - 设$a_1=k*\frac{a_1a_2}{gcd(a_1, a_2)}$ $m_1=k_1*a_1 + m_1$，与接下来式子继续合并
  - 若合并完成，则计算$m_1 mod a_1$得到`x`最小值
```cpp
LL exgcd(LL a, LL b, LL &x, LL &y){
	if(!b){
		x = 1, y = 0;
		return a;
	}
	LL d = exgcd(b, a % b, y, x);
	y -= a / b * x;
	return d;
}

int main(){
	int n;
	LL a1, m1, a2, m2, x = 0;
	cin >> n;
	n--;
	cin >> a1 >> m1;
	while(n--){
		cin >> a2 >> m2;
		LL k1, k2;
		LL d = exgcd(a1, a2, k1, k2);
		if((m2 - m1) % d){
			 x = -1;
			 break;
		}
		
		k1 *= (m2 - m1) / d;
		k1 = (k1 % (a2 / d) + a2 / d) % (a2 / d);
		
		x = k1 * a1 + m1;
		LL m = abs(a1 / d * a2);
		m1 = k1 * a1 + m1;
		a1 = m;
	}
	
	if(x != -1) x = (m1 % a1 + a1) % a1;
	
	cout << x << endl;
	return 0;
}
```
***[返回目录](#目录)***

### 高斯消元解方程组
- 逐列遍历消元
- 逐行找到绝对值最大的行，将此行与当前行交换
- 将此行的第一个系数非零的项的系数变为1
- 将接下来的所有行里有关此项的系数都消为零
- 从a[0][0]~a[n - 1][n]为数据，a[i][n]为最后消元结果
```cpp
int gauss() {
    int c, r;//column, row
    for (c = 0, r = 0; c < n; ++c) {

        int t = r;//从r开始找到绝对值最大的行
        for (int i = r; i < n; ++i)
            if (fabs(a[i][c]) > fabs(a[t][c]))
                t = i;

        if (fabs(a[t][c]) < eps) continue;//如果此列最大值是0，找下一列

        for (int i = c; i <= n; ++i) swap(a[t][i], a[r][i]);//找到后交换行
        for (int i = n; i >= c; --i) a[r][i] /= a[r][c];//将此行第一个数的系数变为1
        for (int i = r + 1; i < n; ++i)
            if (fabs(a[i][c]) > eps)
                for (int j = n; j >= c; --j)
                    a[i][j] -= a[r][j] * a[i][c];//将其他行的此列系数变为0，也就是消元

        r++;//下一行
    }

    if (r < n) {//存在等价的式子或者存在不成立的式子会导致r < n
        for (int i = r; i < n; ++i)
            if (fabs(a[i][n]) > eps)
                return 2;//无解
        return 1;//无穷多解
    }

    for (int i = n - 1; i >= 0; --i)//
        for (int j = i + 1; j < n; ++j)
            a[i][n] -= a[i][j] * a[j][n];//倒过来消元得到答案

    return 0;
}
```
***[返回目录](#目录)***

### 求组合数
- 基本公式
$C^b_a=C^b_{a-1}+C^{b-1}_{a-1}$
```cpp
void init(){
    for(int i = 0; i < N; ++i)
        for(int j = 0; j <= i; ++j)
            if(!j) c[i][j] = 1;
            else c[i][j] = (c[i - 1][j - 1] + c[i - 1][j]) % mod;
}
```
- 直接套公式
	$C^b_a=\frac{a!}{(a-b)!b!}$
  - 逆元求阶乘
```cpp
void init(){
    fact[0] = infact[0] = 1;
    for(int i = 1; i <= N; ++i){
        fact[i] = (LL)fact[i - 1] * i % mod;
        infact[i] = (LL)infact[i - 1] * ksm(i, mod - 2) % mod;
    }
}
```
- 卢卡斯定理
$C^b_a=C^{b\%p}_{a\%p}*C^{b/p}_{a/p}(modp)$
```cpp
int ksm(int base, int power){
    int res = 1;
    while(power){
        if(power & 1) res = (LL)res * base % p;
        base = (LL)base * base % p;
        power >>= 1;
    }
    return res;
}

int C(int a, int b){
    if(b > a) return 0;
    int res = 1;
    for(int i = 1, j = a; i <= b; ++i, j--){
        res = (LL)res * j % p;
        res = (LL)res * ksm(i, p - 2) % p;
    }
    return res;
}

int lucas(LL a, LL b){
    if(a < p && b < p) return C(a, b);
    return (LL)C(a % p, b % p) * lucas(a / p, b / p) % p;
}
```

---
---
## 博弈论

### nim问题
#### 基础
- 若一个游戏满足：
1、由两名玩家交替行动
2、在游戏进行的任意时刻，可以执行的合法行动与轮到哪位玩家无关
3、不能行动的玩家判负
则称该游戏为一个公平组合游戏。
尼姆游戏（NIM）属于公平组合游戏，但常见的棋类游戏，比如围棋就不是公平组合游戏，因为围棋交战双方分别只能落黑子和白子，胜负判定也比较负责，不满足条件2和3。

- 结论
假设n堆石子，石子数目分别是$a_1,a_2,…,a_n$，如果$a1⊕a2⊕…⊕a_n≠0$先手必胜；否则先手必败。

- 证明
操作到最后时，每堆石子数都是0，$0⊕0⊕…0=0$
在操作过程中，如果$a_1⊕a_2⊕…⊕a_n=x≠0$。那么玩家必然可以通过拿走某一堆若干个石子将异或结果变为0。可得不等于0的玩家一定会赢。
```cpp
int main(){
    int n, x, res = 0;
    cin >> n;

    while(n--){
        cin >> x;
        res ^= x;
    }

    if(res) puts("Yes");
    else puts("No");
    return 0;
}
```

#### 集合


---
---

## 拓扑序列
[拓扑序列](https://www.acwing.com/problem/content/850/)
```cpp
void solve() {
    int hh = 0, tt = -1;
    for (int i = 1; i <= n; ++i)
        if (!in[i]) {
        q[++tt] = i;
        in[i]--;
    }
    while (hh <= tt) {
        int u = q[hh++];
        for (int i = head[u]; i != -1; i = ne[i]) {
            int v = to[i];
            if (--in[v] == 0) {
                in[v]--;
                q[++tt] = v;
            }
        }
    }
    if (tt == n - 1)
        for (int i = 0; i < n; ++i)
            cout << q[i] << " ";
    else cout << -1 << endl;
}
```
***[返回目录](#目录)***

---
---

## BFS迷宫最短路
```cpp
typedef struct {
	int x, y;
	string ans;
} node;

int dx[] = {1, 0, 0, -1}, dy[] = {0, -1, 1, 0};
string d = "DLRU";
string s[] = {
	"01010101001011",
	"00001000100000",
	"01111011010010",
	"01000000001010",
	"00011111000000",
	"11001000110101",
	"00011011010100",
};

string bfs() {
	int i, j;
	node t;
	queue <node> q;
	
	q.push({0, 0, ""});
	s[0][0] = '1';
	while (!q.empty()) {
		t = q.front();
		q.pop();
		for (int k = 0; k < 4; ++k) {
			i = t.x + dx[k];
			j = t.y + dy[k];
			if (0 <= i && i < 7 && 0 <= j && j < 15 && s[i][j] == '0') {
				s[i][j] = '1';//走过打标记
				q.push({i, j, t.ans + d[k]});//路径存到队列里
				if (i == 6 && j == 14){//找到终点输出答案，第一次遇到终点肯定为最短路
					cout << t.ans + d[k] << endl;
					exit(0);
				}
			}
		}
		
	}
	
}
```
***[返回目录](#目录)***

---
---
## LCA最近公共祖先
- 用`f[i][j]`表示以`i`为节点，向上`2^j`个祖先为什么
- 统计`i`的深度，利用二进制优化，快速计算出祖先位置

```cpp
void init() {//lg2预处理，处理出的lg[x]比数学上lg(x)多1
	for (int i = 1; i <= n; ++i)
		lg[i] = lg[i - 1] + (1 << lg[i - 1] == i);
}

void dfs(int cur, int fa) {//f[i][j]数组预处理
	dep[cur] = dep[fa] + 1;//深度加一
	f[cur][0] = fa;//上一祖先为fa
	for (int i = 1; i <= lg[dep[cur]] - 1; ++i)//遍历dep能到达的所有j，处理f[i][j]
		f[cur][i] = f[f[cur][i - 1]][i - 1];
	for (auto c : tr[cur])//找下一个节点
		if (c != fa) dfs(c, cur);
}

int LCA(int x, int y) {//LCA本体算法
	if (dep[x] < dep[y]) swap(x, y);//预设x深度大于等于y
	while (dep[x] > dep[y])
		x = f[x][lg[dep[x] - dep[y]] - 1];//每次x向上查找，直到与y同一深度
	if (x == y) return y;//x，y在同一分支，返回y为公共节点
	for (int i = lg[dep[x]] - 1; i >= 0; --i)//从大到小遍历2^i
		if (f[x][i] != f[y][i]) {//如果x，y的第2^i个父节点相同则不改变，不相同则继续向上查找
			x = f[x][i];
			y = f[y][i];
		}
	//遍历之后一定是x与y的父节点相同，返回即可
	return f[x][0];
}
```

***[返回目录](#目录)***

---
---
## A*算法
### 普通A*
- 添加一个估价函数evaluate(), 返回一个到达终点的最小可能值，当估价返回值小于设定值时才继续向下搜索

```cpp
int evaluate(){
	return 当前状态与最终状态不同的个数
}
```

### IDA*
- 在A*的基础上添加了深度限制，遍历可能的设定深度(1~depth)，当当前深度和估价函数的和小于设定深度时才继续搜索
- [骑士精神](#https://www.luogu.com.cn/problem/P2324)
```cpp
if(evaluate() + dep <= depth) bfs();
```

***[返回目录](#目录)***