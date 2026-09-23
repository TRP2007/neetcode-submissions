#include <iostream>
using namespace std;

int m[4][4];
char city[4];
int n;
int visited[10];
int countt = 0;

void initialization(){
    cout << "enter total cities:";
    cin >> n;
    for (int i = 0; i <= n - 1; i++)
    {
        cout << "enter city name :";
        cin >> city[i];
    }
    for (int i = 0; i <= n - 1; i++)
    {
        for (int j = 0; j <= n - 1; j++)
        {
            if (i == j)
            {
                m[i][j] =  0 ;
            }
            else
            {
                m[i][j] = -1;
            }
        }
    }
}

int getindex(char ct){
    for (int i = 0; i <= n - 1; i++)
    {
        if (city[i] == ct)
        {
            return i;
        }
    }
    return -1; // ✅ FIX ADDED
}

void store()
{
    int p;
    cout << "enter total path:";
    cin >> p;
    for (int k = 0; k <= p - 1; k++)
    {
        char s, d;
        int c;
        cout << "enter source city:";
        cin >> s;
        int i = getindex(s);
        cout << "enter destination city:";
        cin >> d;
        int j = getindex(d);
        cout << "enter cost :";
        cin >> c;
        m[i][j] = m[j][i] = c;
    }
}

void displayMatrix()
{
    cout << "\nCost Matrix:\n";
    for (int i = 0; i < n; i++)
    {
        cout << city[i] << "   ";
        for (int j = 0; j < n; j++)
        {
            if (m[i][j] == -1)
                cout << "-1\t";
            else
                cout << m[i][j] << "\t";
        }
        cout << "\n";
    }
}

// DFS FUNCTION
void DFS(int i)
{
    visited[i] = 1;
    countt++;
    for (int j = 0; j < n; j++)
    {
        if (m[i][j] != 0 && m[i][j] != -1 && visited[j] == 0)
        {
            DFS(j);
        }
    }
}

int main() {
    initialization();
    displayMatrix();
    store();
    displayMatrix();

    // CONNECTIVITY CHECK
    for (int i = 0; i < n; i++)
        visited[i] = 0;

    countt = 0;
    DFS(0);

    if (countt == n)
        cout << "\nGraph is connected";
    else
        cout << "\nGraph is not connected";

    return 0;
}
