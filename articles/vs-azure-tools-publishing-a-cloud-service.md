---
title: un servizio Cloud utilizzando strumenti di Azure hello aaaPublishing | Documenti Microsoft
description: Informazioni su come toopublish Azure cloud progetti del servizio tramite Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1a07b6e4-3678-4cbf-b37e-4520b402a3d9
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/14/2017
ms.author: kraigb
ms.openlocfilehash: 31ede8308146de2bb128b768f23f64eb85bc7548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publishing-a-cloud-service-using-hello-azure-tools"></a>Pubblicazione di un servizio Cloud utilizzando strumenti di Azure hello
Utilizzando gli strumenti di hello Azure per Microsoft Visual Studio, è possibile pubblicare l'applicazione Azure direttamente da Visual Studio. Integrato di Visual Studio supporta la pubblicazione tooeither hello gestione temporanea o hello ambiente di produzione di un servizio cloud.

Per poter pubblicare un'applicazione Azure è necessario avere una sottoscrizione di Azure. È inoltre necessario configurare un cloud servizio e l'archiviazione account toobe utilizzati dall'applicazione. È possibile configurare questi a hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!IMPORTANT]
> Quando esegue la pubblicazione, è possibile selezionare l'ambiente di distribuzione hello per il servizio cloud. È inoltre necessario selezionare un account di archiviazione di pacchetto di applicazione hello toostore utilizzato per la distribuzione. Dopo la distribuzione, il pacchetto di applicazione hello viene rimosso dall'account di archiviazione hello.
> 
> 

Quando si sviluppa e si testa un'applicazione Azure, è possibile utilizzare distribuzione Web toopublish modifiche in modo incrementale per i ruoli web. Dopo aver pubblicato l'ambiente di distribuzione applicazione tooa, distribuzione Web consente di distribuire le modifiche direttamente macchina virtuale toohello che esegue il ruolo di web hello. Non si dispone di toopackage e pubblicare l'intera applicazione Azure ogni volta che si desidera tooupdate il tootest ruolo web modifiche hello. Con questo approccio è possibile disporre le modifiche del ruolo web nel cloud hello per il test senza attesa toohave all'ambiente di distribuzione applicazione tooa pubblicato.

Utilizzare l'applicazione Azure e un ruolo web tooupdate hello seguendo procedure toopublish usando distribuzione Web:

* Pubblicare o Assemblare un'applicazione Azure da Visual Studio
* Aggiornare un ruolo web come parte del ciclo hello sviluppo e test

## <a name="publish-or-package-an-azure-application-from-visual-studio"></a>Pubblicare o Assemblare un'applicazione Azure da Visual Studio
Quando si pubblica l'applicazione Azure, è possibile eseguire una delle seguenti attività hello:

* Creare un pacchetto del servizio: È possibile utilizzare questo toopublish file di configurazione del servizio di pacchetto e hello all'ambiente di distribuzione applicazione tooa da hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).
* Pubblicare il progetto Azure da Visual Studio: toopublish l'applicazione direttamente tooAzure, utilizzare hello pubblicazione guidata. Per altre informazioni, vedere [Procedura guidata Pubblica l'applicazione Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="toocreate-a-service-package-from-visual-studio"></a>toocreate un pacchetto del servizio da Visual Studio
1. Quando si è pronti toopublish dell'applicazione, aprire Esplora soluzioni, menu di scelta rapida aprire hello hello progetto Azure che contiene i ruoli, quindi scegliere pubblica.
2. un pacchetto del servizio toocreate solo, seguire questi passaggi:  
   
   1. Nel menu di scelta rapida hello hello Azure del progetto, scegliere **pacchetto**.
   2. In hello **pacchetto applicazione Azure** la finestra di dialogo, scegliere un pacchetto di configurazione del servizio hello per cui si desidera toocreate, quindi scegliere Configurazione compilazione hello.
   3. (facoltativo) tooturn desktop remoto per il servizio cloud hello dopo la sua pubblicazione, seleziona hello **Abilita Desktop remoto per tutti i ruoli** casella di controllo e quindi selezionare **impostazioni** tooconfigure Desktop remoto. Se si desidera toodebug il servizio cloud dopo la sua pubblicazione, attivare il debug remoto selezionando **Abilita Debugger remoto per tutti i ruoli**.
      
      Per altre informazioni, vedere [Utilizzo di Desktop remoto con i ruoli di Azure](vs-azure-tools-remote-desktop-roles.md).
   4. toocreate hello del pacchetto, scegliere hello **pacchetto** collegamento.
      
      Esplora file Mostra percorso del file hello di hello pacchetto appena creato. È possibile copiare questo percorso in modo che è possibile usarlo da hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).
   5. toopublish questo ambiente di distribuzione tooa pacchetto, è necessario utilizzare questo percorso come hello percorso del pacchetto quando si crea un servizio cloud e distribuisce l'ambiente tooan pacchetto con hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).
