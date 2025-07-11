ṇ#include <iostream>
#include <vector>
using namespace std;

void printArray(vector<int> &arr, int n)
{
    cout << endl;
    for (int i = 0; i < arr.size(); i++)
    {
        cout << arr[i] << " ";
    }
    cout << endl;
}

void Sorting(vector<int> &arr, int n)
{
    for (int i = 0; i < n - 1; i++)
    {
        int minIndex = i;
        for (int j = i + 1; j < n; j++)
        {
            if (arr[j] < arr[minIndex])
            {
                minIndex = j;
            }
        }
        int temp = arr[minIndex];
        arr[minIndex] = arr[i];
        arr[i] = temp;
    }
}

void merge(vector<int> &arr, int low, int mid, int high)
{
    vector<int> temp;
    int left = low;
    int right = mid + 1;

    while (left <= mid && right <= high)
    {
        if (arr[left] <= arr[right])
        {
            temp.push_back(arr[left]);
            left++;
        }
        else
        {
            temp.push_back(arr[right]);
            right++;
        }
    }

    while (left <= mid)
    {
        temp.push_back(arr[left]);
        left++;
    }

    while (right <= high)
    {
        temp.push_back(arr[right]);
        right++;
    }

    for (int i = low; i <= high; i++)
    {
        arr[i] = temp[i - low];
    }
}

void mergesort(vector<int> &arr, int low, int high)
{
    if (low >= high)
        return;

    int mid = (low + high) / 2;
    mergesort(arr, low, mid);
    mergesort(arr, mid + 1, high);
    merge(arr, low, mid, high);
}

int BinarySearch(vector<int> &arr, int low, int high, int search)
{
    if (low > high)
        return -1;

    int mid = (high + low) / 2;

    if (search == arr[mid])
        return mid;
    else if (search < arr[mid])
        return BinarySearch(arr, low, mid - 1, search);
    else
        return BinarySearch(arr, mid + 1, high, search);
}

int main()
{
    int choice;
    vector<int> arr;
    bool arrayInitialized = false;

    do
    {
        cout << "-----------------------------------------------------" << endl;
        cout << "Press 0 to Exit" << endl;
        cout << "Press 1 for Selection Sort" << endl;
        cout << "Press 2 for Merge Sort" << endl;
        cout << "Press 3 for Binary Search" << endl;
        cout << "-----------------------------------------------------" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
        case 0:
            break;

        case 1:
        {
            int n;
            cout << "Enter the Size of the Array: ";
            cin >> n;

            arr.clear();
            for (int i = 0; i < n; i++)
            {
                int element;
                cout << "arr[" << i << "]: ";
                cin >> element;
                arr.push_back(element);
            }

            cout << "Original Array: ";
            printArray(arr, n);

            Sorting(arr, n);
            arrayInitialized = true;

            cout << "Sorted Array: ";
            printArray(arr, n);
        }
        break;

        case 2:
        {
            int n;
            cout << "Enter the size of the Array: ";
            cin >> n;

            arr.clear();
            for (int i = 0; i < n; i++)
            {
                int element;
                cout << "arr[" << i << "]: ";
                cin >> element;
                arr.push_back(element);
            }

            cout << "Original Array: ";
            printArray(arr, n);

            mergesort(arr, 0, n - 1);
            arrayInitialized = true;

            cout << "Sorted Array: ";
            printArray(arr, n);
        }
        break;

        case 3:
        {
            if (!arrayInitialized)
            {
                cout << "Please sort the array first using option 1 or 2." << endl;
                break;
            }

            int search;
            cout << "Enter element to search: ";
            cin >> search;

            int index = BinarySearch(arr, 0, arr.size() - 1, search);

            if (index != -1)
                cout << "Element found at index " << index << endl;
            else
                cout << "Element not found!" << endl;
        }
        break;

        default:
            cout << "Invalid choice!" << endl;
        }

    } while (choice != 0);

    return 0;
}
