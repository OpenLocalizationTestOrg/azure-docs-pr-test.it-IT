---
title: aaaRestrict l'accesso con firme di accesso condiviso - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse firme di accesso condiviso toorestrict HDInsight accedere toodata archiviato nel BLOB di archiviazione di Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a><span data-ttu-id="c7bae-103">Utilizzo di firme di accesso condiviso archiviazione Azure toorestrict accesso toodata in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7bae-103">Use Azure Storage Shared Access Signatures toorestrict access toodata in HDInsight</span></span>

<span data-ttu-id="c7bae-104">HDInsight dispone di accesso completo toodata negli account di archiviazione di Azure hello associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="c7bae-104">HDInsight has full access toodata in hello Azure Storage accounts associated with hello cluster.</span></span> <span data-ttu-id="c7bae-105">È possibile utilizzare le firme di accesso condiviso ai dati del blob contenitore toorestrict accesso toohello hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-105">You can use Shared Access Signatures on hello blob container toorestrict access toohello data.</span></span> <span data-ttu-id="c7bae-106">Ad esempio, tooprovide accesso in sola lettura toohello dati.</span><span class="sxs-lookup"><span data-stu-id="c7bae-106">For example, tooprovide read-only access toohello data.</span></span> <span data-ttu-id="c7bae-107">Le firme di accesso condiviso (SAS) sono una funzionalità di account di archiviazione di Azure che consente di toolimit toodata di accesso.</span><span class="sxs-lookup"><span data-stu-id="c7bae-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you toolimit access toodata.</span></span> <span data-ttu-id="c7bae-108">Ad esempio, fornendo toodata accesso in sola lettura.</span><span class="sxs-lookup"><span data-stu-id="c7bae-108">For example, providing read-only access toodata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7bae-109">Per una soluzione che usi Apache Ranger, considerare la possibilità di usare HDInsight aggiunto al dominio.</span><span class="sxs-lookup"><span data-stu-id="c7bae-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="c7bae-110">Per ulteriori informazioni, vedere hello [configurare dominio HDInsight](hdinsight-domain-joined-configure.md) documento.</span><span class="sxs-lookup"><span data-stu-id="c7bae-110">For more information, see hello [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="c7bae-111">HDInsight è necessario spazio di archiviazione di accesso completo toohello predefinito per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-111">HDInsight must have full access toohello default storage for hello cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="c7bae-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="c7bae-112">Requirements</span></span>

* <span data-ttu-id="c7bae-113">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7bae-113">An Azure subscription</span></span>
* <span data-ttu-id="c7bae-114">C# o Python.</span><span class="sxs-lookup"><span data-stu-id="c7bae-114">C# or Python.</span></span> <span data-ttu-id="c7bae-115">Il codice di esempio in C# viene fornito come soluzione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7bae-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="c7bae-116">Visual Studio versione 2013, 2015 o 2017</span><span class="sxs-lookup"><span data-stu-id="c7bae-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="c7bae-117">Python versione 2.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="c7bae-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="c7bae-118">Un cluster HDInsight basati su Linux o [Azure PowerShell] [ powershell] -se si dispone di un cluster esistente basata su Linux, è possibile utilizzare Ambari tooadd un cluster di toohello di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="c7bae-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari tooadd a Shared Access Signature toohello cluster.</span></span> <span data-ttu-id="c7bae-119">In caso contrario, è possibile usare Azure PowerShell toocreate un cluster e aggiungere una firma di accesso condiviso durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="c7bae-119">If not, you can use Azure PowerShell toocreate a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c7bae-120">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="c7bae-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c7bae-121">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c7bae-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c7bae-122">i file di esempio da Hello [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="c7bae-122">hello example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="c7bae-123">Il repository contiene hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="c7bae-123">This repository contains hello following items:</span></span>

  * <span data-ttu-id="c7bae-124">Un progetto di Visual Studio che può creare un contenitore di archiviazione, i criteri archiviati e la firma di accesso condiviso da usare con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7bae-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="c7bae-125">Uno script di Python che può creare un contenitore di archiviazione, i criteri archiviati e la firma di accesso condiviso da usare con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7bae-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="c7bae-126">Uno script di PowerShell che è possibile creare un HDInsight cluster e configurarlo hello toouse SAS.</span><span class="sxs-lookup"><span data-stu-id="c7bae-126">A PowerShell script that can create a HDInsight cluster and configure it toouse hello SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="c7bae-127">Firme di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="c7bae-127">Shared Access Signatures</span></span>

<span data-ttu-id="c7bae-128">Esistono due tipi di firme di accesso condiviso:</span><span class="sxs-lookup"><span data-stu-id="c7bae-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="c7bae-129">Ad hoc: hello ora di inizio, ora di scadenza e le autorizzazioni per hello SAS vengono specificate in hello URI SAS.</span><span class="sxs-lookup"><span data-stu-id="c7bae-129">Ad hoc: hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span>

* <span data-ttu-id="c7bae-130">Criteri di accesso archiviati: i criteri di accesso archiviati vengono definiti per un contenitore di risorse, ovvero un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="c7bae-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="c7bae-131">I criteri possono essere utilizzati toomanage vincoli per uno o più firme di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="c7bae-131">A policy can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="c7bae-132">Quando si associa una firma di accesso condiviso con criteri di accesso archiviati, hello SAS eredita i vincoli di hello: hello ora di inizio, ora di scadenza e le autorizzazioni - definite per i criteri di accesso archiviato hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-132">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span>

<span data-ttu-id="c7bae-133">Hello differenza tra hello due forme è importante per uno scenario di chiave: revoche di certificati.</span><span class="sxs-lookup"><span data-stu-id="c7bae-133">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="c7bae-134">Una firma di accesso condiviso è un URL, chiunque Ottiene hello SAS poterla utilizzare, indipendentemente dal fatto che ne ha richiesto toobegin con.</span><span class="sxs-lookup"><span data-stu-id="c7bae-134">A SAS is a URL, so anyone who obtains hello SAS can use it, regardless of who requested it toobegin with.</span></span> <span data-ttu-id="c7bae-135">Se una firma di accesso condiviso viene pubblicato, può essere utilizzato da chiunque in HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="c7bae-135">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="c7bae-136">Una forma di accesso condiviso rimane valida finché non si verifica una delle quattro condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7bae-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="c7bae-137">ora di scadenza Hello specificato su hello che SAS viene raggiunto.</span><span class="sxs-lookup"><span data-stu-id="c7bae-137">hello expiry time specified on hello SAS is reached.</span></span>

2. <span data-ttu-id="c7bae-138">ora di scadenza Hello specificato nel criterio di accesso archiviato hello hello che viene raggiunto firma di accesso condiviso a cui fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="c7bae-138">hello expiry time specified on hello stored access policy referenced by hello SAS is reached.</span></span> <span data-ttu-id="c7bae-139">negli scenari seguenti Hello causano l'ora di scadenza hello toobe raggiunto:</span><span class="sxs-lookup"><span data-stu-id="c7bae-139">hello following scenarios cause hello expiry time toobe reached:</span></span>

    * <span data-ttu-id="c7bae-140">è trascorso l'intervallo di tempo Hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-140">hello time interval has elapsed.</span></span>
    * <span data-ttu-id="c7bae-141">i criteri di accesso archiviato Hello sono toohave modificata un'ora di scadenza in hello precedente.</span><span class="sxs-lookup"><span data-stu-id="c7bae-141">hello stored access policy is modified toohave an expiry time in hello past.</span></span> <span data-ttu-id="c7bae-142">Modificando l'ora di scadenza hello è un modo toorevoke hello SAS.</span><span class="sxs-lookup"><span data-stu-id="c7bae-142">Changing hello expiry time is one way toorevoke hello SAS.</span></span>

3. <span data-ttu-id="c7bae-143">Hello archiviati i criteri di accesso a cui fa riferimento hello che SAS viene eliminato, ovvero hello toorevoke di un altro modo SAS.</span><span class="sxs-lookup"><span data-stu-id="c7bae-143">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="c7bae-144">Se si ricrea il criterio di accesso archiviato hello con stesso nome, tutti i token di firma di accesso condiviso per hello criteri precedenti hello valide (se l'ora di scadenza hello in hello SAS non ha superato).</span><span class="sxs-lookup"><span data-stu-id="c7bae-144">If you recreate hello stored access policy with hello same name, all  SAS tokens for hello previous policy are valid (if hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="c7bae-145">Se si prevede di hello toorevoke SAS, essere toouse che un altro nome se si ricrea il criterio di accesso hello con un'ora di scadenza in hello future.</span><span class="sxs-lookup"><span data-stu-id="c7bae-145">If you intend toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>

4. <span data-ttu-id="c7bae-146">chiave dell'account che è stato utilizzato toocreate hello SAS Hello viene rigenerato.</span><span class="sxs-lookup"><span data-stu-id="c7bae-146">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="c7bae-147">Rigenerazione della chiave di hello fa sì che tutte le applicazioni che utilizzano l'autenticazione chiave toofail hello precedente.</span><span class="sxs-lookup"><span data-stu-id="c7bae-147">Regenerating hello key causes all applications that use hello previous key toofail authentication.</span></span> <span data-ttu-id="c7bae-148">Aggiornare la chiave di nuovo di tutti i componenti toohello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-148">Update all components toohello new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7bae-149">Un URI di firma di accesso condiviso è associato con firma di hello toocreate utilizzati chiave account hello e hello associati criteri di accesso archiviati (se presente).</span><span class="sxs-lookup"><span data-stu-id="c7bae-149">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="c7bae-150">Se si specifica alcun criterio di accesso archiviati, hello solo modo toorevoke una firma di accesso condiviso è toochange hello account chiave.</span><span class="sxs-lookup"><span data-stu-id="c7bae-150">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

<span data-ttu-id="c7bae-151">È consigliabile usare sempre i criteri di accesso archiviati.</span><span class="sxs-lookup"><span data-stu-id="c7bae-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="c7bae-152">Quando si utilizzano i criteri archiviati, è possibile revocare le firme o estendere la data di scadenza hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c7bae-152">When using stored policies, you can either revoke signatures or extend hello expiry date as needed.</span></span> <span data-ttu-id="c7bae-153">passaggi di Hello in questo documento usano i criteri di accesso archiviati toogenerate SAS.</span><span class="sxs-lookup"><span data-stu-id="c7bae-153">hello steps in this document use stored access policies toogenerate SAS.</span></span>

<span data-ttu-id="c7bae-154">Per ulteriori informazioni sulle firme di accesso condiviso, vedere [modello di firma di accesso condiviso hello comprensione](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="c7bae-154">For more information on Shared Access Signatures, see [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="c7bae-155">Creare un criterio archiviato e una firma di accesso condiviso con C\#</span><span class="sxs-lookup"><span data-stu-id="c7bae-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="c7bae-156">Aprire la soluzione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7bae-156">Open hello solution in Visual Studio.</span></span>

2. <span data-ttu-id="c7bae-157">In Esplora soluzioni, fare clic su hello **SASToken** del progetto e selezionare **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="c7bae-157">In Solution Explorer, right-click on hello **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="c7bae-158">Selezionare **impostazioni** e aggiungere i valori per hello seguenti voci:</span><span class="sxs-lookup"><span data-stu-id="c7bae-158">Select **Settings** and add values for hello following entries:</span></span>

   * <span data-ttu-id="c7bae-159">StorageConnectionString: hello stringa di connessione per l'account di archiviazione hello che si desidera toocreate un criterio archiviato e SAS per.</span><span class="sxs-lookup"><span data-stu-id="c7bae-159">StorageConnectionString: hello connection string for hello storage account that you want toocreate a stored policy and SAS for.</span></span> <span data-ttu-id="c7bae-160">deve essere formato Hello `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` in `myaccount` hello nome dell'account di archiviazione e `mykey` è hello chiave hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c7bae-160">hello format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is hello name of your storage account and `mykey` is hello key for hello storage account.</span></span>

   * <span data-ttu-id="c7bae-161">ContainerName: contenitore hello nell'account di archiviazione hello che si desidera accedere toorestrict a.</span><span class="sxs-lookup"><span data-stu-id="c7bae-161">ContainerName: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="c7bae-162">SASPolicyName: hello Nome toouse per hello archiviati toocreate criteri.</span><span class="sxs-lookup"><span data-stu-id="c7bae-162">SASPolicyName: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="c7bae-163">FileToUpload: hello percorso tooa file contenitore toohello caricato.</span><span class="sxs-lookup"><span data-stu-id="c7bae-163">FileToUpload: hello path tooa file that is uploaded toohello container.</span></span>

4. <span data-ttu-id="c7bae-164">Eseguire il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-164">Run hello project.</span></span> <span data-ttu-id="c7bae-165">Toohello simile di informazioni dopo il testo viene visualizzato dopo che è stato generato hello SAS:</span><span class="sxs-lookup"><span data-stu-id="c7bae-165">Information similar toohello following text is displayed once hello SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="c7bae-166">Salvare i token del criterio SAS hello, nome account di archiviazione e nome del contenitore.</span><span class="sxs-lookup"><span data-stu-id="c7bae-166">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="c7bae-167">Questi valori vengono utilizzati quando si associa l'account di archiviazione hello con il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7bae-167">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="c7bae-168">Creare un criterio archiviato e una firma di accesso condiviso con Python</span><span class="sxs-lookup"><span data-stu-id="c7bae-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="c7bae-169">Aprire il file SASToken.py hello e modificare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="c7bae-169">Open hello SASToken.py file and change hello following values:</span></span>

   * <span data-ttu-id="c7bae-170">criteri\_nome: hello Nome toouse per hello archiviati toocreate criteri.</span><span class="sxs-lookup"><span data-stu-id="c7bae-170">policy\_name: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="c7bae-171">archiviazione\_account\_name: nome hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c7bae-171">storage\_account\_name: hello name of your storage account.</span></span>

   * <span data-ttu-id="c7bae-172">archiviazione\_account\_chiave: hello chiave hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c7bae-172">storage\_account\_key: hello key for hello storage account.</span></span>

   * <span data-ttu-id="c7bae-173">archiviazione\_contenitore\_nome: il contenitore di hello nell'account di archiviazione hello che si desidera accedere toorestrict a.</span><span class="sxs-lookup"><span data-stu-id="c7bae-173">storage\_container\_name: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="c7bae-174">esempio\_file\_percorso: hello percorso tooa file contenitore toohello caricato.</span><span class="sxs-lookup"><span data-stu-id="c7bae-174">example\_file\_path: hello path tooa file that is uploaded toohello container.</span></span>

2. <span data-ttu-id="c7bae-175">Eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-175">Run hello script.</span></span> <span data-ttu-id="c7bae-176">Visualizza hello SAS token simile toohello seguente testo al termine dello script hello:</span><span class="sxs-lookup"><span data-stu-id="c7bae-176">It displays hello SAS token similar toohello following text when hello script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="c7bae-177">Salvare i token del criterio SAS hello, nome account di archiviazione e nome del contenitore.</span><span class="sxs-lookup"><span data-stu-id="c7bae-177">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="c7bae-178">Questi valori vengono utilizzati quando si associa l'account di archiviazione hello con il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7bae-178">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

## <a name="use-hello-sas-with-hdinsight"></a><span data-ttu-id="c7bae-179">Utilizzare hello SAS con HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7bae-179">Use hello SAS with HDInsight</span></span>

<span data-ttu-id="c7bae-180">Quando si crea un cluster HDInsight è necessario specificare un account di archiviazione primario e, facoltativamente, è possibile specificare account di archiviazione aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="c7bae-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="c7bae-181">Entrambi i metodi di aggiunta di memoria richiedono account di archiviazione toohello accesso completo e contenitori che vengono utilizzati.</span><span class="sxs-lookup"><span data-stu-id="c7bae-181">Both of these methods of adding storage require full access toohello storage accounts and containers that are used.</span></span>

<span data-ttu-id="c7bae-182">toouse contenitore tooa accesso toolimit firma di accesso condiviso, aggiungere una voce personalizzata di toohello **core sito** configurazione per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-182">toouse a Shared Access Signature toolimit access tooa container, add a custom entry toohello **core-site** configuration for hello cluster.</span></span>

* <span data-ttu-id="c7bae-183">Per **basati su Windows** o **basati su Linux** cluster HDInsight, è possibile aggiungere la voce hello durante la creazione del cluster tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7bae-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add hello entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="c7bae-184">Per **basati su Linux** cluster HDInsight, modificare la configurazione di hello dopo la creazione di cluster con Ambari.</span><span class="sxs-lookup"><span data-stu-id="c7bae-184">For **Linux-based** HDInsight clusters, change hello configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-hello-sas"></a><span data-ttu-id="c7bae-185">Creare un cluster che usa hello SAS</span><span class="sxs-lookup"><span data-stu-id="c7bae-185">Create a cluster that uses hello SAS</span></span>

<span data-ttu-id="c7bae-186">Un esempio di creazione di un cluster HDInsight che hello utilizza firma di accesso condiviso è incluso in hello `CreateCluster` directory del repository hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-186">An example of creating an HDInsight cluster that uses hello SAS is included in hello `CreateCluster` directory of hello repository.</span></span> <span data-ttu-id="c7bae-187">toouse, utilizzare hello seguendo i passaggi:</span><span class="sxs-lookup"><span data-stu-id="c7bae-187">toouse it, use hello following steps:</span></span>

1. <span data-ttu-id="c7bae-188">Aprire hello `CreateCluster\HDInsightSAS.ps1` file in un editor di testo e modificare i seguenti valori all'inizio di hello del documento hello hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-188">Open hello `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify hello following values at hello beginning of hello document.</span></span>

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="c7bae-189">Ad esempio, modificare `'mycluster'` toohello nome del cluster hello desiderato toocreate.</span><span class="sxs-lookup"><span data-stu-id="c7bae-189">For example, change `'mycluster'` toohello name of hello cluster you want toocreate.</span></span> <span data-ttu-id="c7bae-190">i valori di firma di accesso condiviso Hello devono corrispondere i valori hello nei passaggi precedenti hello durante la creazione di un account di archiviazione e il token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="c7bae-190">hello SAS values should match hello values from hello previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="c7bae-191">Dopo avere modificato i valori hello, salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-191">Once you have changed hello values, save hello file.</span></span>

2. <span data-ttu-id="c7bae-192">Aprire un nuovo prompt dei comandi di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7bae-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="c7bae-193">Se non si ha familiarità con Azure PowerShell o non è stato installato, vedere [Install and configure Azure PowerShell][powershell] (Installare e configurare Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="c7bae-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="c7bae-194">Dal prompt dei comandi hello, utilizzare hello successivo comando tooauthenticate tooyour sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="c7bae-194">From hello prompt, use hello following command tooauthenticate tooyour Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="c7bae-195">Quando richiesto, accedere con l'account hello per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7bae-195">When prompted, log in with hello account for your Azure subscription.</span></span>

    <span data-ttu-id="c7bae-196">Se l'account è associato a più sottoscrizioni di Azure, potrebbe essere necessario toouse `Select-AzureRmSubscription` sottoscrizione hello tooselect desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="c7bae-196">If your account is associated with multiple Azure subscriptions, you may need toouse `Select-AzureRmSubscription` tooselect hello subscription you wish toouse.</span></span>

4. <span data-ttu-id="c7bae-197">Dal prompt dei comandi hello, modificare le directory toohello `CreateCluster` directory che contiene file HDInsightSAS.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-197">From hello prompt, change directories toohello `CreateCluster` directory that contains hello HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="c7bae-198">Quindi utilizzare lo script di comando toorun hello seguente hello</span><span class="sxs-lookup"><span data-stu-id="c7bae-198">Then use hello following command toorun hello script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="c7bae-199">Durante l'esecuzione di script hello, Registra prompt di PowerShell toohello output durante la creazione risorsa hello gli account di archiviazione e di gruppo.</span><span class="sxs-lookup"><span data-stu-id="c7bae-199">As hello script runs, it logs output toohello PowerShell prompt as it creates hello resource group and storage accounts.</span></span> <span data-ttu-id="c7bae-200">Si è utente di hello HTTP richiesta tooenter per hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7bae-200">You are prompted tooenter hello HTTP user for hello HDInsight cluster.</span></span> <span data-ttu-id="c7bae-201">Questo account è di tipo cluster toohello di accesso HTTP/s toosecure utilizzato.</span><span class="sxs-lookup"><span data-stu-id="c7bae-201">This account is used toosecure HTTP/s access toohello cluster.</span></span>

    <span data-ttu-id="c7bae-202">Se si sta creando un cluster basato su Linux, viene chiesto di specificare anche un nome e una password per l'account utente SSH.</span><span class="sxs-lookup"><span data-stu-id="c7bae-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="c7bae-203">Questo account è usato tooremotely log toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="c7bae-203">This account is used tooremotely log in toohello cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c7bae-204">Quando viene richiesto di hello HTTP/s o nome utente SSH e password, è necessario fornire una password che soddisfi i seguenti criteri hello:</span><span class="sxs-lookup"><span data-stu-id="c7bae-204">When prompted for hello HTTP/s or SSH user name and password, you must provide a password that meets hello following criteria:</span></span>
   >
   > * <span data-ttu-id="c7bae-205">La lunghezza non può essere inferiore a 10 caratteri</span><span class="sxs-lookup"><span data-stu-id="c7bae-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="c7bae-206">Deve contenere almeno una cifra</span><span class="sxs-lookup"><span data-stu-id="c7bae-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="c7bae-207">Deve contenere almeno un carattere non alfanumerico</span><span class="sxs-lookup"><span data-stu-id="c7bae-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="c7bae-208">Deve contenere almeno una lettera maiuscola o minuscola</span><span class="sxs-lookup"><span data-stu-id="c7bae-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="c7bae-209">Occorre un po' di tempo per toocomplete questo script, in genere circa 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="c7bae-209">It takes a while for this script toocomplete, usually around 15 minutes.</span></span> <span data-ttu-id="c7bae-210">Al termine dello script hello senza errori, è stato creato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-210">When hello script completes without any errors, hello cluster has been created.</span></span>

### <a name="use-hello-sas-with-an-existing-cluster"></a><span data-ttu-id="c7bae-211">Utilizzare hello SAS con un cluster esistente</span><span class="sxs-lookup"><span data-stu-id="c7bae-211">Use hello SAS with an existing cluster</span></span>

<span data-ttu-id="c7bae-212">Se si dispone di un cluster esistente basata su Linux, è possibile aggiungere hello SAS toohello **core sito** configurazione utilizzando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c7bae-212">If you have an existing Linux-based cluster, you can add hello SAS toohello **core-site** configuration by using hello following steps:</span></span>

1. <span data-ttu-id="c7bae-213">Aprire hello Ambari web dell'interfaccia utente per il cluster.</span><span class="sxs-lookup"><span data-stu-id="c7bae-213">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="c7bae-214">indirizzo Hello questa pagina è https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="c7bae-214">hello address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="c7bae-215">Quando richiesto, eseguire l'autenticazione toohello cluster utilizzando il nome amministratore hello (amministratore) e la password utilizzati durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-215">When prompted, authenticate toohello cluster using hello admin name (admin) and password you used when creating hello cluster.</span></span>

2. <span data-ttu-id="c7bae-216">Hello il lato sinistro di hello Ambari web dell'interfaccia utente, selezionare **HDFS** e quindi selezionare hello **configurazioni** scheda centro hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-216">From hello left side of hello Ambari web UI, select **HDFS** and then select hello **Configs** tab in hello middle of hello page.</span></span>

3. <span data-ttu-id="c7bae-217">Seleziona hello **avanzate** scheda e quindi scorrere fino a individuare hello **dei siti principali personalizzato** sezione.</span><span class="sxs-lookup"><span data-stu-id="c7bae-217">Select hello **Advanced** tab, and then scroll until you find hello **Custom core-site** section.</span></span>

4. <span data-ttu-id="c7bae-218">Espandere hello **Custom. core-sito** sezione, quindi Fine toohello scorrere e seleziona hello **aggiungere proprietà...**  collegamento.</span><span class="sxs-lookup"><span data-stu-id="c7bae-218">Expand hello **Custom core-site** section, then scroll toohello end and select hello **Add property...** link.</span></span> <span data-ttu-id="c7bae-219">I valori seguenti di hello di utilizzo per hello **chiave** e **valore** campi:</span><span class="sxs-lookup"><span data-stu-id="c7bae-219">Use hello following values for hello **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="c7bae-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="c7bae-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="c7bae-221">**Valore**: hello SAS restituito da hello applicazione c# o Python è stato eseguito in precedenza</span><span class="sxs-lookup"><span data-stu-id="c7bae-221">**Value**: hello SAS returned by hello C# or Python application you ran previously</span></span>

     <span data-ttu-id="c7bae-222">Sostituire **CONTAINERNAME** con il nome di contenitore hello è usata con un'applicazione hello in c# o SAS.</span><span class="sxs-lookup"><span data-stu-id="c7bae-222">Replace **CONTAINERNAME** with hello container name you used with hello C# or SAS application.</span></span> <span data-ttu-id="c7bae-223">Sostituire **STORAGEACCOUNTNAME** con nome di account di archiviazione hello è stato utilizzato.</span><span class="sxs-lookup"><span data-stu-id="c7bae-223">Replace **STORAGEACCOUNTNAME** with hello storage account name you used.</span></span>

5. <span data-ttu-id="c7bae-224">Fare clic su hello **Aggiungi** toosave questa chiave e valore, quindi fare clic su hello **salvare** pulsante toosave modifiche alla configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-224">Click hello **Add** button toosave this key and value, then click hello **Save** button toosave hello configuration changes.</span></span> <span data-ttu-id="c7bae-225">Quando richiesto, aggiungere una descrizione della modifica di hello ("aggiunta di accesso all'archiviazione SAS", ad esempio) e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="c7bae-225">When prompted, add a description of hello change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="c7bae-226">Fare clic su **OK** quando le modifiche di hello sono state completate.</span><span class="sxs-lookup"><span data-stu-id="c7bae-226">Click **OK** when hello changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c7bae-227">Prima di hello modifica abbia effetto, è necessario riavviare diversi servizi.</span><span class="sxs-lookup"><span data-stu-id="c7bae-227">You must restart several services before hello change takes effect.</span></span>

6. <span data-ttu-id="c7bae-228">Nell'interfaccia utente web di Ambari hello, selezionare **HDFS** elenco hello hello a sinistra e quindi selezionare **riavviare tutti** da hello **azioni servizio** hello destra elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="c7bae-228">In hello Ambari web UI, select **HDFS** from hello list on hello left, and then select **Restart All** from hello **Service Actions** drop down list on hello right.</span></span> <span data-ttu-id="c7bae-229">Quando richiesto, selezionare **Turn on maintenance mode** e quindi selezionare __Conform Restart All".</span><span class="sxs-lookup"><span data-stu-id="c7bae-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="c7bae-230">Ripetere il processo per MapReduce2 e YARN.</span><span class="sxs-lookup"><span data-stu-id="c7bae-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="c7bae-231">Dopo aver riavviato servizi hello, selezionare ciascuno di essi e disabilitare la modalità di manutenzione da hello **azioni servizio** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="c7bae-231">Once hello services have restarted, select each one and disable maintenance mode from hello **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="c7bae-232">Testare l'accesso limitato</span><span class="sxs-lookup"><span data-stu-id="c7bae-232">Test restricted access</span></span>

<span data-ttu-id="c7bae-233">tooverify che con accesso limitato, hello di utilizzo dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="c7bae-233">tooverify that you have restricted access, use hello following methods:</span></span>

* <span data-ttu-id="c7bae-234">Per **basati su Windows** cluster HDInsight, utilizzare cluster toohello tooconnect di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="c7bae-234">For **Windows-based** HDInsight clusters, use Remote Desktop tooconnect toohello cluster.</span></span> <span data-ttu-id="c7bae-235">Per ulteriori informazioni, vedere [connettersi tramite RDP tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="c7bae-235">For more information, see [Connect tooHDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="c7bae-236">Una volta connessi, utilizzare hello **Hadoop della riga di comando** icona su hello desktop tooopen un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="c7bae-236">Once connected, use hello **Hadoop Command-Line** icon on hello desktop tooopen a command prompt.</span></span>

* <span data-ttu-id="c7bae-237">Per **basati su Linux** cluster HDInsight, usare SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="c7bae-237">For **Linux-based** HDInsight clusters, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="c7bae-238">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c7bae-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="c7bae-239">Una volta connessi toohello cluster, utilizzare hello tooverify passaggi che è possibile solo lettura e l'elenco di elementi presenti in account di archiviazione SAS hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7bae-239">Once connected toohello cluster, use hello following steps tooverify that you can only read and list items on hello SAS storage account:</span></span>

1. <span data-ttu-id="c7bae-240">comando seguente dal prompt dei comandi hello hello del contenuto di hello toolist del contenitore di hello, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="c7bae-240">toolist hello contents of hello container, use hello following command from hello prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="c7bae-241">Sostituire **SASCONTAINER** con nome hello del contenitore di hello creato per l'account di archiviazione SAS hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-241">Replace **SASCONTAINER** with hello name of hello container created for hello SAS storage account.</span></span> <span data-ttu-id="c7bae-242">Sostituire **SASACCOUNTNAME** con nome hello hello dell'account di archiviazione utilizzato per hello SAS.</span><span class="sxs-lookup"><span data-stu-id="c7bae-242">Replace **SASACCOUNTNAME** with hello name of hello storage account used for hello SAS.</span></span>

    <span data-ttu-id="c7bae-243">elenco di Hello include file hello caricate quando sono state create contenitore hello e SAS.</span><span class="sxs-lookup"><span data-stu-id="c7bae-243">hello list includes hello file uploaded when hello container and SAS were created.</span></span>

2. <span data-ttu-id="c7bae-244">Utilizzare hello seguente tooverify comando che è possibile leggere il contenuto di hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-244">Use hello following command tooverify that you can read hello contents of hello file.</span></span> <span data-ttu-id="c7bae-245">Sostituire hello **SASCONTAINER** e **SASACCOUNTNAME** come passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-245">Replace hello **SASCONTAINER** and **SASACCOUNTNAME** as in hello previous step.</span></span> <span data-ttu-id="c7bae-246">Sostituire **FILENAME** con nome hello del file hello visualizzato nel comando precedente hello:</span><span class="sxs-lookup"><span data-stu-id="c7bae-246">Replace **FILENAME** with hello name of hello file displayed in hello previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="c7bae-247">Questo comando Elenca il contenuto di hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-247">This command lists hello contents of hello file.</span></span>

3. <span data-ttu-id="c7bae-248">Utilizzare hello successivo comando toodownload hello file toohello file system locale:</span><span class="sxs-lookup"><span data-stu-id="c7bae-248">Use hello following command toodownload hello file toohello local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="c7bae-249">Questo comando Scarica hello tooa locale da un file denominato **testfile.txt**.</span><span class="sxs-lookup"><span data-stu-id="c7bae-249">This command downloads hello file tooa local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="c7bae-250">Comando che segue di hello utilizzare tooupload hello file locale tooa nuovo file denominato **testupload.txt** su hello archiviazione SAS:</span><span class="sxs-lookup"><span data-stu-id="c7bae-250">Use hello following command tooupload hello local file tooa new file named **testupload.txt** on hello SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="c7bae-251">Viene visualizzato un toohello simile messaggio seguente testo:</span><span class="sxs-lookup"><span data-stu-id="c7bae-251">You receive a message similar toohello following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="c7bae-252">Questo errore si verifica perché il percorso di archiviazione hello lettura + solo nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="c7bae-252">This error occurs because hello storage location is read+list only.</span></span> <span data-ttu-id="c7bae-253">Comando che segue di hello utilizzare dati di hello tooput in hello nell'archivio predefinito per i cluster di hello, che è accessibile in scrittura:</span><span class="sxs-lookup"><span data-stu-id="c7bae-253">Use hello following command tooput hello data on hello default storage for hello cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="c7bae-254">Questa volta, hello operazione deve essere completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="c7bae-254">This time, hello operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c7bae-255">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="c7bae-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="c7bae-256">Un'attività è stata annullata</span><span class="sxs-lookup"><span data-stu-id="c7bae-256">A task was canceled</span></span>

<span data-ttu-id="c7bae-257">**Sintomi**: durante la creazione di un cluster utilizzando uno script di PowerShell hello, potrebbe essere visualizzato hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="c7bae-257">**Symptoms**: When creating a cluster using hello PowerShell script, you may receive hello following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="c7bae-258">**Causa**: questo errore può verificarsi se si utilizza una password per l'utente di amministrazione/HTTP hello per cluster hello o (per i cluster basati su Linux) utente SSH hello.</span><span class="sxs-lookup"><span data-stu-id="c7bae-258">**Cause**: This error can occur if you use a password for hello admin/HTTP user for hello cluster, or (for Linux-based clusters) hello SSH user.</span></span>

<span data-ttu-id="c7bae-259">**Risoluzione**: utilizzare una password che soddisfi i seguenti criteri hello:</span><span class="sxs-lookup"><span data-stu-id="c7bae-259">**Resolution**: Use a password that meets hello following criteria:</span></span>

* <span data-ttu-id="c7bae-260">La lunghezza non può essere inferiore a 10 caratteri</span><span class="sxs-lookup"><span data-stu-id="c7bae-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="c7bae-261">Deve contenere almeno una cifra</span><span class="sxs-lookup"><span data-stu-id="c7bae-261">Must contain at least one digit</span></span>
* <span data-ttu-id="c7bae-262">Deve contenere almeno un carattere non alfanumerico</span><span class="sxs-lookup"><span data-stu-id="c7bae-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="c7bae-263">Deve contenere almeno una lettera maiuscola o minuscola</span><span class="sxs-lookup"><span data-stu-id="c7bae-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7bae-264">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c7bae-264">Next steps</span></span>

<span data-ttu-id="c7bae-265">Ora che si è appreso come tooadd archiviazione ad accesso limitato tooyour cluster HDInsight, informazioni su altri toowork modi con i dati sul cluster:</span><span class="sxs-lookup"><span data-stu-id="c7bae-265">Now that you have learned how tooadd limited-access storage tooyour HDInsight cluster, learn other ways toowork with data on your cluster:</span></span>

* [<span data-ttu-id="c7bae-266">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7bae-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c7bae-267">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7bae-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="c7bae-268">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7bae-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
