#### [Zum Anfang](README.md "Hier gelangen Sie zur Startseite") | [Inhaltsverzeichnis](00_Inhaltsverzeichnis.md "Hier gelangen Sie zum Inhaltsverzeichnis")

# 2 Datenstrukturen

In den folgenden Unterkapiteln wird auf die für das Verständnis von Spark wichtigen Konzepte und Datentrukturen
eingegangen. Auch soll eine Übersicht über die wichtigsten Funktionalitäten gegeben werden.

Die vollständige Behandlung aller Themen soll und kann hierbei nicht geleistet werden. Hierzu sei auf die offizielle
Dokumentation hingewiesen. Eine erste Orientierung kann hierbei die
[Linksliste](https://github.com/ChristianKitte/SparkProjekt/blob/main/Anhang_Linkliste.md
"Hier befindet sich eine Liste mit weiteren Webressourcen zum Thema")
am Ende dieses Repositories geben.

Auch bietet das
[Praxisbeispiel](06_Wordcount_mit_Spark_und_Python.md "Beispiel einer realen Anwendung mit Spark und Python"). einen
guten Einstieg

* [_Hadoop_](02_Datenstrukture#Hadoop )
* [_Spark_](02_Datenstrukture#Spark )
* [_Spark Dataframes_](02_Datenstrukture#Spark_Dataframes )
* [_Spark Datasets_](02_Datenstrukture#Spark_Datasets )

## Hadoop

### Distributed Speicher HDFS C

### Map Reduce C

## Spark

### Resilent Distributed Dataset (RDD)

RDD steht für Resilient Distributed Dataset (auf deutsch etwa “robuster verteilter Datensatz”) und stellt das zentrale
Konzept und Objekt für die Abstraktion von Datasets innerhalb von Spark da.

Die Arbeit von Spark kann letztlich auf das Anlegen neuer sowie der Transformation und das Ausführen Operationen auf
vorhandenen RDDs betrachtet werden. Hierbei ist das RDD immutable. Jede Aktion auf ein RDD verändert das zugrunde
liegende RDD nicht, sondern gibt stets ein neues RDD zurück. Hierbei nutzt Spark in starken Maße die Übergabe von
Funktionen.

Es gibt verschiedene Wege, um ein RDD zu erstellen. Gemein ist allen, dass Spark bei der Erstellung die Arbeitsdaten
verteilt und später alle Operationen automatisch verteilt und parallelisiert ausführt. Der generelle Workflow ist
hierbei:

* Erstellen des RDD
* Anwenden von Transformationen
* Ausführen von Aktionen

#### Erzeugen von RDDs

Grundsätzlich existieren zwei Möglichkeiten, um ein RDD zu erzeugen. Zum einen ist dies die Verwendung einer
existierenden Collection, zum anderen das Referenzieren einer eines extern vorliegenden Datasets.

Bei der Verwendung von Collections werden die Daten bereits im Vorfeld aus den jeweiligen Quellen gelesen und in Form
einer geeigneten Collection gehalten. Mithilfe der Methode parallelize wird dann aus der Collection ein RDD erstellt.
Diese Methode eignet sich insbesondere für Datenbestände, welche mit normalen Werkzeugen gut zu handhaben sind:

```python
sc = SparkContext("local", "SampleApp")
integers = list(range(1,6)
integers_rdd = sc.parallelize(integers)
```

Für sehr große Daten ist die Verwendung der textFile Methode sinnvoller. Mit ihrer Hilfe können auch sehr große,
entfernte Daten einem RDD zugeführt werden:

```python
sc = SparkContext("local", "SampleApp")
lines_rdd = sc.textFile("text.txt")
```

Diese Methode eignet sich auch für externe Datenspeicher wie Amazon S3, HDFS, Cassandra, Elasticsearch sowie JDBC.

### Übergabe von Funktionen in Spark

### Schließen in Spark

#### Transformations

Eine Transformation wendet eine Funktion auf jedes Element des RDD an. Eine häufige Transformation ist das Filtern:

```python
sc = SparkContext("local", "SampleApp")
lines_rdd = sc.textFile("text.txt")
lines_with_friday_rdd = linesRDD.filter(lambda line: "Friday" in line)
```

##### Filter, Map und FlatMap

Mit zu den wichtigsten Transformationen zählen die Funktionen Filter, Map und FlatMap. Gemein ist allen, dass ihnen eine
Funktion als Parameter übergeben wird, welche die eigentliche Transformation oder Selektierung ausführt.

##### filter

Bei der Filtermethode wird der Funktion eine Filtermethode übergeben, die auf alle Elemente des RDD angewendet wird. Als
Ergebnis wird ein neues RDD auf Basis der selektierten Elemente zurückgegeben.

![spark_filter.png](./assets/spark_filter.png "Prinzip der Filterung eines RDD")

##### map

Bei der Map Methode wird die übergebene Funktion auf alle Elemente des RDD angewendet. Hierbei erfolgt genau eine
Transformation von einem Zustand in einen anderen. Als Ergebnis wird auch hier ein RDD mit den neuen Werten zurück
gegeben.

![spark_map.png](./assets/spark_map.png "Prinzip des Map Transformation")

```python
sc = SparkContext("local", "SampleApp")
lines = sc.textFile("text.txt")
lengths = lines.map(lambda line: len(line))
```

Der Typ der zurückgegebenen Elemente muss hierbei nicht dem Typ der ursprünglichen Elemente entsprechen. Wird
beispielsweise für Textelemente die Länge ermittelt, so handelt es sich bei dem zurückgegebenen Elementen um
Zahlenwerte.

##### flatMap

Flat Map unterscheidet sich zu Map dadurch, dass die übergebene Funktion mehr als ein Element zurück geben kann.

![spark_flat_map.png](./assets/spark_flat_map.png "Prinzip der FlatMap Transformation")

##### group, reduce, aggregate und sortByKey

#### Actions

Eine Aktion lieferte ein Ergebnis auf Basis des RDD zurück. Eine häufige Action ist die Wiedergabe des ersten Elements
eines RDD.

```python
sc = SparkContext("local", "SampleApp")
lines = sc.textFile("text.txt")
lengths = lines.first()
```

##### collect

##### first

##### count vs countByKey

##### foreach

##### saveAsTextFile

## Spark Dataframes

Die Arbeit auf Basis der zuvor behandelten RDDs ist gut geeignet, wenn man nahe an Spark arbeiten und den größtmöglichen
Einfluss haben möchte. Auf der anderen Seite erfordert die Einarbeitung und der Umgang mit diesen Objekt eine gewisse
Einarbeitung.

Mit der Version 2.0 führte Spark Dataframes ein. Sie sollen die Arbeit und den Umgang mit Spark vereinfachen und bieten
eine Abstraktion der Datensicht in Spark, nutzen jedoch intern die API der RDDs. Daher können sie nicht nur auf Basis
eines bereits vorhandenen RDDs, sondern auf Basis aller von Spark unterstützten Datenquelle wie beispielsweise einer
Hive Tabelle erzeugt werden.

In der Regel geht man beid er Arbeit mit DataFrames den Weg über eine Spark Session und deren **_build Methode_**.
Anschließend stehen unter anderen eine Reihe von Funktionen wie **_read_** zur Verfügung, um Textdateien einzulesen.

```python
from pyspark.sql import SparkSession
import pyspark.sql.functions as func

session = SparkSession.builder.appName("Anwendungsname").getOrCreate()
dataframe = session.read.text("Pfad zu einer Datei")
```

Spark Dataframes können hierbei sowohl das Schema der vorhandenen Daten ableiten oder aber ein Schema für die Daten
zugewiesen bekommen. Letzteres ist besonders bei sehr großen Datenbeständen sinnvoll. Hierdurch ist eine Optimierung von
Aktionen auf den Daten möglich. Es ist daher nicht verwunderlich, dass Spark Dataframes ein Bestandteil von Spark SQL,
welche die Arbeit mit strukturierten Daten zuständig ist.

Dataframes sind somit kein Ersatz der RDDs, sondern können als eine Abstraktionsschicht auf die Daten und deren Handling
mit RDDs angesehen werden. Dies verdeutlicht auch die folgende Abbildung.

![spark_dataset.png](./assets/spark_dataset.png "Einordnung des Spark DataSet")

Besonders im Umfeld von Python sind Dataframes als Pandas DataFrames bekannt und in der Tat zeigen sich im Umgang eine
Reihe von Gemeinsamkeiten aber auch Unterschiede. Der wichtigste ist, dass ein Spark Dataframe eine verteilte Kollektion
von Daten ist, welche konzeptuell ein zweidimensionalen Array mit den Reihen und Spalten eines Datenbestandes bilden. Es
wurde für die Verarbeitung sehr großer Datenestände optimiert.

## Spark Datasets
