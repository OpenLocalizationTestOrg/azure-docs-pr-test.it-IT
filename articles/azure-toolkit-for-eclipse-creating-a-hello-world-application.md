---
title: aaaCreate Hello World servizio Cloud per Azure in Eclipse
description: Informazioni su come un'applicazione Hello World semplice utilizzando toocreate hello Azure Toolkit per Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: dfb81374aaf78e933c0bf83a1dbd98023801491a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Creare un servizio cloud Hello World per Azure in Eclipse
Hello passaggi seguenti viene illustrato come toocreate e distribuire una base tooAzure di applicazione JSP utilizzando hello Azure Toolkit per Eclipse. Per semplicità è riportato un esempio JSP, ma è possibile adottare una procedura molto simile anche per un servlet Java, per quanto riguarda la distribuzione di Azure.

un'applicazione Hello avrà un aspetto simile toohello seguenti:

![][ic600360]

## <a name="prerequisites"></a>Prerequisiti
* Java Developer Kit (JDK) versione 1.7 o successiva.
* IDE Eclipse per sviluppatori Java EE, Indigo o versione successiva. È possibile scaricare il pacchetto all'indirizzo <http://www.eclipse.org/downloads/>.
* Distribuzione di un server applicazioni o un server Web basato su Java, ad esempio Apache Tomcat, GlassFish, JBoss Application Server, Jetty, or IBM® WebSphere® Application Server Liberty Core.
* Una sottoscrizione di Azure, che può essere ottenuta all'indirizzo <http://azure.microsoft.com/pricing/purchase-options/>.
* Hello Azure Toolkit per Eclipse. Per ulteriori informazioni, vedere [installazione hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate un'applicazione Hello World
Creare innanzitutto un progetto Java.

1. Avviare Eclipse e nel menu hello scegliere **File**, fare clic su **New**, quindi fare clic su **progetto Web dinamico**. (Se non viene visualizzato **progetto Web dinamico** elencati tra i progetti disponibili dopo aver fatto clic **File**, **New**, quindi hello seguente: fare clic su **File**, fare clic su **New**, fare clic su **progetto...** , espandere **Web**, fare clic su **progetto Web dinamico**, fare clic su **Avanti**.)

1. Ai fini di questa esercitazione, denominare il progetto di hello **MyHelloWorld**. (Assicurarsi usare questo nome, i passaggi successivi in questa esercitazione prevedono il toobe file WAR denominato MyHelloWorld). Verrà visualizzata una schermata simile toohello seguenti:

   ![][ic589576]

1. Fare clic su **Finish**.

1. Nella visualizzazione Project Explorer di Eclipse espandere **MyHelloWorld**. Fare clic con il pulsante destro del mouse su **WebContent**, scegliere **New** e quindi fare clic su **JSP File**.

1. In hello **New JSP File** finestra di dialogo, il nome file di hello **index.jsp**. Mantenere come cartella padre di hello **MyHelloWorld/WebContent**, come illustrato nell'esempio hello:

   ![][ic659262]

1. In hello **Select JSP Template** finestra di dialogo, ai fini di questa esercitazione, selezionare **New JSP File (html)** e fare clic su **fine**.

1. All'apertura di file di hello index.jsp in Eclipse, aggiungere la visualizzazione del testo toodynamically **Hello World!** all'interno di hello esistente `<body>` elemento. L'aggiornamento `<body>` contenuto deve essere visualizzato come riportato di seguito hello:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. Salvare index.jsp.

## <a name="toodeploy-your-application-tooazure-hello-quick-and-simple-way"></a>toodeploy l'applicazione tooAzure, hello in modo semplice e rapido
Non appena si dispone di un tootest della applicazione web Java pronto, è possibile utilizzare hello dopo timeout direttamente su hello Azure cloud tootry di scelta rapida.

1. In Project Explorer di Eclipse fare clic su **MyHelloWorld**.

2. Nella barra degli strumenti di hello Eclipse, fare clic su hello **pubblica** pulsante a discesa e quindi fare clic su **pubblicare come servizio Cloud di Azure**

   ![][publishDropdownButton]

3. Se si sta pubblicando tooAzure questa applicazione per hello prima volta, non è stato creato un progetto di distribuzione di Azure per tale applicazione prima di un progetto di distribuzione Azure essere create automaticamente. Dovrebbe essere hello seguente prompt dei comandi, cui sono elencati anche hello JDK pacchetto e applicazione server che verrà automaticamente distribuito toorun l'applicazione.

   ![][ic789598]
   
   Questo approccio rapido consente tootest un modo semplice e rapido dell'applicazione in Azure senza tooconfigure un server specifico o un pacchetto JDK diverso da impostazioni predefinite di hello. Se si è soddisfatti con valori predefiniti di hello, è possibile fare clic su **OK** toocontinue con hello alla procedura seguente.
   Tuttavia, se si desidera toochange hello JDK o toouse server dell'applicazione per l'applicazione, è possibile farlo in un secondo momento modificando hello progetto di distribuzione Azure che è stato creato automaticamente oppure è possibile fare clic su **Annulla** e leggere Hello **sezione progetti di distribuzione su Azure** di questa esercitazione.

4. In hello **pubblicare tooAzure** finestra di dialogo:

   1. Se nessun tooselect sottoscrizioni hello **sottoscrizione** elenco ancora, seguire questi passaggi tooimport le informazioni di sottoscrizione:
      1. Fare clic su **Import from PUBLISH-SETTINGS file**.
      2. In hello **Importa informazioni sottoscrizione** finestra di dialogo, fare clic su **Scarica File PUBLISH-SETTINGS**. Se non si è ancora connessi all'account Azure, sarà richiesta toolog in. Quindi verrà chiesto di file di impostazioni di pubblicazione toosave di Azure. Salvare il file tooyour di computer locale.
      3. Ancora in hello **Importa informazioni sottoscrizione** finestra di dialogo, fare clic su hello **Sfoglia** pulsante, hello seleziona pubblicare file di impostazioni salvato localmente nel passaggio precedente hello e quindi fare clic su  **Aprire**. La schermata dovrebbe essere simile toohello seguenti:![][ic644267]
      4. Fare clic su **OK**.
   2. Per **sottoscrizione**, selezionare hello sottoscrizione che si desidera utilizzare per la distribuzione.
   3. Per **account di archiviazione**, selezionare l'account di archiviazione hello toouse desiderata, oppure fare clic su **New** toocreate un nuovo account di archiviazione.
   4. Per **nome servizio**, selezionare il servizio cloud hello toouse desiderata, oppure fare clic su **New** toocreate un nuovo servizio cloud.
   5. Per **sistema operativo di destinazione**, selezionare la versione di hello del sistema operativo hello che si desidera toouse per la distribuzione.
   6. Per **Target environment** (Ambiente di destinazione) selezionare, ai fini di questa esercitazione **Staging**. (Quando si è pronti toodeploy tooyour sito di produzione, è necessario impostare questa opzione troppo**produzione**.)
   7. Facoltativo: Verificare che **Sovrascrivi distribuzione precedente** viene controllato se si desidera che il nuovo tooautomatically distribuzione Sovrascrivi hello distribuzione precedente. Quando si abilita questa opzione, sarà possibile non problemi di esperienza di "conflitto 409" quando si pubblicano toohello nello stesso percorso.
      Si noti che hello **pubblicare tooAzure** finestra di dialogo contiene una sezione per **accesso remoto**. Per impostazione predefinita, l'accesso remoto non è abilitato e non verrà abilitato per questo esempio. tooenable accesso remoto, immettere un toouse di nome e una password utente durante l'accesso in modalità remota. Per altre informazioni sull'accesso remoto, vedere [Abilitazione dell'accesso remoto per distribuzioni di Azure in Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].
      Il **pubblicare tooAzure** finestra di dialogo verrà visualizzati simile toohello seguenti:![][ic719488]

