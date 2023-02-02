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

## Bits

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
