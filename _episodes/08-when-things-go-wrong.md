---
title: Wenn etwas schief geht
teaching: 0
exercises: 0
questions: How do I troubleshoot errors in the GitLab pipelines?
objectives:
- Get feedback from GitLab about why a pipeline failed
keypoints:
- If a pipeline fails, GitLab will provide you useful feedback on why
---



## Wenn etwas schief geht

Bis jetzt haben wir gesehen, wie man erfolgreich verschiedene Technologien zur
Erstellung einer Website einsetzt. Es gibt jedoch einige Situationen, in denen dies
aufgrund eines Tippfehlers oder fehlender Informationen nicht möglich ist. Wir werden
einen dieser Fälle anhand eines Jekyll-Beispiels durchgehen.

> ## Übung: Fehlersuche in Jekyll
> 
> Diese Übung soll Ihnen helfen zu erkennen, wie häufige Fehler bei der Arbeit mit
> diesen Elementen einer Jekyll-Website aussehen.
> 
> Bearbeiten Sie Ihre `_config.yml` Datei und ersetzen Sie ein `:` durch ein `=` Zeichen
> in einer der Variablen.
> 
> > ## Lösung
> > 
> > Zum Beispiel `mail=team@carpentries.org` anstelle von `mail:team@carpentries.org`.
> > ~~~
> > description: "This research project develops training materials for reseachers wanting to learn to build project
> > websites in GitHub with GitHub Pages."
> > email: "team@carpentries.org"
> > twitter: "https://twitter.com/thecarpentries
> > ~~~
> > {: .language-yaml}
> > 
> > 
> > Wenn Sie in Ihrem GitHub-Repository navigieren, könnten Sie sehen, dass etwas in
> > `about.md` kaputt geht, wo wir `{% raw %}{{ site.twitter }}{% endraw %}` verwenden.
> > Im Gegensatz zu dem, was wir zuvor mit ungültigem Markdown gesehen haben, weigert
> > sich Jekyll jedoch, die Website zu erstellen und gibt eine Fehlermeldung aus.
> > 
> > Danach werden wir sehen, wo die Fehlermeldung zu finden ist und was sie verursacht
> > hat.
> > 
> {: .solution }
> 
{: .challenge }

Wenn Sie die Seite zur Ausführung der GitLab-Pipeline bis jetzt im Auge behalten haben
(`CI/CD > Pipelines`), ist Ihnen vielleicht aufgefallen, dass die Ergebnisse der
Pipeline nach dem Verschieben "ausstehend" sind, dann "laufen" und schließlich
"bestanden" werden. Irgendwann. Wenn dies nicht der Fall ist, lautet der Status
"fehlgeschlagen", Sie erhalten möglicherweise eine E-Mail darüber (je nach den
Einstellungen Ihres GitLab-Kontos) und sollten nicht in Panik geraten. Wie können wir
stattdessen verstehen, was den Fehler verursacht hat, und ihn beheben? Der Status
"fehlgeschlagen" ist zufällig eine Schaltfläche, klicken wir sie an.

![Klicken Sie auf die Schaltfläche "failed", um das Pipeline-Protokoll
aufzurufen](../fig/gitlab-error.png)

Auch hier können Sie auf die Schaltfläche ❌ <span style="color:red">Seiten</span>
klicken, um auf weitere Details zuzugreifen, z. B. auf das vollständige Protokoll der
Ausführung unserer Pipeline. Scrollen Sie im terminalähnlichen Fenster nach oben, um zu
sehen, wie die Pipeline gestartet, die Umgebungen vorbereitet, die Abhängigkeiten
installiert und bis zum Befehl `bundle exec jekyll build - public` korrekt ausgeführt
wurde. Erinnern Sie sich daran? Es ist der Befehl, der Jekyll startet, wir haben ihn in
die Datei `.gitlab-ci.yml` aufgenommen.

Wir haben Grund zu der Annahme, dass der Fehler hier damit zusammenhängt, dass Jekyll
die Seite nicht erstellen kann. Wenn wir genauer lesen, um mehr Details zu erhalten,
finden wir:

~~~
$ bundle exec jekyll build -d public
                    ------------------------------------------------
      Jekyll 4.2.1   Please append `--trace` to the `build` command
                     for any additional information or backtrace.
                    ------------------------------------------------
