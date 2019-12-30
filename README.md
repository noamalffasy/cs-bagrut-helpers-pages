# חומר עזר לבגרות במדעי המחשב

אפשר למצוא כאן שורות קוד, תמונות, איורים ובעצם כל דבר שתצטרכו בשביל המבחן.

הכל מחולק לנושאים אז תוכלו להוציא בדיוק את מה שאתם צריכים.

- [חומר עזר לבגרות במדעי המחשב](#חומר-עזר-לבגרות-במדעי-המחשב)
  - [Stack](#stack)
    - [API](#api)
    - [ציור](#ציור)
    - [פעולות](#פעולות)
  - [Queue](#queue)
    - [API](#api-1)
    - [פעולות](#פעולות-1)
  - [Node](#node)
    - [API](#api-2)
    - [ציור](#ציור-1)
    - [פעולות](#פעולות-2)

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

![Stack](img/Stack.png)

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
