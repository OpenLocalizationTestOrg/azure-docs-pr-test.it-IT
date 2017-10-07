---
title: BLOB di tooaccess aaaUsing hello rete CDN di Azure con i domini personalizzati tramite HTTPS
description: Informazioni su come BLOB toointegrate hello rete CDN di Azure con tooaccess di archiviazione blob con i domini personalizzati tramite HTTPS
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: f6cee36ca5495983545f2f6a8ff140677cf6914b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cdn-tooaccess-blobs-with-custom-domains-over-https"></a>Tramite i BLOB in tooaccess hello rete CDN di Azure con i domini personalizzati tramite HTTPS

La rete per la distribuzione di contenuti (rete CDN) di Azure supporta ora HTTPS per i nomi di dominio personalizzati.
È possibile sfruttare i BLOB di archiviazione tooaccess questa funzionalità utilizzando il dominio personalizzato tramite HTTPS. toodo in tal caso, è necessario innanzitutto tooenable rete CDN di Azure nel blob endpoint e mappa hello CDN tooa nome di dominio personalizzato. Una volta è eseguire questi passaggi, abilitazione di HTTPS per il dominio personalizzato è semplificata tramite un solo clic abilitazione, la gestione dei certificati completato e tutti i dati con nessun prezzi di costi aggiuntivi toonormal rete CDN.

Questa possibilità è importante perché consente si tooprotect hello riservatezza e integrità dei dati dell'applicazione web riservati in transito. Utilizzando hello SSL protocollo tooserve il traffico tramite HTTPS garantisce che i dati vengono crittografati quando vengono inviate in hello internet. HTTPS garantisce attendibilità e autenticazione e protegge le applicazioni Web dagli attacchi.

> [!NOTE]
> Inoltre tooproviding supporta SSL per i nomi di dominio personalizzato, hello rete CDN di Azure consente di ridimensionare il contenuto dell'applicazione toodeliver larghezza di banda elevata tutto il mondo hello.
> toolearn, estrarre [panoramica delle rete CDN di Azure hello](../../cdn/cdn-overview.md).
>
>

## <a name="quick-start"></a>Avvio rapido

Si tratta di hello passaggi necessari tooenable HTTPS per l'endpoint di archiviazione blob personalizzato:

1.  [Integrare un account di archiviazione di Azure con la rete CDN di Azure](../../cdn/cdn-create-a-storage-account-with-cdn.md).
    In questo articolo illustra la creazione di un account di archiviazione nel portale di Azure hello se non è già.
2.  [Dominio personalizzato di mappa della rete CDN Azure tooa contenuto](../../cdn/cdn-map-content-to-custom-domain.md).
3.  [Abilitare HTTPS in un dominio personalizzato della rete CDN di Azure](../../cdn/cdn-custom-ssl.md).

## <a name="shared-access-signatures"></a>Firme di accesso condiviso

Se l'endpoint di archiviazione blob è toodisallow configurato l'accesso in lettura anonimo, sarà necessario tooprovide un [firma di accesso condiviso (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) in ogni richiesta di token è rendere tooyour di dominio personalizzato. Per impostazione predefinita, gli endpoint di archiviazione BLOB non consentono l'accesso anonimo in lettura. Per altre informazioni sulle firme di accesso condiviso, vedere [Gestire l'accesso anonimo in lettura a contenitori e BLOB](storage-manage-access-to-resources.md).

Rete CDN di Azure non rispetta un token di firma di accesso condiviso restrizioni toohello aggiunto. Ad esempio, tutti i token di firma di accesso condiviso hanno una data di scadenza. Ciò significa che il contenuto può comunque accedere con una firma di accesso condiviso scaduta fino a quando tale contenuto viene eliminato dalla nodi periferici CDN di hello. È possibile controllare quanto tempo vengono memorizzati i dati nella rete CDN hello dall'impostazione di intestazione di risposta della cache hello. Per istruzioni, vedere [Gestire la scadenza dei BLOB di archiviazione di Azure nella rete CDN di Azure](../../cdn/cdn-manage-expiration-of-blob-content.md).

Se si creano più URL di firma di accesso condiviso per hello stesso endpoint blob, è consigliabile attivare la memorizzazione nella cache stringa query per la rete CDN di Azure. Si tratta di tooensure che ogni URL viene considerato come un'entità univoca. Per altre informazioni, vedere [Controllare il comportamento di memorizzazione nella cache della rete CDN di Azure con stringhe di query](../../cdn/cdn-query-string.md).

## <a name="http-toohttps-redirection"></a>Reindirizzamento tooHTTPS HTTP

È possibile scegliere tooredirect HTTP traffico tooHTTPS. Questo richiede l'utilizzo dell'offerta premium di Azure CDN hello da Verizon. È necessario troppo[il comportamento di Override HTTP utilizzando il motore regole di rete CDN di Azure](../../cdn/cdn-rules-engine.md) con la seguente regola:

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

"Nome dell'endpoint rete Cdn" si riferisce toohello nome configurato per l'endpoint CDN. È possibile selezionare questo valore dall'elenco a discesa hello. "Percorso di origine" fa riferimento al percorso di hello all'interno dell'account di archiviazione di origine in cui risiede il contenuto statico.
Se si ospitano tutto il contenuto statico in un singolo contenitore, sostituire "percorso di origine" con il nome di hello del contenitore.

Per un approfondimento nelle regole, vedere hello [le funzionalità del motore regole di rete CDN di Azure](../../cdn/cdn-rules-engine-reference-features.md).

## <a name="pricing-and-billing"></a>Prezzi e fatturazione

Quando si accede BLOB tramite una rete CDN di Azure, si paga [prezzi di archiviazione Blob](https://azure.microsoft.com/pricing/details/storage/blobs/) per il traffico tra i nodi di edge hello e origine hello (archiviazione Blob), e [prezzi CDN](https://azure.microsoft.com/pricing/details/cdn/) per i dati dal nodi periferici hello.

Si supponga, ad esempio, un account di archiviazione negli Stati Uniti occidentali cui si accede con una rete CDN di Azure. Se un utente di hello Regno Unito tenta tooaccess uno di hello BLOB nell'account di archiviazione tramite hello CDN, Azure controlla innanzitutto un nodo del bordo hello più vicino a messaggi hello UK per tale blob. Se viene trovato, accede tale copia di blob hello e utilizzerà CDN sui prezzi, perché sono connessi in rete CDN hello. Se non viene trovato, Azure copierà hello blob toohello bordo nodo, determinando in uscita e i costi di transazione come specificato in hello Blob prezzi di archiviazione e quindi accedere ai file hello nel nodo di edge hello, che comporterà la fatturazione della rete CDN.

Quando si esaminano hello [CDN pagina dei prezzi](https://azure.microsoft.com/pricing/details/cdn/), si noti che il supporto di HTTPS per i nomi di dominio personalizzato sono disponibili solo per la rete CDN di Azure da Verizon prodotti (Standard e Premium).

## <a name="next-steps"></a>Passaggi successivi

[Configurare un nome di dominio completo per l'endpoint di archiviazione BLOB](storage-custom-domain-name.md)
