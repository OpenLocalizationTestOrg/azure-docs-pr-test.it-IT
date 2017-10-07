---
title: i moduli R personalizzati in Azure Machine Learning aaaAuthor | Documenti Microsoft
description: Guida introduttiva alla creazione di moduli R personalizzati in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a>Creare moduli R personalizzati in Azure Machine Learning
Questo argomento viene descritto come tooauthor e distribuire un modulo R personalizzato in Azure Machine Learning. Viene spiegato che cosa sono i moduli R personalizzati e quali sono i file toodefine utilizzato li. Viene illustrato come tooconstruct hello file che definiscono un modulo e come tooregister hello modulo per la distribuzione in un'area di lavoro di Machine Learning. Hello elementi e attributi utilizzati nella definizione di hello del modulo personalizzata hello vengono descritti più dettagliatamente. Come viene anche illustrata toouse ausiliario funzionalità e i file e più output. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a>In cosa consiste un modulo R personalizzato?
Oggetto **modulo personalizzato** è un modulo definito dall'utente che può essere caricato tooyour dell'area di lavoro ed eseguito come parte di un esperimento di Azure Machine Learning. Un **modulo R personalizzato** è un modulo personalizzato che esegue una funzione R definita dall'utente. **R** è un linguaggio di programmazione per il calcolo e statistico e la grafica ampiamente usato in campo statistico e di analisi dei dati per l'implementazione degli algoritmi. R è attualmente hello unica lingua supportata in moduli personalizzati, ma il supporto per lingue aggiuntive è pianificata per le versioni future.

I moduli personalizzati hanno **stato di prima classe** in Azure Machine Learning nel senso hello che possono essere usati come qualsiasi altro modulo. Possono essere eseguiti con altri moduli, inclusi nelle visualizzazioni o negli esperimenti pubblicati. È necessario controllare algoritmo hello implementato dal modulo hello, hello toobe porte di input e output utilizzati, hello modellazione parametri e altri comportamenti di runtime diversi. Un esperimento che contiene i moduli personalizzati può essere pubblicato anche in hello Cortana Intelligence Gallery per la condivisione semplice.

## <a name="files-in-a-custom-r-module"></a>File in un modulo R personalizzato
Un modulo R personalizzato viene definito da un file ZIP che contiene almeno due file:

* Oggetto **file di origine** che implementa una funzione hello R esposta dal modulo hello
* Un **file di definizione XML** che descrive l'interfaccia del modulo personalizzata hello

I file ausiliari aggiuntivi possono essere inclusi anche nel file con estensione zip hello che fornisce funzionalità di cui è possibile accedere dal modulo personalizzato hello. Questa opzione viene trattata in hello **argomenti** fa parte della sezione di riferimento hello **elementi nel file di definizione XML hello** hello avvio rapido esempio seguente.

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a>Esempio di guida introduttiva: definire, creare un pacchetto e registrare un modulo R personalizzato
Questo esempio viene illustrato come tooconstruct hello i file necessari per un modulo R personalizzato, inserirle in un pacchetto in un file zip e quindi registrare hello modulo nell'area di lavoro di Machine Learning. Hello esempio pacchetti di esempio con estensione zip può essere scaricato da [CustomAddRows.zip scaricare file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).

## <a name="hello-source-file"></a>file di origine Hello
Si consideri ad esempio hello un **personalizzato Add Rows** modulo che modifica l'implementazione standard di hello di hello **Add Rows** modulo utilizzato tooconcatenate righe (osservazioni) da due set di dati (frame di dati). Hello standard **Add Rows** modulo aggiunge righe hello di hello secondo set di dati input toohello fine hello primo input set di dati utilizzando hello `rbind` algoritmo. Hello personalizzato `CustomAddRows` funzione Analogamente accetta due set di dati, ma accetta inoltre un parametro booleano swap come un input aggiuntivo. Se il parametro di scambio hello è troppo**FALSE**, restituisce hello stesso set di dati come hello implementazione standard. Tuttavia, se il parametro di scambio hello è **TRUE**, la funzione hello aggiunge invece di righe del primo set di dati input toohello fine hello secondo set di dati. file CustomAddRows.R Hello che contiene l'implementazione di hello di hello R `CustomAddRows` funzione esposta da hello **personalizzato Add Rows** modulo ha hello seguente codice R.

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a>file di definizione XML Hello
tooexpose questo `CustomAddRows` funzione come un modulo di Azure Machine Learning, un file di definizione XML deve essere creato toospecify come hello **personalizzato Add Rows** modulo debba aspetto e comportamento. 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