3. Processo di distribuzione hello toocancel (facoltativo), nel menu di scelta rapida hello hello voce nel registro attività hello, scegliere **Annulla e Rimuovi**. Questo arresta il processo di distribuzione hello e si elimina l'ambiente di distribuzione hello da Azure.
   
   > [!NOTE]
   > tooremove questo ambiente di distribuzione dopo è stato distribuito, è necessario utilizzare hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).
   > 
   > 
4. (Facoltativo) Una volta avviate le istanze del ruolo, Visual Studio verrà visualizzato ambiente di distribuzione hello in hello **servizi Cloud** nodo in Esplora Server. Da qui è possibile visualizzare lo stato di hello di hello singole istanze del ruolo. Vedere [risorse di gestione di Azure con Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md).hello seguente figura mostra le istanze del ruolo hello mentre sono ancora in stato Initializing hello:
   
    ![VST_DeployComputeNode](./media/vs-azure-tools-publishing-a-cloud-service/IC744134.png)

## <a name="update-a-web-role-as-part-of-hello-development-and-testing-cycle"></a>Aggiornare un ruolo Web come parte di hello lo sviluppo e test del ciclo
Se l'infrastruttura di back-end dell'app è stabile, ma i ruoli web hello necessitano aggiornamenti più frequenti, è possibile utilizzare distribuzione Web tooupdate solo un ruolo web nel progetto. Ciò è utile quando non si desidera toorebuild e ridistribuire i ruoli di lavoro di hello back-end, o se si dispone di più ruoli web e si desidera tooupdate solo uno dei ruoli web hello.

### <a name="requirements"></a>Requisiti
Di seguito è hello requisiti toouse distribuzione Web tooupdate il ruolo web:

* **Solo a scopo di sviluppo e test:** hello le modifiche vengono apportate direttamente macchina virtuale toohello in cui è in esecuzione ruolo web hello. Se la macchina virtuale ha toobe riciclato, le modifiche di hello andranno perse perché pacchetto hello originale è stato pubblicato è macchina virtuale di hello toorecreate utilizzato per il ruolo di hello. È necessario ripubblicare le modifiche più recenti di hello tooget applicazione per il ruolo web hello.
* **Possono essere aggiornati solo i ruoli web:** I ruoli di lavoro non possono essere aggiornati. Inoltre, è possibile aggiornare hello RoleEntryPoint nel file web role.cs.
* **Può supportare solo una singola istanza di un ruolo web:** Non è possibile avere più istanze di qualsiasi ruolo web nell'ambiente di distribuzione. Tuttavia, sono supportati più ruoli web con una sola istanza.
* **È necessario abilitare le connessioni desktop remoto:** questa operazione è necessaria in modo che distribuzione Web è possibile utilizzare hello utente e password tooconnect toohello macchina virtuale toodeploy hello modifiche toohello server che esegue Internet Information Services (IIS). Inoltre, potrebbe essere necessario tooconnect toohello macchina virtuale tooadd tooIIS un certificato attendibile per questa macchina virtuale. (In modo che hello connessione remota per IIS utilizzata da distribuzione Web sia sicura.)

Hello nella procedura si presuppone che si sta utilizzando hello **pubblica l'applicazione Azure** procedura guidata.

### <a name="tooenable-web-deploy-when-you-publish-your-application"></a>tooEnable distribuire quando si pubblica l'applicazione Web
1. hello tooenable **Abilita distribuzione Web** per tutte le casella di controllo ruoli web, è innanzitutto necessario configurare le connessioni desktop remoto. Selezionare **Abilita Desktop remoto** per tutti i ruoli e quindi specificare le credenziali di hello che verrà utilizzato tooconnect in modalità remota in hello **configurazione Desktop remoto** visualizzata. Vedere [Utilizzo di Desktop remoto con i ruoli di Azure](vs-azure-tools-remote-desktop-roles.md) per ulteriori informazioni.
2. Selezionare tooenable distribuzione Web per tutti i ruoli web nell'applicazione, di hello **Abilita distribuzione Web per tutti i ruoli web**.
   
    Viene visualizzato un triangolo giallo. Distribuzione Web utilizza un certificato autofirmato non attendibile per impostazione predefinita, che non è consigliato per il caricamento dei dati riservati. Se è necessario toosecure questo processo per i dati sensibili, è possibile aggiungere un toobe certificato SSL utilizzato per le connessioni di distribuzione Web. Questo certificato deve toobe un certificato attendibile. Per informazioni su come toodo, vedere la sezione hello **tooMake sicuro distribuzione Web** più avanti in questo argomento.
