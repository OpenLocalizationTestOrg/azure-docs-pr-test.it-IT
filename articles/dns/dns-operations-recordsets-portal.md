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
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a><span data-ttu-id="5ebd3-103">Gestire i record DNS e set di record mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5ebd3-103">Manage DNS records and record sets by using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ebd3-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5ebd3-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="5ebd3-105">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="5ebd3-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="5ebd3-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5ebd3-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="5ebd3-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ebd3-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="5ebd3-108">Questo articolo illustra come set di record toomanage e i record per la zona DNS mediante hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-108">This article shows you how toomanage record sets and records for your DNS zone by using hello Azure portal.</span></span>

<span data-ttu-id="5ebd3-109">È importante toounderstand hello differenza set di record DNS e singoli record DNS.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-109">It's important toounderstand hello difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="5ebd3-110">Un set di record è una raccolta di record in una zona con hello stesso nome e sono hello stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-110">A record set is a collection of records in a zone that have hello same name and are hello same type.</span></span> <span data-ttu-id="5ebd3-111">Per ulteriori informazioni, vedere [set di record DNS di creare e i record utilizzando hello Azure portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5ebd3-111">For more information, see [Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="5ebd3-112">Creare un nuovo set di record e record</span><span class="sxs-lookup"><span data-stu-id="5ebd3-112">Create a new record set and record</span></span>

<span data-ttu-id="5ebd3-113">toocreate un set di record in hello portale di Azure, vedere [i record DNS creare utilizzando hello Azure portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5ebd3-113">toocreate a record set in hello Azure portal, see [Create DNS records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="5ebd3-114">Visualizzare un set di record</span><span class="sxs-lookup"><span data-stu-id="5ebd3-114">View a record set</span></span>

1. <span data-ttu-id="5ebd3-115">Nel portale di Azure hello, passare toohello **zona DNS** blade.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-115">In hello Azure portal, go toohello **DNS zone** blade.</span></span>
2. <span data-ttu-id="5ebd3-116">Ricerca per i set di record hello e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-116">Search for hello record set and select it.</span></span> <span data-ttu-id="5ebd3-117">Consente di aprire le proprietà del set di record di hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-117">This opens hello record set properties.</span></span>

    ![Ricerca di un set di record](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a><span data-ttu-id="5ebd3-119">Aggiungere un nuovo set di record tooa record</span><span class="sxs-lookup"><span data-stu-id="5ebd3-119">Add a new record tooa record set</span></span>

<span data-ttu-id="5ebd3-120">È possibile aggiungere i set di record tooany too20 record.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-120">You can add up too20 records tooany record set.</span></span> <span data-ttu-id="5ebd3-121">Un set di record non può contenere due record identici.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="5ebd3-122">Set di record vuoto (con zero record) possono essere creati, ma non vengono visualizzati in server dei nomi DNS di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-122">Empty record sets (with zero records) can be created, but do not appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="5ebd3-123">I set di record di tipo CNAME possono contenere al massimo un record.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="5ebd3-124">In hello **proprietà set di Record** pannello per la zona DNS, fare clic su record hello impostata che si desidera tooadd un record.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-124">On hello **Record set properties** blade for your DNS zone, click hello record set that you want tooadd a record to.</span></span>

    ![Selezionare un set di record](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="5ebd3-126">Specificare le proprietà del set di record hello compilando hello campi.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-126">Specify hello record set properties by filling in hello fields.</span></span>

    ![Aggiungere un record](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="5ebd3-128">Fare clic su **salvare** in hello cima hello pannello toosave le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-128">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="5ebd3-129">Quindi, chiudere il pannello hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-129">Then close hello blade.</span></span>
4. <span data-ttu-id="5ebd3-130">Nell'angolo hello, si noterà che i record di hello sta salvando.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-130">In hello corner, you will see that hello record is saving.</span></span>

    ![Salvataggio del set di record](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="5ebd3-132">Dopo che è stato salvato il record di hello, hello valori hello **zona DNS** pannello rifletterà il nuovo record di hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-132">After hello record has been saved, hello values on hello **DNS zone** blade will reflect hello new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="5ebd3-133">Aggiornare un record</span><span class="sxs-lookup"><span data-stu-id="5ebd3-133">Update a record</span></span>

<span data-ttu-id="5ebd3-134">Quando si aggiorna un record in un set di record esistente, è possibile aggiornare i campi di hello dipendono dal tipo di hello del record in uso.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-134">When you update a record in an existing record set, hello fields you can update depend on hello type of record you're working with.</span></span>

1. <span data-ttu-id="5ebd3-135">In hello **proprietà set di Record** pannello per il set di record, cercare il record di hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-135">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="5ebd3-136">Modificare il record di hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-136">Modify hello record.</span></span> <span data-ttu-id="5ebd3-137">Quando si modifica un record, è possibile modificare le impostazioni disponibili hello per record hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-137">When you modify a record, you can change hello available settings for hello record.</span></span> <span data-ttu-id="5ebd3-138">Nell'esempio seguente di hello, hello **indirizzo IP** campo sia selezionato e l'indirizzo IP hello è in corso di hello della fase di modifica.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-138">In hello following example, hello **IP address** field is selected, and hello IP address is in hello process of being modified.</span></span>

    ![Modificare un record](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="5ebd3-140">Fare clic su **salvare** in hello cima hello pannello toosave le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-140">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="5ebd3-141">In hello angolo superiore destro, si noterà notifica hello che hello record è stato salvato.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-141">In hello upper right corner, you'll see hello notification that hello record has been saved.</span></span>

    ![Set di record salvato](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="5ebd3-143">Dopo hello record è stato salvato, i valori hello hello record impostare sulla hello **zona DNS** pannello rifletterà record hello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-143">After hello record has been saved, hello values for hello record set on hello **DNS zone** blade will reflect hello updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="5ebd3-144">Rimuovere un record da un set di record</span><span class="sxs-lookup"><span data-stu-id="5ebd3-144">Remove a record from a record set</span></span>

<span data-ttu-id="5ebd3-145">È possibile utilizzare i record di hello Azure tooremove portale da un set di record.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-145">You can use hello Azure portal tooremove records from a record set.</span></span> <span data-ttu-id="5ebd3-146">Si noti che rimozione dell'ultimo record hello un set di record non comporta l'eliminazione del set di record hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-146">Note that removing hello last record from a record set does not delete hello record set.</span></span>

1. <span data-ttu-id="5ebd3-147">In hello **proprietà set di Record** pannello per il set di record, cercare il record di hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-147">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="5ebd3-148">Fare clic su record hello che si desidera tooremove.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-148">Click hello record that you want tooremove.</span></span> <span data-ttu-id="5ebd3-149">Selezionare **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-149">Then select **Remove**.</span></span>

    ![Rimuovere un record](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="5ebd3-151">Fare clic su **salvare** in hello cima hello pannello toosave le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-151">Click **Save** at hello top of hello blade toosave your settings.</span></span>
4. <span data-ttu-id="5ebd3-152">Dopo aver rimosso il record di hello, hello valori hello record su hello **zona DNS** pannello rifletterà la rimozione di hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-152">After hello record has been removed, hello values for hello record on hello **DNS zone** blade will reflect hello removal.</span></span>

## <span data-ttu-id="5ebd3-153"><a name="delete"></a>Eliminare un set di record</span><span class="sxs-lookup"><span data-stu-id="5ebd3-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="5ebd3-154">In hello **proprietà set di Record** pannello per il set di record, fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-154">On hello **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Eliminare un set di record](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="5ebd3-156">Viene visualizzato un messaggio che chiede se si desidera toodelete hello record set.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-156">A message appears asking if you want toodelete hello record set.</span></span>
3. <span data-ttu-id="5ebd3-157">Verificare che hello Nome corrispondenze hello record impostata che desidera toodelete e quindi fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-157">Verify that hello name matches hello record set that you want toodelete, and then click **Yes**.</span></span>
4. <span data-ttu-id="5ebd3-158">In hello **zona DNS** pannello, verificare che i set di record hello non è più visibili.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-158">On hello **DNS zone** blade, verify that hello record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="5ebd3-159">Usare record NS e SOA</span><span class="sxs-lookup"><span data-stu-id="5ebd3-159">Work with NS and SOA records</span></span>

<span data-ttu-id="5ebd3-160">I record NS e SOA creati automaticamente vengono gestiti in modo diverso rispetto ad altri tipi di record.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="5ebd3-161">Modificare i record SOA</span><span class="sxs-lookup"><span data-stu-id="5ebd3-161">Modify SOA records</span></span>

<span data-ttu-id="5ebd3-162">È possibile aggiungere o rimuovere i record da hello automaticamente creato un record SOA impostato al vertice zona hello (nome = "@").</span><span class="sxs-lookup"><span data-stu-id="5ebd3-162">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (name = "@").</span></span> <span data-ttu-id="5ebd3-163">Tuttavia, è possibile modificare i parametri di hello all'interno di hello record SOA (ad eccezione di "Host") e impostare il valore TTL record hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-163">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

### <a name="modify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="5ebd3-164">Modificare i record NS al vertice zona hello</span><span class="sxs-lookup"><span data-stu-id="5ebd3-164">Modify NS records at hello zone apex</span></span>

<span data-ttu-id="5ebd3-165">record NS Hello impostato al vertice zona hello viene creato automaticamente con ogni zona DNS.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-165">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="5ebd3-166">Contiene i nomi hello della zona di hello DNS di Azure nome server toohello assegnato.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-166">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="5ebd3-167">È possibile aggiungere nomi aggiuntivi server toothis NS set di record, toosupport CO-ospitano i domini con più di un provider DNS.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-167">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="5ebd3-168">È inoltre possibile modificare hello durata (TTL) e i metadati per questo set di record.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-168">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="5ebd3-169">Tuttavia, è Impossibile rimuovere o modificare server dei nomi DNS di Azure prepopolato hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-169">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="5ebd3-170">Si noti che questo si applica solo toohello NS set di record al vertice zona hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-170">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="5ebd3-171">Altri set di record NS nella zona (come le aree figlio toodelegate usato) possono essere modificati senza vincoli.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-171">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="5ebd3-172">Eliminare set di record SOA o NS</span><span class="sxs-lookup"><span data-stu-id="5ebd3-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="5ebd3-173">Non è possibile eliminare hello SOA e NS set di record al vertice zona hello (nome = "@") che vengono creati automaticamente quando si crea la zona hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-173">You cannot delete hello SOA and NS record sets at hello zone apex (name = "@") that are created automatically when hello zone is created.</span></span> <span data-ttu-id="5ebd3-174">Vengono eliminate automaticamente quando si elimina la zona hello.</span><span class="sxs-lookup"><span data-stu-id="5ebd3-174">They are deleted automatically when you delete hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ebd3-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5ebd3-175">Next steps</span></span>

* <span data-ttu-id="5ebd3-176">Per ulteriori informazioni su DNS di Azure, vedere hello [Panoramica di DNS di Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ebd3-176">For more information about Azure DNS, see hello [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="5ebd3-177">Per ulteriori informazioni su come automatizzare DNS, vedere [le zone DNS di creazione e set di record mediante .NET SDK di hello](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5ebd3-177">For more information about automating DNS, see [Creating DNS zones and record sets using hello .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="5ebd3-178">Per altre informazioni sui record DNS inversi, vedere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ebd3-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
