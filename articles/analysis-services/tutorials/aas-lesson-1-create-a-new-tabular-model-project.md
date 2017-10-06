---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 1: creare un nuovo progetto di modello tabulare | Descrizione di "Microsoft Docs: viene descritto come toocreate un nuovo Azure Analysis Services progetto tutorial. servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 01/06/2017: owend
---
# <a name="lesson-1-create-a-tabular-model-project"></a>Lezione 1: Creare un progetto di modello tabulare

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione, utilizzare SQL Server Data Tools (SSDT) toocreate un nuovo progetto di modello tabulare a livello di compatibilità 1400 hello. Dopo aver creato il nuovo progetto, è possibile iniziare ad aggiungere i dati e a lavorare al modello. In questa lezione offre inoltre un breve introduzione toohello creazione di modelli tabulari in SSDT ambiente.  
  
Stimato toocomplete ora questa lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
In questo argomento è hello prima lezione di un'esercitazione sulla creazione di modelli tabulari. toocomplete questa lezione, esistono diversi prerequisiti, è necessario toohave sul posto. vedere, più toolearn [Azure Analysis Services - esercitazione Adventure Works](../tutorials/aas-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Creare un nuovo progetto di modello tabulare  
  
#### <a name="toocreate-a-new-tabular-model-project"></a>toocreate un nuovo progetto di modello tabulare  
  
1.  In SSDT, su hello **File** menu, fare clic su **New** > **progetto**.  
  
2.  In hello **nuovo progetto** finestra di dialogo espandere **installato** > **Business Intelligence** > **diAnalysisServices**, quindi fare clic su **progetto tabulare di Analysis Services**.  
  
3.  In **nome**, tipo **AW Internet Sales**e quindi specificare un percorso per i file di progetto hello.  
  
    Per impostazione predefinita, **Nome soluzione** hello stesso come nome del progetto hello; tuttavia, è possibile digitare un nome diverso per la soluzione.  
  
4.  Fare clic su **OK**.  
  
5.  In hello **progettazione di modelli tabulari** nella finestra di dialogo **integrato dell'area di lavoro**.  
  
    area di lavoro Hello ospita un database modello tabulare con hello stesso nome come progetto di hello durante la creazione di modelli. Area di lavoro integrata significa che SSDT utilizza un'istanza predefinita, eliminando l'esigenza di hello tooinstall un'istanza del server Analysis Services separata solo per la creazione di modelli.
      
6.  In **Livello di compatibilità** selezionare **SQL Server 2017 / Azure Analysis Services (1400)**.   
 
    ![aas-lesson1-tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    Se SQL Server 2017 / Azure Analysis Services (1400) non viene visualizzato nella casella di riepilogo a livello compatibilità hello, non si utilizza più recente di SQL Server Data Tools hello. versione più recente di hello tooget, vedere [installare SQL Server Data tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-hello-ssdt-tabular-model-authoring-environment"></a>Informazioni sul modello tabulare SSDT hello ambiente di creazione  
Dopo aver creato un nuovo progetto di modello tabulare, prendiamo un istante tooexplore hello modello tabulare in SSDT ambiente di creazione.  
  
Il progetto creato viene aperto in SSDT. Sul lato destro, in hello **Esplora modelli tabulari**, vedrai una visualizzazione albero di oggetti hello nel modello. Poiché non sono stati ancora importati i dati, cartelle hello sono vuote. È possibile fare doppio clic su un oggetto azioni tooperform cartella simile toohello sulla barra dei menu. Mentre si esamina questa esercitazione, utilizzare hello Esplora modelli tabulari toonavigate diversi oggetti nel progetto di modello.

![aas-lesson1-tme](../tutorials/media/aas-lesson1-tme.png)

Fare clic su hello **Esplora** scheda. In questa scheda è possibile visualizzare il file **Model.bim**. Se non viene visualizzato hello finestra di progettazione toohello a sinistra (hello finestra vuota con la scheda Model.bim hello), in **Esplora**in **progetto AW Internet Sales**, fare doppio clic su hello  **Model.bim** file. file Model.bim Hello contiene i metadati di hello per il progetto di modello. 

![aas-lesson1-se](../tutorials/media/aas-lesson1-se.png)
  
Fare clic su **Model.bim**. In hello **proprietà** è visualizzare hello proprietà dei modelli più importanti delle quali è hello **modalità DirectQuery** proprietà. Questa proprietà specifica se il modello di hello viene distribuito in modalità In-Memory (disattivata) o in modalità DirectQuery (attivata). Per questa esercitazione, il modello viene creato e distribuito in modalità In-Memory.

![aas-lesson1-properties](../tutorials/media/aas-lesson1-properties.png)
  
Quando si crea un progetto di modello, determinate proprietà del modello vengono impostate automaticamente in base toohello le impostazioni di modellazione dati che possono essere specificate in hello **strumenti** menu > **opzioni** la finestra di dialogo. Proprietà Server dell'area di lavoro, memorizzazione area di lavoro e Backup dei dati specificare come e dove hello dell'area di lavoro (il modello di creazione di database) viene eseguito il backup conservati in memoria e il database incorporato. È possibile modificare queste impostazioni in un secondo momento, se necessario, ma per ora, lasciarle come sono.  

In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **AW Internet Sales** (progetto) e quindi scegliere **Proprietà**. Hello **pagine delle proprietà di AW Internet Sales** viene visualizzata la finestra di dialogo. Alcune di queste proprietà verranno impostate in un secondo momento, durante la distribuzione del modello.  
  
Durante l'installazione di SSDT, nuove voci di menu sono stati aggiunti toohello ambiente di Visual Studio. Fare clic su hello **modello** menu. Da qui è possibile importare i dati, aggiornare i dati dell'area di lavoro, esplorare il modello in Excel, creare prospettive e ruoli, vista modello selezionare hello e impostare le opzioni di calcolo. Fare clic su hello **tabella** menu. Da questo menu è possibile creare e gestire relazioni, specificare le impostazioni della tabella data, creare partizioni e modificare le proprietà della tabella. Se si fa clic hello **colonna** menu, è possibile aggiungere ed eliminare colonne in una tabella, bloccare le colonne e specificare l'ordinamento. SSDT aggiunge inoltre alcuni barra toohello pulsanti. Più utile è hello Somma automatica funzionalità toocreate una misura di aggregazione standard per una colonna selezionata. Altri pulsanti della barra degli strumenti offrono accesso rapido toofrequently funzionalità e i comandi.  
  
Esplorare alcune finestre di dialogo hello e i percorsi per i modelli tabulari varie funzionalità tooauthoring specifico. Mentre alcuni elementi non sono ancora attivi, è possibile ottenere una buona idea dell'ambiente di creazione di modelli tabulari hello.  
  

## <a name="whats-next"></a>Passaggi successivi
[Lezione 2: Ottenere i dati](../tutorials/aas-lesson-2-get-data.md).

  
  
  
