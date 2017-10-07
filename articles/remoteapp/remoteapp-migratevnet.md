---
title: toomigrate aaaHow da una rete virtuale di Azure di tooan RemoteApp VNET | Documenti Microsoft
description: Informazioni su come toomigrate da una rete virtuale di Azure di tooan RemoteApp VNET
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a>Come una raccolta ibrida da una rete virtuale di Azure di tooan RemoteApp VNET toomigrate
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Ottime notizie! È stata abilitata per le raccolte di RemoteApp ibrida toodeploy direttamente in esistente Azure reti virtuali (Vnet) invece di creare reti virtuali RemoteApp specifiche. Ciò consente di sfruttare i vantaggi di hello ultime funzionalità di rete virtuale (ad esempio ExpressRoute) e concedere l'accesso tooother di ibrida raccolte diretta alla rete servizi di Azure e le macchine virtuali distribuite toothat rete virtuale.  È così possibile migliorare le prestazioni e facilitare l'installazione rispetto alle configurazioni tra reti virtuali.

Si supponga di avere già creato una raccolta RemoteApp ibrida denominata *RaccoltaOriginale* con una rete virtuale RemoteApp denominata *ReteVirtualeRemoteApp*. Di seguito sono toomigrate passaggi hello è tooa nuova rete virtuale di Azure chiamato *AzureVNET*.

1. In hello **reti** scheda hello [portale di gestione](http://manage.windowsazure.com/), creare una rete virtuale denominata *AzureVNET*tramite hello nello stesso percorso, la configurazione di DNS e lo spazio degli indirizzi (per almeno di hello *AzureVNET* subnet) come è stato utilizzato per *RemoteAppVNET*.
2. Configurare *AzureVNET* tooeither host o dispone di connettività di rete toohello distribuzione di Active Directory che *OriginalCollection* appartenga.
3. In hello **programmi RemoteApp** scheda, creare una nuova raccolta RemoteApp denominata *nuova raccolta*. (Hello utilizzare **Create con una rete virtuale** opzione, non **creazione rapida**.)
4. Configurare *NewCollection* toobe distribuito subnet tooa *AzureVNET*.
5. Configurare *NewCollection* toouse hello stessa immagine e le informazioni di join di dominio come è stato utilizzato per *OriginalCollection*.
6. Dopo alcune ore, *NuovaRaccolta* verrà visualizzata nell'elenco di raccolte con uno stato attivo.

A questo punto, se non è necessario toomigrate le informazioni utente hello originale raccolta toohello nuova raccolta, eseguire successivamente questi passaggi:

1. Eliminare *RaccoltaOriginale*.
2. Eliminare *ReteVirtualeRemoteApp*.

L'operazione è così completata.

In alternativa, se si richiedono informazioni utente toomigrate hello originale raccolta toohello nuova raccolta, eseguire successivamente questi passaggi:

1. Inviare un messaggio di posta elettronica troppo[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) con l'ID sottoscrizione di Azure, hello nome della raccolta originale e hello nome della raccolta di nuovo e chiedere toomigrate le informazioni sull'utente.
2. Entro 2 giorni lavorativi team RemoteApp hello sposterà elenco di accesso utente hello e tutti i documenti dell'utente e impostazioni utente da hello originale raccolta toohello nuova raccolta.
3. Eliminare *RaccoltaOriginale*.
4. Eliminare *ReteVirtualeRemoteApp*.

L'operazione è così completata.

In caso di domande o se è necessaria un'assistenza particolare, inviare un messaggio di posta elettronica a [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

