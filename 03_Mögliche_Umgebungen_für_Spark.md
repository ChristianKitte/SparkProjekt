#### [Zum Anfang](README.md "Hier gelangen Sie zur Startseite") | [Inhaltsverzeichnis](00_Inhaltsverzeichnis.md "Hier gelangen Sie zum Inhaltsverzeichnis")

# 3 Mögliche Umgebungen für Spark

## Spark in der Cloud (Amazon, Google, Azure, ..., Databrick) D

## Spark lokal A

## Spark mit Google Colaboratory (Colab) A

## Spark mit Docker C

Spark mit Docker bietet eine weitere einfache Möglichkeit, um Docker auf einen lokalen Rechner verfügbar zu machen. In
diesen Abschnitt wird gezeigt, wie mit Hilfe von Docker eine in _Jupyter Notebook_ verfügbare Sparkumgebung angelegt
werden kann.

Bei Docker arbeitet man mit sogenannten Containern, welche einen Prozess visualisieren. Die Basis eines Containers
bildet ein Image. Ein gute Einführung zu Docker findet sich auf den Seiten von
[Docker](https://docs.docker.com/get-started/overview/ "Hier gelangen Sie zur Homepage von Docker").

Einer der Vorteile von Docker ist die sehr große Sammlung bereits fertiger Images
im [Docker Hub](https://hub.docker.com/
"Hier gelangen Sie zum Portal von Docker Hub"). Hier finden sich für viele Anwendungsfälle bereits vorgefertigte
Lösungen.

Unabhängig von Spark ist für die Ausführung eines Docker Containers die Installation einer Docker Runtime notwendig.
Diese ist in Form eines _Docker Desktop_ für die Plattformen Mac, Windows und Linux verfügbar. Die Installation von
Docker ist nicht Teil dieser Arbeit, jedoch findet sich eine gute Einführung
auf [Docker](https://docs.docker.com/get-started/overview/ "Hier gelangen Sie zur Homepage von Docker").

### Dockerimage

Als Basis dient das [_Jupyter Notebook Python, Spark
Stack_](https://hub.docker.com/r/jupyter/pyspark-notebook "Hier gelangen Sie zum Image im Docker Hub")
Notebook. Es beinhaltet ein fertig konfiguriertes Linux System mit installierten Java, Python und Spark. Es ist also
nicht nötig, manuelle Einstallungen oder Installationen auszuführen, um Spark innerhalb eines [_Jupyter
Notebooks_](https://jupyter.org/index.html "Hier gelangen Sie zur Homepage von Jupyter") auszuführen.

### Download und erster Start

Dieser Schritt setzt die Installation des _Docker Desktop_ wie oben beschrieben voraus. In einer Eingabekonsole wird der
folgende Befehl eingegeben:

    docker run -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes --name pyspark jupyter/pyspark-notebook

Bei der ersten Ausführung wurde das Image _jupyter/pyspark-notebook_ noch nicht vom Docker Hub herunter geladen. Daher
erfolgt bei der erstmaligen Ausführung der Download des Images. Anschließend wird auf Basis des heruntergeladenen Image
ein Container erstellt. Dieser Container horcht auf dem Port 8888
und [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/
"Hier gelangen Sie zur Dokumentation von JupyterLab") ist aktiv. Der Name des erstellten Containers lautet pyspark.

### Zugriff auf das Jupyter Notebook

### Vor- und Nachteile
