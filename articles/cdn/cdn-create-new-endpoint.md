---
title: aaaGetting avviato con una rete CDN di Azure | Documenti Microsoft
description: Questo argomento viene illustrato come tooenable hello Azure rete CDN (Content Delivery). esercitazione Hello tramite la creazione di hello di un nuovo profilo di rete CDN e l'endpoint.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a>Introduzione alla rete CDN di Azure
Questo argomento descrive in dettaglio l'abilitazione della rete CDN di Azure creando un nuovo profilo di rete CDN e un endpoint.

> [!IMPORTANT]
> Per un funzionamento della rete CDN di introduzione toohow, nonché un elenco delle funzionalità, vedere hello [Panoramica della rete CDN](cdn-overview.md).
> 
> 

## <a name="create-a-new-cdn-profile"></a>Creare un nuovo profilo di rete CDN
Un profilo di rete CDN è una raccolta di endpoint della rete CDN.  Ogni profilo contiene uno o più endpoint della rete CDN.  È preferibile toouse più profili tooorganize gli endpoint CDN dal dominio internet, l'applicazione web o ad altri criteri.

> [!NOTE]
> Per impostazione predefinita, una singola sottoscrizione di Azure è limitato tooeight i profili di rete CDN. Ogni profilo CDN è l'endpoint rete CDN tooten limitato.
> 
> Rete CDN prezzi viene applicato a livello di profilo rete CDN di hello. Se si desidera toouse una combinazione di rete CDN di Azure i livelli di prezzo, è necessario più profili di rete CDN.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Creare un nuovo endpoint della rete CDN
**toocreate un nuovo endpoint CDN**

1. In hello [portale Azure](https://portal.azure.com), passare il profilo CDN tooyour.  Si potrebbe avere aggiunto toohello dashboard nel passaggio precedente hello.  Se è, non sarà possibile trovarlo facendo **Sfoglia**, quindi **i profili di rete CDN**, e fare clic sul profilo hello prevede tooadd l'endpoint.
   
    verrà visualizzata la finestra di blade profilo rete CDN di Hello.
   
    ![Profilo di rete CDN][cdn-profile-settings]
2. Fare clic su hello **Aggiungi Endpoint** pulsante.
   
    ![Pulsante Aggiungi endpoint][cdn-new-endpoint-button]
   
    Hello **aggiungere un endpoint** pannello viene visualizzato.
   
    ![Pannello Aggiungi endpoint][cdn-add-endpoint]
3. Immettere un **Nome** per questo endpoint della rete CDN.  Questo nome verrà usato tooaccess le risorse memorizzate nella cache nel dominio hello `<endpointname>.azureedge.net`.
4. In hello **tipo di origine** elenco a discesa selezionare il tipo di origine.  Selezionare **Archiviazione** per un account di archiviazione di Azure, **Servizio Cloud** per un servizio cloud di Azure, **App Web** per un'app Web di Azure oppure **Origine personalizzata** per qualsiasi altra origine di server Web accessibile pubblicamente, ospitata in Azure o altrove.
   
    ![Tipo di origine della rete CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. In hello **nome host dell'origine** elenco a discesa, selezionare o digitare il dominio di origine.  elenco a discesa Hello elencherà tutte le origini disponibili del tipo di hello che è specificato nel passaggio 4.  Se si seleziona *origine personalizzata* come il **tipo di origine**, digitato nel dominio hello dell'origine personalizzata.
6. In hello **il percorso di origine** testo immettere hello percorso toohello risorse desiderate toocache o lasciare vuoto tooallow cache qualsiasi risorsa dominio hello specificato nel passaggio 5.
7. In hello **intestazione host di origine**, intestazione host hello desiderato hello CDN toosend con ogni richiesta di immettere o lasciare hello predefinito.
   
   > [!WARNING]
   > Alcuni tipi di origini, ad esempio l'archiviazione di Azure e le applicazioni Web, richiedono hello intestazione toomatch hello dominio di origine hello. A meno che non si dispone di un'origine che richiede un'intestazione host diversa dal relativo dominio, è consigliabile lasciare il valore di predefinito hello.
   > 
   > 
8. Per **protocollo** e **porta di origine**, specificare hello protocolli e porte tooaccess usate le risorse di origine hello.  È necessario selezionare almeno un protocollo (HTTP o HTTPS).
   
   > [!NOTE]
   > Hello **porta di origine** influisce solo sulle quali endpoint hello porta utilizza le informazioni tooretrieve origine hello.  Hello endpoint stesso sarà solo client tooend disponibili su hello predefinito porte HTTP e HTTPS (80 e 443), indipendentemente dal hello **porta di origine**.  
   > 
   > **Rete CDN di Azure da Akamai** endpoint non consentano hello completo TCP intervallo di porte per le origini.  Per un elenco delle porte di origine non consentite, vedere l'articolo relativo ai [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Porte di origine consentite in Rete CDN di Azure da Akamai).  
   > 
   > Accesso rete CDN il contenuto usando HTTPS ha hello seguenti vincoli:
   > 
   > * È necessario utilizzare il certificato SSL hello fornito da hello CDN. I certificati di terze parti non sono supportati.
   > * È necessario utilizzare il dominio di condizione della rete CDN hello (`<endpointname>.azureedge.net`) contenuto HTTPS tooaccess. Il supporto HTTPS non è disponibile per i nomi di dominio personalizzato (CNAME) poiché hello CDN non supporta i certificati personalizzati in questo momento.
   > 
   > 
9. Fare clic su hello **Aggiungi** toocreate pulsante hello nuovo endpoint.
10. Dopo aver creato endpoint hello, viene visualizzato in un elenco di endpoint per il profilo hello. visualizzazione elenco Hello Mostra hello URL toouse tooaccess memorizzati nella cache il contenuto, nonché il dominio di origine hello.
    
    ![Endpoint della rete CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > endpoint di Hello non immediatamente saranno disponibili per l'utilizzo, come il tempo per hello registrazione toopropagate tramite hello CDN.  Per <b>Rete CDN di Azure da Akamai</b> la propagazione in genere viene completata entro un minuto.  Per i profili della <b>rete CDN di Azure fornita da Verizon</b>, la propagazione in genere viene completata entro 90 minuti, ma in alcuni casi può richiedere più tempo.
    > 
    > Gli utenti che tentano di nome di dominio della rete CDN hello toouse prima configurazione di endpoint hello è propagata POP toohello riceverà i codici di risposta HTTP 404.  Se sono trascorse diverse ore da quando è stato creato l'endpoint e si ricevono ancora risposte 404, vedere l'articolo relativo alla [risoluzione dei problemi degli endpoint della rete CDN che restituiscono stati 404](cdn-troubleshoot-endpoint.md).
    > 
    > 

## <a name="see-also"></a>Vedere anche
* [Controllo del comportamento di memorizzazione nella cache delle richieste della rete CDN con le stringhe di query](cdn-query-string.md)
* [Come tooMap CDN contenuto tooa dominio personalizzato](cdn-map-content-to-custom-domain.md)
* [Precaricamento di risorse in un endpoint della rete CDN di Azure](cdn-preload-endpoint.md)
* [Ripulire un endpoint della rete CDN di Azure](cdn-purge-endpoint.md)
* [Risoluzione dei problemi degli endpoint della rete CDN che restituiscono stati 404](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