3. Scegliere **Avanti** tooshow hello **riepilogo** schermata e quindi scegliere **pubblica** servizio cloud di hello toodeploy.
   
    servizio cloud Hello viene pubblicato. Hello macchina virtuale in cui viene creato con le connessioni remote abilitate per IIS in modo che distribuzione Web può essere utilizzato tooupdate i ruoli web senza necessità di pubblicarli nuovamente.
   
   > [!NOTE]
   > Se si dispone di più istanze configurate per un ruolo web, viene visualizzato un messaggio di avviso che informa che ogni ruolo web sarà limitato tooone istanza solo nel pacchetto hello che ha creato l'applicazione toopublish. Selezionare **OK** toocontinue. Come indicato nella sezione requisiti hello, è possibile avere più di un ruolo web, ma solo un'istanza di ogni ruolo.
   > 
   > 

### <a name="tooupdate-your-web-role-by-using-web-deploy"></a>tooUpdate del ruolo Web da utilizzare distribuzione Web
1. toouse distribuzione Web, assicurarsi di progetto toohello modifiche del codice per uno dei ruoli web in Visual Studio desiderate toopublish, quindi fare doppio clic su questo nodo del progetto nella soluzione e scegliere troppo**pubblica**. Hello **pubblica sul Web** viene visualizzata la finestra di dialogo.
2. (Facoltativo) Se è stato aggiunto un toouse certificato SSL attendibile per le connessioni remote per IIS, è possibile deselezionare hello **Consenti certificato non attendibile** casella di controllo. Per informazioni su come tooadd toomake un certificato di distribuzione Web proteggere, vedere la sezione hello **tooMake sicuro distribuzione Web** più avanti in questo argomento.
3. toouse distribuzione Web, meccanismo di pubblicazione hello richiede nome utente hello e la password configurati per la connessione desktop remota alla prima pubblicazione del pacchetto di hello.
   
   1. In **nome utente**, immettere nome utente hello.
   2. In **Password**, immettere la password di hello.
   3. (Facoltativo) Se si desidera toosave questa password in questo profilo, scegliere **Salva password**.
4. ruolo toopublish hello modifiche tooyour web scegliere **pubblica**.
   
    Visualizza la riga di stato Hello **pubblica avviato**. Al termine, la pubblicazione di hello **pubblicazione completata** viene visualizzato. modifiche di Hello sono stati distribuiti toohello ruolo web sulla macchina virtuale. È ora possibile avviare l'applicazione Azure in hello ambiente Azure tootest le modifiche.

### <a name="toomake-web-deploy-secure"></a>tooMake sicuro distribuzione Web
1. Distribuzione Web utilizza un certificato autofirmato non attendibile per impostazione predefinita, che non è consigliato per il caricamento dei dati riservati. Se è necessario toosecure questo processo per i dati sensibili, è possibile aggiungere un toobe certificato SSL utilizzato per le connessioni di distribuzione Web. Questo certificato deve toobe un certificato attendibile, forniti da un'autorità di certificazione (CA).
   
    toomake Web Deploy sicuro per ogni macchina virtuale per ognuno dei ruoli web, è necessario caricare certificato attendibile di hello che si desidera toouse per distribuzione web toohello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885). Ciò assicura che il certificato hello viene aggiunto toohello macchina virtuale in cui viene creato per il ruolo web hello quando si pubblica l'applicazione.
