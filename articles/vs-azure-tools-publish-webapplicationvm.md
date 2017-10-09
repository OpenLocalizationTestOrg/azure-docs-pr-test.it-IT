---
title: aaaPublish-WebApplicationVM | Documenti Microsoft
description: Informazioni su come toodeploy una macchina virtuale del tooa applicazioni web. In caso contrario, questo script crea le risorse necessarie hello nella sottoscrizione di Azure.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publish-WebApplicationVM (Windows PowerShell script)
Consente di distribuire una macchina virtuale del tooa applicazioni web. script di Hello crea risorse hello necessarie nella sottoscrizione di Azure, se non sono presenti.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>Configurazione
Hello percorso toohello file di configurazione JSON che descrive i dettagli di hello della distribuzione hello.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

### <a name="subscriptionname"></a>SubscriptionName
nome Hello di hello sottoscrizione di Azure in cui si desidera macchina virtuale di toocreate hello.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |false |
| Posizione |denominata |
| Valore predefinito |Usa prima sottoscrizione hello nel file di sottoscrizione hello |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

### <a name="webdeploypackage"></a>WebDeployPackage
Hello percorso toohello web distribuzione pacchetto toopublish toohello macchina virtuale. È possibile creare il pacchetto utilizzando la procedura guidata pubblica Web hello in Visual Studio. Vedere [Procedura: Creare un pacchetto di distribuzione Web in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |false |
| Posizione |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

### <a name="allowuntrusted"></a>AllowUntrusted
Se true, consente l'uso di hello di certificati che non sono firmati da un'autorità radice attendibile.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |false |
| Posizione |denominata |
| Valore predefinito |false |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

### <a name="vmpassword"></a>VMPassword
credenziali di Hello per l'account della macchina virtuale hello. Esempio: - VMPassword @{nome = "admin"; Password = "password"}

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |false |
| Posizione |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
credenziali Hello per il database SQL di hello in Azure. Esempio: - DatabaseServerPassword @{nome = "admin"; Password = "password"}

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |false |
| Posizione |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Se true, i messaggi di stampanti da hello script toohello flusso di output.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |false |
| Posizione |denominata |
| Valore predefinito |false |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

## <a name="remarks"></a>Osservazioni
Per una spiegazione completa di toouse hello script toocreate Dev e ambienti di Test, vedere [tooDev tooPublish tramite script di Windows PowerShell e gli ambienti di Test](vs-azure-tools-publishing-using-powershell-scripts.md).

file di configurazione JSON Hello specifica dettagli hello novità toobe distribuito. Sono incluse informazioni hello specificato al momento della creazione progetto di hello, ad esempio nome hello, gruppo di affinità, immagine VHD e dimensioni di macchina virtuale hello. Inoltre include endpoint hello nella macchina virtuale hello hello tooprovision di database, se presente e i parametri di distribuzione web. Hello di codice seguente viene illustrato un file di configurazione JSON di esempio:

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

È possibile modificare hello JSON configurazione file toochange ciò che viene eseguito il provisioning. Una macchina virtuale e un servizio cloud sono necessarie, ma hello database sezione è facoltativa.

