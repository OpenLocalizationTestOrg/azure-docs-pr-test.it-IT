---
title: Gestire set di record e record DNS con DNS di Azure | Documentazione Microsoft
description: DNS di Azure consente di gestire i set di record DNS in caso di hosting del dominio.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 001b80ccba43beab44f6a598f820df65a85a345f
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-the-azure-portal"></a>Gestire record e set di record DNS con il portale di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](dns-operations-recordsets-portal.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Questo articolo descrive come gestire i set di record e i record per la zona DNS usando il portale di Azure.

È importante comprendere la differenza tra i set di record DNS e i singoli record DNS. Un set di record è una raccolta di record con lo stesso nome e lo stesso tipo in una zona. Per altre informazioni vedere [Creare set di record e record DNS mediante il portale di Azure](dns-getstarted-create-recordset-portal.md).

## <a name="create-a-new-record-set-and-record"></a>Creare un nuovo set di record e record

Per creare un set di record nel portale di Azure, vedere [Creare record e set di record DNS mediante il portale di Azure](dns-getstarted-create-recordset-portal.md).

## <a name="view-a-record-set"></a>Visualizzare un set di record

1. Nel portale di Azure passare al pannello **Zona DNS** .
2. Cercare e selezionare il set di record. Vengono aperte le proprietà del set di record.

    ![Ricerca di un set di record](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-to-a-record-set"></a>Aggiungere un nuovo record a un set di record

È possibile aggiungere fino a 20 record a qualsiasi set di record. Un set di record non può contenere due record identici. È possibile creare set di record vuoti, con zero record, che non vengono però visualizzati nei server dei nomi DNS di Azure. I set di record di tipo CNAME possono contenere al massimo un record.

1. Dal pannello **Proprietà del set di record** per la zona DNS, fare clic sul set di record al quale aggiungere un record.

    ![Selezionare un set di record](./media/dns-operations-recordsets-portal/selectset500.png)

2. Specificare le proprietà del record compilando i campi.

    ![Aggiungere un record](./media/dns-operations-recordsets-portal/addrecord500.png)

3. Fare clic su **Salva** nella parte superiore del pannello per salvare le impostazioni. Chiudere il pannello.
4. Nell'angolo viene visualizzato il processo di salvataggio del record.

    ![Salvataggio del set di record](./media/dns-operations-recordsets-portal/saving150.png)

Dopo aver salvato il record, i valori nel pannello **Zona DNS** rifletteranno il nuovo record.

## <a name="update-a-record"></a>Aggiornare un record

Quando si aggiorna un record in un set di record esistente, i campi che è possibile aggiornare dipendono dal tipo di record in uso.

1. Cercare il record nel pannello **Proprietà del set di record** per il set di record.
2. Modificare il record. Quando si modifica un record, è possibile cambiare le impostazioni disponibili per il record. Nell'esempio seguente è stato fatto clic sul campo **Indirizzo IP** , quindi l'indirizzo IP viene modificato.

    ![Modificare un record](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. Fare clic su **Salva** nella parte superiore del pannello per salvare le impostazioni. Nell'angolo superiore destro viene visualizzata la notifica che indica che il record è stato salvato.

    ![Set di record salvato](./media/dns-operations-recordsets-portal/saved150.png)

Dopo aver salvato il record, i valori per il set di record nel pannello **Zona DNS** rifletteranno il record aggiornato.

## <a name="remove-a-record-from-a-record-set"></a>Rimuovere un record da un set di record

È possibile usare il portale di Azure per rimuovere i record da un set di record. Si noti che la rimozione dell'ultimo record da un set di record non elimina il set di record.

1. Cercare il record nel pannello **Proprietà del set di record** per il set di record.
2. Fare clic sul record da rimuovere. Selezionare **Rimuovi**.

    ![Rimuovere un record](./media/dns-operations-recordsets-portal/removerecord500.png)

3. Fare clic su **Salva** nella parte superiore del pannello per salvare le impostazioni.
4. Dopo aver rimosso il record, i valori per il set di record nel pannello **Zona DNS** rifletteranno la rimozione.

## <a name="delete"></a>Eliminare un set di record

1. Fare clic su **Elimina** nel pannello **Proprietà del set di record** per il set di record.

    ![Eliminare un set di record](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. Viene visualizzato un messaggio in cui viene chiesto se eliminare il set di record.
3. Verificare che il nome corrisponda al set di record da eliminare, quindi fare clic su **Sì**.
4. Nel pannello **Zona DNS** è possibile verificare che il set di record non sia più visibile.

## <a name="work-with-ns-and-soa-records"></a>Usare record NS e SOA

I record NS e SOA creati automaticamente vengono gestiti in modo diverso rispetto ad altri tipi di record.

### <a name="modify-soa-records"></a>Modificare i record SOA

Non è possibile aggiungere o rimuovere record dal set di record SOA creato automaticamente al vertice della zona (name = "@"). È tuttavia possibile modificare i parametri all'interno del record SOA, ad eccezione di "Host", e la durata (TTL) del set di record.

### <a name="modify-ns-records-at-the-zone-apex"></a>Modificare i record NS al vertice della zona

Il set di record NS al vertice della zona viene creato automaticamente con ogni zona DNS. Contiene i nomi dei server dei nomi DNS di Azure assegnati alla zona.

È possibile aggiungere ulteriori server dei nomi a questo set di record NS per supportare domini coesistenti con più provider DNS. È anche possibile modificare il valore TTL e i metadati per questo set di record. Tuttavia, non è possibile rimuovere o modificare i server dei nomi DNS di Azure già popolati.

Notare che questo si applica solo al set di record NS al vertice della zona. Gli altri set di record NS nella zona (usati per delegare le zone figlio) possono essere modificati senza vincoli.

### <a name="delete-soa-or-ns-record-sets"></a>Eliminare set di record SOA o NS

Non è possibile eliminare i set di record SOA e NS al vertice della zona (name = "@") che vengono creati automaticamente quando viene creata la zona. Vengono eliminate automaticamente quando si elimina la zona.

## <a name="next-steps"></a>Passaggi successivi

* Per altre informazioni sul servizio DNS di Azure, vedere [Panoramica di DNS di Azure](dns-overview.md).
* Per altre informazioni sull'automazione di DNS, vedere [Creazione di zone e set di record DNS con .NET SDK](dns-sdk.md).
* Per altre informazioni sui record DNS inversi, vedere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md).
