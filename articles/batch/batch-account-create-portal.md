---
title: un account di Batch nel portale di Azure hello aaaCreate | Documenti Microsoft
description: Informazioni su come account toocreate un Batch di Azure in hello toorun portale Azure carichi di lavoro paralleli su larga scala nel cloud hello
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a>Creare un account Batch con hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](batch-account-create-portal.md)
> * [.NET per la gestione di Batch](batch-management-dotnet.md)
>
>

Informazioni su come l'account toocreate un Batch di Azure hello [portale di Azure][azure_portal], quindi scegliere Proprietà account hello che adattarlo allo scenario di calcolo. Informazioni in cui le proprietà dell'account importante toofind come chiavi di accesso e gli URL di account.

Per informazioni sugli account di Batch e scenari, vedere hello [panoramica delle funzioni](batch-api-basics.md).



## <a name="create-a-batch-account"></a>Creare un account Batch

Utilizzare hello portale toocreate un account Batch in uno dei due hello *modalità di allocazione del pool*: **Batch servizio** modalità o hello più recente **sottoscrizione utente** modalità, che richiede più configurazione. Per informazioni su queste due modalità, vedere hello [panoramica delle funzioni](batch-api-basics.md#account). Per le funzionalità della modalità di sottoscrizione utente hello, vedere anche hello [post di blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).

## <a name="batch-service-mode"></a>Modalità di servizio Batch



1. Accedi toohello [portale di Azure][azure_portal].
2. Fare clic su **Nuovo** > **Calcolo** > **Servizio Batch**.

    ![Batch in hello Marketplace][marketplace_portal]
3. Hello **nuovo Account Batch** pannello viene visualizzato. Vedere le descrizioni di hello di sotto di ciascun elemento del pannello.

    ![Creare un account Batch][account_portal]

    a. **Nome dell'account**: nome dell'account Batch hello scelto deve essere univoco all'interno di hello regione di Azure in cui viene creato l'account di hello (vedere **percorso** sotto). nome dell'account Hello può contenere solo caratteri minuscoli o numeri e deve essere compresa tra 3 e 24 caratteri.

    b. **Sottoscrizione**: hello sottoscrizione in cui hello toocreate account Batch. Se è presente solo una sottoscrizione, è selezionata per impostazione predefinita.

    c. **Modalità di allocazione pool**: selezionare **Batch service**.

    c. **Gruppo di risorse**: selezionare un gruppo di risorse esistente per il nuovo account Batch. È possibile crearne facoltativamente uno nuovo.

    d. **Percorso**: hello Azure area in cui hello toocreate account Batch. Solo le aree di hello è supportate per la sottoscrizione e il gruppo di risorse vengono visualizzate come opzioni.

    e. **Account di archiviazione** (facoltativo): account di Archiviazione di Azure per uso generico associato all'account Batch. Tale operazione è consigliata per la maggior parte degli account Batch. Per altri dettagli, vedere più avanti [Account di archiviazione di Azure collegato](#linked-azure-storage-account) .

4. Fare clic su **crea** account hello toocreate.

   portale Hello indica la distribuzione è in corso. Al termine, un viene visualizzata una notifica **Le distribuzioni sono riuscite** in **Notifiche**.

## <a name="user-subscription-mode"></a>Modalità di sottoscrizione utente

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a>Consente di Azure Batch tooaccess hello della sottoscrizione (operazione monouso)
Quando si crea il primo account Batch in modalità di sottoscrizione utente, eseguire la sottoscrizione con Batch hello tooregister i passaggi seguenti. (Se viene eseguita in precedenza questa operazione, ignorare toohello nella sezione successiva).

1. Accedi toohello [portale di Azure][azure_portal].

2. Fare clic su **più servizi** > **sottoscrizioni**, fare clic su sottoscrizione hello da toouse per hello account Batch.

3. In hello **sottoscrizione** pannello, fare clic su **Access control (IAM)** > **Aggiungi**.

    ![Controllo di accesso alla sottoscrizione][subscription_access]

4. In hello **aggiungere autorizzazioni** blade, seleziona hello **collaboratore** ruolo, cercare hello API Batch. Fino a individuare hello API di ricerca per ognuna di queste stringhe:
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. I tenant di Azure AD più recenti potrebbero usare questo nome.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** ID hello per hello API Batch. 

5. Dopo aver individuato hello API Batch, selezionarlo e fare clic su **salvare**.

    ![Aggiungere le autorizzazioni di Batch][add_permission]

### <a name="create-a-key-vault"></a>Creare un insieme di credenziali delle chiavi
In modalità di sottoscrizione utente, è necessario un insieme di credenziali chiave di Azure che appartiene toothe stesso gruppo di risorse hello Batch account toobe creato. Verificare che il gruppo di risorse hello è in un'area in cui è Batch [disponibile](https://azure.microsoft.com/regions/services/) e che supporta la sottoscrizione.

1. In hello [portale di Azure][azure_portal], fare clic su **New** > **sicurezza + identità** > **insieme di credenziali chiave** .

2. In hello **Crea insieme di credenziali chiave** pannello, immettere un nome per l'insieme di credenziali chiave hello e creare un gruppo di risorse nell'area di hello desiderato per l'account Batch. Lasciare le impostazioni di valori predefiniti rimanenti hello, quindi fare clic su **crea**.

### <a name="create-a-batch-account"></a>Creare un account Batch

1. In hello [portale di Azure][azure_portal], fare clic su **New** > **calcolo** > **servizio Batch**.

    ![Batch in hello Marketplace][marketplace_portal]
3. Hello **nuovo Account Batch** pannello viene visualizzato. Vedere le descrizioni di hello di sotto di ciascun elemento del pannello.

    ![Creare un account Batch][account_portal_byos]

    a. **Nome dell'account**: nome dell'account Batch hello scelto deve essere univoco all'interno di hello regione di Azure in cui viene creato l'account di hello (vedere **percorso** sotto). nome dell'account Hello può contenere solo caratteri minuscoli o numeri e deve essere compresa tra 3 e 24 caratteri.

    b. **Sottoscrizione**: se si dispone di più di una sottoscrizione, selezionare una sottoscrizione hello registrati con hello servizio Batch.

    c. **Modalità di allocazione pool**: selezionare **Sottoscrizione utente**.

    d. **Insieme di credenziali chiave**: hello selezionare insieme di credenziali chiave creata per l'account Batch nella sezione precedente hello. In modo facoltativo creare un nuovo insieme di credenziali delle chiavi. Dopo aver selezionato l'insieme di credenziali hello, selezionare hello casella di controllo toogrant Azure Batch accesso toohello chiave dell'insieme di credenziali.

    c. **Gruppo di risorse**: gruppo di risorse selezionare hello in cui viene creato l'insieme di credenziali chiave hello.

    d. **Percorso**: hello Azure area in cui è stato creato hello chiave dell'insieme di credenziali per l'account Batch hello.

    e. **Account di archiviazione** (facoltativo): account di Archiviazione di Azure per uso generico associato all'account Batch. Tale operazione è consigliata per la maggior parte degli account Batch. Per altri dettagli, vedere più avanti [Account di archiviazione di Azure collegato](#linked-azure-storage-account) .

4. Fare clic su **crea** account hello toocreate.

   portale Hello indica la distribuzione è in corso. Al termine, un viene visualizzata una notifica **Le distribuzioni sono riuscite** in **Notifiche**.



## <a name="view-batch-account-properties"></a>Visualizzare le proprietà dell'account Batch
Una volta hello account è stato creato, è possibile aprire hello **pannello account Batch** tooaccess le impostazioni e proprietà. È possibile accedere a tutte le impostazioni dell'account e le proprietà tramite i menu a sinistra del Pannello di account Batch hello hello.

![Pannello Account Batch nel portale di Azure][account_blade]

* **URL dell'account batch**: quando si sviluppa un'applicazione con hello [API Batch](batch-apis-tools.md#azure-accounts-for-batch-development), è necessario un tooaccess URL di account delle risorse di Batch. Un URL dell'account Batch è hello seguente formato:

    `https://<account_name>.<region>.batch.azure.com`

![URL dell'account Batch nel portale][account_url]

* **Le chiavi di accesso** (modalità servizio Batch): tooauthenticate accesso tooyour account Batch dall'applicazione, è necessario una chiave di accesso di account. Questa impostazione non è disponibile in modalità di sottoscrizione utente, in cui si usa l'autenticazione di Azure Active Directory.

    tooview o rigenerare le chiavi di accesso dell'account Batch, immettere `keys` nel menu a sinistra di hello **ricerca** nel Pannello di account Batch hello e quindi selezionare **chiavi**.

    ![Chiavi dell'account Batch nel portale di Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a>Account di archiviazione di Azure collegato

Facoltativamente, è possibile collegare un utilizzo generale tooyour di account di archiviazione di Azure account Batch. Hello [pacchetti di applicazioni](batch-application-packages.md) funzionalità di Batch utilizza l'archiviazione Blob di Azure, come hello [Batch File convenzioni .NET](batch-task-output.md) libreria. Queste funzionalità opzionali facilitano la distribuzione delle applicazioni che eseguono le attività Batch hello e rendere persistenti i dati di hello che producono.

È consigliabile creare un nuovo account di archiviazione da usare esclusivamente con l'account Batch.

![Creazione di un account di archiviazione per utilizzo generico][storage_account]

> [!NOTE]
> Azure Batch supporta attualmente solo hello Storage account tipi generici. Questo tipo di account è descritto nel passaggio 5, [Creare un account di archiviazione] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).
>
>

> [!WARNING]
> Prestare attenzione quando si rigenerano le chiavi di accesso hello di un account di archiviazione collegato. Rigenera solo una chiave di account di archiviazione e fare clic su **sincronizzazione delle chiavi** su hello collegato blade di account di archiviazione. Attendere cinque minuti tooallow hello chiavi toopropagate toohello nodi di calcolo nei pool, quindi rigenerare e sincronizzare hello altre chiavi, se necessario. Se si rigenera entrambe le chiavi in hello stesso tempo, i nodi di calcolo non saranno in grado di toosynchronize ognuna delle due chiavi e account di accesso toohello archiviazione andranno perse.
>
>

![Rigenerazione delle chiavi degli account di archiviazione][4]

## <a name="batch-service-quotas-and-limits"></a>Quote e limiti del servizio Batch
Essere consapevoli che come con la sottoscrizione di Azure e altri Azure dei servizi, alcuni [quote e limiti](batch-quota-limit.md) applicare tooBatch account. Le quote correnti per un account Batch vengono visualizzate nel portale di hello nell'account hello **proprietà**.

![Quote dell'account Batch nel portale di Azure][quotas]



Inoltre, molte di queste quote possono essere aumentate semplicemente con una richiesta di supporto prodotto gratuito inviata nel portale di Azure hello. Vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md) per ulteriori informazioni sulla richiesta di quota aumenta.

## <a name="other-batch-account-management-options"></a>Altre opzioni di gestione dell'account Batch
Inoltre toousing hello portale di Azure, è anche possibile creare e gestire gli account Batch con seguenti hello:

* [Cmdlet di PowerShell per Batch](batch-powershell-cmdlets-get-started.md)
* [Interfaccia della riga di comando di Azure](batch-cli-get-started.md)
* [.NET per la gestione di Batch](batch-management-dotnet.md)

## <a name="next-steps"></a>Passaggi successivi
* Vedere hello [Cenni preliminari sulle funzionalità di Batch](batch-api-basics.md) toolearn ulteriori informazioni sulle funzionalità e concetti relativi al servizio Batch. articolo Hello illustra risorse Batch primarie hello come pool, nodi di calcolo, i processi e attività e viene fornita una panoramica di hello funzionalità del servizio che consentono l'esecuzione del carico di lavoro di calcolo su larga scala.
* Nozioni di base hello dello sviluppo di un'applicazione abilitata per Batch utilizzando hello [libreria client .NET per Batch](batch-dotnet-get-started.md) o [Python](batch-python-tutorial.md). Questi articoli introduttivi consentono di eseguire un'applicazione funzionante che utilizza hello Batch servizio tooexecute un carico di lavoro in più nodi di calcolo e include l'utilizzo di archiviazione di Azure per il recupero e la gestione temporanea di file del carico di lavoro.

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Rigenerazione delle chiavi degli account di archiviazione"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
