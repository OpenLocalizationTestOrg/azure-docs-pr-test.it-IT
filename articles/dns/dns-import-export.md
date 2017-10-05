---
title: Importare ed esportare un file di zona del dominio in DNS di Azure usando l'interfaccia della riga di comando di Azure 1.0 | Microsoft Docs
description: Informazioni su come importare ed esportare un file di zona DNS in DNS di Azure usando l'interfaccia della riga di comando di Azure 1.0
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: d6d3fa7aa0e8b2462b3a6b4b66d3d87ab5535314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli-10"></a><span data-ttu-id="b6a47-103">Importare ed esportare un file di zona DNS usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b6a47-103">Import and export a DNS zone file using the Azure CLI 1.0</span></span> 

<span data-ttu-id="b6a47-104">Questo articolo spiega come importare ed esportare file di zona DNS per Azure DNS usando l'interfaccia della riga di comando di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="b6a47-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 1.0.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="b6a47-105">Introduzione alla migrazione di zone DNS</span><span class="sxs-lookup"><span data-stu-id="b6a47-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="b6a47-106">Un file di zona DNS è un file di testo che contiene i dettagli di tutti i record DNS (Domain Name System) nella zona.</span><span class="sxs-lookup"><span data-stu-id="b6a47-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="b6a47-107">Segue un formato standard, ideale per il trasferimento dei record DNS tra sistemi DNS.</span><span class="sxs-lookup"><span data-stu-id="b6a47-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="b6a47-108">L'uso di un file di zona è un modo rapido, affidabile e pratico per trasferire una zona DNS all'interno o all'esterno di DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="b6a47-109">DNS di Azure supporta l'importazione e l'esportazione di file di zona tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="b6a47-110">L'importazione di file di zona **non** è attualmente supportata tramite Azure PowerShell o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="b6a47-111">L'interfaccia della riga di comando di Azure 1.0 è uno strumento a riga di comando multipiattaforma usato per la gestione di servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-111">The Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="b6a47-112">È disponibile per le piattaforme Windows, Mac e Linux nella [pagina di download di Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b6a47-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="b6a47-113">Il supporto multipiattaforma è importante per importare ed esportare i file di zona, perché il software server più conosciuto, [BIND](https://www.isc.org/downloads/bind/), viene generalmente eseguito in Linux.</span><span class="sxs-lookup"><span data-stu-id="b6a47-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="b6a47-114">Esistono attualmente due versioni dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-114">There are currently two versions of the Azure CLI.</span></span> <span data-ttu-id="b6a47-115">CLI1.0 è basata su Node.js e ha comandi che iniziano con "azure".</span><span class="sxs-lookup"><span data-stu-id="b6a47-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="b6a47-116">CLI2.0 è basata su Python e ha comandi che iniziano con "az".</span><span class="sxs-lookup"><span data-stu-id="b6a47-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="b6a47-117">Nonostante l'importazione dei file di zona sia supportata in entrambe le versioni, è consigliabile usare i comandi CLI1.0, come descritto in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="b6a47-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="b6a47-118">Recupero del file di zona DNS esistente</span><span class="sxs-lookup"><span data-stu-id="b6a47-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="b6a47-119">Prima di importare un file di zona DNS in DNS di Azure, è necessario ottenere una copia del file di zona.</span><span class="sxs-lookup"><span data-stu-id="b6a47-119">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span></span> <span data-ttu-id="b6a47-120">L'origine di questo file dipende da dove è attualmente ospitata la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b6a47-120">The source of this file depends on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="b6a47-121">Se la zona DNS è ospitata da un servizio partner, ad esempio un registrar, un provider di servizi di hosting DNS dedicato o un provider di servizi cloud alternativo, tale servizio deve fornire la possibilità di scaricare il file di zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b6a47-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="b6a47-122">Se la zona DNS è ospitata nel DNS di Windows, la cartella predefinita per i file di zona è **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="b6a47-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="b6a47-123">Il percorso completo di ogni file di zona viene visualizzato anche nella scheda **Generale** della console DNS.</span><span class="sxs-lookup"><span data-stu-id="b6a47-123">The full path to each zone file also shows on the **General** tab of the DNS console.</span></span>
* <span data-ttu-id="b6a47-124">Se la zona DNS è ospitata con BIND, il percorso del file di zona per ogni zona è specificato nel file di configurazione di BIND **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="b6a47-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="b6a47-125">I file di zona scaricati da GoDaddy hanno un formato leggermente non standard.</span><span class="sxs-lookup"><span data-stu-id="b6a47-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="b6a47-126">È necessario correggerlo prima di importare questi file di zona in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-126">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="b6a47-127">I nomi DNS in RDATA di ogni record DNS sono specificati come nomi completi, ma non hanno un "." alla fine. Ciò significa che vengono interpretati da altri sistemi DNS come nomi relativi.</span><span class="sxs-lookup"><span data-stu-id="b6a47-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="b6a47-128">È necessario modificare il file di zona aggiungendo il '.' di terminazione ai relativi nomi prima di importarli in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="b6a47-129">Ad esempio, il record CNAME "www 3600 IN CNAME contoso.com" deve essere modificato in "www 3600 IN CNAME contoso.com."</span><span class="sxs-lookup"><span data-stu-id="b6a47-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="b6a47-130">con un "." alla fine.</span><span class="sxs-lookup"><span data-stu-id="b6a47-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="b6a47-131">Importare un file di zona DNS in DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="b6a47-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="b6a47-132">L'importazione di un file di zona crea una nuova zona in DNS di Azure se non ne esiste già una.</span><span class="sxs-lookup"><span data-stu-id="b6a47-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="b6a47-133">Se la zona esiste già, i set di record nel file di zona devono essere uniti a quelli esistenti.</span><span class="sxs-lookup"><span data-stu-id="b6a47-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="b6a47-134">Unione</span><span class="sxs-lookup"><span data-stu-id="b6a47-134">Merge behavior</span></span>

