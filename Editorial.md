# Editorial for Intra-IUT Junior Programming Contest 2024

<details>
<summary>Problem A - Colorful Socks</summary>

Problem Setter: [Rafio](https://codeforces.com/profile/Rafio)

Difficulty: Easy-Medium

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

</details>
</details>

<details>
<summary>Problem B - Darhi Palla</summary>

Problem Setter: [Rafio](https://codeforces.com/profile/Rafio)

Difficulty: Hard

Tags: Math, Binary Search

<details>
<summary>Hint</summary>

Hint

</details>

<details>
<summary>Solution</summary>

Ternary Number Solution

</details>

<details>

<summary>Alternate Solution</summary>

Recursive Solution

</details>
</details>

<details>
<summary>Problem C - World Peace</summary>

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
<summary>Problem D - Sabbir Sir's Problem</summary>

Problem Setter: [Sabbir Ahmed](https://cse.iutoic-dhaka.edu/profile/sabbir)

Difficulty: Impossible

Tags: Machine Learning

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
<summary>Problem E - Moniter Goja, Gojar Monit</summary>

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
<summary>Problem F - Reaz' Pattern Problem</summary>

Problem Setter: [Reaz Hassan Joarder](https://codeforces.com/profile/ssshanto)

Difficulty: Easy

Tags: Implementation

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
<summary>Problem G - Monks' Game of Cards</summary>

Problem Setter: [Rafio](https://codeforces.com/profile/Rafio)

Difficulty: Medium

Tags: Math, Graphs

<details>
<summary>Hint</summary>

Hint

</details>

<details>
<summary>Solution</summary>

Number Theory Solution

</details>

<details>

<summary>Alternate Solution</summary>

Graph Solution

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
