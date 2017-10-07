---
title: un account di archiviazione di Azure con la rete CDN Azure aaaIntegrate | Documenti Microsoft
description: Informazioni su come contenuto di toouse hello rete recapito contenuti (CDN) di Azure toodeliver larghezza di banda elevata memorizzando nella cache BLOB dall'archiviazione di Azure.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a>Integrare un account di archiviazione di Azure con la rete CDN di Azure
Rete CDN può essere abilitato toocache contenuto lo spazio di archiviazione Azure. Offre agli sviluppatori una soluzione globale per recapitare contenuti di larghezza di banda elevata memorizzando nella cache BLOB e il contenuto statico delle istanze di calcolo in nodi fisici di hello Uniti, Europa, Asia, Australia e del Sud America.

## <a name="step-1-create-a-storage-account"></a>Passaggio 1: Creare un account di archiviazione
Utilizzare hello seguendo procedure toocreate un nuovo account di archiviazione per una sottoscrizione di Azure. Un account di archiviazione consente di accedere ai servizi di archiviazione di Azure. account di archiviazione Hello rappresenta livello più elevato di hello dello spazio dei nomi di hello per accedere a ognuno dei componenti del servizio di archiviazione di Azure hello: Blob services, servizi di coda e i servizi di tabella. Per ulteriori informazioni, vedere toohello [tooMicrosoft introduzione di archiviazione di Azure](../storage/common/storage-introduction.md).

toocreate un account di archiviazione, è necessario essere amministratore del servizio hello o un coamministratore per hello associata sottoscrizione.

> [!NOTE]
> Esistono diversi metodi che è possibile utilizzare un account di archiviazione, tra cui hello portale di Azure e Powershell toocreate.  Per questa esercitazione, verrà usato hello portale di Azure.  
> 
> 

**toocreate un account di archiviazione per una sottoscrizione di Azure**