* <span data-ttu-id="b6a47-135">Per impostazione predefinita, i set di record nuovi ed esistenti vengono uniti.</span><span class="sxs-lookup"><span data-stu-id="b6a47-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="b6a47-136">I record identici all'interno di un set di record unito vengono deduplicati.</span><span class="sxs-lookup"><span data-stu-id="b6a47-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="b6a47-137">In alternativa, se si specifica l'opzione `--force`, il processo di importazione sostituisce i set di record esistenti con quelli nuovi.</span><span class="sxs-lookup"><span data-stu-id="b6a47-137">Alternatively, by specifying the `--force` option, the import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="b6a47-138">I set di record esistenti che non hanno un set di record corrispondente nel file di zona importato non devono essere rimossi.</span><span class="sxs-lookup"><span data-stu-id="b6a47-138">Existing record sets that do not have a corresponding record set in the imported zone file are not be removed.</span></span>
* <span data-ttu-id="b6a47-139">Quando i set di record sono uniti, viene usato il valore di durata (TTL) dei set di record preesistenti.</span><span class="sxs-lookup"><span data-stu-id="b6a47-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="b6a47-140">Se si usa `--force`, viene applicato il valore TTL del nuovo set di record.</span><span class="sxs-lookup"><span data-stu-id="b6a47-140">When `--force` is used, the TTL of the new record set is used.</span></span>
* <span data-ttu-id="b6a47-141">I parametri di origine di autorità (SOA), tranne `host`, vengono sempre rilevati dal file di zona importato, indipendentemente dall'uso di `--force`.</span><span class="sxs-lookup"><span data-stu-id="b6a47-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="b6a47-142">Analogamente, per il set di record del server di nomi al vertice della zona viene sempre applicato il valore TTL dal file di zona importato.</span><span class="sxs-lookup"><span data-stu-id="b6a47-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="b6a47-143">Un record CNAME importato non sostituisce un record CNAME esistente con lo stesso nome, a meno che non sia stato specificato il parametro `--force`.</span><span class="sxs-lookup"><span data-stu-id="b6a47-143">An imported CNAME record does not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span></span>
* <span data-ttu-id="b6a47-144">Quando si verifica un conflitto tra un record CNAME e a un altro record con lo stesso nome, ma di tipo diverso, indipendentemente dal fatto che sia nuovo o esistente viene mantenuto il record esistente.</span><span class="sxs-lookup"><span data-stu-id="b6a47-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> <span data-ttu-id="b6a47-145">È indipendente dall'uso di `--force`.</span><span class="sxs-lookup"><span data-stu-id="b6a47-145">This is independent of the use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="b6a47-146">Altre informazioni sull'importazione</span><span class="sxs-lookup"><span data-stu-id="b6a47-146">Additional information about importing</span></span>

