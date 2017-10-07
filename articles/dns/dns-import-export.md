---
title: aaaImport e una zona del dominio di esportazione file tooAzure DNS mediante Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come tooimport ed esportare un DNS zone file tooAzure DNS mediante Azure CLI 1.0
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
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="22c46-103">Importare ed esportare un file di zona DNS mediante hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="22c46-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="22c46-104">In questo articolo illustra come tooimport ed esportare file di zona DNS per l'utilizzo di DNS di Azure hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="22c46-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="22c46-105">Migrazione di zona tooDNS introduzione</span><span class="sxs-lookup"><span data-stu-id="22c46-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="22c46-106">Un file di zona DNS è un file di testo che contiene i dettagli di tutti i record nella zona hello sistema DNS (Domain Name).</span><span class="sxs-lookup"><span data-stu-id="22c46-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="22c46-107">Segue un formato standard, ideale per il trasferimento dei record DNS tra sistemi DNS.</span><span class="sxs-lookup"><span data-stu-id="22c46-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="22c46-108">Utilizzando un file di zona è un veloce, affidabile e un modo pratico tootransfer una zona DNS interno o all'esterno di DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="22c46-109">DNS di Azure supporta l'importazione ed esportazione di file di zona utilizzando hello Azure interfaccia della riga di comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="22c46-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="22c46-110">Importazione di file di zona è **non** attualmente supportate tramite Azure PowerShell o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="22c46-111">Hello Azure CLI 1.0 è uno strumento da riga di comando multipiattaforma utilizzato per la gestione dei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="22c46-112">È disponibile per le piattaforme Windows, Mac e Linux hello da hello [pagina di download di Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="22c46-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="22c46-113">Supporto multipiattaforma è importante per importare ed esportare file di zona, in quanto hello Nome server del software più comuni, [ASSOCIARE](https://www.isc.org/downloads/bind/), in genere viene eseguito in Linux.</span><span class="sxs-lookup"><span data-stu-id="22c46-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="22c46-114">Esistono attualmente due versioni di hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="22c46-115">CLI1.0 è basata su Node.js e ha comandi che iniziano con "azure".</span><span class="sxs-lookup"><span data-stu-id="22c46-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="22c46-116">CLI2.0 è basata su Python e ha comandi che iniziano con "az".</span><span class="sxs-lookup"><span data-stu-id="22c46-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="22c46-117">L'importazione di file di zona è supportata in entrambe le versioni, è consigliabile utilizzare i comandi CLI1.0 hello, come descritto in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="22c46-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="22c46-118">Recupero del file di zona DNS esistente</span><span class="sxs-lookup"><span data-stu-id="22c46-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="22c46-119">Prima di importare un file di zona DNS in DNS di Azure, è necessario tooobtain una copia del file di zona hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="22c46-120">Hello origine di questo file dipende da dove zona DNS hello è attualmente ospitato.</span><span class="sxs-lookup"><span data-stu-id="22c46-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="22c46-121">Se la zona DNS è ospitata da un servizio (ad esempio un registrar, un provider di hosting DNS dedicato o provider di cloud alternativi), che il servizio deve fornire il file di zona DNS hello possibilità toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="22c46-122">Se la zona DNS è ospitata il servizio DNS di Windows, cartella di hello predefinita per i file di zona hello è **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="22c46-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="22c46-123">file di zona tooeach Hello percorso Mostra anche su hello **generale** scheda della console DNS hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="22c46-124">Se la zona DNS è ospitata usando l'associazione, percorso hello del file di zona hello per ogni zona è specificato nel file di configurazione di binding hello **named. conf**.</span><span class="sxs-lookup"><span data-stu-id="22c46-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="22c46-125">I file di zona scaricati da GoDaddy hanno un formato leggermente non standard.</span><span class="sxs-lookup"><span data-stu-id="22c46-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="22c46-126">È necessario toocorrect questo prima di importare questi file di zona DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="22c46-127">I nomi DNS in hello RDATA di ogni record DNS vengono specificati come nomi completi, ma che non dispongono di una terminazione "." Ciò significa che vengono interpretati da altri sistemi DNS come nomi relativi.</span><span class="sxs-lookup"><span data-stu-id="22c46-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="22c46-128">È necessario tooedit hello zona file tooappend hello terminazione "." tootheir nomi prima di importarli in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="22c46-129">Ad esempio, è necessario modificato troppo record CNAME "www 3600 IN contoso.com CNAME" hello "www 3600 CNAME IN contoso.com."</span><span class="sxs-lookup"><span data-stu-id="22c46-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="22c46-130">con un "." alla fine.</span><span class="sxs-lookup"><span data-stu-id="22c46-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="22c46-131">Importare un file di zona DNS in DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="22c46-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="22c46-132">L'importazione di un file di zona crea una nuova zona in DNS di Azure se non ne esiste già una.</span><span class="sxs-lookup"><span data-stu-id="22c46-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="22c46-133">Se esiste già una zona hello, hello set di record nel file di zona hello devono essere uniti con i set di record esistenti hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="22c46-134">Unione</span><span class="sxs-lookup"><span data-stu-id="22c46-134">Merge behavior</span></span>

* <span data-ttu-id="22c46-135">Per impostazione predefinita, i set di record nuovi ed esistenti vengono uniti.</span><span class="sxs-lookup"><span data-stu-id="22c46-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="22c46-136">I record identici all'interno di un set di record unito vengono deduplicati.</span><span class="sxs-lookup"><span data-stu-id="22c46-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="22c46-137">In alternativa, specificando hello `--force` opzione, hello sostituisce processo di importazione il set di record esistente con nuovi set di record.</span><span class="sxs-lookup"><span data-stu-id="22c46-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="22c46-138">I set di record esistenti che non dispone di un record corrispondente impostato nel file di zona importati hello vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="22c46-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="22c46-139">Durante l'unione di set di record, hello toolive TTL (time) preesistenti di set di record è utilizzato.</span><span class="sxs-lookup"><span data-stu-id="22c46-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="22c46-140">Quando `--force` è utilizzato, hello durata (TTL) del set di record nuovo hello viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="22c46-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="22c46-141">Avvio di parametri di autorità (SOA) (ad eccezione di `host`) vengono sempre ricavate dal file di zona importati hello, indipendentemente dal fatto che `--force` viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="22c46-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="22c46-142">Analogamente, per impostare al vertice zona hello record hello del server, hello TTL viene sempre acquisito dal file di zona importati hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="22c46-143">Un record CNAME importato non sostituisce un CNAME esistente registrare con stesso nome a meno che non hello hello `--force` parametro specificato.</span><span class="sxs-lookup"><span data-stu-id="22c46-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="22c46-144">Quando si verifica un conflitto tra un record CNAME e un altro record di hello stesso nome ma è diversa, digitare (indipendentemente dal fatto che è esistente o nuova), record esistente hello viene mantenuto.</span><span class="sxs-lookup"><span data-stu-id="22c46-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="22c46-145">Si tratta indipendentemente dall'utilizzo di hello di `--force`.</span><span class="sxs-lookup"><span data-stu-id="22c46-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="22c46-146">Altre informazioni sull'importazione</span><span class="sxs-lookup"><span data-stu-id="22c46-146">Additional information about importing</span></span>

<span data-ttu-id="22c46-147">Hello note seguenti forniscono altri dettagli tecnici sulla zona hello processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="22c46-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="22c46-148">Hello `$TTL` direttiva è facoltativa ed è supportata.</span><span class="sxs-lookup"><span data-stu-id="22c46-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="22c46-149">Se non si `$TTL` direttiva viene specificata, vengono importati i record senza una durata (TTL) esplicita impostare tooa TTL predefinito di 3600 secondi.</span><span class="sxs-lookup"><span data-stu-id="22c46-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="22c46-150">Quando due record in stesso set di record hello specificano TTLs diversi, valore inferiore hello viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="22c46-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="22c46-151">Hello `$ORIGIN` direttiva è facoltativa ed è supportata.</span><span class="sxs-lookup"><span data-stu-id="22c46-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="22c46-152">Se non si `$ORIGIN` è impostata, predefinito hello valore utilizzato è il nome zona hello come specificato nella riga di comando hello (più terminazione hello ".").</span><span class="sxs-lookup"><span data-stu-id="22c46-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="22c46-153">Hello `$INCLUDE` e `$GENERATE` direttive non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="22c46-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="22c46-154">Sono supportati questi tipi di record: A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.</span><span class="sxs-lookup"><span data-stu-id="22c46-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="22c46-155">Hello record SOA viene creato automaticamente da DNS di Azure quando viene creata una zona.</span><span class="sxs-lookup"><span data-stu-id="22c46-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="22c46-156">Quando si importa un file di zona, tutti i parametri SOA vengono estratti dal file di zona hello *tranne* hello `host` parametro.</span><span class="sxs-lookup"><span data-stu-id="22c46-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="22c46-157">Questo parametro utilizza il valore di hello fornito dal servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="22c46-158">Questo avviene perché questo parametro deve fare riferimento a server dei nomi primario toohello fornite da DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="22c46-159">record server dei nomi Hello impostato al vertice zona hello viene anche creato automaticamente da DNS di Azure quando si crea la zona hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="22c46-160">Solo hello durata (TTL) di questo set di record viene importato.</span><span class="sxs-lookup"><span data-stu-id="22c46-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="22c46-161">Questi record contengono nomi di server di nome hello forniti da DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="22c46-162">dati del record di Hello non viene sovrascritto da valori hello contenuti nel file di zona importati hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="22c46-163">Durante l'anteprima pubblica, DNS di Azure supporta solo i record TXT a stringa singola.</span><span class="sxs-lookup"><span data-stu-id="22c46-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="22c46-164">Multistringa record TXT sono essere troncati e concatenati too255 caratteri.</span><span class="sxs-lookup"><span data-stu-id="22c46-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="22c46-165">Valori e formato dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="22c46-165">CLI format and values</span></span>

<span data-ttu-id="22c46-166">formato Hello di hello Azure CLI comando tooimport una zona DNS è:</span><span class="sxs-lookup"><span data-stu-id="22c46-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="22c46-167">Valori:</span><span class="sxs-lookup"><span data-stu-id="22c46-167">Values:</span></span>

* <span data-ttu-id="22c46-168">`<resource group>`è il nome di hello hello del gruppo di risorse per la zona hello in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="22c46-169">`<zone name>`è il nome di hello della zona di hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="22c46-170">`<zone file name>`è hello/nome del percorso toobe file di zona hello importati.</span><span class="sxs-lookup"><span data-stu-id="22c46-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="22c46-171">Se una zona con questo nome non esiste nel gruppo di risorse hello, viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="22c46-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="22c46-172">Se hello zona esiste già, hello set di record importati vengono unite con i set di record esistenti.</span><span class="sxs-lookup"><span data-stu-id="22c46-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="22c46-173">toooverwrite hello esistente set di record, utilizzare hello `--force` opzione.</span><span class="sxs-lookup"><span data-stu-id="22c46-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="22c46-174">formato di hello tooverify di un file di zona senza effettivamente l'importazione, utilizzare hello `--parse-only` opzione.</span><span class="sxs-lookup"><span data-stu-id="22c46-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="22c46-175">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="22c46-175">Step 1.</span></span> <span data-ttu-id="22c46-176">Importare un file di zona</span><span class="sxs-lookup"><span data-stu-id="22c46-176">Import a zone file</span></span>

<span data-ttu-id="22c46-177">un file di zona per la zona hello tooimport **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="22c46-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="22c46-178">Accedi tooyour sottoscrizione di Azure mediante Azure CLI 1.0 hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="22c46-179">Selezionare la sottoscrizione di hello in cui si desidera toocreate la nuova zona DNS.</span><span class="sxs-lookup"><span data-stu-id="22c46-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="22c46-180">DNS di Azure è un servizio di gestione risorse di sola Azure, pertanto hello CLI di Azure deve essere disattivati tooResource modalità di gestione.</span><span class="sxs-lookup"><span data-stu-id="22c46-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="22c46-181">Prima di utilizzare il servizio di DNS di Azure hello, è necessario registrare il provider di risorse di sottoscrizione toouse hello Network.</span><span class="sxs-lookup"><span data-stu-id="22c46-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="22c46-182">Questa operazione viene eseguita una sola volta per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="22c46-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="22c46-183">Se si non è ancora disponibile, è necessario anche toocreate un gruppo di risorse di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="22c46-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="22c46-184">zona hello tooimport **contoso.com** dal file hello **contoso.com.txt** in una nuova zona DNS in gruppo di risorse hello **myresourcegroup**, eseguire il comando hello `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="22c46-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="22c46-185">Questo comando consente di caricare il file di zona hello e analizzarlo.</span><span class="sxs-lookup"><span data-stu-id="22c46-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="22c46-186">comando Hello esegue una serie di comandi nel hello Azure servizio toocreate hello zona e i set di tutti i record di hello nella zona hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="22c46-187">comando Hello segnala lo stato nella finestra di console hello, insieme a eventuali errori o avvisi.</span><span class="sxs-lookup"><span data-stu-id="22c46-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="22c46-188">Poiché set di record vengono creati in serie, potrebbe richiedere alcuni minuti tooimport un file di zona di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="22c46-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="22c46-189">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="22c46-189">Step 2.</span></span> <span data-ttu-id="22c46-190">Verificare la zona hello</span><span class="sxs-lookup"><span data-stu-id="22c46-190">Verify hello zone</span></span>

<span data-ttu-id="22c46-191">tooverify hello zona DNS dopo aver importato il file hello, è possibile utilizzare uno qualsiasi dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="22c46-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="22c46-192">È possibile elencare i record di hello hello comando CLI di Azure seguente:</span><span class="sxs-lookup"><span data-stu-id="22c46-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="22c46-193">È possibile elencare i record di hello tramite i cmdlet di PowerShell hello `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="22c46-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="22c46-194">È possibile utilizzare `nslookup` tooverify risoluzione dei nomi per i record di hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="22c46-195">Poiché la zona hello non delegata ancora, è necessario toospecify hello corretto Azure server dei nomi DNS in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="22c46-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="22c46-196">Hello esempio seguente viene illustrato come nomi di server di nome hello tooretrieve assegnati toohello zona.</span><span class="sxs-lookup"><span data-stu-id="22c46-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="22c46-197">IT illustra anche come tooquery hello "www" registrare tramite `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="22c46-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
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

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="22c46-198">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="22c46-198">Step 3.</span></span> <span data-ttu-id="22c46-199">Aggiornare la delega DNS</span><span class="sxs-lookup"><span data-stu-id="22c46-199">Update DNS delegation</span></span>

<span data-ttu-id="22c46-200">Dopo aver verificato che la zona hello è stata importata correttamente, è necessario tooupdate hello DNS delega toopoint toohello server dei nomi DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="22c46-201">Per ulteriori informazioni, vedere l'articolo hello [Aggiorna delega DNS hello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="22c46-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="22c46-202">Esportare un file di zona DNS da DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="22c46-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="22c46-203">formato Hello di hello Azure CLI comando tooimport una zona DNS è:</span><span class="sxs-lookup"><span data-stu-id="22c46-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="22c46-204">Valori:</span><span class="sxs-lookup"><span data-stu-id="22c46-204">Values:</span></span>

* <span data-ttu-id="22c46-205">`<resource group>`è il nome di hello hello del gruppo di risorse per la zona hello in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="22c46-206">`<zone name>`è il nome di hello della zona di hello.</span><span class="sxs-lookup"><span data-stu-id="22c46-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="22c46-207">`<zone file name>`è hello/nome del percorso toobe file di zona hello esportata.</span><span class="sxs-lookup"><span data-stu-id="22c46-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="22c46-208">Come con l'importazione di zona hello, è innanzitutto necessario toosign in, scegliere la sottoscrizione e configurare la modalità di gestione risorse di hello Azure CLI toouse.</span><span class="sxs-lookup"><span data-stu-id="22c46-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="22c46-209">tooexport un file di zona</span><span class="sxs-lookup"><span data-stu-id="22c46-209">tooexport a zone file</span></span>

1. <span data-ttu-id="22c46-210">Accedi tooyour sottoscrizione di Azure tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="22c46-211">Selezionare la sottoscrizione di hello in cui si desidera toocreate la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="22c46-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="22c46-212">DNS di Azure è un servizio solo di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c46-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="22c46-213">Hello CLI di Azure deve essere disattivati tooResource modalità di gestione.</span><span class="sxs-lookup"><span data-stu-id="22c46-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="22c46-214">zona DNS di Azure esistente di hello tooexport **contoso.com** nel gruppo di risorse **myresourcegroup** toohello file **contoso.com.txt** (in hello cartella corrente), eseguire `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="22c46-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="22c46-215">Questo comando chiama hello tooenumerate servizio DNS di Azure set di record nella zona hello ed esportare file di zona hello risultati tooa compatibile con associazione.</span><span class="sxs-lookup"><span data-stu-id="22c46-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
