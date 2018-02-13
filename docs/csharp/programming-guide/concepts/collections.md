---
title: Collections (C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: get-started-article
ms.assetid: 317d7dc3-8587-4873-8b3e-556f86497939
caps.latest.revision: "6"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 271939b869433742f8b5720ba05955169ea5c410
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="collections-c"></a>Collections (C#)
Pour de nombreuses applications, vous voulez créer et gérer des groupes d’objets connexes. Il existe deux manières de grouper des objets : en créant des tableaux d’objets ou des collections d’objets.  
  
 Les tableaux sont particulièrement utiles pour la création et l’utilisation d’un nombre fixe d’objets fortement typés. Pour plus d’informations sur les tableaux, consultez [Tableaux](../../../csharp/programming-guide/arrays/index.md).  
  
 Les collections offrent plus de souplesse quand il s’agit d’utiliser des groupes d’objets. Contrairement aux tableaux, le groupe d’objets que vous utilisez peut être développé et réduit de manière dynamique selon les modifications de l’application. Pour certaines collections, vous pouvez affecter une clé à tout objet que vous placez dans la collection de sorte à pouvoir récupérer rapidement l’objet à l’aide de la clé.  
  
 Une collection est une classe, vous devez déclarer une instance de la classe avant de pouvoir ajouter des éléments à la collection.  
  
 Si votre collection contient des éléments d’un seul type de données, vous pouvez utiliser une des classes dans l’espace de noms <xref:System.Collections.Generic?displayProperty=nameWithType>. Une collection générique applique la cohérence des types pour éviter qu’un autre type puisse y être ajouté. Quand vous récupérez un élément d’une collection générique, il n’est pas utile de déterminer son type de données ou de le convertir.  
  
> [!NOTE]
>  Pour les exemples de cette rubrique, ajoutez des instructions [using](../../../csharp/language-reference/keywords/using-directive.md) pour les espaces de noms `System.Collections.Generic` et `System.Linq`.  
  
 **Dans cette rubrique**  
  
-   [Utilisation d’une collection simple](#BKMK_SimpleCollection)  
  
-   [Types de collections](#BKMK_KindsOfCollections)  
  
    -   [Classes System.Collections.Generic](#BKMK_Generic)  
  
    -   [Classes System.Collections.Concurrent](#BKMK_Concurrent)  
  
    -   [Classes System.Collections](#BKMK_Collections)  
  
-   [Implémentation d’une collection de paires clé-valeur](#BKMK_KeyValuePairs)  
  
-   [Utilisation de LINQ pour accéder à une collection](#BKMK_LINQ)  
  
-   [Tri d’une collection](#BKMK_Sorting)  
  
-   [Définition d’une collection personnalisée](#BKMK_CustomCollection)  
  
-   [Itérateurs](#BKMK_Iterators)  
  
<a name="BKMK_SimpleCollection"></a>
## <a name="using-a-simple-collection"></a>Utilisation d’une collection simple  
 Les exemples de cette section utilisent la classe <xref:System.Collections.Generic.List%601> générique, qui vous permet d’utiliser une liste d’objets fortement typée.  
  
 L’exemple suivant crée une liste de chaînes, puis itère au sein des chaînes à l’aide d’une instruction [foreach](../../../csharp/language-reference/keywords/foreach-in.md).  
  
```csharp  
// Create a list of strings.  
var salmons = new List<string>();  
salmons.Add("chinook");  
salmons.Add("coho");  
salmons.Add("pink");  
salmons.Add("sockeye");  
  
// Iterate through the list.  
foreach (var salmon in salmons)  
{  
    Console.Write(salmon + " ");  
}  
// Output: chinook coho pink sockeye  
```  
  
 Si le contenu d’une collection est connu d’avance, vous pouvez utiliser un *initialiseur de collection* pour initialiser la collection. Pour plus d’informations, consultez [Initialiseurs d’objets et de collections](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).  
  
 L’exemple suivant est identique à l’exemple précédent, à la différence qu’un initialiseur de collection est utilisé pour ajouter des éléments à la collection.  
  
```csharp  
// Create a list of strings by using a  
// collection initializer.  
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };  
  
// Iterate through the list.  
foreach (var salmon in salmons)  
{  
    Console.Write(salmon + " ");  
}  
// Output: chinook coho pink sockeye  
```  
  
 Vous pouvez utiliser une instruction [for](../../../csharp/language-reference/keywords/for.md) au lieu d’une instruction `foreach` pour itérer au sein d’une collection. Pour cela, accédez aux éléments de la collection à la position d’index. L’index des éléments commence à 0 et se termine au nombre d’éléments moins 1.  
  
 L’exemple suivant itère au sein des éléments d’une collection à l’aide de `for` au lieu de `foreach`.  
  
```csharp  
// Create a list of strings by using a  
// collection initializer.  
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };  
  
for (var index = 0; index < salmons.Count; index++)  
{  
    Console.Write(salmons[index] + " ");  
}  
// Output: chinook coho pink sockeye  
```  
  
 L’exemple suivant supprime un élément de la collection en spécifiant l’objet à supprimer.  
  
```csharp  
// Create a list of strings by using a  
// collection initializer.  
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };  
  
// Remove an element from the list by specifying  
// the object.  
salmons.Remove("coho");  
  
// Iterate through the list.  
foreach (var salmon in salmons)  
{  
    Console.Write(salmon + " ");  
}  
// Output: chinook pink sockeye  
```  
  
 L’exemple suivant supprime les éléments d’une liste générique. À la place d’une instruction `foreach`, une instruction [for](../../../csharp/language-reference/keywords/for.md), qui itère dans l’ordre décroissant, est utilisée. En effet, avec la méthode <xref:System.Collections.Generic.List%601.RemoveAt%2A>, les éléments après l’élément supprimé ont une valeur d’index moins élevée.  
  
```csharp  
var numbers = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };  
  
// Remove odd numbers.  
for (var index = numbers.Count - 1; index >= 0; index--)  
{  
    if (numbers[index] % 2 == 1)  
    {  
        // Remove the element by specifying  
        // the zero-based index in the list.  
        numbers.RemoveAt(index);  
    }  
}  
  
// Iterate through the list.  
// A lambda expression is placed in the ForEach method  
// of the List(T) object.  
numbers.ForEach(  
    number => Console.Write(number + " "));  
// Output: 0 2 4 6 8  
```  
  
 Pour le type d’éléments de <xref:System.Collections.Generic.List%601>, vous pouvez également définir votre propre classe. Dans l’exemple suivant, la classe `Galaxy` qui est utilisée par <xref:System.Collections.Generic.List%601> est définie dans le code.  
  
```csharp  
private static void IterateThroughList()  
{  
    var theGalaxies = new List<Galaxy>  
        {  
            new Galaxy() { Name="Tadpole", MegaLightYears=400},  
            new Galaxy() { Name="Pinwheel", MegaLightYears=25},  
            new Galaxy() { Name="Milky Way", MegaLightYears=0},  
            new Galaxy() { Name="Andromeda", MegaLightYears=3}  
        };  
  
    foreach (Galaxy theGalaxy in theGalaxies)  
    {  
        Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears);  
    }  
  
    // Output:  
    //  Tadpole  400  
    //  Pinwheel  25  
    //  Milky Way  0  
    //  Andromeda  3  
}  
  
public class Galaxy  
{  
    public string Name { get; set; }  
    public int MegaLightYears { get; set; }  
}  
```  

<a name="BKMK_KindsOfCollections"></a>
## <a name="kinds-of-collections"></a>Types de collections 
 Plusieurs collections courantes sont fournies par le .NET Framework. Chaque type de collection est conçu dans un but spécifique.  
  
 Certaines des classes de collection courantes sont décrites dans cette section :  
  
-   Classes <xref:System.Collections.Generic>  
  
-   Classes <xref:System.Collections.Concurrent>  
  
-   Classes <xref:System.Collections>  
  
<a name="BKMK_Generic"></a>
### <a name="systemcollectionsgeneric-classes"></a>Classes System.Collections.Generic  
 Vous pouvez créer une collection générique en utilisant l’une des classes dans l’espace de noms <xref:System.Collections.Generic>. Une collection générique est utile quand chaque élément de la collection a le même type de données. Une collection générique applique un typage fort en autorisant uniquement l’ajout des types de données souhaités.  
  
 Le tableau suivant liste quelques classes de l’espace de noms <xref:System.Collections.Generic?displayProperty=nameWithType> fréquemment utilisées :  

|Classe|Description| 
|---|---|  
|<xref:System.Collections.Generic.Dictionary%602>|Représente une collection de paires clé/valeur organisées en fonction de la clé.|  
|<xref:System.Collections.Generic.List%601>|Représente une liste d’objets accessibles par index. Fournit des méthodes de recherche, de tri et de modification de listes.|  
|<xref:System.Collections.Generic.Queue%601>|Représente une collection d’objets premier entré, premier sorti (FIFO).|  
|<xref:System.Collections.Generic.SortedList%602>|Représente une collection de paires clé/valeur triées par clé en fonction de l'implémentation <xref:System.Collections.Generic.IComparer%601> associée.|  
|<xref:System.Collections.Generic.Stack%601>|Représente une collection d’objets dernier entré, premier sorti (LIFO).|  
  
 Pour plus d’informations, consultez [Types de collections couramment utilisés](../../../standard/collections/commonly-used-collection-types.md), [Sélection d’une classe de collection](../../../standard/collections/selecting-a-collection-class.md) et <xref:System.Collections.Generic>.  
  
<a name="BKMK_Concurrent"></a>
### <a name="systemcollectionsconcurrent-classes"></a>Classes System.Collections.Concurrent  
 Dans .NET Framework 4 ou ultérieur, les collections de l’espace de noms <xref:System.Collections.Concurrent> fournissent des opérations thread-safe efficaces pour accéder aux éléments de collection à partir de plusieurs threads.  
  
 Les classes de l’espace de noms <xref:System.Collections.Concurrent> doivent être utilisées à la place des types correspondants dans les espaces de noms <xref:System.Collections.Generic?displayProperty=nameWithType> et <xref:System.Collections?displayProperty=nameWithType> chaque fois que plusieurs threads accèdent simultanément à la collection. Pour plus d’informations, consultez [Collections thread-safe](../../../standard/collections/thread-safe/index.md) et <xref:System.Collections.Concurrent>.  
  
 Certaines classes incluses dans l’espace de noms <xref:System.Collections.Concurrent> sont <xref:System.Collections.Concurrent.BlockingCollection%601>, <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, <xref:System.Collections.Concurrent.ConcurrentQueue%601> et <xref:System.Collections.Concurrent.ConcurrentStack%601>.  
  
<a name="BKMK_Collections"></a>
### <a name="systemcollections-classes"></a>Classes System.Collections  
 Les classes de l’espace de noms <xref:System.Collections?displayProperty=nameWithType> ne stockent pas les éléments comme des objets spécifiquement typés, mais comme des objets de type `Object`.  
  
 Si possible, vous devez utiliser les collections génériques dans l’espace de noms <xref:System.Collections.Generic?displayProperty=nameWithType> ou <xref:System.Collections.Concurrent> à la place des types hérités de l’espace de noms `System.Collections`.  
  
 Le tableau suivant répertorie certaines des classes fréquemment utilisées de l’espace de noms `System.Collections` :  
  
|Classe|Description|  
|---|---|  
|<xref:System.Collections.ArrayList>|Représente un tableau d’objets dont la taille est augmentée de manière dynamique selon les besoins.|  
|<xref:System.Collections.Hashtable>|Représente une collection de paires clé/valeur qui sont organisées en fonction du code de hachage de la clé.|  
|<xref:System.Collections.Queue>|Représente une collection d’objets premier entré, premier sorti (FIFO).|  
|<xref:System.Collections.Stack>|Représente une collection d’objets dernier entré, premier sorti (LIFO).|  
  
 L’espace de noms <xref:System.Collections.Specialized> fournit des classes de collection spécialisées et fortement typées, telles que les collections à chaîne unique et les dictionnaires de liste liée et hybrides.  

<a name="BKMK_KeyValuePairs"></a>
## <a name="implementing-a-collection-of-keyvalue-pairs"></a>Implémentation d’une collection de paires clé/valeur  
 La collection générique <xref:System.Collections.Generic.Dictionary%602> vous permet d’accéder aux éléments d’une collection à l’aide de la clé de chaque élément. Chaque ajout au dictionnaire se compose d’une valeur et de sa clé associée. La récupération d’une valeur à l’aide de sa clé est très rapide, car la classe `Dictionary` est implémentée en tant que table de hachage.  
  
 L’exemple suivant crée une collection `Dictionary` et itère au sein du dictionnaire à l’aide d’une instruction `foreach`.  
  
```csharp  
private static void IterateThruDictionary()  
{  
    Dictionary<string, Element> elements = BuildDictionary();  
  
    foreach (KeyValuePair<string, Element> kvp in elements)  
    {  
        Element theElement = kvp.Value;  
  
        Console.WriteLine("key: " + kvp.Key);  
        Console.WriteLine("values: " + theElement.Symbol + " " +  
            theElement.Name + " " + theElement.AtomicNumber);  
    }  
}  
  
private static Dictionary<string, Element> BuildDictionary()  
{  
    var elements = new Dictionary<string, Element>();  
  
    AddToDictionary(elements, "K", "Potassium", 19);  
    AddToDictionary(elements, "Ca", "Calcium", 20);  
    AddToDictionary(elements, "Sc", "Scandium", 21);  
    AddToDictionary(elements, "Ti", "Titanium", 22);  
  
    return elements;  
}  
  
private static void AddToDictionary(Dictionary<string, Element> elements,  
    string symbol, string name, int atomicNumber)  
{  
    Element theElement = new Element();  
  
    theElement.Symbol = symbol;  
    theElement.Name = name;  
    theElement.AtomicNumber = atomicNumber;  
  
    elements.Add(key: theElement.Symbol, value: theElement);  
}  
  
public class Element  
{  
    public string Symbol { get; set; }  
    public string Name { get; set; }  
    public int AtomicNumber { get; set; }  
}  
```  
  
 Au lieu d’utiliser un initialiseur de collection pour générer la collection `Dictionary`, vous pouvez remplacer les méthodes `BuildDictionary` et `AddToDictionary` par la méthode suivante.  
  
```csharp  
private static Dictionary<string, Element> BuildDictionary2()  
{  
    return new Dictionary<string, Element>  
    {  
        {"K",  
            new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},  
        {"Ca",  
            new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},  
        {"Sc",  
            new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},  
        {"Ti",  
            new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}  
    };  
}  
```  
  
 L’exemple suivant utilise la méthode <xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A> et la propriété <xref:System.Collections.Generic.Dictionary%602.Item%2A> de `Dictionary` pour rechercher rapidement un élément par clé. En C#, la propriété `Item` vous permet d’accéder à un élément de la collection `elements` à l’aide d’`elements[symbol]`.  
  
```csharp  
private static void FindInDictionary(string symbol)  
{  
    Dictionary<string, Element> elements = BuildDictionary();  
  
    if (elements.ContainsKey(symbol) == false)  
    {  
        Console.WriteLine(symbol + " not found");  
    }  
    else  
    {  
        Element theElement = elements[symbol];  
        Console.WriteLine("found: " + theElement.Name);  
    }  
}  
```  
  
 L’exemple suivant utilise à la place la méthode <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> pour rechercher rapidement un élément par clé.  
  
```csharp  
private static void FindInDictionary2(string symbol)  
{  
    Dictionary<string, Element> elements = BuildDictionary();  
  
    Element theElement = null;  
    if (elements.TryGetValue(symbol, out theElement) == false)  
        Console.WriteLine(symbol + " not found");  
    else  
        Console.WriteLine("found: " + theElement.Name);  
}  
```  

<a name="BKMK_LINQ"></a>
## <a name="using-linq-to-access-a-collection"></a>Utilisation de LINQ pour accéder à une collection  
 LINQ (Language-Integrated Query) peut être utilisé pour accéder aux collections. Les requêtes LINQ fournissent des fonctionnalités de filtrage, de classement et de regroupement. Pour plus d’informations, consultez [Bien démarrer avec LINQ en C#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md).  
  
 L’exemple suivant exécute une requête LINQ sur un `List` générique. La requête LINQ retourne une autre collection qui contient les résultats.  
  
```csharp  
private static void ShowLINQ()  
{  
    List<Element> elements = BuildList();  
  
    // LINQ Query.  
    var subset = from theElement in elements  
                 where theElement.AtomicNumber < 22  
                 orderby theElement.Name  
                 select theElement;  
  
    foreach (Element theElement in subset)  
    {  
        Console.WriteLine(theElement.Name + " " + theElement.AtomicNumber);  
    }  
  
    // Output:  
    //  Calcium 20  
    //  Potassium 19  
    //  Scandium 21  
}  
  
private static List<Element> BuildList()  
{  
    return new List<Element>  
    {  
        { new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},  
        { new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},  
        { new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},  
        { new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}  
    };  
}  
  
public class Element  
{  
    public string Symbol { get; set; }  
    public string Name { get; set; }  
    public int AtomicNumber { get; set; }  
}  
```  

<a name="BKMK_Sorting"></a>
## <a name="sorting-a-collection"></a>Tri d’une collection  
 L’exemple suivant illustre une procédure de tri d’une collection. L’exemple trie les instances de la classe `Car` stockées dans un <xref:System.Collections.Generic.List%601>. La classe `Car` implémente l’interface <xref:System.IComparable%601>, ce qui implique l’implémentation de la méthode <xref:System.IComparable%601.CompareTo%2A>.  
  
 Chaque appel à la méthode <xref:System.IComparable%601.CompareTo%2A> effectue une comparaison unique qui est utilisée pour le tri. Le code écrit par l’utilisateur dans la méthode `CompareTo` retourne une valeur pour chaque comparaison de l’objet actuel avec un autre objet. La valeur retournée est inférieure à zéro si l’objet actuel est inférieur à l’autre objet, supérieure à zéro l’objet actuel est supérieur à l’autre et égale à zéro s’ils sont égaux. Cela vous permet de définir dans le code les critères définissant « supérieur à », « inférieur à » et « égal à ».  
  
 Dans la méthode `ListCars`, l’instruction `cars.Sort()` trie la liste. Cet appel à la méthode <xref:System.Collections.Generic.List%601.Sort%2A> de <xref:System.Collections.Generic.List%601> entraîne l’appel automatique de la méthode `CompareTo` pour les objets `Car` dans `List`.  
  
```csharp  
private static void ListCars()  
{  
    var cars = new List<Car>  
    {  
        { new Car() { Name = "car1", Color = "blue", Speed = 20}},  
        { new Car() { Name = "car2", Color = "red", Speed = 50}},  
        { new Car() { Name = "car3", Color = "green", Speed = 10}},  
        { new Car() { Name = "car4", Color = "blue", Speed = 50}},  
        { new Car() { Name = "car5", Color = "blue", Speed = 30}},  
        { new Car() { Name = "car6", Color = "red", Speed = 60}},  
        { new Car() { Name = "car7", Color = "green", Speed = 50}}  
    };  
  
    // Sort the cars by color alphabetically, and then by speed  
    // in descending order.  
    cars.Sort();  
  
    // View all of the cars.  
    foreach (Car thisCar in cars)  
    {  
        Console.Write(thisCar.Color.PadRight(5) + " ");  
        Console.Write(thisCar.Speed.ToString() + " ");  
        Console.Write(thisCar.Name);  
        Console.WriteLine();  
    }  
  
    // Output:  
    //  blue  50 car4  
    //  blue  30 car5  
    //  blue  20 car1  
    //  green 50 car7  
    //  green 10 car3  
    //  red   60 car6  
    //  red   50 car2  
}  
  
public class Car : IComparable<Car>  
{  
    public string Name { get; set; }  
    public int Speed { get; set; }  
    public string Color { get; set; }  
  
    public int CompareTo(Car other)  
    {  
        // A call to this method makes a single comparison that is  
        // used for sorting.  
  
        // Determine the relative order of the objects being compared.  
        // Sort by color alphabetically, and then by speed in  
        // descending order.  
  
        // Compare the colors.  
        int compare;  
        compare = String.Compare(this.Color, other.Color, true);  
  
        // If the colors are the same, compare the speeds.  
        if (compare == 0)  
        {  
            compare = this.Speed.CompareTo(other.Speed);  
  
            // Use descending order for speed.  
            compare = -compare;  
        }  
  
        return compare;  
    }  
}  
```  
  
<a name="BKMK_CustomCollection"></a>
## <a name="defining-a-custom-collection"></a>Définition d’une collection personnalisée  
 Vous pouvez définir une collection en implémentant l’interface <xref:System.Collections.Generic.IEnumerable%601> ou <xref:System.Collections.IEnumerable>. Pour plus d’informations, consultez [Guide pratique pour accéder à une classe de collection à l’aide de foreach](../../../csharp/programming-guide/classes-and-structs/how-to-access-a-collection-class-with-foreach.md).  
  
 Même si vous pouvez définir une collection personnalisée, il est généralement préférable d’utiliser les collections comprises dans le .NET Framework, lesquelles sont décrites dans [Types de collections](#BKMK_KindsOfCollections), plus haut dans cette rubrique.  
  
 L’exemple suivant définit une classe de collection personnalisée nommée `AllColors`. Cette classe implémente l’interface <xref:System.Collections.IEnumerable>, ce qui implique l’implémentation de la méthode <xref:System.Collections.IEnumerable.GetEnumerator%2A>.  
  
 La méthode `GetEnumerator` retourne une instance de la classe `ColorEnumerator`. `ColorEnumerator` implémente l’interface <xref:System.Collections.IEnumerator>, ce qui implique l’implémentation de la propriété <xref:System.Collections.IEnumerator.Current%2A>, la méthode <xref:System.Collections.IEnumerator.MoveNext%2A> et la méthode <xref:System.Collections.IEnumerator.Reset%2A>.  
  
```csharp  
private static void ListColors()  
{  
    var colors = new AllColors();  
  
    foreach (Color theColor in colors)  
    {  
        Console.Write(theColor.Name + " ");  
    }  
    Console.WriteLine();  
    // Output: red blue green  
}  
  
// Collection class.  
public class AllColors : System.Collections.IEnumerable  
{  
    Color[] _colors =  
    {  
        new Color() { Name = "red" },  
        new Color() { Name = "blue" },  
        new Color() { Name = "green" }  
    };  
  
    public System.Collections.IEnumerator GetEnumerator()  
    {  
        return new ColorEnumerator(_colors);  
  
        // Instead of creating a custom enumerator, you could  
        // use the GetEnumerator of the array.  
        //return _colors.GetEnumerator();  
    }  
  
    // Custom enumerator.  
    private class ColorEnumerator : System.Collections.IEnumerator  
    {  
        private Color[] _colors;  
        private int _position = -1;  
  
        public ColorEnumerator(Color[] colors)  
        {  
            _colors = colors;  
        }  
  
        object System.Collections.IEnumerator.Current  
        {  
            get  
            {  
                return _colors[_position];  
            }  
        }  
  
        bool System.Collections.IEnumerator.MoveNext()  
        {  
            _position++;  
            return (_position < _colors.Length);  
        }  
  
        void System.Collections.IEnumerator.Reset()  
        {  
            _position = -1;  
        }  
    }  
}  
  
// Element class.  
public class Color  
{  
    public string Name { get; set; }  
}  
```  

<a name="BKMK_Iterators"></a> 
##  <a name="iterators"></a>Iterators  
 Un *itérateur* est utilisé pour exécuter une itération personnalisée sur une collection. Un itérateur peut être une méthode ou un accesseur `get`. Un itérateur utilise une instruction [yield return](../../../csharp/language-reference/keywords/yield.md) pour retourner chaque élément de la collection un par un.  
  
 Vous appelez un itérateur en utilisant une instruction [foreach](../../../csharp/language-reference/keywords/foreach-in.md). Chaque itération de la boucle `foreach` appelle l’itérateur. Quand une instruction `yield return` est atteinte dans l’itérateur, une expression est retournée et la localisation actuelle dans le code est retenue. L’exécution est redémarrée à partir de cet emplacement la prochaine fois que l’itérateur est appelé.  
  
 Pour plus d’informations, consultez [Itérateurs (C#)](../../../csharp/programming-guide/concepts/iterators.md).  
  
 L'exemple suivant utilise une méthode Iterator. La méthode Iterator a une instruction `yield return` qui se trouve à l’intérieur d’une boucle [for](../../../csharp/language-reference/keywords/for.md). Dans la méthode `ListEvenNumbers`, chaque itération du corps de l’instruction `foreach` crée un appel à la méthode Iterator, qui continue sur l’instruction `yield return` suivante.  
  
```csharp  
private static void ListEvenNumbers()  
{  
    foreach (int number in EvenSequence(5, 18))  
    {  
        Console.Write(number.ToString() + " ");  
    }  
    Console.WriteLine();  
    // Output: 6 8 10 12 14 16 18  
}  
  
private static IEnumerable<int> EvenSequence(  
    int firstNumber, int lastNumber)  
{  
    // Yield even numbers in the range.  
    for (var number = firstNumber; number <= lastNumber; number++)  
    {  
        if (number % 2 == 0)  
        {  
            yield return number;  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Initialiseurs d’objets et de collections](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)  
 [Concepts de programmation (C#)](../../../csharp/programming-guide/concepts/index.md)  
 [Option Strict (instruction)](../../../visual-basic/language-reference/statements/option-strict-statement.md)  
 [LINQ to Objects (C#)](../../../csharp/programming-guide/concepts/linq/linq-to-objects.md)  
 [Parallel LINQ (PLINQ)](../../../standard/parallel-programming/parallel-linq-plinq.md)  
 [Collections et structures de données](../../../standard/collections/index.md)  
 [Création et manipulation de collections](http://msdn.microsoft.com/library/2065398e-eb1a-4821-9188-75f16e42e069)  
 [Sélection d’une classe de collection](../../../standard/collections/selecting-a-collection-class.md)  
 [Comparaisons et tris dans les collections](../../../standard/collections/comparisons-and-sorts-within-collections.md)  
 [Quand utiliser les collections génériques](../../../standard/collections/when-to-use-generic-collections.md)  
 [Comment : accéder à une classe de collection à l’aide de foreach](../../../csharp/programming-guide/classes-and-structs/how-to-access-a-collection-class-with-foreach.md)
