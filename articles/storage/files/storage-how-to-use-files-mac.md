---
title: condivisione di File di Azure aaaMount su SMB con macOS | Documenti Microsoft
description: Informazioni su come condividere un File di Azure toomount su SMB con macOS.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>Montare una condivisione file di Azure tramite SMB con macOS
[Archiviazione di Azure File](../storage-dotnet-how-to-use-files.md) il servizio che consente di toocreate e utilizzare condivisioni di file di rete in hello Azure utilizza standard di settore hello. Le condivisioni file di Azure possono essere montate in macOS Sierra (10.12) ed El Capitan (10.11). Questo articolo illustra due modi diversi toomount una condivisione di File di Azure in macOS con hello dell'interfaccia utente di ricerca e l'utilizzo di hello Terminal.

> [!Note]  
> Prima di montare una condivisione file di Azure tramite SMB, è consigliabile disabilitare la firma dei pacchetti SMB. Operazione non può produrre un peggioramento delle prestazioni quando si accede a una condivisione hello Azure da macOS. La connessione SMB verrà crittografata, pertanto non influisce sulla protezione hello della connessione. Da hello terminal, hello seguenti comandi disabiliterà la firma dei pacchetti SMB, come descritto da questa [articolo del supporto tecnico Apple sulla disabilitazione di firma dei pacchetti SMB](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>Prerequisiti per il montaggio di una condivisione file di Azure in macOS
* **Nome account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello nome dell'account di archiviazione hello.

* **Chiave dell'account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello chiave di archiviazione primaria (o secondario). Le chiavi di firma di accesso condiviso non sono attualmente supportate per il montaggio.

* **Assicurarsi che la porta 445 sia aperta**: SMB comunica tramite la porta TCP 445. Nel computer client (Buongiorno Mac), verificare che il firewall non blocchi la porta TCP 445 toomake.

## <a name="mount-an-azure-file-share-via-finder"></a>Montare una condivisione file di Azure tramite il Finder
1. **Aprire il Finder**: Finder è aperto in macOS per impostazione predefinita, ma è possibile assicurarsi sia hello attualmente selezionato applicazione facendo clic sul pulsante hello "macOS faccia icona" nella finestra di ancoraggio hello:  
    ![icona di affrontare macOS Hello](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)

2. **Selezionare "Connect tooServer" hello "Go" Menu**: il percorso UNC hello da hello [prerequisiti](#preq), convertire hello inizio doppia barra rovesciata (`\\`) troppo`smb://` e tutte le altre barre rovesciate (`\`) barre di tooforwards (`/`). Il collegamento dovrebbe essere simile hello seguente: ![finestra di dialogo "Connect tooServer" hello](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)

3. **Utilizzare hello condivisione nome e l'archiviazione chiave dell'account quando viene richiesto un nome utente e password**: quando si fa clic su "Connetti" nella finestra di dialogo "Connect tooServer" hello, verrà richiesto di hello username e password (sarà autopopulated con il macOS nome utente). È possibile hello inserimento chiave dell'account di archiviazione di nome/condivisione hello nel portachiavi di Mac OS.

4. **Condivisione di File di Azure usare hello in base alle esigenze**: dopo la sostituzione di hello condivisione nome e l'archiviazione chiave dell'account in utente hello e la password, verrà montato condivisione hello. È possibile utilizzare questo in genere si utilizza una condivisione di file/cartella locale, tra cui trascinando e rilasciando i file nella condivisione di file hello:

    ![Snapshot di una condivisione file di Azure montata](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Montare una condivisione file di Azure tramite il terminale
1. Sostituire `<storage-account-name>` con nome hello dell'account di archiviazione. Specificare la chiave dell'account di archiviazione come password quando viene chiesta. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Condivisione di File di Azure usare hello in base alle esigenze**: condivisione di File di Azure hello verrà montata il punto di montaggio hello specificato dal comando precedente hello.  

    ![Uno snapshot della condivisione di File di Azure hello montato](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Passaggi successivi
Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.

* [Articolo del supporto tecnico Apple - come tooconnect con la condivisione File su Mac](https://support.apple.com/HT204445)
* [Domande frequenti](../storage-files-faq.md)
* [Risoluzione dei problemi in Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Risoluzione dei problemi in Linux](storage-troubleshoot-linux-file-connection-problems.md)    