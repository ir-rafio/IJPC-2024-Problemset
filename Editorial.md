# Editorial for Intra-IUT Junior Programming Contest 2024

<details>
<summary>Problem A - Colorful Socks</summary>

Problem Setter: [Rafio](https://codeforces.com/profile/Rafio)

Difficulty: Easy

Tags: Greedy

<details>
<summary>Hint 1</summary>

Handle the possible and impossible case separately.

</details>

<details>
<summary>Hint 2</summary>

If there remains at least $2$ socks of the same color, it is always possible.

</details>

<details>
<summary>Hint 3</summary>

If Abid grabs $n+1$ socks, he will surely get at least $2$ socks of the same color.

</details>

<details>
<summary>Hint 4</summary>

Does he always need to grab $n+1$ socks?

</details>

<details>
<summary>Solution</summary>

Solution

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;
 
// #define int long long
#define fastio ios_base::sync_with_stdio(0); cin.tie(0)
#define endl "\n"
 
 
 
void pre()
{
    fastio;
 
    
}
 
void solve(int tc)
{
    int i, n;
    cin >> n;
 
    vector<int> a(n), b(n);
    for(i=0; i<n; i++) cin >> a[i];
    for(i=0; i<n; i++) cin >> b[i];

    int remaining, z=0, flag=0;
    for(i=0; i<n; i++)
    {
        remaining=a[i]-b[i];
        if(remaining==0) z++;
        if(remaining>1) flag=1;
    }
 
    if(flag) cout << n+1-z;
    else cout << -1;
}
 
signed main()
{
    pre();
 
    int tc, tt=1;
    // cin >> tt;
    
    for(tc=1; tc<=tt; tc++)
    {
        solve(tc);
        // cout << endl;
    }
 
    return 0;
}
```

</details>
</details>
</details>

<details>
<summary>Problem B - Darhi Palla</summary>

Problem Setter: [Rafio](https://codeforces.com/profile/Rafio)

Difficulty: Hard

Tags: Math, Implementation

<details>
<summary>Hint</summary>

Hint

</details>

<details>
<summary>Solution</summary>

Ternary Number Solution

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;
 
#define int long long
#define fastio ios_base::sync_with_stdio(0); cin.tie(0)
#define endl "\n"
 

 
void pre()
{
    fastio;
 

}
 
void solve(int tc)
{
    int i, w, x=0, y=0;
    cin >> w;

    vector<int> ternary;
    while(w>0)
    {
        ternary.push_back(w%3);
        w/=3;
    }

    // Check out how the ternary number looks
    // for(i=ternary.size()-1; i>=0; i--) cout << ternary[i] << ' '; cout << endl;

    ternary.push_back(0);
    for(i=0; i<ternary.size()-1; i++) if(ternary[i]>1)
    {
        ternary[i]-=3;
        ternary[i+1]+=1;
    }

    // for(i=ternary.size()-1; i>=0; i--) cout << ternary[i] << ' '; cout << endl;

    int val=1;
    for(i=0; i<ternary.size(); i++)
    {
        if(ternary[i]==1) x+=val;
        else if(ternary[i]==-1) y+=val;

        val*=3;
    }
 
    cout << x << ' ' << y;
}
 
signed main()
{
    pre();
 
    int tc, tt=1;
    cin >> tt;
    
    for(tc=1; tc<=tt; tc++)
    {
        solve(tc);
        cout << endl;
    }
 
    return 0;
}
```

</details>
</details>

<details>

<summary>Alternate Solution</summary>

Recursive Solution

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;
 
#define int long long
#define fastio ios_base::sync_with_stdio(0); cin.tie(0)
#define endl "\n"
 
pair<int,int> flip(pair<int,int> p)
{
    return {p.second, p.first};
}
 
pair<int,int> add(pair<int,int> p1, pair<int,int> p2)
{
    return {p1.first+p2.first, p1.second+p2.second};
}
 
pair<int,int> balance(int w)
{
    if(w==0) return {0, 0};
 
    int i=0, sum=1, stone=1;
 
    while(stone*3<=w)
    {
        stone*=3;
        sum+=stone;
    }
 
    if(w<=sum) return add({stone, 0}, balance(w-stone));
 
    stone*=3;
    return add({stone, 0}, flip(balance(stone-w)));
}
 
void pre()
{
    fastio;
 
    
}
 
void solve(int tc)
{
    int w;
    cin >> w;
 
    auto [x, y] = balance(w);
    cout << x << ' ' << y;
}
 
signed main()
{
    pre();
 
    int tc, tt=1;
    cin >> tt;
    
    for(tc=1; tc<=tt; tc++)
    {
        solve(tc);
        cout << endl;
    }
 
    return 0;
}
```

</details>
</details>
</details>

<details>
<summary>Problem C - World Peace!</summary>

Problem Setter: [Abdullah Abrar](https://codeforces.com/profile/lelbaba)

Difficulty: Easy-Medium

Tags: Number Theory, Data Structures

<details>
<summary>Hint</summary>

Hint

</details>

<details>
<summary>Solution</summary>

Solution

</details>
</details>

<details>
<summary>Problem D - Kingslayer</summary>

Problem Setter: [Reaz Hassan Joarder](https://codeforces.com/profile/ssshanto)

Difficulty: Medium

Tags: Brute Force, Implementation

<details>
<summary>Hint</summary>

Hint

</details>

<details>
<summary>Solution</summary>

Solution

</details>
</details>

<details>
<summary>Problem E - Monks' Game of Cards</summary>

Problem Setter: [Rafio](https://codeforces.com/profile/Rafio)

Difficulty: Medium

Tags: Math, Graphs

<details>
<summary>Solution</summary>

Math Solution

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;
 
#define int long long
#define fastio ios_base::sync_with_stdio(0); cin.tie(0)
#define endl "\n"
 
void shuffle(vector<int>& a, vector<int>& s)
{
    int i, n=a.size();
 
    vector<int> temp(n);
    for(i=0; i<n; i++) temp[i]=a[s[i]];
 
    a=temp;
}
 
void pre()
{
    fastio;
 
    
}
 
void solve(int tc)
{
    int i, n, r, k, p;
    cin >> n >> r;
 
    vector<int> a(n), temp(n), sk(n);
    vector<vector<int>> s(61, vector<int>(n));
 
    for(auto &it: a) cin >> it;
    for(auto &it: s[0]) cin >> it;
    for(auto &it: s[0]) it--;
 
    for(i=1; i<61; i++) s[i]=s[i-1], shuffle(s[i], s[i-1]);
 
    while(r--)
    {
        cin >> k >> p;
        
        for(i=0; i<n; i++) sk[i]=i;
        for(i=0; i<61; i++) if((k>>i)&1) shuffle(sk, s[i]);
        
        temp=a;
        shuffle(temp, sk);
 
        cout << temp[p] << endl;
    }
}
 
signed main()
{
    pre();
 
    int tc, tt=1;
    cin >> tt;
    
    for(tc=1; tc<=tt; tc++)
    {
        solve(tc);
        // cout << endl;
    }
 
    return 0;
}
```

</details>
</details>

<details>

<summary>Alternate Solution</summary>

Graph Solution

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;
 
#define int long long
#define fastio ios_base::sync_with_stdio(0); cin.tie(0)
#define endl "\n"
 
void pre()
{
    fastio;
 
    
}
 
void solve(int tc)
{
    int i, j, n, r, c=0;
    cin >> n >> r;
 
    vector<int> a(n), s(n), temp;
    vector<bool> visited(n, 0);
    vector<vector<int>> cycles;
    vector<pair<int,int>> pos(n);
 
    for(auto &it: a) cin >> it;
    for(auto &it: s) cin >> it;
    for(auto &it: s) it--;
 
    for(i=0; i<n; i++) if(!visited[i])
    {
        temp.clear();
 
        j=i;
        do
        {
            pos[j]={c, temp.size()};
            temp.push_back(j);
            visited[j]=1;
            j=s[j];
        }
        while(j!=i);
 
        cycles.push_back(temp);
        c++;
    }
 
    int k, p, cs;
    while(r--)
    {
        cin >> k >> p;
        
        auto [id, offset]=pos[p];
        cs=cycles[id].size();
 
        k%=cs;
        p=(offset+k)%cs;
 
        cout << a[cycles[id][p]] << endl;
    }
}
 
signed main()
{
    pre();
 
    int tc, tt=1;
    cin >> tt;
    
    for(tc=1; tc<=tt; tc++)
    {
        solve(tc);
        // cout << endl;
    }
 
    return 0;
}
```

</details>
</details>
</details>

<details>
<summary>Problem F - Moniter Goja, Gojar Monit</summary>

Problem Setter: [Rafio](https://codeforces.com/profile/Rafio)

Difficulty: Very Easy

Tags: Math

<details>
<summary>Hint 1</summary>

Take a pen and a paper and solve the problem manually for a few small values of $k$.

</details>

<details>
<summary>Hint 2</summary>

If there exists multiple solutions, you may output any of them. So try to find the easiest one.

</details>

<details>
<summary>Solution</summary>

You have two unknown variables and only one equations. So you can choose a value for one of the variables and try to solve the equation for the other.

Let's start with $x=1$.

$k=1^y+y^1=1+y$

So, $y=k-1$.

Woah, you found a solution!

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

#define int long long
#define fastio ios_base::sync_with_stdio(0); cin.tie(0)
#define endl "\n"



void pre()
{
    fastio;


}

void solve(int tc)
{
    int k;
    cin >> k;
    cout << 1 << ' ' << k-1;
}

signed main()
{
    pre();

    int tc, tt=1;
    cin >> tt;

    for(tc=1; tc<=tt; tc++)
    {
        solve(tc);
        cout << endl;
    }

    return 0;
}
```

</details>
</details>
</details>

<details>
<summary>Problem G - It's Time to Duel!</summary>

Problem Setter: [Abdullah Abrar](https://codeforces.com/profile/lelbaba)

Difficulty: Easy

Tags: Greedy

<details>
<summary>Hint</summary>

Hint

</details>

<details>
<summary>Solution</summary>

Solution

</details>
</details>

<details>
<summary>Problem H - Forever Matrix</summary>

Problem Setter: [Adib Farhan](https://codeforces.com/profile/Brownbear2710)

Difficulty: Medium-Hard

Tags: Implementation, Bitmasks

<details>
<summary>Hint</summary>

Hint

</details>

<details>
<summary>Solution</summary>

Recursive Solution

</details>

<details>

<summary>Alternate Solution</summary>

Bitmasks Solution

</details>
</details>
