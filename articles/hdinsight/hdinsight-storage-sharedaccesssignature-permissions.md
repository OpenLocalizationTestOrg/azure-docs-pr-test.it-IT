---
title: 'Limitare l''accesso usando le firme di accesso condiviso: Azure HDInsight | Microsoft Docs'
description: Informazioni su come usare le firme di accesso condiviso per limitare l'accesso di HDInsight ai dati archiviati nei BLOB di archiviazione di Azure.
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
ms.openlocfilehash: 2e4b1a307fae06c0639d93b9804c6f0f703d5900
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-shared-access-signatures-to-restrict-access-to-data-in-hdinsight"></a><span data-ttu-id="1f5c6-103">Usare le firme di accesso condiviso di archiviazione di Azure per limitare l'accesso ai dati in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f5c6-103">Use Azure Storage Shared Access Signatures to restrict access to data in HDInsight</span></span>

<span data-ttu-id="1f5c6-104">HDInsight ha accesso completo ai dati negli account di archiviazione di Azure associati al cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-104">HDInsight has full access to data in the Azure Storage accounts associated with the cluster.</span></span> <span data-ttu-id="1f5c6-105">È possibile usare le firme di accesso condiviso nel contenitore BLOB per limitare l'accesso ai dati,</span><span class="sxs-lookup"><span data-stu-id="1f5c6-105">You can use Shared Access Signatures on the blob container to restrict access to the data.</span></span> <span data-ttu-id="1f5c6-106">ad esempio per fornire accesso di sola lettura ai dati.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-106">For example, to provide read-only access to the data.</span></span> <span data-ttu-id="1f5c6-107">Le firme di accesso condiviso sono una funzionalità degli account di archiviazione di Azure che consente di limitare l'accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you to limit access to data.</span></span> <span data-ttu-id="1f5c6-108">Ad esempio, concedendo l'accesso in sola lettura ai dati.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-108">For example, providing read-only access to data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f5c6-109">Per una soluzione che usi Apache Ranger, considerare la possibilità di usare HDInsight aggiunto al dominio.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="1f5c6-110">Per altre informazioni, vedere il documento [Configurare i cluster HDInsight aggiunti al dominio](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1f5c6-110">For more information, see the [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="1f5c6-111">HDInsight deve avere accesso completo alla risorsa di archiviazione predefinita per il cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-111">HDInsight must have full access to the default storage for the cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="1f5c6-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="1f5c6-112">Requirements</span></span>

* <span data-ttu-id="1f5c6-113">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-113">An Azure subscription</span></span>
* <span data-ttu-id="1f5c6-114">C# o Python.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-114">C# or Python.</span></span> <span data-ttu-id="1f5c6-115">Il codice di esempio in C# viene fornito come soluzione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="1f5c6-116">Visual Studio versione 2013, 2015 o 2017</span><span class="sxs-lookup"><span data-stu-id="1f5c6-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="1f5c6-117">Python versione 2.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="1f5c6-118">Un cluster HDInsight basato su Linux OPPURE [Azure PowerShell][powershell]. Se è disponibile un cluster basato su Linux esistente, è possibile usare Ambari per aggiungere una firma di accesso condiviso al cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari to add a Shared Access Signature to the cluster.</span></span> <span data-ttu-id="1f5c6-119">In caso contrario, è possibile usare Azure PowerShell per creare un cluster e aggiungere una firma di accesso condiviso durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-119">If not, you can use Azure PowerShell to create a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1f5c6-120">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1f5c6-121">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1f5c6-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="1f5c6-122">I file di esempio da [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="1f5c6-122">The example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="1f5c6-123">Il repository contiene gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-123">This repository contains the following items:</span></span>

  * <span data-ttu-id="1f5c6-124">Un progetto di Visual Studio che può creare un contenitore di archiviazione, i criteri archiviati e la firma di accesso condiviso da usare con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="1f5c6-125">Uno script di Python che può creare un contenitore di archiviazione, i criteri archiviati e la firma di accesso condiviso da usare con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="1f5c6-126">Uno script di PowerShell in grado di creare un cluster HDInsight e configurarlo per l'uso della firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-126">A PowerShell script that can create a HDInsight cluster and configure it to use the SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="1f5c6-127">Firme di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="1f5c6-127">Shared Access Signatures</span></span>

<span data-ttu-id="1f5c6-128">Esistono due tipi di firme di accesso condiviso:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="1f5c6-129">Ad hoc: l'ora di inizio, la scadenza e le autorizzazioni per la firma di accesso condiviso vengono tutte specificate nell'URI corrispondente.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-129">Ad hoc: The start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span>

* <span data-ttu-id="1f5c6-130">Criteri di accesso archiviati: i criteri di accesso archiviati vengono definiti per un contenitore di risorse, ovvero un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="1f5c6-131">I criteri di accesso archiviati possono essere usati per gestire i vincoli per una o più firme di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-131">A policy can be used to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="1f5c6-132">Quando si associa una firma di accesso condiviso a criteri di accesso archiviati, la firma eredita i vincoli, ovvero ora di inizio, scadenza e autorizzazioni, definiti per i criteri di accesso archiviati.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-132">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span>

<span data-ttu-id="1f5c6-133">La differenza tra le due forme è importante un unico scenario chiave, la revoca.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-133">The difference between the two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="1f5c6-134">Una firma di accesso condiviso è un URL, pertanto chiunque la ottiene può utilizzarla indipendentemente da chi l'ha richiesta per iniziare.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-134">A SAS is a URL, so anyone who obtains the SAS can use it, regardless of who requested it to begin with.</span></span> <span data-ttu-id="1f5c6-135">Se la firma di accesso condiviso è stata pubblicata e resa pubblica, può essere usata da chiunque in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-135">If a SAS is published publicly, it can be used by anyone in the world.</span></span> <span data-ttu-id="1f5c6-136">Una forma di accesso condiviso rimane valida finché non si verifica una delle quattro condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="1f5c6-137">Viene raggiunta la scadenza specificata nella firma.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-137">The expiry time specified on the SAS is reached.</span></span>

2. <span data-ttu-id="1f5c6-138">Viene raggiunta la scadenza specificata nei criteri di accesso archiviati a cui fa riferimento la firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-138">The expiry time specified on the stored access policy referenced by the SAS is reached.</span></span> <span data-ttu-id="1f5c6-139">Gli scenari seguenti portano a raggiungere la scadenza:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-139">The following scenarios cause the expiry time to be reached:</span></span>

    * <span data-ttu-id="1f5c6-140">L'intervallo di tempo è trascorso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-140">The time interval has elapsed.</span></span>
    * <span data-ttu-id="1f5c6-141">Per i criteri di accesso archiviati è stata impostata una scadenza nel passato.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-141">The stored access policy is modified to have an expiry time in the past.</span></span> <span data-ttu-id="1f5c6-142">Modificando la scadenza è possibile revocare la firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-142">Changing the expiry time is one way to revoke the SAS.</span></span>

3. <span data-ttu-id="1f5c6-143">I criteri di accesso archiviati cui viene fatto riferimento nella firma di accesso condiviso vengono eliminati e ciò corrisponde a un altro modo per revocare la firma.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-143">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span></span> <span data-ttu-id="1f5c6-144">Se si ricreano i criteri di accesso archiviati specificando lo stesso nome, tutti i token di firma di accesso condiviso relativi ai criteri precedenti restano validi, a condizione che l'ora di scadenza indicata nella firma di accesso condiviso non sia trascorsa.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-144">If you recreate the stored access policy with the same name, all  SAS tokens for the previous policy are valid (if the expiry time on the SAS has not passed).</span></span> <span data-ttu-id="1f5c6-145">Se si intende revocare la firma di accesso condiviso, verificare di usare un nome diverso per ricreare i criteri di accesso archiviati con scadenza nel futuro.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-145">If you intend to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span></span>

4. <span data-ttu-id="1f5c6-146">La chiave dell'account utilizzata per creare la firma di accesso condiviso viene rigenerata.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-146">The account key that was used to create the SAS is regenerated.</span></span> <span data-ttu-id="1f5c6-147">Se si rigenera la chiave, l'autenticazione di tutte le applicazioni che usano la chiave precedente avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-147">Regenerating the key causes all applications that use the previous key to fail authentication.</span></span> <span data-ttu-id="1f5c6-148">Aggiornare tutti i componenti con la nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-148">Update all components to the new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f5c6-149">L'URI di una firma di accesso condiviso è associato alla chiave dell'account usata per creare la firma e ai relativi criteri di accesso archiviati (se presenti).</span><span class="sxs-lookup"><span data-stu-id="1f5c6-149">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span></span> <span data-ttu-id="1f5c6-150">Se non sono specificati criteri di accesso archiviati, l'unico modo per revocare una firma di accesso condiviso consiste nel modificare la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-150">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span></span>

<span data-ttu-id="1f5c6-151">È consigliabile usare sempre i criteri di accesso archiviati.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="1f5c6-152">Con i criteri archiviati, è possibile revocare le firme o estendere la scadenza in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-152">When using stored policies, you can either revoke signatures or extend the expiry date as needed.</span></span> <span data-ttu-id="1f5c6-153">I passaggi illustrati in questo documento permettono di usare i criteri di accesso archiviati per generare firme di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-153">The steps in this document use stored access policies to generate SAS.</span></span>

<span data-ttu-id="1f5c6-154">Per altre informazioni sulle firme di accesso condiviso, vedere [Informazioni sul modello di firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="1f5c6-154">For more information on Shared Access Signatures, see [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="1f5c6-155">Creare un criterio archiviato e una firma di accesso condiviso con C\#</span><span class="sxs-lookup"><span data-stu-id="1f5c6-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="1f5c6-156">Aprire la soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-156">Open the solution in Visual Studio.</span></span>

2. <span data-ttu-id="1f5c6-157">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **SASToken** e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-157">In Solution Explorer, right-click on the **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="1f5c6-158">Selezionare **Impostazioni** e aggiungere i valori per le voci seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-158">Select **Settings** and add values for the following entries:</span></span>

   * <span data-ttu-id="1f5c6-159">StorageConnectionString: stringa di connessione per l'account di archiviazione per cui si vuole creare un criterio archiviato e una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-159">StorageConnectionString: The connection string for the storage account that you want to create a stored policy and SAS for.</span></span> <span data-ttu-id="1f5c6-160">Il formato deve essere `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey`, dove `myaccount` è il nome dell'account di archiviazione e `mykey` è la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-160">The format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is the name of your storage account and `mykey` is the key for the storage account.</span></span>

   * <span data-ttu-id="1f5c6-161">ContainerName: contenitore nell'account di archiviazione a cui si vuole limitare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-161">ContainerName: The container in the storage account that you want to restrict access to.</span></span>

   * <span data-ttu-id="1f5c6-162">SASPolicyName: nome da usare per i criteri archiviati da creare.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-162">SASPolicyName: The name to use for the stored policy to create.</span></span>

   * <span data-ttu-id="1f5c6-163">FileToUpload: percorso di un file caricato nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-163">FileToUpload: The path to a file that is uploaded to the container.</span></span>

4. <span data-ttu-id="1f5c6-164">Eseguire il progetto.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-164">Run the project.</span></span> <span data-ttu-id="1f5c6-165">Dopo la generazione della firma di accesso condiviso, vengono visualizzate informazioni simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-165">Information similar to the following text is displayed once the SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="1f5c6-166">Salvare il token dei criteri di firma di accesso condiviso, il nome dell'account di archiviazione e il nome del contenitore.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-166">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="1f5c6-167">Questi valori vengono usati quando si associa l'account di archiviazione al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-167">These values are used when associating the storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="1f5c6-168">Creare un criterio archiviato e una firma di accesso condiviso con Python</span><span class="sxs-lookup"><span data-stu-id="1f5c6-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="1f5c6-169">Aprire il file SASToken.py e modificare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-169">Open the SASToken.py file and change the following values:</span></span>

   * <span data-ttu-id="1f5c6-170">policy\_name: nome da usare per i criteri archiviati da creare.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-170">policy\_name: The name to use for the stored policy to create.</span></span>

   * <span data-ttu-id="1f5c6-171">storage\_account\_name: nome del proprio account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-171">storage\_account\_name: The name of your storage account.</span></span>

   * <span data-ttu-id="1f5c6-172">storage\_account\_key: chiave per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-172">storage\_account\_key: The key for the storage account.</span></span>

   * <span data-ttu-id="1f5c6-173">storage\_container\_name: contenitore nell'account di archiviazione a cui si vuole limitare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-173">storage\_container\_name: The container in the storage account that you want to restrict access to.</span></span>

   * <span data-ttu-id="1f5c6-174">example\_file\_path: percorso di un file caricato nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-174">example\_file\_path: The path to a file that is uploaded to the container.</span></span>

2. <span data-ttu-id="1f5c6-175">Eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-175">Run the script.</span></span> <span data-ttu-id="1f5c6-176">Al termine dello script viene visualizzato un token della firma di accesso condiviso simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-176">It displays the SAS token similar to the following text when the script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="1f5c6-177">Salvare il token dei criteri di firma di accesso condiviso, il nome dell'account di archiviazione e il nome del contenitore.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-177">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="1f5c6-178">Questi valori vengono usati quando si associa l'account di archiviazione al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-178">These values are used when associating the storage account with your HDInsight cluster.</span></span>

## <a name="use-the-sas-with-hdinsight"></a><span data-ttu-id="1f5c6-179">Usare la firma di accesso condiviso con HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f5c6-179">Use the SAS with HDInsight</span></span>

<span data-ttu-id="1f5c6-180">Quando si crea un cluster HDInsight è necessario specificare un account di archiviazione primario e, facoltativamente, è possibile specificare account di archiviazione aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="1f5c6-181">Entrambi i metodi di aggiunta di risorse di archiviazione richiedono l'accesso completo agli account di archiviazione e ai contenitori usati.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-181">Both of these methods of adding storage require full access to the storage accounts and containers that are used.</span></span>

<span data-ttu-id="1f5c6-182">Per usare una firma di accesso condiviso allo scopo di limitare l'accesso a un contenitore, aggiungere una voce personalizzata alla configurazione del **core-site** per il cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-182">To use a Shared Access Signature to limit access to a container, add a custom entry to the **core-site** configuration for the cluster.</span></span>

* <span data-ttu-id="1f5c6-183">Per i cluster HDInsight **basati su Windows** o **basati su Linux**, è possibile aggiungere la voce durante la creazione del cluster con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add the entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="1f5c6-184">Per i cluster HDInsight **basati su Linux**, modificare la configurazione dopo la creazione del cluster con Ambari.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-184">For **Linux-based** HDInsight clusters, change the configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-the-sas"></a><span data-ttu-id="1f5c6-185">Creare un cluster che usa la firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="1f5c6-185">Create a cluster that uses the SAS</span></span>

<span data-ttu-id="1f5c6-186">La directory `CreateCluster` del repository include un esempio di creazione di un cluster HDInsight che usa la firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-186">An example of creating an HDInsight cluster that uses the SAS is included in the `CreateCluster` directory of the repository.</span></span> <span data-ttu-id="1f5c6-187">Per usarlo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-187">To use it, use the following steps:</span></span>

1. <span data-ttu-id="1f5c6-188">Aprire il file `CreateCluster\HDInsightSAS.ps1` in un editor di testo e modificare i valori seguenti all'inizio del documento.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-188">Open the `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify the following values at the beginning of the document.</span></span>

    ```powershell
    # Replace 'mycluster' with the name of the cluster to be created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with the name of the group to be created
    $resourceGroupName = 'myresourcegroup'
    # Replace with the Azure data center you want to the cluster to live in
    $location = 'North Europe'
    # Replace with the name of the default storage account to be created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with the name of the SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with the name of the SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with the SAS token generated earlier
    $SASToken = 'sastoken'
    # Set the number of worker nodes in the cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="1f5c6-189">Ad esempio, sostituire `'mycluster'` con il nome del cluster che si vuole creare.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-189">For example, change `'mycluster'` to the name of the cluster you want to create.</span></span> <span data-ttu-id="1f5c6-190">I valori della firma di accesso condiviso devono corrispondere ai valori usati nei passaggi precedenti durante la creazione di un token dell'account di archiviazione e della firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-190">The SAS values should match the values from the previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="1f5c6-191">Dopo aver modificato i valori, salvare il file.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-191">Once you have changed the values, save the file.</span></span>

2. <span data-ttu-id="1f5c6-192">Aprire un nuovo prompt dei comandi di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="1f5c6-193">Se non si ha familiarità con Azure PowerShell o non è stato installato, vedere [Install and configure Azure PowerShell][powershell] (Installare e configurare Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="1f5c6-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="1f5c6-194">Dal prompt dei comandi usare il comando seguente per eseguire l'autenticazione alla sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-194">From the prompt, use the following command to authenticate to your Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="1f5c6-195">Quando richiesto, accedere con l'account associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-195">When prompted, log in with the account for your Azure subscription.</span></span>

    <span data-ttu-id="1f5c6-196">Se l'account è associato a più sottoscrizioni di Azure, può essere necessario usare `Select-AzureRmSubscription` per selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-196">If your account is associated with multiple Azure subscriptions, you may need to use `Select-AzureRmSubscription` to select the subscription you wish to use.</span></span>

4. <span data-ttu-id="1f5c6-197">Dal prompt dei comandi, passare alla directory `CreateCluster` che contiene il file HDInsightSAS.ps1.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-197">From the prompt, change directories to the `CreateCluster` directory that contains the HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="1f5c6-198">Usare quindi il comando seguente per eseguire lo script</span><span class="sxs-lookup"><span data-stu-id="1f5c6-198">Then use the following command to run the script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="1f5c6-199">Durante l'esecuzione dello script, mentre vengono creati il gruppo di risorse e gli account di archiviazione, l'output viene registrato nel prompt di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-199">As the script runs, it logs output to the PowerShell prompt as it creates the resource group and storage accounts.</span></span> <span data-ttu-id="1f5c6-200">Viene chiesto di immettere l'utente HTTP per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-200">You are prompted to enter the HTTP user for the HDInsight cluster.</span></span> <span data-ttu-id="1f5c6-201">Questo account viene usato per proteggere l'accesso HTTP/s al cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-201">This account is used to secure HTTP/s access to the cluster.</span></span>

    <span data-ttu-id="1f5c6-202">Se si sta creando un cluster basato su Linux, viene chiesto di specificare anche un nome e una password per l'account utente SSH.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="1f5c6-203">Questo account viene usato per accedere in remoto al cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-203">This account is used to remotely log in to the cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1f5c6-204">Quando vengono richiesti un nome e una password per HTTP/S o SSH, è necessario fornire una password che soddisfi i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-204">When prompted for the HTTP/s or SSH user name and password, you must provide a password that meets the following criteria:</span></span>
   >
   > * <span data-ttu-id="1f5c6-205">La lunghezza non può essere inferiore a 10 caratteri</span><span class="sxs-lookup"><span data-stu-id="1f5c6-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="1f5c6-206">Deve contenere almeno una cifra</span><span class="sxs-lookup"><span data-stu-id="1f5c6-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="1f5c6-207">Deve contenere almeno un carattere non alfanumerico</span><span class="sxs-lookup"><span data-stu-id="1f5c6-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="1f5c6-208">Deve contenere almeno una lettera maiuscola o minuscola</span><span class="sxs-lookup"><span data-stu-id="1f5c6-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="1f5c6-209">Il completamento dello script richiede in genere circa 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-209">It takes a while for this script to complete, usually around 15 minutes.</span></span> <span data-ttu-id="1f5c6-210">Se lo script viene completato senza errori, il cluster è stato creato.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-210">When the script completes without any errors, the cluster has been created.</span></span>

### <a name="use-the-sas-with-an-existing-cluster"></a><span data-ttu-id="1f5c6-211">Usare la firma di accesso condiviso con un cluster esistente</span><span class="sxs-lookup"><span data-stu-id="1f5c6-211">Use the SAS with an existing cluster</span></span>

<span data-ttu-id="1f5c6-212">Se è disponibile un cluster basato su Linux esistente, è possibile aggiungere la firma di accesso condiviso alla configurazione del **core-site** seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-212">If you have an existing Linux-based cluster, you can add the SAS to the **core-site** configuration by using the following steps:</span></span>

1. <span data-ttu-id="1f5c6-213">Aprire l'interfaccia utente Web di Ambari per il cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-213">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="1f5c6-214">L'indirizzo di questa pagina è https://NOMECLUSTER.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-214">The address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="1f5c6-215">Quando richiesto, eseguire l'autenticazione al cluster con il nome amministratore (admin) e la password usati durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-215">When prompted, authenticate to the cluster using the admin name (admin) and password you used when creating the cluster.</span></span>

2. <span data-ttu-id="1f5c6-216">Nel lato sinistro dell'interfaccia utente Web di Ambari selezionare **HDFS** e quindi selezionare la scheda **Configs** al centro della pagina.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-216">From the left side of the Ambari web UI, select **HDFS** and then select the **Configs** tab in the middle of the page.</span></span>

3. <span data-ttu-id="1f5c6-217">Selezionare la scheda **Advanced** e scorrere fino alla sezione **Custom core-site**.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-217">Select the **Advanced** tab, and then scroll until you find the **Custom core-site** section.</span></span>

4. <span data-ttu-id="1f5c6-218">Espandere la sezione **Custom core-site**, quindi scorrere fino alla fine e selezionare il collegamento **Add property**.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-218">Expand the **Custom core-site** section, then scroll to the end and select the **Add property...** link.</span></span> <span data-ttu-id="1f5c6-219">Usare i valori seguenti per i campi **Key** e **Value**:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-219">Use the following values for the **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="1f5c6-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1f5c6-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="1f5c6-221">**Value**: la firma di accesso condiviso restituita dall'applicazione C# o Python eseguita in precedenza</span><span class="sxs-lookup"><span data-stu-id="1f5c6-221">**Value**: The SAS returned by the C# or Python application you ran previously</span></span>

     <span data-ttu-id="1f5c6-222">Sostituire **CONTAINERNAME** con il nome del contenitore usato con l'applicazione C# o della firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-222">Replace **CONTAINERNAME** with the container name you used with the C# or SAS application.</span></span> <span data-ttu-id="1f5c6-223">Sostituire **STORAGEACCOUNTNAME** con il nome dell'account di archiviazione usato.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-223">Replace **STORAGEACCOUNTNAME** with the storage account name you used.</span></span>

5. <span data-ttu-id="1f5c6-224">Fare clic sul pulsate **Add** per salvare la chiave e il valore, quindi fare clic sul pulsante **Save** per salvare le modifiche alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-224">Click the **Add** button to save this key and value, then click the **Save** button to save the configuration changes.</span></span> <span data-ttu-id="1f5c6-225">Quando richiesto, aggiungere una descrizione della modifica, ad esempio "aggiunta di accesso alle risorse di archiviazione per le firme di accesso condiviso", e quindi fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="1f5c6-225">When prompted, add a description of the change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="1f5c6-226">Al termine delle modifiche, fare clic su **OK** .</span><span class="sxs-lookup"><span data-stu-id="1f5c6-226">Click **OK** when the changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1f5c6-227">Perché le modifiche siano effettive, è necessario riavviare diversi servizi.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-227">You must restart several services before the change takes effect.</span></span>

6. <span data-ttu-id="1f5c6-228">Nell'interfaccia utente Web di Ambari selezionare **HDFS** dall'elenco a sinistra e quindi selezionare **Restart All** dall'elenco a discesa **Service Actions** a destra.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-228">In the Ambari web UI, select **HDFS** from the list on the left, and then select **Restart All** from the **Service Actions** drop down list on the right.</span></span> <span data-ttu-id="1f5c6-229">Quando richiesto, selezionare **Turn on maintenance mode** e quindi selezionare __Conform Restart All".</span><span class="sxs-lookup"><span data-stu-id="1f5c6-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="1f5c6-230">Ripetere il processo per MapReduce2 e YARN.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="1f5c6-231">Dopo il riavvio di questi servizi, selezionarli uno alla volta e disabilitare la modalità di manutenzione dall'elenco a discesa **Service Actions** (Azioni servizio).</span><span class="sxs-lookup"><span data-stu-id="1f5c6-231">Once the services have restarted, select each one and disable maintenance mode from the **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="1f5c6-232">Testare l'accesso limitato</span><span class="sxs-lookup"><span data-stu-id="1f5c6-232">Test restricted access</span></span>

<span data-ttu-id="1f5c6-233">Per verificare che l'accesso sia effettivamente limitato, usare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-233">To verify that you have restricted access, use the following methods:</span></span>

* <span data-ttu-id="1f5c6-234">Per i cluster HDInsight **basati su Windows** , usare Desktop remoto per connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-234">For **Windows-based** HDInsight clusters, use Remote Desktop to connect to the cluster.</span></span> <span data-ttu-id="1f5c6-235">Per altre informazioni, vedere [Connettersi a HDInsight con RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="1f5c6-235">For more information, see [Connect to HDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="1f5c6-236">Dopo aver stabilito la connessione, usare l'icona della **riga di comando di Hadoop** sul desktop per aprire il prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-236">Once connected, use the **Hadoop Command-Line** icon on the desktop to open a command prompt.</span></span>

* <span data-ttu-id="1f5c6-237">Per i cluster HDInsight **basati su Linux** , usare SSH per connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-237">For **Linux-based** HDInsight clusters, use SSH to connect to the cluster.</span></span> <span data-ttu-id="1f5c6-238">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1f5c6-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="1f5c6-239">Dopo aver stabilito la connessione al cluster, usare la procedura seguente per verificare che nell'account di archiviazione della firma di accesso condiviso sia solo possibile leggere ed elencare gli elementi:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-239">Once connected to the cluster, use the following steps to verify that you can only read and list items on the SAS storage account:</span></span>

1. <span data-ttu-id="1f5c6-240">Per elencare il contenuto del contenitore, usare il comando seguente dal prompt:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-240">To list the contents of the container, use the following command from the prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="1f5c6-241">Sostituire **SASCONTAINER** con il nome del contenitore creato per l'account di archiviazione della firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-241">Replace **SASCONTAINER** with the name of the container created for the SAS storage account.</span></span> <span data-ttu-id="1f5c6-242">Sostituire **SASACCOUNTNAME** con il nome dell'account di archiviazione usato per la firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-242">Replace **SASACCOUNTNAME** with the name of the storage account used for the SAS.</span></span>

    <span data-ttu-id="1f5c6-243">L'elenco include il file caricato quando sono stati creati il contenitore e la firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-243">The list includes the file uploaded when the container and SAS were created.</span></span>

2. <span data-ttu-id="1f5c6-244">Usare il comando seguente per verificare che sia possibile leggere il contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-244">Use the following command to verify that you can read the contents of the file.</span></span> <span data-ttu-id="1f5c6-245">Sostituire **SASCONTAINER** e **SASACCOUNTNAME** come indicato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-245">Replace the **SASCONTAINER** and **SASACCOUNTNAME** as in the previous step.</span></span> <span data-ttu-id="1f5c6-246">Sostituire **FILENAME** con il nome del file visualizzato nel comando precedente:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-246">Replace **FILENAME** with the name of the file displayed in the previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="1f5c6-247">Verrà visualizzato il contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-247">This command lists the contents of the file.</span></span>

3. <span data-ttu-id="1f5c6-248">Usare il comando seguente per scaricare il file nel file system locale:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-248">Use the following command to download the file to the local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="1f5c6-249">Il file verrà scaricato in un file locale denominato **testfile.txt**.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-249">This command downloads the file to a local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="1f5c6-250">Usare il comando seguente per caricare il file locale in un nuovo file denominato **testupload.txt** nella risorsa di archiviazione della firma di accesso condiviso:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-250">Use the following command to upload the local file to a new file named **testupload.txt** on the SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="1f5c6-251">Verrà visualizzato un messaggio simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-251">You receive a message similar to the following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="1f5c6-252">Questo errore si verifica perché il percorso di archiviazione è di sola lettura+elenco.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-252">This error occurs because the storage location is read+list only.</span></span> <span data-ttu-id="1f5c6-253">Usare il comando seguente per inserire i dati nella risorsa di archiviazione predefinita per il cluster, accessibile in scrittura:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-253">Use the following command to put the data on the default storage for the cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="1f5c6-254">Questa volta l'operazione avrà esito positivo.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-254">This time, the operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1f5c6-255">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="1f5c6-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="1f5c6-256">Un'attività è stata annullata</span><span class="sxs-lookup"><span data-stu-id="1f5c6-256">A task was canceled</span></span>

<span data-ttu-id="1f5c6-257">**Sintomi**: durante la creazione di un cluster con lo script di PowerShell, si potrebbe ricevere il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-257">**Symptoms**: When creating a cluster using the PowerShell script, you may receive the following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="1f5c6-258">**Causa**: questo errore può verificarsi se si usa una password per l'utente admin/HTTP per il cluster oppure, nei cluster basati su Linux, per l'utente SSH.</span><span class="sxs-lookup"><span data-stu-id="1f5c6-258">**Cause**: This error can occur if you use a password for the admin/HTTP user for the cluster, or (for Linux-based clusters) the SSH user.</span></span>

<span data-ttu-id="1f5c6-259">**Risoluzione**: usare una password che soddisfi i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-259">**Resolution**: Use a password that meets the following criteria:</span></span>

* <span data-ttu-id="1f5c6-260">La lunghezza non può essere inferiore a 10 caratteri</span><span class="sxs-lookup"><span data-stu-id="1f5c6-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="1f5c6-261">Deve contenere almeno una cifra</span><span class="sxs-lookup"><span data-stu-id="1f5c6-261">Must contain at least one digit</span></span>
* <span data-ttu-id="1f5c6-262">Deve contenere almeno un carattere non alfanumerico</span><span class="sxs-lookup"><span data-stu-id="1f5c6-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="1f5c6-263">Deve contenere almeno una lettera maiuscola o minuscola</span><span class="sxs-lookup"><span data-stu-id="1f5c6-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f5c6-264">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1f5c6-264">Next steps</span></span>

<span data-ttu-id="1f5c6-265">Ora che si è appreso come aggiungere risorse di archiviazione ad accesso limitato al cluster HDInsight, è possibile conoscere altri modi per usare i dati nel cluster:</span><span class="sxs-lookup"><span data-stu-id="1f5c6-265">Now that you have learned how to add limited-access storage to your HDInsight cluster, learn other ways to work with data on your cluster:</span></span>

* [<span data-ttu-id="1f5c6-266">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f5c6-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1f5c6-267">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f5c6-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="1f5c6-268">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f5c6-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
