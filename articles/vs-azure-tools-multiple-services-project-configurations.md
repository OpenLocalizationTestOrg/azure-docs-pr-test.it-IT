---
title: "aaaConfiguring del progetto Azure tramite più configurazioni del servizio | Documenti Microsoft"
description: Informazioni su come tooconfigure di Azure cloud progetto di servizio modificando i file servicedefinition. Csdef e ServiceConfiguration. cscfg hello.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 14222266093eb876db0ac9ce8d3d17a04c65d1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-your-azure-project-using-multiple-service-configurations"></a>Configurazione del progetto Azure tramite più configurazioni del servizio
Un progetto di servizio cloud di Azure include due file di configurazione: ServiceDefinition.csdef e ServiceConfiguration.cscfg. Questi file sono inclusi con l'applicazione di servizio cloud di Azure e distribuiti tooAzure.

* Hello **Servicedefinition** contiene metadati hello richieste dall'ambiente Azure per hello requisiti dell'applicazione di servizio cloud, inclusi i ruoli contenuti hello. Questo file contiene inoltre le impostazioni di configurazione che si applicano tooall istanze. Queste impostazioni di configurazione possono essere letti in fase di esecuzione utilizzando hello API Runtime di Hosting di servizi di Azure. Questo file non può essere aggiornato mentre il servizio è in esecuzione in Azure.
* Hello **ServiceConfiguration. cscfg** file imposta valori per le impostazioni di configurazione hello definite nel file di definizione del servizio hello e specifica il numero di hello di toorun istanze per ogni ruolo. Questo file può essere aggiornato mentre il servizio cloud è in esecuzione in Azure.

