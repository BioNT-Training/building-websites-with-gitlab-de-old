---
title: GitLab-Seiten mit Jupyter-Büchern
teaching: 0
exercises: 0
questions:
- How do I publish web pages through GitLab and Jupyter books?
objectives:
- Publish Jupyter notebooks as HTML on the web with GitHub Pages
keypoints:
- Through Jupyter books, you'll be able to integrate interactive components and code
  in your web pages
---


Lassen Sie uns etwas anderes machen, das ein wenig vertrauter klingt, wenn Sie mit den
[Jupyter](https://jupyter.org/) Projekten vertraut sind. Von deren Website:
> Das Projekt Jupyter dient der Entwicklung von Open-Source-Software, offenen Standards
> und Diensten für interaktives Rechnen in Dutzenden von Programmiersprachen.

**Jupyter-Notizbücher** ermöglichen es Ihnen, Dokumente zu erstellen und auszutauschen,
die sowohl Live-Code als auch erzählenden Text enthalten. **Jupyter Lab** erweitert ihre
Funktionalitäten durch die Schaffung einer interaktiven Entwicklungsumgebung (die es
Ihnen ermöglicht, in Ihrem Dateisystem zu navigieren und die Codierungsumgebung zu
definieren). **Jupyter Hub** ist eine Mehrbenutzerversion von Jupyter Lab, die
Institutionen lokal implementieren können ([wie wir am
EMBL](https://jupyterhub.embl.de/)).

Und **Jupyter-Buch**?
> Jupyter Book ist ein Open-Source-Projekt zur Erstellung von schönen,
> publikationsreifen Büchern und Dokumenten aus Berechnungsmaterial.

Das [ausführliche Tutorial](https://jupyterbook.org/start/your-first-book.html) wird Sie
durch die Installationsschritte und die detaillierten Anpassungsmöglichkeiten führen, im
Rahmen dieser Lektion werden wir nur die Grundlagen behandeln. Das Wichtigste zuerst:
Installieren wir Jupyter Book. In Ihrem Terminal:

~~~
pip install -U jupyter-book
~~~
> 
{: .language-bash }

Bitte beachten Sie: Sie müssen auch **pip** installiert haben. Lassen Sie uns nun unser
erstes Buchprojekt erstellen. Der Befehl `jupyter-book --help` würde uns dabei helfen,
die Optionen zu überprüfen, aber diese Lektion wird etwas spoilern: die

~~~
jupyter-book create jupyter-book-demo
~~~
> 
{: .language-bash }

Befehl erstellt ein einfaches Jupyter-Buch in einem `jupyter-book-demo`-Ordner. Dieser
Ordner enthält bereits die drei Dinge, die zum Erstellen eines Buches benötigt werden:
eine `_config.yml`-Datei, ein `_toc.yml`-Inhaltsverzeichnis und den Inhalt des Buches in
einer Sammlung von MarkDown-, reStructuredText- oder Jupyter Notebook-Dateien.

Da wir von der ganzen Entwicklung und Bereitstellung müde sind, wollen wir nicht
wirklich etwas am Inhalt ändern, aber wir priorisieren stattdessen, dass er in GitLab
läuft. Raten Sie mal, was wir hinzufügen müssen? In der Tat eine `.gitlab-ci.yml`-Datei.

~~~
pages:
  stage: deploy
  image: python:slim
  script:
    - pip install -U jupyter-book
    - jupyter-book clean .
    - jupyter-book build .
    - mv _build/html public
  artifacts:
    paths:
      - public
~~~
> 
{: .language-yaml }

Dieser Teil des Codes:
1. Installiert jupyter-book (oder prüft, ob es korrekt installiert ist).
2. Säubert den Ordner von Dateien, die von (eventuellen) früheren Builds stammen.
3. führt den Befehl `jupyter-book build .` aus, der das Buch im Ordner in einem
   Unterordner `_build` erstellt. Sie können die Ausgabe überprüfen, indem Sie den
   gleichen Befehl in Ihrem Terminal ausführen, und Sie werden feststellen, dass sich
   die eigentlichen HTML-Dateien im Unterordner `_build/html` befinden.
4. Es verschiebt dann den HTML-Inhalt in unseren üblichen `public`-Ordner, wo die
   Artefakte gespeichert sind.

> ## Deine Zeit zum Experimentieren mit einer Vorlage
> Diese Vorlage ist absichtlich minimal gehalten, um Ihnen die Möglichkeit zu geben,
> Ihre Fähigkeiten beim Lesen der Dokumentation zu testen. Schauen Sie sich die
> Themenleitfäden auf [jupyterbook.org](https://jupyterbook.org/intro.html) an und
> finden Sie einen Weg, um:
> 1. Fügen Sie eine weitere Seite mit dem Namen "Über" hinzu, die mit dem
>    Inhaltsverzeichnis verlinkt ist.
> 2. Spielen Sie mit dem Dateiformat dieser neuen Seite, fügen Sie die gleiche Art von
>    Inhalt in den Formaten MarkDown, reStructuredTex und Notebook hinzu.
> 3. Füge eine Abbildung und eine Bildunterschrift hinzu.
> 4. Fügen Sie eine Codezelle ein. Wenn Sie mit einer Programmiersprache vertraut sind,
>    fügen Sie einen einfachen Plot ein und visualisieren Sie die Ausgabe dieses Plots
>    in Ihrer Seite.
> 5. Für weitere fortgeschrittene Code-Funktionen, siehe [how to make the code
>    executable](https://jupyterbook.org/interactive/thebe.html)
> 6. Schauen Sie in der [Galerie der
>    Jupyter-Bücher](https://executablebooks.org/en/latest/gallery.html) nach, um sich
>    inspirieren zu lassen!
> 
{: .challenge}



