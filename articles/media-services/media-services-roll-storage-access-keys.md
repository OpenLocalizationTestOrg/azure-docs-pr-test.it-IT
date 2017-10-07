---
title: le chiavi di accesso ai servizi multimediali aaaUpdate dopo l'operazione di archiviazione | Documenti Microsoft
description: In questo articolo offrono indicazioni su come le chiavi di accesso tooupdate Media Services dopo l'operazione di archiviazione.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a>Aggiornare Servizi multimediali dopo il rollover delle chiavi di accesso alle risorse di archiviazione

Quando si crea un nuovo account di servizi multimediali di Azure (AMS), verrà anche chiesto tooselect account di archiviazione di Azure che è utilizzato toostore i contenuti multimediali. È possibile aggiungere tooyour gli account di archiviazione più di un account di servizi multimediali. Questo argomento viene illustrato come chiavi per l'archiviazione toorotate. Viene inoltre illustrato come archiviazione tooadd account tooa account di supporto. 

azioni di hello tooperform descritte in questo argomento, è consigliabile usare [API ARM](https://docs.microsoft.com/rest/api/media/mediaservice) e [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).  Per ulteriori informazioni, vedere [come toomanage Azure risorse con PowerShell e Gestione risorse](../azure-resource-manager/powershell-azure-resource-manager.md).

## <a name="overview"></a>Panoramica

Quando viene creato un nuovo account di archiviazione, Azure genera due chiavi di accesso archiviazione a 512 bit, che sono utilizzati tooauthenticate accedere tooyour account di archiviazione. tookeep le connessioni di archiviazione più sicure, che è consigliabile tooperiodically rigenerano e ruotare la chiave di accesso di archiviazione. Due chiavi di accesso (primari e secondari) vengono forniti in ordine tooenable toomaintain connessioni toohello account di archiviazione utilizzando uno tasto mentre si rigenera hello altre chiavi di accesso. Questa procedura viene anche denominata "rollover delle chiavi di accesso".

Servizi multimediali dipende da una chiave di archiviazione fornita tooit. In particolare, i localizzatori hello toostream usato o scaricare gli asset dipendono dalla chiave di accesso di archiviazione specificato hello. Quando viene creato un account di sistema AMS assume una dipendenza di chiave di accesso di archiviazione primaria hello per impostazione predefinita, ma come un utente è possibile aggiornare una chiave di archiviazione hello AMS con. È necessario assicurarsi di servizi multimediali toolet sapere quale chiave toouse seguendo i passaggi descritti in questo argomento.  

>[!NOTE]
> Se si dispone di più account di archiviazione, è necessario eseguire questa procedura per ogni account di archiviazione. ordine di Hello in cui si ruotare le chiavi di archiviazione non è fisso. È possibile ruotare la chiave secondaria hello prima e quindi hello principale viceversa chiave o viceversa.
>
> Prima di eseguire i passaggi descritti in questo argomento in un account di produzione, assicurarsi che tootest loro un account di pre-produzione.
>

## <a name="steps-toorotate-storage-keys"></a>Chiavi per l'archiviazione toorotate passaggi 
 
 1. Modifica hello chiave account di archiviazione primario tramite il cmdlet powershell hello o [Azure](https://portal.azure.com/) portale.
 2. Chiamare il cmdlet AzureRmMediaServiceStorageKeys di sincronizzazione con i parametri appropriati tooforce supporti account toopick le chiavi di account di archiviazione
 
    Hello di esempio seguente viene illustrato come toosync chiavi account toostorage.
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. Attendere circa un'ora. Verificare gli scenari di streaming hello funzionino.
 4. Modifica chiave account di archiviazione secondario tramite i cmdlet di powershell hello o il portale di Azure.
 5. Chiamare powershell AzureRmMediaServiceStorageKeys di sincronizzazione con i parametri appropriati tooforce supporti account toopick di nuove chiavi dell'account di archiviazione. 
 6. Attendere circa un'ora. Verificare gli scenari di streaming hello funzionino.
 
### <a name="a-powershell-cmdlet-example"></a>Esempio di cmdlet PowerShell 

Hello esempio seguente viene illustrato come tooget hello account di archiviazione e sincronizzarlo con account hello AMS.

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a>Account di sistema AMS tooyour gli account di archiviazione di tooadd passaggi

Hello argomento seguente viene illustrato come archiviazione tooadd account account tooyour AMS: [allegare tooa gli account di archiviazione più account di servizi multimediali](meda-services-managing-multiple-storage-accounts.md).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Ringraziamenti
Desideriamo hello tooacknowledge seguente persone che hanno contribuito per la creazione di questo documento: Cenk Dingiloglu, Milano Gada, Seva Titov.
