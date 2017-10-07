---
title: aaaManage DNS zone DNS di Azure - portale di Azure | Documenti Microsoft
description: "È possibile gestire le zone DNS utilizzando hello portale di Azure. In questo articolo viene descritto come tooupdate, eliminare e creare le zone DNS in DNS di Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>Come le zone DNS toomanage nella hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-operations-dnszones-cli.md)

Questo articolo illustra come toomanage zone DNS utilizzando hello portale di Azure. È inoltre possibile gestire le zone DNS utilizzando hello multipiattaforma [CLI di Azure](dns-operations-dnszones-cli.md) o hello Azure [PowerShell](dns-operations-dnszones.md).

## <a name="create-a-dns-zone"></a>Creare una zona DNS

1. Accedi toohello portale di Azure
2. Nel menu Hub hello, fare clic su e fare clic su **nuovo > rete >** e quindi fare clic su **zona DNS** blade di zona DNS creare hello tooopen.

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. In hello **zona DNS creare** pannello immettere i seguenti valori hello, quindi fare clic su **crea**:


   | **Impostazione** | **Valore** | **Dettagli** |
   |---|---|---|
   |**Nome**|contoso.com|nome Hello della zona DNS hello|
   |**Sottoscrizione**|[Sottoscrizione]|Selezionare una zona DNS di sottoscrizione toocreate hello in.|
   |**Gruppo di risorse**|**Crea nuovo:** contosoDNSRG|Creare un gruppo di risorse. nome del gruppo di risorse Hello deve essere univoco all'interno di sottoscrizione hello selezionata. ulteriori informazioni sui gruppi di risorse, leggere hello toolearn [Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) articolo introduttivo.|
   |**Posizione**|Stati Uniti occidentali||

> [!NOTE]
> gruppo di risorse Hello fa riferimento il percorso toohello hello del gruppo di risorse e non influisce sulla zona DNS hello. percorso di zona DNS Hello sono sempre "globale" e non viene visualizzato.

## <a name="list-dns-zones"></a>Elencare le zone DNS

Nel portale di Azure hello, passare troppo**più servizi** > **rete** > **zone DNS**. Ogni zona DNS è una risorsa a sé e in questa vista sono disponibili informazioni quali il numero di set di record e i server dei nomi. colonna Hello **server dei nomi** non è nella visualizzazione predefinita di hello, tooadd fare clic su **colonne**selezionare **server dei nomi** e fare clic su **eseguita**.

![elenco delle zone DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>Eliminare una zona DNS

Passare una zona DNS tooa nel portale di hello. In hello **zona DNS** pannello, fare clic su **Elimina zona**. Si è tooconfirm richiesta che si occupano di zona DNS di hello toodelete. L'eliminazione di una zona DNS elimina inoltre tutti i record contenuti nella zona hello hello.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come toowork con la zona DNS e i record visitando [introduzione DNS di Azure tramite il portale di Azure hello](dns-getstarted-portal.md).
