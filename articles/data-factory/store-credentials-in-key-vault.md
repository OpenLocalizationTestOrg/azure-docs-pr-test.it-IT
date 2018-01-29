---
title: Archiviare le credenziali in Azure Key Vault | Microsoft Docs
description: "Informazioni su come archiviare le credenziali per gli archivi dati usati in un insieme di credenziali delle chiavi di Azure che Azure Data Factory può recuperare automaticamente in fase di esecuzione."
services: data-factory
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2017
ms.author: jingwang
ms.openlocfilehash: 145c2bc0556010389e78e523fde6fd4b9063f930
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="store-credential-in-azure-key-vault"></a>Archiviare le credenziali in Azure Key Vault

È possibile archiviare le credenziali per gli archivi dati in un [insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-whatis.md). Azure Data Factory Azure recupera le credenziali durante l'esecuzione di un'attività che usa l'archivio dati.

Attualmente, [connettore di Dynamics](connector-dynamics-crm-office-365.md), [connettore Salesforce](connector-salesforce.md) e alcuni appena attivare il supporto di connettori questa funzionalità. Prevedere più presto in un secondo momento. È possibile controllare ogni argomento connettore su Dettagli. Per i campi di segreto che supportano questa funzionalità, verrà visualizzata una nota nella pronuncia descrizione "*è possibile scegliere di contrassegnare questo campo come SecureString per archiviare in modo sicuro nel file ADF, o archiviare password in Azure e consentire il pull di attività di copia da qui Quando si esegue la copia dei dati - informazioni dalle credenziali di archiviazione nell'insieme di credenziali chiave.* "

> [!NOTE]
> Questo articolo si applica alla versione 2 del servizio Data Factory, attualmente in versione di anteprima. Se si usa la versione 1 del servizio di Data Factory, disponibile a livello generale, vedere la [documentazione sulla versione 1 di Data Factory](v1/data-factory-introduction.md).

## <a name="prerequisites"></a>Prerequisiti

Questa funzionalità si basa sull'identità del servizio Data Factory. È necessario apprenderne il funzionamento tramite l'[identità del servizio Data Factory](data-factory-service-identity.md) e verificare che la data factory in uso abbia un'identità associata.

## <a name="steps"></a>Passaggi

Per fare riferimento a una credenziale archiviata in Azure Key Vault, è necessario:

1. [Recuperare l'identità del servizio Data Factory](data-factory-service-identity.md#retrieve-service-identity) copiando il valore di "SERVICE IDENTITY APPLICATION ID" generato con la factory.
2. Concedere l'accesso dell'identità del servizio ad Azure Key Vault. Nell'insieme di credenziali delle chiavi -> Controllo dell'accesso -> Aggiungi -> cercare l'ID applicazione identità del servizio per aggiungere almeno l'autorizzazione **Lettore**. Consente a questa factory designata di accedere al segreto nell'insieme di credenziali.
3. Creare un servizio collegato che punta ad Azure Key Vault. Fare riferimento a [Servizio collegato di Azure Key Vault](#azure-key-vault-linked-service).
4. Creare il servizio collegato di archiviazione dati, nel cui riferimento il segreto corrispondente è archiviato nell'insieme di credenziali delle chiavi. Vedere [Credenziali di riferimento archiviate nell'insieme di credenziali delle chiavi](#reference-credential-stored-in-key-vault).

## <a name="azure-key-vault-linked-service"></a>Servizio collegato di Azure Key Vault

Per il servizio collegato di Azure Key Vault sono supportate le proprietà seguenti:

| Proprietà | DESCRIZIONE | Obbligatoria |
|:--- |:--- |:--- |
| type | La proprietà type deve essere impostata su **AzureKeyVault**. | Sì |
| baseUrl | Specificare l'URL di Azure Key Vault. | Sì |

**Esempio:**

```json
{
    "name": "AzureKeyVaultLinkedService",
    "properties": {
        "type": "AzureKeyVault",
        "typeProperties": {
            "baseUrl": "https://<azureKeyVaultName>.vault.azure.net"
        }
    }
}
```

## <a name="reference-credential-stored-in-key-vault"></a>Credenziali di riferimento archiviate nell'insieme di credenziali delle chiavi

Quando si configura un campo nel servizio collegato che fa riferimento a un segreto dell'insieme di credenziali delle chiavi, sono supportate le proprietà seguenti:

| Proprietà | DESCRIZIONE | Obbligatoria |
|:--- |:--- |:--- |
| type | La proprietà type del campo deve essere impostata su: **AzureKeyVaultSecret**. | Sì |
| secretName | Il nome del segreto in Azure Key Vault. | Sì |
| secretVersion | La versione del segreto in Azure Key Vault.<br/>Se non specificata, usare sempre la versione più recente del segreto.<br/>Se specificata, corrisponde alla versione specificata.| No  |
| store | Fa riferimento a un servizio collegato di Azure Key Vault che si usa per archiviare la credenziale. | Sì |

**Esempio: (vedere la sezione "password")**

```json
{
    "name": "DynamicsLinkedService",
    "properties": {
        "type": "Dynamics",
        "typeProperties": {
            "deploymentType": "<>",
            "organizationName": "<>",
            "authenticationType": "<>",
            "username": "<>",
            "password": {
                "type": "AzureKeyVaultSecret",
                "secretName": "<secret name in AKV>",
                "store":{
                    "referenceName": "<Azure Key Vault linked service>",
                    "type": "LinkedServiceReference"
                }
            }
        }
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
Per un elenco degli archivi dati supportati come origini o sink dall'attività di copia in Azure Data Factory, vedere gli [archivi dati supportati](copy-activity-overview.md#supported-data-stores-and-formats).