5. Fare clic su **pubblica** toopublish toohello ambiente di gestione temporanea.

   Quando richiesto tooperform una compilazione completa, fare clic su **Sì**. L'operazione potrebbe richiedere alcuni minuti per la compilazione prima di hello.
   Nella scheda **Azure Activity Log** della sezione a schede relativa alle visualizzazioni di Eclipse verrà visualizzato un log.
   ![][ic719489]È possibile utilizzare questo file di registro, nonché hello **Console** visualizzare, lo stato di hello toosee della distribuzione. In alternativa, è toolog in toohello [il portale di gestione di Azure][Azure Management Portal]e utilizzare hello **servizi Cloud** sezione stato hello toomonitor.

6. Quando la distribuzione è stata distribuita, hello **Log attività Azure** mostrerà lo stato di **pubblicato**. Fare clic su **pubblicato**, come illustrato nella seguente hello immagine e il browser verrà aperta un'istanza della distribuzione.

   ![][ic719490]

Poiché si tratta di una distribuzione tooa ambiente di gestione temporanea, nome DNS hello sarà hello formato http://&lt;*guid*&gt;. cloudapp.net e hello URL conterrà il nome DNS hello e un suffisso per l'applicazione. ad esempio, http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. (hello **MyHelloWorld** parte è tra maiuscole e minuscole.) È inoltre possibile visualizzare hello DNS nome se si fa clic su nome distribuzione hello in hello portale di gestione della piattaforma Azure (all'interno di parte di servizi Cloud hello hello del portale di gestione).

