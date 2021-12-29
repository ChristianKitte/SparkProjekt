#### [Zum Anfang](README.md "Hier gelangen Sie zur Startseite") | [Inhaltsverzeichnis](00_Inhaltsverzeichnis.md "Hier gelangen Sie zum Inhaltsverzeichnis")

# 1 Spark
to Do: kurzes Intro...

* [Was ist Spark](01_Spark.md#sprachunterstützung)
* [Bisherige Entwicklungsgeschichte](01_Spark.md#bisherige-entwicklungsgeschichte)
* [Sprachunterstützung](01_Spark.md#sprachunterstützung)
* [Spark Ecosystem](01_Spark.md#spark-ecosystem)

## Was ist Spark

[_zurück_](01_Spark.md#1-Spark "Zurück")

## Bisherige Entwicklungsgeschichte

[_zurück_](01_Spark.md#1-Spark "Zurück")

Nach 
[eigenen Angaben](https://spark.apache.org/history.html "zur Webseite")
startete Apache Spark 2009 als ein Forschungsprojekt an der 
[UC Berkley](https://www.berkeley.edu/ "zur Webseite")
in Californien und wurde 2010 als Open Source Projekt veröffentlicht. In den folgenden Jahren erschienen 
eine Reihe wissenschaftlicher Puplikationen, die sich mit den zugrunde liegenden Ideen beschäftigten. Es bildete sich 
eine rasch wachsende Community. Seit 2014 ist es als 
[Top-Level-Projekt](https://blogs.apache.org/foundation/entry/the_apache_software_foundation_announces50 "Zum 
Blogeintrag")
Teil der  
[Apache Software Foundation](https://www.apache.org/ "zur Webseite").
Als Nutzer werden u.a. IBM, Intel und Yahoo aufgelistet.

Laut angaben von
[Databricks](https://databricks.com/de/spark/about "Zur Webseite") 
arbeiten (Stand 2021) über 1000 aktive Entwickler aus mehr als 250 Unternehmen und Organisationen an dem Projekt mit, 
welches sich zur größten Open Source Community im Bereich Big Data entwickelt habe. Am 13. Oktober 2021 wurde die 
aktuelle 
[Version 3.2.0](https://spark.apache.org/releases/spark-release-3-2-0.html "zur Webseite") 
veröffentlicht. 

Ebenfalls in 2013 wurde von den ehemaligen Entwicklern die Firma  
[Databricks](https://databricks.com "Zur Einstiegsseite von Databricks")
ins Leben gerufen. Databricks sieht sich selbst in der Verantwortung, das offene Entwicklungsmodell von Spark 
aufrecht zu erhalten und Spark selbst weiter zu entwickeln. Gleichzeitig verdient es Geld im Umfeld von Spark unter 
anderen durch Online Kurse und Eigenentwicklungen auf Basis von Spark wie **_lakehouse_**, einer eigenen Cloud Data 
Plattform. 

Laut 
[Wikipedia](https://en.wikipedia.org/wiki/Databricks "Zum Wikipediaeintrag von Databricks") 
arbeitet Databricks seit 2017 mit Microsoft zusammen, und ist hier unter den Namen **_Azure Databricks_** verfügbar. 
2021 Wurde eine Kooperation mit Google eingegangen, um Spark in dessen Cloud verfügbar zu machen. 

## Sprachunterstützung

[_zurück_](01_Spark.md#1-Spark "Zurück")

Auch wenn Apache Spark ursprünglich in Scala programmiert wurde, unterstützt es eine Reihe weiterer Sprachen, 
darunter die für das Umfeld von Big Data und Machine Learning wichtigen Sprachen Python und R.

Auf der Übersichtsseite zur aktuellen Version 3.2.0 (Stand Dezember 2021) werden die unterstützten Sprachen und 
deren jeweilige Mindestversion näher angegeben. Hiernach wird 

- [Java](https://openjdk.java.net/ "zur Webseite von OpenJDK")
  8/11 (Versionen vor 8u201 sind deprecated ab Spark 3.2.0, Maven Support, kann DataSets nutzen)
- [Scala](https://www.scala-lang.org/ "zur Webseite")
  2.12 (Maven Support, kann DataSets nutzen)
- [Python](https://www.python.org/ "zur Webseite")
  3.6+ (Version 3.6 und davor sind deprecated ab Spark 3.2.0, PySpark)  
- [R](https://www.r-project.org/ "zur Webseite")
  3.5+ (SparkR)
 

unterstützt. Insbesondere bei der Zusammenarbeit mit 
[Apache Arrow](https://arrow.apache.org/ "zur Webseite") 
wird zudem auf mögliche Probleme Im Umfeld von Java und Python angesprochen und auf die entsprechende 
[Dokumentation](https://arrow.apache.org/docs/ "zur Dokumentation") 
verwiesen.

Mit Spark SQL besteht zudem die Möglichkeit, auf strukturierte Daten unter Verwendung von 
[SQL](https://de.wikipedia.org/wiki/SQL "zur Wikipediaseite") 
(Structured Query Language) zuzugreifen.

Die Verwendung von Java und Scala als höhere objektorientierte Programmiersprachen ermöglicht die Verwendung der mit 
SparkSQL zuletzt eingeführten streng typisierten Datasets im Code zu nutzen. Ein weitere Vorteil dieser Sprachen ist 
die Möglichkeit, Apache Spark mit Hilfe von Maven direkt in Projekte einzubinden. 

Für die Arbeit Python existiert mit 
[PySpark](https://spark.apache.org/docs/latest/api/python/index.html "zur Webseite")
ein Interface, dass eine starke Integration vmit Python ermöglicht. 
Daneben existieren eine Vielzahl an Erweiterungen im Python, so dass keinerlei Einschränkungen bei der Arbeit 
mit Python existieren. Die fehlende Möglichkeit, SparkSQL zu nutzen, wird durch das Vorhandensein entsprechender 
Alternativen ausgeglichen. 

Mit
[SparkR (R on Spark)](https://spark.apache.org/docs/latest/sparkr.html "zur Webseite")
existiert leichtgewichtiges Frontend zur Nutzung von Spark. Daneben unterstützt das Paket auch das verteilte Lernen 
in Zusammenarbeit mit SparkML. Nach Meinung des Authors, scheint die Integration von Python jedoch bei weitem 
tiefergehend und in sich intuitiver zu sein. 

 




## Spark Ecosystem 

[_zurück_](01_Spark.md#1-Spark "Zurück")

### Spark Core

Spark Core bildet das Fundament des gesamten Spark Frameworks. Es bietet grundlegende Funktionen wie die Ablaufsteuerung, Aufgaben- und Zeitplanung (Scheduling), Bereitstellung von Input- und Output-Operationen sowie eine API für diverse Programmiersprachen.

### Resilient distributed Datasets

Die zu Grunde liegende Datenstruktur basiert auf sogenannten Resilient Distributed Datasets (RDD). RDDs dienen dazu, Datenmengen in Partitionen aufzuteilen und auf mehrere Systeme zu verteilen. Dies ermöglicht eine hohe Verarbeitungsgeschwindigkeit da Prozesse parallel auf mehreren Systemen ausgeführt und verteilte Daten zeitgleich abgerufen werden können. Außerdem erhöht es die Fehlertoleranz, da verlorene oder zerstörte Datenfragmente wiederhergestellt werden können.

![image](https://user-images.githubusercontent.com/45334665/146559813-ed25c571-6ce4-4e0d-94f9-26ed0bf2460b.png)

**Abbildung 1: Darstellung eines RDDs mit mehreren Spark Workern und Partitionen**

Die Verteilung der partitionierten Daten erfolgt durch Spark Core, wobei die Daten auf verschiedene Rechner innerhalb eines Clusters verteilt werden. Aus diesem Grund ist ein Cluster Manager eine Grundvoraussetzung, um die Funktionalität von Spark zu gewährleisten.

Als Cluster Manager werden Softwaresysteme bezeichnet, welche für das Management von Computerverbünden (Cluster) zuständig sind. Diese sorgen unter anderem dafür, dass Rechnerausfälle erkannt und auf Alternativsysteme umgeschaltet werden kann.

Eine weitere Voraussetzung für Apache Spark ist der Einsatz von Distributed Storage Systems, also Systemen, welche es erlauben, dass Daten auf mehreren Knotenpunkten gespeichert werden können. Beispiele für solche Systeme sind Apache Cassandra, welches von Facebook genutzt wird oder Couchbase welches von LinkedIn, PayPal und eBay genutzt wird.

### SQL (SparkSQL)

Bei Spark SQL handelt es sich um eine weitere Ebene von Apache Spark, welche auf Apache Core aufbaut. Spark SQL ermöglicht die Umwandlung von RDDs in Data Frames. Data Frames haben eine tabellenartige Struktur und werden von Spark SQL als temporäre Tabellen angelegt. Dies ermöglicht die Ausführung von SQL-Anfragen und somit die Durchführung von Selektionen, Projektionen, Joins, Gruppierungen und weiteren SQL-Operationen.

Spark SQL unterstützt Scala, Java Python und R. Um mit Spark SQL zu arbeiten, gibt es seit Spark 2.0 einen einheitlichen Einstiegspunkt für alle Spark Anwendungen, welcher als SparkSession bezeichnet wird.

```
from pyspark.sql import SparkSession

spark = SparkSession \
    .builder \
    .appName("Python Spark SQL basic example") \
    .config("spark.some.config.option", "some-value") \
    .getOrCreate()
```

**Abbildung 2: Erzeugung einer Spark Session in Python**

Ein enormer Vorteil bei der Nutzung von Spark SQL ist, dass auf verschiedene Datenquellen gleichzeitig zugegriffen werden kann, selbst wenn es sich dabei um unterschiedliche Systeme handelt. Dabei können aus verschiedenen Datenbanksystemen Daten innerhalb einer Tabelle zusammengefasst werden. Es werden diverse gängige Datenbanksysteme und Schnittstellen unterstützt. Dazu gehören Hive, Avro, Parquet, ORC, JSON, ODBC und JDBC.

```
spark.read.json(“jdbc://...“)
	.registerTempTable(“json“)

results = spark.sql(
	“““SELECT *
	FROM people
	JOIN json ...“““
)
```

**Abbildung 3: Einheitliche Datenabfrage mit Spark SQL**

Um die Geschwindigkeit von Abfragen zu erhöhen, verfügt Spark SQL über kostenbasierte Optimierungsfunktionen, einen spaltenbasierten Speicher und automatische Codegenerierung zur Erleichterung der Anwendung. Des Weiteren wird die Skalierung auf tausende von Knoten und mehrstündigen Abfragen geboten. Die hohe Fehlertoleranz von Spark SQL ermöglicht dabei den Verzicht auf weitere Softwarelösung zur Verarbeitung verloren gegangener oder zerstörter Daten.

### Maschine Learning (Mllib)

Die sogenannte MLlib von Apache Spark bietet Zugang zu einer großen Machine Learning (ML) Bibliothek. Der Vorteil gegenüber herkömmlichen ML Bibliotheken wie beispielsweise scikit-learn liegt in der Skalierbarkeit. Durch Apache Spark als Grundlage können die Vorteile der RDDs auch hier genutzt werden und riesige Datenmengen aus verschiedensten Quellen als Basis für Machine Learning Algorithmen verwendet werden.

Neben der Aggregation von Daten, welche durch Spark Core realisiert werden kann, bietet die ML-Bibliothek von Spark alles, was zur Umsetzung von ML-Projekten notwendig ist. Dies beginnt bei den verschiedenen Algorithmen zur Klassifikation, Regression oder dem Clustering. Diese Algorithmen funktionieren jedoch nur mit sauber aufbereiteten Daten doch auch dafür bietet die MLlib entsprechende Funktionen. Im Folgenden ist eine Abbildung dargestellt, auf welcher ein klassischer ML-Prozess abgebildet ist. Häufig wird dieser Prozess iterativ durchlaufen, solange, bis die gewünschte Modellqualität erreicht ist.

![image](https://user-images.githubusercontent.com/45334665/146560173-a3762714-af28-4bfe-86d5-1e04b9ad4996.png)

**Abbildung 4: Die Etappen eines Machine-Learning-Prozesses**

#### Featurization

Als Features werden im ML-Bereich die Spalten einer Tabelle genannt, welche als Trainingsgrundlage genutzt beziehungsweise auf welchen Vorhersagen getroffen werden sollen. Unter dem Begriff Featurization versteht man die Aufbereitung der Daten und Auswahl der Features (Feature Extraction), welche zum Trainieren des ML-Modells verwendet werden sollen. Bei der Klassifikation und der Regression müssen zusätzlich Zielvariablen gewählt werden, welche durch das ML-Modell vorhergesagt werden sollen. Zusätzlich müssen die Daten transformiert, in ihrer Dimensionalität reduziert und selektiert werden. Dies wird im nächsten Abschnitt „Pipelines&quot; erläutert.

#### Pipelines

Als Pipelines werden Workflows bezeichnet, welche die Schritte der Featurization automatisiert und sequenziell abarbeiten. Zunächst werden die Daten selektiert, es werden also jene Spalten ausgewählt, welche zum Trainieren genutzt werden sollen. Es ist sinnvoll dabei zunächst alle Daten zu wählen und im Nachhinein zu schauen, welche Daten wirklich zur Optimierung des ML-Algorithmus beitragen. Daten, welche keinen oder einen negativen Einfluss haben, werden aus den Daten entfernt, um die Dimensionen zu reduzieren und bessere Ergebnisse zu erhalten.

Anschließend müssen Daten häufig transformiert werden. Numerische Werte werden dabei beispielsweise auf einen Wertebereich von -1 bis 1 skaliert und alphabetische Werte werden dabei in Spalten umgewandelt, welche dann jeweils den Wert 0 oder 1 beinhalten.

#### Persistence

Neben dem Aufbereiten von Daten und dem Trainieren der entsprechenden ML-Modelle bietet Spark ML die Möglichkeit, Pipelines, Modelle und Algorithmen zu speichern und zu laden. So kann beispielsweise ein Algorithmus trainiert und das daraus resultierende Modell gespeichert und an anderer Stelle geladen und verwendet werden. Die Verwendung von vortrainierten Modellen ist gerade im Bereich des Deep Learning fest verankert, da das Training, je nach Datenmenge und Algorithmus, sehr viel Zeit beanspruchen kann.

#### Utilites

Über die erläuterten Kernkomponenten hinaus bietet Spark ML noch einige Utility Funktionen, um Statistiken zu erzeugen oder Daten handzuhaben.

### Graphdatenbanken (GraphX)

### Streaming (Spark Streaming)

## Quellen

[https://datasolut.com/was-ist-spark/](https://datasolut.com/was-ist-spark/)

[https://en.wikipedia.org/wiki/Distributed\_data\_store](https://en.wikipedia.org/wiki/Distributed_data_store)

[https://de.wikipedia.org/wiki/Cluster\_Manager#:~:text=Ein%20Cluster%20Manager%20ist%20eine,Fehlerfall%20sowie%20Switchover%20für%20Wartungszwecke](https://de.wikipedia.org/wiki/Cluster_Manager#:~:text=Ein%20Cluster%20Manager%20ist%20eine,Fehlerfall%20sowie%20Switchover%20f%C3%BCr%20Wartungszwecke).

[https://spark.apache.org/docs/latest/ml-guide.html](https://spark.apache.org/docs/latest/ml-guide.html)

[https://www.heise.de/select/ix/2017/5/1492971380429106](https://www.heise.de/select/ix/2017/5/1492971380429106)
