---
title: aaaPrepare toopublish o distribuire un'applicazione Azure da Visual Studio | Documenti Microsoft
description: Informazioni su hello procedure tooset dei cloud e account servizi di archiviazione e configurare l'applicazione Azure.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: b5231d400e2ad9e20c3f21bad48a77c328b1f7a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-toopublish-or-deploy-an-azure-application-from-visual-studio"></a>Preparare tooPublish oppure distribuire un'applicazione Azure da Visual Studio
## <a name="overview"></a>Panoramica
Prima di poter pubblicare un progetto servizio cloud, è necessario impostare hello seguenti servizi:

* Oggetto **servizio cloud** toorun i ruoli nell'ambiente Azure hello
* Oggetto **account di archiviazione** servizi Blob, coda e tabella di toohello che fornisce l'accesso.

Utilizzare hello seguendo procedure tooset di questi servizi e configurare l'applicazione

## <a name="create-a-cloud-service"></a>Creare un servizio cloud
toopublish un tooAzure servizio cloud, è innanzitutto necessario creare un servizio cloud che esegua i ruoli nell'ambiente Azure hello. È possibile creare un servizio cloud in hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), come descritto nella sezione hello **toocreate un servizio cloud utilizzando hello portale di Azure classico**, più avanti in questo argomento. È anche possibile creare un servizio cloud in Visual Studio utilizzando hello pubblicazione guidata.

### <a name="toocreate-a-cloud-service-by-using-visual-studio"></a>toocreate un servizio cloud con Visual Studio
1. Aprire il menu di scelta rapida hello per hello progetto Azure e scegliere **pubblica**.

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. Se è stato eseguito l'accesso, accedere con il nome utente e password di account Microsoft hello o un account aziendale associato alla sottoscrizione di Azure.
3. Scegliere hello **Avanti** pulsante tooadvance toohello **impostazioni** pagina.

    ![Impostazioni comuni della Pubblicazione guidata](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. In hello **servizi Cloud** scegliere **Crea nuovo**. Hello **Crea servizi Azure** viene visualizzata la finestra.
5. Immettere il nome di hello del servizio cloud. nome Hello fa parte di hello URL per il servizio e pertanto deve essere globalmente univoco. nome di Hello non è tra maiuscole e minuscole.

### <a name="toocreate-a-cloud-service-by-using-hello-azure-classic-portal"></a>toocreate un servizio cloud utilizzando hello portale di Azure classico
1. Accedi toohello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkId=253103) nel sito Web Microsoft hello.
2. toodisplay (facoltativo) un elenco di servizi cloud che è già stato creato, scegliere il collegamento servizi Cloud hello sul lato sinistro di hello della pagina hello.
3. Scegliere hello  **+**  icona in hello in basso a sinistra angolo e quindi scegliere **servizio Cloud** hello dal menu visualizzato. Verrà visualizzata un'altra schermata con due opzioni disponibili, **Creazione rapida** e **Creazione personalizzata**. Se si sceglie **creazione rapida**, è possibile creare un servizio cloud semplicemente specificandone il relativo URL e hello area in cui si sarà ospitato fisicamente. L'opzione **Creazione personalizzata**consente di pubblicare immediatamente un servizio cloud specificando un pacchetto (file con estensione .cspkg), un file di configurazione (file con estensione .cscfg) e un certificato. Creazione personalizzata non è necessario se si intende toopublish il servizio cloud utilizzando hello **pubblica** comando in un progetto Azure. Hello **pubblica** comando è disponibile nel menu di scelta rapida hello per un progetto Azure.
4. Scegliere **creazione rapida** toolater pubblicare il servizio cloud con Visual Studio.
5. Specificare un nome per il servizio cloud. URL completo di Hello viene visualizzato il nome toohello successivo.
6. Nell'elenco di hello, scegliere l'area di hello in cui si trovano la maggior parte degli utenti.
7. Nella parte inferiore di hello della finestra hello, scegliere hello **Crea servizio Cloud** collegamento.

## <a name="create-a-storage-account"></a>Creare un account di archiviazione
Un account di archiviazione fornisce l'accesso toohello i servizi Blob, coda e tabella. È possibile creare un account di archiviazione usando Visual Studio o hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkId=253103).

