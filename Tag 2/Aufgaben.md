```
import java.util.*;

// Aufgabe 1 - Reise planen
class ReisePlanung {
    private List<String> route;

    public ReisePlanung() {
        this.route = new ArrayList<>();
    }

    public void addDestination(String destination) {
        route.add(destination);
    }

    public void removeDestination(String destination) {
        route.remove(destination);
    }

    public void updateDestination(String oldDestination, String newDestination) {
        int index = route.indexOf(oldDestination);
        if (index != -1) {
            route.set(index, newDestination);
        }
    }

    public void displayRoute() {
        System.out.println("Aktuelle Route: " + String.join(" -> ", route));
    }
}

// Aufgabe 2 - Wörter mit Punkten bewerten
class WortBewertung {
    private Map<String, Integer> wordScores = new HashMap<>();

    public void addWord(String word) {
        int score = calculateScore(word);
        wordScores.put(word, score);
    }

    private int calculateScore(String word) {
        int score = 0;
        for (char c : word.toCharArray()) {
            if (c != 'a' && c != 'A') {
                score++;
            }
        }
        return score;
    }

    public void displaySortedWords() {
        wordScores.entrySet().stream()
            .sorted((a, b) -> b.getValue().compareTo(a.getValue()))
            .forEach(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));
    }
}

// Aufgabe 3 - Autorennen
class AutoRennen {
    private List<Integer> zeiten;

    public AutoRennen() {
        this.zeiten = new ArrayList<>();
    }

    public void addTime(int time) {
        zeiten.add(time);
    }

    public int calculateTotalTime() {
        return zeiten.stream().skip(1).mapToInt(Integer::intValue).sum();
    }

    public double calculateAverageTime() {
        if (zeiten.size() <= 1) return 0;
        return zeiten.stream().skip(1).mapToInt(Integer::intValue).average().orElse(0);
    }
}

// Main-Klasse zum Testen
public class Main {
    public static void main(String[] args) {
        // Test für ReisePlanung
        ReisePlanung reise = new ReisePlanung();
        reise.addDestination("Berlin");
        reise.addDestination("Paris");
        reise.addDestination("Rom");
        reise.displayRoute();
        reise.updateDestination("Paris", "Madrid");
        reise.displayRoute();

        // Test für WortBewertung
        WortBewertung wb = new WortBewertung();
        wb.addWord("Hallo");
        wb.addWord("Apfel");
        wb.addWord("Banane");
        wb.displaySortedWords();

        // Test für AutoRennen
        AutoRennen rennen = new AutoRennen();
        rennen.addTime(60); // Warm-up Runde
        rennen.addTime(55);
        rennen.addTime(58);
        rennen.addTime(57);
        System.out.println("Gesamtzeit: " + rennen.calculateTotalTime());
        System.out.println("Durchschnittszeit: " + rennen.calculateAverageTime());
    }
}
```
