---
title:  'Scrivere documenti in MarkDown e convertirli in PDF con Pandoc e \LaTeX\ : un modo diverso di creare documenti PDF avanzati'
lang: it
author:
- Filippo Strozzi
papersize:
	- a4
numbersections: true

header-includes: |
    \usepackage{geometry}
    \usepackage{lastpage}
	\usepackage{fancyhdr}
	\pagestyle{fancy}
	\usepackage{multicol}
	\setlength{\columnsep}{5mm}
	\setlength{\columnseprule}{0.5pt}
	\usepackage{lipsum}
	\usepackage{marginnote}
	\lhead{Filippo Strozzi}
	\chead{}
	\rhead{}
	\lfoot{}
	\cfoot{\thepage\ di \pageref{LastPage}}
	\rfoot{[XXXF]}
keywords: [MarkDown, LaTeX, Pandoc]
abstract: |
	In questo articolo spiegherò come creare un PDF avanzato da un documento scritto in MarkDown attraverso Pandoc e \LaTeX. 

	Questo è un estratto dell'articolo ed un secondo paragrafo solo a titolo dimostrativo. Per creare il “Sommario” (_abstract_ in inglese) occorre fare delle modifiche all'intestazione [YAML](https://it.wikipedia.org/wiki/YAML) all'inizio del documento in MarkDown, più informazioni al XXX

...
[Commento]: <> (Inserimento variabili per il documento)
\newcommand{\attore}{Questo è il nome dell'attore}
\newcommand{\attore01}{super attore numero 1}
\newcommand{\attoreDue}{super attore numero 2}

\tableofcontents

\newpage
# Installazione dei software necessari sul vostro Mac

Prima di sperimentare con MarkDown, Pandoc e \LaTeX, occorre installare il _software_ necessario.

Ho dovuto installare:

* [Pandoc](http://pandoc.org) (ho testato la versione 2.2.1);
* [MacTeX](https://www.tug.org/mactex/mactex-download.html) – la versione completa che è un download di circa 3,2 Gb ma che contiene la maggior parte dei pacchetti che poi vi permetteranno di personalizzare l'aspetto del vostro documento PDF attraverso \LaTeX\ ; 
* Utilizzare il [Terminale](https://it.wikipedia.org/wiki/Terminale_(Apple)) di _macOS_ la conversione dei _file_ .MD in .PDF - sarà necessario sporcarsi le mani con la riga di comando dal terminale.

## Considerazioni preliminari

Questo documento cerca di dare una veloce guida su come  utilizzare MarkDown, Pandoc e \LaTeX\ per generare velocemente documenti PDF tipograficamente validi e, soprattutto, con funzioni avanzate.

Per fare ciò è necessario avere una infarinatura dei comandi principali del _MarkDown_ e soprattutto dovrete imparare qualche comando di \LaTeX. Se inizialmente può sembrare complesso, la cosa interessante è che, utilizzando questi strumenti, ed una volta conosciute le regole di base, la scrittura di un documento è relativamente semplice.

Inoltro parte del “lessico” speciale di \LaTeX\ può essere automatizzato attraverso trucchi di automazione che, tuttavia, non saranno oggetto di questo documento.

Segnalo da ultimo che chi scrive è tutto fuorché un esperto di questi sistemi e, il documento che avete tra le mani, è prevalentemente stato scritto ad uso personale e per risolvere proprie esigenze.

# Formattazione del documento

Di seguito esamino velocemente come creare la formattazione di base in MarkDown, Pandoc e \LaTeX.

## Formattazione del testo

Vediamo quindi come formattare il testo attraverso un misto di comandi in _MarkDown_ e \LaTeX.

_corsivo_ Si utilizza ```_corsivo_```\par
**grassetto** Si utilizza ```**grassetto**```\par
*enfasi* Si utilizza ```*enfasi*```

[maiuscoletto]{.smallcaps} Si utilizza ```[maiuscoletto]{.smallcaps}``` questo è un comando di \LaTeX.

~~testo cancellato~~ Si utilizza ```~~testo cancellato~~```

### Caratteri speciali

* ~ viene generato premendo ALT+5;
* le parentesi graffe {} si creano premendo SHIFT+ALT+[ e SHIFT+ALT]

## Creare un nuovo paragrafo

Il codice per inserire un nuovo paragrafo è il seguente:

```\par``` (comando in \LaTeX)

oppure basta premere invio e lasciare uno spazio tra le righe

## Allineamento del testo

Di fatto per far funzionare l'allineamento del testo è necessario inserire nel _Markdown_ alcuni comandi di \LaTeX \ perché non è possibile altrimenti avere queste opzioni. Per gli avvocati questo è abitualmente necessario per l'intestazione del Tribunale, la parola “CONCLUSIONI” etc \dots

\LaTeX\ testo a seguire

### Testo centrato

Di seguito un esempio di _testo centrato_:
\begin{center}
testo centrato
\end{center}

Il codice utilizzato è il seguente:

```\begin{center}``` \par
```	testo centrato``` \par
```\end{center}``` \par

### Testo a sinistra

Di seguito un esempio di _testo giustificato a sinistra_:
\begin{flushleft}
testo a sinistra
\end{flushleft}

Il codice utilizzato è il seguente:

```\begin{flushleft}``` \par
```	testo a sinistra``` \par
```\end{flushleft}``` \par

### Testo a destra

Di seguito un esempio di _testo giustificato a destra_:
\begin{flushright}
testo a destra
\end{flushright}

Il codice utilizzato è il seguente:

```\begin{flushright}``` \par
```	testo a destra``` \par
```\end{flushright}``` \par

## Metadati YAML

É possibile inserire nel documento in markdown tutta una serie di meta-dati utili per la generazione e personalizzazione del PDF finale.

### Titolo del documento

```title:  'Scrivere documenti in MarkDown …'```

### Autore/i

```author:```\par
```- Filippo Strozzi```\par
```- altro eventuale autore```\par
```- e così via …```\par

### Sinossi

```abstract: |```\par
```	In questo articolo spiegherò come …```

### Parole chiave

Per inserire della parole chiave all'interno del PDF è sufficente inserire 

```keywords: [MarkDown, LaTeX, Pandoc]```

### Inclusione nell'intestazione di comandi di \LaTeX

Invece di dover personalizzare il file di _templete_ di \LaTeX è possibile includere dei comandi (nello specifico dei pacchetti di \LaTeX) direttamente nel YAML. Questo è molto utile perché, così facendo è possibile personalizzare anche molto il PDF finale.

Per fare ciò occorre digitare all'interno dello YAML il seguente codice:

```header-includes: |```\par

Dopo di ciò dovranno essere indentati (ovvero messi dopo una serie di spazi / TAB).

### Numeri di pagina

Di seguito vedete l'esempio di come ho creato la gestione del piè di pagina e dell'intestazione di questo PDF.

```   \usepackage{lastpage}``` pacchetto lastpage [qui](http://ctan.mirror.garr.it/mirrors/CTAN/macros/latex/contrib/lastpage/lastpage.pdf) trovate il manuale in inglese \par
```	\usepackage{fancyhdr}``` pacchetto “fancyheadings” per la gestione dell'intestazione e piè di pagina \par
```	\pagestyle{fancy}```\par
```	\lhead{Filippo Strozzi}```intestazione di sinistra \par
```	\chead{}```intestazione centrale \par
```	\rhead{}```intestazione di destra \par
```	\lfoot{}``` piè di pagina sinistro \par 
```	\cfoot{\thepage\ di \pageref{LastPage}}``` piè di pagina centrale \par 
```	\rfoot{[XXXF]}``` piè di pagina destro \par


[Qui](http://ctan.mirror.garr.it/mirrors/CTAN/info/italian/fancyhdr/itfancyhdr.pdf) trovate il manuale sul _Layout di pagina in \LaTeX_.

## Come creare i link ai documenti allegati

E\' sufficiente utilizzare lo schema base del _MarkDown_ ovvero il seguente codice:

```[Testo che comparirà nel PDF](file_a_cui_fare_il_link.pdf)```

Di seguito potete testare un [**link ad un documento**](IOL2.pdf).

> Il link funziona sia in _Anteprima_ che in _Acrobat_. Unico difetto è che non apre il PDF all'esterno ma dentro Acrobat stesso e quindi si "perde" il PDF originario che si stava leggendo[^nota01]. Inoltre **in Acrobat apre automaticamente il tab dei segnalibri**. 

Se volete fare un link ad un documento il cui nome ha all’interno degli spazi come ad esempio:

```file a cui fare il link.pdf```

Occorrerà codificarlo in formato URL, ovvero trasformarlo come segue:

```file%20a%20cui%20fare%20il%20link.pdf```

Segnalo per scrupolo che per convertire non è sufficiente sostituire ad uno spazio il testo "%20" infatti il testo:

```questo è un file.pdf``` viene convertito in:

```questo%20%C3%A8%20un%20file.pdf```

## Link a siti Web / email

Per fare un link a siti web o email occorre chiudere tra minore e maggiore l'URL o l'indirizzo email:

``` <info@avvocati-e-mac.it> ```
``` <https://www.avvocati-e-mac.it/> ```

Di seguito il risultato del codice:

* <info@avvocati-e-mac.it>
* <https://www.avvocati-e-mac.it/>

## Riferimenti incrociati

\LaTeX\ permette di creare all'interno dei PDF dei riferimenti ad altre parti del documento creando così riferimenti incrociati.

> Quello che segue è un riferimento alla sottosezione \ref{sec:immagini} dove si trova la figura \ref{fig:terminale} che si trova nella pagina \pageref{fig:terminale}.

Questo è quanto ho scritto veramente in MarkDown / \LaTeX:

```Quello che segue è un riferimento alla sottosezione \ref{sec:immagini} dove si trova la figura \ref{fig:terminale} che si trova nella pagina \pageref{fig:terminale}.```

I **riferimenti incrociati** sono un potente strumento di \LaTeX\ per creare senza troppa complessità in una parte del testo riferimenti ad un'altra parte del documento.

Vediamo come funzionano nel dettaglio.

### Inserire un'etichetta

Prima cosa da fare è scegliere a cosa si vuol far riferimento ed inserire l'opportuno codice \LaTeX\  per riferirsi all'oggetto all'interno dell'intero documento.

Per fare ciò è necessario **agganciare una etichetta** (_label_ in inglese) all'oggetto che vogliamo richiamare.

Per fare ciò occorre inserire il seguente testo nel punto del documento a cui si vuole fare riferimento. Di seguito vedete un esempio:

```\label{nome_dell_oggetto}```

Dove il nome dell'oggetto racchiuso tra parentesi graffe è una stringa di testo identificativa dell'oggetto a cui volete fare riferimento.

### Inserire i riferimenti

Ora che abbiamo un'etichetta possiamo inserire i riferimenti alla stessa. \LaTeX\ si occuperà di recuperare l'indice di riferimento, ad esempio il numero del paragrafo o il numero dell'immagine a cui si è associata l'etichetta nonchè la pagina in cui si trova.

**Per fare riferimento al sezione del documento** in cui si trova il riferimento occorre digitare all'interno del testo:

```\ref{nome_dell_oggetto}```

**Per fare riferimento** invece **al numero della pagina** in cui si trova il riferimento occorrerà inserire la seguente stringa di testo:

```\pageref{nome_dell_oggetto}```

## Inserire un commento (invisibile nel PDF finale) all'interno del documento in Markdown

Ho dovuto curiosare un po' su internet ma ho trovato un metodo efficace per inserire commenti nel nostro documento markdown. 
Ho trovato [qui](https://stackoverflow.com/questions/4823468/comments-in-markdown#20885980) il suggerimento utile. Basta utilizzare la sintassi che segue.

```[Commento]: <> (Questo è un commento e non verrà visualizzato)```

## Utilizzare le variabili di \LaTeX\ per inserire i nomi delle parti

Spesso come avvocati è necessario inserire nomi nelle parti, delle controparte etc … 

Il metodo che ho imparato da [Franco Pasut](https://francopasut.tumblr.com/post/171908802565/latex-create-and-use-variable-names) è il seguente.

Create un comando di \LaTeX\ con questa sintassi:

```\newcommand{\attore}{Questo è il nome dell'attore}```

A questo punto basta scrivere all'interno del nostro documento in Markdown ```\nome_attore``` e comparirà il testo della variabile. Qui di seguito vi faccio vedere un esempio.

\attore

Alcune note:

1. Anzitutto quando si utilizzano le variabili di \LaTeX\ non è possibile utilizzare i comandi di formattazione del markdown (ad esempio ```**```  per creare il grassetto);
2. Occorrerà usare invece i comandi di \LaTeX\  per formattare correttamente (ad esempio digitare ```\textbf{\attore}``` per creare il grassetto così: \textbf{\attore});
3. Il nome della variabile deve essere univoco non potremo quindi avere una variabile chiamata ```\attore``` e ```\attore01``` ; il risultato se lo andassimo a inserire nel nostro PDF finale sarebbe questo "\attore01": ovvero il testo contenuto all'interno della variabile e quanto scritto dopo.
4. Se vogliamo utilizzare il "medesimo" nome della variabile è opportuno usare uno schema come questo: AttoreUno, AttoreDue, etc …


## Interruzione di pagina

Per creare un'interruzione di pagina basta inserire il codice

```\pagebreak```

all'interno del testo in Markdown.

\pagebreak

## Nuova pagina

Con il comando 

```\newpage```

è invece possibile creare una nuova pagina.

Di fatto i comandi ```\pagebreak``` e ```\newpage``` potrebbero sembrare identici. Tendenzialmente si usa il prima per interrompere la pagina dopo una certa unità di testo, mentre il secondo anteposto alla parte di testo che si vuole inizi in una pagina nuova.

Il prossimo sotto-capito è introdotto dal comando ```\newpage``` perché volevo che lo stesso partisse dall'inizio di una pagina nuova … a dir la verità no ma volevo farvi un esempio! 

\newpage

## Inserire indice all'interno del testo del documento

Soprattutto per la redazione di atti giudiziari è utile poter inserire all'interno del corpo del documento l'indice dell'atto.

Per fare ciò occorre inserire la seguente riga di testo in \LaTeX.

```\tableofcontents```

Da qualche test fatto non è possibile inserire due indici all'interno del medesimo documento; ne approfitto per segnalarvi la possiiblità di inserire anche liste delle immagini con il comando:

```\listoffigures``` indice delle figure / immagini (se presenti nel vostro documento);

```\listoftables``` indice delle tabelle (se presenti nel vostro documento).

\listoffigures

\pagebreak

# Pandoc e comandi a terminale

Per creare un documento PDF dal nostro file .MD occorrerà dare le opportune istruzioni a Pandoc a mezzo del Terminale.

Aperto il Terminale per creare il PDF dal nostro file .MD occorre entrare nella cartella in cui è salvato il file.

Nel terminale digitare ```cd``` e poi trascinate la cartella all'interno del terminale fino a che non viene visualizzata l'icona con il simbolo + come nell'immagine che segue.

![Come trascinare una cartella nel terminale per averne il percorso](trascinare%20cartella%20per%20CD.png)

Quando avrete rilasciato vi troverete nella seguente situazione di Figura

## I comandi di base per convertire da .MD in .PDF

Di seguito vedete il comando di base.

```pandoc nome_file_input.md -o nome_file_output.pdf```

Con il comando ```pandoc``` si invoca l'esecuzione del programma, con ```nome_file_input.md``` il documento sorgente da cui creare il PDF, con l'opzione ```-o``` si dice a Pandoc qual'è il documento che si vuole creare (file di output) nel nostro ```caso nome_file_output.pdf```.
A fronte dell'estensione del nome del documento da creare Pandoc comprende che c'è da generare un PDF ed utilizzare \LaTeX per la sua creazione.

![title](esempio%20di%20comando%20pandoc.png)

## Numerazione dei capitoli e sotto-capitoli

Tra le cose interessanti di utilizzare un software come \LaTeX per generare il PDF finale c'è la possibilità di avere la numerazione dei capitoli e sotto-capitoli generata in automatico. In questo modo non è necessario scervellarsi mentre si generano i contenuti di un documento.

Per fare ciò è sufficiente l'inserimento nella stringa di comandi di Pandoc che abbiamo già visto del parametro ```-N```, come si vede nell'esempio sottostante.

```pandoc nome_file_input.md -N -o nome_file_output.pdf```

## Inserimento dell'indice / tabella dei contenuti (TOC - Tables of Contents)

Altra funzione interessante è quella di poter inserire l'indice del documento (generato in automatico in base alla struttura gerarchica del nostro documento scritto in _MarkDown_) all'inizio dello stesso.

Per fare ciò è necessario inserire il parametro ```--toc``` dopo il nome del documento da convertire come mostrato qui sotto. 

```pandoc nome_file_input.md --toc -o nome_file_output.pdf```

Segnalo, se fosse di interesse (ad esempio nel caso di soggetti come avvocati) che è possibile inserire l'indice anche nel corpo del documento stesso che stiamo scrivento (ad esempio un atto giudiziario dopo l'intestazione del documento in cui vengono individuate la curia e le parti).

Per fare ciò, all'interno del nostro documento, dovremo inserire del codice \LaTeX come mostrato qui.

## Impostazione della lingua di \LaTeX\ in italiano

Se avete fatto qualche test con i comandi che vi ho fino ad ora insergnato probabilmente vi sarete accordi di un problema alcune parti del PDF generato (come ad esempio l'Indice che viene visualizzato come _Contents_ e non “Indice”).

Anche qui è possibile inserire un parametro per dire a Pandoc qual'è la lingua utilizzata per il nostro documento e, conseguentemente, utilizzare i parametri di \LaTeX corretti.

Per fare ciò occorre introdurre il concetto di Variabile in Pandoc. è infatti possibile inserire de parametri variabili per personalizzare la conversione del nostro documento scritto in MarkDown in PDF.

Per fare ciò occorre anzitutto inserie il parametro ```-V``` per dire a Pandoc che, dopo questo parametro si inserirà una variabile. Nel nostro caso utilizzeremo una variabile legata all'impostrazione del liguaggio del documento che utilizza la seguente formulazione ```lang=``` (che indica lingua = a …) ed il parametro specifico della lingua nel caso dell'italiano ```it-IT```.

Nel codice sottostante ne vedete un esempio più chiaro.

```pandoc nome_file_input.md -V lang=it-IT -o nome_file_output.pdf```



## Colorare i link all'interno del proprio documento per renderne più semplice la navigazione

La generazione di un PDF sin qui fatta crea PDF belli da stampare. Nel nostro caso, tuttavia, è di maggior interesse che i PDF, dotati di capacità avantate di navigazione, siano facilmente navigabili dall'utente finale.

Per fare ciò è utile creare un PDF in cui i link (siano essi a documenti, ad altre parti dell'atto come riferimenti o note a piè di pagina) siano ben visibili.

Ciò è facilmente ottenibile passando la seguente variabile ```-V colorlinks ```

```pandoc nome_file_input.md -V lang=it-IT -V colorlinks -o nome_file_output.pdf```

Piccola nota perché mentre facevo i test mi ha causato degli errori: ogni volta che inserite una variabile è neccassario dichiararlo con il parametro ```-V``` altrimenti la variabile non verrà presa da Pandoc e, nel nostro esempio, i link non risulteranno colorati.

## Il risultato finale dei comandi

```pandoc nome_file_input.md -V lang=it-IT -V colorlinks --toc -N -o nome_file_output.pdf```

## Caratteri Unicode non riconosciuti da pdflatex

Fino ad ora abbiamo utilizzato, per la conversione dei nostri documenti solo il motore di conversione di \LaTeX\ denominato pdflatex.

Questo è il motore più vecchio e non gestisce tutta una serie di caratteri speciali. In particolare se si taglia ed incolla da un PDF del testo all’interno del nostro documento in markdown è possibile ricevere un errore come nell’immagine seguente.


Per ovviare a ciò occorre utilizzare il motore di conversione xelatex\ più moderno ed in grado di gestire i simboli Unicode.

```pandoc nome_file_input.md --pdf-engine=xelatex -o nome_file_output.pdf```

Ovviamente tutti i parametri indicati nei punti precedenti sono utilizzabili dopo aver invocato l’uso del motore XeLaTeX.

# Work in Progress

## Attivare la auto-numerazione delle sezioni e sottosezioni

Per attivare l'auto-numerazione delle sezione è possibile farlo da riga di comandi (relativamente scomodo) o dalla solita intestazione YAML inserendo la riga:

	numbersections: true

Funziona sia con la sezione in _markdown_ utilizzando “#” si con il comando ```\section{Oggetto}```.

> Nota: non è possibile però usare markdown e dialetto \LaTeX assieme, perché altrimenti da un errore.

## Testo su più colonne

Per attivare l'impaginazione del documento a più colonne occorre inserire nel intestazione YAML i seguenti comando dopo ```header-includes: |```:

	\usepackage{multicol}

Il primo comando attiva il pacchetto _multicol_ per gestire le colonne multiple di testo, il secondo  ```\setlength{\columnsep}{}```permette di impostare lo spazio tra le due colonne.

Per attivare poi la suddivisione a colonne all'interno del nostro documento occorrerà digitare:

	\begin{multicols}{2}
	…
	\end{multicols} 
	
### Personalizzare la distanza tra le colonne

Per impostare la distanza in millimentri o centimetri tra le varie colonne occorre inserire nel intestazione YAML i seguenti comando dopo ```header-includes: |```:

	\setlength{\columnsep}{5mm}

Dove ```5mm``` è la misura che si vuole avere. é possibile usare i millimetri con “mm” o i centimetri con “cm”.

### Inserire una linea divisoria tra le colonne 

Per impostare la presenza di una linea tra le colonne che è possibile quantificare  in punti occorre inserire nel intestazione YAML i seguenti comando dopo ```header-includes: |```:

	\setlength{\columnseprule}{0.5pt}

###  Sezioni e sotto-sezioni all'interno ed all'esterno del testo a colonna

All'interno del testo suddiviso in colonne è possibile suddividere in sezioni il testo. In questo caso occorre tuttavia utilizzare solo i comandi in \LaTeX.

Se si vuole è possibile creare una sorta di preambolo prima delle colonne utilizzando 

	[\section{titolo della sezione} ed eventuale testo 
	ulteriore da non suddividere in colonne]
	
Di seguito mostro un esempio:

	\begin{multicols}{2}
	[\subsubsection{Test} Questo è un testo non formattato in colonne]
	\lipsum[1]
	\end{multicols}

e qui la sua realizzazione grafica:

\begin{multicols}{2}
[\subsubsection{Test} Questo è un testo non formattato in colonne]
\lipsum[1]
\end{multicols}


[Link](http://ctan.mirror.garr.it/mirrors/CTAN/macros/latex/required/tools/multicol.pdf) al manuale di riferimento del pacchetto (in lingua inglese) ma non molto chiaro, meglio [questo](https://www.overleaf.com/learn/latex/Multiple_columns).

\subsection{Note a margine}

\marginnote{Questa è una nota a margine!}

Per impostare la presenza di una linea tra le colonne che è possibile quantificare  in punti occorre inserire nel intestazione YAML i seguenti comando dopo ```header-includes: |```:

	\usepackage{geometry}
	\usepackage{marginnote}

e poi inserire nel testo:

	\marginnote{Questa è una nota a margine!}[3cm]
	
Il secondo parametro tra parentesi quadre indica l'altezza verticale della nota (è possibile inserire anche valori negativi). 

\subsubsection{Nota a sinistra}

È possibile inserire anche note sul margine sinistro.
\reversemarginpar
\marginnote{Nota sul margine sinistro!}

Occorrerà inserire il seguente testo:

	\reversemarginpar
	\marginnote{Questa è una nota sul margine sinistro!}


## Cose da fare

* vedere come modificare o specificare un templates (presumo in LateX)
* creare un templates standard

## Immagini \label{sec:immagini}

![Immagine del Terminale \label{fig:terminale}](trascinare%20cartella%20per%20CD.png)


## Test di inserimento di variabile

Questo è \attore

_________

::::: {#special .sidebar}
Questo è un paragrafo.

… e questo un'altro.
:::::

_________


[torna al primo capitolo](#Primo capitolo)

[^nota01]: Sarà bene studiare come e se si può implementare la funzione meglio.
