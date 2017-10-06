---
title: 'aaaGuide toohello neurale reti linguaggio specifica Net # | Documenti Microsoft'
description: 'Sintassi per hello Net # neural networks lingua specifica, con relativi esempi di come toocreate una rete neurale personalizzata del modello in Microsoft Azure Machine Learning tramite Net #'
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: cfd1454b-47df-4745-b064-ce5f9b3be303
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 3493247ecc39ca3a1382510ad520d7017159ff62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a>Guida di linguaggio di specifica di rete neurale tooNet # per Azure Machine Learning
## <a name="overview"></a>Panoramica
NET # è un linguaggio sviluppato da Microsoft che viene utilizzato toodefine architetture di rete neurale. È possibile usare Net# in moduli di reti neurali in Microsoft Azure Machine Learning.

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

In questo articolo si apprenderà concetti di base necessarie toodevelop una rete neurale personalizzata: 

* Requisiti di rete neurale e come toodefine hello componenti primari
* sintassi di Hello e parole chiave del linguaggio di specifica Net # hello
* Esempi di reti neurali personalizzate create usando Net# 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a>Nozioni di base sulla rete neurale
Costituito da una struttura di rete neurale ***nodi*** organizzati in ***livelli***e ponderata ***connessioni*** (o ***bordi***) tra nodi Hello. connessioni Hello sono direzionali e ogni connessione dispone di un ***origine*** nodo e un ***destinazione*** nodo.  

Ogni ***livello di cui è possibile eseguire il training*** (livello nascosto o di output) ha una o più ***aggregazioni di connessioni***. Un bundle di connessione è costituito da un livello di origine e una specifica di connessioni hello di tale livello di origine. Tutte le connessioni di hello in una condivisione di bundle specificato hello stesso ***livello origine*** e hello stesso ***livello destinazione***. In Net #, un bundle di connessione viene considerato come livello di destinazione del bundle toohello appartiene.  

NET # supporta vari tipi di pacchetti di connessione, che consente di personalizzare la modalità di hello gli input sono mappate toohidden livelli e output toohello mappato.   

predefinito Hello o bundle standard è un **bundle completo**, in cui ogni nodo in hello del livello di origine è nodo tooevery connessi nel livello di destinazione hello.  

Net # supporta inoltre hello seguenti quattro tipi di pacchetti di connessione avanzate:  

* **Aggregazioni filtrate**. utente di Hello può definire un predicato utilizzando percorsi hello del nodo di livello di origine hello e hello destinazione livello. I nodi connessi ogni volta che il predicato hello è True.
* **Aggregazioni convoluzionali**. utente di Hello può definire Villaggi piccoli di nodi nel livello di origine hello. Ogni nodo nel livello di destinazione hello è connesso tooone risorse di nodi nel livello di origine hello.
* **Aggregazioni di pooling** e **aggregazioni di normalizzazione delle risposte**. Questi sono raggruppamenti di tooconvolutional simili in tale hello utente definisce Villaggi piccoli di nodi nel livello di origine hello. differenza Hello è che non si è trainable pesi hello dei bordi hello in questi pacchetti. In alternativa, in cui viene applicata una funzione predefinita nodo di origine toohello valori toodetermine hello destinazione nodo valore.  

Tramite Net # toodefine hello struttura di una rete neurale rende possibili toodefine strutture complesse, ad esempio le reti neurali o convoluzioni di dimensioni arbitrarie, che sono note learning tooimprove sui dati, ad esempio immagini, audio o video.  

## <a name="supported-customizations"></a>Personalizzazioni supportate
architettura Hello dei modelli di rete neurale creati in Azure Machine Learning può essere ampiamente personalizzato tramite Net #. È possibile:  

* Creare livelli nascosti e controllo hello numero di nodi in ogni livello.
* Specificare la modalità livelli tooeach toobe connessi altri.
* Definire strutture di connettività speciali, ad esempio aggregazioni di convoluzioni e per la condivisione dei pesi.
* Specificare diverse funzioni di attivazione.  

