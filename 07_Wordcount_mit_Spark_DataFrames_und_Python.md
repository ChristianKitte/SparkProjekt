#### [Zum Anfang](README.md "Hier gelangen Sie zur Startseite") | [Inhaltsverzeichnis](00_Inhaltsverzeichnis.md "Hier gelangen Sie zum Inhaltsverzeichnis")

# 7 Wordcount mit Spark DataFrames und Python

An dieser Stelle wird eine Variante der zuvor im Kapitel
[Wordcount mit Spark und Python](06_Wordcount_mit_Spark_RDDs_und_Python.md "Beispiel einer realen Anwendung mit Spark und Python")
vorgestellten Beispiels vorgestellt.

Auch wenn viele der Methoden auf Grund der gleichen Aufgabenstellung gleichbleiben, finden sich im Gegensatz zur
vorherigen Anwendung entscheidende Änderungen in der Art der Sparknutzung. Statt mit RDDs kommen nunmehr die neueren
Data Frames Objekte zum Einsatz.

Im folgenden soll nun auf die Unterschiede in der Programmierung kurz eingegangen werden. Um unnötige Wiederholungen zu
vermeiden wird auf die Erklärung der bereits zuvor verwendeten Codebestandteile verzichtet. Diese werden bereits
ausführlich im
[vorhergehenden Kapitel](06_Wordcount_mit_Spark_RDDs_und_Python.md "Beispiel einer realen Anwendung mit Spark und Python")
erklärt.

Wie bereits zuvor ist auch der Code dieses Abschnitts als lauffähiges  
[_Jupyter Notebook_](notebook/Wordcount_mit_Spark.ipynb "Zum Notebook")
Teil dieser Arbeit und frei verwendbar.

## Session statt Context

Ein wichtiger Unterschied im Gegensatz zur Nutzung eines Spark Context ist, das hier nun eine Spark Session verwendet
werden soll. Zugriff auf Spark Session erhält man über die Bibliothek pyspark.sql, welche aus Gründen der
Übersichtlichkeit erst hier eingebunden wird.

Mit der folgenden Codesquenz erhält man eine Spark Session mit der Bezeichnung Wordcount. Ist diese Session noch nicht
vorhanden, so wird sie erstellt, ansonsten die vorhandene zurückgegeben.

```python
# Erzeugen einer Spark Session

from pyspark.sql import SparkSession
session = SparkSession.builder.appName("Wordcount").getOrCreate()

print("Die Spark Session wurde angelegt...")
```

## DataFrame Methoden statt Map

Anschließend wird die Textdatei eingelesen. Die Funktion Session.read.text liest eine Textdatei ein und gibt ein direkt
nutzbares typisiertes Spark DataFrame zurück. Über ein Reflexion-Prozess kann das Schema der enthaltenen Daten - in
diesem Fall ein nullable String – erkannt und ausgegeben werden.

Im Weiteren finden zunächst eine Reihe von Ersetzungen (replace), dann eine Konvertierung in Kleinbuchstaben (lower)
und am Schluss eine Filterung (filter) auf leere Zeilen statt. Hierbei wird jedes Mal ein neues DataFrame zurückgegeben.
Da Spark DataFrames auf RDDs basieren, sind auch sie immutable. Die Methode withColumn bewirkt, dass die übergebene
Funktion ähnlich der Map Funktion auf alle Datensätze angewendet wird.

Der letzte Schritt erinnert stark an ein SQL Konstrukt. Zunächst wird jeder Zeile durch ihre Leerzeichen gesplittet. Die
Funktion explode sorgt dafür, dass das so entstandene Array mit n Spalten als ein Array mit einer Spalte (value2)
und n Reihen zurückgegeben wird.

Die Funktion groupBy gruppiert die in value2 enthaltenen Werte (Wörter) und Count aggregiert die Anzahl der einzelnen
Vorkommen. Abgeschlossen wir die Anweisung mit einem sort und der Ausgabe der sortierten Liste. Die Nutzung der Fluent
API macht den Code hierbei gut lesbar. Ebenso fällt die Ähnlichkeit zu Panda DataFrames auf.

https://spark.apache.org/docs/2.1.0/api/python/pyspark.sql.html#pyspark.sql.functions.explode
https://dwgeek.com/replace-pyspark-dataframe-column-value-methods.html/

```python
# Auszählen der Wörter

import pyspark.sql.functions as func

df = session.read.text(file_target)

print("")
print("Schema der eingelesenen Datei:")
df.printSchema()
print("")

top_out = 30
top_length = 30

print("")
print("Ausgabe der ersten {} Zeilen des Textes".format(top_out))
print("")

df.show(n=top_out,truncate=False)

#df.printSchema()
#df.describe().show()
#print(df.columns)

df=df.withColumn('value', func.translate('value', ',', ' '))
df=df.withColumn('value', func.translate('value', '.', ' '))
df=df.withColumn('value', func.translate('value', '-', ' '))
df=df.withColumn('value', func.lower('value'))

print("")
print("Ausgabe der {} größten Vorkommen".format(top_length))
print("")

df=df.withColumn('value2',func.explode(func.split(func.col('value'), ' ')))\
  .groupBy('value2')\
  .count()\
  .sort('count', ascending=False)\
  .show(n=top_length,truncate=False)
```  

Das Ergebnis ist eine Liste aller Wörter mit deren Vorkommen in absteigender Reihenfolge. Hierbei steht an erster Stelle
das Leerzeichen als häufigster Vertreter.

![dataframe_wörter.png](./assets/dataframe_wörter.png "Ausgabe der Wortliste in absteigender Reihenfolge")
