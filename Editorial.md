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

If Abid grabs $(n+1)$ socks, he will surely get at least $2$ socks of the same color.

</details>

<details>
<summary>Hint 4</summary>

Does he always need to grab $(n+1)$ socks?

</details>

<details>
<summary>Solution</summary>

Initially Abid had $a_i$ socks of color $i$ in his drawer. His brother took $b_i$ socks of color $i$. So there remains $a_i - b_i$ socks of color $i$ in Abid's drawer.

The only case when Abid will not be able to find $2$ socks of the same color is when it doesn't exist. If there exists at least $2$ socks of the same color, in the worst case, Abid can grab all the socks of the drawer and later pick those $2$. This can be detected by checking if $a_i - b_i < 2$ for all $i$.

Now, if there remains socks of $k$ different colors in Abis's drawer and he grabs $(k+1)$ socks, it is guaranteed that at least $2$ socks will have the same color (Pigeonhole Principle).  
You can easily prove it using proof by contradiction. If no $2$ socks that Abid grabs have the same color, all the $(k+1)$ socks Abid grabs have different colors. But according to the premise, socks of $(k+1)$ different colors do not exist in Abid's drawer. So it's a contradiction.

Now, since Abid had socks of $n$ different colors, the maximum possible value of $k$ is $n$. However, there can be cases where $k$ is less than $n$. If for a color, Abid's brother took all the socks of that color, then socks of that color do not exist on the drawer anymore.

So, the final solution is, after handling the impossible case separately, you need to count the number of $i$ where $a_i - b_i = 0$. Let's define it as $z$. Currently, Abid's drawer contains socks of $k = n - z$ different colors. So Abid needs to grab $n - z + 1$ socks to guarantee that at least $2$ socks will have the same color.

Time complexity = $O(n)$.

You can also handle the impossible case at the end. Count the total number of socks remaining in Abid's drawer, $\sum_{i} (a_i - b_i)$. If it is less than $n - z + 1$, then Abid can't grab that many socks. So it is impossible.

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
<summary>Hint 1</summary>

You only need the first $21$ stones.

</details>

<details>
<summary>Hint 2</summary>

A correct combination always exists.

</details>

<details>
<summary>Hint 3</summary>

The correct combination is unique.

</details>

<details>
<summary>Hint 4</summary>

Manually find the answer for $W = 1$, $W = 2$, $W = 3$, $...$, $W = 15$ and try to find a pattern.

</details>

<details>
<summary>Solution</summary>

The weight of the $i^{th}$ stone is $3^i$ ($i$ starts from $0$). For every stone, you have three options: use it at the left pan, don't use it, or use it at the right pan. You can define the value of a stone as its weight multiplied by $-1$, $0$ or $1$ if it's used at the right pan, not used, or used at the left pan respectively. The sum of the values of all stones must equal to $W$.

Now, there are $3$ possible multipliers for each stone and the weights of the stones are powers of $3$. So, you can represent any $W$ in a modified ternary number system ($3$-based number system) where the digits of the number will represent the multipiers. Since it is a valid number system, forming any $W$ is possible. So, the impossible case will never occur.

Formally, if the weight of the $i^{th}$ stone is $w_i$ and the multipler with the $i^{th}$ stone is $m_i$, then -  
$W = \sum_{i} m_i \times w_i$.  
$w_i = 3^i$.  
And for all $i$, $m_i = -1, 0, \text{or } 1$.

Since $3^{20} > 2 \times 10^9$, you will never need more than $21$ stones. \[nice reference to 'The Luncheon', right?\]

For the solution, you can follow this algorithm:
- Convert $W$ into a ternary ($3$-based) number.
- Iterate over the digits from right to left.
- If you find the $i^{th}$ digit to be $0$, you will not use the $i^{th}$ stone (keep $m_i$ as $0$).
- If the $i^{th}$ digit is $1$, you will use the stone at the left pan (keep $m_i$ as $1$).
- If the $i^{th}$ digit is $2$, you were supposed to use the stone twice on the left pan. But you have only one stone of a specific weight. Instead, you will use it at the right pan (set $m_i$ to $-1$). Now, you were supposed to add $2w_i$ but instead you subtracted $w_i$. To balance it, you need to add $3w_i$ which is equal to $w_{i+1}$. So, you will increase the next digit by $1$.
- If the $i^{th}$ digit is $3$, you will not use that stone (set $m_i$ to $0$) and increase the next digit by $1$.
- The digit will never be more than $3$. Because in a $3$-based number system, the maximum digit is $2$. Here, at max you can get an increase of $1$ from the previous digit and get it to $3$ but you'll never find a digit exceeding $3$.

