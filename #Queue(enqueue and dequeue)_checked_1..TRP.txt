#include <iostream>
using namespace std;

class queue
{
public:
    int f, r;
    int jqueue[5];
    int max;

    queue()
    {
        f = 0;
        r = -1;
        max = 5;
    }
    int IsEmpty();
    int IsFull();
    void enqueue();
    void dequeue();
    void display();
};

int queue::IsFull()
{
    return (r == max - 1);
}

int queue::IsEmpty()
{
    if(f > r)
    {
        return 1;
    }
    else
    {
        return 0;
    }
}

void queue::enqueue()
{
    char ch;
    int e;
    do
    {
        cout << "Enter element for inserting into queue: ";
        cin >> e;
        if (!IsFull())
        {
            r++;
            jqueue[r] = e;
        }
        else
        {
            cout << "Queue is overflow\n";
        }
        cout << "Do you want to add more element(y/n): ";
        cin >> ch;
    } 
    while (ch == 'y' || ch == 'Y');
}

void queue::dequeue()
{
    char ch;
    int del, found;
    do
    {
        if (!IsEmpty())
        {
            cout << "Enter element you want to delete: ";
            cin >> del;
            found = 0;

            for (int i = f; i <= r; i++)
            {
                if (jqueue[i] == del)
                {
                    cout << "Job no " << jqueue[i] << " is deleted\n";
                    found = 1;

                    // Shift elements left
                    for (int j = i; j < r; j++)
                        jqueue[j] = jqueue[j + 1];
                    r--;
                    break;
                }
            }

            if (!found)
                cout << "Element not found in queue\n";

            if (f > r)
            {
                f = 0;
                r = -1;
            }
        }
        else
        {
            cout << "\nqueue underflow\n";
        }

        cout << "Do you want to delete more elements(y/n): ";
        cin >> ch;
    } 
    while (ch == 'y' || ch == 'Y');
}

void queue::display()
{
    if (!IsEmpty())
    {
        cout << "element of the queue: ";
        for (int i = f; i <= r; i++)
        {
            cout << jqueue[i] << " ";
        }
        cout << endl;
    }
    else
    {
        cout << "Queue is empty\n";
    }
}

int main()
{
    queue q1;
    q1.enqueue();
    q1.display();
    q1.dequeue();
    q1.display();

    return 0;
}