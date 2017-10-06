---
title: aaaMount una condivisione di File di Azure e hello accesso condividono Windows | Documenti Microsoft
description: Montare una condivisione di File di Azure e la condivisione di hello access in Windows.
services: storage
documentationcenter: na
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
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>Montare una condivisione di File di Azure e la condivisione di hello access in Windows
[Archiviazione di Azure File](storage-dotnet-how-to-use-files.md) è facile toouse cloud file sistema Microsoft. Le condivisioni file di Azure possono essere montate in Windows e Windows Server. Questo articolo illustra tre modi diversi toomount una condivisione di File di Azure in Windows: con interfaccia utente di Esplora File, tramite PowerShell e tramite il prompt dei comandi di hello hello. 

Ordine toomount un File di Azure condividono di fuori di hello regione di Azure è ospitato in, ad esempio in locale o in un'area diversa di Azure, hello del sistema operativo deve supportare SMB 3.0. 

La condivisione file di Azure può essere montata nel computer Windows in locale o in una VM di Azure a seconda della versione del sistema operativo, Tabella che segue illustra hello 

| Versione di Windows        | Versione SMB |Montabile in VM di Azure|Montabile in locale|
|------------------------|-------------|---------------------|---------------------|
| Windows 7              | SMB 2.1     | Sì                 | No                  |
| Windows Server 2008 R2 | SMB 2.1     | Sì                 | No                  |
| Windows 8              | SMB 3.0     | Sì                 | Sì                 |
| Windows Server 2012    | SMB 3.0     | Sì                 | Sì                 |
| Windows Server 2012 R2 | SMB 3.0     | Sì                 | Sì                 |
| Windows 10             | SMB 3.0     | Sì                 | Sì                 |

> [!Note]  
> È sempre consigliabile acquisire hello KB più recente per la versione di Windows.

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>Prerequisiti per il montaggio della condivisione file di Azure con Windows 
* **Nome Account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello nome dell'account di archiviazione hello.

* **Chiave dell'Account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello chiave di archiviazione primaria (o secondario). Le chiavi di firma di accesso condiviso non sono attualmente supportate per il montaggio.

* **Assicurarsi che la porta 445 sia aperta**: Archiviazione file di Azure usa il protocollo SMB. SMB comunica sulla porta TCP 445 - controllare toosee se il firewall non blocchi le porte TCP 445 da computer client.

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>Montare hello Azure in una condivisione con Esplora File
> [!Note]  
> Si noti che hello attenendosi alle istruzioni presenti in Windows 10 e possono differire leggermente in versioni precedenti. 

1. **Aprire Esplora File**: si possono eseguire aprendo dal Menu Start hello o premendo scelta Win + E.

2. **Passare l'elemento di "Questo PC" toohello sul lato sinistro hello della finestra hello. Menu hello disponibili nella barra multifunzione hello verrà modificato. Selezionare "Connetti unità di rete" dal menu Computer hello**.
    
    ![Menu a discesa una schermata di hello "Connetti unità di rete"](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. **Percorso UNC di hello copia dal riquadro "Connetti" hello nel portale di Azure hello**: una descrizione dettagliata delle modalità toofind queste informazioni sono reperibili [qui](storage-file-how-to-use-files-portal.md#connect-to-file-share).

    ![percorso UNC Hello dal riquadro Connetti archiviazione dei File di Azure hello](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. **Selezionare la lettera di unità hello e immettere il percorso UNC hello.** 
    
    ![Una schermata della finestra di dialogo "Connetti unità di rete" hello](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. **Hello di utilizzare il nome di Account di archiviazione preceduto da `Azure\` come nome utente hello e una chiave di Account di archiviazione come password hello.**
    
    ![Una schermata della finestra di dialogo hello rete](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. **Usare la condivisione file di Azure nel modo desiderato**.
    
    ![La condivisione file di Azure viene ora montata](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. **Quando si toodismount pronto (o disconnettersi) in una condivisione hello Azure, è possibile farlo facendo clic sulla voce hello per condivisione hello in hello "percorsi di rete" in Esplora File e selezionando "Disconnetti"**.

## <a name="mount-hello-azure-file-share-with-powershell"></a>Montare hello Azure in una condivisione con PowerShell
1. **Comando che segue di hello utilizzare Condivisione di File di Azure hello toomount**: ricordare tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` con le informazioni appropriate hello.

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **Condivisione di File di Azure usare hello in base alle esigenze**.

3. **Al termine, smontare hello Azure condivisione File che utilizza hello comando seguente**.

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> È possibile utilizzare hello `-Persist` parametro `New-PSDrive` toomake hello rest toohello visibile di condivisione File di Azure di hello del sistema operativo mentre montato.

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>Condivisione di File di Azure hello con il prompt dei comandi di montaggio
1. **Comando che segue di hello utilizzare Condivisione di File di Azure hello toomount**: ricordare tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` con le informazioni appropriate hello.

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **Condivisione di File di Azure usare hello in base alle esigenze**.

3. **Al termine, smontare hello Azure condivisione File che utilizza hello comando seguente**.

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> È possibile configurare hello Azure File condivisione tooautomatically riconnettersi al riavvio del sistema per rendere persistenti le credenziali di hello in Windows. comando seguente Hello manterrà le credenziali di hello:
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>Passaggi successivi
Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.

* [Domande frequenti](storage-files-faq.md)
* [Risoluzione dei problemi](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Articoli concettuali e video
* [Archiviazione di file in Azure: un file system SMB nel cloud senza problemi per Windows e Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Come toouse archiviazione di File di Azure con Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Supporto degli strumenti per Archiviazione file di Azure
* [Uso di Azure PowerShell con Archiviazione di Azure](storage-powershell-guide-full.md)
* [Come toouse AzCopy con archiviazione di Microsoft Azure](storage-use-azcopy.md)
* [Con l'archiviazione di Azure hello CLI di Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Risoluzione dei problemi di archiviazione file di Azure](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a>Post di BLOG
* [Archiviazione file di Azure è attualmente disponibile a livello generale](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File storage (Analisi di Archiviazione file di Azure)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introduzione al servizio File di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [La migrazione dei dati tooAzure File](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>riferimento
* [Informazioni di riferimento sulla libreria client di archiviazione per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Riferimento API REST del servizio File](http://msdn.microsoft.com/library/azure/dn167006.aspx)
