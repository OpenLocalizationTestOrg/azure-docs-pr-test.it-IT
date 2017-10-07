---
title: file aaaPersist nella Shell di Cloud di Azure (anteprima) | Documenti Microsoft
description: Procedura dettagliata su come Azure Cloud Shell rende persistenti i file.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>Rendere persistenti i file in Azure Cloud Shell
Shell cloud consente di sfruttare i file toopersist di archiviazione di File di Azure tra le sessioni.

## <a name="set-up-a-clouddrive-file-share"></a>Configurare una condivisione file `clouddrive`
All'avvio iniziale, Shell Cloud richiede tooassociate condivisione file nuovo o esistente di file toopersist tra sessioni.

### <a name="create-new-storage"></a>Creare una nuova risorsa di archiviazione

Quando si utilizzano le impostazioni di base e selezionare solo una sottoscrizione, Shell di Cloud crea tre risorse per conto dell'utente nell'area di hello supportato più vicino al tooyou:
* Gruppo di risorse: `cloud-shell-storage-<region>`
* Account di archiviazione: `cs<uniqueGuid>`
* Condivisione file: `cs-<user>-<domain>-com-<uniqueGuid>`

![impostazioni di sottoscrizione Hello](media/basic-storage.png)

condivisione di file Hello collega come `clouddrive` nel `$Home` directory. Hello condivisione file è anche usato toostore un'immagine di 5 GB che viene creata automaticamente per l'utente e che gli aggiornamenti e viene mantenuta la `$Home` directory. Si tratta di un'azione singola e condivisione di file hello Monta automaticamente nelle sessioni successive.

### <a name="use-existing-resources"></a>Usare le risorse esistenti

Tramite l'opzione avanzata hello, è possibile associare le risorse esistenti. Quando viene visualizzata hello archiviazione installazione richiesta, selezionare **Mostra impostazioni avanzate** tooview ulteriori opzioni. Condivisioni di file esistenti ricevono un toopersist immagine utente 5 GB il `$Home` directory. menu a discesa Hello vengono filtrati per paese Shell Cloud e per gli account di archiviazione con ridondanza geografica e con ridondanza locale.

