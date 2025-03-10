# Mapping
// Übung 1: Jede Zahl verdoppeln
val zahlen = List(1, 2, 3, 4, 5)
val verdoppelt = zahlen.map(_ * 2)
println(verdoppelt) // List(2, 4, 6, 8, 10)

// Übung 2: Namen in Großbuchstaben umwandeln
val namen = List("Alice", "Bob", "Charlie")
val grossbuchstaben = namen.map(_.toUpperCase)
println(grossbuchstaben) // List("ALICE", "BOB", "CHARLIE")

// Übung 3: Die Hälfte jeder Zahl berechnen
val zahlen2 = List(12, 45, 68, 100)
val halbiert = zahlen2.map(_ / 2.0)
println(halbiert) // List(6.0, 22.5, 34.0, 50.0)

// Übung 4: Adressformatierung
case class Adresse(strasse: String, hausnummer: Int, postleitzahl: String, stadt: String)

val adressen = List(
  Adresse("Hauptstrasse", 10, "12345", "Musterstadt"),
  Adresse("Nebenstrasse", 5, "23456", "Beispielburg")
)

val adressStrings = adressen.map(a => s"${a.strasse} ${a.hausnummer}, ${a.postleitzahl} ${a.stadt}")
println(adressStrings) // List("Hauptstrasse 10, 12345 Musterstadt", "Nebenstrasse 5, 23456 Beispielburg")

// Übung 5: Nur die Vornamen in Großbuchstaben extrahieren
val namen2 = List("Max Mustermann", "Erika Mustermann")
val vornamenGross = namen2.map(_.split(" ")(0).toUpperCase)
println(vornamenGross) // List("MAX", "ERIKA")
