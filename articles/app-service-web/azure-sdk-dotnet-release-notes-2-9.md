---
title: note sulla versione 2.9 di .NET SDK per aaaAzure
description: Note sulla versione di Azure SDK per .NET 2.9
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="c44c9-103">Note sulla versione di Azure SDK per .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="c44c9-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="c44c9-104">Questo argomento contiene le note sulle versioni 2.9 e 2.9.6 di Azure SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="c44c9-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="c44c9-105">Riepilogo sulla versione Azure SDK per .NET 2.9.6</span><span class="sxs-lookup"><span data-stu-id="c44c9-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="c44c9-106">Data di rilascio: 16/11/2016</span><span class="sxs-lookup"><span data-stu-id="c44c9-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="c44c9-107">Non toohello modifiche di rilievo in Azure SDK 2.9 sono state introdotte in questa versione.</span><span class="sxs-lookup"><span data-stu-id="c44c9-107">No breaking changes toohello Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="c44c9-108">Non è inoltre alcun tooleverage del processo di aggiornamento necessita questo SDK con i progetti servizio Cloud esistenti.</span><span class="sxs-lookup"><span data-stu-id="c44c9-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="c44c9-109">Visual Studio 2017 Release Candidate</span><span class="sxs-lookup"><span data-stu-id="c44c9-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="c44c9-110">In Visual Studio RC 2017, questa versione di hello Azure SDK per .NET è incorporata in hello del carico di lavoro di Azure.</span><span class="sxs-lookup"><span data-stu-id="c44c9-110">In Visual Studio 2017 RC, this release of hello Azure SDK for .NET is built in in hello Azure Workload.</span></span> <span data-ttu-id="c44c9-111">Tutti gli strumenti di hello è necessario lo sviluppo di Azure toodo faranno parte di Visual Studio 2017 RC in futuro.</span><span class="sxs-lookup"><span data-stu-id="c44c9-111">All hello tools you need toodo Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="c44c9-112">Per Visual Studio 2015 e Visual Studio 2013, hello SDK sarà comunque disponibile tramite WebPI.</span><span class="sxs-lookup"><span data-stu-id="c44c9-112">For Visual Studio 2015 and Visual Studio 2013, hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="c44c9-113">Le versioni per Visual Studio 2013 di Azure SDK per .NET verranno sospese quando Visual Studio 2017 verrà rilasciato come prodotto finale.</span><span class="sxs-lookup"><span data-stu-id="c44c9-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="c44c9-114">Seguire questa toodownload collegamento Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="c44c9-114">Follow this link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="c44c9-115">Diagnostica Azure</span><span class="sxs-lookup"><span data-stu-id="c44c9-115">Azure Diagnostics</span></span>