È toonote critici che hello valore hello **id** gli attributi di hello **Input** e **Arg** elementi nel file XML di hello devono corrispondere i nomi dei parametri di funzione hello di hello R codice nel file CustomAddRows.R hello esattamente: (*dataset1*, *dataset2*, e *scambio* nell'esempio hello). Analogamente, hello valore hello **entryPoint** attributo di hello **Language** elemento deve corrispondere esattamente a nome hello della funzione hello nello script R hello: (*CustomAddRows* Nell'esempio hello). 

Al contrario, hello **id** attributo per hello **Output** elemento non corrisponde a variabili tooany nello script R hello. Quando più di un output è obbligatorio, restituire semplicemente un elenco dalla funzione hello R con risultati inseriti *in hello stesso ordine* come **output** elementi vengono dichiarati nel file XML di hello.

### <a name="package-and-register-hello-module"></a>Pacchetto e registrare il modulo di hello
Salvare questi file come due *CustomAddRows.R* e *CustomAddRows.xml* e quindi zip hello due file insieme in un *CustomAddRows.zip* file.

Nell'area di lavoro Machine Learning, dell'area di lavoro tooyour andare in hello Machine Learning Studio, fare clic su hello tooregister **+ nuovo** pulsante nella parte inferiore di hello **modulo -> dal pacchetto ZIP** tooupload nuovo Hello **personalizzato Add Rows** modulo.