2. tooadd un toouse tooIIS di certificato SSL attendibile per le connessioni remote, seguire questi passaggi:
   
   1. macchina virtuale di toohello tooconnect dotato di ruolo web hello, istanza hello selezionare il ruolo web hello in **Cloud Explorer** o **Esplora Server**, quindi scegliere hello **Connetti tramite Desktop remoto** comando. Per informazioni dettagliate sulla macchina virtuale di toohello tooconnect, vedere [tramite Desktop remoto con i ruoli Azure](vs-azure-tools-remote-desktop-roles.md).
      
      Il browser richiederà toodownload un. File RDP.
   2. tooadd un certificato SSL, il servizio di gestione di hello aperto in Gestione IIS. In Gestione IIS abilitare SSL apertura hello **associazioni** collegamento hello **azione** riquadro. Hello **Aggiungi Binding sito** viene visualizzata la finestra di dialogo. Scegliere **Aggiungi**, quindi scegliere HTTPS in hello **tipo** elenco a discesa. In hello **certificato SSL** scegliere il certificato SSL hello che è stato firmato da un'autorità di certificazione e caricato toohello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885). Per ulteriori informazioni, vedere [configurare le impostazioni di connessione per servizio di gestione di hello](http://go.microsoft.com/fwlink/?LinkId=215824).
      
      > [!NOTE]
      > Se si aggiunge un certificato SSL attendibile, triangolo di avviso gialla hello non viene più visualizzata in hello **pubblicazione guidata**.
      > 
      > 

## <a name="include-files-in-hello-service-package"></a>Includere i file nel pacchetto del servizio hello
Potrebbe essere necessario tooinclude specifici file nel pacchetto del servizio in modo che siano disponibili nella macchina virtuale hello creato per un ruolo. Ad esempio, è consigliabile tooadd .exe o un file con estensione msi che viene utilizzato da un pacchetto di servizio di avvio script tooyour. O potrebbe essere necessario tooadd un assembly che richiede un progetto di ruolo web ruolo o di lavoro. file di tooinclude che devono essere aggiunti toohello soluzione per l'applicazione Azure.

### <a name="tooinclude-files-in-hello-service-package"></a>file nel pacchetto di servizio hello tooinclude
1. tooadd un pacchetto del servizio tooa assembly, utilizzare hello alla procedura seguente:
   
   1. In **Esplora** nodo hello Apri progetto hello privo di assembly hello a cui fa riferimento.
   2. tooadd hello assembly toohello progetto, menu di scelta rapida aprire hello hello **riferimenti** cartella e quindi scegliere **Aggiungi riferimento**. viene visualizzata la finestra Aggiungi riferimento Hello.
   3. Scegliere riferimento hello tooadd desiderati e quindi scegliere hello **OK** pulsante.
      
      riferimento Hello viene aggiunto l'elenco toohello hello **riferimenti** cartella.
   4. Aprire il menu di scelta rapida hello per assembly hello che è stato aggiunto e scegliere **proprietà**. Hello **proprietà** verrà visualizzata la finestra.
      
      tooinclude questo assembly nel servizio hello del pacchetto, in hello **elenco copia locale** scegliere **True**.
2. In **Esplora** nodo hello Apri progetto hello privo di assembly hello a cui fa riferimento.
3. tooadd hello assembly toohello progetto, menu di scelta rapida aprire hello hello **riferimenti** cartella e quindi scegliere **Aggiungi riferimento**. Hello **Aggiungi riferimento** viene visualizzata la finestra.
4. Scegliere riferimento hello tooadd desiderati e quindi scegliere hello **OK** pulsante.
   
    riferimento Hello viene aggiunto l'elenco toohello hello **riferimenti** cartella.
5. Aprire il menu di scelta rapida hello per assembly hello che è stato aggiunto e scegliere **proprietà**. verrà visualizzata la finestra Proprietà Hello.
6. tooinclude questo assembly nel servizio hello del pacchetto, in hello **Copia localmente** scegliere **True**.
7. file tooinclude nel pacchetto di servizio hello che sono stati aggiunti tooyour progetto di ruolo web, aprire il menu di scelta rapida hello per file hello e quindi scegliere **proprietà**. Da hello **proprietà** finestra, scegliere **contenuto** da hello **azione di compilazione** casella di riepilogo.
8. file tooinclude nel pacchetto di servizio hello che sono stati aggiunti tooyour progetto di ruolo di lavoro, aprire il menu di scelta rapida hello per file hello e quindi scegliere **proprietà**. Da hello **proprietà** finestra, scegliere **copia se più recente** da hello **copia nella directory toooutput** casella di riepilogo.

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sulla pubblicazione tooAzure da Visual Studio, vedere [pubblicazione guidata applicazione Azure](vs-azure-tools-publish-azure-application-wizard.md).