In this representation, you will get the values of $m_i$ from the $i^{th}$ digit of the the number. 

Finally, you will add the weights of all the stones placed in the left pan to get $X$ and the weights of all the stones in the right pan to get $Y$.

Formally,  
$W = \sum_{i} (m_i \times w_i)$.  
$X = \sum_{i} w_i$ where $m_i = 1$.  
And, $Y = \sum_{i} w_i$ where $m_i = -1$.

Time Complexity for getting ternary representation of $W$ = $O(\log (W))$.  
Time Complexity for modifying ternary representation of $W$ = $O(\log (W))$.  
Time Complexity for calculating $X$ and $Y$ = $O(\log (W))$.  
Overall Time Complexity for a test case = $O(\log (W))$.

<details>
<summary>Example Simulation</summary>

<details>
<summary>$W = 10$</summary>

$W = 10 = 9 + 1 = (101)_3$

The $0^{th}$ digit is $1$.  
The $1^{st}$ digit is $0$.  
The $2^{nd}$ digit is $1$.

Modified ternary representation of $W$ = $101$.  
Final answer: $X = 3^0 + 3^2 = 1 + 9 = 10$, $Y = 0$.

</details>

<details>
<summary>$W = 775$</summary>

$W = 775 = 729 + 27 + 18 + 1 = 729 + 27 + 2 \times 9 + 1 = (1001201)_3$

The $0^{th}$ digit is $1$.  
The $1^{st}$ digit is $0$.  
The $2^{nd}$ digit is $2$. Change it to $-1$ and increase the next digit by $1$. Now the $3^{rd}$ digit is 2.  
The $3^{rd}$ digit is $2$. Change it to $-1$ and increase the next digit by $1$. Now the $4^{th}$ digit is 1.  
The $4^{rd}$ digit is $1$.  
The $5^{th}$ digit is $0$.  
The $6^{th}$ digit is $1$.

Modified ternary representation of $W$ = $101mm01$. Here, $m$ means the digit is $-1$.  
Final answer: $X = 3^0 + 3^4 + 3^6 = 1 + 81 + 729 = 811$, $Y = 3^2 + 3^3 = 9 + 27 = 36$.  
Verification: $811 - 36 = 775$.  

