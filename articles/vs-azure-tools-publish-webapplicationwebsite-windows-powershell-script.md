---
title: aaaPublish-WebApplicationWebSite (script di Windows PowerShell) | Documenti Microsoft
description: Informazioni su come toopublish web progetto tooan sito Web di Azure. In caso contrario, questo script crea le risorse necessarie hello nella sottoscrizione di Azure.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publish-WebApplicationWebSite (script di Windows PowerShell)
## <a name="syntax"></a>Sintassi
Pubblica un tooan progetto web sito Web di Azure. script di Hello crea risorse hello necessarie nella sottoscrizione di Azure, se non sono presenti.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Configurazione
Hello percorso toohello file di configurazione JSON che descrive i dettagli di hello della distribuzione hello.

| . | Valore predefinito |
| --- | --- |
| Alias |nessuno |
| Obbligatorio? |true |
| Posizione |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

## <a name="subscriptionname"></a>SubscriptionName
nome Hello della sottoscrizione di Azure da sito Web di hello toocreate in hello.

| . | Valore predefinito |
| --- | --- |
| Alias |nessuno |
| Obbligatorio? |false |
| Posizione |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

## <a name="webdeploypackage"></a>WebDeployPackage
Hello percorso toohello web pacchetto toopublish toohello sito Web di distribuzione. È possibile creare il pacchetto utilizzando la procedura guidata pubblica Web hello in Visual Studio. Per ulteriori informazioni, vedere [Introduzione a Servizi cloud di Azure e ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Parametro | Valore predefinito |
| --- | --- |
| Alias |nessuno |
| Obbligatorio? |false |
| Posizione |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
Hello username e password per il database SQL di hello in Azure.

| . | Valore predefinito |
| --- | --- |
| Alias |nessuno |
| Obbligatorio? |false |
| Posizione |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Se true, i messaggi di stampanti da hello script toohello flusso di output.

| . | Valore predefinito |
| --- | --- |
| Alias |nessuno |
| Obbligatorio? |false |
| Posizione |denominata |
| Valore predefinito |false |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

## <a name="remarks"></a>Osservazioni
Per una spiegazione completa di toouse hello script toocreate Dev e ambienti di Test, vedere [tooDev tooPublish tramite script di Windows PowerShell e gli ambienti di Test](vs-azure-tools-publishing-using-powershell-scripts.md).

file di configurazione JSON Hello specifica dettagli hello novità toobe distribuito. Sono incluse informazioni hello specificato al momento della creazione progetto di hello, ad esempio nome hello e il nome utente per il sito Web di hello. Include inoltre tooprovision database hello, se presente. Hello di codice seguente viene illustrato un file di configurazione JSON di esempio:

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

È possibile modificare i file hello JSON configurazione toochange con gli elementi da distribuire. Una sezione del sito Web è necessaria, ma hello database sezione è facoltativa.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere [Publish-WebApplicationVM (script di Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)

