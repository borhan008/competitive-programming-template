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
    cin.tie(0);  cout.tie(0);

 	ll t=1; //cin >> t;
 	while(t--) solve();

	return 0;
}
```

</p>
</details>
