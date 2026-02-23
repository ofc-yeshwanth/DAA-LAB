#include <iostream>
using namespace std;

int main() 
{
    int n, key;

    cout << "Enter number of elements: ";
    cin >> n;

    int a[n];   // Variable Length Array (works in most compilers like GCC)

    cout << "Enter elements:\n";
    for (int i = 0; i < n; i++)
        cin >> a[i];

    cout << "Enter element to search: ";
    cin >> key;

    for (int i = 0; i < n; i++) 
    {
        if (a[i] == key) 
        {
            cout << "Element found at position " << i + 1 << endl;
            return 0;
        }
    }

    cout << "Element not found" << endl;

    return 0;
}