![impostazione di gruppo di risorse Hello](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>Limitare la creazione di risorse con i criteri delle risorse di Azure
Gli account di archiviazione che si creano in Cloud Shell sono contrassegnati con `ms-resource-usage:azure-cloud-shell`. Se si desidera che gli utenti toodisallow dalla creazione di account di archiviazione in Cloud Shell, creare un [criteri delle risorse di Azure per i tag](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) che vengono attivate da questo tag specifico.

## <a name="how-cloud-shell-works"></a>Funzionamento di Cloud Shell
Shell cloud persiste file tramite entrambi hello dei seguenti metodi:
* Creazione di un'immagine di disco del `$Home` toopersist directory tutti contenuto all'interno di directory hello. immagine del disco Hello viene salvato nella condivisione di file specificato come `acc_<User>.img` in `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, e venga eseguita automaticamente la sincronizzazione delle modifiche.

* Montaggio della condivisione file specificata come `clouddrive` nella directory `$Home` per l'interazione diretta con la condivisione file. `/Home/<User>/clouddrive`viene eseguito il mapping troppo`fileshare.storage.windows.net/fileshare`.
 
> [!NOTE]
> Tutti i file della directory `$Home`, come le chiavi SSH, vengono mantenuti nell'immagine del disco utente archiviata nella condivisione file montata. Applicare le procedure consigliate quando si rendono persistenti le informazioni nella directory `$Home` e nella condivisione file montata.

## <a name="use-hello-clouddrive-command"></a>Hello utilizzare `clouddrive` comando
Con la Shell di Cloud, è possibile eseguire un comando denominato `clouddrive`, che consente di toomanually aggiornamento hello condivisione file che tooCloud montato Shell.
![Comando di "clouddrive" hello in esecuzione](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>Montare un nuovo elemento `clouddrive`

### <a name="prerequisites-for-manual-mounting"></a>Prerequisiti per il montaggio manuale
È possibile aggiornare una condivisione di file hello associata Cloud Shell utilizzando hello `clouddrive mount` comando.

Se si monta una condivisione di file esistente, deve essere l'account di archiviazione hello:
* Archiviazione con ridondanza locale o condivisioni di file di archiviazione con ridondanza geografica toosupport.
* Trovarsi nell'area assegnata. Quando si è onboarding, area hello vengono assegnati toois elencati nella casella Nome gruppo di risorse hello `cloud-shell-storage-<region>`.

### <a name="supported-storage-regions"></a>Aree di archiviazione supportate
Hello Azure file devono risiedere in hello stessa area hello Cloud Shell macchina che si sta montaggio per. I cluster Shell cloud attualmente esistono nel hello seguenti aree:
|Area|Region|
|---|---|
|Americhe|Stati Uniti orientali, Stati Uniti centro-meridionali, Stati Uniti occidentali|
|Europa|Europa settentrionale, Europa occidentale|
|Asia/Pacifico|India centrale, Asia sud-orientale|

### <a name="hello-clouddrive-mount-command"></a>Hello `clouddrive mount` comando

> [!NOTE]
> Se si sta il montaggio di una nuova condivisione file, una nuova immagine utente viene creata per il `$Home` directory, in quanto precedente `$Home` immagine viene mantenuta nella condivisione di file precedente hello.

Eseguire hello `clouddrive mount` con hello seguenti parametri:

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

eseguire ulteriori dettagli, tooview `clouddrive mount -h`, come illustrato di seguito:

![Hello in esecuzione ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>Smontare `clouddrive`
È possibile effettuare lo smontaggio di una condivisione di file della Shell che tooCloud montati in qualsiasi momento. Dopo aver disinstallata la condivisione di file, sarà richiesta toomount un nuovo tooyour preliminare di condivisione file sessione successiva.

un file tooremove condividere dalla Shell di Cloud:
1. Eseguire `clouddrive unmount`.
2. Conoscenza e hello prompt di conferma.

Condivisione di file continuerà tooexist a meno che non si elimina manualmente. Cloud Shell non eseguirà più la ricerca di questa condivisione file nelle sessioni successive.

eseguire ulteriori dettagli, tooview `clouddrive unmount -h`, come illustrato di seguito:

![Hello in esecuzione ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> L'esecuzione di questo comando non elimina alcuna risorsa. Eliminazione manuale di un gruppo di risorse, account di archiviazione o condivisione file che è stato eseguito il mapping tooCloud Shell eliminerà definitivamente la `$Home` immagine di directory e qualsiasi altro file nella condivisione di file. Questa azione non può essere annullata.

## <a name="list-clouddrive-file-shares"></a>Elencare le condivisioni file `clouddrive`
quali condivisione file è montato come toodiscover `clouddrive`, eseguire il seguente hello `df` comando. 

tooclouddrive percorso di file Hello mostra che il nome account di archiviazione e della condivisione file nell'URL hello. Ad esempio, `//storageaccountname.file.core.windows.net/filesharename`

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a>Trasferimento file locali tooCloud Shell
Hello `clouddrive` esegue la sincronizzazione directory con il pannello di archiviazione del portale di Azure hello. Utilizzare questo tooor di file locali pannello tootransfer dalla condivisione di file. Aggiornare i file nella Shell di Cloud viene riflessa nell'archiviazione di file hello GUI quando si aggiorna il pannello hello.

### <a name="download-files"></a>Download dei file

![Elenco di file locali](media/download.png)
1. Nel portale di Azure hello, andare toohello condivisione di file montati.
2. Selezionare il file di destinazione hello.
3. Seleziona hello **scaricare** pulsante.

### <a name="upload-files"></a>Caricare file

![File locali toobe caricato](media/upload.png)
1. Passare tooyour montati condivisione file.
2. Seleziona hello **caricare** pulsante.
3. Selezionare hello o i file che si desidera tooupload.
4. Verificare il caricamento di hello.

Dovrebbe essere file hello che sono accessibili nel `clouddrive` directory nella Shell di Cloud.

## <a name="next-steps"></a>Passaggi successivi
[Avvio rapido di Cloud Shell](quickstart.md) <br>
[Informazioni sull'archiviazione file di Azure](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[Informazioni sui tag di archiviazione](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