Per informazioni dettagliate della sintassi del linguaggio di specifica hello, vedere [struttura specifica](#Structure-specifications).  

Per esempi di definizione di reti neurali per alcune attività, dalla toocomplex simplex, di apprendimento automatico comune vedere [esempi](#Examples-of-Net#-usage).  

## <a name="general-requirements"></a>Requisiti generali
* Devono essere esattamente disponibili un livello di output, almeno un livello di input e zero o più livelli nascosti. 
* Ogni livello ha un numero fisso di nodi, disposti concettualmente in una matrice rettangolare di dimensioni arbitrarie. 
* Input livelli privi di parametri con training associato e rappresentano hello punto dati di istanza in cui vengono immessi rete hello. 
* Livelli trainable (livelli nascosti e di output di hello) sono associati parametri con training, noto come pesi e i pregiudizi. 
* nodi di origine e destinazione Hello devono trovarsi in livelli separati. 
* Le connessioni devono essere acicliche; in altre parole, non può essere una catena di connessioni iniziali toohello back-nodo di origine iniziale.
* il livello di output di Hello non può essere un livello di origine di un pacchetto di connessione.  

## <a name="structure-specifications"></a>Specifiche di struttura
Una specifica struttura di rete neurale è composto da tre sezioni: hello **dichiarazione di costante**, hello **livello dichiarazione**, hello **dichiarazione connessione**. È anche disponibile una sezione facoltativa denominata **dichiarazione delle condivisioni**. sezioni Hello possono essere specificate in qualsiasi ordine.  

## <a name="constant-declaration"></a>Dichiarazione della costante
Una dichiarazione della costante è facoltativa. Fornisce un toodefine indica i valori utilizzati in un' posizione nella definizione di rete neurale hello. istruzione di dichiarazione Hello è costituito da un identificatore seguito da un segno di uguale e un'espressione di valore.   

Ad esempio, hello istruzione definisce una costante **x**:  

    Const X = 28;  

toodefine due o più costanti contemporaneamente, racchiudere i nomi di identificatore hello e i valori tra parentesi graffe ed è necessario separarli con punti e virgola. ad esempio:  

    Const { X = 28; Y = 4; }  

Hello destra di ogni espressione di assegnazione può essere un numero intero, un numero reale, un valore booleano (True o False) o un'espressione matematica. ad esempio:  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a>Dichiarazione dei livelli
dichiarazione di livello Hello è obbligatorio. Definisce dimensioni hello e l'origine del livello di hello, inclusi i bundle di connessione e relativi attributi. salve inizia di istruzione di dichiarazione con il nome di hello del livello di hello (di input, nascosto o di output), seguito dalle dimensioni di hello del livello di hello (una tupla di numeri interi positivi). ad esempio:  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* prodotto Hello di dimensioni hello è il numero di hello di nodi nel livello hello. In questo esempio, sono presenti due dimensioni [5,20], che non vi sono 100 nodi nel livello hello.
* livelli di Hello possono essere dichiarati in qualsiasi ordine, con una sola eccezione: se è definito più di un livello di input, hello ordine in cui sono dichiarati deve corrispondere hello di funzioni nei dati di input hello.  

toospecify che hello numero di nodi in un livello determinato automaticamente, utilizzare hello **auto** (parola chiave). Hello **auto** parola chiave ha effetti diversi, a seconda di livello hello:  

* In una dichiarazione a livello di input, il numero di hello di nodi è il numero di hello di funzioni nei dati di input hello.
* In una dichiarazione di livello nascosto, il numero di hello di nodi è il numero hello specificato dal valore del parametro hello per **numero di nodi nascosti**. 
* In una dichiarazione di livello di output, il numero di hello di nodi è 2 per classificazione a due classi, 1 per la regressione e uguale toohello numero di nodi di output per la classificazione multiclasse.   

Ad esempio, hello seguente definizione di rete consente dimensioni hello di tutti i livelli toobe determinato automaticamente:  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


Una dichiarazione di livello per un livello trainable (livelli nascosti o di output di hello) può includere facoltativamente funzione output hello (denominata anche una funzione di attivazione), che per impostazione predefinita troppo**sigmoidale** per i modelli di classificazione e **lineare** per i modelli di regressione. (Anche se si utilizza l'impostazione predefinita di hello, è possibile dichiarare in modo esplicito funzione di attivazione hello, se lo si desidera per maggiore chiarezza.)

Hello output funzioni seguenti sono supportate:  

* sigmoid
* linear
* softmax
* rlinear
* square
* sqrt
* srlinear
* abs
* tanh 
* brlinear  

Ad esempio che segue la dichiarazione di hello utilizza hello **softmax** funzione:  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a>Dichiarazione della connessione
Immediatamente dopo aver definito livello trainable hello, è necessario dichiarare le connessioni tra i livelli di hello che è definito. dichiarazione di bundle connessione Hello inizia con la parola chiave hello **da**, seguiti dal nome hello di tipo del bundle hello origine hello e di livello di connessione bundle toocreate.   

Sono attualmente supportati cinque tipi di aggregazioni di connessioni:  

* **Completa** bundle, indicati dalla parola chiave hello **tutti**
* **Filtrati** bundle, indicati dalla parola chiave hello **in**, seguito da un'espressione del predicato
* **Convolutional** bundle, indicati dalla parola chiave hello **convolve**, seguito da attributi convoluzione hello
* **Il pool** bundle, indicati dalle parole chiave hello **max pool** o **significa pool**
* **Normalizzazione di risposta** bundle, indicati dalla parola chiave hello **norm risposta**      

## <a name="full-bundles"></a>Aggregazioni complete
Un bundle di connessione completa include una connessione da ogni nodo nel nodo di hello origine livello tooeach nel livello di destinazione hello. Si tratta di tipo di connessione di rete predefinito hello.  

## <a name="filtered-bundles"></a>Aggregazioni filtrate
Una specifica di aggregazione di connessioni filtrata include un predicato, espresso sintatticamente in modo analogo a un'espressione lambda in C#. Hello seguente definisce due pacchetti filtrati:  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* Nel predicato hello per *ByRow*, **s** è un parametro che rappresenta un indice nella matrice rettangolare di hello dei nodi del livello di input hello, *pixel*, e **d**  è un parametro che rappresenta un indice nella matrice hello dei nodi del livello nascosto hello, *ByRow*. tipo di entrambi Hello **s** e **d** è una tupla di interi di lunghezza due. Concettualmente, **s** include tutte le coppie di valori interi con *0 <= s[0] < 10* e *0 <= s[1] < 20* e **d** include tutte le coppie di valori interi con *0 <= d[0] < 10* e *0 <= d[1] < 12*. 
* Sul lato destro di hello dell'espressione predicato hello, vi è una condizione. In questo esempio, per ogni valore di **s** e **d** tale condizione hello è True, è un bordo dal nodo di livello di hello origine livello nodo toohello destinazione. Di conseguenza, questa espressione di filtro indica il file di bundle hello include una connessione dal nodo hello definito da **s** toohello nodo definito da **d** in tutti i casi in cui s [0] è uguale tood [0].  

È facoltativamente possibile specificare un insieme di pesi per un'aggregazione filtrata. valore per hello Hello **pesi** attributo deve essere una tupla di valori a virgola mobile con una lunghezza corrispondente hello numero di connessioni definito dal bundle hello. Per impostazione predefinita, i pesi sono generati in modo casuale.  

I valori di peso sono raggruppati in base all'indice di nodo di destinazione hello. Vale a dire, se è connesso il nodo di destinazione prima hello ha impiegato i nodi di origine, hello innanzitutto *K* gli elementi di hello **pesi** tupla sono pesi hello per hello primo nodo di destinazione, in ordine di indice di origine. Hello che stesso vale per hello rimanenti nodi di destinazione.  

È possibile toospecify pesi direttamente come valori costanti. Ad esempio, se si è appreso pesi hello in precedenza, è possibile specificarli come costanti utilizzando questa sintassi:

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a>Aggregazioni convoluzionali
Se i dati di training hello presenta una struttura omogenea, le connessioni convolutional sono funzionalità di alto livello dei dati hello toolearn comunemente utilizzati. Ad esempio, nei dati di tipo immagine, audio o video è possibile che la dimensionalità spaziale o temporale sia abbastanza uniforme.  

Bundle convolutional impiegano rettangolare **directcompute** che vengono portati sopra tramite dimensioni hello. In pratica, ogni kernel definisce un set di pesi applicato in locali Villaggi, cui viene fatto riferimento tooas **applicazioni kernel**. Ogni applicazione kernel corrisponde tooa nodo nel livello di origine hello, ovvero tooas cui hello **nodo centrale**. numero di connessioni sono condivise con pesi Hello di un kernel. In un bundle convolutional, ogni kernel rettangolare e tutte le applicazioni kernel hello stessa dimensione.  

Bundle convolutional supportano hello gli attributi seguenti:

**InputShape** definisce dimensionalità hello del livello di origine hello per scopi di hello per il raggruppamento convolutional. il valore di Hello deve essere una tupla di numeri interi positivi. prodotto di Hello di numeri interi hello deve essere uguale hello numero di nodi nel livello di origine hello, ma in caso contrario, è necessario dimensionalità hello toomatch dichiarata per il livello di origine hello. lunghezza Hello di questo tipo di tupla diventa hello **grado** valore per bundle convolutional hello. (In genere grado fa riferimento toohello numero di argomenti o una funzione può accettare gli operandi).  

forma hello toodefine e le posizioni dei kernel hello, utilizzare gli attributi di hello **KernelShape**, **Stride**, **Padding**, **LowerPad**, e **UpperPad**:   

* **KernelShape**: dimensionalità di hello definisce (obbligatoria) di ogni kernel per bundle convolutional hello. il valore di Hello deve essere una tupla di numeri interi positivi con una lunghezza pari al grado hello del bundle hello. Ogni componente di questo tipo di tupla deve essere maggiore di componente corrispondente di hello del **InputShape**. 
* **Stride**: (facoltativo) hello definisce la variabile di dimensioni di passaggio di convoluzione hello (dimensioni di un passaggio per ogni dimensione), che corrisponde alla distanza hello tra i nodi centrale hello. il valore di Hello deve essere una tupla di numeri interi positivi con una lunghezza di grado hello del bundle hello. Ogni componente di questo tipo di tupla deve essere maggiore di componente corrispondente di hello del **KernelShape**. valore predefinito di Hello è una tupla con tooone uguale di tutti i componenti. 
* **Condivisione**: condivisione per ogni dimensione di convoluzione hello un peso di hello definisce (facoltativo). il valore di Hello può essere un singolo valore booleano o una tupla di valori booleani con una lunghezza di grado hello del bundle hello. Un singolo valore booleano è estesa toobe una tupla di lunghezza corretta di hello con tutti i componenti toohello uguale valore specificato. valore predefinito di Hello è una tupla costituita da tutti i valori True. 
* **MapCount**: (facoltativo) definisce hello numerose funzionalità esegue il mapping per bundle convolutional hello. il valore di Hello può essere un numero intero positivo o una tupla di numeri interi positivi con una lunghezza di grado hello del bundle hello. Un singolo valore integer viene esteso toobe una tupla di lunghezza corretta di hello con hello prima componenti uguale toohello specificato valore e tutti i hello tooone uguale a componenti rimanenti. valore predefinito di Hello è uno. numero totale di Hello delle mappe di funzionalità è prodotto hello dei componenti di hello di hello tupla. Hello factoring del numero totale di vari componenti hello determina la modalità di raggruppamento hello funzionalità mappare i valori nei nodi di destinazione hello. 
* **Pesi**: (facoltativo) definisce hello iniziale i pesi per il bundle di hello. il valore di Hello deve essere una tupla di valori a virgola mobile con una lunghezza hello numero kernel volte hello del pesi per kernel, come definito più avanti in questo articolo. pesi predefiniti Hello, vengono generati in modo casuale.  

Esistono due set di proprietà che controllano la spaziatura interna ovvero la proprietà come hello si escludono a vicenda:

* **Spaziatura interna**: (facoltativo) consente di determinare se un input hello deve essere completato utilizzando un **schema di riempimento predefinito**. il valore di Hello può essere un singolo valore booleano o può essere una tupla di valori booleani con una lunghezza di grado hello del bundle hello. Un singolo valore booleano è estesa toobe una tupla di lunghezza corretta di hello con tutti i componenti toohello uguale valore specificato. Se il valore di hello per una dimensione è True, origine hello viene riempita logicamente in tale dimensione con le applicazioni aggiuntive kernel toosupport di celle con valori zero, in modo che i nodi di centrale hello del kernel e il cognome di hello in tale dimensione siano hello prima e l'ultimo nodo in tale dimensione nel livello di origine hello. Pertanto, il numero di hello dei nodi "fittizi" in ogni dimensione è determinata automaticamente in toofit esattamente *(InputShape [d] - 1) / Stride [d] + 1* kernel nel livello di origine hello applicato un riempimento. Se il valore di hello per una dimensione è False, hello kernel sono definiti in modo che sia il numero di hello di nodi su ciascun lato che sono stati esclusi hello stesso (backup differenza tooa 1). il valore predefinito Hello di questo attributo è una tupla con tooFalse uguale di tutti i componenti.
* **UpperPad** e **LowerPad**: (facoltativo) specificare un controllo maggiore sulla quantità di hello di spaziatura interna toouse. **Importante:** questi attributi possono essere definiti se e solo se hello **Padding** proprietà precedente è ***non*** definito. i valori Hello devono essere tuple con valori integer con lunghezze di grado hello del bundle hello. Quando vengono specificati questi attributi, nodi "fittizi" vengono aggiunti toohello inferiore ed estremità superiore di ogni dimensione di hello livello di input. numero di nodi Hello aggiunto toohello inferiore e superiore termina in ogni dimensione è determinata da **LowerPad**[i] e **UpperPad**[i] rispettivamente. è necessario soddisfare tooensure che kernel corrispondenti nodi solo troppo "reali" e non troppo "fittizio" hello seguenti condizioni:
  * Ogni componente di**LowerPad** deve essere rigorosamente minore di KernelShape[d]/2. 
  * Ogni componente di **UpperPad** non deve essere maggiore di KernelShape[d]/2. 
  * il valore predefinito Hello di questi attributi è una tupla con too0 uguale di tutti i componenti. 

impostazione di Hello **Padding** = true consente in base alle esigenze di spaziatura come tookeep hello "center" del kernel hello all'interno di hello "real" di input. In questo caso matematiche hello un bit per il calcolo delle dimensioni di output di hello. In genere, l'output di hello dimensioni *D* viene calcolata come *D = (I - K) / S + 1*, dove *si* dimensioni input hello, *K* dimensioni kernel hello, *S* è stride hello, e  */*  è la divisione di interi (arrotondare per difetto). Se si imposta UpperPad = [1, 1], hello input dimensioni *si* in modo efficace è 29 e pertanto *D = (29-5) / 2 + 1 = 13*. Se **Padding** è true, *I* viene essenzialmente incrementato di *K - 1*, ovvero *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*. Specificando i valori per **UpperPad** e **LowerPad** ottenere un maggiore controllo riguardo hello padding rispetto ai casi si appena **Padding** = true.

Per altre informazioni sulle reti convoluzionali e le relative applicazioni, vedere gli articoli seguenti:  

* [http://deeplearning.net/tutorial/lenet.html ](http://deeplearning.net/tutorial/lenet.html)
* [http://research.microsoft.com/pubs/68920/icdar03.pdf](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a>Aggregazioni di pooling
Oggetto **pool bundle** applica connettività tooconvolutional simile di geometry, ma usa le funzioni predefinite toosource nodo valori tooderive hello nodo valore di destinazione. Le aggregazioni di pooling non hanno quindi stati sottoponibili a training (pesi o distorsioni). Supporto di bundle tutti hello convolutional attributi ad eccezione di pool **condivisione**, **MapCount**, e **pesi**.  

In genere, non si sovrappongano kernel hello riepilogati per unità del pool di connessioni adiacenti. Se Stride [d] è uguale tooKernelShape [d] in ogni dimensione, il livello di hello ottenuto è hello tradizionale locale pooling livello, che è comunemente usato in reti neurali convolutional. Ogni nodo di destinazione calcola hello massima o Media hello delle attività di hello del relativo kernel nel livello di origine hello.  

Hello di esempio seguente viene illustrato un bundle del pool di connessioni: 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* grado di Hello del bundle hello è 3 (lunghezza di tuple hello hello **InputShape**, **KernelShape**, e **Stride**). 
* Hello numero di nodi nel livello di origine hello è *5 * 24 * 24 = 2880*. 
* Questo è un livello di pooling locale tradizionale, perché **KernelShape** e **Stride** sono uguali. 
* Hello numero di nodi nel livello di destinazione hello è *5 * 12 * 12 = 1440*.  

Per altre informazioni sui livelli di pooling, vedere gli articoli seguenti:  

* [http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Sezione 3.4)
* [http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a>Aggregazioni di normalizzazione delle risposte
**Normalizzazione di risposta** è uno schema di normalizzazione locale che è stato introdotto da Geoffrey Hinton, et al., nel documento hello [ImageNet Classiﬁcation con complete reti neurali Convolutional](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf). Normalizzazione di risposta è una generalizzazione tooaid utilizzato nelle reti neurali. Quando un neurone la generazione di un livello molto elevato di attivazione, un livello di normalizzazione risposta locale elimina il livello di attivazione hello di hello circostanti neuroni. Ciò avviene tramite tre parametri (***α***, ***β***, e ***k***) e una struttura convoluzionale (o forma di vicinato). Ogni neurone nel livello di destinazione hello ***y*** corrisponde tooa neurone ***x*** nel livello di origine hello. livello di attivazione di Hello ***y*** viene fornito dalla seguente formula, hello in cui ***f*** hello livello di attivazione di un neurone, e ***Nx*** è kernel hello (o set di hello contenente hello neuroni di circa hello ***x***), come definito da hello convolutional struttura seguente:  

![][1]  

Bundle di normalizzazione risposta supportano tutti gli attributi convolutional hello, tranne **condivisione**, **MapCount**, e **pesi**.  

* Se kernel hello contiene neuroni hello stessa mappa come ***x***, lo schema di normalizzazione hello è tooas cui **stessa mappa normalizzazione**. toodefine stesso eseguire il mapping di normalizzazione, hello prima coordinata **InputShape** deve avere valore hello 1.
* Se il kernel hello contiene neuroni hello stessa posizione spaziale ***x***, senza neuroni hello in altri mapping, viene chiamato lo schema di normalizzazione hello **attraverso esegue il mapping di normalizzazione**. Questo tipo di normalizzazione risposta implementa una forma di inibizione laterale ispirata hello trovato tipo nel neuroni reali, la creazione di concorrenza per i livelli di attivazione big tra output neurone calcolato in mappe diverse. toodefine tra esegue il mapping di normalizzazione, coordinate prima hello deve essere un numero intero maggiore di uno e non è maggiore del numero di hello delle mappe e rest hello di coordinate hello deve avere il valore di hello 1.  

Poiché il bundle di normalizzazione risposta applicano un funzione predefinita toosource nodo valori toodetermine hello nodo valore di destinazione, non presentano alcun stato trainable (pesi o pregiudizi).   

**Avviso**: i nodi nel livello di destinazione hello hello corrispondono tooneurons che sono nodi centrale hello kernel hello. Ad esempio, se KernelShape [d] è dispari, verrà restituito *KernelShape [d] / 2* corrispondente nodo centrale kernel toohello. Se *KernelShape [d]* è pari, Trova nodo centrale hello *KernelShape [d] / 2-1*. Pertanto, se **Padding**[d] è False, hello prima e ultima hello *KernelShape [d] / 2* nodi non dispongono di nodi corrispondenti nel livello di destinazione hello. tooavoid questa situazione, definire **Padding** come [true, true,..., true].  

Inoltre toohello quattro attributi descritti in precedenza, il bundle di normalizzazione risposta anche supporto hello gli attributi seguenti:  

* **Alpha**: (obbligatorio) specifica un valore a virgola mobile che corrisponde a troppo***α*** nella formula precedente hello. 
* **Beta**: (obbligatorio) specifica un valore a virgola mobile che corrisponde a troppo***β*** nella formula precedente hello. 
* **Offset**: (facoltativo) specifica un valore a virgola mobile che corrisponde a troppo***k*** nella formula precedente hello. Per impostazione predefinita too1.  

Hello seguente definisce un raggruppamento di normalizzazione risposta mediante tali attributi:  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* livello di origine Hello include cinque mappe, ognuna con dimensione aof 12 x 12, per un totale di nodi 1440. 
* valore di Hello **KernelShape** indica che si tratta di un livello di normalizzazione mappa stessa, in cui le risorse di hello sono un 3x3 rettangolo. 
* il valore predefinito di Hello **Padding** è False, pertanto il livello di destinazione hello è solo 10 nodi in ogni dimensione. tooinclude un nodo nel livello di destinazione hello corrispondente nodo tooevery nel livello di origine di hello, aggiungere spaziatura interna = [true, true, true]; e modificare anche le dimensioni di hello di RN1 [5, 12, 12].  

## <a name="share-declaration"></a>Dichiarazione delle condivisioni
Net# supporta facoltativamente la definizione di più aggregazioni con pesi condivisi. pesi Hello qualsiasi due pacchetti di possono essere condiviso se le strutture sono hello stesso. la seguente sintassi Hello definisce bundle con pesi condivisi:  

    share-declaration:
        share    {    layer-list    }
        share    {    bundle-list    }
       share    {    bias-list    }

    layer-list:
        layer-name    ,    layer-name
        layer-list    ,    layer-name

    bundle-list:
       bundle-spec    ,    bundle-spec
        bundle-list    ,    bundle-spec

    bundle-spec:
       layer-name    =>     layer-name

    bias-list:
        bias-spec    ,    bias-spec
        bias-list    ,    bias-spec

    bias-spec:
        1    =>    layer-name

    layer-name:
        identifier  

Ad esempio, hello condivisione-dichiarazione seguente specifica i nomi dei livelli di hello, che indica che devono essere condivisa pesi sia pregiudizi:  

    Const {
      InputSize = 37;
      HiddenSize = 50;
    }
    input {
      Data1 [InputSize];
      Data2 [InputSize];
    }
    hidden {
      H1 [HiddenSize] from Data1 all;
      H2 [HiddenSize] from Data2 all;
    }
    output Result [2] {
      from H1 all;
      from H2 all;
    }
    share { H1, H2 } // share both weights and biases  

* le funzionalità di Hello input vengono suddivisi in due livelli di input con dimensioni uguali. 
* i livelli nascosto Hello per calcolare le funzionalità di livello superiore nei due livelli di input hello. 
* dichiarazione di Hello condivisione specifica che *H1* e *H2* deve essere calcolato in hello allo stesso modo dal loro rispettivi input.  

In alternativa, è possibile specificare questo concetto con due dichiarazioni delle condivisioni separate, come indicato di seguito:  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

È possibile utilizzare la forma breve hello solo quando i livelli di hello contengono un unico bundle. In generale, è possibile condividere solo quando si struttura rilevanti hello è identico, vale a dire che dispongono di hello stessa dimensione, geometry convolutional stesso e così via.  

## <a name="examples-of-net-usage"></a>Esempi di utilizzo di Net#
In questa sezione vengono forniti alcuni esempi di come è possibile utilizzare Net # livelli tooadd nascosto, definire modo hello che interagiscono con gli altri livelli livelli nascosti e compilare convolutional reti.   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a>Definire una semplice rete neurale personalizzata, ad esempio "Hello World"
Questo semplice esempio viene illustrato come toocreate un neurale rete modello che dispone di un singolo livello nascosto.  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

esempio Hello alcuni comandi di base viene illustrato come indicato di seguito:  

* prima riga Hello definisce livello input hello (denominato *dati*). Quando si utilizza hello **auto** (parola chiave), la rete neurale hello include automaticamente tutte le colonne di funzionalità negli esempi di input hello. 
* seconda riga Hello Crea livello nascosto hello. nome Hello *H* viene assegnato il livello nascosto toohello, che dispone di 200 nodi. Questo livello è completamente connesso toohello input.
* terza riga Hello definisce il livello di output di hello (denominato *O*), che contiene 10 nodi di output. Se la rete neurale hello viene utilizzata per la classificazione, c'è un nodo di output per ogni classe. parola chiave Hello **sigmoidale** indica che il livello di output toohello applicato hello output funzione.   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a>Definire più livelli nascosti: esempio obiettivo computer
Hello esempio seguente viene illustrato come toodefine una rete neurale leggermente più complessa con più livelli nascosti personalizzati.  

    // Define hello input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define hello first two hidden layers, using data only from hello Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define hello third hidden layer, which uses as source hello hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define hello output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

In questo esempio vengono illustrate diverse funzionalità del linguaggio di specifica di reti neurali hello:  

* struttura Hello ha due livelli di input, *pixel* e *metadati*.
* Hello *pixel* livello è un livello di origine per due bundle di connessione, con livelli di destinazione, *ByRow* e *ByCol*.
* Hello livelli *raccogliere* e *risultato* sono livelli di destinazione in più bundle di connessione.
* livello di output di Hello, *risultato*, è un livello di destinazione in due pacchetti di connessione, uno con hello di secondo livello nascosto (raccolta) come un livello di destinazione e hello altro con livello di input hello (metadati) come un livello di destinazione.
* Hello livelli nascosti, *ByRow* e *ByCol*, specificare la connettività filtrate tramite le espressioni del predicato. Più precisamente, hello nodo *ByRow* a [x, y] è nodi connessi toohello *pixel* che dispongono di x di coordinate, prima di hello primo indice toohello uguale coordinate del nodo. Analogamente, hello nodo *ByCol a [x, y] è nodi connessi toohello _Pixels* che dispongono di coordinate indice secondo di hello all'interno di uno di coordinate a seconda del nodo hello, y.  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a>Definire una rete per la classificazione multiclasse convoluzionale: esempio di riconoscimento cifra
definizione di Hello di hello seguente rete è progettato toorecognize numeri e illustra alcune tecniche avanzate per la personalizzazione di una rete neurale.  

    input Image [29, 29];
    hidden Conv1 [5, 13, 13] from Image convolve 
    {
       InputShape  = [29, 29];
       KernelShape = [ 5,  5];
       Stride      = [ 2,  2];
       MapCount    = 5;
    }
    hidden Conv2 [50, 5, 5]
    from Conv1 convolve 
    {
       InputShape  = [ 5, 13, 13];
       KernelShape = [ 1,  5,  5];
       Stride      = [ 1,  2,  2];
       Sharing     = [false, true, true];
       MapCount    = 10;
    }
    hidden Hid3 [100] from Conv2 all;
    output Digit [10] from Hid3 all;  


* struttura Hello ha un solo livello di input, *immagine*.
* parola chiave Hello **convolve** indica che i livelli di hello denominati *Conv1* e *Conv2* convolutional livelli. Ognuna di queste dichiarazioni di livello è seguito da un elenco di attributi convoluzione hello.
* nascosto di Hello net dispone di un terzo livello, *Hid3*, che è completamente connesso toohello secondo livello nascosto, *Conv2*.
* livello di output di Hello, *cifra*, è connessa toohello solo terzo livello nascosto, *Hid3*. parola chiave Hello **tutti** indica il livello di output di hello è completamente connesso troppo*Hid3*.
* Hello grado del convoluzione hello è tre (lunghezza di tuple hello hello **InputShape**, **KernelShape**, **Stride**, e **condivisione**). 
* numero di Hello di pesi per kernel è *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26. Oppure 26 * 50 = 1300*.
* È possibile calcolare nodi hello in ogni livello nascosto, come indicato di seguito:
  * **NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.
  * **NodeCount**\[1] = (13 - 5) / 2 + 1 = 5. 
  * **NodeCount**\[2] = (13 - 5) / 2 + 1 = 5. 
* Hello numero totale di nodi può essere calcolato tramite hello dichiarato dimensionalità di hello dei livelli, [50, 5, 5], come indicato di seguito:  ***MapCount** * **NodeCount** \[ 0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*
* Poiché **condivisione**[d] è impostato su False solo per *d = = 0*, numero di hello del kernel è  ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*. 

## <a name="acknowledgements"></a>Riconoscimenti
Hello linguaggio Net # per personalizzare l'architettura di hello delle reti neurali è stato sviluppato da Microsoft da Shon Katzenberger (Architect, Machine Learning) e Alexey Kamenev (tecnico del Software, Microsoft Research). Viene utilizzata internamente per machine learning progetti e applicazioni, da analitica tootext rilevamento di immagine. Per ulteriori informazioni, vedere [reti neurali in Machine Learning di Azure - introduzione tooNet #](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

