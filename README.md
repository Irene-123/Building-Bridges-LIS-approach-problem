# Building-Bridges-LIS-approach-problem
Building bridges problem using LIS approach 

![image](https://user-images.githubusercontent.com/58950467/87802494-f1635c80-c86e-11ea-83e8-166205a19dc7.png)

Source-Narsimha Karumachi's C++ data structures & algorithms 

Consider a very long, straight river which moves
from north to south. Assume there are n cities on both sides of the river: n cities on the left
of the river and n cities on the right side of the river.
Also, assume that these cities are
numbered from 1 to n but the order is not known. Now we want to connect as many leftright
pairs of cities as possible with bridges such that no two bridges cross. 
When
connecting cities, we can only connect city i on the left side to city i on the right side.


Solution:
Input: Two pairs of sets with each numbered from 1 to n.


Goal: Construct as many bridges as possible without any crosses between left side cities to right
side cities of the river.

To understand better let us consider the diagram below. In the diagram it can be seen that there
are n cities on the left side of river and n cities on the right side of river. Also, note that we are
connecting the cities which have the same number [a requirement in the problem]
 Our goal is to connect the maximum cities on the left side of river to cities on the right side of the river, without
any cross edges. Just to make it simple, let us sort the cities on one side of the river.

If we observe carefully, since the cities on the left side are already sorted, the problem can be
simplified to finding the maximum increasing sequence. That means we have to use the LIS
solution for finding the maximum increasing sequence on the right side cities of the river.


Time Complexity: O(n<sup>2</sup>), (same as LIS).

```
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;
bool cmp(pair<int,int> a, pair<int,int> b){
    return a.first<b.first;
}

int bridges(vector<pair<int,int> > connect){
    int i, j, n=connect.size();
    sort(connect.begin(),connect.end(),cmp);
    vector<int> lis(n,1);
    int m=0;
    for(i=0;i<n;i++){
        for(j=i-1;j>=0;j--){
            if(connect[i].second>connect[i].first)lis[i]=max(lis[i],lis[j]+1);
        }
        m=max(m,lis[i]);
    }
    return m;
}

int main(){
    int n, i;
    cin >> n;
    vector<pair<int,int> > a(n);
    for(i=0;i<n;i++)cin >> a[i].first >> a[i].second;
    cout << bridges(a) <<endl;
    return 0;
}
```