Hello Azure Tools per Microsoft Visual Studio forniscono pagine di proprietà che è possibile utilizzare le impostazioni di configurazione tooset archiviate in questi file. tooaccess hello pagine delle proprietà, fare doppio clic sul riferimento ruolo hello di sotto di progetto di servizio cloud di Azure hello in Esplora soluzioni o fare riferimento ruolo hello e scegliere **proprietà**, come illustrato nella seguente illustrazione hello.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Per informazioni su hello sottostante schemi per la definizione del servizio hello e file di configurazione del servizio, vedere hello [riferimento allo Schema](https://msdn.microsoft.com/library/azure/dd179398.aspx). Per ulteriori informazioni sulla configurazione del servizio, vedere [come servizi Cloud tooConfigure](cloud-services/cloud-services-how-to-configure.md).

## <a name="configuring-role-properties"></a>Configurazione delle proprietà del ruolo
pagine delle proprietà Hello per un ruolo web e un ruolo di lavoro sono simili, ma esistono alcune differenze, descritte nelle sezioni che seguono hello.

Da hello **la memorizzazione nella cache** pagina, è possibile configurare hello servizi di caching di Azure.

### <a name="configuration-page"></a>Pagina Configurazione
In hello **configurazione** pagina, è possibile impostare queste proprietà:

**Istanze**

Set hello **istanza** conteggio proprietà toohello numero di istanze servizio hello deve eseguire per questo ruolo.

Set hello **dimensioni delle macchine Virtuali** proprietà troppo**molto piccolo**, **Small**, **Media**, **grande**, o **Molto grande**.  Per altre informazioni, vedere [Dimensioni dei servizi cloud](cloud-services/cloud-services-sizes-specs.md).

**Azione di avvio** (solo ruolo Web)

Impostare questa proprietà toospecify che Visual Studio deve essere avviato un web browser per endpoint HTTP hello o endpoint HTTPS hello o entrambi quando avvia il debug.

Hello opzione endpoint HTTPS è disponibile solo se già stato definito un endpoint HTTPS per il ruolo. È possibile definire un endpoint HTTPS in hello **endpoint** pagina delle proprietà.

Se è già stato aggiunto un endpoint HTTPS, hello opzione endpoint HTTPS è abilitato per impostazione predefinita e Visual Studio verrà avviato un browser per questo endpoint quando si avvia il debug, inoltre tooa browser per l'endpoint HTTP. Ciò presuppone che siano abilitate entrambe le opzioni di avvio.

**Diagnostica**

Per impostazione predefinita, la diagnostica è abilitata per il ruolo Web hello. emulatore di archiviazione locale hello toouse vengono impostati Hello progetto servizio cloud di Azure e account di archiviazione. Quando si è pronti toodeploy tooAzure, è possibile selezionare pulsante Generatore hello (**...** ) toouse account di archiviazione hello tooupdate archiviazione di Azure nel cloud hello. È possibile trasferire account di archiviazione toohello hello diagnostica dati su richiesta o a intervalli pianificati automaticamente. Per altre informazioni sulla diagnostica di Azure, vedere [Abilitazione della diagnostica nei servizi cloud e nelle macchine virtuali di Azure](cloud-services/cloud-services-dotnet-diagnostics.md).

## <a name="settings-page"></a>Pagina Impostazioni
In hello **impostazioni** pagina, è possibile aggiungere le impostazioni di configurazione per il servizio. Tali impostazioni sono coppie nome/valore. Il codice in esecuzione nel ruolo hello può leggere i valori di hello delle impostazioni di configurazione in fase di esecuzione utilizzando le classi fornite da hello [libreria gestita di Azure](http://go.microsoft.com/fwlink?LinkID=171026). In particolare, hello [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx) il metodo restituisce il valore di hello di un'impostazione di configurazione denominata in fase di esecuzione.

### <a name="configuring-a-connection-string-tooa-storage-account"></a>Configurazione di un account di archiviazione tooa di stringa di connessione
Una stringa di connessione è un'impostazione di configurazione che fornisce informazioni di connessione e autenticazione per l'emulatore di archiviazione hello o per un account di archiviazione di Azure. Ogni volta che il codice deve accedere ai dati di servizi di archiviazione di Azure –, blob, coda o dati di tabella: dal codice in esecuzione in un ruolo, sarà necessario toodefine una stringa di connessione per l'account di archiviazione.

Una stringa di connessione che punta tooan account di archiviazione Azure è necessario utilizzare un formato definito. Per informazioni su come toocreate le stringhe di connessione, vedere [configurare le stringhe di connessione di Azure Storage](storage/common/storage-configure-connection-string.md).

Quando si è pronti tootest di servizi da servizi di archiviazione Azure hello oppure quando sei pronto a toodeploy il tooAzure servizio cloud, è possibile modificare il valore di hello di qualsiasi tooyour toopoint stringhe di connessione account di archiviazione di Azure. Selezionare (**…**), quindi **Immettere le credenziali dell'account di archiviazione**. Immettere le informazioni sull'account, inclusi il nome e la chiave dell'account. In hello **stringa di connessione di Account di archiviazione** nella finestra di dialogo è possibile anche indicare se si desidera endpoint HTTPS predefiniti di toouse hello (opzione predefinita di hello), gli endpoint HTTP di hello predefinito o personalizzato. È possibile decidere endpoint personalizzati toouse se è stato registrato un nome di dominio personalizzato per il servizio, come descritto in [configurare un nome di dominio personalizzato per i dati blob in un account di archiviazione di Azure](storage/blobs/storage-custom-domain-name.md).

> [!IMPORTANT]
> Prima di distribuire il servizio, è necessario modificare il tooan toopoint stringhe di connessione account di archiviazione di Azure. In mancanza di toodo ciò potrebbe causare il ruolo non toostart o toocycle tramite hello stati inizializzazione, occupati e arresto.
> 
> 

## <a name="endpoints-page"></a>Pagina Endpoint
Un ruolo di lavoro può disporre di qualsiasi numero di endpoint HTTP, HTTPS o TCP. Gli endpoint possono essere endpoint di input, sono disponibili tooexternal client, o endpoint interni, che sono ruoli tooother disponibili che sono in esecuzione nel servizio di hello.

* tooexternal disponibile nel client di endpoint HTTP toomake Web browser, modificare tooinput di tipo endpoint hello e specificare un nome e un numero di porta pubblica.
* toomake HTTPS tooexternal disponibile nel client di endpoint e browser Web, cambiare il tipo di endpoint di hello troppo**input**e specificare un nome, un numero di porta pubblica e un nome di certificato di gestione.
  
    Si noti che è possibile specificare un certificato di gestione, è necessario definire il certificato di hello in hello **certificati** pagina delle proprietà.
* toomake un endpoint disponibile per l'accesso interno da altri ruoli nel servizio cloud hello, modificare toointernal di tipo endpoint hello e specificare un nome e le possibili porte private per questo endpoint.

## <a name="local-storage-page"></a>Pagina Archiviazione locale
È possibile utilizzare hello **archiviazione locale** tooreserve pagina proprietà uno o più risorse di archiviazione locale per un ruolo. Una risorsa di archiviazione locale è una directory riservata nel file system di hello di hello macchina virtuale di Azure in cui è in esecuzione un'istanza di un ruolo.

## <a name="certificates-page"></a>Pagina Certificati
In hello **certificati** pagina, è possibile associare certificati al ruolo. certificati di Hello che si aggiungono possono essere utilizzati tooconfigure agli endpoint HTTPS in hello **endpoint** pagina delle proprietà.

Hello **certificati** pagina delle proprietà consente di aggiungere informazioni sulla configurazione del servizio tooyour certificati. Si noti che i certificati non sono inclusi con il servizio; è necessario caricare i certificati separatamente tooAzure tramite hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).

tooassociate un certificato con il ruolo, specificare un nome per il certificato di hello. Utilizzare questo certificato di toohello toorefer nome quando si configura un endpoint HTTPS sul hello **endpoint** pagina delle proprietà. Successivamente, specificare se l'archivio certificati hello è **computer locale** o **utente corrente** e il nome dell'archivio di hello hello. Infine, immettere l'identificazione personale del certificato hello. Se è certificato hello in hello utente corrente\Personale di archivio (personale), è possibile immettere l'identificazione personale del certificato hello selezionandolo hello da un elenco popolato. Se si trova in qualsiasi altra posizione, è possibile immettere manualmente il valore di identificazione personale hello.

Quando si aggiunge un certificato dall'archivio certificati hello, vengono aggiunti automaticamente i certificati intermedi toohello impostazioni di configurazione. Questi certificati intermedi devono anche essere caricati in ordine toocorrectly tooAzure configurare il servizio per SSL.

I certificati di gestione che è possibile associare il servizio si applicano tooyour servizio solo quando è in esecuzione nel cloud hello. Quando il servizio è in esecuzione nell'ambiente di sviluppo locale hello, utilizza un certificato standard gestito dall'emulatore di calcolo hello.

## <a name="configuring-hello-azure-cloud-service-project"></a>Configurazione di progetto di servizio cloud di Azure hello
impostazioni tooconfigure applicabili al progetto di servizio cloud di Azure intero tooan, si apre il menu di scelta rapida hello nodo del progetto e scegliere Proprietà tooopen le pagine delle proprietà. Hello nella tabella seguente mostra le pagine delle proprietà.

| Pagina Proprietà | Descrizione |
| --- | --- |
| Applicazione |In questa pagina, è possibile visualizzare informazioni sulla versione di hello degli strumenti di Azure che utilizza il progetto servizio cloud, ed è possibile eseguire l'aggiornamento di versione corrente di toohello degli strumenti di hello. |
| Eventi di compilazione |In questa pagina è possibile impostare gli eventi di pre-compilazione e di post-compilazione. |
| Sviluppo. |In questa pagina, è possibile specificare le istruzioni di configurazione di compilazione e le condizioni di hello in cui vengono eseguiti gli eventi di post-compilazione. |
| Web |In questa pagina, è possibile configurare le impostazioni relative a server web toohello. |