### <a name="toocreate-a-storage-account-by-using-visual-studio"></a>toocreate un account di archiviazione usando Visual Studio
1. In **Esplora soluzioni**, aprire il menu di scelta rapida hello per hello **archiviazione** nodo e quindi scegliere **crea Account di archiviazione**.

    ![Creare un nuovo account di archiviazione di Azure](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. Selezionare o immettere le seguenti informazioni per hello nuovo account di archiviazione in hello hello **crea Account di archiviazione** la finestra di dialogo.

   * Hello desiderato di account di archiviazione hello tooadd toowhich di sottoscrizione di Azure.
   * Hello nome toouse per il nuovo account di archiviazione hello.
   * area di Hello o un gruppo di affinità (ad esempio Stati Uniti occidentali o Asia orientale).
   * Hello tipo di replica desiderato toouse hello account di archiviazione, ad esempio con ridondanza geografica.
3. Al termine, scegliere **crea**.hello nuovo account di archiviazione viene visualizzato in hello **archiviazione** nell'elenco **Esplora Server**.

### <a name="toocreate-a-storage-account-by-using-hello-azure-classic-portal"></a>toocreate un account di archiviazione tramite hello portale di Azure classico
1. Accedi toohello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkId=253103) nel sito Web Microsoft hello.
2. Tooview (facoltativo) l'account di archiviazione, scegliere hello **archiviazione** collegamento nel Pannello di hello hello il lato sinistro di pagina hello.
3. Nell'angolo inferiore sinistro hello della pagina hello scegliere hello  **+**  icona.
4. Nel menu hello visualizzato, scegliere **archiviazione**, quindi scegliere **creazione rapida**.
5. Assegnare account di archiviazione hello un nome che si tradurrà in un url univoco.
6. Assegnare un nome al servizio cloud. URL completo di Hello viene visualizzato il nome toohello successivo.
7. Nell'elenco hello delle aree, scegliere un'area in cui si trovano la maggior parte degli utenti.
8. Specificare se si desidera tooenable-replica geografica. Se si abilita la replica geografica, i dati verranno salvati in più posizioni fisiche tooreduce hello probabilità perdita. Questa funzionalità rende più costosa archiviazione, ma è possibile ridurre il costo di hello abilitando posizione geografica, quando si crea l'account di archiviazione hello anziché aggiungere funzionalità hello in un secondo momento. Per altre informazioni, vedere [Replica geografica](http://go.microsoft.com/fwlink/?LinkId=253108).
9. Nella parte inferiore di hello della finestra hello, scegliere hello **crea Account di archiviazione** collegamento.

Dopo aver creato l'account di archiviazione, si noterà hello gli URL che è possibile utilizzare le risorse tooaccess in ognuno dei servizi di archiviazione Azure hello e hello anche le chiavi di accesso primarie e secondarie per l'account. Utilizzare questi tasti tooauthenticate richieste nei servizi di archiviazione hello.

> [!NOTE]
> chiave di accesso secondaria Hello fornisce hello stesso accesso tooyour account di archiviazione come chiave di accesso primaria hello e viene generato come una copia di backup deve essere compromessa la chiave di accesso primaria. È anche consigliabile rigenerare regolarmente le chiavi di accesso. È possibile modificare una connessione stringa impostazione toouse hello chiave secondaria mentre si rigenera una chiave primaria hello, quindi è possibile modificarla in chiave primaria di toouse hello rigenerata mentre si rigenera la chiave secondaria hello.
>
>

## <a name="configure-your-app-toouse-services-provided-by-hello-storage-account"></a>Configurare i servizi toouse app forniti tramite account di archiviazione hello
È necessario configurare un ruolo che accede ai servizi toouse hello archiviazione di Azure servizi di archiviazione creato. toodo, è possibile utilizzare più configurazioni del servizio per il progetto Azure. Per impostazione predefinita, nel progetto Azure vengono create due configurazioni. Utilizzando più configurazioni del servizio, è possibile utilizzare hello stessa connessione stringa nel codice, ma dispone di un valore diverso per una stringa di connessione in ogni configurazione del servizio. Ad esempio, è possibile utilizzare un servizio configurazione toorun e debug dell'applicazione localmente utilizzando l'emulatore di archiviazione di Azure hello e una toopublish di configurazione del servizio diverso tooAzure l'applicazione. Per altre informazioni sulle configurazioni del servizio, vedere [Configurazione di un progetto Azure usando configurazioni del servizio multiple](vs-azure-tools-multiple-services-project-configurations.md).

