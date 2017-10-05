---
title: Richiedere il trasferimento sicuro in Archiviazione di Azure | Microsoft Docs
description: "Informazioni sulla funzionalità \"Trasferimento sicuro obbligatorio\" per Archiviazione di Azure e su come abilitarla."
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
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="1d3da-103">Richiedere il trasferimento sicuro</span><span class="sxs-lookup"><span data-stu-id="1d3da-103">Require secure transfer</span></span>

<span data-ttu-id="1d3da-104">L'opzione Trasferimento sicuro obbligatorio aumenta la sicurezza dell'account di archiviazione perché consente le richieste all'account di archiviazione solo tramite connessioni sicure il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1d3da-104">The "Secure transfer required" option enhances the security of your storage account by only allowing requests to the storage account from secure connections.</span></span> <span data-ttu-id="1d3da-105">Ad esempio, quando si chiamano API REST per accedere all'account di archiviazione, è necessario connettersi usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1d3da-105">For example, when calling REST APIs to access your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="1d3da-106">Quando questa impostazione è abilitata, le eventuali richieste tramite HTTP vengono rifiutate.</span><span class="sxs-lookup"><span data-stu-id="1d3da-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="1d3da-107">Quando si usa il servizio File di Azure, se è abilitata l'opzione "Trasferimento sicuro obbligatorio" le connessioni senza crittografia hanno esito negativo.</span><span class="sxs-lookup"><span data-stu-id="1d3da-107">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="1d3da-108">Questo include scenari in cui si usano SMB 2.1, SMB 3.0 senza crittografia e alcuni tipi del client SMB Linux.</span><span class="sxs-lookup"><span data-stu-id="1d3da-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span> 

<span data-ttu-id="1d3da-109">Per impostazione predefinita, l'opzione "Trasferimento sicuro obbligatorio" è disattivata.</span><span class="sxs-lookup"><span data-stu-id="1d3da-109">By default, the "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="1d3da-110">Poiché Archiviazione di Azure non supporta HTTPS per i nomi di dominio personalizzati, l'opzione non è applicabile quando si usa un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1d3da-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a><span data-ttu-id="1d3da-111">Abilitare "Trasferimento sicuro obbligatorio" nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1d3da-111">Enable "Secure transfer required" in the Azure portal</span></span>

<span data-ttu-id="1d3da-112">È possibile abilitare l'impostazione "Trasferimento sicuro obbligatorio" sia quando si crea un account di archiviazione nel [portale di Azure](https://portal.azure.com), sia per gli account di archiviazione esistenti.</span><span class="sxs-lookup"><span data-stu-id="1d3da-112">You can enable the "Secure transfer required" setting both when you create a storage account in the [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="1d3da-113">Richiedere il trasferimento sicuro quando si crea un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d3da-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="1d3da-114">Aprire il pannello **Crea account di archiviazione** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d3da-114">Open the **Create storage account** blade in the Azure portal.</span></span>
1. <span data-ttu-id="1d3da-115">In **Trasferimento sicuro obbligatorio** selezionare **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="1d3da-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![screenshot](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="1d3da-117">Richiedere il trasferimento sicuro per un account di archiviazione esistente</span><span class="sxs-lookup"><span data-stu-id="1d3da-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="1d3da-118">Selezionare un account di archiviazione esistente nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d3da-118">Select an existing storage account in the Azure portal.</span></span>
1. <span data-ttu-id="1d3da-119">Selezionare **Configurazione** in **IMPOSTAZIONI** nel pannello del menu dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1d3da-119">Select **Configuration** under **SETTINGS** in the storage account menu blade.</span></span>
1. <span data-ttu-id="1d3da-120">In **Trasferimento sicuro obbligatorio** selezionare **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="1d3da-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![screenshot](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="1d3da-122">Abilitare "Trasferimento sicuro obbligatorio" a livello di codice</span><span class="sxs-lookup"><span data-stu-id="1d3da-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="1d3da-123">Nelle proprietà dell'account di archiviazione, il nome dell'impostazione è _supportsHttpsTrafficOnly_.</span><span class="sxs-lookup"><span data-stu-id="1d3da-123">The setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="1d3da-124">È possibile abilitare l'impostazione "Trasferimento sicuro obbligatorio" tramite l'API REST, strumenti o librerie:</span><span class="sxs-lookup"><span data-stu-id="1d3da-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="1d3da-125">**API REST** (versione: 2016-12-01): [pacchetto versione](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="1d3da-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="1d3da-126">**PowerShell** (versione: 4.1.0): [pacchetto versione](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="1d3da-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="1d3da-127">**Interfaccia della riga di comando** (versione: 2.0.11): [pacchetto versione](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="1d3da-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="1d3da-128">**NodeJS** (versione: 1.1.0): [pacchetto versione](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="1d3da-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="1d3da-129">**.NET SDK** (versione: 6.3.0): [pacchetto versione](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="1d3da-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="1d3da-130">**Python SDK** (versione: 1.1.0): [pacchetto versione](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="1d3da-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="1d3da-131">**Ruby SDK** (versione: 0.11.0): [pacchetto versione](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="1d3da-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="1d3da-132">Abilitare l'impostazione "Trasferimento sicuro obbligatorio" tramite l'API REST</span><span class="sxs-lookup"><span data-stu-id="1d3da-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="1d3da-133">Per semplificare il test con l'API REST, è possibile usare [ArmClient](https://github.com/projectkudu/ARMClient) per eseguire la chiamata dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="1d3da-133">To simplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) to call from command line.</span></span>

 <span data-ttu-id="1d3da-134">Per verificare l'impostazione con l'API REST, usare la riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d3da-134">You can use below command line to check the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="1d3da-135">Nella risposta è possibile trovare l'impostazione _supportsHttpsTrafficOnly_.</span><span class="sxs-lookup"><span data-stu-id="1d3da-135">In the response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="1d3da-136">Esempio:</span><span class="sxs-lookup"><span data-stu-id="1d3da-136">Sample:</span></span>

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

<span data-ttu-id="1d3da-137">Per abilitare l'impostazione con l'API REST, usare la riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d3da-137">You can use below command line to enable the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="1d3da-138">Esempio di Input.json:</span><span class="sxs-lookup"><span data-stu-id="1d3da-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="1d3da-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d3da-139">Next steps</span></span>
<span data-ttu-id="1d3da-140">Archiviazione di Azure fornisce un set completo di funzionalità di sicurezza, che consentono agli sviluppatori di creare applicazioni sicure.</span><span class="sxs-lookup"><span data-stu-id="1d3da-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers to build secure applications.</span></span> <span data-ttu-id="1d3da-141">Per altre informazioni, vedere la [Guida alla sicurezza delle risorse di archiviazione](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="1d3da-141">For more details, visit the [Storage Security Guide](storage-security-guide.md).</span></span>
