# FindMissingAndRepeating
Given an unsorted array of size N of positive integers. One number 'A' from set {1, 2, …N} is missing and one number 'B' occurs twice in array. Find these two numbers.  Note: If you find multiple answers then print the Smallest number found. Also, expected solution is O(n) time and constant extra space.



#include <iostream>
#include <iosfwd>
#include <iomanip>
#include <cstdio>
#include <cstring>
#include <cstdlib>
#include <ctime>
#include <cmath>
#include <cassert>
#include <cctype>
#include <climits>
#include <vector>
#include <bitset>
#include <set>
#include <queue>
#include <stack>
#include <map>
#include <deque>
#include <string>
#include <list>
#include <iterator>
#include <sstream>
#include <complex>
#include <fstream>
#include <functional>
#include <numeric>
#include <utility>
#include <algorithm>
#include <assert.h>
#include <unordered_map>
#include <random>
#include <ctime>
#include <chrono>
#define F first
#define S second
#define PB push_back
#define MP make_pair
#define ll long long

using namespace std;
const int N = 1e6 + 1e5 + 500;
const long long mod = 1e9 + 7;
const long long INF = 1LL << 57;

long long arr[N];

ll firstSetBits(ll n)
{
    ll pos = 1;

    for(ll i = 0;i < 32; i++)
    {

        if(!(n & (1 << i)))
            pos++;
        else
            break;
    }
    return pos;

}

bool isKthBitSet(ll n, ll k)
{

    if(n & (1 << (k-1)))
        return true;
    else
        return false;

}

int main()
{
    ll tt = 0;cin >> tt;

    while(tt--)
    {
        ll N = 0;cin >> N;
        ll arr[N] = {0};
        for(ll i = 0;i < N;i++) cin >> arr[i];

        ll firstXor = 0,secondXor = 0;
        for(ll i = 0;i < N; i++)
            firstXor ^= arr[i];

        for(ll i = 1; i <= N; i++)
            secondXor ^= i;

        ll finalXor = (firstXor^secondXor);

        ll kthsetbit = firstSetBits(finalXor);

        ll firstBucket = 0,secondBucket = 0;
        for(ll i = 0;i < N; i++)
        {
            if(isKthBitSet(arr[i],kthsetbit))
                firstBucket ^= arr[i];
            else
                secondBucket ^= arr[i];
        }
        for(ll i =1 ;i <= N; i++)
        {
            if(isKthBitSet(i,kthsetbit))
                firstBucket ^= i;
            else
                secondBucket ^= i;
        }
        ll count = 0;
        for(ll i = 0;i < N; i++) {
            if (arr[i] == firstBucket)
                count++;
            else continue;
        }

        if(count == 2) cout << firstBucket << " " << secondBucket << endl;
        else cout << secondBucket << " " << firstBucket << endl;

    }


    return 0;
}