<span data-ttu-id="b6a47-147">Le note seguenti forniscono altri dettagli tecnici sul processo di importazione di zone.</span><span class="sxs-lookup"><span data-stu-id="b6a47-147">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="b6a47-148">La direttiva `$TTL` è facoltativa e supportata.</span><span class="sxs-lookup"><span data-stu-id="b6a47-148">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="b6a47-149">Se non si specifica una direttiva `$TTL`, i record senza una TTL esplicita vengono importati e impostati su una TLL predefinita di 3600 secondi.</span><span class="sxs-lookup"><span data-stu-id="b6a47-149">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="b6a47-150">Quando per due record nello stesso set di record sono specificati TTL diversi, viene usato il valore più basso.</span><span class="sxs-lookup"><span data-stu-id="b6a47-150">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="b6a47-151">La direttiva `$ORIGIN` è facoltativa e supportata.</span><span class="sxs-lookup"><span data-stu-id="b6a47-151">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="b6a47-152">Se `$ORIGIN` non è impostata, il valore predefinito usato è il nome della zona specificato nella riga di comando, con "." di terminazione.</span><span class="sxs-lookup"><span data-stu-id="b6a47-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="b6a47-153">Le direttive `$INCLUDE` e `$GENERATE` non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="b6a47-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="b6a47-154">Sono supportati questi tipi di record: A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.</span><span class="sxs-lookup"><span data-stu-id="b6a47-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="b6a47-155">Il record SOA viene creato automaticamente da DNS di Azure quando si crea una zona.</span><span class="sxs-lookup"><span data-stu-id="b6a47-155">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="b6a47-156">Quando si importa un file di zona, tutti i parametri SOA vengono rilevati dal file di zona *tranne* il parametro `host`.</span><span class="sxs-lookup"><span data-stu-id="b6a47-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="b6a47-157">Questo parametro usa il valore fornito da DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-157">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="b6a47-158">Questo parametro deve infatti fare riferimento al server dei nomi primario fornito da DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="b6a47-159">Anche il set di record del server dei nomi al vertice della zona viene creato automaticamente da DNS di Azure quando si crea la zona.</span><span class="sxs-lookup"><span data-stu-id="b6a47-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="b6a47-160">Viene importata solo la durata TTL di questo set di record.</span><span class="sxs-lookup"><span data-stu-id="b6a47-160">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="b6a47-161">Questi record contengono i nomi dei server dei nomi forniti da DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-161">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="b6a47-162">I dati dei record non vengono sovrascritti dai valori contenuti nel file di zona importato.</span><span class="sxs-lookup"><span data-stu-id="b6a47-162">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="b6a47-163">Durante l'anteprima pubblica, DNS di Azure supporta solo i record TXT a stringa singola.</span><span class="sxs-lookup"><span data-stu-id="b6a47-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="b6a47-164">I record TXT multistringa vengono concatenati e troncati a 255 caratteri.</span><span class="sxs-lookup"><span data-stu-id="b6a47-164">Multistring TXT records are be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="b6a47-165">Valori e formato dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="b6a47-165">CLI format and values</span></span>

