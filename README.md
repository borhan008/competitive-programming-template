# competitive-programming-template

## Basic

<details><summary>Fastter I/O</summary>
<p>

```C++
ios_base::sync_with_stdio(0);
cin.tie(0);
```

</p>
</details>

<details><summary>Very Simple Template</summary>
<p>

```C++
#include<bits/stdc++.h>
using namespace std;

#define ll long long

int main(){
	ios_base::sync_with_stdio(0);
	cin.tie(0);

	ll t; cin >> t;
	while(t--){

	}

	return 0;
}
```

</p>
</details>

<details><summary>Simple Template</summary>
<p>

```C++
#include<bits/stdc++.h>
using namespace std;

#define ll long long
#define ff first
#define ss second
#define pb push_back
#define pii pair<ll,ll>
#define vi vector<ll>
#define mi map<ll,ll>
#define inf 2e18
#define endl "\n"


void solve(){

}

int main(){
	ios_base::sync_with_stdio(0);
	cin.tie(0);
	ll t=1; //cin >> t;
	while(t--) solve();
	return 0;
}
```

</p>
</details>

<details><summary>Template Version 2</summary>
<p>

```C++
#include<bits/stdc++.h>
using namespace std;

#define ll long long
#define F first
#define S second
#define pb push_back
#define mp make_pair
#define pii pair<ll,ll>
#define vi vector<ll>
#define mi map<ll,ll>
#define inf 2e18
#define fo(i,n) for(ll i=0; i<n; i++)
#define all(x) x.begin(), x.end()
#define input(n,x) fo(i, n) cin >> x[i];
#define output(x) for(auto i : x) printf("%lld ", i)
#define sortall(x) sort(all(x))
#define YES printf("YES\n")
#define NO printf("NO\n")
#define endl "\n"


void solve(){
	ll n;
	cin >> n;
	ll a[n];
	input(n,a);
	output(a);
}

int main(){
	ios_base::sync_with_stdio(0);
	cin.tie(0);

	ll t=1; //cin >> t;
	while(t--) solve();

	return 0;
}
```

</p>
</details>

## Number Thoery

<details><summary>GCD & LCM (Basic)</summary>
<p>

```C++
#define ll long long
ll gcd(ll a,ll b){
	if(b==0)return a;
	else return gcd(b,a%b);
}

ll lcm(ll a,ll b){
	return a*b/gcd(a,b);
}
```

</p>
</details>

<details><summary>Check Integer overflow or not</summary>
<p>

```C++
Built-in Function: bool __builtin_add_overflow (type1 a, type2 b, type3 *res)
Built-in Function: bool __builtin_sub_overflow (type1 a, type2 b, type3 *res)
Built-in Function: bool __builtin_mul_overflow (type1 a, type2 b, type3 *res)

Built-in Function: bool __builtin_add_overflow_p (type1 a, type2 b, type3 c)
Built-in Function: bool __builtin_sub_overflow_p (type1 a, type2 b, type3 c)
Built-in Function: bool __builtin_mul_overflow_p (type1 a, type2 b, type3 c)

if(__builtin_mul_overflow(a, b, &temp)) Overflow;
```

</p>
</details>

<details><summary>BitInt</summary>
<p>

```C++
struct bigint {
    typedef vector<int> lnum;
    const int base = 1000 * 1000 * 1000;
    lnum a;
    bigint() {}
    bigint(string s) {
        for (int i = (int)s.length(); i > 0; i -= 9)
            if (i < 9)
                a.push_back (atoi (s.substr (0, i).c_str()));
            else
                a.push_back (atoi (s.substr (i - 9, 9).c_str()));

    }
    void print() {
        printf ("%d", a.empty() ? 0 : a.back());
        for (int i = (int)a.size() - 2; i >= 0; --i)
            printf ("%09d", a[i]);
    }
    void operator += (const bigint &B) {
        const lnum &b = B.a;
        int carry = 0;
        for (size_t i = 0; i < max(a.size(),b.size()) || carry; ++i) {
            if (i == a.size())
                a.push_back (0);
            a[i] += carry + (i < b.size() ? b[i] : 0);
            carry = a[i] >= base;
            if (carry)  a[i] -= base;
        }
    }
};
```

