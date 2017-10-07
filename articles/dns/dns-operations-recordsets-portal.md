---
title: aaaManage DNS record set e i record con DNS di Azure | Documenti Microsoft
description: "DNS di Azure fornisce i record DNS di hello funzionalità toomanage imposta e registra quando si ospita il dominio."
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
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a>Gestire i record DNS e set di record mediante hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](dns-operations-recordsets-portal.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Questo articolo illustra come set di record toomanage e i record per la zona DNS mediante hello portale di Azure.

È importante toounderstand hello differenza set di record DNS e singoli record DNS. Un set di record è una raccolta di record in una zona con hello stesso nome e sono hello stesso tipo. Per ulteriori informazioni, vedere [set di record DNS di creare e i record utilizzando hello Azure portal](dns-getstarted-create-recordset-portal.md).

## <a name="create-a-new-record-set-and-record"></a>Creare un nuovo set di record e record

toocreate un set di record in hello portale di Azure, vedere [i record DNS creare utilizzando hello Azure portal](dns-getstarted-create-recordset-portal.md).

## <a name="view-a-record-set"></a>Visualizzare un set di record

1. Nel portale di Azure hello, passare toohello **zona DNS** blade.
2. Ricerca per i set di record hello e selezionarlo. Consente di aprire le proprietà del set di record di hello.

    ![Ricerca di un set di record](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a>Aggiungere un nuovo set di record tooa record

È possibile aggiungere i set di record tooany too20 record. Un set di record non può contenere due record identici. Set di record vuoto (con zero record) possono essere creati, ma non vengono visualizzati in server dei nomi DNS di Azure hello. I set di record di tipo CNAME possono contenere al massimo un record.

1. In hello **proprietà set di Record** pannello per la zona DNS, fare clic su record hello impostata che si desidera tooadd un record.

    ![Selezionare un set di record](./media/dns-operations-recordsets-portal/selectset500.png)

2. Specificare le proprietà del set di record hello compilando hello campi.

    ![Aggiungere un record](./media/dns-operations-recordsets-portal/addrecord500.png)

3. Fare clic su **salvare** in hello cima hello pannello toosave le impostazioni. Quindi, chiudere il pannello hello.
4. Nell'angolo hello, si noterà che i record di hello sta salvando.

    ![Salvataggio del set di record](./media/dns-operations-recordsets-portal/saving150.png)

Dopo che è stato salvato il record di hello, hello valori hello **zona DNS** pannello rifletterà il nuovo record di hello.

## <a name="update-a-record"></a>Aggiornare un record

Quando si aggiorna un record in un set di record esistente, è possibile aggiornare i campi di hello dipendono dal tipo di hello del record in uso.

1. In hello **proprietà set di Record** pannello per il set di record, cercare il record di hello.
2. Modificare il record di hello. Quando si modifica un record, è possibile modificare le impostazioni disponibili hello per record hello. Nell'esempio seguente di hello, hello **indirizzo IP** campo sia selezionato e l'indirizzo IP hello è in corso di hello della fase di modifica.

    ![Modificare un record](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. Fare clic su **salvare** in hello cima hello pannello toosave le impostazioni. In hello angolo superiore destro, si noterà notifica hello che hello record è stato salvato.

    ![Set di record salvato](./media/dns-operations-recordsets-portal/saved150.png)

Dopo hello record è stato salvato, i valori hello hello record impostare sulla hello **zona DNS** pannello rifletterà record hello aggiornato.

## <a name="remove-a-record-from-a-record-set"></a>Rimuovere un record da un set di record

È possibile utilizzare i record di hello Azure tooremove portale da un set di record. Si noti che rimozione dell'ultimo record hello un set di record non comporta l'eliminazione del set di record hello.

1. In hello **proprietà set di Record** pannello per il set di record, cercare il record di hello.
2. Fare clic su record hello che si desidera tooremove. Selezionare **Rimuovi**.

    ![Rimuovere un record](./media/dns-operations-recordsets-portal/removerecord500.png)

3. Fare clic su **salvare** in hello cima hello pannello toosave le impostazioni.
4. Dopo aver rimosso il record di hello, hello valori hello record su hello **zona DNS** pannello rifletterà la rimozione di hello.

## <a name="delete"></a>Eliminare un set di record

1. In hello **proprietà set di Record** pannello per il set di record, fare clic su **eliminare**.

    ![Eliminare un set di record](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. Viene visualizzato un messaggio che chiede se si desidera toodelete hello record set.
3. Verificare che hello Nome corrispondenze hello record impostata che desidera toodelete e quindi fare clic su **Sì**.
4. In hello **zona DNS** pannello, verificare che i set di record hello non è più visibili.

## <a name="work-with-ns-and-soa-records"></a>Usare record NS e SOA

I record NS e SOA creati automaticamente vengono gestiti in modo diverso rispetto ad altri tipi di record.

### <a name="modify-soa-records"></a>Modificare i record SOA

È possibile aggiungere o rimuovere i record da hello automaticamente creato un record SOA impostato al vertice zona hello (nome = "@"). Tuttavia, è possibile modificare i parametri di hello all'interno di hello record SOA (ad eccezione di "Host") e impostare il valore TTL record hello.

### <a name="modify-ns-records-at-hello-zone-apex"></a>Modificare i record NS al vertice zona hello

record NS Hello impostato al vertice zona hello viene creato automaticamente con ogni zona DNS. Contiene i nomi hello della zona di hello DNS di Azure nome server toohello assegnato.

È possibile aggiungere nomi aggiuntivi server toothis NS set di record, toosupport CO-ospitano i domini con più di un provider DNS. È inoltre possibile modificare hello durata (TTL) e i metadati per questo set di record. Tuttavia, è Impossibile rimuovere o modificare server dei nomi DNS di Azure prepopolato hello.

Si noti che questo si applica solo toohello NS set di record al vertice zona hello. Altri set di record NS nella zona (come le aree figlio toodelegate usato) possono essere modificati senza vincoli.

### <a name="delete-soa-or-ns-record-sets"></a>Eliminare set di record SOA o NS

Non è possibile eliminare hello SOA e NS set di record al vertice zona hello (nome = "@") che vengono creati automaticamente quando si crea la zona hello. Vengono eliminate automaticamente quando si elimina la zona hello.

## <a name="next-steps"></a>Passaggi successivi

* Per ulteriori informazioni su DNS di Azure, vedere hello [Panoramica di DNS di Azure](dns-overview.md).
* Per ulteriori informazioni su come automatizzare DNS, vedere [le zone DNS di creazione e set di record mediante .NET SDK di hello](dns-sdk.md).
* Per altre informazioni sui record DNS inversi, vedere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md).