</details>
</details>

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
        ternary[i]-=3; // 2 becomes -1 and 3 becomes 0
        ternary[i+1]+=1;
    }

    // Check out how the modified ternary number looks
    // for(i=ternary.size()-1; i>=0; i--) cout << ternary[i] << ' '; cout << endl;

    int stone=1;
    for(i=0; i<ternary.size(); i++)
    {
        if(ternary[i]==1) x+=stone;
        else if(ternary[i]==-1) y+=stone;

        stone*=3;
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

You have an object of weight $W$ on the right pan. To reach equilibrium, you need to add weight $W$ on the left pan.

The weight of the $i^{th}$ stone is $3^i$ ($i$ starts from $0$).  
If you use all stones from $0$ to $(i-1)$, the total weight will be $3^0 + 3^1 + 3^2 + ... + 3^{i-1} = \frac{3^i - 1}{2}$ (sum of geometric series). Let's define it as $s_{i-1}$.  
So, if $W \ge 3^i$, using all the stones from $0$ to $(i-1)$ will not be enough.  
If you use all stones from $0$ to $i$, you can get to the total of $s_i = \frac{3^{i+1} - 1}{2}$. Clearly, $3^i < s_i < 3^{i+1}$ for any $i \in \mathbb{N}$.  
Now, you can find the value of $i$ such that $W$ falls in the range $[3^i, 3^{i+1})$, divide the problem into two cases and solve the problem recursively.  

Case $1$: $W \le s_i$  
At first, place the $i^{th}$ stone on the left pan. Now the left pan has weight $3^i$ and the left pan has weight $W$. To reach equilibrium, we need to add weight $(W - 3^i)$ on the left pan.

Case $2$: $W > s_i$  
At first, place the $(i+1)^{th}$ stone on the left pan. Now the left pan has weight $3^{i+1}$ and the left pan has weight $W$. To reach equilibrium, we need to add weight $(3^{i+1} - W)$ on the right pan.

Base Case: $W = 0$  
The balance has reached equilibrium and no more weight needs to be added.

Time Complexity for a single recursion is $O(\log (W))$ for finding the value of $i$ such that $3^i \le W < 3^{i+1}$.  
Maximum number of recursion calls for a single test case is $O(\log (W))$.  
Overall Time Complexity for a test case = $O({\log (W)}^2)$.

By using binary search to find the value of $i$, you can reduce the complexity for a single test to $O(\log (W) \log \log (W))$ but that won't be necessary here.

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
 
    int stone=1, sum=1;
 
    while(stone*3<=w) // After escaping this loop: stone<=w, stone*3>w
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

Instead of thinking about the number of gift-boxes to remove, think about the number of gift-boxes to keep.

</details>

<details>
<summary>Solution</summary>

The list of gift-boxes are represented by an array $a$ where the $a_i$ represents the number of toys in the $i^{th}$ box.

After removing some gift-boxes from the left and from the right, what you'll have remaining is a contiguous subarray of $a$, $\[a_l, a_{l+1}, ..., a_r\]$ such that $a_l + a_{l+1} + ... + a_r$ is divisible by $m$. If multiple subarrays are valid, you have to take the longest one. If no non-empty subarray is valid, the mission can't be completed.

However, if you try to check all possible subarrays, you'll need $O(n^2)$ time which will not pass within the time limit.

Here's an observation:  
If $(a_l + a_{l+1} + ... + a_r) \mod m = 0$,  
$(a_1 + a_2 + ... + a_{l-1}) \mod m = (a_1 + a_2 + ... + a_r) \mod m$ (assuming $l > 1$).  
So, $p_{l-1} \mod m = p_r \mod m$, where $p_i = a_1 + a_2 + ... + a_i$.

Now, what you need to do is calculate $p$, the prefix sum of $a$, and keep track of where each remainder appeared in $p$. For that, you can use a map. If a remainder only appeared once, ignore that. Otherwise for each remainder, pick the distance between the positions of the first appearance and the last appearance. The first appearance of the remainder $0$ has to be manually set to $0$.  
Your final answer should be $n$ minus the maximum distance or $-1$ if no remainders are found at least twice.

Number of iterations = $O(n)$.  
Access time for map = $O(\log (n))$.  
So, Overall Time Complexity= $O(n \times \log (n))$.


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
    int i, n, m;
    cin >> n >> m;

    vector<int> v(n);
    for(auto &it: v) cin >> it;

    vector<int> p(n+1);
    for(i=0; i<n; i++) p[i+1]=p[i]+v[i];

    map<int,int> firstAppearance;
    int rem, keep=-1, dist;
    for(i=0; i<n+1; i++)
    {
        rem=p[i]%m;

        if(firstAppearance.count(rem)==0) firstAppearance[rem]=i;
        else
        {
            dist=i-firstAppearance[rem];
            keep=max(keep, dist);
        }
    }

    if(keep==-1) cout << -1;
    else cout << n-keep;
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
<summary>Problem D - Kingslayer</summary>

Problem Setter: [Reaz Hassan Joarder](https://codeforces.com/profile/ssshanto)

Difficulty: Medium

Tags: Brute Force, Implementation

<details>
<summary>Solution</summary>

Solution

</details>
</details>

<details>
<summary>Problem E - Monks' Game of Cards</summary>

Problem Setter: [Rafio](https://codeforces.com/profile/Rafio)

Difficulty: Medium-Hard

Tags: Math, Graphs

<details>
<summary>Hint 1</summary>

What is the effect of shuffling multiple times?

</details>

<details>
<summary>Hint 2</summary>

The effect of shuffling multiple times is the same as shuffling once with a different shuffle order.

</details>

<details>
<summary>Solution</summary>

In the process of shuffling the deck multiple times, no new card enters the deck and no card leaves from the deck. The overall effect of shuffling multiple times is that some cards go from some positions to some different positions. So the effect of shuffling multiple times is the same as shuffling once with a different shuffle order (could even be the same order in some cases).

For example, in the first sample test case, the initial deck is $a = \[10, 20, 30, 40, 50\]$. Shuffling it twice with the shuffle order, $s_1 = \[3, 5, 4, 1, 2\]$ has the same effect as shuffling once with the shuffle order $s_2 = \[4, 2, 1, 3, 5\]$. Here, $s_i$ means the shuffle order applying which on an array has the same effect as applying $s_1$ on the array $i$ times.

One interesting observation is that the shuffle operation is associative.  
If you apply the shuffle order on itself, you'll get a new shuffle order, applying which on an array has the effect of applying the original shuffle order twice.  
Formally, if you have a shuffle order $s_1$, then you can create a new shuffle order $s_2 = s_1(s_1)$ such that $s_2(a) = s_1(s_1(a))$.

In the same way, you can get $s_3 = s_2(s_1))$ and $s_4 = s_3(s_1)$. But instead of building linearly, you can build the shuffle orders exponentially.  
$s_4 = s_2(s_2)$  
$s_8 = s_4(s_4)$  
$s_{16} = s_8(s_8)$  
$s_{2i} = s_i(s_i)$

Now, given a shuffle order $s_1$, you can calculate and store $s_2$, $s_4$, $s_8$, $...$, $s_{2^{60}}$.  
Whenever, you find a $k$, you can find $s_k$ using its binary representation.  
For example, $s_{22} = s_{16}(s_4(s_2))$.  
With this approach, you can find $s_k(a)$ in $O(n \times \log(k))$ time.

Finally, the cut operation is simply bringing the $p^{th}$ element ($0$-indexed) to the top.

Overall Time Complexity per round = $O(n \times \log(k))$.  
Time complexity for $r$ rounds = $O(n \times r \times \log(k))$.

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
 
    vector<int> a(n), temp, sk(n);
    vector<vector<int>> s(61, vector<int>(n)); // s[i] is s_{2 power i}
 
    for(auto &it: a) cin >> it;
    for(auto &it: s[0]) cin >> it;
    for(auto &it: s[0]) it--; // Converting from 1-indexed to 0-indexed
 
    for(i=1; i<61; i++) s[i]=s[i-1], shuffle(s[i], s[i-1]);
 
    while(r--)
    {
        cin >> k >> p;
        
        for(i=0; i<n; i++) sk[i]=i; // Identity permutation (shuffle order): keeps every element where it is.
        for(i=0; i<61; i++) if((k>>i)&1) shuffle(sk, s[i]); // ((k>>i)&1) checks whether the i-th bit of k is set.
        
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

The shuffle order is a permutation.  
Every permutation can be decomposed into one or more cycles.  
Applying a permutaion once is equivalent to moving every element one step ahead in its cycle.

For the solution, you can decompose the given permutation into cycles and for each element, store which cycle it belongs to and its position.  
For each round, find which cycle $p$ is in and move it $k$ steps ahead. If it goes beyong the cycle size, simply take the remainder modulo $m$.

Time Complexity for preprocessing = $O(n)$.  
Time Complexity per round = $O(1)$.  
Time complexity for $r$ rounds = $O(r)$.  
Overall Time Complexity for a test case = $O(n + r)$.

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
<summary>Problem G - MDP</summary>

Problem Setter: [Bakhtiar Hasan](https://codeforces.com/profile/ishtupeed)

Difficulty: Giveaway

<details>
<summary>Solution</summary>

Just count the flag stands in IUT.

</details>

<details>
<summary>Alternate Solution</summary>

Ask a senior.

</details>
</details>

<details>
<summary>Problem H - It's Time to Duel!</summary>

Problem Setter: [Abdullah Abrar](https://codeforces.com/profile/lelbaba)

Difficulty: Easy

Tags: Greedy

<details>
<summary>Hint</summary>

A player's optimal play does not depend on what his opponent will do.

</details>

<details>
<summary>Solution</summary>

Both players will maximize their scores. Whoever has a higher score will win the duel. If they are equal, the duel will end in a tie.

Let's define the value of a card as the number written on it, a positive card as a card with a non-negative value and a negative cards as one with a negative value.  
The optimal play of a player is the best among these three options:
- Use $1$ positive card with the highest value (if available).
- Use $2$ positive cards with the highest value (if available).
- Use $2$ negative cards with the lowest value (highest absolute value).

Now, from a deck, you need the highest value $mx_1$, 2nd highest value $mx_2$, lowest value $mn_1$ and 2nd lowest value $mn_2$. You can loop over the array in $O(n)$ time to get these, but an easier implementation is to simply sort the array in $O(n \log(n))$ time. And get the values from the first $2$ and last $2$ indexes.  
Maximum Score = $\max(mx_1, mx_1 \times mx_2, mn_1 \times mn_2)$.

You can divide it into three cases: no positive value, one positive value and more than one positive values, and handle them separately, but the result will be the same.

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

#define int long long
#define fastio ios_base::sync_with_stdio(0); cin.tie(0)
#define endl "\n"

const int N=2e5+5;
int a[N], b[N];

int maxScore(int cards[], int n)
{
    sort(cards, cards+n);

    int mx1=cards[n-1], mx2=cards[n-2], mn1=cards[0], mn2=cards[1];
    return max(mx1, max(mx1*mx2, mn1*mn2));
}

void pre()
{
    fastio;

    
}

void solve(int tc)
{
    int i, n1, n2;
    cin >> n1 >> n2;

    for(i=0; i<n1; i++) cin >> a[i];
    for(i=0; i<n2; i++) cin >> b[i];

    int yugi=maxScore(a, n1), kaiba=maxScore(b, n2);
    
    if(yugi>kaiba) cout << "Yugi";
    else if(kaiba>yugi) cout << "Kaiba";
    else cout << "Tie";
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
<summary>Problem I - Forever Matrix</summary>

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
