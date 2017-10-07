---
title: dominio personalizzato tooa contenuto di rete CDN di Azure aaaMap | Documenti Microsoft
description: Informazioni su come rete CDN di Azure toomap contenuto tooa di dominio personalizzato.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d3ee77297f1dd7dbf31a9391191cc2910fbd2cee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="map-azure-cdn-content-tooa-custom-domain"></a>Eseguire il mapping di dominio personalizzato tooa contenuto di rete CDN di Azure
È possibile eseguire il mapping di un endpoint rete CDN tooa di dominio personalizzato in ordine toouse il nome di dominio in toocached URL contenuto anziché utilizzare un sottodominio di azureedge.net.

Esistono due modi toomap endpoint della rete CDN tooa dominio personalizzato:

1. [Creare un record CNAME con il registrar ed eseguire il mapping personalizzato domini e sottodomini toohello endpoint della rete CDN](#register-a-custom-domain-for-an-azure-cdn-endpoint).
   
    Un record CNAME è una funzionalità DNS che esegue il mapping di un dominio di origine, ad esempio `www.contosocdn.com` o `cdn.contoso.com`, tooa dominio di destinazione. In questo caso, il dominio di origine hello è il dominio personalizzato e un sottodominio (un sottodominio, ad esempio **www** o **cdn** è sempre necessario). dominio di destinazione Hello è l'endpoint rete CDN.  
   
    processo Hello di mapping di endpoint della rete CDN tooyour dominio personalizzato può, tuttavia, comportare un breve periodo di tempo di inattività per il dominio hello durante la registrazione di dominio hello in hello portale di Azure.
2. [Aggiungere un passaggio di registrazione intermedio con **cdnverify**](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    Se il dominio personalizzato supporta attualmente un'applicazione con un contratto di servizio (SLA) che richiede che vi siano periodi di inattività, è quindi possibile utilizzare hello Azure **cdnverify** tooprovide sottodominio una registrazione intermedia passaggio in modo che gli utenti saranno in grado di tooaccess al dominio durante hello DNS mapping viene eseguita.  

Dopo aver registrato il dominio personalizzato utilizzando uno dei hello sopra procedure, è troppo[verificare che il sottodominio personalizzato hello fa riferimento a endpoint della rete CDN](#verify-that-the-custom-subdomain-references-your-cdn-endpoint).

> [!NOTE]
> È necessario creare un record CNAME con il toomap registrar di dominio dell'endpoint CDN toohello di dominio. I record CNAME eseguono il mapping di sottodomini specifici, ad esempio `www.contoso.com` o `cdn.contoso.com`. Non è possibile toomap un dominio radice tooa record CNAME, ad esempio `contoso.com`.
> 
> Un sottodominio può essere associato a un solo endpoint della rete CDN. record CNAME creato Hello indirizza tutto il traffico indirizzato toohello sottodominio toohello specificato endpoint.  Ad esempio, se si associa `www.contoso.com` all'endpoint della rete CDN, non è possibile associarlo ad altri endpoint di Azure, come un endpoint dell'account di archiviazione o del servizio cloud. Tuttavia, è possibile utilizzare sottodomini diversi da hello nello stesso dominio per gli endpoint di servizio diverso. È anche possibile mappare i sottodomini diversi toohello stesso endpoint rete CDN.
> 
> Per **rete CDN di Azure da Verizon** endpoint (Standard e Premium), si noti che occupi troppo**90 minuti** per i nodi di edge tooCDN toopropagate modifiche del dominio personalizzato.
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>Registrare un dominio personalizzato per un endpoint della rete CDN di Azure
1. Accedere al hello [portale Azure](https://portal.azure.com/).
2. Fare clic su **Sfoglia**, quindi **CDN profili**, quindi hello profilo CDN con endpoint hello desiderato toomap tooa personalizzato dominio.  
3. In hello **profilo CDN** pannello, fare clic sull'endpoint rete CDN hello con cui si desidera sottodominio hello tooassociate.
4. Nella parte superiore di hello del pannello endpoint hello, fare clic su hello **Aggiungi dominio personalizzato** pulsante.  In hello **aggiungere un dominio personalizzato** pannello, si noterà hello endpoint nome host, derivato dall'endpoint della rete CDN, toouse nella creazione di un nuovo record CNAME. Hello formato dell'indirizzo di nome host hello verrà visualizzato come  **&lt;EndpointName >. azureedge.net**.  È possibile copiare questo toouse nome host per la creazione di record CNAME hello.  
5. Sito web del registrar di dominio tooyour passare e individuare la sezione hello per la creazione di record DNS. Queste informazioni possono essere disponibili in una sezione come **Domain Name**, **DNS** o **Name Server Management**.
6. Trovare la sezione hello per la gestione dei record CNAME. È possibile avere una pagina di impostazioni avanzate tooan toogo e cercare parole hello CNAME, Alias o diversi sottodomini.
7. Creare un nuovo record CNAME che esegue il mapping del sottodominio scelto (ad esempio, **www** o **cdn**) nome di host toohello fornito in hello **aggiungere un dominio personalizzato** blade. 
8. Restituire toohello **aggiungere un dominio personalizzato** pannello e immettere il dominio personalizzato, inclusi il sottodominio hello, nella finestra di dialogo hello. Ad esempio, immettere il nome di dominio hello in formato hello `www.contoso.com` o `cdn.contoso.com`.   
   
   Azure è necessario verificare che i record CNAME hello esista per il nome di dominio hello immesso. Se hello CNAME è corretto, viene convalidato il dominio personalizzato.  Per **rete CDN di Azure da Verizon** endpoint (Standard e Premium), potrebbe richiedere fino too90 minuti per dominio personalizzato toopropagate tooall CDN edge nodi di impostazioni, tuttavia.  
   
   Si noti che in alcuni casi, possono richiedere tempo per i server di tooname toopropagate record CNAME hello in hello Internet. Se il dominio non viene convalidato immediatamente e si ritiene hello record CNAME sia corretto, attendere qualche minuto e riprovare.

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-hello-intermediary-cdnverify-subdomain"></a>Registrare un dominio personalizzato per un endpoint rete CDN di Azure utilizzando hello sottodominio cdnverify di Azure
1. Accedere al hello [portale Azure](https://portal.azure.com/).
2. Fare clic su **Sfoglia**, quindi **CDN profili**, quindi hello profilo CDN con endpoint hello desiderato toomap tooa personalizzato dominio.  
3. In hello **profilo CDN** pannello, fare clic sull'endpoint rete CDN hello con cui si desidera sottodominio hello tooassociate.
4. Nella parte superiore di hello del pannello endpoint hello, fare clic su hello **Aggiungi dominio personalizzato** pulsante.  In hello **aggiungere un dominio personalizzato** pannello, si noterà hello endpoint nome host, derivato dall'endpoint della rete CDN, toouse nella creazione di un nuovo record CNAME. Hello formato dell'indirizzo di nome host hello verrà visualizzato come  **&lt;EndpointName >. azureedge.net**.  È possibile copiare questo toouse nome host per la creazione di record CNAME hello.
5. Sito web del registrar di dominio tooyour passare e individuare la sezione hello per la creazione di record DNS. Queste informazioni possono essere disponibili in una sezione come **Domain Name**, **DNS** o **Name Server Management**.
6. Trovare la sezione hello per la gestione dei record CNAME. È possibile avere una pagina di impostazioni avanzate tooan toogo e cercare parole hello **CNAME**, **Alias**, o **sottodomini**.
7. Creare un nuovo record CNAME e fornire un alias di sottodominio che include hello **cdnverify** sottodominio. Ad esempio, sarà sottodominio hello specificato nel formato hello **cdnverify.www** o **cdnverify.cdn**. Quindi specificare il nome host hello, che è l'endpoint CDN, nel formato hello **cdnverify.&lt; EndpointName >. azureedge.net**. Il mapping DNS dovrebbe avere un aspetto simile a: `cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. Restituire toohello **aggiungere un dominio personalizzato** pannello e immettere il dominio personalizzato, inclusi il sottodominio hello, nella finestra di dialogo hello. Ad esempio, immettere il nome di dominio hello in formato hello `www.contoso.com` o `cdn.contoso.com`. Si noti che in questo passaggio non è necessario il sottodominio hello toopreface con **cdnverify**.  
   
    Azure è necessario verificare che i record CNAME hello esista hello cdnverify nome di dominio immesso.
9. A questo punto, il dominio personalizzato è stato verificato da Azure, ma il dominio tooyour traffico non viene ancora endpoint rete CDN tooyour indirizzato. Dopo aver atteso abbastanza a lungo toopropagate le impostazioni di tooallow hello dominio personalizzato CDN toohello bordo nodi (90 minuti per **rete CDN di Azure da Verizon**, 1-2 minuti per **rete CDN di Azure da Akamai**), restituiscono tooyour DNS sito web del Registrar e creare un altro record CNAME che esegue il mapping dell'endpoint CDN tooyour di sottodominio. Ad esempio, specificare il sottodominio hello come **www** o **cdn**, e nome host come hello  **&lt;EndpointName >. azureedge.net**. Con questo passaggio è stata completata la registrazione di hello del dominio personalizzato.
10. Infine, è possibile eliminare i record CNAME hello è stato creato mediante **cdnverify**, poiché è stato necessario solo come passaggio intermedio.  

## <a name="verify-that-hello-custom-subdomain-references-your-cdn-endpoint"></a>Verificare che il sottodominio personalizzato hello fa riferimento a endpoint della rete CDN
* Dopo aver completato la registrazione di hello del dominio personalizzato, è possibile accedere a contenuto memorizzato nella cache all'endpoint della rete CDN utilizzando hello di dominio personalizzato.
  Innanzitutto, assicurarsi di disporre i contenuti pubblici che vengano memorizzato nella cache hello endpoint. Ad esempio, se l'endpoint CDN è associato a un account di archiviazione, hello rete CDN memorizza nella cache il contenuto nei contenitori blob pubblici. dominio personalizzato hello tootest, assicurarsi che il contenitore sia impostato l'accesso pubblico tooallow e che sia presente almeno un blob.
* Nel browser, passare l'indirizzo toohello del blob hello utilizzando hello di dominio personalizzato. Ad esempio, se il dominio personalizzato è `cdn.contoso.com`, blob memorizzato nella cache di hello URL tooa saranno simile toohello seguente URL: http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>Vedere anche
[Come tooEnable hello rete CDN (Content Delivery) per Azure](cdn-create-new-endpoint.md)  