- <span data-ttu-id="c44c9-116">Tooonly comportamento modificato hello archiviare una stringa di connessione parziale con chiave hello sostituito da un token di stringa di connessione di archiviazione di diagnostica servizi Cloud.</span><span class="sxs-lookup"><span data-stu-id="c44c9-116">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="c44c9-117">chiave di archiviazione effettivo Hello è ora archiviata nella cartella del profilo utente hello quindi può essere controllato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c44c9-117">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="c44c9-118">Visual Studio verrà letta la chiave di archiviazione hello dalla cartella del profilo utente per il debug locale e il processo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="c44c9-118">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="c44c9-119">Modifica di risposta toohello descritto in precedenza, Visual Studio Online team hello avanzato modello di attività di distribuzione di servizi Cloud di Azure pertanto gli utenti è possibile specificare la chiave di archiviazione hello per impostare l'estensione di diagnostica quando si pubblicano tooAzure nell'integrazione continua e la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c44c9-119">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="c44c9-120">Abbiamo apportato la stringa di connessione protetta toostore possibili e per diagnostica Azure (WAD), risolvere i problemi di configurazione tra environements toohelp la suddivisione in token.</span><span class="sxs-lookup"><span data-stu-id="c44c9-120">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="c44c9-121">Macchine virtuali Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c44c9-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="c44c9-122">Visual Studio supporta ora la distribuzione tooOS servizi Cloud macchine virtuali famiglia 5 (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="c44c9-122">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="c44c9-123">Per i servizi cloud esistenti, è possibile modificare le impostazioni tootarget hello nuova famiglia di sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="c44c9-123">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="c44c9-124">Quando si creano nuovi servizi cloud, se si sceglie il servizio di hello toocreate usando .net 4.6 o successiva, esso verrà aperto hello servizio toouse 5 famiglia del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c44c9-124">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="c44c9-125">Per ulteriori informazioni, è possibile esaminare hello [famiglia di sistemi operativi Guest supportano tabella](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="c44c9-125">For more information, you can review hello [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c44c9-126">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="c44c9-126">Known issues</span></span>

- <span data-ttu-id="c44c9-127">Azure .NET SDK 2.9.6 è stata introdotta una restrizione che blocca la distribuzione di progetti non supportati .NET Framework (ad esempio .NET 4.6) tooany famiglia di sistemi operativi utilizzando < 5.</span><span class="sxs-lookup"><span data-stu-id="c44c9-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) tooany OS Family < 5.</span></span> <span data-ttu-id="c44c9-128">Una soluzione alternativa viene fornita [qui](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="c44c9-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="c44c9-129">Cache nel ruolo di Azure</span><span class="sxs-lookup"><span data-stu-id="c44c9-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="c44c9-130">Il supporto per Cache nel ruolo di Azure termina il 30 novembre 2016.</span><span class="sxs-lookup"><span data-stu-id="c44c9-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="c44c9-131">Per altri dettagli, fare clic [qui](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="c44c9-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="c44c9-132">Modelli di Azure Resource Manager per Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c44c9-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="c44c9-133">Azure Stack è stato introdotto come destinazione di distribuzione per i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c44c9-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="c44c9-134">Riepilogo su Azure SDK per .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="c44c9-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="c44c9-135">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c44c9-135">Overview</span></span>
<span data-ttu-id="c44c9-136">Questo documento contiene le note sulla versione di hello per hello Azure SDK versione 2.9 .NET.</span><span class="sxs-lookup"><span data-stu-id="c44c9-136">This document contains hello release notes for hello Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="c44c9-137">Per informazioni dettagliate sugli aggiornamenti in questa versione, vedere hello [post annuncio di Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="c44c9-137">For detailed information about updates in this release, see hello [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="c44c9-138">Anteprima di Azure SDK 2.9 per Visual Studio 2015 Update 2 e Visual Studio "15"</span><span class="sxs-lookup"><span data-stu-id="c44c9-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="c44c9-139">Questo aggiornamento include hello seguenti correzioni di bug:</span><span class="sxs-lookup"><span data-stu-id="c44c9-139">This update includes hello following bug fixes:</span></span>

* <span data-ttu-id="c44c9-140">Problema correlato tooREST API Client generazione nella cui stringa hello "Tipo sconosciuto" venisse visualizzato come nome di hello della cartella di generazione di codice hello e/o nome hello dello spazio dei nomi hello rilasciati nel codice hello generato.</span><span class="sxs-lookup"><span data-stu-id="c44c9-140">Issue related tooREST API Client Generation in in which hello string "Unknown Type” would appear as hello name of hello code-gen folder and/or hello name of hello namespace dropped into hello generated code.</span></span>
* <span data-ttu-id="c44c9-141">Eseguire i processi Web tooScheduled correlate in cui hello informazioni di autenticazione si verifica un errore toobe passato toohello processo di provisioning dell'utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="c44c9-141">Issue related tooScheduled WebJobs in which hello authentication information was failing toobe passed toohello Scheduler provisioning process.</span></span>

<span data-ttu-id="c44c9-142">Questo aggiornamento include hello nuova funzionalità seguente:</span><span class="sxs-lookup"><span data-stu-id="c44c9-142">This update includes hello following new feature:</span></span>

* <span data-ttu-id="c44c9-143">Supporto per i servizi di App secondario nella scheda "Servizi" hello di hello finestra di dialogo provisioning di servizio App.</span><span class="sxs-lookup"><span data-stu-id="c44c9-143">Support for secondary App Services in hello "Services" tab of hello App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="c44c9-144">Strumenti di Azure Data Lake per Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="c44c9-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="c44c9-145">Questo aggiornamento include seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c44c9-145">This updates includes hello following:</span></span>

* <span data-ttu-id="c44c9-146">**Gli strumenti di Azure Data Lake** per Visual Studio viene quindi unita hello Azure SDK per la versione di .NET.</span><span class="sxs-lookup"><span data-stu-id="c44c9-146">**Azure Data Lake Tools** for Visual Studio is now merged into hello Azure SDK for .NET release.</span></span> <span data-ttu-id="c44c9-147">Hello viene installato automaticamente quando si installa Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="c44c9-147">hello tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="c44c9-148">strumento Hello viene aggiornato di frequente, visitare [qui](http://aka.ms/datalaketool) tooget hello aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="c44c9-148">hello tool is updated frequently, go [here](http://aka.ms/datalaketool) tooget hello updates.</span></span>
* <span data-ttu-id="c44c9-149">**Esplora server** ora consente tooview tutti e creare alcune entità di metadati U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c44c9-149">**Server Explorer** now enables you tooview all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="c44c9-150">Per altre informazioni, vedere [questo](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span><span class="sxs-lookup"><span data-stu-id="c44c9-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="c44c9-151">Strumenti HDInsight</span><span class="sxs-lookup"><span data-stu-id="c44c9-151">HDInsight Tools</span></span>
<span data-ttu-id="c44c9-152">**Strumenti HDInsight** per Visual Studio ora supporta HDInsight versione 3.3, che include la visualizzazione di grafici Tez e altre correzioni della lingua.</span><span class="sxs-lookup"><span data-stu-id="c44c9-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="c44c9-153">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="c44c9-153">Azure Resource Manager</span></span>
<span data-ttu-id="c44c9-154">In questa versione è stato aggiunto il supporto di [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) per i modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c44c9-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="c44c9-155">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c44c9-155">See also</span></span>
[<span data-ttu-id="c44c9-156">Post di annuncio di Azure SDK 2.9</span><span class="sxs-lookup"><span data-stu-id="c44c9-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

