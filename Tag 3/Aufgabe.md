# Pure Functions

+
Keine Seiteneffekte → Vorhersehbares Verhalten & weniger Bugs.
Einfach zu testen → Da sie nur von Parametern abhängen, braucht man keine komplexe Testumgebung.
Klarer Code → Verständlicher, weil keine externen Abhängigkeiten berücksichtigt werden müssen.

-
Performance-Einbußen → Weil neue Kopien von Daten erstellt werden, kann das mehr Speicher & Zeit kosten.
Komplexität durch Rekursion → Kann schwerer zu verstehen sein & erhöht den Speicherverbrauch.

# Lösung - Pure vs. Impure Functions

## Aufgabe 1 - Bewertung der Funktionen  

| **Aufgabe** | **Nur ein Rückgabewert** | **Resultat nur abhängig von Parametern** | **Verändert keine existierenden Werte** | **pure oder impure** |
|------------|--------------------------|------------------------------------------|-----------------------------------------|----------------------|
| **1.1** `addToCart(item)` | ✅ Ja | ❌ Nein (greift auf `cartItems` zu) | ❌ Nein (verändert `cartItems`) | **impure** |
| **1.2** `add(a, b)` | ✅ Ja | ✅ Ja | ✅ Ja | **pure** |
| **1.3** `firstCharacter(str)` | ✅ Ja | ✅ Ja | ✅ Ja | **pure** |
| **1.4** `multiplyWithRandom(number)` | ✅ Ja | ❌ Nein (`Math.random()` ist nicht deterministisch) | ✅ Ja | **impure** |
| **1.5** `divideNumbers(dividend, divisor)` | ✅ Ja | ✅ Ja | ✅ Ja | **pure** |
| **1.6** `printAndReturnString(str)` | ✅ Ja | ✅ Ja | ❌ Nein (`console.log()` erzeugt Seiteneffekte) | **impure** |

---

## Aufgabe 2 - Umschreiben von impure zu pure functions  

### Java - Pure Function Versionen  

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Random;

public class PureFunctions {

    // Aufgabe 1.1 - Pure Version: Erstellt eine neue Liste, statt das Original zu verändern
    public static List<String> addToCart(List<String> cart, String item) {
        List<String> newCart = new ArrayList<>(cart);
        newCart.add(item);
        return newCart;
    }

    // Aufgabe 1.4 - Pure Version: Zufallszahl als Parameter übergeben
    public static double multiplyWithRandom(double number, double randomValue) {
        return number * randomValue;
    }

    // Aufgabe 1.6 - Pure Version: Keine Ausgabe auf der Konsole
    public static String returnString(String str) {
        return str;
    }

    public static void main(String[] args) {
        List<String> cart = new ArrayList<>();
        List<String> updatedCart = addToCart(cart, "Apple");
        System.out.println(updatedCart); // Ausgabe: [Apple]

        double randomValue = new Random().nextDouble();
        System.out.println(multiplyWithRandom(5, randomValue));

        System.out.println(returnString("Hello")); // Ausgabe: Hello
    }
}
```

import java.util.List;
import java.util.Collections;
import java.util.Comparator;
import java.util.ArrayList;

public class RecursiveFunctions {

    // Aufgabe 3.1 - Summe der Listenelemente berechnen
    public static int sumList(List<Integer> numbers) {
        if (numbers.isEmpty()) return 0;
        return numbers.get(0) + sumList(numbers.subList(1, numbers.size()));
    }

    // Aufgabe 3.2 - Mittelwert der Listenelemente berechnen
    public static double averageList(List<Integer> numbers) {
        if (numbers.isEmpty()) return 0;
        return (double) sumList(numbers) / numbers.size();
    }

    // Aufgabe 3.3 - Alphabetische Sortierung mit Rekursion
    public static List<String> sortStrings(List<String> strings) {
        if (strings.size() <= 1) return strings;
        String pivot = strings.get(0);
        List<String> smaller = new ArrayList<>();
        List<String> greater = new ArrayList<>();
        for (int i = 1; i < strings.size(); i++) {
            if (strings.get(i).compareTo(pivot) <= 0) smaller.add(strings.get(i));
            else greater.add(strings.get(i));
        }
        List<String> sorted = new ArrayList<>(sortStrings(smaller));
        sorted.add(pivot);
        sorted.addAll(sortStrings(greater));
        return sorted;
    }

    // Aufgabe 3.4 - Sortieren von Objekten nach Datum, Priorität, Titel
    public static List<Task> sortTasks(List<Task> tasks) {
        if (tasks.size() <= 1) return tasks;
        Task pivot = tasks.get(0);
        List<Task> smaller = new ArrayList<>();
        List<Task> greater = new ArrayList<>();
        for (int i = 1; i < tasks.size(); i++) {
            if (tasks.get(i).compareTo(pivot) <= 0) smaller.add(tasks.get(i));
            else greater.add(tasks.get(i));
        }
        List<Task> sorted = new ArrayList<>(sortTasks(smaller));
        sorted.add(pivot);
        sorted.addAll(sortTasks(greater));
        return sorted;
    }

    // Aufgabe 3.5 - Blätter aus einem Baum auslesen (Annahme: Der Baum ist eine verschachtelte Liste)
    public static List<Integer> getLeaves(List<Object> tree) {
        List<Integer> leaves = new ArrayList<>();
        for (Object node : tree) {
            if (node instanceof Integer) {
                leaves.add((Integer) node);
            } else if (node instanceof List) {
                leaves.addAll(getLeaves((List<Object>) node));
            }
        }
        return leaves;
    }

    public static void main(String[] args) {
        // Beispieltests
        List<Integer> numbers = List.of(1, 2, 3, 4, 5);
        System.out.println(sumList(numbers)); // Ausgabe: 15
        System.out.println(averageList(numbers)); // Ausgabe: 3.0

        List<String> words = List.of("Banane", "Apfel", "Zitrone", "Orange");
        System.out.println(sortStrings(words));

        List<Object> tree = List.of(1, List.of(2, 3), List.of(4, List.of(5, 6)));
        System.out.println(getLeaves(tree)); // Ausgabe: [1, 2, 3, 4, 5, 6]
    }
}

// Klasse für Aufgabe 3.4 - Vergleich von Aufgaben
class Task implements Comparable<Task> {
    String date;
    int priority;
    String title;

    public Task(String date, int priority, String title) {
        this.date = date;
        this.priority = priority;
        this.title = title;
    }

    @Override
    public int compareTo(Task other) {
        int dateCompare = this.date.compareTo(other.date);
        if (dateCompare != 0) return dateCompare;
        int priorityCompare = Integer.compare(this.priority, other.priority);
        if (priorityCompare != 0) return priorityCompare;
        return this.title.compareTo(other.title);
    }

    @Override
    public String toString() {
        return date + " | " + priority + " | " + title;
    }
}
