#### [Zum Anfang](README.md "Hier gelangen Sie zur Startseite") | [Inhaltsverzeichnis](00_Inhaltsverzeichnis.md "Hier gelangen Sie zum Inhaltsverzeichnis")

# 7 Wordcount mit Spark DataFrames und Python

An dieser Stelle wird eine Variante der zuvor im Kapitel
[Wordcount mit Spark und Python](06_Wordcount_mit_Spark_und_Python.md "Beispiel einer realen Anwendung mit Spark und Python")
vorgestellten Beispiels vorgestellt.

Auch wenn viele der Methoden auf Grund der gleichen Aufgabenstellung gleichbleiben, finden sich im Gegensatz zur
vorherigen Anwendung entscheidende Änderungen in der Art der Sparknutzung. Statt mit RDDs kommen nunmehr die neueren
Data Frames Objekte zum Einsatz.

Im folgenden soll nun auf die Unterschiede in der Programmierung kurz eingegangen werden. Um unnötige Wiederholungen
zu vermeiden wird auf die Erklärung der bereits zuvor verwendeten Codebestandteile verzichtet. Diese werden bereits
ausführlich im
[vorhergehenden Kapitel](06_Wordcount_mit_Spark_und_Python.md "Beispiel einer realen Anwendung mit Spark und Python")
erklärt.

Wie bereits zuvor ist auch der Code dieses Abschnitts als lauffähiges  
[_Jupyter Notebook_](notebook/Wordcount_mit_Spark.ipynb "Zum Notebook")
Teil dieser Arbeit und frei verwendbar.

## Session statt Context

to do: erklären

```python
# Initialisieren von findspark

try: 
  import findspark
  from pyspark.sql import SparkSession
  
  findspark.init()
  
  print("FindSpark und PySpark wurden initialisiert")
except ImportError: 
  raise ImportError("Fehler bei der Initialiserung von FindSpark und PySpark")
```  

```python
# Erzeugen einer Spark Session

session = SparkSession.builder.appName("Wordcount").getOrCreate()

print("Die Spark Session wurde angelegt...")
```

## DataFrame Methoden statt Map

to do: erklären

```python
# Auszählen der Wörter

import pyspark.sql.functions as func

dfx = session.read.text(file_target)

top_out = 30
top_length = 30

print("")
print("Ausgabe der ersten {} Zeilen des Textes".format(top_out))
print("")

dfx.show(n=top_out,truncate=False)

#dfx.printSchema()
#dfx.describe().show()
#print(dfx.columns)

dfx=dfx.withColumn('value', func.translate('value', ',', ' '))
dfx=dfx.withColumn('value', func.translate('value', '.', ' '))
dfx=dfx.withColumn('value', func.translate('value', '-', ' '))
dfx=dfx.withColumn('value', func.lower('value'))

print("")
print("Ausgabe der {} größten Vorkommen".format(top_length))
print("")

dfx=dfx.withColumn('value2',func.explode(func.split(func.col('value'), ' ')))\
  .groupBy('value2')\
  .count()\
  .sort('count', ascending=False)\
  .show(n=top_length,truncate=False)
```  
