---
title: trasferimento sicuro di aaaRequire in archiviazione di Azure | Documenti Microsoft
description: "Informazioni sulle funzionalità di \"Richiede il trasferimento protetto\" hello per archiviazione di Azure e come tooenable è."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="8cebd-103">Richiedere il trasferimento sicuro</span><span class="sxs-lookup"><span data-stu-id="8cebd-103">Require secure transfer</span></span>

<span data-ttu-id="8cebd-104">opzione Hello "trasferimento sicuro richiesto" migliora la sicurezza hello dell'account di archiviazione consentendo solo le richieste di account di archiviazione toohello da connessioni protette.</span><span class="sxs-lookup"><span data-stu-id="8cebd-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="8cebd-105">Ad esempio, quando si chiama l'API REST tooaccess account di archiviazione, è necessario connettersi usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8cebd-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="8cebd-106">Quando questa impostazione è abilitata, le eventuali richieste tramite HTTP vengono rifiutate.</span><span class="sxs-lookup"><span data-stu-id="8cebd-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="8cebd-107">Quando si utilizza il servizio di Azure file hello, qualsiasi connessione senza crittografia ha esito negativo quando la "Protezione di trasferimento richiesto" è abilitate.</span><span class="sxs-lookup"><span data-stu-id="8cebd-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="8cebd-108">Sono inclusi scenari con alcune varianti di hello client Linux SMB, SMB 2.1 e SMB 3.0 senza crittografia.</span><span class="sxs-lookup"><span data-stu-id="8cebd-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="8cebd-109">Per impostazione predefinita, l'opzione di hello "trasferimento sicuro richiesto" è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="8cebd-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="8cebd-110">Poiché Archiviazione di Azure non supporta HTTPS per i nomi di dominio personalizzati, l'opzione non è applicabile quando si usa un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="8cebd-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="8cebd-111">Abilitare "Trasferimento sicuro richiesto" in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8cebd-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="8cebd-112">È possibile abilitare hello "trasferimento sicuro richiesto" Se si impostano entrambe quando si crea un account di archiviazione in hello [portale di Azure](https://portal.azure.com)e per gli account di archiviazione esistente.</span><span class="sxs-lookup"><span data-stu-id="8cebd-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="8cebd-113">Richiedere il trasferimento sicuro quando si crea un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8cebd-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="8cebd-114">Aprire hello **creare account di archiviazione** pannello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8cebd-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="8cebd-115">In **Trasferimento sicuro obbligatorio** selezionare **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="8cebd-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![screenshot](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="8cebd-117">Richiedere il trasferimento sicuro per un account di archiviazione esistente</span><span class="sxs-lookup"><span data-stu-id="8cebd-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="8cebd-118">Selezionare un account di archiviazione esistente nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8cebd-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="8cebd-119">Selezionare **configurazione** in **impostazioni** nel Pannello di hello storage account dal menu.</span><span class="sxs-lookup"><span data-stu-id="8cebd-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="8cebd-120">In **Trasferimento sicuro obbligatorio** selezionare **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="8cebd-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![screenshot](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="8cebd-122">Abilitare "Trasferimento sicuro obbligatorio" a livello di codice</span><span class="sxs-lookup"><span data-stu-id="8cebd-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="8cebd-123">nome dell'impostazione Hello _supportsHttpsTrafficOnly_ nelle proprietà di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8cebd-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="8cebd-124">È possibile abilitare l'impostazione "Trasferimento sicuro obbligatorio" tramite l'API REST, strumenti o librerie:</span><span class="sxs-lookup"><span data-stu-id="8cebd-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="8cebd-125">**API REST** (versione: 2016-12-01): [pacchetto versione](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="8cebd-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="8cebd-126">**PowerShell** (versione: 4.1.0): [pacchetto versione](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="8cebd-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="8cebd-127">**Interfaccia della riga di comando** (versione: 2.0.11): [pacchetto versione](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="8cebd-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="8cebd-128">**NodeJS** (versione: 1.1.0): [pacchetto versione](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="8cebd-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="8cebd-129">**.NET SDK** (versione: 6.3.0): [pacchetto versione](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="8cebd-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="8cebd-130">**Python SDK** (versione: 1.1.0): [pacchetto versione](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="8cebd-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="8cebd-131">**Ruby SDK** (versione: 0.11.0): [pacchetto versione](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="8cebd-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="8cebd-132">Abilitare l'impostazione "Trasferimento sicuro obbligatorio" tramite l'API REST</span><span class="sxs-lookup"><span data-stu-id="8cebd-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="8cebd-133">toosimplify test con l'API REST, è possibile utilizzare [ArmClient](https://github.com/projectkudu/ARMClient) toocall dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8cebd-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="8cebd-134">È possibile utilizzare di sotto della riga di comando toocheck hello con hello API REST:</span><span class="sxs-lookup"><span data-stu-id="8cebd-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="8cebd-135">In risposta hello, è possibile trovare _supportsHttpsTrafficOnly_ impostazione.</span><span class="sxs-lookup"><span data-stu-id="8cebd-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="8cebd-136">Esempio:</span><span class="sxs-lookup"><span data-stu-id="8cebd-136">Sample:</span></span>

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

<span data-ttu-id="8cebd-137">È possibile utilizzare di sotto della riga di comando tooenable hello con hello API REST:</span><span class="sxs-lookup"><span data-stu-id="8cebd-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="8cebd-138">Esempio di Input.json:</span><span class="sxs-lookup"><span data-stu-id="8cebd-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="8cebd-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8cebd-139">Next steps</span></span>
<span data-ttu-id="8cebd-140">Archiviazione di Azure fornisce un set completo di funzionalità di sicurezza, che insieme consentono agli sviluppatori di applicazioni sicure toobuild.</span><span class="sxs-lookup"><span data-stu-id="8cebd-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="8cebd-141">Per ulteriori dettagli, visitare hello [Guida alla protezione di archiviazione](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="8cebd-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
