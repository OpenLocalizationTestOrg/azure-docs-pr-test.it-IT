---
title: dati dell'utente da Azure RemoteApp aaaMigrate | Documenti Microsoft
description: Informazioni su come toomigrate i dati utente da e verso Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a>Come toomigrate dati dentro e fuori da Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

È possibile utilizzare molti strumenti e metodi tootransfer [dati utente](remoteapp-upd.md) dentro e fuori da Azure RemoteApp. Ecco alcuni metodi:

* Copiare e incollare i dati usando la condivisione degli Appunti
* Copiare i file e i dati server file tooa
* Copiare i file tooOneDrive per le aziende tramite un browser
* Copiare i file mediante il reindirizzamento

> [!NOTE]
> È possibile abilitare hello OneDrive per Business o i Consumer di agenti di sincronizzazione - essi [non sono supportati](remoteapp-onedrive.md) in Azure RemoteApp.
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a>Usare l'operazione di copia e incolla in Esplora file
Copia e Incolla di utilizzo degli Appunti hello è abilitato nelle distribuzioni di RemoteApp [per impostazione predefinita](remoteapp-redirection.md). Gli utenti possono quindi copiare i file tra le app RemoteApp e del PC locale. Spesso, tramite hello normali usano le App in RemoteApp, gli utenti abbiano salvato i file che tootheir - lo spostamento di dati da RemoteApp sono facili:

1. [Pubblicare Esplora file come app](remoteapp-publish.md) in una raccolta RemoteApp. Si noti che questa è un'attività amministrativa.
2. Diretto utenti toolaunch hello Esplora File app che è stato pubblicato e toouse che toocopy e incollare i file nella loro UPD ed esplicitamente.

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a>Caricare i file e dati tooa file server mediante copia dei file di rete standard
Spesso le organizzazioni di utilizzare dati generale toostore di file server. Se si conosce il nome di server hello o un percorso, gli utenti possono cercare hello rete locale server hello e quindi copiare i file, analogamente a quanto avveniva in precedenza. Si verrà nuovamente desidera toopublish tooRemoteApp di Esplora File e quindi condividerlo con gli utenti.

> [!NOTE]
> server di file Hello deve trovarsi nella rete instradabile hello RemoteApp è stato distribuito in.
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a>Copiare i file tooOneDrive for Business
Anche se non è possibile abilitare hello OneDrive per agente di sincronizzazione di Business in RemoteApp, è tuttavia possibile copiare file dal tooOneDrive UPD per le aziende tramite un browser. 

1. Pubblicare tooRemoteApp Esplora File e quindi indicare agli utenti tooaccess hello file tramite tale app. 
2. È più semplice tootransfer file se in modalità compressa, in modo gli utenti devono creare un file con estensione zip che contiene tutti gli tooOneDrive toomove di file hello for Business.
3. Chiedere portale per gli utenti toogo toohello Office 365 e quindi passare tooOneDrive e caricare file con estensione zip hello.

## <a name="copy-files-by-using-drive-redirection"></a>Copiare i file usando il reindirizzamento delle unità
Se è stato abilitato il [reindirizzamento delle unità](remoteapp-redirection.md), è già stata creata un'unità mappata per gli utenti. In questo caso, è possibile comprimere i file nell'unità hello reindirizzato e salvarle tootheir PC locale.

## <a name="how-administrators-can-export-data"></a>Modalità di esportazione dei dati degli amministratori

Amministra per Azure RemoteApp è possibile esportare tutti i dischi dei profili utente (UPD) per tutte le raccolte all'interno di un tooAzure sottoscrizione Storage utilizzando Azure PowerShell cmdlet Export-AzureRemoteAppUserDisk.  Non vi è alcuna possibilità tooselect singoli UPD.  Quando viene eseguito il comando di PowerShell hello, ogni disco utente sarà un 50gb di dimensioni di disco fisso e archiviazione tooAzure esportato.  I costi di archiviazione di Azure verranno generati immediatamente per questa risorsa di archiviazione.  Quando l'esecuzione del comando verificare che non sono presenti sessioni in caso contrario hello esportazione avrà esito negativo.

Gli UPD per le distribuzioni di Azure RemoteApp aggiunte a un dominio possono solo essere riusati in una distribuzione di Servizi desktop remoto; non è possibile usare distribuzioni non aggiunte a dominio.  Se tali dischi verranno utilizzati in una distribuzione di servizi desktop remoto, è consigliabile toouse nostri [automatizzata script](https://github.com/arcadiahlyy/aramigration) che verrà esportare, convertire e importare hello del UPD in una distribuzione di servizi desktop remoto.

