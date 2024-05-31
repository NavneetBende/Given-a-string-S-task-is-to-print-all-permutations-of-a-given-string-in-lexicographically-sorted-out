Given a string S, task is to print all permutations of a given string in lexicographically sorted order in C++
Permutations of a given string in lexicographically sorted order in C++
Here, in this page we will discuss the program to print all permutations of a given string in lexicographically sorted order in C++ Programming language. We are given with string and need to print them.

Permutation in C++
Algorithm :
Sort and print the given string in ascending order.
The string sorted in non-decreasing order is always the first permutation.
Begin creating the next higher permutation.
Continue until the next higher permutation is no longer conceivable.
When we arrive at a permutation in which all characters are arranged in non-increasing order, we have arrived at the final permutation.
Permutations of a string in lexicographically sorted order in C++
Code in C++
Run
#include <bits/stdc++.h>
using namespace std;
 
int compare (const void *a, const void * b)
{ return ( *(char *)a - *(char *)b ); }
 
void swap (char* a, char* b)
{
    char t = *a;
    *a = *b;
    *b = t;
}

int findCeil (char str[], char first, int l, int h)
{
    int ceilIndex = l;
 
    for (int i = l+1; i <= h; i++)
    if (str[i] > first && str[i] < str[ceilIndex])
            ceilIndex = i;
 
    return ceilIndex;
}

void sortedPermutations ( char str[] )
{
    int size = strlen(str);
 
    qsort( str, size, sizeof( str[0] ), compare );
 
    bool isFinished = false;
    while ( ! isFinished )
    {
        cout << str << endl;
        int i;
        
        for ( i = size - 2; i >= 0; --i )
        if (str[i] < str[i+1])
            break;
 
        if ( i == -1 )
            isFinished = true;
        else
        {
            int ceilIndex = findCeil( str, str[i], i + 1, size - 1 );
            swap( &str[i], &str[ceilIndex] );
            qsort( str + i + 1, size - i - 1, sizeof(str[0]), compare );
        }
    }
}

int main()
{
    char str[] = "ABC";
    sortedPermutations( str );
    return 0;
}
 
Output :
ABC 
ACB 
BAC 
BCA 
CAB 
CBA 