<span data-ttu-id="b6a47-166">Il formato del comando dell'interfaccia della riga di comando di Azure per importare una zona DNS è:</span><span class="sxs-lookup"><span data-stu-id="b6a47-166">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="b6a47-167">Valori:</span><span class="sxs-lookup"><span data-stu-id="b6a47-167">Values:</span></span>

* <span data-ttu-id="b6a47-168">`<resource group>` è il nome del gruppo di risorse per la zona in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="b6a47-169">`<zone name>` è il nome della zona.</span><span class="sxs-lookup"><span data-stu-id="b6a47-169">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="b6a47-170">`<zone file name>` è il nome/percorso del file di zona da importare.</span><span class="sxs-lookup"><span data-stu-id="b6a47-170">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="b6a47-171">Se una zona con questo nome non esiste nel gruppo di risorse, viene creata.</span><span class="sxs-lookup"><span data-stu-id="b6a47-171">If a zone with this name does not exist in the resource group, it is created for you.</span></span> <span data-ttu-id="b6a47-172">Se la zona esiste già, i set di record importati vengono uniti con quelli esistenti.</span><span class="sxs-lookup"><span data-stu-id="b6a47-172">If the zone already exists, the imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="b6a47-173">Per sovrascrivere i set di record esistenti, usare l'opzione `--force` .</span><span class="sxs-lookup"><span data-stu-id="b6a47-173">To overwrite the existing record sets, use the `--force` option.</span></span>

<span data-ttu-id="b6a47-174">Per verificare il formato di un file di zona senza eseguirne effettivamente l'importazione, usare l'opzione `--parse-only` .</span><span class="sxs-lookup"><span data-stu-id="b6a47-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="b6a47-175">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="b6a47-175">Step 1.</span></span> <span data-ttu-id="b6a47-176">Importare un file di zona</span><span class="sxs-lookup"><span data-stu-id="b6a47-176">Import a zone file</span></span>

<span data-ttu-id="b6a47-177">Per importare un file di zona per la zona **contoso.com**:</span><span class="sxs-lookup"><span data-stu-id="b6a47-177">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="b6a47-178">Accedere alla sottoscrizione di Azure usando l'interfaccia della riga di comando di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="b6a47-178">Sign in to your Azure subscription by using the Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="b6a47-179">Selezionare la sottoscrizione in cui si vuole creare la nuova zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b6a47-179">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="b6a47-180">DNS di Azure è un servizio solo di Gestione risorse di Azure, quindi nell'interfaccia della riga di comando di Azure deve essere impostata la modalità Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="b6a47-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="b6a47-181">Prima di usare il servizio DNS di Azure, è necessario registrare la sottoscrizione per l'uso del provider di risorse Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="b6a47-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span></span> <span data-ttu-id="b6a47-182">Questa operazione viene eseguita una sola volta per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b6a47-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="b6a47-183">È anche necessario creare un gruppo di risorse di Resource Manager, se non ne è già disponibile uno.</span><span class="sxs-lookup"><span data-stu-id="b6a47-183">If you don't have one already, you also need to create a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="b6a47-184">Per importare la zona **contoso.com** dal file **contoso.com.txt** in una nuova zona DNS nel gruppo di risorse **myresourcegroup**, eseguire il comando `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="b6a47-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span></span><BR><span data-ttu-id="b6a47-185">Questo comando carica il file di zona e lo analizza.</span><span class="sxs-lookup"><span data-stu-id="b6a47-185">This command loads the zone file and parse it.</span></span> <span data-ttu-id="b6a47-186">Il comando esegue una serie di comandi nel servizio DNS di Azure per creare la zona e tutti i set di record nella zona.</span><span class="sxs-lookup"><span data-stu-id="b6a47-186">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span></span> <span data-ttu-id="b6a47-187">Il comando visualizza l'avanzamento nella finestra della console insieme agli errori o agli avvisi.</span><span class="sxs-lookup"><span data-stu-id="b6a47-187">The command reports progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="b6a47-188">Poiché i set di record vengono creati in serie, l'importazione di un file di zona di grandi dimensioni può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="b6a47-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="b6a47-189">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="b6a47-189">Step 2.</span></span> <span data-ttu-id="b6a47-190">Verificare la zona</span><span class="sxs-lookup"><span data-stu-id="b6a47-190">Verify the zone</span></span>

