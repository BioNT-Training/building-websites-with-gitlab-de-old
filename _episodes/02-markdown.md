---
title: Verfassen mit Markdown
teaching: 0
exercises: 0
questions:
- How can I write content for my webpages?
- How do I link to other pages?
objectives:
- create simple pages of formatted text
keypoints:
- Markdown is an relatively easy way to write formatted text
- Markdown and HTML tags can be used together in a single page
- I recommend writing Markdown links 'reference-style'
- The landing page for a website is conventionally named `index.md`
---


# Markdown
Markdown ist eine leichtgewichtige Auszeichnungssprache, d.h. eine Konvention zum
Hinzufügen von Stilinformationen zu Textinhalten. Wie der Name Markdown schon sagt, sind
die Syntaxelemente dieser Sprache auf ein Minimum reduziert. Mit einer eher
minimalistischen Syntax ist in Markdown formatierter Text vergleichsweise gut lesbar.
Dies mag ein Grund dafür sein, dass Markdown die Sprache der Wahl für formatierte
Benutzereingaben auf Websites wie z. B.:
- [Stack Exchange](https://stackexchange.com/)
- [GitLab](https://about.gitlab.com/)
- [GitHub](https://github.com/).

# Where to Start Writing Markdown?
Es gibt eine Vielzahl von Tools zum Rendern von Markdown-Quellcode. Rendering ist der
Prozess der Erzeugung einer schönen Ansicht des Inhalts unter Verwendung der im
Quelltext enthaltenen Stilinformationen. Die Chancen stehen gut, dass Ihr Editor dies
kann. Da wir auf die Erstellung von Websites mit GitLab-Seiten hinarbeiten, werden wir
GitLab gleich zum Erlernen der Grundlagen von Markdown verwenden. Das GitLab-Projekt,
das Sie in der letzten Folge erstellt haben, enthält eine Datei `README.md`. Klicken Sie
auf den Dateinamen, um sie zu öffnen.

Das Bild unten zeigt die Standardansicht. Diese Ansicht enthält eine gerenderte Ansicht
des Inhalts der Datei `README.md`, wie die auf unserer Projekthomepage.

![README preview](../fig/gitlab_readme.png){: .image-with-shadow width="900px" }

Mit den Schaltflächen auf der rechten Seite können Sie mit der Datei und der
Visualisierung interagieren. Mit den ersten beiden Schaltflächen, den Schaltflächen mit
den Symbolen, können Sie zwischen `Display source` und `Display rendered file`
umschalten. Fahren Sie mit der Maus darauf, um diese beiden Meldungen in Tooltips
anzuzeigen. Die Quelle ist die nicht gerenderte Ansicht unserer Datei. Wir können sie
über die blaue Schaltfläche `Edit` bearbeiten. Klicken Sie ihn an.

![Bearbeitungsoberfläche der Gruppen-Websites
README-Datei](../fig/gitlab_edit_readme.png){: .image-with-shadow width="900px" }

Wir können den Inhalt ändern und einen Blick auf die gerenderte Ansicht werfen, indem
wir oben auf den Reiter `Preview` klicken.

![Vorschau auf den gerenderten Inhalt der README-Datei der
Gruppen-Websites](../fig/gitlab_edit_readme_preview.png){: .image-with-shadow
width="900px" }

Fügen wir `Some **bold** font` hinzu und sehen wir uns an, was passiert, wenn wir die
Vorschau auf der Registerkarte Vorschau verwenden. Was ist mit der fetten Welt passiert?

Um den Inhalt in der Datei `README.md` zu speichern, sollten wir auf die Schaltfläche
`Commit changes` am unteren Ende der Seite klicken. Bitte beachten Sie, dass es sich
hierbei nicht um eine einfache Schaltfläche "Speichern" handelt, sondern um eine
tatsächliche Übertragung. Diese Version des Projekts wird in Git unter dem Namen `Commit
message` gespeichert, den Sie hier im Commit-Menü angeben, und in dem Zweig, den Sie als
`Target branch` festlegen. Wir haben im Moment nur den Hauptzweig - also ist diese Wahl
offensichtlich - und die Commit-Nachricht wird mit dem Namen der Datei, die Sie gerade
bearbeitet haben, vorkompiliert. Vielleicht möchten Sie in Ihrer Commit-Nachricht
genauer sein, aber für den Moment nehmen wir die vorgegebene Option. Übertragen Sie
diese Änderung.

> ## Schreiben einer Commit-Nachricht
> 
> Eine Commit-Nachricht ist ein kurzer, beschreibender und spezifischer Kommentar, der
> uns später helfen wird, uns daran zu erinnern, was wir getan haben und warum. Mehr
> über das Schreiben von Commit-Nachrichten finden Sie in [diesem
> Abschnitt](https://swcarpentry.github.io/git-novice/04-changes/index.html) der
> Git-novice Lektion.
> 
{: .callout}

![Nach dem Übertragen von README-Änderungen](../fig/gitlab_readme_committed.png){:
.image-with-shadow width="900px" }

Die Schnittstelle leitet Sie auf die Hauptseite des Projekts um. Oben steht eine
Meldung: "Ihre Änderungen wurden erfolgreich übertragen." Unsere Änderungen wurden in
die README-Datei aufgenommen, die nun die zweite Zeile mit der fetten Schrift zeigt.

# Markdown schreiben

Nachdem wir nun die Bearbeitungsoberfläche und die Vorschauregisterkarte unseres
Projekts `README.md` kennen, können wir es als Texteditor verwenden und ausgewählte
Markdown-Funktionen untersuchen.

Unser `README.md` enthält bereits Text und zwei Formatierungsfunktionen:
- Überschrift `# group-website`
- Hervorhebung durch `**bold**`.

Lassen Sie uns etwas mehr Markdown lernen, indem wir einige Formatierungen hinzufügen
und sehen, was passiert, wenn wir die Vorschau auf der Registerkarte "Vorschau"
verwenden. Fügen Sie das Folgende zu Ihrer `README.md` Datei hinzu.

~~~
# group-website
Repo for learning how to make websites with GitLab pages

## Learning Markdown

Vanilla text may contain *italics* and **bold words**.

This paragraph is separated from the previous one by a blank line.
Line breaks
are caused by two trailing spaces at the end of a line.

[Carpentries Webpage](https://carpentries.org/)

### Carpentries Lesson Programs:
- Software Carpentry
- Data Carpentry
- Library Carpentry
~~~
> 
{: .language-markdown }

Sie können dann erneut auf die Registerkarte "Vorschau" klicken, um zu sehen, wie die
Formatierung wiedergegeben wird.

![Vorschau auf die Formatierung in der README](../fig/gitlab_learning_markdown.png){:
.image-with-shadow width="900px" }

> ## Markdown Trailing Spaces Are Meaningful
> 
> In dem obigen Beispiel gibt es zwei Leerzeichen am Ende von `Line breaks `. Diese
> leiten einen sogenannten **harten Zeilenumbruch** ein, der bewirkt, dass der Absatz in
> der nächsten Zeile fortgesetzt wird, indem dem generierten HTML ein `<br/>`
> hinzugefügt wird.
> 
> Wenn Sie die Zeile in einer Markdown-Datei umbrechen, aber die beiden Leerzeichen am
> Ende nicht einfügen, wird der generierte HTML-Code in der gleichen Zeile fortgesetzt,
> **ohne** ein `<br/>` einzufügen. Dies wird **weicher Zeilenumbruch** genannt.
> 
> In einigen Fällen kann es vorkommen, dass **weiche Zeilenumbrüche** ein `<br/>`
> einführen. Dies kann passieren, wenn Sie verschiedene [markdown
> flavors](#markdown-flavours) verwenden. {: .language-markdown }
> 
{: .callout}

Sie können diese Änderungen übertragen, um sie zu speichern. Aber zuerst machen wir eine
Übung, um das Schreiben von mehr Markdown auszuprobieren.

> ## Übung: Ausprobieren von Markdown
> Verwenden Sie [dieses Cheatsheet][gitlab-flavored-markdown], um das Folgende zu Ihrem
> `README.md` hinzuzufügen:
> 
> - Eine weitere Überschrift der zweiten Ebene
> - Etwas Text unter dieser Überschrift der zweiten Ebene, der einen Link und
>   ~~durchgestrichenen~~ Text enthält.
> - Eine Überschrift der dritten Ebene
> - Eine nummerierte Liste
> - Bonus: Dieses Bild hinzufügen
>   <https://github.com/carpentries/carpentries.org/blob/main/images/TheCarpentries-opengraph.png>
> 
> > ## Beispiellösung
> > Ihr Markdown könnte zum Beispiel wie folgt aussehen:
> > ~~~
> > ## More info on the lesson
> > You can find this lesson [here](https://grp-bio-it-workshops.embl-community.io/building-websites-with-gitlab/).
> > 
> > ### Four reasons you should learn Markdown:
> > 
> > 1. Less formatting than HTML
> > 2. Easy to read even with formatting
> > 3. Commonly used for websites and software development
> > 4. We ~~don't~~ use it in The Carpentries
> > 
> > ![Carpentries Logo](https://github.com/carpentries/carpentries.org/raw/main/images/TheCarpentries-opengraph.png)
> > ~~~
> > {: .language-markdown }
> > 
> > 
> > 
> {: .solution }
> 
{: .challenge }


> ## Referenz-Stil Links
> 
> Bisher haben wir _inline-style_ Links verwendet, bei denen die URL inline mit dem
> Beschreibungstext steht, zum Beispiel:
> 
> ~~~
> [Carpentries Webpage](https://carpentries.org/)
> ~~~
> {: .language-markdown }
> 
> Wenn Sie einen Link mehr als einmal verwenden, sollten Sie stattdessen so genannte
> _reference-style_ Links verwenden. Links im Verweis-Stil verweisen auf die URL über
> ein Label. Das Label wird in eckige Klammern `[ ]` direkt nach dem Beschreibungstext
> des Links gesetzt und später, normalerweise am Ende der Seite, können Sie dieses Label
> mit der URL verbinden, auf die es verweist, um den Link zu vervollständigen. Das sieht
> dann so aus:
> ~~~
> [Carpentries Webpage][carpentries]
> 
> [carpentries]: https://carpentries.org/
> ~~~
> {: .language-markdown }
> 
{: .callout}

Im weiteren Verlauf der Lektion werden wir Markdown verwenden und mehr darüber lernen.
Unabhängig davon, ob Sie sich dafür entscheiden, Ihre Website mit Markdown-basierten
Technologien oder mit HTML zu strukturieren, müssen Sie dennoch einige Grundlagen von
Markdown beherrschen, um Ihre README-Datei zu bearbeiten. Die README-Datei ist ein
wichtiger Leitfaden - der auf der Startseite Ihres Projekts angezeigt wird - für Ihre
Mitarbeiter und auch für Sie, um zu verstehen, worum es in dem Projekt geht und wie Sie
dazu beitragen können.

> ## Markdown Flavours
> Die anfängliche Beschreibung von Markdown war informell und enthielt gewisse
> Unklarheiten, so dass im Laufe der Jahre [verschiedene Markdown-Implementierungen und
> Syntax-Variationen](https://github.com/commonmark/commonmark-spec/wiki/markdown-flavors)
> (oft als "Flavours" bezeichnet) erschienen, um verschiedene Syntax-Merkmale und
> Erweiterungen zu unterstützen. Dies hat zur Folge, dass die Syntax einer Variante in
> einer anderen möglicherweise nicht wie erwartet interpretiert wird - man muss sich
> also bewusst sein, welche Variante von einer bestimmten Plattform verwendet wird. Hier
> sind ein paar bekannte Varianten:
>   - [GitLab-flavored Markdown][gitlab-flavored-markdown] (verwendet in dieser Lektion
>     und von GitLab)
>   - [GitHub-flavored Markdown][github-flavored-markdown] (von GitHub verwendet)
>   - [Kramdown][kramdown] (eine schnelle, Ruby, Open-Source-Implementierung, die unter
>     der MIT-Lizenz veröffentlicht wurde)
> 
> Mardown ist auch die Sprache der Plattform für kollaborative Notizen, die am EMBL
> verfügbar ist. Sie können darauf [hier] zugreifen (https://pad.bio-it.embl.de/). Die
> Plattform basiert auf [CodiMD](https://github.com/hackmdio/codimd).
> 
{: .callout}

> ## Übung: Fügen Sie Ihre Repository-Details zu CodiMD hinzu
> 
> Verwenden Sie die Markdown-Syntax, um einen Link in das Dokument mit den gemeinsamen
> Notizen einzufügen, das Sie verwenden, um dieser Lektion zu folgen. Der Linktext
> sollte Ihr GitLab-Benutzername und das Ziel Ihr Repository sein.
> 
{: .challenge }

[kramdown]: https://kramdown.gettalong.org/
[gitlab-flavored-markdown]: https://docs.gitlab.com/ee/user/markdown.html
[github-flavored-markdown]:
https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

{% include links.md %}

