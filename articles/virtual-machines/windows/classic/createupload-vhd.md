---
title: immagini aaaCreate e caricamento di una macchina virtuale mediante Powershell | Documenti Microsoft
description: Informazioni su toocreate e caricare un'immagine di Windows Server generalizzata (VHD) con il modello di distribuzione classica hello e Powershell di Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a>Creare e caricare tooAzure un disco rigido virtuale di Windows Server
Questo articolo illustra come tooupload la propria macchina virtuale generalizzata immagine come un disco rigido virtuale (VHD) in modo è possibile utilizzare le macchine virtuali toocreate. Per informazioni dettagliate sui dischi e sui dischi rigidi virtuali in Microsoft Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. È anche possibile [caricare](../upload-generalized-managed.md) una macchina virtuale utilizzando il modello di gestione risorse hello.

## <a name="prerequisites"></a>Prerequisiti
Questo articolo presuppone che l'utente abbia:

* **Una sottoscrizione di Azure** : se non si ha tale sottoscrizione, [è possibile aprire un account Azure per ottenerne gratuitamente una](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
* **[Microsoft Azure PowerShell](/powershell/azure/overview)**  -si dispone di Microsoft Azure PowerShell hello modulo installato e configurato toouse la sottoscrizione.
* **A. File VHD** - archiviato in un file con estensione vhd e la macchina virtuale associata tooa sistema operativo di Windows supportati. Controllare toosee se i ruoli del server hello in esecuzione sul disco rigido virtuale hello sono supportati da Sysprep. Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

    > [!IMPORTANT]
    > formato VHDX Hello non è supportata in Microsoft Azure. È possibile convertire hello disco tooVHD formato Hyper-V Manager oppure hello [cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx). Per informazioni dettagliate, vedere questo [post di blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).

## <a name="step-1-prep-hello-vhd"></a>Passaggio 1: Preparare hello disco rigido virtuale
Prima di caricare hello tooAzure di disco rigido virtuale, è necessario che toobe generalizzato usando lo strumento Sysprep hello. Questa funzione Prepara hello toobe di disco rigido virtuale utilizzato come immagine. Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx). Eseguire il backup hello VM prima di eseguire Sysprep.

È stato installato da macchina virtuale hello hello del sistema operativo per completare hello seguente procedura:

1. Accedi toohello del sistema operativo.
2. Aprire una finestra del prompt dei comandi come amministratore. Modificare anche le directory hello**%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.

    ![Apertura della finestra del Prompt dei comandi](./media/createupload-vhd/sysprep_commandprompt.png)
3. Hello **System Preparation Tool** viene visualizzata la finestra di dialogo.

   ![Avvio di Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. In hello **System Preparation Tool**selezionare **immettere sistema fuori casella guidata** e verificare che **Generalize** è selezionata.
5. In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.
6. Fare clic su **OK**.

## <a name="step-2-create-a-storage-account-and-a-container"></a>Passaggio 2: Creare un account di archiviazione e un contenitore
È necessario un account di archiviazione di Azure in modo che sia un file con estensione vhd hello tooupload sul posto. Questo passaggio illustra come toocreate un account o get hello informazioni è necessario un account esistente. Sostituire le variabili di hello in &lsaquo; tra parentesi quadre &rsaquo; con informazioni personali.

1. Login

    ```powershell
    Add-AzureAccount
    ```

2. Impostare la sottoscrizione di Azure.

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. Creare un nuovo account di archiviazione. nome Hello hello dell'account di archiviazione deve essere univoco, 3 e 24 caratteri. nome di Hello può essere qualsiasi combinazione di lettere e numeri. È inoltre necessario disporre di una posizione, come "Orientale US" toospecify

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. Impostare il nuovo account di archiviazione hello come valore predefinito di hello.

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. Creare un nuovo contenitore.

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a>Passaggio 3: Caricare il file con estensione vhd hello
Hello utilizzare [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) hello tooupload disco rigido virtuale.

Finestra di Azure PowerShell hello utilizzata nel passaggio precedente hello, digitare quanto segue di hello comando e sostituire le variabili di hello in &lsaquo; tra parentesi quadre &rsaquo; con informazioni personali.

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a>Passaggio 4: Aggiungere hello immagine tooyour elenco immagini personalizzate
Hello utilizzare [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello toohello ImageList di immagini personalizzate.

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a>Passaggi successivi
È ora possibile [creare una macchina virtuale personalizzata](createportal.md) utilizzando hello immagine caricata.