![Caricamento file ZIP](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

Hello **personalizzato Add Rows** modulo è ora pronto toobe accedere tramite gli esperimenti di Machine Learning.

## <a name="elements-in-hello-xml-definition-file"></a>Elementi nel file di definizione XML hello
### <a name="module-elements"></a>Elementi dei moduli
Hello **modulo** elemento è toodefine usato un modulo personalizzato nel file XML di hello. Si possono definire più moduli in un file XML usando più elementi **Module** . Ogni modulo nell'area di lavoro deve avere un nome univoco. Registrare un modulo personalizzato con hello stesso nome di un modulo personalizzato esistente e sostituisce un modulo esistente hello con hello uno nuovo. Moduli personalizzati, tuttavia, possono essere registrato con hello stesso nome di un modulo di Azure Machine Learning esistente. Se in tal caso, sono visualizzate in hello **personalizzato** categoria della tavolozza modulo hello.

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


All'interno di hello **modulo** elemento, è possibile specificare due elementi facoltativi aggiuntivi:

* un **proprietario** elemento che viene incorporata nel modulo hello  
* un **descrizione** elemento che contiene il testo che viene visualizzato nella Guida rapida per il modulo hello e quando si posiziona su modulo hello in hello dell'interfaccia utente di Machine Learning.

Regole per i limiti di caratteri in elementi modulo hello:

* valore di hello Hello **nome** attributo hello **modulo** elemento non deve superare i 64 caratteri. 
* contenuto di hello Hello **descrizione** elemento non deve superare i 128 caratteri.
* contenuto di hello Hello **proprietario** elemento non deve superare i 32 caratteri.

I risultati di un modulo possono essere deterministici o nondeterministic.* * per impostazione predefinita, tutti i moduli vengono considerati toobe deterministica. Vale a dire, dato un set di parametri di input e di dati rimane invariato, modulo hello deve restituire hello stesso risultati eacRAND o functionh ora che viene eseguito. Questo comportamento, Azure Machine Learning Studio riesegue solo moduli contrassegnati come deterministica se un parametro o i dati di input hello sono stato modificato. Restituzione di risultati memorizzati nella cache di hello fornisce inoltre quantità velocizzare l'esecuzione di esperimenti.

Sono disponibili funzioni che sono non deterministiche, ad esempio RAND o una funzione che restituisce hello data o ora. Se il modulo utilizza una funzione non deterministica, è possibile specificare tale modulo hello è non deterministico per l'impostazione facoltativa hello **isDeterministic** attributo troppo**FALSE**. In questo modo si assicura che modulo hello viene eseguito di nuovo ogni volta che viene eseguito l'esperimento hello, anche se hello modulo parametri di input e non sono stati modificati. 

### <a name="language-definition"></a>Definizione lingua
Hello **Language** elemento nel file di definizione XML viene utilizzato toospecify hello modulo personalizzato language. R è attualmente hello solo lingua supportata. valore di hello Hello **sourceFile** attributo deve essere il nome di hello del file hello R contenente toocall funzione hello quando viene eseguito il modulo hello. Questo file deve essere parte del pacchetto zip hello. valore di hello Hello **entryPoint** attributo hello nome di funzione hello chiamata e deve corrispondere a una funzione valida definita con nel file di origine hello.

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a>Porte
Hello porte di input e outpue per un modulo personalizzato vengono specificate in elementi figlio di hello **porte** sezione del file di definizione XML di hello. ordine di Hello di questi elementi determina hello layout esperti (UX) da parte degli utenti. primo elemento figlio di Hello **input** o **output** elencati in hello **porte** elemento del file XML di hello diventa porta di input a sinistra hello in hello UX. di Machine Learning
Ogni input e output porta potrebbe essere facoltativa **descrizione** elemento figlio che specifica il testo di hello visualizzato quando si posiziona il cursore di mouse hello su porta hello in hello dell'interfaccia utente di Machine Learning.

**Regole porte**:

* Il numero massimo di **porte di input e di output** è 8 per ciascuno.

### <a name="input-elements"></a>Elementi di input
Porte di input consentono di area di lavoro e la funzione di toopass dati tooyour R. Hello **tipi di dati** che sono supportati per le porte di input sono i seguenti: 

**DataTable:** questo tipo viene passato a funzione tooyour R come un data.frame. In realtà, qualsiasi tipo (ad esempio, file CSV o i file ARFF) è supportati da Machine Learning e che è compatibili con **DataTable** sono data.frame tooa convertito automaticamente. 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

Hello **id** associata a ogni attributo **DataTable** porta di input deve essere un valore univoco e questo valore deve corrispondere il parametro nella funzione di R denominato corrispondente.
Parametro facoltativo **DataTable** le porte che non vengono passate come input in un esperimento avere valore hello **NULL** passato toohello R (funzione) e porte zip facoltativo vengono ignorate se hello input non è connesso. Hello **isOptional** attributo è facoltativo per entrambi hello **DataTable** e **Zip** tipi e viene *false* per impostazione predefinita.

**Zip:** i moduli personalizzati possono accettare un file ZIP come input. Questo input è decompresso nella directory di lavoro hello R della funzione

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

Per i moduli R personalizzati, id hello per una porta di Zip è toomatch eventuali parametri della funzione hello R. Infatti, file zip hello viene automaticamente estratto toohello R directory di lavoro.

**Regole di input:**

* valore di hello Hello **id** attributo di hello **Input** elemento deve essere un nome di variabile valido di R.
* valore di hello Hello **id** attributo di hello **Input** elemento non deve essere più lungo di 64 caratteri.
* valore di hello Hello **nome** attributo di hello **Input** elemento non deve essere più lungo di 64 caratteri.
* contenuto di hello Hello **descrizione** elemento non deve essere più lungo di 128 caratteri
* valore di hello Hello **tipo** attributo di hello **Input** l'elemento deve essere *Zip* o *DataTable*.
* valore hello Hello **isOptional** attributo di hello **Input** elemento non è necessario (e *false* per impostazione predefinita, quando non è specificato); ma se viene specificato, deve essere *true* o *false*.

### <a name="output-elements"></a>Elementi di output
**Porte di output standard:** le porte di Output vengono mappate toohello i valori restituiti dalla funzione R, che può quindi essere usato dai moduli successivi. *DataTable* è tipo di porta di output standard solo hello attualmente supportato. Il supporto per *Learners* e *Transforms* è di prossima introduzione. Un output *DataTable* è definito come:

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

Per gli output in moduli R personalizzati, hello valore hello **id** attributo non è in uno script R hello toocorrespond con elementi, ma deve essere univoco. Per un output di un modulo singolo, valore restituito di hello dalla funzione hello R deve essere un *data.frame*. In ordine toooutput più di un oggetto di un tipo di dati supportati, porte di output appropriato hello necessario toobe specificato nel file di definizione XML hello e oggetti hello necessitano toobe restituito come un elenco. gli oggetti di output di Hello vengono assegnati porte toooutput da tooright a sinistra, indicare l'ordine di hello in cui gli oggetti di hello vengono inseriti nell'elenco restituito hello.

Ad esempio, se si desidera hello toomodify **personalizzato Add Rows** toooutput modulo hello originale due set di dati, *dataset1* e *dataset2*, inoltre aggiunti a un nuovo toohello set di dati, *dataset*, (in ordine da sinistra tooright, come: *dataset*, *dataset1*, *dataset2*), quindi definire hello l'output nel file CustomAddRows.xml hello porte come indicato di seguito:

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


E restituire l'elenco di hello degli oggetti in un elenco nella sequenza corretta hello 'CustomAddRows.R':

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

**Output di visualizzazione:** è inoltre possibile specificare una porta di output di tipo *visualizzazione*, visualizzare l'output di hello dall'output di console e dispositivo di grafica hello R. Questa porta non fa parte dell'output di hello R funzione e non interferire con l'ordine di hello di hello altri tipi di porta di output. aggiungere una visualizzazione porta toohello personalizzato i moduli, tooadd un **Output** elemento con un valore di *visualizzazione* per relativo **tipo** attributo:

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

**Regole di output:**

* valore di hello Hello **id** attributo di hello **Output** elemento deve essere un nome di variabile valido di R.
* valore di hello Hello **id** attributo di hello **Output** elemento non deve essere più di 32 caratteri.
* valore di hello Hello **nome** attributo di hello **Output** elemento non deve essere più lungo di 64 caratteri.
* valore di hello Hello **tipo** attributo di hello **Output** l'elemento deve essere *visualizzazione*.

### <a name="arguments"></a>Argomenti
Dati aggiuntivi possono essere passati toohello R funzione tramite i parametri di modulo che sono definiti in hello **argomenti** elemento. Questi parametri vengono visualizzati nel riquadro delle proprietà all'estrema destra hello di hello dell'interfaccia utente di Machine Learning quando è selezionata modulo hello. Gli argomenti possono essere uno qualsiasi dei tipi di hello supportata o è possibile creare un enumeratore personalizzato quando necessario. Toohello simile **porte** elementi **argomenti** gli elementi possono avere un parametro facoltativo **descrizione** elemento che specifica il testo hello visualizzato quando si passa il mouse hello nel nome del parametro hello.
È possibile aggiungere proprietà facoltativa di un modulo, ad esempio defaultValue minValue e maxValue argomento tooany come attributi tooa **proprietà** elemento. Proprietà valide per hello **proprietà** elemento dipendono dal tipo di argomento hello e sono descritti con tipi di argomento hello è supportato nella sezione successiva hello. Gli argomenti con hello **isOptional** impostata troppo**"true"** non richiedono hello utente tooenter un valore. Se l'argomento toohello non viene fornito un valore, quindi hello argomento non viene passato toohello funzione di punto di ingresso. Gli argomenti della funzione di punto di ingresso hello toobe necessità facoltativo gestite in modo esplicito dalla funzione hello, ad esempio assegnato un valore predefinito null nella definizione di funzione di punto di ingresso hello. Un argomento facoltativo imporrà solo hello altri vincoli di argomento, ad esempio min o max, se viene fornito un valore dall'utente hello.
Come con input e output, è fondamentale che ciascun parametro hello sono associati valori di id univoco. Nel nostro avvio rapido esempio hello associata/parametro id è stato *scambio*.

### <a name="arg-element"></a>Elemento Arg
Un parametro di modulo viene definito utilizzando hello **Arg** elemento figlio di hello **argomenti** sezione del file di definizione XML di hello. Come con gli elementi figlio di hello in hello **porte** sezione, hello l'ordine dei parametri in hello **argomenti** sezione definisce il layout di hello rilevato in hello UX. Hello parametri vengono visualizzati dall'alto verso il basso in hello dell'interfaccia utente in hello stesso ordine in cui sono definite nel file XML di hello. tipi di Hello supportati da Machine Learning per i parametri sono elencati di seguito. 

**int** : parametro di tipo Integer (32 bit).

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* *Proprietà facoltative*: **min**, **max**, **default** e **isOptional**

**double** : parametro di tipo doppio.

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* *Proprietà facoltative*: **min**, **max**, **default** e **isOptional**

**bool** : parametro booleano rappresentato da una casella di controllo nell'esperienza utente.

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* *Proprietà facoltative*: **default** (false se non impostato)

**string**: stringa standard

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* *Proprietà facoltative*: **default** e **isOptional**

**ColumnPicker**: parametro di selezione della colonna. Questo tipo come un selettore di colonna in hello UX. Hello **proprietà** elemento è utilizzato toospecify qui hello id della porta hello da cui vengono selezionate le colonne, in cui deve essere il tipo di porta di hello destinazione *DataTable*. il risultato di Hello di selezione della colonna hello viene passato toohello R funzione come un elenco di stringhe contenente i nomi di colonna hello selezionato. 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* *Proprietà obbligatorie*: **portId** -corrispondenze hello id di un elemento di Input con tipo *DataTable*.
* *Proprietà facoltative*:
  
  * **allowedTypes** -da cui è possibile selezionare i tipi di colonna hello filtri. I valori validi includono: 
    
    * Numeric
    * Boolean
    * Categorical
    * string
    * Etichetta
    * Funzionalità
    * Score
    * Tutti
  * **predefinito** -selezioni predefinito valido per il selettore di colonna hello includono: 
    
    * Nessuno
    * NumericFeature
    * NumericLabel
    * NumericScore
    * NumericAll
    * BooleanFeature
    * BooleanLabel
    * BooleanScore
    * BooleanAll
    * CategoricalFeature
    * CategoricalLabel
    * CategoricalScore
    * CategoricalAll
    * StringFeature
    * StringLabel
    * StringScore
    * StringAll
    * AllLabel
    * AllFeature
    * AllScore
    * Tutti

**DropDown**: elenco enumerato specificato dall'utente (elenco a discesa). gli elementi di elenco a discesa Hello vengono specificati all'interno di hello **proprietà** elemento utilizzando un **elemento** elemento. Hello **id** per ogni **elemento** deve essere univoco e una variabile di R valida. valore di hello Hello **nome** di un **elemento** agisce come testo hello e valore hello che viene passato a funzione toohello R.

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* *Proprietà facoltative*:
  * **predefinito** : hello valore per proprietà predefinita hello deve corrispondere a un valore di id da una delle hello **elemento** elementi.

### <a name="auxiliary-files"></a>File ausiliari
Qualsiasi file inserito nel file ZIP modulo personalizzato è toobe corso disponibile per l'utilizzo durante la fase di esecuzione. Vengono mantenute le strutture di directory presenti. Ciò significa che funziona acquisti file hello stesso in locale e in esecuzione in Azure Machine Learning. 

> [!NOTE]
> Si noti che tutti i file sono estratti too'src' directory in modo da tutti i percorsi devono avere ' src /' prefisso.
> 
> 

Si supponga, ad esempio, si desidera tooremove tutte le righe con NAs del set di dati hello e rimuovere anche tutte le righe duplicate, prima l'output in CustomAddRows e già creato una funzione di R che vengono eseguite in un file RemoveDupNARows.R:

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
Si può ottenere file ausiliario hello RemoveDupNARows.R nella funzione CustomAddRows hello:

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

Quindi, caricare il file ZIP contenente 'CustomAddRows.R', 'CustomAddRows.xml' e 'RemoveDupNARows.R' come modulo R personalizzato.

## <a name="execution-environment"></a>Ambiente di esecuzione
ambiente di esecuzione Hello per lo script R hello utilizza hello stessa versione di R hello **Execute R Script** modulo e può utilizzare hello stesso predefinito pacchetti. Inoltre, è possibile aggiungere ulteriori R pacchetti tooyour modulo personalizzato includendoli nel pacchetto zip di hello modulo personalizzato. È sufficiente caricare i pacchetti nello script R come si farebbe nel proprio ambiente R. 

**Limitazioni dell'ambiente di esecuzione hello** includono:

* Sistema di file non-persistent: i file scritti quando viene eseguito il modulo personalizzato di hello non sono persistenti tra più esecuzioni di hello stesso modulo.
* Nessun accesso alla rete

