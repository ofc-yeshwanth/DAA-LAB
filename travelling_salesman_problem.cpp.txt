#include <iostream>
#include <climits>
#include <algorithm>
using namespace std;

int n;
int dist[10][10];
int dp[1 << 10][10];

int tsp(int mask, int pos) 
{
    // If all cities are visited, return cost to go back to start
    if (mask == (1 << n) - 1)
        return dist[pos][0];

    // Return already computed value
    if (dp[mask][pos] != -1)
        return dp[mask][pos];

    int ans = INT_MAX;

    // Try all unvisited cities
    for (int city = 0; city < n; city++) 
    {
        if ((mask & (1 << city)) == 0) 
        {
            int newAns = dist[pos][city] +
                         tsp(mask | (1 << city), city);

            ans = min(ans, newAns);
        }
    }

    return dp[mask][pos] = ans;
}

int main() 
{
    cout << "Enter number of cities (max 10): ";
    cin >> n;

    if (n > 10) 
    {
        cout << "Maximum 10 cities allowed.\n";
        return 0;
    }

    cout << "Enter distance matrix:\n";
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            cin >> dist[i][j];

    // Initialize dp table
    for (int i = 0; i < (1 << n); i++)
        for (int j = 0; j < n; j++)
            dp[i][j] = -1;

    cout << "Minimum travel cost: " << tsp(1, 0) << endl;

    return 0;
}
