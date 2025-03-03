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
