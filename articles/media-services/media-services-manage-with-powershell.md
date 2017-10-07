---
title: aaaManage account servizi multimediali di Azure con PowerShell
description: Informazioni su come account di toomanage servizi multimediali di Azure con i cmdlet di PowerShell.
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>Gestire gli account di Servizi multimediali di Azure con PowerShell
> [!div class="op_single_selector"]
> * [Portale](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toobe toocreate in grado di un account di servizi multimediali di Azure, è necessario disporre di un account di Azure. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">versione di valutazione gratuita di Azure</a>.
> 
> 

## <a name="overview"></a>Panoramica
Questo articolo vengono elencati i cmdlet di hello Azure PowerShell per Azure Media Services (AMS) nel framework di gestione risorse di Azure hello. i cmdlet di Hello esistono in hello **Microsoft.Azure.Commands.Media** dello spazio dei nomi.

## <a name="versions"></a>Versioni
**ApiVersion**:   "2015-10-01"

## <a name="new-azurermmediaservice"></a>New-AzureRmMediaService
Crea un servizio multimediale.

### <a name="syntax"></a>Sintassi
Set di parametri: StorageAccountIdParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

Set di parametri: StorageAccountsParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a>Parametri
**-ResourceGroupName &lt;String&gt;**

Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |0 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**-AccountName &lt;String&gt;**

Specifica il nome di hello del servizio multimediale hello.

| Alias | Nome |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |1 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

**-Location &lt;String&gt;**

Specifica percorso della risorsa del servizio di supporto hello hello.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |2 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**-StorageAccountId &lt;String&gt;**

Specifica un account di archiviazione primario associato al servizio multimediale hello.

* Nuovo account di archiviazione (creata con l'API di gestione risorse di hello) è supportato solo.
* deve esistere Hello account di archiviazione e ha hello stessa località del servizio di supporto hello.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |3 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Nome del set di parametri |StorageAccountIdParamSet |
| Caratteri jolly accettati? |false |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Specifica l'account di archiviazione associato al servizio multimediale hello.

* Nuovo account di archiviazione (creata con l'API di gestione risorse di hello) è supportato solo.
* deve esistere Hello account di archiviazione e ha hello stessa località del servizio di supporto hello.
* È possibile specificare come primario un solo account di archiviazione.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |3 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Nome del set di parametri |StorageAccountsParamSet |
| Caratteri jolly accettati? |false |

**-Tags &lt;Hashtable&gt;**

Specifica una tabella hash di tag hello associati al servizio multimediale hello.

* Esempio: @{"tag1"="Valore1";" tag2 "=: value2"}

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |false |
| Posizione? |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

**&lt;CommandParameters&gt;**

Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Input
tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.

### <a name="outputs"></a>outputs
tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
Aggiorna un servizio multimediale.

### <a name="syntax"></a>Sintassi
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>Parametri
**-ResourceGroupName &lt;String&gt;**

Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |0 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**-AccountName &lt;String&gt;**

Specifica il nome di hello del servizio multimediale hello.

| Alias | Nome |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |1 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Specifica l'account di archiviazione associato al servizio multimediale hello.

* Nuovo account di archiviazione (creata con l'API di gestione risorse di hello) è supportato solo.
* deve esistere Hello account di archiviazione e ha hello stessa località del servizio di supporto hello.
* È possibile specificare come primario un solo account di archiviazione.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |false |
| Posizione? |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Nome del set di parametri |StorageAccountsParamSet |
| Caratteri jolly accettati? |false |

**-Tags &lt;Hashtable&gt;**

Specifica una tabella hash di tag hello che sono associati a questo servizio di supporto.

* i tag associati al servizio multimediale hello Hello vengono sostituiti con il valore specificato dal cliente hello.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |false |
| Posizione? |denominata |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**&lt;CommandParameters&gt;**

Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Input
tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.

### <a name="outputs"></a>outputs
tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
Rimuove un servizio multimediale.

### <a name="syntax"></a>Sintassi
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametri
**-ResourceGroupName &lt;String&gt;**

Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |0 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**-AccountName &lt;String&gt;**

Specifica il nome di hello del servizio multimediale hello.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |2 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |False |

**&lt;CommandParameters&gt;**

Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Input
tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.

### <a name="outputs"></a>outputs
tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
Ottiene tutti i servizi multimediali in un gruppo di risorse o un servizio multimediale con un nome specificato.

### <a name="syntax"></a>Sintassi
Set di parametri: ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

Set di parametri: AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametri
**-ResourceGroupName &lt;String&gt;**

Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |0 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Nome del set di parametri |ResourceGroupParameterSet, AccountNameParameterSet |

Caratteri jolly accettati?   false

**-AccountName &lt;String&gt;**

Specifica il nome di hello del servizio multimediale hello.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |1 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Nome del set di parametri |AccountNameParameterSet |
| Caratteri jolly accettati? |false |

**&lt;CommandParameters&gt;**

Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Input
tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.

### <a name="outputs"></a>outputs
tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
Ottiene le chiavi di un servizio multimediale.

### <a name="syntax"></a>Sintassi
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametri
**-ResourceGroupName &lt;String&gt;**

Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |0 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**-AccountName &lt;String&gt;**

Specifica il nome di hello del servizio multimediale hello.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |1 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**&lt;CommandParameters&gt;**

Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Input
tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.

### <a name="outputs"></a>outputs
tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
Rigenera una chiave primaria o secondaria di un servizio multimediale.

### <a name="syntax"></a>Sintassi
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>Parametri
**-ResourceGroupName &lt;String&gt;**

Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |0 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**-AccountName &lt;String&gt;**

Specifica il nome di hello del servizio multimediale hello.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |1 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**-KeyType &lt;KeyType&gt;**

Specifica tipo di chiave del servizio di supporto hello hello.

* Primaria o secondaria

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |2 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |false |
| Caratteri jolly accettati? |false |

**&lt;CommandParameters&gt;**

Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Input
tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toothe cmdlet.

### <a name="outputs"></a>outputs
tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Consente di sincronizzare le chiavi di account di archiviazione per un account di archiviazione associato al servizio multimediale hello.

### <a name="syntax"></a>Sintassi
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametri
**-ResourceGroupName &lt;String&gt;**

Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |0 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**-AccountName &lt;String&gt;**

Specifica il nome di hello del servizio multimediale hello.

| Alias | nessuno |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |1 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**-StorageAccountId &lt;String&gt;**

Specifica l'account di archiviazione hello associato al servizio multimediale hello.

| Alias | ID |
| --- | --- |
| Obbligatorio? |true |
| Posizione? |2 |
| Valore predefinito |nessuno |
| Input pipeline accettato? |true(ByPropertyName) |
| Caratteri jolly accettati? |false |

**&lt;CommandParameters&gt;**

Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Input
tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.

### <a name="outputs"></a>outputs
tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.

## <a name="next-step"></a>Passaggio successivo
Vedere i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

