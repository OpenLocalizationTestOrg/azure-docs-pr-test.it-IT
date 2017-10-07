---
title: Guida introduttiva di aaaAzure Cloud Shell (anteprima) | Documenti Microsoft
description: Avvio rapido per hello Shell di Cloud di Azure
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
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a>Guida introduttiva per l'utilizzo di hello Shell di Cloud di Azure

Questo documento illustra in dettaglio come toouse hello Azure Cloud Shell in hello [portale di Azure](https://ms.portal.azure.com/).

## <a name="start-cloud-shell"></a>Avviare Cloud Shell
1. Avviare **Shell Cloud** dal riquadro di spostamento superiore hello di hello portale di Azure <br>
![](media/shell-icon.png)
2. Selezionare una sottoscrizione toocreate un account di archiviazione e condivisione di file di Azure
3. Fare clic su "Create storage" (Crea risorsa di archiviazione)

> [!TIP]
> Si viene automaticamente autenticati per l'interfaccia della riga di comando di Azure 2.0 in ogni sessione.

### <a name="set-your-subscription"></a>Impostare la sottoscrizione
1. Elencare le sottoscrizioni a cui si ha accesso: <br>
`az account list`
2. Impostare la sottoscrizione preferita: <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> La sottoscrizione verrà memorizzata per le sessioni future con `/home/<user>/.azure/azureProfile.json`.

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse
Creare un nuovo gruppo di risorse negli Stati Uniti occidentali denominato "MyRG": <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>Creare una macchina virtuale Linux
Creare una VM Ubuntu nel nuovo gruppo di risorse. Hello Azure CLI 2.0 verrà create le chiavi SSH e hello installazione VM con essi. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> Hello tooauthenticate chiavi pubbliche e private usate la macchina virtuale vengono inseriti in `/User/.ssh/id_rsa` e `/User/.ssh/id_rsa.pub` dall'interfaccia CLI di Azure 2.0 per impostazione predefinita. La cartella .ssh è persistente nell'immagine da 5 GB della condivisione file di Azure collegata.

Il nome utente in questa VM sarà quello usato in Cloud Shell ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>Usare SSH per connettersi alla VM Linux
1. Cercare il nome della macchina virtuale nella barra di ricerca del portale Azure hello
2. Fare clic su "Connetti" ed eseguire: `ssh username@ipaddress`

![](media/sshcmd-copy.png)

Al momento di stabilire una connessione SSH hello, dovrebbe essere prompt di hello Ubuntu iniziale.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>+ Cleaning up 
Eliminare il gruppo di risorse e tutte le risorse al suo interno: <br>
Eseguire `az group delete -n MyRG`

## <a name="next-steps"></a>Passaggi successivi
[Informazioni sull'archiviazione permanente su Cloud Shell](persisting-shell-storage.md) <br>
[Informazioni sull'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/) <br>
[Informazioni sull'archiviazione file di Azure](../storage/files/storage-files-introduction.md) <br>