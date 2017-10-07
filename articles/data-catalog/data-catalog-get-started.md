---
title: aaaGet avviato con il catalogo dati | Documenti Microsoft
description: "Esercitazione end-to-end presentazione scenari hello e le funzionalità di Azure Data Catalog."
documentationcenter: 
services: data-catalog
author: steelanddata
manager: jhubbard
editor: 
tags: 
ms.assetid: 03332872-8d84-44a0-8a78-04fd30e14b18
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 7652918b5a8254f5cff9e32d77b1fd3e1bf59d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-catalog"></a>Introduzione ad Azure Data Catalog
Azure Data Catalog è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per asset di dati aziendali. Per una panoramica dettagliata, vedere [Definizione di Azure Data Catalog](data-catalog-what-is-data-catalog.md).

Questa esercitazione consente di iniziare a usare Azure Data Catalog. L'esecuzione hello seguire le procedure seguenti in questa esercitazione:

| Procedura | Descrizione |
|:--- |:--- |
| [Effettuare il provisioning del catalogo dati](#provision-data-catalog) |In questa procedura si effettuerà il provisioning o la configurazione di Azure Data Catalog. Eseguire questo passaggio solo se il catalogo di hello non è stato impostato prima. È possibile avere solo un catalogo dati per ogni organizzazione (dominio di Microsoft Azure Active Directory), anche se all'account di Azure sono associate più sottoscrizioni. |
| [Registrare gli asset di dati](#register-data-assets) |In questa procedura, registrare gli asset di dati dal database di esempio AdventureWorks2014 hello catalogo dati hello. La registrazione è il processo di hello di estrazione dei metadati strutturali chiavi, ad esempio nomi, tipi e i percorsi di origine di dati hello e la copia di quel catalogo toohello metadati. Hello origine dati e gli asset di dati rimangono in cui sono, ma i metadati di hello vengono utilizzati da hello catalogo toomake più facilmente individuabili e comprensibile. |
| [Individuare gli asset di dati](#discover-data-assets) |In questa procedura, si utilizza hello Azure Data Catalog toodiscover portale asset di dati sono stati registrati nel passaggio precedente hello. Dopo la registrazione di un'origine dati con Azure Data Catalog, dei metadati sono indicizzato dai servizio hello in modo che gli utenti possono cercare dati hello che necessari. |
| [Annotare gli asset di dati](#annotate-data-assets) |In questa procedura, si forniscono le annotazioni (informazioni quali le descrizioni, tag, la documentazione o esperti) per hello asset di dati. Queste informazioni integrano hello metadati estratti dall'origine dati hello e più comprensibile toomore utenti dell'origine dati di hello toomake. |
| [Connettersi toodata Asset](#connect-to-data-assets) |In questa procedura, gli asset di dati verranno aperti in strumenti client integrati (come Excel e SQL Server Data Tools) e in uno strumento non integrato (SQL Server Management Studio). |
| [Gestire gli asset di dati](#manage-data-assets) |In questa procedura verrà configurata la sicurezza per gli asset di dati. Catalogo dati non è possibile accedere ai dati di toohello stesso. proprietario Hello dell'origine dati hello controlla l'accesso ai dati. <br/><br/> Con il catalogo dati, è possibile individuare le origini dati e hello vista **metadati** relative origini toohello registrate nel catalogo di hello. Possono esistere situazioni, tuttavia, in cui le origini dati devono essere visibile toospecific solo utenti o toomembers di gruppi specifici. Per questi scenari, è possibile utilizzare la proprietà tootake catalogo dati di asset di dati registrati all'interno di hello catalogo e controllo hello la visibilità degli asset hello che si è proprietari. |
| [Rimuovere gli asset di dati](#remove-data-assets) |In questa procedura viene illustrato come asset di dati tooremove da hello catalogo dati. |

## <a name="tutorial-prerequisites"></a>Prerequisiti per l'esercitazione
### <a name="azure-subscription"></a>Sottoscrizione di Azure
tooset di Azure Data Catalog, è necessario essere proprietario di hello o Comproprietario di una sottoscrizione di Azure.

Le sottoscrizioni di Azure consentono di organizzare le risorse del servizio di accesso toocloud come Azure Data Catalog. Consentono inoltre di controllare come l'utilizzo delle risorse viene segnalato, fatturato e pagato. Ogni sottoscrizione può disporre di un’impostazione di fatturazione e pagamento diversa, in modo da poter avere sottoscrizioni e piani diversi per reparto, progetto, ufficio regionale e così via. Ogni servizio cloud appartiene tooa sottoscrizione ed è necessario toohave una sottoscrizione prima di configurare Azure Data Catalog. vedere, più toolearn [gestire account, sottoscrizioni e ruoli amministrativi](../active-directory/active-directory-how-subscriptions-associated-directory.md).

Se non è disponibile una sottoscrizione, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/) .

### <a name="azure-active-directory"></a>Azure Active Directory
tooset di Azure Data Catalog, è necessario essere connessi con un account utente di Azure Active Directory (Azure AD). È necessario essere proprietario di hello o Comproprietario di una sottoscrizione di Azure.  

Azure AD fornisce un modo semplice per le identità di business toomanage e l'accesso, sia nel cloud hello e locali. È possibile usare un singola aziendale o dell'istituto di istruzione account toosign nel cloud tooany o applicazione web locale. Azure Data Catalog Usa Azure AD tooauthenticate Accedi. vedere, più toolearn [che cos'è Azure Active Directory](../active-directory/active-directory-whatis.md).

### <a name="azure-active-directory-policy-configuration"></a>Configurazione dei criteri di Azure Active Directory
Può verificarsi una situazione in cui è possibile accedere al portale di Azure Data Catalog toohello, ma quando si tenta di toosign nello strumento di registrazione origine dati toohello, che si verifichi un messaggio di errore che impedisce l'accesso. Questo errore può verificarsi quando si è nella rete aziendale hello o quando ci si connette dalla rete aziendale hello esterno.

utilizza lo strumento di registrazione Hello *autenticazione basata su form* toovalidate accessi degli utenti in Azure Active Directory. Per la corretta connessione, un amministratore di Azure Active Directory deve abilitare l'autenticazione basata su form in hello *criteri di autenticazione globali*.

Con criteri di autenticazione globali hello, è possibile abilitare l'autenticazione separatamente per le connessioni, extranet e intranet, come illustrato nella seguente immagine hello. Se l'autenticazione basata su form non è abilitato per la rete hello da cui si esegue la connessione, potrebbero verificarsi errori di accesso.

 ![Criteri di autenticazione globali di Azure Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

Per altre informazioni, vedere [Configurazione dei criteri di autenticazione](https://technet.microsoft.com/library/dn486781.aspx).

## <a name="provision-data-catalog"></a>Effettuare il provisioning del catalogo dati
È possibile effettuare il provisioning di un solo catalogo dati per organizzazione (dominio di Azure Active Directory). Pertanto, se il proprietario di hello o Comproprietario di una sottoscrizione di Azure che appartiene toothis dominio Azure Active Directory è già creato un catalogo, non sarà in grado di toocreate un catalogo nuovamente anche se si dispone di più sottoscrizioni di Azure. tootest se è stato creato un catalogo di dati da un utente nel dominio Active Directory di Azure, visitare toohello [home page di Azure Data Catalog](http://azuredatacatalog.com) e verificare se viene visualizzato il catalogo di hello. Se un catalogo è già stato creato per l'utente, è possibile ignorare hello seguente procedura e passare toohello sezione successiva.    

1. Passare toohello [pagina servizio Catalogo dati](https://azure.microsoft.com/services/data-catalog) e fare clic su **iniziare**.
   
    ![Azure Data Catalog - Pagina di destinazione di marketing](media/data-catalog-get-started/data-catalog-marketing-landing-page.png)
2. Accedere con un account utente è proprietario di hello o Comproprietario di una sottoscrizione di Azure. Vedrai hello seguente pagina dopo l'accesso.
   
    ![Azure Data Catalog - Effettuare il provisioning del catalogo dati](media/data-catalog-get-started/data-catalog-create-azure-data-catalog.png)
3. Specificare un **nome** per catalogo dati hello, hello **sottoscrizione** toouse desiderato e hello **percorso** per catalogo hello.
4. Espandere **Prezzi** e selezionare un'**edizione** di Azure Data Catalog (Gratuito o Standard).
    ![Azure Data Catalog - Selezionare l'edizione](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)
5. Espandere **utenti catalogo** e fare clic su **Aggiungi** utenti tooadd per catalogo dati hello. Aggiunti automaticamente toothis gruppo.
    ![Azure Data Catalog - Utenti](media/data-catalog-get-started/data-catalog-add-catalog-user.png)
6. Espandere **gli amministratori del catalogo** e fare clic su **Aggiungi** tooadd altri amministratori per catalogo dati hello. Aggiunti automaticamente toothis gruppo.
    ![Azure Data Catalog - Amministratori](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)
7. Fare clic su **Crea catalogo** catalogo dati di hello toocreate per l'organizzazione. Vedrai hello home page di catalogo dati hello dopo averlo creato.
    ![Azure Data Catalog - Creazione](media/data-catalog-get-started/data-catalog-created.png)    

### <a name="find-a-data-catalog-in-hello-azure-portal"></a>Trovare un catalogo di dati nel portale di Azure hello
1. In una scheda separata nel browser web hello o in una finestra del browser web separato, andare toohello [portale di Azure](https://portal.azure.com) e Accedi con hello stesso account che si toocreate utilizzati hello catalogo dati nel passaggio precedente hello.
2. Selezionare **Esplora** e quindi fare clic su **Catalogo dati**.
   
    ![Azure Data Catalog - Sfoglia Azure](media/data-catalog-get-started/data-catalog-browse-azure-portal.png) vedrai dati hello catalogo creato.
   
    ![Azure Data Catalog - Visualizzare il catalogo nell'elenco](media/data-catalog-get-started/data-catalog-azure-portal-show-catalog.png)
3. Fare clic su catalogo hello creato. Vedrai hello **catalogo dati** pannello nel portale di hello.
   
   ![Azure Data Catalog - Pannello nel portale ](media/data-catalog-get-started/data-catalog-blade-azure-portal.png)
4. È possibile visualizzare le proprietà del catalogo dati hello e aggiornarli. Ad esempio, fare clic su **tariffario** e modificare l'edizione di hello.
   
    ![Azure Data Catalog - Piano tariffario](media/data-catalog-get-started/data-catalog-change-pricing-tier.png)

### <a name="adventure-works-sample-database"></a>Database di esempio Adventure Works
In questa esercitazione, si registra l'asset di dati (tabelle) dal database di esempio AdventureWorks2014 hello per hello il motore di Database di SQL Server, ma se si preferisce toowork con i dati rilevanti e familiare tooyour ruolo, è possibile utilizzare qualsiasi origine dati supportata. Per un elenco di origini dati supportate, vedere [Origini dati supportate](data-catalog-dsr.md).

### <a name="install-hello-adventure-works-2014-oltp-database"></a>Installare i database OLTP di Adventure Works 2014 hello
database Adventure Works Hello supporta scenari di elaborazione delle transazioni online standard per un produttore di biciclette fittizio (Adventure Works Cycles), che include i prodotti, venditi e acquisti. In questa esercitazione si registreranno le informazioni sui prodotti in Azure Data Catalog.

database di esempio Adventure Works hello tooinstall:

1. Scaricare [Adventure Works 2014 Full Database Backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) in CodePlex.
2. database hello toorestore nel computer in uso, seguire le istruzioni hello [ripristinare un Backup del Database tramite SQL Server Management Studio](http://msdn.microsoft.com/library/ms177429.aspx), o eseguendo la procedura seguente:
   1. Aprire SQL Server Management Studio e connettersi toohello il motore di Database di SQL Server.
   2. Fare clic con il pulsante destro del mouse su **Database** e scegliere **Ripristina database**.
   3. In **Restore Database**, fare clic su hello **dispositivo** opzione **origine** e fare clic su **Sfoglia**.
   4. In **Seleziona dispositivi di backup** fare clic su **Aggiungi**.
   5. Cartella toohello andare in cui si dispone di hello **AdventureWorks2014.bak** file, file hello selezionare e fare clic su **OK** tooclose hello **individua File di Backup** la finestra di dialogo.
   6. Fare clic su **OK** tooclose hello **Seleziona dispositivi di backup** la finestra di dialogo.    
   7. Fare clic su **OK** tooclose hello **Restore Database** la finestra di dialogo.

È ora possibile registrare l'asset di dati dal database di esempio Adventure Works hello usando Azure Data Catalog.

## <a name="register-data-assets"></a>Registrare gli asset di dati
In questo esercizio, si utilizza hello registrazione strumento tooregister asset di dati dal database Adventure Works hello con catalogo hello. La registrazione è il processo di hello di estrazione dei metadati strutturali della chiave, ad esempio nomi, tipi e i percorsi dall'origine dati hello e gli asset hello che contiene e la copia di tale catalogo toohello dei metadati. Hello origine dati e gli asset di dati rimangono in cui sono, ma i metadati di hello vengono utilizzati da hello catalogo toomake più facilmente individuabili e comprensibile.

### <a name="register-a-data-source"></a>Registrazione di un'origine dati
1. Passare toohello [home page di Azure Data Catalog](http://azuredatacatalog.com) e fare clic su **pubblicare dati**.
   
   ![Azure Data Catalog - Pulsante Pubblica dati](media/data-catalog-get-started/data-catalog-publish-data.png)
2. Fare clic su **Avvia applicazione** toodownload, installazione e lo strumento di registrazione hello esecuzione nel computer in uso.
   
   ![Azure Data Catalog - Pulsante Avvia](media/data-catalog-get-started/data-catalog-launch-application.png)
3. In hello **iniziale** pagina, fare clic su **Accedi** e immettere le credenziali.     
   
    ![Azure Data Catalog - Pagina Introduzione](media/data-catalog-get-started/data-catalog-welcome-dialog.png)
4. In hello **Microsoft Azure Data Catalog** pagina, fare clic su **SQL Server** e **Avanti**.
   
    ![Azure Data Catalog - Origini dati](media/data-catalog-get-started/data-catalog-data-sources.png)
5. Immettere le proprietà di connessione di SQL Server hello per **AdventureWorks2014** (vedere il seguente esempio hello) e fare clic su **CONNETTI**.
   
   ![Azure Data Catalog - Impostazioni di connessione SQL Server](media/data-catalog-get-started/data-catalog-sql-server-connection.png)
6. Registrare i metadati di hello nell'asset di dati. In questo esempio, si registra **/prodotto** oggetti dallo spazio dei nomi di hello produzione AdventureWorks:
   
   1. In hello **Server gerarchia** espandere **AdventureWorks2014** e fare clic su **produzione**.
   2. Selezionare **Product**, **ProductCategory**, **ProductDescription** e **ProductPhoto** usando CTRL+clic.
   3. Fare clic su hello **spostare freccia selezionata** (**>**). Questa azione consente di spostare tutti gli oggetti selezionati in hello **toobe oggetti registrati** elenco.
      
      ![Esercitazione di Azure Data Catalog - Esplorare e selezionare gli oggetti](media/data-catalog-get-started/data-catalog-server-hierarchy.png)
   4. Selezionare **includono un'anteprima** tooinclude un'anteprima di snapshot dei dati di hello. snapshot Hello include i record too20 da ogni tabella e viene copiato nel catalogo di hello.
   5. Selezionare **includono dati profilo** tooinclude uno snapshot delle statistiche di oggetto hello per profilo dati hello (ad esempio: i valori minimi, massimo e medi per una colonna, il numero di righe).
   6. In hello **aggiungere tag** immettere **adventure funziona, cicli**. Questa azione aggiunge i tag di ricerca per gli asset di dati. I tag sono un ottimo modo gli utenti toohelp trovare un'origine dati registrato.
   7. Specificare il nome di hello di un **esperto** per i dati (facoltativi).
      
      ![Esercitazione di Azure Data Catalog--toobe oggetti registrati](media/data-catalog-get-started/data-catalog-objects-register.png)
   8. Fare clic su **REGISTRA**. Nel Catalogo dati di Azure vengono registrati gli oggetti selezionati. In questo esercizio, vengono registrati gli oggetti selezionato hello da Adventure Works. lo strumento di registrazione Hello estrae i metadati da asset di dati hello e copia i dati nel servizio Azure Data Catalog hello. Hello dati restano in cui risiede e rimane in Criteri di sistema corrente hello e controllo hello degli amministratori di hello.
      
      ![Azure Data Catalog - Oggetti registrati](media/data-catalog-get-started/data-catalog-registered-objects.png)
   9. Fare clic su oggetti di origine dati registrata, toosee **portale vista**. Nel portale di Azure Data Catalog hello, assicurarsi di visualizzare tutte e quattro le tabelle e database hello nella visualizzazione griglia hello.
      
      ![Oggetti nel portale di Azure Data Catalog hello ](media/data-catalog-get-started/data-catalog-view-portal.png)

In questo esercizio, gli oggetti dal database di esempio Adventure Works hello è registrato in modo che essi possono essere facilmente individuati dagli utenti dell'organizzazione. Nel prossimo esercizio hello, si apprenderà come toodiscover registrato asset di dati.

## <a name="discover-data-assets"></a>Individuare gli asset di dati
L'individuazione in Azure Data Catalog usa due meccanismi principali: ricerca e filtri.

La ricerca è progettato toobe sia intuitiva e potente. Per impostazione predefinita, i termini di ricerca vengono confrontati con qualsiasi proprietà nel catalogo di hello, inclusi le annotazioni fornito dall'utente.

Il filtro è progettato toocomplement la ricerca. È possibile selezionare caratteristiche specifiche, ad esempio esperti, tipo di origine dati, tipo di oggetto e tooview tag asset di dati e di ricerca tooconstrain corrispondenti risultati toomatching asset.

Utilizzando una combinazione di ricerca e filtro, è possibile passare rapidamente le origini dati hello che sono state registrate con risorse di Azure Data Catalog toodiscover hello dati che è necessario.

In questo esercizio, si utilizza asset di hello Azure Data Catalog toodiscover portale dati che è stato registrato nell'esercizio precedente hello. Per informazioni dettagliate sulla sintassi di ricerca, vedere [Riferimento alla sintassi di ricerca in Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) .

Di seguito sono riportati alcuni esempi per l'individuazione di asset di dati nel catalogo di hello.  

### <a name="discover-data-assets-with-basic-search"></a>Individuare gli asset di dati con la ricerca di base
La ricerca di base consente di eseguire ricerche nel catalogo con uno o più termini di ricerca. I risultati sono tutte le risorse che corrispondono a una proprietà con una o più delle condizioni di hello specificati.

1. Fare clic su **Home** nel portale di Azure Data Catalog hello. Se la chiusura del browser web hello, andare toohello [home page di Azure Data Catalog](https://www.azuredatacatalog.com).
2. Nella casella di ricerca hello, immettere `cycles` e premere **invio**.
   
    ![Azure Data Catalog - Ricerca di testo di base](media/data-catalog-get-started/data-catalog-basic-text-search.png)
3. Assicurarsi di visualizzare tutte le quattro tabelle e database hello (AdventureWorks2014) nei risultati di hello. È possibile passare da **visualizzazione griglia** e **visualizzazione elenco** facendo clic sui pulsanti sulla barra degli strumenti hello come illustrato nella seguente immagine hello. La parola chiave ricerca hello viene evidenziato nei risultati della ricerca hello quanto hello **evidenziare** opzione **ON**. È inoltre possibile specificare il numero di hello di **risultati per pagina** nei risultati della ricerca.
   
    ![Azure Data Catalog - Risultati della ricerca di testo di base](media/data-catalog-get-started/data-catalog-basic-text-search-results.png)
   
    Hello **ricerche** pannello è hello a sinistra e hello **proprietà** pannello è su hello destra. In hello **ricerche** pannello, è possibile modificare i criteri di ricerca e filtrare i risultati. Hello **proprietà** pannello sono visualizzate le proprietà di un oggetto selezionato nella griglia di hello o elenco.
4. Fare clic su **prodotto** nei risultati della ricerca hello. Fare clic su hello **anteprima**, **colonne**, **profilo dati**, e **documentazione** schede, oppure fare clic su riquadro inferiore di hello freccia tooexpand hello.  
   
    ![Azure Data Catalog - Riquadro inferiore](media/data-catalog-get-started/data-catalog-data-asset-preview.png)
   
    In hello **anteprima** scheda visualizzare un'anteprima dei dati di hello in hello **prodotto** tabella.  
5. Fare clic su hello **colonne** scheda toofind dettagli sulle colonne (ad esempio **nome** e **tipo di dati**) nell'asset di dati hello.
6. Fare clic su hello **profilo dati** scheda toosee hello profiling dei dati (ad esempio: numero di righe, le dimensioni dei dati o il valore minimo in una colonna) nel asset di dati hello.
7. Filtrare i risultati di hello usando **filtri** a sinistra di hello. Ad esempio, fare clic su **tabella** per **tipo di oggetto**, e si vedere solo hello quattro tabelle, non hello database.
   
    ![Azure Data Catalog - Filtrare i risultati della ricerca](media/data-catalog-get-started/data-catalog-filter-search-results.png)

### <a name="discover-data-assets-with-property-scoping"></a>Individuare gli asset di dati con la ricerca dell'ambito della proprietà
Proprietà dell'ambito consente che individuare gli asset di dati in cui il termine di ricerca hello viene abbinato hello la proprietà specificata.

1. Crittografato hello **tabella** filtrare sotto **tipo di oggetto** in **filtri**.  
2. Nella casella di ricerca hello, immettere `tags:cycles` e premere **invio**. Vedere [riferimento alla sintassi di ricerca nel catalogo dati](https://msdn.microsoft.com/library/azure/mt267594.aspx) per tutte le proprietà utilizzati per la ricerca del catalogo dati hello di hello.
3. Assicurarsi di visualizzare tutte le quattro tabelle e database hello (AdventureWorks2014) nei risultati di hello.  
   
    ![Data Catalog - Risultati della ricerca dell'ambito della proprietà](media/data-catalog-get-started/data-catalog-property-scoping-results.png)

### <a name="save-hello-search"></a>Salva ricerca hello
1. In hello **ricerche** riquadro hello **ricerca corrente** sezione, immettere un nome per la ricerca hello e fare clic su **salvare**.
   
    ![Azure Data Catalog - Salvare la ricerca](media/data-catalog-get-started/data-catalog-save-search.png)
2. Verificare che le ricerche salvata hello viene visualizzato in **ricerche salvate**.
   
    ![Azure Data Catalog - Ricerche salvate](media/data-catalog-get-started/data-catalog-saved-search.png)
3. Selezionare una delle azioni di hello è possibile eseguire la ricerca salvata hello in (**rinominare**, **eliminare**, **Salva come predefinito** ricerca).
   
    ![Azure Data Catalog - Opzioni delle ricerche salvate](media/data-catalog-get-started/data-catalog-saved-search-options.png)

### <a name="boolean-operators"></a>Operatori booleani
È possibile ampliare o limitare la ricerca con operatori booleani.

1. Nella casella di ricerca hello, immettere `tags:cycles AND objectType:table`e premere **invio**.
2. Assicurarsi di visualizzare solo le tabelle (non il database hello) nei risultati di hello.  
   
    ![Azure Data Catalog - Operatore booleano nella ricerca](media/data-catalog-get-started/data-catalog-search-boolean-operator.png)

### <a name="grouping-with-parentheses"></a>Raggruppamento con parentesi
Raggruppamento tra parentesi, è possibile raggruppare parti di hello query tooachieve isolamento logico, in particolare, insieme a operatori booleani.

1. Nella casella di ricerca hello, immettere `name:product AND (tags:cycles AND objectType:table)` e premere **invio**.
2. Assicurarsi di visualizzare solo hello **prodotto** tabella nei risultati della ricerca hello.
   
    ![Azure Data Catalog - Raggruppamento delle ricerche](media/data-catalog-get-started/data-catalog-grouping-search.png)   

### <a name="comparison-operators"></a>Operatori di confronto
Gli operatori di confronto consentono di usare confronti diversi dall'uguaglianza per le proprietà che hanno dati di tipo numero e data.

1. Nella casella di ricerca hello, immettere `lastRegisteredTime:>"06/09/2016"`.
2. Crittografato hello **tabella** filtrare sotto **tipo di oggetto**.
3. Premere **INVIO**.
4. Assicurarsi di visualizzare hello **prodotto**, **ProductCategory**, **ProductDescription**, e **ProductPhoto** hello e tabelle Database AdventureWorks2014 registrato nei risultati della ricerca.
   
    ![Azure Data Catalog - Risultati della ricerca di confronto](media/data-catalog-get-started/data-catalog-comparison-operator-results.png)

Vedere [come asset di dati toodiscover](data-catalog-how-to-discover.md) per informazioni dettagliate sull'individuazione di asset di dati e [riferimento alla sintassi di ricerca nel catalogo dati](https://msdn.microsoft.com/library/azure/mt267594.aspx) per la sintassi di ricerca.

## <a name="annotate-data-assets"></a>Annotare gli asset di dati
In questo esercizio, utilizzare tooannotate portale di Azure Data Catalog hello (aggiunta di informazioni quali le descrizioni, tag o esperti) è stato registrato in precedenza nel catalogo di hello asset di dati. le annotazioni Hello integrano e migliorano hello metadati strutturali estratti dall'origine dati hello durante la registrazione e rende molto più semplice toodiscover di asset di dati hello e comprendano.

In questo esercizio verrà annotato un singolo asset di dati (ProductPhoto). Aggiungere un nome descrittivo e un asset di dati ProductPhoto toohello descrizione.  

1. Passare toohello [home page di Azure Data Catalog](https://www.azuredatacatalog.com) e di ricerca con `tags:cycles` toofind asset di dati di hello è stato registrato.  
2. Fare clic su **ProductPhoto** nei risultati della ricerca.  
3. Immettere **le immagini dei prodotti** per **nome descrittivo** e **foto del prodotto per i materiali di marketing** per hello **descrizione**.
   
    ![Azure Data Catalog - Descrizione di ProductPhoto](media/data-catalog-get-started/data-catalog-productphoto-description.png)
   
    Hello **descrizione** consente ad altri utenti individuare e comprendere come e perché toouse hello selezionato asset di dati. È anche possibile aggiungere altri tag e visualizzare le colonne. Ora è possibile provare la ricerca e filtro asset di dati toodiscover utilizzando metadati descrittivi hello aggiunti toohello catalogo.

È inoltre possibile eseguire hello seguenti in questa pagina:

* Aggiungere esperti per l'asset di dati hello. Fare clic su **Aggiungi** in hello **esperti** area.
* Aggiungere tag a livello di set di dati hello. Fare clic su **Aggiungi** in hello **tag** area. Un tag può essere un tag utente o un tag di glossario. Hello edizione Standard di catalogo dati include un glossario aziendale che consente di definire una tassonomia di business centrale gli amministratori del catalogo. Gli utenti del catalogo possono quindi annotare gli asset di dati con i termini di glossario. Per ulteriori informazioni, vedere [come tooset backup hello glossario aziendale per contrassegnare i governato](data-catalog-how-to-business-glossary.md)
* Aggiungere tag a livello di colonna hello. Fare clic su **Aggiungi** in **tag** per colonna hello desiderato tooannotate.
* Aggiungere una descrizione a livello di colonna hello. Immettere una **Descrizione** per una colonna. È inoltre possibile visualizzare i metadati di descrizione hello estratti dall'origine dati hello.
* Aggiungere **richiedere l'accesso** informazioni in cui viene visualizzato come toorequest accedere toohello asset di dati.
  
    ![Azure Data Catalog - Aggiungere tag, descrizioni](media/data-catalog-get-started/data-catalog-add-tags-experts-descriptions.png)
* Scegliere hello **documentazione** scheda e fornire la documentazione per l'asset di dati hello. Con la documentazione di Azure Data Catalog, è possibile utilizzare il catalogo dati come un toocreate repository contenuto un resoconto completato degli asset di dati.
  
    ![Azure Data Catalog - Scheda Documentazione](media/data-catalog-get-started/data-catalog-documentation.png)

È anche possibile aggiungere un asset di dati di annotazione toomultiple. Ad esempio, è possibile selezionare tutti gli asset di dati hello che è stato registrato e specificare un esperto per tali.

![Azure Data Catalog - Annotare più asset di dati](media/data-catalog-get-started/data-catalog-multi-select-annotate.png)

Azure Data Catalog supporta un tooannotations approccio sovraccaricare-sourcing. Qualsiasi utente di catalogo dati possa aggiungere tag (utente o glossario), descrizioni e altri metadati, in modo che qualsiasi utente con un punto di vista in un asset di dati e sul relativo uso può avere tale prospettiva acquisiti e gli utenti tooother disponibili.

Vedere [come asset di dati tooannotate](data-catalog-how-to-annotate.md) per informazioni dettagliate sulle annotazioni di asset di dati.

## <a name="connect-toodata-assets"></a>Connettersi toodata Asset
In questo esercizio, gli asset di dati verranno aperti in uno strumento client integrato (Excel) e in uno strumento non integrato (SQL Server Management Studio) usando le informazioni di connessione.

> [!NOTE]
> È importante tooremember che Azure Data Catalog non consentono di accedere a origine dati effettiva toohello: semplicemente rende più semplice per l'utente toodiscover e capire. Quando ci si connette l'origine dati tooa, hello applicazione client che si sceglie utilizza credenziali di Windows o richiede le credenziali necessarie. Se non si è già state concesse origine dati di access toohello, è necessario toobe concesso l'accesso prima di poter connettere.
> 
> 

### <a name="connect-tooa-data-asset-from-excel"></a>Connettersi tooa asset di dati da Excel
1. Selezionare **Product** nei risultati della ricerca. Fare clic su **Apri In** sulla barra degli strumenti hello scegliere **Excel**.
   
    ![Azure Data Catalog - connettersi toodata asset](media/data-catalog-get-started/data-catalog-connect1.png)
2. Fare clic su **aprire** nella finestra popup di hello download. Questa esperienza può variare a seconda del browser hello.
   
    ![Azure Data Catalog - File di connessione Excel scaricato](media/data-catalog-get-started/data-catalog-download-open.png)
3. In hello **avviso di protezione di Microsoft Excel** finestra, fare clic su **abilitare**.
   
    ![Azure Data Catalog - Popup di sicurezza Excel](media/data-catalog-get-started/data-catalog-excel-security-popup.png)
4. Mantenere i valori predefiniti di hello in hello **l'importazione dei dati** la finestra di dialogo e fare clic su **OK**.
   
    ![Azure Data Catalog - Importazione dati di Excel](media/data-catalog-get-started/data-catalog-excel-import-data.png)
5. Visualizza l'origine dati hello in Excel.
   
    ![Azure Data Catalog - Tabella Product in Excel](media/data-catalog-get-started/data-catalog-connect2.png)

In questo esercizio si connessi asset toodata individuati tramite Azure Data Catalog. Con il portale di Azure Data Catalog hello, è possibile connettersi direttamente tramite applicazioni client hello integrate hello **aperto in** menu. È inoltre possibile connettere qualsiasi applicazione desiderate utilizzando le informazioni sul percorso di connessione hello inclusi nei metadati di asset hello. Ad esempio, è possibile utilizzare i dati di SQL Server Management Studio tooconnect toohello AdventureWorks2014 database tooaccess hello in hello asset di dati registrati in questa esercitazione.

1. Aprire **SQL Server Management Studio**.
2. In hello **connettersi tooServer** finestra di dialogo immettere il nome di server hello da hello **proprietà** riquadro nel portale di Azure Data Catalog hello.
3. Utilizzare asset di dati hello tooaccess credenziali e autenticazione appropriata. Se non si dispone di accesso, utilizzare le informazioni in hello **richiesta di accesso** campo tooget è.
   
    ![Azure Data Catalog - Richiedi accesso](media/data-catalog-get-started/data-catalog-request-access.png)

Fare clic su **Visualizza le stringhe di connessione** tooview e copia ADF.NET, ODBC e OLEDB connessione stringhe toohello Appunti per l'utilizzo dell'applicazione.

## <a name="manage-data-assets"></a>Gestire gli asset di dati
In questo passaggio, viene visualizzato come tooset della protezione per l'asset di dati. Catalogo dati non è possibile accedere ai dati di toohello stesso. proprietario Hello dell'origine dati hello controlla l'accesso ai dati.

È possibile utilizzare il catalogo dati toodiscover le origini dati e metadati hello tooview relative origini toohello registrate nel catalogo di hello. Possono esistere situazioni, tuttavia, in cui devono essere solo origini dati visibili toospecific utenti o toomembers di gruppi specifici. Per questi scenari, è possibile utilizzare la proprietà tootake catalogo dati di asset di dati registrati all'interno del catalogo hello e toothen controllo hello visibilità degli asset hello che si è proprietari.

> [!NOTE]
> funzionalità di gestione di Hello descritta in questa esercitazione sono disponibili solo in hello Standard Edition di Azure Data Catalog, non in hello edizione gratuita.
> In Azure Data Catalog, può diventare proprietario dell'asset di dati, aggiungere risorse toodata comproprietari e impostare la visibilità di hello dell'asset di dati.
> 
> 

### <a name="take-ownership-of-data-assets-and-restrict-visibility"></a>Assumere la proprietà di asset di dati e limitarne la visibilità
1. Passare toohello [home page di Azure Data Catalog](https://www.azuredatacatalog.com). In hello **ricerca** testo immettere `tags:cycles` e premere **invio**.
2. Fare clic su un elemento nell'elenco risultati hello e fare clic su **Take Ownership** sulla barra degli strumenti hello.
3. In hello **Management** sezione di hello **proprietà** pannello, fare clic su **Take Ownership**.
   
    ![Azure Data Catalog - Diventa proprietario](media/data-catalog-get-started/data-catalog-take-ownership.png)
4. visibilità toorestrict, scegliere **proprietari e utenti** in hello **visibilità** sezione e fare clic su **Aggiungi**. Immettere indirizzi di posta elettronica utente nella casella di testo hello e premere **invio**.
   
    ![Azure Data Catalog - Limitazione accesso](media/data-catalog-get-started/data-catalog-ownership.png)

## <a name="remove-data-assets"></a>Rimuovere gli asset di dati
In questo esercizio, utilizzare dati di anteprima di Azure Data Catalog tooremove portale da asset di dati registrata hello ed eliminare asset di dati dal catalogo hello.

In Azure Data Catalog è possibile eliminare un singolo asset o più asset contemporaneamente.

1. Passare toohello [home page di Azure Data Catalog](https://www.azuredatacatalog.com).
2. In hello **ricerca** testo immettere `tags:cycles` e fare clic su **invio**.
3. Selezionare un elemento nell'elenco risultati hello e fare clic su **eliminare** sulla barra degli strumenti hello, come illustrato nella seguente immagine hello:
   
    ![Azure Data Catalog - Eliminare un elemento della griglia](media/data-catalog-get-started/data-catalog-delete-grid-item.png)
   
    Se si utilizza la visualizzazione elenco hello, casella di controllo di hello è toohello a sinistra dell'elemento hello, come illustrato nella seguente immagine hello:
   
    ![Azure Data Catalog - Eliminare un elemento dell'elenco](media/data-catalog-get-started/data-catalog-delete-list-item.png)
   
    È anche possibile selezionare più asset di dati ed eliminarli, come illustrato nella seguente immagine hello:
   
    ![Azure Data Catalog - Eliminare più asset di dati](media/data-catalog-get-started/data-catalog-delete-assets.png)

> [!NOTE]
> il comportamento predefinito del catalogo hello Hello è tooallow tooregister qualsiasi utente qualsiasi origine dati e tooallow toodelete qualsiasi utente qualsiasi asset di dati che è stato registrato. funzionalità di gestione di Hello inclusa nell'edizione Standard di Azure Data Catalog hello forniscono opzioni aggiuntive per assumere la proprietà di risorse, che può individuare gli asset di limitazione e per limitare, che può eliminare l'asset.
> 
> 

## <a name="summary"></a>Riepilogo
In questa esercitazione sono state analizzate le funzionalità di base di Azure Data Catalog, compresa la registrazione, l'annotazione, l'individuazione e la gestione di asset di dati aziendali. Dopo aver completato l'esercitazione hello, è ora tooget avviato. È possibile iniziare oggi registrando le origini dati hello che e al team di affidarsi e invitando catalogo hello toouse di colleghi.

## <a name="references"></a>Riferimenti
* [Come asset di dati tooregister](data-catalog-how-to-register.md)
* [Come asset di dati toodiscover](data-catalog-how-to-discover.md)
* [Come asset di dati tooannotate](data-catalog-how-to-annotate.md)
* [Come asset di dati toodocument](data-catalog-how-to-documentation.md)
* [Come tooconnect toodata Asset](data-catalog-how-to-connect.md)
* [Come asset di dati toomanage](data-catalog-how-to-manage.md)