<span data-ttu-id="b6a47-191">Per verificare la zona DNS dopo aver importato il file, è possibile usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6a47-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="b6a47-192">È possibile elencare i record usando il seguente comando dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="b6a47-192">You can list the records by using the following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="b6a47-193">È possibile elencare i record usando il cmdlet PowerShell `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="b6a47-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="b6a47-194">Per verificare la risoluzione dei nomi per i record, è possibile usare `nslookup` .</span><span class="sxs-lookup"><span data-stu-id="b6a47-194">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="b6a47-195">Poiché la zona non è ancora stata delegata, è necessario specificare esplicitamente i server dei nomi DNS di Azure corretti.</span><span class="sxs-lookup"><span data-stu-id="b6a47-195">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="b6a47-196">Il seguente esempio mostra come recuperare i nomi dei server dei nomi assegnati alla zona.</span><span class="sxs-lookup"><span data-stu-id="b6a47-196">The following sample shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="b6a47-197">Illustra anche come eseguire una query sul record "www" con `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="b6a47-197">IT also shows how to query the "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up the DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="b6a47-198">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="b6a47-198">Step 3.</span></span> <span data-ttu-id="b6a47-199">Aggiornare la delega DNS</span><span class="sxs-lookup"><span data-stu-id="b6a47-199">Update DNS delegation</span></span>

<span data-ttu-id="b6a47-200">Dopo aver verificato che la zona è stata importata correttamente, è necessario aggiornare la delega DNS in modo che punti verso i server dei nomi DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-200">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="b6a47-201">Per altre informazioni, vedere l'articolo [Aggiornare la delega DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="b6a47-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="b6a47-202">Esportare un file di zona DNS da DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="b6a47-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="b6a47-203">Il formato del comando dell'interfaccia della riga di comando di Azure per importare una zona DNS è:</span><span class="sxs-lookup"><span data-stu-id="b6a47-203">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="b6a47-204">Valori:</span><span class="sxs-lookup"><span data-stu-id="b6a47-204">Values:</span></span>

* <span data-ttu-id="b6a47-205">`<resource group>` è il nome del gruppo di risorse per la zona in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="b6a47-206">`<zone name>` è il nome della zona.</span><span class="sxs-lookup"><span data-stu-id="b6a47-206">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="b6a47-207">`<zone file name>` è il nome/percorso del file di zona da esportare.</span><span class="sxs-lookup"><span data-stu-id="b6a47-207">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="b6a47-208">Come per l'importazione di una zona, è necessario prima di tutto accedere, scegliere la sottoscrizione e configurare l'interfaccia della riga di comando di Azure per l'uso della modalità Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b6a47-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="b6a47-209">Per esportare un file di zona:</span><span class="sxs-lookup"><span data-stu-id="b6a47-209">To export a zone file</span></span>

1. <span data-ttu-id="b6a47-210">Accedere alla sottoscrizione di Azure con l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-210">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="b6a47-211">Selezionare la sottoscrizione in cui creare la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b6a47-211">Select the subscription where you want to create your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="b6a47-212">DNS di Azure è un servizio solo di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a47-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="b6a47-213">L'interfaccia della riga di comando di Azure deve essere impostata sulla modalità Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="b6a47-213">The Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="b6a47-214">Per esportare la zona **contoso.com** di DNS di Azure esistente nel gruppo di risorse **myresourcegroup** nel file **contoso.com.txt** nella cartella corrente, eseguire `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="b6a47-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="b6a47-215">Questo comando chiama il servizio DNS di Azure per enumerare i set di record nella zona ed esportare i risultati in un file di zona compatibile con BIND.</span><span class="sxs-lookup"><span data-stu-id="b6a47-215">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
