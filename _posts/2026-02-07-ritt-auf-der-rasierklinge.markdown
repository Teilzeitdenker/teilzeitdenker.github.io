---
layout: default
title:  "Ritt auf der Rasierklinge"
date:   2026-02-07
categories: introduction
---
In Zeiten von GitHub Copilot ist es nicht mehr ganz so leicht, im Bereich der wettbewerbsmäßigen Programmierung (competitive programming) herausfordernde Projekte und Aufgaben im Internet zu finden, die sich nicht mit einer kurzen GitHub-Suche oder ein paar Minuten AgentChat mühelos (und folglich auch ohne jeglichen wünschenswerten Lerneffekt oder Ego-Boost) "lösen" lassen. 

So ist das ursprüngliche [Projekt Euler][project-euler] bereits vollständig entzaubert worden, siehe [Ciro Santillis Repo][ciro-santilli] oder noch viel schlimmer, einfach nur die Liste aller Lösungszahlen auf dem sehr passend benannten Account [Lucky Toilet][lucky-toilet]. Die finnische CP-Seite [CSES][cses] hat zwar Ende 2025 ein Update erhalten (statt ehemals 300 sind es jetzt 400 Aufgaben), aber auch hier waren schon zu viele Leute unterwegs als dass sich nicht zu leicht Lösungen in diversen online repos finden ließen.

Auch das [Projekt Euler+][project-euler-plus] auf [HackerRank][hacker-rank] wird sich dieser Entwicklung binnen absehbarer Zeit wohl nicht mehr entziehen können, aber bis heute gibt es erstaunlich wenig dazu zu finden, was den Wert jeder eigenen Lösung erheblich steigert (schon klar, dass es jedem selbst überlassen ist, ob er "Lösungen nachschaue" und damit das eigene Lernerlebnis torpediert, aber leider ist es ja so, dass vernünftige Menschen dazu neigen, sich die Arbeit grundsätzlich erleichtern zu wollen, auch wenn das auf lange Sicht den Untergang des Abendlandes verursachen mag). Bis es auch dort soweit kommt, will ich mich daher weiter damit beschäftigen, um wie ein Verdurstender noch die letzten köstlichen Tropfen Erkenntnisgewinn-Nektars herauszupressen. Dieser "Blog" soll eine Art Tagebuch meines Fortschritts ab Aufgabe 120 werden. 

Der im Titel genannte "Ritt auf der Rasierklinge" besteht nun darin, hier nicht einfach ganz öde die alles verratenden Lösungen zu posten, die ja dem hilflos ausgelieferten geneigten Leser vom so seltsam satanisch grinsenden Autor den eben gerade in großen Tönen gelobten Spaß am Selbstversuch vergällen würden, sondern vielmehr zielgerichtete kleine Hinweise zu geben, die eventuelles Ungemach abwenden können. Denn nicht jeder scheitert mit Würde und verfügt über die nötige Resilienz, um seinen aufgestauten Frust durch das stetige Rennen gegen eine Ziegelmauer aus Wrong Answers und TLEs nicht irgendwann an der klapprigen Tastatur oder unschuldig herumstehenden Möbeln und Haustieren auslassen zu wollen. Diese Seite sieht sich damit auch der medizinischen Wutanfalls-Prävention und dem Tierschutz verpflichtet. 

Um das Jekyll-Theme [Hacker][hacker], das hier am Werk ist, kurz auszuprobieren, poste ich mal mein "hackerrank_minimal_template.cpp", das einige handgemachte I/O-Funktionen enthält, die einem bei inputlastigen Aufgaben tatsächlich den Allerwertesten retten können. 

{% highlight c++ %}
#pragma GCC optimize("Ofast", "unroll-loops", "fast-math")
#include <bits/stdc++.h>

using namespace std;

//---------------------------------- IO functions ----------------------------------------

// Use "-D WINDOWS"  when compiling to do the job on WINDOWS
#ifdef WINDOWS
int getchar_unlocked() {return _getchar_nolock();}
int putchar_unlocked(int c) {return _putchar_nolock(c);}
#endif

static inline int read() {
    int res, ch;
    while ((res = getchar_unlocked()) < '0') {}
    res -= '0';
    while ((ch = getchar_unlocked()) >= '0') res = (res << 3) + (res << 1) + (ch ^ 48);
    return res;
}

static inline void write(int n) {
    char s[10]; // this buffer is only big enough for ints!
    short i{0};
    if (n == 0) { putchar_unlocked('0'); return; }
    while (n) {
        s[i++] = (n % 10) + '0';
        n /= 10;
    }
    while (i--) putchar_unlocked(s[i]);
}

//---------------------------------- GLOBAL variables --------------------------------------

//---------------------------------- Helper functions --------------------------------------

//---------------------------------- MAIN function -----------------------------------------

auto main() -> int {
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    int n = read();
    int res{0};
    write(res); putchar_unlocked('\n');
    return 0;
}
{% endhighlight %}

Mit etwas Vorsicht zu genießen ist der kleine char-Buffer bei write(). Dieser muss angepasst werden, falls größere primitive Datentypen ausgegegeben werden. Für long longs reichen 20 Charaktere, für die 128-bit integer __int128, die nur mit g++ verfügbar sind und keine Unterstützung durch std::cout haben, sollte man auf 40 gehen (ich weiß, man könnte ihn auch einfach standardmäßig auf 40 setzen, aber das wäre ja Verschwendung!)

Kompiliert wird unter bash einfach mit 

{% highlight bash %}
g++ -o program source.cpp -std=c++20 -Wall -Wextra
{% endhighlight %}

und eine eventuelle input.txt-Datei übergeben wir dem Programm mit

{% highlight bash %}
./program < input.txt
{% endhighlight %}

Im obigen Beispiel-Template bestände der nötige Input aus genau einem Integer, das Ergebnis ist unabhängig davon immer eine Nullnummer.

Unter Windows muss man obiges Template mit einer Präprozessor-Direktive etwas anpassen, da getchar_unlocked() und Konsorten dort unbekannt sind. Kompiliere unter Powershell also mit 

{% highlight powershell %}
g++ -o program source.cpp -std=c++20 -Wall -Wextra -D WINDOWS
{% endhighlight %}

und pipe den Input einfach mit
{% highlight powershell %}
Get-Content input.txt | program.exe
{% endhighlight %}

in das executable.

[project-euler]: https://projecteuler.net/
[project-euler-plus]: https://www.hackerrank.com/contests/projecteuler/challenges
[ciro-santilli]: https://github.com/cirosantilli/project-euler-solutions
[lucky-toilet]: https://github.com/lucky-bai/projecteuler-solutions
[hacker-rank]: https://www.hackerrank.com/
[hacker]: https://github.com/pages-themes/hacker
[cses]: https://cses.fi/problemset/