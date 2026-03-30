# [P3853] 路标设置

## 1. 题目链接
- [Luogu / Codeforces 链接地址]

## 2. 题目描述
> B 市和 T 市之间有一条长长的高速公路，这条公路的某些地方设有路标，但是大家都感觉路标设得太少了，相邻两个路标之间往往隔着相当长的一段距离。为了便于研究这个问题，我们把公路上相邻路标的最大距离定义为该公路的“空旷指数”。

题目描述
现在政府决定在公路上增设一些路标，使得公路的“空旷指数”最小。他们请求你设计一个程序计算能达到的最小值是多少。请注意，公路的起点和终点保证已设有路标，公路的长度为整数，并且原有路标和新设路标都必须距起点整数个单位距离。

输入格式
第 1 行包括三个数 L,N,K，分别表示公路的长度，原有路标的数量，以及最多可增设的路标数量。

第 2 行包括递增排列的 N 个整数，分别表示原有的 N 个路标的位置。路标的位置用距起点的距离表示，且一定位于区间 [0,L] 内。

输出格式
输出 1 行，包含一个整数，表示增设路标后能达到的最小“空旷指数”值。

## 3. 解题思路
- **算法模型**：二分、max中找min
- **逻辑核心**：根据题意可知是max里找min，由此锁定二分思路，模板确定，其次，若发现当前路标与前一路标相距大于mid，则需要在前一路标后mid位置增加一个路标，并且（关键）计算新增路标与当前路标的距离。若小于，则i++，计算下一个间隙距离。
    
## 4. 复杂度分析
- 时间复杂度：O(N \log L)
- 空间复杂度：O(N)

## 5. 核心代码 (C++/Java)
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
vector<ll> v;
ll L, N, K, temp;
bool check(ll mid){
    ll lastpos = 0;
    ll count = 0;
    for(ll i = 0; i < N; i++){
        ll dist = v[i] - lastpos;
        if(dist > mid){
        lastpos = lastpos + mid;
            count++;
            i--;
        }else{
            lastpos = v[i];        
        }
    }
    if(L - lastpos >= mid) count++;
    if(count <= K) return true;
    return false;
    
}
void solve(){
    if(!(cin >> L >> N >> K)) return;
    for(ll i = 0; i < N; i++){
        cin >> temp;
        v.push_back(temp);
    }
    ll l = 1;
    ll r = L;
    while(l < r){
        ll mid = l + (r - l) / 2;
        if(check(mid)){
            r = mid;
        }else {

            l = mid + 1;
        }
    }
    cout << l;
}
int main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    solve();
    return 0;
}
