plotcourses
===========

Dette er et pythonscript som plotter generell vurdering av et kurs over
tid. Scriptet skal brukes til kursevalueringen som gjøres av Fagutvalget ved
Institutt for informatikk. Her er et eksempel på hvordan et plot kan se ut:

![screenshot](example_plot.pdf)

Merk at dette scriptet er laget for å passe til Fui sitt filområde, og vil
antageligvis ikke være til nytte for noen utenfor Fui. 

## Bruk

Scriptet er inkludert i `~/internt/kk/kursevaluering/v2013/Makefile`, og
denne makefilen kan gjenbrukes i senere semestre. Les videre dersom du
ønsker mer innsikt i hvordan scriptet fungerer (eller at Makefilen mot
formodning ikke lenger fungerer).

Scriptet bruker `python3.3` og er avhengig av `matplotlib`. På Ifi's
maskiner ligger `python3.3` i `/snacks/bin/` området.

    [fui@nonsuch v2013]$ /snacks/bin/python3.3 ./pyscript/plotcourses.py --help
    usage: plotcourses.py [-h] [-o OUTPUT] [-t SCORE_TREE_PATH] [-d FILTER_PATH]
                          [-r REPORT] [-m]
    
    optional arguments:
      -h, --help          show this help message and exit
      -o OUTPUT           Sets OUTPUT destination ('.' is default)
      -t SCORE_TREE_PATH  Traverse SCORE_TREE_PATH for score_overview.txt files
      -d FILTER_PATH      Searches FILTER_PATH for courses to plot
      -r REPORT           rebuilds a REPORT with plots
      -m                  enable multiprocessing

For at scripet skal fungere må den finne en rekke filer, som alle sammen
heter  `score_overview.txt`. Det finnes en slik fil for hvert semester siden
våren 2009. For at scriptet skal finne disse filene må enten scriptet kjøres
fra `~/internt/kk/kursevaluering/` eller bruke opsjonen `-t`.

Siden vi ikke trenger generere plot for alle kurs som har gått hvert
semester finnes det en opsjon som lar deg filtrere vekk kurs. Ved å bruke
`-d ~/internt/kk/kursevaluering/v2013/` vil scriptet kun generere plots for
kurs som det er skrevet en evaluering for. Dette gjøres ved å finne filer
med navn som `INFxxxx.txt`.

`compile-summaries.py` genererer kursevalueringen, som får navn
`report.tex`. For å legge til plottene som genereres i rapporten kan man
bruke opsjonen `-r` etterfulgt av `/path/to/report.tex`.

For å forbedre hastigheten til scriptet kan man bruke opsjonen `-m` for å
skrive plottene parallelt.

### Eksempelkjøring

    fui@safir: ~/internt/kk/kursevaluering/v2013$ /snacks/bin/python3.3 ./pyscript/plotcourses.py -o plots/ -t .. -d . -r report.tex -m

Denne kommandoen vil produsere plots (i parallell) som legges i mappen
`plots`. Det vil hente ut `score_overview.txt` filer fra `..` som er den
relative stien til `~/internt/kk/kursevaluering/`. Det vil kun genereres
plot til kurs som det er blitt skrevet evaluering for våren 2013. Til slutt
oppdateres `report.tex` filen til å inkludere plottene som er generert.
