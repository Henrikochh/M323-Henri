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