/usr/local/bundle/gems/safe_yaml-1.0.5/lib/safe_yaml/load.rb:143:in `parse': (/builds/hpg_ToyM/0/grp-bio-it/template-pages-jekyll/_config.yml): could not find expected ':' while scanning a simple key at line 3 column 1 (Psych::SyntaxError)
~~~
> 
{: .language-bash }

Dies bedeutet zwei Dinge: Erstens schlägt das Protokoll einen Weg vor, um mehr Details
zu erhalten, d.h. die Datei `.gitlab-ci.yml` zu modifizieren, indem man `--trace` zum
Befehl `bundle exec jekyll build -d public` hinzufügt, der so zu `bundle exec jekyll
build -d public --trace` wird. Aber das brauchen wir nicht wirklich: der nächste Satz
ist klar genug. Er besagt, dass es einen Fehler beim Parsen der Datei `_config.yml` gab,
weil Jekyll das erwartete Zeichen `:` nicht finden konnte. Da dieser Tippfehler Jekyll
daran hindert, die Seite zu erstellen, kann der Prozess nicht fortgesetzt werden.

> ## Bei Misserfolg wird Ihre Website nicht entfernt
> 
> Angesichts des Fehlers fragen Sie sich vielleicht, was mit der Website passiert ist?
> Wenn Sie die Adresse besuchen, werden Sie feststellen, dass die Website immer noch
> verfügbar ist.
> 
> GitLab hält Ihre vorherige Version online, bis der Fehler behoben ist und ein neuer
> Build erfolgreich abgeschlossen wurde.
> 
{: .callout }

Wir sollten zu unserer Datei `_config.yml` zurückkehren und den Fehler `=` beheben, den
wir (diesmal absichtlich) gemacht haben. Dann pushen Sie das Projekt erneut, und das
Problem ist gelöst!

> ## Übung: Übung mit der Fehlersuche in Jekyll
> 
> Manchmal passieren Tippfehler und können Ihre Website auf überraschende Weise
> verändern. Lassen Sie uns mit einigen möglichen Problemen experimentieren und sehen,
> was passiert.
> 
> Probieren Sie die unten aufgeführten Änderungen an Ihrer `index.md`-Datei aus und
> beobachten Sie, was passiert, wenn die Seite gerendert wird. Sie werden jedes Mal den
> vorherigen Fehler korrigieren wollen.
> 1. Verwenden Sie eine globale oder lokale Variable, die Sie nicht vorher definiert
>    haben.
> 2. Lassen Sie den Bindestrich am Ende des YAML-Headers weg.
> 3. Fügen Sie kein Leerzeichen zwischen dem YAML-Header und dem Rest der Seite ein
> 4. Setzen Sie den YAML-Header an eine andere Stelle in der Seite.
> 
> > ## Lösung
> > 
> > 1. Die Stelle, an der Sie die undefinierte Variable verwendet haben, ist leer, aber
> >    ansonsten kein Fehler. Beispiel:
> > 
> >    ~~~
> >    Hi! {% raw %}{{ site.greeting }}{% endraw %}. What have you been up to?
> >    ~~~
> >    {: .language-markdown }
> > 
> > 
> > 2. Die Kopfzeile zeigt etwas in der Datei an und die Variable, die definiert wurde,
> >    geht zur Indexseite anstelle des Links, den wir gesetzt haben.
> > 
> >    ~~~
> >    ---
> >    lesson-example: "https://carpentries.github.io/lesson-example/"
> > 
> >    Examples of our work can be found at: {% raw %}{{ page.lesson-example }}{% endraw %}
> >    ~~~
> >    {: .language-markdown }
> > 
> > 
> > 3. Dies scheint unsere Seite nicht zu beeinträchtigen, kann aber oft dazu führen,
> >    dass komplexere Seiten abbrechen.
> > 
> >    ~~~
> >    ---
> >    lesson-example: "https://carpentries.github.io/lesson-example/"
> >    ---
> >    Examples of our work can be found at: {% raw %}{{ page.lesson-example }}{% endraw %}
> >    ~~~
> >    {: .language-markdown }
> > 
> > 
> > 4. Dadurch wird auch die Kopfzeile auf der Seite angezeigt und die von uns erstellte
> >    variable Verknüpfung unterbrochen.
> > 
> >    ~~~
> >    Examples of our work can be found at: {% raw %}{{ page.lesson-example }}{% endraw %}
> >    ---
> >    lesson-example: "https://carpentries.github.io/lesson-example/"
> >    ---
> >    ~~~
> >    {: .language-markdown }
> > 
> {: .solution}
> 
> Hinweis: Beheben Sie alle Fehler, die Sie absichtlich in Ihre Seite eingefügt haben,
> bevor Sie weitermachen.
> 
{: .challenge}


