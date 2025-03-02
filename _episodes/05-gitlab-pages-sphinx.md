---
title: GitLab-Seiten mit Sphinx
teaching: 0
exercises: 0
questions:
- How do I publish web pages through GitLab and Sphinx?
objectives:
- Publish reStructuredText files as HTML on the web with GitHub Pages
keypoints:
- Through Sphinx, GitLab serves pages are generated from `.rst` files
---


[Sphinx](https://www.sphinx-doc.org/en/master/) ist ein Werkzeug zur Generierung von
Webseiten oder PDF, das hauptsächlich für die Erstellung einer Projektdokumentation
entwickelt wurde. Es wurde ursprünglich für die Python-Dokumentation entwickelt, verfügt
aber über ausgezeichnete Möglichkeiten für die Dokumentation von Softwareprojekten in
einer Reihe von Sprachen. Polyglotte Dokumentationssysteme können sehr nützlich sein,
wenn Ihr Projekt an Komplexität oder Anzahl der Mitarbeiter zunimmt, also beachten Sie
dies.

In diesem Kapitel der Lektion werden wir die Programmiersprache Python verwenden. Auch
wenn dies nicht unbedingt notwendig ist, empfehlen wir Ihnen, sich mit Python vertraut
zu machen, da die Erklärung dieser Sprache nicht Gegenstand dieser Lektion ist. Sie
können dies tun, indem Sie die Lektion [Programmieren mit Python]
(https://swcarpentry.github.io/python-novice-inflammation/) durcharbeiten.

> ## Übung: Dokumentation
> Lassen Sie in einer Gruppe jedes Mitglied die Dokumentation eines der folgenden Pakete
> öffnen
> - [pytest](https://docs.pytest.org/en/latest/)
> - [seaborn](https://seaborn.pydata.org/)
> - [numpy](https://docs.scipy.org/doc/numpy/reference/)
> - [scipy-cookbook](https://scipy-cookbook.readthedocs.io/)
> - [scikit-learn](http://scikit-learn.org/stable/)
> 
> Diskutieren Sie, was die gemeinsamen Komponenten sind, was an diesen
> Dokumentations-Sites hilfreich ist, wie sie die allgemeinen Konzepte zur Dokumentation
> ansprechen, wie sie sich ähneln und wie sie sich unterscheiden.
> 
{: .challenge}

Während Jekyll Markdown-Dateien (`.md`) in HTML konvertiert, konvertiert Sphinx
reStructureText-Dateien (`.rts`). Obwohl diese beiden Formate auf den ersten Blick sehr
ähnlich erscheinen, wurden sie für zwei unterschiedliche Zwecke entwickelt: Markdown zum
Schreiben für das Web, reStructuredText zum Schreiben von Dokumentation. [In diesem
Blogbeitrag (https://www.zverovich.net/2016/06/16/rst-vs-markdown.html) erfahren Sie
mehr darüber, was das in der Praxis bedeutet. Der wichtigste Punkt, den wir in diesem
Zusammenhang hervorheben möchten, ist, dass reStructuredText auch für die Konvertierung
in PDF gut geeignet ist. Das macht es zu einem nützlichen Werkzeug auch für die
Entwicklung von Dokumenten, die Sie sowohl online als auch in Papierform benötigen, z.B.
Schulungsunterlagen oder eine Meeting-Agenda.

> ## Sphinx-Schnellstart
> Aus Gründen der Übersichtlichkeit werden sich die nächsten Schritte dieses Kapitels
> nur auf die Sphinx-Dateien konzentrieren, die für die Erzeugung von HTML-Dateien
> relevant sind. Durch die lokale Installation von Sphinx können Sie jedoch den
> Quickstart-Befehl ausführen, um ein grundlegendes Sphinx-Projekt zu starten. Wir
> empfehlen diese Option, wenn Sie Ihr Verständnis für das Dokumentieren mit Sphinx
> vertiefen möchten. Zu diesem Zweck berichten wir hier über die notwendigen Schritte.
> 
> Auf Ihrem System ist Sphinx wahrscheinlich bereits installiert. Prüfen Sie, ob dies
> der Fall ist, indem Sie in Ihrem Terminal eingeben:
> 
> ~~~
> sphinx-build --version
> ~~~
> {: .language-bash }
> 
> Wenn das nicht der Fall ist, können Sie die Installation durch Eingabe von:
> 
> ~~~
> pip install -U sphinx
> ~~~
> {: .language-bash }
> 
> Oder lesen Sie die detaillierten Installationsanweisungen
> [hier](https://www.sphinx-doc.org/en/master/usage/installation.html). Sobald Sphinx
> installiert ist, können wir den Quickstart-Befehl ausführen, um einen Überblick über
> den minimalen Satz an Dateien zu erhalten, die zur Erstellung der Dokumentation
> erforderlich sind. Mit dem folgenden Befehl wird ein leeres Repository erstellt und
> der Befehl dort ausgeführt:
> 
> ~~~
> mkdir sphinx-quickstart-test
> cd sphinx-quickstart-test
> sphinx-quickstart
> ...
> Separate source and build directories (y/n) [n]:
> ...
> Project name: My project
> Author name(s): <Your name>
> Project release []:
> ...
> Project language [en]:
> ~~~
> {: .language-bash }
> 
> Es werden mehrere Dokumente erzeugt. Hier ein Überblick:
> 
> ![Sphinx quickstart](../fig/sphinx-quickstart.png){: .image-with-shadow width="600px"
> }
> 
> Die Dateien, die für uns in diesem Zusammenhang relevant sind, sind die
> `index.rst`-Datei - das ist das Äquivalent zu unserer `index.md`-Datei im Beispiel mit
> Jekyll - und die `conf.py`-Datei. Deshalb werden in dieser Lektion auch nur diese
> beiden Dateien behandelt.
> 
{: .callout}

Erstellen Sie einen leeren Projektordner. Lassen Sie uns unsere `index.rst`-Datei im
Stammordner unseres Projekts initialisieren.

~~~
.. this is a comment, it is not rendered

Sphinx Example Project's documentation
======================================

Contents:

.. toctree::
    :maxdepth: 2
~~~
> 
{: .language-markdown }

Es meldet die Hauptüberschrift unseres Projekts, und dann ein Inhaltsverzeichnis durch
den "TOC-Baum". Es kann eine numerische Option maxdepth angegeben werden (wir haben sie
auf 2 gesetzt), um die Tiefe des Baums anzugeben; standardmäßig werden alle Ebenen
einbezogen. Mehr über den Toc-Baum unter [dieser
Link](https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html). Kurz
gesagt, wenn wir *.rst-Dateien zu unserem Inhaltsverzeichnis hinzufügen, sollten sie
hier aufgeführt werden. Fügen wir eine Datei hinzu, um zu sehen, wie das funktioniert.

Erstellen Sie eine Datei `about.rst`, ebenfalls im Hauptstammordner, mit dem Inhalt:

~~~
About
=====

Hello, this is the about page of my project.
~~~
> 
{: .language-markdown }

Nun fügen wir diese Datei dem TOC-Baum hinzu, indem wir die Datei `index.rst`
bearbeiten:

~~~
.. this is a comment, it is not rendered

Sphinx Example Project's documentation
======================================

Contents:

.. toctree::
    :maxdepth: 2

    about.rst
~~~
> 
{: .language-markdown }

Das war's: Unsere Homepage (die mit der Datei `index.rst` erzeugt wurde) verlinkt nun
auf die Über-Seite (`about.rst`). Als nächstes schreiben wir eine minimale `conf.py`
Datei, ebenfalls im Stammverzeichnis.

~~~
# -- Project information -----------------------------------------------------

project = 'My project'
copyright = '2021, <Your name>'
author = '<Your name>'
release = '1.0'

# -- Options for HTML output -------------------------------------------------

html_theme = 'alabaster'
~~~
> 
{: .language-bash }

Eine vollständige Liste der Optionen, die in dieser Datei angegeben werden können,
finden Sie in der
[documentation](https://www.sphinx-doc.org/en/master/usage/configuration.html).

> ## Sphinx-Schnellstart
> Auch hier hilft es Ihnen, wenn Sie Sphinx lokal installiert haben, um die nächsten
> Schritte durchzuführen. In der Tat können Sie Ihre Dokumentations-Website lokal mit
> dem Befehl `sphinx-build . build/` erstellen, der in Ihrem Stammverzeichnis ausgeführt
> wird. Nach der Ausführung wird Ihre Ausgabewebsite im Ordner `build/` erstellt. Sie
> können sie einfach visualisieren, indem Sie die Datei `index.html` in Ihrem
> Lieblingsbrowser öffnen.
> 
{: .callout}

Auch in diesem Fall ist die Datei `.gitlab-ci.yml` erforderlich, um Anweisungen für die
Bereitstellung in GitLab anzugeben. Füllen Sie sie mit:

~~~
pages:
  stage: deploy
  image: python:3.6
  script:
    - pip install -U sphinx
    - sphinx-build -b html . public
  artifacts:
    paths:
      - public
~~~
> 
{: .language-yaml }

Dieses Skript: gibt den Container für unsere Pipeline an (Python, Version 3.6),
installiert Sphinx durch [Pip](https://pypi.org/project/pip/), führt den Befehl
`sphinx-build` aus - der HTML-Dateien im Stammordner (`.`) in einen `public`-Ordner
baut, den es ebenfalls erstellt. Schließlich gibt er an, wo die HTML-Artefakte zu finden
sind (in der Tat im Ordner `public`).

Das war's schon. Jetzt sollten wir noch einmal dem Abschnitt "Einrichten eines Projekts"
in der [Einführung]
(https://grp-bio-it-workshops.embl-community.io/building-websites-with-gitlab/01-introduction/index.html)
folgen, um ein entferntes Projekt in GitLab einzurichten, und es als entfernt für
unseren lokalen Ordner mit `git remote add origin <git URL>`, `git add . && git commit
-m <message>` und dann `git push -u` festlegen. Überwachen Sie schließlich die
Ausführung Ihrer Pipeline und prüfen Sie das Endergebnis.

{% include links.md %}

