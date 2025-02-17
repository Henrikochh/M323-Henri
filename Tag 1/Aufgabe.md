# Aufgabe 1

```
    // Imperative Lösung
    public static int calculateScore(String word) {
        int score = 0;
        for (char c : word.toCharArray()) {
            if (c != 'a') {
                score++;
            }
        }
        return score;
    }
    // Deklarative Lösung
    public static int wordScore(String word) {
        return (int) word.chars()
                         .filter(c -> c != 'a')
                         .count();
    }
```
# Aufgabe 2

## Imperativ
```
import java.util.List;

public class ShoppingCartFunctional {

    public static double getDiscountPercentage(List<String> items) {
        return items.stream().anyMatch(item -> item.toLowerCase().contains("buch")) ? 5.0 : 0.0;
    }

    public static void main(String[] args) {
        List<String> cart1 = List.of("Laptop", "Buch: Java Programmierung");
        System.out.println("Rabatt: " + getDiscountPercentage(cart1) + "%");

        List<String> cart2 = List.of("Laptop", "Tablet");
        System.out.println("Rabatt: " + getDiscountPercentage(cart2) + "%");
    }
}
```

## Deklarativ

```
import java.util.ArrayList;
import java.util.List;

public class ShoppingCart {
    private List<String> items;
    private boolean bookAdded;

    public ShoppingCart() {
        this.items = new ArrayList<>();
        this.bookAdded = false;
    }

    public void addItem(String item) {
        items.add(item);
        if (item.toLowerCase().contains("buch")) {
            bookAdded = true;
        }
    }

    public void removeItem(String item) {
        items.remove(item);
        if (item.toLowerCase().contains("buch")) {
            bookAdded = items.stream().anyMatch(i -> i.toLowerCase().contains("buch"));
        }
    }

    public List<String> getItems() {
        return new ArrayList<>(items);
    }

    public double getDiscountPercentage() {
        return bookAdded ? 5.0 : 0.0;
    }

    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        cart.addItem("Laptop");
        cart.addItem("Buch: Java Programmierung");
        System.out.println("Rabatt: " + cart.getDiscountPercentage() + "%");
        
        cart.removeItem("Buch: Java Programmierung");
        System.out.println("Rabatt nach Entfernung: " + cart.getDiscountPercentage() + "%");
    }
}
```