### <a name="tooconfigure-your-application-toouse-services-that-hello-storage-account-provides"></a>Fornisce i servizi dell'applicazione toouse che hello account di archiviazione tooconfigure
1. In Visual Studio aprire la soluzione Azure. In Esplora soluzioni, aprire il menu di scelta rapida hello per ogni ruolo nel progetto Azure che accede ai servizi di archiviazione hello e scegliere **proprietà**. Una pagina con il nome di hello del ruolo hello viene visualizzata nell'editor di Visual Studio hello. pagina di Hello Visualizza campi hello per hello **configurazione** scheda.
2. Nelle pagine delle proprietà di hello per ruolo hello, scegliere **impostazioni**.
3. In hello **configurazione del servizio** scegliere nome hello della configurazione del servizio hello che si desidera tooedit. Se si desidera toomake modifiche tooall hello configurazioni del servizio per questo ruolo, è possibile scegliere **tutte le configurazioni**.  Per ulteriori informazioni su come tooupdate configurazioni del servizio, vedere la sezione hello **gestire stringhe di connessione per gli account di archiviazione** in argomento hello [configurare hello ruoli per un servizio Cloud di Azure con Visual Studio ](vs-azure-tools-configure-roles-for-cloud-service.md).
4. toomodify le impostazioni della stringa di connessione, scegliere hello **...** pulsante Avanti toohello impostazione. Hello **crea stringa di connessione di archiviazione** viene visualizzata la finestra di dialogo.
5. In **connettersi utilizzando**, scegliere hello **sottoscrizione** opzione.
6. In hello **sottoscrizione** scegliere la sottoscrizione. Se l'elenco di sottoscrizioni hello non include hello quello che si desidera, scegliere hello **Download impostazioni di pubblicazione** collegamento.
7. In hello **nome Account** scegliere il nome di account di archiviazione. Gli strumenti di Azure ottengono automaticamente le credenziali dell'account di archiviazione utilizzando file con estensione publishsettings hello. toospecify credenziali di account di archiviazione manualmente, scegliere hello **credenziali immesse manualmente** opzione e quindi continuare con questa procedura. È possibile ottenere il nome account di archiviazione e la chiave primaria da hello [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=213885). Se non si desidera toospecify le impostazioni dell'account di archiviazione manualmente, scegliere hello **OK** pulsante tooclose hello finestra di dialogo.
8. Scegliere hello **immettere l'account di archiviazione** collegamento credenziali.
9. In hello **nome Account** immettere hello nome dell'account di archiviazione.

   > [!NOTE]
   > Accedere al hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), quindi scegliere hello **archiviazione** pulsante. portale Hello Mostra un elenco di account di archiviazione. Se si sceglie un account, viene aperta una pagina corrispondente. È possibile copiare il nome di hello hello dell'account di archiviazione da questa pagina. Se si utilizza una versione precedente di portale classico hello, hello Nome account di archiviazione viene visualizzato nella hello **gli account di archiviazione** visualizzazione. toocopy il nome, evidenziarlo nel hello **proprietà** questa finestra consente di visualizzare e quindi premere Ctrl-C hello. nome hello toopaste in Visual Studio, scegliere hello **nome Account** testo casella e quindi scegliere i tasti Ctrl + V hello.
   >
   >
10. In hello **chiave dell'Account** casella, immettere la chiave primaria, oppure copiare e incollare da hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).
     Questa chiave toocopy:

    1. Nella parte inferiore di hello della pagina hello per account di archiviazione appropriato hello, scegliere hello **Gestisci chiavi** pulsante.
    2. In hello **Gestisci chiavi di accesso** pagina, selezionare il testo hello della chiave di accesso primaria hello e quindi premere hello Ctrl + C.
    3. In strumenti di Azure, incollare la chiave hello hello **chiave dell'Account** casella.
    4. È necessario selezionare una delle seguenti opzioni toodetermine hello modalità di accesso account di archiviazione hello hello servizio:

       * **Usa HTTP**. Questo è l'opzione standard hello. ad esempio `http://<account name>.blob.core.windows.net`.
       * **Usa HTTPS** per una connessione sicura. ad esempio `https://<accountname>.blob.core.windows.net`.
       * **Specifica endpoint personalizzati** per ognuno dei servizi hello tre. È quindi possibile digitare questi endpoint nel campo hello per servizio specifico hello.

         > [!NOTE]
         > Se si creano endpoint personalizzati, sarà possibile creare una stringa di connessione più complessa. Quando si utilizza questo formato di stringa, è possibile specificare endpoint servizio di archiviazione che includono un nome di dominio personalizzato registrato per l'account di archiviazione con hello servizio Blob. È inoltre possibile concedere accesso tooblob solo le risorse in un singolo contenitore tramite una firma di accesso condiviso. Per ulteriori informazioni su come toocreate endpoint personalizzati, vedere [configurare le stringhe di connessione di Azure Storage](storage/common/storage-configure-connection-string.md).
         >
         >
11. toosave queste modifiche della stringa di connessione, scegliere hello **OK** pulsante e quindi scegliere hello **salvare** sulla barra degli strumenti hello. Dopo avere salvato queste modifiche, è possibile ottenere il valore di hello di questa stringa di connessione nel codice utilizzando [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx). Quando si pubblica l'applicazione tooAzure, scegliere configurazione del servizio hello che contiene account di archiviazione di Azure hello hello stringa di connessione. Dopo l'applicazione viene pubblicata, verificare che l'applicazione hello funzioni come previsto nei servizi di archiviazione Azure hello

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su pubblicazione tooAzure app da Visual Studio, vedere [pubblicazione di un servizio Cloud utilizzando strumenti di Azure hello](vs-azure-tools-publishing-a-cloud-service.md).