1. Accedi toohello [portale Azure](https://portal.azure.com).
2. In hello nell'angolo superiore sinistro, selezionare **New**. In hello **New** selezionare **dati e archiviazione**, quindi fare clic su **account di archiviazione**.
    
    Hello **creare account di archiviazione** pannello viene visualizzato.   

    ![Crea account di archiviazione][create-new-storage-account]  

3. In hello **nome** , digitare un nome di sottodominio. Il nome può contenere tra 3 e 24 lettere minuscole e numeri.
   
    Questo valore diventa il nome host hello all'interno di hello URI utilizzato per indirizzare le risorse Blob, coda o tabella per la sottoscrizione di hello. Per risolvere una risorsa contenitore nel servizio Blob hello, si utilizzerebbe un URI nel seguente formato, hello in  *&lt;StorageAccountLabel&gt;*  toohello valore digitato in **immettere un URL**:
   
    http://*&lt;EtichettaAccountArchiviazione&gt;*.blob.core.windows.net/*&lt;contenitorepersonale&gt;*
   
    **Importante:** hello sottodominio di hello form etichetta URL dell'account di archiviazione hello URI e deve essere univoco tra tutti i servizi ospitati in Azure.
   
    Questo valore è utilizzato anche come nome hello di questo account di archiviazione nel portale di hello o quando si accede a questo account a livello di codice.
4. Lasciare i valori predefiniti di hello per **modello di distribuzione**, **Account kind**, **prestazioni**, e **replica**. 
5. Seleziona hello **sottoscrizione** verrà utilizzato con account di archiviazione hello.
6. Selezionare o creare un **gruppo di risorse**.  Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Selezionare la località per l'account di archiviazione.
8. Fare clic su **Crea**. Hello creazione account di archiviazione hello potrebbe richiedere diversi minuti toocomplete.

## <a name="step-2-enable-cdn-for-hello-storage-account"></a>Passaggio 2: Abilitare la rete CDN per account di archiviazione hello

Con l'integrazione più recente di hello è ora possibile abilitare rete CDN per l'account di archiviazione senza lasciare l'estensione del portale di archiviazione. 

1. Selezionare l'account di archiviazione hello, cercare "CDN" o scorrere verso il basso dal menu di navigazione a sinistra di hello, quindi fare clic su "Rete CDN di Azure".
    
    Hello **rete CDN di Azure** pannello viene visualizzato.

    ![spostamento per l'abilitazione della rete CDN][cdn-enable-navigation]
    
2. Creare un nuovo endpoint immettendo le informazioni necessarie hello
    - **Profilo CDN**: è possibile creare un nuovo profilo o usarne uno esistente.
    - **Livello di prezzo**: È necessario solo tooselect prezzi di un livello se si crea un nuovo profilo di rete CDN.
    - **Nome endpoint rete CDN** : immettere un nome dell'endpoint a scelta.

    > [!TIP]
    > l'endpoint rete CDN Hello creato Usa hello nome host dell'account di archiviazione come origine per impostazione predefinita.

    ![cdn new endpoint creation][cdn-new-endpoint-creation]

3. Dopo la creazione del nuovo endpoint hello verrà visualizzata nell'elenco di endpoint hello precedente.

    ![nuovo endpoint di archiviazione rete CDN][cdn-storage-new-endpoint]

> [!NOTE]
> È anche possibile passare tooAzure CDN estensione tooenable rete CDN. [Esercitazione](#Tutorial-cdn-create-profile).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a>Passaggio 3: Abilitare funzionalità aggiuntive della rete CDN

Pannello "Rete CDN di Azure" account di archiviazione, fare clic su endpoint rete CDN hello dal Pannello di configurazione della rete CDN tooopen elenco hello. È possibile abilitare funzionalità aggiuntive della rete CDN per il recapito, ad esempio la compressione, la stringa di query, il filtro geografico. È anche possibile aggiungere endpoint rete CDN tooyour mapping del dominio personalizzato e abilitare il dominio personalizzato HTTPS.
    
![configurazione CDN di archiviazione della rete CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a>Passaggio 4: Accedere al contenuto della rete CDN
tooaccess memorizzato nella cache il contenuto nella rete CDN hello, utilizzare hello URL della rete CDN fornito nel portale di hello. indirizzo di Hello per un blob memorizzato nella cache sarà simile toohello seguenti:

http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\>

> [!NOTE]
> Dopo aver abilitato l'account di archiviazione tooa accesso alla rete CDN, tutti gli oggetti disponibili pubblicamente sono idonei per la memorizzazione nella cache perimetrale della rete CDN. Se si modifica un oggetto attualmente memorizzato nella cache di hello CDN, il nuovo contenuto hello non sarà disponibile tramite hello CDN fino a quando non hello CDN consente di aggiornare il contenuto quando scade il periodo time-to-live del contenuto memorizzato nella cache di hello.
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a>Passaggio 5: Rimuovere contenuto dalla rete CDN hello
Se non si desidera più toocache un oggetto in hello Azure rete CDN (Content Delivery), è possibile eseguire una delle hello alla procedura seguente:

* È possibile apportare hello contenitore privato anziché pubblico. Vedere [gestire BLOB e accesso in lettura anonimo toocontainers](../storage/blobs/storage-manage-access-to-resources.md) per ulteriori informazioni.
* È possibile disabilitare o eliminare l'endpoint rete CDN hello utilizzando hello portale di gestione.
* È possibile modificare il toorequests di rispondere più servizio ospitato toono per oggetto hello.

Un oggetto già memorizzato nella cache di hello CDN rimarrà memorizzato fino alla scadenza del periodo di time-to-live hello per oggetto hello o fino a quando non vengono eliminati l'endpoint di hello. Allo scadere hello time-to-live, hello CDN controllerà toosee se l'endpoint rete CDN hello è ancora valido e oggetto hello ancora accessibile in modo anonimo. In caso contrario, non verrà memorizzata non più oggetto hello.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Come tooMap CDN contenuto tooa dominio personalizzato](cdn-map-content-to-custom-domain.md)
* [Abilitare HTTPS per il dominio personalizzato](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