</p>
</details>

<details><summary>GCD Fastest Implementation</summary>
<p>

[maxplus's comment in codeforces](https://codeforces.com/blog/entry/13410?#comment-205881)

```C++
template<typename T>
inline T gcd(T a, T b)
{
    T c;
    while (b)
    {
        c = b;
        b = a % b;
        a = c;
    }
    return a;
}
```

</p>
</details>

<details><summary>nCk Simple Version</summary>
<p>

```C++
ll nck(ll n, ll k){
	ll ans = 1;

	for(ll i=n-k+1; i<=n; i++) ans*=i;
	for(ll i=2; i<=k; i++) ans/=i;

	return ans;
}
```

</p>
</details>

<details><summary>Binary Exponentiation W/O Modulo</summary>
<p>

[cp-algorithms](https://cp-algorithms.com/algebra/binary-exp.html#implementation)

```C++
long long binpow(long long a, long long b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1)
            res = res * a;
        a = a * a;
        b >>= 1;
    }
    return res;
}
```

</p>
</details>

<details><summary>Counting divisors upto 1e18</summary>
<p>

```C++
#define int long long int
#define all(a) a.begin(), a.end()

set<int> primes;
vector<bool> is_Prime(1e5+5, true);

void seive(){
	is_Prime[1] = false;
	for(int i=4; i<=1e5; i+=2) is_Prime[i]=false;

	for(int i=3; i<=1e5; i+=2){
		if(is_Prime[i]==false) continue;
		for(int j=i*2; j<=1e5; j+=i){
			is_Prime[j]=false;
		}
	}

	primes.insert(2);
	for(int i=3; i<=1e5; i+=2){
		if(is_Prime[i]) primes.insert(i);
	}
}

int countFactos(int n){
	int ans = 1;
	for(auto l:primes){
		if(l*l*l > n) break;
		int cnt=1;
		while(n%l == 0){
			n/=l;
			cnt++;
		}
		ans *= cnt;
	}

	if(binary_search(all(primes), n)){
		ans *= 2;
	} else if(floor(sqrtl(n*1.000000))==ceil(sqrtl(n*1.000)) && binary_search(all(primes), sqrtl(n))){
		ans *= 3;
	} else if(n != 1) {
		ans *= 4;
	}

	return ans;
}

```

</p>
</details>

<details><summary>Prime Factorization</summary>
<p>

[cp-algorithms](https://cp-algorithms.com/algebra/factorization.html#wheel-factorization)

```C++
vector<ll> primeFactorization(ll n){
   vector<ll> v;

   while(n%2 == 0){
      v.push_back(2);
      n/=2;
   }
   for(ll i=3; i*i<=n; i+=2){
      while(n%i == 0){
         v.push_back(i);
         n/=i;
      }
   }

   if(n > 1)  v.push_back(n);

   return v;
}
```

</p>
</details>

<details>
	<summary>Prime Numbers untill 1e5</summary>

<p>

```C++
set<ll> primes;
vector<bool> is_Prime(1e5+5, true);

void seive(){
	is_Prime[1] = false;
	for(ll i=4; i<=1e5; i+=2) is_Prime[i]=false;

	for(ll i=3; i<=1e5; i+=2){
		if(is_Prime[i]==false) continue;
		for(ll j=i*2; j<=1e5; j+=i){
			is_Prime[j]=false;
		}
	}

	primes.insert(2);
	for(ll i=3; i<=1e5; i+=2){
		if(is_Prime[i]) primes.insert(i);
	}
}

```

</p>
</details>

<details><summary>Matrix Exponentiation</summary>
<p>

```C++
vector<vector<int>> mul(vector<vector<int>> a, vector<vector<int>> b, int n){
	vector<vector<int>> ans(n, vector<int>(n, 0));
	for(int i=0; i<n; i++){
		for(int j=0; j<n; j++){
			for(int k=0; k<n; k++){
				ans[i][j] += (a[i][k]*b[k][j])%mod;
				ans[i][j] %= mod;
			}
		}
	}
	return ans;
}

vector<vector<int>> matExp(vector<vector<int>> a, int n){
		vector<vector<int>> ans = a;

		while(n >= 1){
			if(n%2 == 0){
				a = mul(a, a, 2);
				n/=2;
			} else {
				ans = mul(a, ans, 2);
				n--;
			}
		}

		return ans;
}
```

</p>
</details>

## Bits & Others

<details><summary>Checking i-th Bit Set or not</summary>
<p>

```C++
ll checkBit  = ((n >> i) & 1);
```

</p>
</details>
<details><summary>Setting i-th Bit</summary>
<p>

```C++
n = n + (1LL << i);
```

</p>
</details>
<details><summary>Knight Movement</summary>
<p>

```C++
int dx[8] = {-1, 1, -2, 2, -2, 2, -1, 1};
int dy[8] = {-2, -2, -1, -1, 1, 1, 2, 2};
```

</p>
</details>

## Algorithms

<details><summary>Number of subarray with sum K</summary>
<p>

```C++
ll subarrayOfK(ll n, ll k, ll arr[]){
	ll ans=0;
	ll sum=0;
	map<ll, ll> mp;
	mp[0]=1;
	for(ll i=0; i<n; i++){
		sum += arr[i];
		ans += mp[sum-k];
		mp[sum]++;
	}
	return ans;
}
```

</p>
</details>
<details><summary>Subarray Divisible By K</summary>
<p>

```C++
ll subarraysDivByK(ll nums[], ll n, ll k) {
	ll sum=0, ans=0;

	map<ll, ll> x;
	x[0]=1;

	for(ll i=0; i<n; i++){
		sum += nums[i];
		ans += x[(sum%k + k)%k];
		x[(sum%k +k)%k]++;
	}

	return ans;
}
```

</p>
</details>

## Graph

<details><summary>BFS</summary>
<p>

```C++
	ll n,e;	cin >> n >> e;
	vector<ll> adj[n+1];
	for(ll i=1; i<=n; i++){
		ll x,y;	cin >> x >> y;
		adj[x].push_back(y);
		adj[y].push_back(x);
	}

	queue<ll> q;
	vector<ll> p(n+1);
	vector<ll> d(n+1);
	vector<bool> used(n+1, false);

	ll src=1;
	q.push(src);
	p[src]=-1;
	used[src]=true;

	while(!q.empty()){
		ll v=q.front();
		q.pop();
		for(auto u:adj[v]){
			if(!used[u]){
				used[u]=true;
				q.push(u);
				d[u]=d[v]+1;
				p[u]=v;
			}
		}
	}

	ll dist = 4;
	list<ll> path;
	for(ll i=dist; i!=-1; i=p[i]){
		path.push_front(i);
	}
	for(auto v:path)	cout << v << " ";
```

</p>
</details>

<details><summary>DSU by Size</summary>
<p>

```C++
const int N = (int)1e5 + 10;
struct DSU {
int parent[N];
int sizes[N];

void make(int v){
	parent[v] = v;
	sizes[v] = 1;
}

int find(int v){
	if(v == parent[v]) return v;
	return parent[v] = find(parent[v]);
}

void Union(int a, int b){
	a = find(a);
	b = find(b);
	if(a != b){
		if(sizes[a] < sizes[b])
			swap(a,b);

		parent[b]=a;
		sizes[a] += sizes[b];
	}
}
}
```

</p>
</details>

## Range Query Template

<details><summary>Sparse Table</summary>
<p>

```C++
#include<bits/stdc++.h>
using namespace std;

#define int long long int
const int mod = 998244353;

const int mx = 1e6+2;
const int maxN = log2(mx);
int dp[maxN + 2][mx + 2];

void table(int a[], int n){
	int k = log2(n);
	for(int i=0; i < n; i++){
		dp[0][i] = a[i];
	}

	for(int j=1; j<=k; j++){
		for(int i=0; i + (1 << (j-1)) <= n; i++){
			dp[j][i] = min(dp[j-1][i], dp[j-1][i + (1 << (j-1))]);
		}
	}
}

int query(int a, int b){
	a--; b--;
	int len = b - a + 1;
	int k = log2(len);
	return min(dp[k][a], dp[k][b - (1<<k) + 1]);
}

int32_t main() {
	ios_base::sync_with_stdio(0);
	cin.tie(0);
	int t=1; //cin >> t;

	while(t--){
		int n, q;	cin >> n >> q;
		int a[n];
		for(int i=0; i<n; i++) cin >> a[i];
		table(a, n);
		while(q--){
			int a, b; cin >> a>> b;
			cout << query(a, b) << "\n";
		}
	}
}
```

</p>
</details>

<details><summary>Segment Tree Template</summary>
<p>

```C++
#include<bits/stdc++.h>
using namespace std;

#define int long long int
const int N = 1e6+5;
int t[4*N];

void build(int a[], int v, int tl, int tr){
	if(tl ==tr){
		t[v] = a[tl];
	} else{
		int tm = (tl + tr) >> 1;
		build(a, 2*v, tl, tm);
		build(a, 2*v+(int)1, tm+1, tr);
		t[v] = t[2*v]^t[2*v+1];
	}
}
int query(int v, int tl, int tr, int l, int r){
	if(l > r) return 0;
	if(tl == l && tr==r) return t[v];
	int tm = (tl+tr) >> 1;
	return (query(2*v, tl, tm, l, min(tm, r))^query(2*v + 1, tm+1, tr, max(l, tm+1), r));

}

void update(int v, int tl, int tr, int pos, int val){
	if(tl == tr){
		t[v] = t[v]^val;
	} else{
		int tm = (tl+tr) >> 1;
		if(pos <= tm)	update(2*v, tl, tm, pos, val);
		else					update(2*v+1, tm+1, tr, pos, val);
		t[v] = t[2*v]^t[2*v + 1];
	}
}


int32_t main(){
	int n, q;	cin >> n >> q;
	int a[n+1];
	for(int i=1; i<=n; i++) cin >> a[i];
	build(a, (int)1, (int)1, n);
	while(q--){
		int ti, x, y;	cin >> ti >> x >> y;
		if(ti == 1){
			update(1,1, n, x, y);
		} else{
			cout << query(1, 1, n, x, y) << "\n";
		}

	}


	return 0;
}
```

</p>
</details>

<details> <summary>Counting unique/distinct element within a range using Segment Tree</summary>
<p>

```c++
#include <bits/stdc++.h>
using namespace std;

int n;
const int mx = 2e5 + 10;
int v[mx];
int nxt_ri[mx];
struct segtree {
vector < int > tr[4 * mx];

void build(int nod, int a, int b) {
if (a == b) {
tr[nod].push_back(nxt_ri[a]);
return;
}
int mid = (a + b) >> 1;
build(nod << 1, a, mid);
build(nod << 1 | 1, mid + 1, b);
merge(tr[nod << 1].begin(), tr[nod << 1].end(), tr[nod << 1 | 1].begin(), tr[nod << 1 | 1].end(), back_inserter(tr[nod]));
}

int query(int nod, int a, int b, int l, int r) {
if (a > r || b < l) {
return 0;
}
if (a >= l && b <= r) {
return tr[nod].end() - upper_bound(tr[nod].begin(), tr[nod].end(), r);
}
int mid = (a + b) >> 1;

    return (query(nod << 1, a, mid, l, r) + query(nod << 1 | 1, mid + 1, b, l, r));

}

}
seg;

int main() {
ios::sync_with_stdio(0);
cin.tie(0);
int ts = 1;
// cin >> ts;
while (ts--) {
int m, q, res = 1;
cin >> n >> q;
for (int i = 1; i <= n; i++)
cin >> v[i];
map < int, int > ump;
for (int i = n; i >= 0; i--) {
if (ump[v[i]] == 0) {
nxt_ri[i] = n + 1;
ump[v[i]] = i;
} else {
nxt_ri[i] = ump[v[i]];
ump[v[i]] = i;
}
}
seg.build(1, 1, n);
while (q--) {
int l, r, typ, idx;
cin >> l >> r;

      cout << seg.query(1, 1, n, l, r);
      cout << "\n";
    }

}
}
```

</p>
</details>
