---
title: aaaGet avviato con il DNS di Azure utilizzando hello portale di Azure | Documenti Microsoft
description: "Informazioni su come toocreate un DNS zona e questo record in DNS di Azure. Questo è un toocreate Guida dettagliata e gestire la prima zona DNS e il record utilizzando hello portale di Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a>Introduzione a DNS di Azure utilizzando hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-getstarted-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-getstarted-cli.md)

In questo articolo illustra hello passaggi toocreate prima zona DNS il record utilizzando hello portale di Azure. È anche possibile eseguire questi passaggi con Azure PowerShell o hello multipiattaforma CLI di Azure.

Una zona DNS è utilizzato toohost hello DNS record per un particolare dominio. toostart hosting del dominio DNS di Azure, è necessario toocreate una zona DNS per il nome di dominio. Ogni record DNS per il dominio viene quindi creato all'interno di questa zona DNS. Infine, toopublish della zona DNS toohello Internet, server dei nomi tooconfigure hello è necessario per il dominio hello. Ognuno di questi passaggi viene descritto in hello alla procedura seguente.

## <a name="create-a-dns-zone"></a>Creare una zona DNS

1. Accedi toohello portale di Azure
2. Nel menu Hub hello, fare clic su e fare clic su **nuovo > rete >** e quindi fare clic su **zona DNS** blade di zona DNS creare hello tooopen.

    ![Zona DNS](./media/dns-getstarted-portal/openzone650.png)

4. In hello **zona DNS creare** pannello immettere i seguenti valori hello, quindi fare clic su **crea**:


   | **Impostazione** | **Valore** | **Dettagli** |
   |---|---|---|
   |**Nome**|contoso.com|nome Hello della zona DNS hello|
   |**Sottoscrizione**|[Sottoscrizione]|Selezionare una zona DNS di sottoscrizione toocreate hello in.|
   |**Gruppo di risorse**|**Crea nuovo:** contosoDNSRG|Creare un gruppo di risorse. nome del gruppo di risorse Hello deve essere univoco all'interno di sottoscrizione hello selezionata. ulteriori informazioni sui gruppi di risorse, leggere hello toolearn [Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) articolo introduttivo.|
   |**Posizione**|Stati Uniti occidentali||

> [!NOTE]
> gruppo di risorse Hello fa riferimento il percorso toohello hello del gruppo di risorse e non influisce sulla zona DNS hello. percorso di zona DNS Hello sono sempre "globale" e non viene visualizzato.

## <a name="create-a-dns-record"></a>Creare un record DNS

Hello seguente esempio illustra hello processo di creazione di nuovi record "A". Per altri tipi di record e i record esistenti toomodify, vedere [record DNS di gestire e set di record mediante il portale di Azure di hello](dns-operations-recordsets-portal.md). 

1. Con hello zona DNS creato, nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**. Fare clic su hello **contoso.com** della zona DNS in hello tutti pannello risorse. Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere **contoso.com** in hello **filtrare in base al nome...** casella tooeasily accedere hello zona di DNS.

1. Nella parte superiore di hello di hello **zona DNS** pannello seleziona **+ registrare set** tooopen hello **aggiungere set di record** blade.

1. In hello **aggiungere set di record** pannello, immettere i seguenti valori hello e fare clic su **OK**. In questo esempio viene creato un record A.

   |**Impostazione** | **Valore** | **Dettagli** |
   |---|---|---|
   |**Nome**|www|Nome del record di hello|
   |**Tipo**|Una | Tipo di toocreate record DNS, i valori accettabili sono A, AAAA, CNAME, MX, NS, SRV, TXT e PTR.  Per altre informazioni sui tipi di record, vedere [Panoramica delle zone e dei record DNS](dns-zones-records.md)|
   |**TTL**|1|Time-to-live della richiesta DNS hello.|
   |**Unità TTL**|Ore|Misura di tempo per il valore TTL.|
   |**Indirizzo IP**|ipAddressValue| Questo valore è l'indirizzo IP hello che risolve i record DNS hello.|

## <a name="view-records"></a>Visualizzare i record

Nella parte inferiore di hello del Pannello di zona DNS hello, è possibile visualizzare i record per la zona DNS hello hello. Verranno visualizzati i record DNS e SOA predefinito di hello, che vengono creati in ogni area, oltre a qualsiasi nuovo record che è stato creato.

![zona](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a>Aggiornare i server dei nomi

Dopo aver soddisfatto che la zona DNS e i record sono stati impostati correttamente, è necessario tooconfigure il nome di dominio toouse server dei nomi DNS di Azure hello. In questo modo altri utenti nel hello Internet toofind i record DNS.

Server dei nomi per l'area Hello sono indicati nella hello portale di Azure:

![zona](./media/dns-getstarted-portal/viewzonens500.png)

Questi server dei nomi deve essere configurato con hello registrar (in cui è stato acquistato il nome di dominio hello). Registrar offre hello opzione tooset dei server dei nomi per il dominio hello hello. Per ulteriori informazioni, vedere [delegare il tooAzure di dominio DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Eliminare tutte le risorse

toodelete tutte le risorse create in questo articolo, hello completo alla procedura seguente:

1. Nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**. Fare clic su hello **MyResourceGroup** gruppo di risorse in hello tutti pannello risorse. Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere **MyResourceGroup** in hello **filtrare in base al nome...** gruppo di risorse hello accesso tooeasily casella.
1. In hello **MyResourceGroup** pannello, fare clic su hello **eliminare** pulsante.
1. Hello portale richiede nome hello tootype di hello tooconfirm di gruppo di risorse che si desidera toodelete è. Fare clic su **eliminare**, tipo *MyResourceGroup* per nome gruppo di risorse hello, quindi fare clic su **eliminare**. Elimina un gruppo di risorse, tutte le risorse nel gruppo di risorse hello, pertanto sempre certi tooconfirm contenuto hello di un gruppo di risorse prima di eliminarlo. portale Hello Elimina tutte le risorse contenute nel gruppo di risorse hello, quindi Elimina gruppo di risorse hello stesso. Questo processo richiede alcuni minuti.


## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni su DNS di Azure, vedere [Panoramica di DNS di Azure](dns-overview.md).

toolearn informazioni su gestione dei record DNS nel sistema DNS di Azure, vedere [record DNS di gestire e set di record mediante il portale di Azure di hello](dns-operations-recordsets-portal.md).