Sebbene questa procedura dettagliata è stato per una distribuzione toohello ambiente di gestione temporanea, tooproduction una distribuzione segue hello stessi passaggi, ad eccezione all'interno di hello **pubblicare tooAzure** finestra di dialogo Seleziona **produzione** invece di **gestione temporanea** per hello **ambiente di destinazione**. Una distribuzione tooproduction risultati in un URL in base al nome DNS hello di propria scelta, anziché un GUID come quello usato per la gestione temporanea.

> [!WARNING]
> A questo punto è stato distribuito il cloud toohello applicazione Azure. Tuttavia, prima di procedere, tenere presente che un'applicazione distribuita, anche se non è in esecuzione, continuerà tooaccrue tempo fatturabile per la sottoscrizione. È quindi estremamente importante eliminare le distribuzioni indesiderate dalla sottoscrizione di Azure.
> 
> 

## <a name="about-azure-deployment-projects"></a>Informazioni sui progetti di distribuzione di Azure
Ordinare toodeploy uno o più tooAzure applicazioni Java, è necessario un progetto di distribuzione di Azure. Ha il ruolo di hello di hello "pacchetto" in cui le applicazioni devono toobe racchiuse in ordine toobe pubblicato in Azure.

Oltre alle informazioni di hello relative alle applicazioni, un progetto di distribuzione di Azure contiene anche informazioni sugli altri componenti chiave della distribuzione, soprattutto: hello applicazione server contenitore toorun dell'app web e Java runtime toorun hello è in. Azure supporta un'ampia gamma di runtime e server applicazioni Java tra cui è possibile scegliere.

Sebbene l'esempio hello qui utilizzato è notevolmente semplificato per scopi didattici, un progetto di distribuzione di Azure può contenere anche altre importanti informazioni di configurazione che consente di toocreate quasi arbitrariamente complesse, scalabile e a disponibilità elevata, servizi cloud a più livelli con le applicazioni. È possibile abilitare l'**affinità di sessione (sessioni permanenti)**, la **memorizzazione rapida nella cache**, l'**offload SSL**, il **routing firewall/porta**, l'**accesso remoto** e altre potenti funzionalità.

Se è stata completata sezione precedente di hello di questa esercitazione ("toodeploy l'applicazione tooAzure, hello in modo semplice e rapido"), verrà visualizzato un nuovo progetto di distribuzione di Azure in Esplora progetti generato automaticamente e denominate di hello " **MyHelloWorld_onAzure**".

