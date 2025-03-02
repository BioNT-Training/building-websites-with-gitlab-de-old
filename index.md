---
layout: lesson
root: .
permalink: index.html
---


> ## Voraussetzungen
> Vor der Teilnahme an dieser Lektion sollten die Lernenden idealerweise in der Lage
> sein:
> 
> 1. ein Projekt auf [GitLab][gitlab] / [EMBL GitLab][embl-gitlab] erstellen.
> 1. Klonen einer lokalen Kopie eines Projekts mit Git, Hinzufügen und Übertragen
>    geänderter Dateien und Push/Pull von Änderungen zwischen lokalen und entfernten
>    Repositories.
> 1. Befehle in der Shell ausführen.
> 
> Keine der oben genannten Voraussetzungen ist absolut notwendig, um der Lektion zu
> folgen. Sie werden jedoch benötigt, um die Entwicklung der Website von Ihrem Laptop
> aus effizient zu verwalten und zu testen, wie sie aussieht, bevor Sie offizielle
> Versionen erstellen.
> 
> Wenn Sie eine der oben aufgeführten Fähigkeiten erlernen möchten, sind die [Software
> Carpentry][swc]-Lektionen über [die Shell][swc-shell] und [Git][swc-git] ein guter
> Anfang.
> 
{: .prereq }

Für diejenigen, die bereits mit den Möglichkeiten von Git und einer Online-Plattform wie
GitLab oder GitHub vertraut sind, um Änderungen an flachen Textdateien zu verfolgen und
zu vergleichen und mit anderen an Projekten zusammenzuarbeiten, bieten __GitLab__ (und
GitHub) __Pages__ eine kostenlose Möglichkeit, Webseiten zu erstellen und zu hosten.
Dieser Ansatz wird häufig für die Dokumentation von Softwareprojekten und für die
Erstellung von Blogs und Websites für Einzelpersonen und Organisationen verwendet, die
bereits mit dem Git-Toolset für ihre anderen Projekte arbeiten. Für diejenigen, die sich
zum ersten Mal mit der Erstellung solcher Websites befassen, kann der Prozess jedoch
verwirrend und einschüchternd sein. Dieses Tutorial soll dies beheben, indem es
1. eine Schritt-für-Schritt-Anleitung zur Erstellung einer Sammlung von Seiten,
1. zeigt mehrere Beispiele, wie man sie zu einer kohärenten Site strukturieren kann,
1. Demonstration der Verwendung verschiedener Frameworks für die Entwicklung von
   Webseiten, von einfachem _HTML_ bis _Jekyll_ und _Sphinx_.

Der Unterschied zwischen der Entwicklung von GitLab- und GitHub-Seiten wird ebenfalls
kurz besprochen.

> ## Veraltete Screenshots
> 
> In dieser Lektion werden wir Inhalte und Screenshots von [git.embl.de]
> (https://git.embl.de/) verwenden und zeigen. Als sich ständig weiterentwickelnde
> Plattform fügt GitLab seiner Website ständig neue Funktionen und neue visuelle
> Elemente hinzu. **Screenshots** in der Lektion können dann nicht mehr synchron sein,
> auf Inhalte verweisen oder diese zeigen, die nicht mehr existieren.
> 
> Wenn Sie während der Lektion **Screenshots** finden, die nicht mehr mit dem
> übereinstimmen, was Sie in Ihrem Browser sehen, [öffnen Sie bitte ein
> Problem](https://git.embl.de/grp-bio-it-workshops/building-websites-with-gitlab/-/issues),
> das beschreibt, was Sie sehen und wie es sich vom Inhalt der Lektion unterscheidet.
> Fügen Sie bitte so viele Screenshots wie nötig hinzu, um die Diskrepanz zu
> verdeutlichen.
> 
{: .callout }

> ## Lernziele
> 
> Nach dieser Lektion werden die Lernenden in der Lage sein:
> 
> - __erstelle__ formatierten Seiteninhalt mit _HTML_ oder _Markdown_
> - __configure__ their project to build and serve pages on GitLab
> - __build__ eine einfache Seite, um Inhalte in einfachem _HTML_ zu hosten
> - __erstelle__ eine kohärente Site mit mehreren Seiten unter Verwendung des _Jekyll_
>   oder _Sphinx_ Frameworks
> - __anpassen__ des Layouts und Stils der Seiten auf ihrer Website
> 
{: .objectives }

[gitlab]: https://gitlab.com/
[embl-gitlab]: https://git.embl.de/

{% include links.md %}

