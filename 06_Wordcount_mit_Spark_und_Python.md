#### [Zum Anfang](README.md "Hier gelangen Sie zur Startseite") | [Inhaltsverzeichnis](00_Inhaltsverzeichnis.md "Hier gelangen Sie zum Inhaltsverzeichnis")

# 6 Wordcount mit Spark und Python

In diesem Kapitel wird beispielhaft die Installation und Verwendung von _Spark_ auf Basis folgender Komponenten
demonstriert:

* Java zur Unterstützung von Spark
* Spark in der aktuellen Version 3.2.0
* FindSpark zum einfachen Zugriff auf Spark (Python Bibliothek)
* PySpark als Bibliothek zur Arbeit mit Spark (Python Bibliothek)

Für diese Aufgabe wird auf Grund der einfachen Verfügbarkeit
[_Google Colaboratory_](03_Mögliche_Umgebungen_für_Spark.md#spark-mit-google-colaboratory-colab "Hier geht es zum Abschnitt Google Colaboratory")
verwendet, die Programmierung erfolgt mit Python. Das hierbei entstehende [_Jupyter Notebook_](06__Wordcount_mit_Spark.ipynb "Zum Notebook") ist Teil dieser Arbeit und
kann frei verwendet werden. Insbesondere der erste Teil, in dem die Arbeitsumgebung selbst aufgesetzt wird, bietet
hierbei eine einfache Basis zur Wiederverwendung, um erste Erfahrungen mit Spark zu sammeln.

Als Beispielaufgabe dient eine einzelne Textdatei mit allen
[literarischen Werken von Shakespeare](https://ocw.mit.edu/ans7870/6/6.006/s08/lecturenotes/files/t8.shakespeare.txt "Link zum Download der Datei")
. Diese Textdatei ist an mehreren Stellen im Internet frei verfügbar. Für dieses Beispiel wird auf das Angebot des
Massachusetts [Institute of Technology (MIT)](https://ocw.mit.edu/ "Zur Webseite des MIT") zurück gegriffen.

Insgesamt enthält die Datei:

* 5.333.743 Zeichen ohne Zeilenende in,
* 929.396 Wörter in
* 124.457 Zeilen.

## Vorbereiten des Notebooks

Alle Arbeiten, die der Vorbereitung des Notebooks dienen, snd im Abschnitt _Vorbereitung des Notebooks_ hinterlegt. Für
diesen Abschnitt kann auf das Kapitel [_Google
Colaboratory_](03_Mögliche_Umgebungen_für_Spark.md#spark-mit-google-colaboratory-colab "Hier geht es zum Abschnitt Google Colaboratory")
dieser Arbeit zurück gegriffen werden.

## Auszählen der Wörter

Im Abschnitt _Auszählen der Wörter_ wird die hier vorgestellt Aufgabe konkret umgesetzt. 
