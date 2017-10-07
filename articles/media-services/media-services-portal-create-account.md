---
title: un account di servizi multimediali di Azure con il portale di Azure hello aaaCreate | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di creazione di un account di servizi multimediali di Azure con hello portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a>Creare un account di servizi multimediali di Azure tramite hello portale di Azure
> [!div class="op_single_selector"]
> * [Portale](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocomplete questa esercitazione, è necessario un account di Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Hello portale di Azure fornisce un modo tooquickly creare un account di servizi multimediali di Azure (AMS). È possibile utilizzare il tooaccess account servizi multimediali che abilita è toostore, crittografare, codificare, gestire e trasmettere contenuto multimediale in Azure. In fase di hello è creare un account di servizi multimediali, inoltre creare un account di archiviazione associato (o utilizzarne uno esistente) in hello stessa area geografica hello account di servizi multimediali.

In questo articolo vengono illustrati alcuni concetti comuni e viene illustrato come toocreate servizi multimediali di un account con hello portale di Azure.

## <a name="concepts"></a>Concetti
Per accedere a Servizi multimediali è necessario disporre di due account associati:

* Account di Servizi multimediali. I consente di account, accedere tooa set di servizi multimediali di basato su cloud che sono disponibili in Azure. In un account di Servizi multimediali non è possibile archiviare contenuti multimediali effettivi, Archivia invece i metadati relativi a contenuti multimediali hello e processi di elaborazione media nell'account. Al momento di hello che creazione account hello, si seleziona un'area di servizi multimediali disponibile. paese Hello selezionato è un centro dati che vengono archiviati i record di metadati hello per l'account.
  
* Un account di archiviazione di Azure. Gli account di archiviazione devono trovarsi in hello stessa area geografica hello account di servizi multimediali. Quando si crea un account di servizi multimediali, è possibile scegliere un account di archiviazione esistente in hello stessa area oppure è possibile creare un nuovo account di archiviazione hello stessa area. Se si elimina un account di servizi multimediali, BLOB hello nell'account di archiviazione correlati non vengono eliminati.

> [!NOTE]
> Per informazioni sulla disponibilità delle funzionalità di Servizi multimediali di Azure nelle diverse aree, vedere la [disponibilità delle funzionalità di AMS nei data center](scenarios-and-availability.md#availability).

## <a name="create-an-ams-account"></a>Creare un account AMS
passaggi di Hello in questa sezione mostra come toocreate sistema AMS di un account.

1. Accedere all'indirizzo hello [portale di Azure](https://portal.azure.com/).
2. Fare clic su **+Nuovo** > **Web e dispositivi mobili** > **Servizi multimediali**.
   
    ![Creare Servizi multimediali](./media/media-services-create-account/media-services-new1.png)
3. In **CREARE UN ACCOUNT DEL SERVIZIO MULTIMEDIALE** immettere i valori richiesti.
   
    ![Creare Servizi multimediali](./media/media-services-create-account/media-services-new3.png)
   
   1. In **nome Account**, immettere il nome di hello del nuovo account di sistema AMS hello. Un nome di account di servizi multimediali è tutte lettere minuscole o numeri senza spazi e 3 caratteri too24.
   2. Nella sottoscrizione, effettuare una scelta tra hello diverse sottoscrizioni di Azure che è possibile accedere.
   3. In **gruppo di risorse**, selezionare hello risorse nuova o esistente.  Un gruppo di risorse è una raccolta di risorse che condividono il ciclo di vita, le autorizzazioni e i criteri. Fare clic [qui](../azure-resource-manager/resource-group-overview.md#resource-groups) per altre informazioni.
   4. In **percorso**, selezionare hello area geografica che verrà utilizzato toostore hello supporti e i metadati record per l'account di servizi multimediali. Quest'area verrà utilizzato tooprocess e trasmettere file multimediali. Solo hello servizi multimediali aree disponibili vengono visualizzati nell'elenco a discesa hello. 
   5. In **Account di archiviazione**, selezionare un archivio di blob storage account tooprovide del contenuto multimediale hello dall'account servizi multimediali. È possibile selezionare un account di archiviazione esistente in hello stessa area geografica account servizi multimediali, oppure è possibile creare un account di archiviazione. Viene creato un nuovo account di archiviazione in hello stessa area. le regole di Hello per account di archiviazione sono nomi hello stesso come account di servizi multimediali.
      
       Altre informazioni sull'archiviazione sono disponibili [qui](../storage/common/storage-introduction.md).
   6. Selezionare **Pin toodashboard** toosee lo stato di avanzamento hello di distribuzione account hello.
4. Fare clic su **crea** nella parte inferiore di hello del modulo hello.
   
    Una volta account hello viene creata correttamente, carica la pagina Panoramica. In hello account hello tabella di endpoint di streaming avrà un valore predefinito in hello endpoint di streaming **arrestato** stato. 

    >[!NOTE]
    >Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 
   
## <a name="toomanage-your-ams-account"></a>toomanage l'account di sistema AMS

toomanage l'account di sistema AMS (ad esempio, connettersi toohello AMS API a livello di codice, di caricare video, codificare asset, configurare la protezione del contenuto, monitorare lo stato del processo) selezionare **impostazioni** sul lato sinistro di portale hello hello. Da hello **impostazioni**, passare tooone dei pannelli disponibili hello (ad esempio: **l'accesso all'API**, **asset**, **processi**, **Protezione del contenuto**).


## <a name="next-steps"></a>Passaggi successivi

Ora è possibile caricare i file nell'account AMS. Per altre informazioni, vedere [Upload files](media-services-portal-upload-files.md)(Caricare file).

Se si intende tooaccess AMS API a livello di codice, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

