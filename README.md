# חומר עזר לבגרות במדעי המחשב

אפשר למצוא כאן שורות קוד, תמונות, איורים ובעצם כל דבר שתצטרכו בשביל המבחן.

הכל מחולק לנושאים אז תוכלו להוציא בדיוק את מה שאתם צריכים.

- [חומר עזר לבגרות במדעי המחשב](#חומר-עזר-לבגרות-במדעי-המחשב)
  - [מערכים](#מערכים)
    - [מציאת מינימום ומקסימום](#מציאת-מינימום-ומקסימום)
    - [מיונים](#מיונים)
    - [חיפושים](#חיפושים)
  - [Stack](#stack)
    - [API](#api)
    - [ציור](#ציור)
    - [פעולות](#פעולות)
  - [Queue](#queue)
    - [API](#api-1)
    - [ציור](#ציור-1)
    - [פעולות](#פעולות-1)
  - [Node](#node)
    - [API](#api-2)
    - [ציור](#ציור-2)
    - [פעולות](#פעולות-2)

## מערכים

### מציאת מינימום ומקסימום

```cs
/// <summary>
/// Finds the minimum value of given array
/// Time complexity: O(n), n = given array length
/// </summary>
/// <param name="arr"> The given array </param>
/// <returns> The minimum value of given array </returns>
public static int FindMin(int[] arr)
{
    int min = Int32.MaxValue;
    for (int i = 0, i < arr.Length; i++)
        if (arr[i] < min)
            min = arr[i];
    return min;
}
```

```cs
/// <summary>
/// Finds the maximum value of given array
/// Time complexity: O(n), n = given array length
/// </summary>
/// <param name="arr"> The given array </param>
/// <returns> The maximum value of given array </returns>
public static int FindMax(int[] arr)
{
    int max = Int32.MinValue;
    for (int i = 0, i < arr.Length; i++)
        if (arr[i] > max)
            max = arr[i];
    return max;
}
```

```cs
/// <summary>
/// Finds the index of the minimum value of given array
/// Time complexity: O(n), n = given array length
/// </summary>
/// <param name="arr"> The given array </param>
/// <returns> The index of the minimum value of given array </returns>
public static int FindIndexMin(int[] arr)
{
    int min = Int32.MaxValue, loc = 0;
    for (int i = 0, i < arr.Length; i++)
        if (arr[i] < min)
        {
            loc = i;
            min = arr[i];
        }
    return loc;
}
```

```cs
/// <summary>
/// Finds the index of the maximum value of given array
/// Time complexity: O(n), n = given array length
/// </summary>
/// <param name="arr"> The given array </param>
/// <returns> The index of the maximum value of given array </returns>
public static int FindIndexMax(int[] arr)
{
    int max = Int32.MinValue, loc = 0;
    for (int i = 0, i < arr.Length; i++)
        if (arr[i] > max)
        {
            loc = i;
            max = arr[i];
        }
    return loc;
}
```

### מיונים

```cs
/// <summary>
/// Merges two sorted arrays
/// Time complexity: O(n + m), n = first array length, m = second array length
/// </summary>
/// <param name="a"> First array </param>
/// <param name="b"> Second array </param>
/// <returns> Merged array from both arrays </returns>
public static int[] MergeSorted(int[] a, int[] b)
{
    int[] c = new int[a.Length + b.Length];
    for (int indexA = 0, indexB = 0, indexC = 0; indexC < c.Length; indexC++)
    {
        if (indexA < a.Length && indexB < b.Length && a[indexA] > b[indexB])
        {
            c[indexC] = b[indexB];
            indexB++;
        }
        else if (indexA < a.Length)
        {
            c[indexC] = a[indexA];
            indexA++;
        }
        else
            c[indexC] = b[indexB];
    }
    return c;
}
```

```cs
/// <summary>
/// Sorts an array
/// Time complexity: O(n ^ 2), n = array length
/// </summary>
/// <param name="arr"> The given array </param>
/// <returns> The given array, sorted </returns>
public static int[] BubbleSort(int[] arr)
{
    for (int write = 0; write < arr.Length; write++)
        for (int sort = 0; sort < arr.Length - 1; sort++)
            if (arr[sort] > arr[sort + 1])
            {
                temp = arr[sort + 1];
                arr[sort + 1] = arr[sort];
                arr[sort] = temp;
            }
    return arr;
}
```

```cs
/// <summary>
/// Sorts an array using Counting Sort
///
/// n - 's'
/// O(n)
/// </summary>
/// <param name="arr">The array to sort</param>
/// <param name="k">The numbers' range</param>
/// <returns>The sorted array</returns>
public static int[] SortWithCounting(int[] arr, int k)
{
    // output - The resulting array
    int[] output = new int[arr.Length];
    // count - A temporary counting array
    int[] count = new int[k];

    for (int i = 0; i < count.Length; i++)
        count[i] = 0;

    for (int i = 0; i < arr.Length; i++)
        count[arr[i]]++;

    for (int i = 1; i < count.Length; i++)
        count[i] += count[i - 1];

    for (int i = 0; i < arr.Length; i++)
    {
        output[count[arr[i]] - 1] = arr[i];
        count[arr[i]]--;
    }

    return output;
}
```

### חיפושים

```cs
/// <summary>
/// Searches given value
/// Time complexity: O(log2 n), n = array length
/// </summary>
/// <param name="arr"> The given array </param>
/// <returns> Index of given key if exist in the array, else -1 </returns>
public static int BinarySearch(int[] arr, int searchKey)
{
    int mid, max = arr.Length, min = 0;
    while (min <= max)
    {
        mid = (max + min) / 2;
        if (arr[mid] == searchKey)
            return mid;
        if (arr[mid] > searchKey)
            max = mid - 1;
        else if (arr[middle] < searchKey)
            min = mid + 1;
        return -1;
    }
}
```

## Stack

### API

| פעולה                                        | תיאור                |
| -------------------------------------------- | -------------------- |
| יוצר מחסנית ריקה                             | `Stack()`            |
| בודק אם המחסנית ריקה או לא                   | `IsEmpty(): bool`    |
| מוסיף ערך למחסנית                            | `Push(T value)`      |
| מוציא ערך מהמחסנית                           | `Pop(): T`           |
| מחזיר את הערך הראשון של המחסנית              | `Top(): T`           |
| מחזיר כסטרינג את כל הערכים של המחסנית ברשימה | `ToString(): string` |

### ציור

![Stack drawing](img/stack.png)

### פעולות

```cs
public static int Size<T>(Stack<T> s )
{
    if (s.IsEmpty())
        return 0;
    T val = s.Pop();
    int counter = Size(s) + 1;
    s.Push(val);
    return counter;
}
```

```cs
public static int FindMin(Stack<int> s)
{
    if (s.IsEmpty())
        return int.MaxValue;
    int val = s.Pop();
    int min = Math.Min(val, FindMin(s));
    s.Push(val);
    return min;
}
```

```cs
/// <summary>
/// Copies a stack to an additional stack
/// Time complexity: O(n), n = the number of items in the source stack
/// </summary>
/// <param name="source"> The source stack </param>
/// <returns> A new stack with the same content as the given stack </returns>
public static Stack<T> CopyStack<T>(Stack<T> source, Stack<T> destination = null)
{
    if (destination == null)
        destination = new Stack<T>();
    Stack<T> temp = new Stack<T>();

    while (!source.IsEmpty())
    {
        temp.Push(source.Top());
        destination.Push(source.Pop());
    }

    SpillStack(temp, source);
    return destination;
}
```

```cs
/// <summary>
/// Takes a stack and putting its content in a different stack
/// Time complexity: O(n), n = the number of items in the source stack
/// </summary>
/// <param name="from"> The source stack </param>
/// <param name="to"> The target stack </param>
/// <returns> A new stack with the same content as the given stack </returns>
public static Stack<T> SpillStack<T>(Stack<T> source, Stack<T> destination = null)
{
    if (destination == null)
        destination = new Stack<T>();
    while (!source.IsEmpty())
        destination.Push(source.Pop());
    return destination;
}
```

```cs
/// <summary>
/// Checks if two stacks have the same items
/// Time complexity: O(n * m), n = number of items in s1, m = number of items in s2
/// </summary>
/// <param name="s1"> The first source stack </param>
/// <param name="s2"> The second source stack </param>
/// <returns> True if both stacks have the same items, otherwise false </returns>
public static bool DeepEqual<T>(Stack<T> s1, Stack<T> s2)
{
    Stack<T> temp = CopyStack(s1);
    while (!temp.IsEmpty())
        if (SearchStack(s2, temp.Pop()))
            return true;
    return false;
}
```

```cs
/// <summary>
/// Searches an item in a given stack
/// Time complexity: O(n), n = the number of items in the source stack
/// </summary>
/// <param name="source"> The source stack </param>
/// <param name="item"> The item to search </param>
/// <returns> True if the item exists in the stack, otherwise false </returns>
public static bool SearchStack<T>(Stack<T> source, T item)
{
    if (source.IsEmpty())
        return false;
    T top = source.Top();
    if (item.Equals(top))
        return true;
    source.Pop();
    bool found = SearchStack(source, item);
    source.Push(top);
    return found;
}
```

```cs
public static int[] ToArray(Stack<int> stc)
{
    Stack<int> stc2 = new Stack<int>();

    int counter = 0;
    while (!stc.IsEmpty())
    {
        stc2.Push(stc.Pop());
        counter++;
    }
    int[] arr = new int[counter];
    while (!stc2.IsEmpty())
    {
        counter--;
        arr[counter] = stc2.Top();
        stc.Push(stc2.Pop());
    }
    return arr;
}
```

## Queue

### API

| פעולה                                     | תיאור                |
| ----------------------------------------- | -------------------- |
| יוצר תור ריק                              | `Queue()`            |
| בודק אם התור ריק או לא                    | `IsEmpty(): bool`    |
| מוסיף ערך לתור                            | `Insert(T value)`    |
| מוציא ערך מהתור                           | `Remove(): T`        |
| מחזיר את הערך הראשון של התור              | `Head(): T`          |
| מחזיר כסטרינג את כל הערכים של התור ברשימה | `ToString(): string` |

### ציור

![Queue drawing](img/queue.png)

### פעולות

```cs
/// <summary>
/// Spills a queue to a different queue
/// </summary>
/// <param name="from"> The source queue </param>
/// <param name="to"> The destenation queue </param>
public static void SpillQueue<T>(Queue<T> from, Queue<T> to)
{
    while (!from.IsEmpty())
        to.Insert(from.Remove());
}
```

```cs
/// <summary>
/// Copies a queue
/// Time complexity: O(n), n = number of items in the queue
/// </summary>
/// <param name="source"> The source queue </param>
/// <returns> A copy of the queue </returns>
public static Queue<T> CopyQueue<T>(Queue<T> source)
{
    Queue<T> result = CopyQueue<T>(source, new Queue<T>());
    FlipQueue(source);
    return result;
}
public static Queue<T> CopyQueue<T>(Queue<T> source, Queue<T> result = null)
{
    if (source.IsEmpty())
        return result;
    T temp = source.Remove();
    result.Insert(temp);
    result = CopyQueue(source, result);
    source.Insert(temp);
    return result;
}
```

```cs
/// <summary>
/// Returns the number of items in the queue
/// Time complexity: O(n), n = number of items in the queue
/// </summary>
/// <param name="source"> The source queue </param>
/// <returns> The number of items in the queue </returns>
public static int QueueSize<T>(Queue<T> source)
{
    int size = QueueSize(source, 0);
    FlipQueue(source);
    return size;
}

public static int QueueSize<T>(Queue<T> source, int counter = 0)
{
    if (source.IsEmpty())
        return 0;
    T temp = source.Remove();
    counter = 1 + QueueSize(source, 0);
    source.Insert(temp);
    return counter;
}
```

```cs
/// <summary>
/// Flips a queue
/// Time complexity: O(n), n = number of items in the queue
/// </summary>
/// <param name="source"> The source queue </param>
public static void FlipQueue<T>(Queue<T> source)
{
    if (source.IsEmpty())
        return;
    T temp = source.Remove();
    FlipQueue(source);
    source.Insert(temp);
}
```

## Node

### API

| פעולה                                | תיאור                         |
| ------------------------------------ | ----------------------------- |
| נוד בעל ערך בלבד                     | `Node(T value)`               |
| נוד בעל ערך ועוד נוד מקושר לו        | `Node(T value, Node<T> next)` |
| מחזיר את הערך של הנוד                | `GetValue(): T`               |
| שם את הערך המבוקש במקום הקודם        | `SetValue(T value)`           |
| הנוד המקושר                          | `GetNext(): Node<T>`          |
| שם את הנוד המבוקש בתור הנוד המקושר   | `SetNext(Node<T> next)`       |
| בודק האם קיים נוד מקושר              | `HasNext(): bool`             |
| מחזיר כסטרינג את הערך של הנוד הנוכחי | `ToString(): string`          |

### ציור

![Node drawing](img/node.png)

### פעולות

```cs
public static string PrintNode<T>(Node<T> n, string str)
{
    if (n == null)
        return str;

    str += n.GetValue().ToString();

    if (n.HasNext())
        str += "--";

    return PrintNode(n.GetNext(), str);
}
```

```cs
public static int Size<T>(Node<T> node)
{
    // num - Holds the size of the node
    int num = 1;

    while (node.HasNext())
    {
        num++;
        node = node.GetNext();
    }

    return num;
}
```

```cs
public static bool IsInNode<T>(Node<T> p, T val)
{
    if (p == null)
        return false;
    if (val.Equals(p.GetValue()))
        return true;
    return IsInList(p.GetNext(), val);
}
```

```cs
public static int MinValue(Node<int> p)
{
    if (!p.HasNext())
        return int.MaxValue;
    return Math.Min(p.GetValue(), MinValue(p.GetNext()));
}
```

```cs
public static int MaxValue(Node<int> p)
{
    if (!p.HasNext())
        return int.MinValue;
    return Math.Max(p.GetValue(), MaxValue(p.GetNext()));
}
```
