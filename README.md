# חומר עזר לבגרות במדעי המחשב

אפשר למצוא כאן שורות קוד, תמונות, איורים ובעצם כל דבר שתצטרכו בשביל המבחן.

הכל מחולק לנושאים אז תוכלו להוציא בדיוק את מה שאתם צריכים.

## Node

### API

| פעולה | תיאור |
|-------|-------|
|נוד בעל ערך בלבד|`Node(T value)`|
|נוד בעל ערך ועוד נוד מקושר לו|`Node(T value, Node<T> next)`|
|מחזיר את הערך של הנוד|`GetValue(): T`|
|שם את הערך המבוקש במקום הקודם|`SetValue(T value)`|
|הנוד המקושר|`GetNext(): Node<T>`|
|שם את הנוד המבוקש בתור הנוד המקושר|`SetNext(Node<T> next)`|
|בודק האם קיים נוד מקושר|`HasNext(): bool`|
|מחזיר כסטרינג את הערך של הנוד הנוכחי|`ToString(): string`|

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