Si potrebbe essere stata avviata anche in questa esercitazione creando innanzitutto un progetto di distribuzione di Azure vuoto e quindi aggiungendo tooit le applicazioni. È il processo, ma che garantisce maggiore controllo sulla configurazione iniziale di hello dall'inizio di hello.

toocreate un nuovo progetto di distribuzione di Azure da zero, fare clic su hello **New Azure Deployment Project** pulsante ![][ic710876].

Indipendentemente dal fatto che si utilizza un progetto di distribuzione di Azure già esistente, o crearne uno nuovo da zero, sono in grado di toochange le impostazioni di configurazione e i componenti, ad esempio hello JDK o hello server applicazioni, allo stesso modo in qualsiasi momento.

hello toochange JDK, o server applicazioni hello o elenco di applicazioni hello in un progetto di distribuzione di Azure esistente:

1. Espandere il nodo di progetto hello (ad esempio **MyHelloWorld_onAzure**) in Esplora progetti hello

2. Fare clic con il pulsante destro del mouse su **WorkerRole1**

3. Espandere hello **Azure** sottomenu nel menu di scelta rapida hello

4. Fare clic su **Server Configuration**

Indipendentemente dal valore se è stato avviato questi passaggi di configurazione server modificando un progetto di distribuzione di Azure esistente, come illustrato in precedenza o crearne uno nuovo da zero, verrà visualizzato hello stesso tipo di finestre di dialogo consentono di tooconfigure il JDK, server e dell'applicazione componenti. toolearn più come impostazioni hello toochange nelle finestre di dialogo, ad esempio toochange hello JDK, hello server applicazioni e aggiungere o rimuovere applicazioni in una distribuzione, vedere hello [proprietà di configurazione Server] [ Server configuration properties] articolo.

## <a name="windows-only-toodeploy-your-application-toohello-compute-emulator"></a>Solo Windows: toodeploy toohello l'applicazione dell'emulatore di calcolo

> [!NOTE]
> Hello dell'emulatore di Azure è disponibile solo in Windows. Ignorare questa sezione se si usa un sistema operativo diverso da Windows.
> 
> 

Se è stato creato un nuovo progetto di distribuzione di Azure descritto in precedenza, ovvero in modo implicito pubblicando tooAzure l'applicazione, come segue hello hello JDK e server applicazioni sono state configurate per il cloud hello, ma non per l'emulazione locale. tooprepare il progetto di test nell'emulatore locale hello, seguire questi passaggi:

1. In Project Explorer (Esplora progetti) di Eclipse fare clic su **MyHelloWorld_onAzure**.

2. Fare clic con il pulsante destro del mouse su **WorkerRole1**.

3. Espandere hello **Azure** sottomenu nel menu di scelta rapida hello.

4. Fare clic su **Server Configuration**.

5. In hello **JDK** scheda, controllare se hello toolkit ha preconfigurato automaticamente un valore predefinito JDK locale. In caso contrario, o se si desidera hello toochange si presuppone che le impostazioni predefinite, verificare che hello **hello Usa JDK da questo percorso di file per test locale** casella di controllo è selezionata e viene specificato il percorso di installazione di JDK che si desidera toouse hello. Se si desidera toochange, fare clic su hello **Sfoglia** e utilizza il controllo di hello Sfoglia, selezionare il percorso di directory hello di hello JDK toouse.

6. Fare clic su hello **Server** scheda.

7. In hello **percorso server locale** casella di testo nella parte inferiore di hello della finestra di dialogo hello, immettere il percorso di hello di un server installato in locale che corrisponde al tipo hello e il numero di versione principale del server di hello selezionato nella parte superiore di hello della finestra di dialogo hello in Hello **distribuire un server di questo tipo** casella di controllo. Se si desidera toouse un tipo diverso o una versione principale del server applicazioni hello, modificare innanzitutto selezione hello sotto tale casella di controllo.

8. Fare clic su **OK**.

