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
# <a name="require-secure-transfer"></a>Richiedere il trasferimento sicuro

opzione Hello "trasferimento sicuro richiesto" migliora la sicurezza hello dell'account di archiviazione consentendo solo le richieste di account di archiviazione toohello da connessioni protette. Ad esempio, quando si chiama l'API REST tooaccess account di archiviazione, è necessario connettersi usando HTTPS. Quando questa impostazione è abilitata, le eventuali richieste tramite HTTP vengono rifiutate.

Quando si utilizza il servizio di Azure file hello, qualsiasi connessione senza crittografia ha esito negativo quando la "Protezione di trasferimento richiesto" è abilitate. Sono inclusi scenari con alcune varianti di hello client Linux SMB, SMB 2.1 e SMB 3.0 senza crittografia. 

Per impostazione predefinita, l'opzione di hello "trasferimento sicuro richiesto" è disabilitata.

> [!NOTE]
> Poiché Archiviazione di Azure non supporta HTTPS per i nomi di dominio personalizzati, l'opzione non è applicabile quando si usa un nome di dominio personalizzato.

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>Abilitare "Trasferimento sicuro richiesto" in hello portale di Azure

È possibile abilitare hello "trasferimento sicuro richiesto" Se si impostano entrambe quando si crea un account di archiviazione in hello [portale di Azure](https://portal.azure.com)e per gli account di archiviazione esistente.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Richiedere il trasferimento sicuro quando si crea un account di archiviazione

1. Aprire hello **creare account di archiviazione** pannello in hello portale di Azure.
1. In **Trasferimento sicuro obbligatorio** selezionare **Abilitato**.

  ![screenshot](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Richiedere il trasferimento sicuro per un account di archiviazione esistente

1. Selezionare un account di archiviazione esistente nel portale di Azure hello.
1. Selezionare **configurazione** in **impostazioni** nel Pannello di hello storage account dal menu.
1. In **Trasferimento sicuro obbligatorio** selezionare **Abilitato**.

  ![screenshot](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>Abilitare "Trasferimento sicuro obbligatorio" a livello di codice

nome dell'impostazione Hello _supportsHttpsTrafficOnly_ nelle proprietà di account di archiviazione. È possibile abilitare l'impostazione "Trasferimento sicuro obbligatorio" tramite l'API REST, strumenti o librerie:

* **API REST** (versione: 2016-12-01): [pacchetto versione](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (versione: 4.1.0): [pacchetto versione](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **Interfaccia della riga di comando** (versione: 2.0.11): [pacchetto versione](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (versione: 1.1.0): [pacchetto versione](https://www.npmjs.com/package/azure-arm-storage/)
* **.NET SDK** (versione: 6.3.0): [pacchetto versione](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **Python SDK** (versione: 1.1.0): [pacchetto versione](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **Ruby SDK** (versione: 0.11.0): [pacchetto versione](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>Abilitare l'impostazione "Trasferimento sicuro obbligatorio" tramite l'API REST

toosimplify test con l'API REST, è possibile utilizzare [ArmClient](https://github.com/projectkudu/ARMClient) toocall dalla riga di comando.

 È possibile utilizzare di sotto della riga di comando toocheck hello con hello API REST:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

In risposta hello, è possibile trovare _supportsHttpsTrafficOnly_ impostazione. Esempio:

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

È possibile utilizzare di sotto della riga di comando tooenable hello con hello API REST:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Esempio di Input.json:
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>Passaggi successivi
Archiviazione di Azure fornisce un set completo di funzionalità di sicurezza, che insieme consentono agli sviluppatori di applicazioni sicure toobuild. Per ulteriori dettagli, visitare hello [Guida alla protezione di archiviazione](storage-security-guide.md).
