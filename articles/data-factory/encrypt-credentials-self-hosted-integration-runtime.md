---
title: Crittografare credenziali in Azure Data Factory | Microsoft Docs
description: Altre informazioni su come crittografare e archiviare le credenziali per gli archivi dati locali in un computer con il runtime di integrazione self-hosted.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2018
ms.author: abnarain
ms.openlocfilehash: 0f42d971fcf21d0f719468a8c10ff637f2e523f9
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/23/2018
---
# <a name="encrypt-credentials-for-on-premises-data-stores-in-azure-data-factory"></a>Crittografare le informazioni sulle credenziali per gli archivi dati locali in Azure Data Factory
È possibile crittografare e archiviare le credenziali per gli archivi dati locali (servizi collegati con informazioni riservate) in un computer con il runtime di integrazione self-hosted. 

Si passa un file di definizione JSON con le credenziali per il <br/>cmdlet [**New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential**](https://docs.microsoft.com/powershell/module/azurerm.datafactoryv2/New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential?view=azurermps-4.4.0) per generare un file di definizione JSON di output con le credenziali crittografate. Quindi, è possibile utilizzare la definizione JSON aggiornata per creare i servizi collegati.

> [!NOTE]
> Questo articolo si applica alla versione 2 del servizio Data Factory, attualmente in versione di anteprima. Se si usa la versione 1 del servizio Data Factory, disponibile a livello generale, vedere la [documentazione su Data Factory versione 1](v1/data-factory-introduction.md).

## <a name="author-sql-server-linked-service"></a>Servizio collegato di SQL Server autore
Creare un file JSON denominato **SqlServerLinkedService.json** in qualsiasi cartella con il seguente contenuto:  

Sostituire `<servername>`, `<databasename>`, `<username>` e `<password>` con i valori per SQL Server prima di salvare il file. Inoltre, sostituire `<integration runtime name>` con il nome del runtime di integrazione. 

```json
{
    "properties": {
        "type": "SqlServer",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Server=<servername>;Database=<databasename>;User ID=<username>;Password=<password>;Timeout=60"
            }
        },
        "connectVia": {
            "type": "integrationRuntimeReference",
            "referenceName": "<integration runtime name>"
        },
        "name": "SqlServerLinkedService"
    }
}
```

## <a name="encrypt-credentials"></a>Crittografare le credenziali
Per crittografare i dati sensibili del payload JSON in un runtime di integrazione self-hosted locale, eseguire **New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential** e passare il payload JSON. Questo cmdlet assicura che le credenziali vengano crittografate utilizzando DPAPI e archiviate nel nodo del runtime di integrazione self-hosted in locale. Il payload di output può essere reindirizzato a un altro file JSON (in questo caso 'encryptedLinkedService.json') che contiene le credenziali crittografate.

```powershell
New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "SqlServerLinkedService" -DefinitionFile ".\SQLServerLinkedService.json" > encryptedSQLServerLinkedService.json
```

## <a name="use-the-json-with-encrypted-credentials"></a>Usare JSON con credenziali crittografate
A questo punto, utilizzare il file JSON di output del comando precedente contenente le credenziali crittografate per impostare il **SqlServerLinkedService**.

```powershell
Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "EncryptedSqlServerLinkedService" -DefinitionFile ".\encryptedSqlServerLinkedService.json" 
```

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sulle considerazioni relative alla sicurezza per lo spostamento dei dati, vedere [Considerazioni relative alla sicurezza per lo spostamento dei dati](data-movement-security-considerations.md).