9. Nella barra degli strumenti di hello Eclipse, fare clic su hello **Run in Azure Emulator** pulsante ![][ic710879]. Se hello **Run in Azure Emulator** pulsante non è abilitato, verificare che **MyHelloWorld_onAzure** sia selezionato in Project Explorer di Eclipse e verificare che Project Explorer di Eclipse abbia lo stato attivo come hello finestra corrente. Verrà prima di avviare una compilazione completa del progetto e quindi avviare l'applicazione web Java nell'emulatore di calcolo hello. (Si noti che, a seconda delle caratteristiche di prestazioni del computer, hello prima build può richiedere tra pochi secondi tooa alcuni minuti, mentre le build successive riceverà più velocemente.) Dopo la prima istruzione di compilazione hello è stata completata, verrà richiesto da controllo Account utente (UAC) di Windows tooallow toomake questo comando Modifica tooyour computer. Fare clic su **Sì**.

> [!IMPORTANT]
> Se non è possibile visualizzare hello UAC, Chiedi hello barra delle applicazioni di Windows per l'icona di controllo dell'account utente di hello e selezionarla prima. In alcuni casi hello prompt dei comandi di controllo dell'account utente non viene visualizzato come una finestra in primo piano, ma è visibile solo come icona sulla barra delle applicazioni.
> 
> 

1. Esaminare l'output di hello di toodetermine dell'interfaccia utente emulatore di hello calcolo se sono presenti eventuali problemi con il progetto. A seconda della distribuzione del contenuto hello potrebbe richiedere un paio di minuti per toobe l'applicazione completamente avviato nell'emulatore di calcolo hello.

2. Avviare il browser e utilizzare URL hello `http://localhost:8080/MyHelloWorld` come indirizzo hello (hello `MyHelloWorld` parte dell'URL hello è distinzione maiuscole/minuscole). È necessario visualizzare l'applicazione MyHelloWorld (output di hello di index.jsp), un simile toohello seguente immagine:

   ![][ic589579]

Quando si è pronti toostop applicazione in esecuzione nell'emulatore di calcolo hello, nella barra degli strumenti di hello Eclipse, fare clic su hello **Reimposta emulatore di Azure** pulsante ![][ic710880].

## <a name="toodelete-your-deployment"></a>toodelete la distribuzione
Verificare la distribuzione in Azure Toolkit per Eclipse, hello toodelete che **MyHelloWorld_onAzure** è selezionata in Project Explorer di Eclipse, assicurarsi di hello Project Explorer di Eclipse abbia finestra corrente hello lo stato attivo e quindi fare clic su Hello **Annulla pubblicazione** pulsante ![][ic710883], sulla barra degli strumenti di Eclipse hello. (È possibile farlo hello stessa operazione facendo clic **MyHelloWorld_onAzure** in Project Explorer di Eclipse, facendo clic su **Azure** e quindi fare clic su **Undeploy from Azure Cloud**.) Verrà visualizzata hello **Annulla pubblicazione progetto Azure** finestra di dialogo.

![][ic719491]

Selezionare hello sottoscrizione e il servizio cloud che contiene la distribuzione, distribuzione selezionare hello che desidera toodelete e quindi fare clic su **Annulla pubblicazione**.

(Una distribuzione di hello toousing alternativo hello toolkit toodelete è hello toouse **servizi Cloud** sezione del portale di gestione Azure hello: passare distribuzione tooyour, selezionarlo e quindi fare clic su hello **eliminare** pulsante. Si interrompe e quindi si elimina, hello distribuzione. Se si desidera solo distribuzione hello toostop e non eliminarla, fare clic su hello **arrestare** pulsante anziché hello **eliminare** pulsante, ma come indicato in precedenza, se non si elimina la distribuzione di hello, verrà spese fatturabili continuare tooaccrue per la distribuzione anche se è stato arrestato).

## <a name="see-also"></a>Vedere anche
[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]

[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Novità in Azure Toolkit per Eclipse hello][What's New in hello Azure Toolkit for Eclipse]

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
