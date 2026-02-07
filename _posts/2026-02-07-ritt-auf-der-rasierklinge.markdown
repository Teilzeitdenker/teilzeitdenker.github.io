---
layout: default
title:  "Ritt auf der Rasierklinge"
date:   2026-02-05 22:57:37 +0100
categories: jekyll update
---
In Zeiten von GitHub Copilot ist es nicht mehr ganz so leicht, im Bereich der wettbewerbsmäßigen Programmierung (competitive programming) herausfordernde Aufgaben zu finden, die sich nicht mit ein paar Minuten AgentChat mühelos (und folglich auch ohne jeglichen wünschenswerten Lerneffekt oder Ego-Boost) erledigen lassen. 

So ist das ursprüngliche [Projekt Euler][project-euler] bereits vollständig entzaubert worden, siehe [Ciro Santillis Repo][ciro-santilli] oder noch viel schlimmer, einfach nur die Liste aller Lösungszahlen auf dem sehr passend benannten Account [Lucky Toilet][lucky-toilet].

Und auch das Projekt Euler+ auf [HackerRank][hacker-rank] wird sich dieser Entwicklung binnen absehbarer Zeit wohl nicht mehr erwehren können. Aber bis dahin werde ich daran weiterarbeiten, um wie ein Verdurstender noch die letzten köstlichen Tropfen Erkenntnisgewinn-Nektars herauszupressen. Dieser Blog soll eine Art Tagebuch meines Fortschritts ab Aufgabe 120 werden. 

Der im Titel genannte "Ritt auf der Rasierklinge" besteht nun darin, nicht nurmehr fade vollständige Lösungen zu posten, die ja dem geneigten Leser den vom Autor in großen Tönen gelobten Spaß am Selbstversuch vergällen würden, sondern vielmehr zielgerichtete kleine Hinweise zu geben, die eventuelles Ungemach abwenden können. Nicht jeder scheitert mit Würde und verfügt über die nötige Resilienz, seinen aufgestauten Frust durch das stetige Rennen gegen eine Ziegelmauer aus Wrong Answers und TLEs nicht irgendwann an der Tastatur oder unschuldig herumstehenden Möbeln auszulassen. 

Um das Jekyll-Theme "Hacker", das hier am Werk ist, noch kurz auszuprobieren, poste ich mal mein "hackerrank_minimal_template.cpp", das einige handgemachte I/O-Funktionen enthält, die einem bei inputlastigen Aufgaben tatsächlich den Arsch retten können. 

Aber Vorsicht: Der Buffer bei write() muss angepasst werden, falls größere primitive Datentypen ausgegegeben werden. Für long longs reichen 20 Charaktere, für die 128-bit integer __int128, die nur mit g++ verfügbar sind und keine Unterstützung durch std::cout haben, sollte man auf 40 gehen. 

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


[project-euler]: https://projecteuler.net/
[ciro-santilli]: https://github.com/cirosantilli/project-euler-solutions
[lucky-toilet]: https://github.com/lucky-bai/projecteuler-solutions
[hacker-rank]: https://www.hackerrank.com/