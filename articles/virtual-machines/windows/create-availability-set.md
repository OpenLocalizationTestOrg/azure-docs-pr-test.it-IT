---
title: "Imposta aaaCreate la disponibilità di una macchina virtuale in Azure | Documenti Microsoft"
description: "Informazioni su come imposta toocreate una disponibilità gestito o non gestita disponibilità impostato per le macchine virtuali tramite Azure PowerShell o hello portale nel modello di distribuzione di gestione risorse di hello."
keywords: "set di disponibilità"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Aumentare la disponibilità per una macchina virtuale tramite la creazione di un set di disponibilità di Azure 
Set di disponibilità di forniscono all'applicazione tooyour di ridondanza. È consigliabile raggruppare due o più macchine virtuali in un set di disponibilità. Questa configurazione assicura che durante un evento di manutenzione pianificato o non pianificato, almeno una macchina virtuale sarà disponibile e soddisfa hello pari al 99,95% SLA di Azure. Per ulteriori informazioni, vedere hello [contratto di servizio per le macchine virtuali](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Macchine virtuali devono essere create in hello stesso gruppo di risorse come set di disponibilità hello.
> 

Se si desidera la parte toobe VM di un set di disponibilità, è necessario che la disponibilità di hello toocreate impostare prima o durante la sta creando la prima macchina virtuale nel set di hello. Se la macchina virtuale utilizza dischi gestiti, è necessario creare set di disponibilità hello come un set di disponibilità gestito.

Per ulteriori informazioni sulla creazione e utilizzo di set di disponibilità, vedere [gestione hello disponibilità delle macchine virtuali](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a>Utilizzare toocreate portale hello un set prima di creare le macchine virtuali di disponibilità
1. Nel menu hub hello, fare clic su **Sfoglia** e selezionare **set di disponibilità**.
2. In hello **disponibilità imposta pannello**, fare clic su **Aggiungi**.
   
    ![Schermata che mostra hello pulsante Aggiungi per creare un nuovo set di disponibilità.](./media/create-availability-set/add-availability-set.png)
3. In hello **creare set di disponibilità** pannello, le informazioni di hello completo per il set.
   
    ![Schermata che mostra hello informazioni sono necessarie tooenter toocreate hello disponibilità impostato.](./media/create-availability-set/create-availability-set.png)
   
   * **Nome** -nome hello deve essere costituiti da numeri, lettere, punti, caratteri di sottolineatura e trattini, caratteri di 1-80. Hello primo carattere deve essere una lettera o un numero. ultimo carattere Hello deve essere una lettera, numero o un carattere di sottolineatura.
   * **Domini di errore** -domini di errore definiscono gruppo hello delle macchine virtuali che condividono un commutatore power di origine e di rete comune. Per impostazione predefinita, le macchine virtuali hello sono separate tra i domini di errore toothree e possono essere modificate toobetween 1 e 3.
   * **Domini di aggiornamento** : cinque domini di aggiornamento vengono assegnati per impostazione predefinita e può essere impostata toobetween 1 e 20. Indicano i domini di aggiornamento gruppi di macchine virtuali e l'hardware fisico sottostante che può essere riavviata in hello contemporaneamente. Ad esempio, se si specifica update cinque domini, quando sono configurate più di cinque macchine virtuali all'interno di un singolo Set di disponibilità, macchina virtuale sesto hello saranno inseriti hello stesso dominio di aggiornamento come macchina virtuale prima di hello, hello settimo hello stesso UD come hello seconda macchina virtuale e così via. ordine di Hello di riavvii hello potrebbe non essere sequenziale, ma verrà riavviato in una fase di aggiornamento di un solo dominio.
   * **Sottoscrizione** -selezionare hello toouse sottoscrizione se si dispone di più di uno.
   * **Gruppo di risorse** -selezionare un gruppo di risorse esistente facendo clic sulla freccia di hello e selezionando un gruppo di risorse di hello elenco a discesa. È inoltre possibile creare un nuovo gruppo di risorse digitando un nome. Hello nome può contenere nessuno dei hello seguenti caratteri: lettere, numeri, punti, trattini, caratteri di sottolineatura e apertura o la parentesi di chiusura. nome Hello non può terminare con un punto. Tutti i hello macchine virtuali nel gruppo di disponibilità hello necessario toobe creato in hello stesso gruppo di risorse come set di disponibilità hello.
   * **Percorso** -selezionare un percorso dall'elenco a discesa hello.
   * **Gestito** : selezionare questa opzione *Sì* toocreate una disponibilità gestito imposta toouse con macchine virtuali che usano dischi gestiti per l'archiviazione. Selezionare **n** se le macchine virtuali presenti nel set di hello hello Usa i dischi non gestiti in un account di archiviazione.
   
4. Una volta immesse le informazioni di hello, fare clic su **crea**. 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a>Utilizzare una macchina virtuale e una disponibilità impostazione hello stesso la toocreate portale hello ora
Se si sta creando una nuova macchina virtuale tramite il portale di hello, è inoltre possibile creare un nuovo set di disponibilità per hello VM durante la creazione di hello prima macchina virtuale nel set di hello. Se si sceglie di dischi gestiti toouse per la macchina virtuale, verrà creato un set di disponibilità gestito.

![Screenshot che illustra il processo di hello per la creazione di un nuovo set durante la creazione di VM hello di disponibilità.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a>Aggiungere una nuova macchina virtuale tooan esistente set di disponibilità nel portale di hello
Per ogni VM aggiuntive che crei che deve appartenere nel set di hello, assicurarsi che venga creato in hello stesso **gruppo di risorse** e quindi selezionare hello set nel passaggio 3 di disponibilità esistente. 

![Screenshot che illustra come impostare toouse di tooselect un gruppo di disponibilità per la macchina virtuale.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a>Utilizzare PowerShell toocreate una disponibilità impostato
Questo esempio viene creato un set denominato di disponibilità **myAvailabilitySet** in hello **myResourceGroup** gruppo di risorse in hello **Stati Uniti occidentali** percorso. Questa operazione deve toobe eseguita prima di creare hello prima macchina virtuale che verrà aggiunto il set di hello.

Prima di iniziare, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello. Eseguire hello seguenti comando tooinstall.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).


Se si usano dischi gestiti per le macchine virtuali, digitare:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

Se si usa il proprio account di archiviazione per le macchine virtuali, digitare:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

Per ulteriori informazioni, vedere [New AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).

## <a name="troubleshooting"></a>Risoluzione dei problemi
* Quando si crea una macchina virtuale, se il set di disponibilità hello desiderato non è nell'elenco a discesa hello nel portale di hello si potrebbe avere creati in un gruppo di risorse diverso. Se non si conosce il gruppo di risorse hello per la disponibilità del set di fare clic su Sfoglia e passare menu hub toohello > toosee imposta un elenco della disponibilità e i gruppi di risorse che appartengono a gruppi di disponibilità.

## <a name="next-steps"></a>Passaggi successivi
Aggiungere ulteriore spazio di archiviazione tooyour VM aggiungendo un ulteriore [disco dati](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

