---
title: aaaManage le macchine virtuali tramite Azure PowerShell | Documenti Microsoft
description: "Informazioni sui comandi che è possibile utilizzare attività tooautomate nella gestione delle macchine virtuali."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Gestire le macchine virtuali con Azure PowerShell
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per i comandi PowerShell utilizzando il modello di gestione risorse hello comuni, vedere [qui](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Molte attività si toomanage ogni giorno le macchine virtuali possono essere automatizzate tramite i cmdlet PowerShell di Azure. In questo articolo fornisce comandi di esempio per attività più semplice e tooarticles di collegamenti che mostra i comandi di hello per attività più complesse.

> [!NOTE]
> Se non è ancora stato installato e configurato Azure PowerShell, è possibile ottenere le istruzioni nell'articolo hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
> 
> 

## <a name="how-toouse-hello-example-commands"></a>Come toouse hello comandi di esempio
È necessario tooreplace parte del testo hello in hello comandi con il testo che è appropriato per l'ambiente. Hello < e > simboli indicano il testo è necessario tooreplace. Quando si sostituisce il testo hello, rimuovere i simboli di hello ma lasciare virgolette hello sul posto.

## <a name="get-a-vm"></a>Ottenere una macchina virtuale
Si tratta di un'attività di base che si utilizzerà spesso. Utilizzarlo tooget informazioni su una macchina virtuale, eseguire le attività in una macchina virtuale o ottenere output toostore in una variabile.

tooget informazioni hello macchina virtuale, eseguire questo comando, sostituendo tutti gli elementi di offerta di hello, che includono caratteri hello < e >:

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

hello toostore output in una variabile $vm, eseguire:

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>Accedere tooa VM basate su Windows
Eseguire i comandi seguenti.

> [!NOTE]
> È possibile ottenere macchine virtuali hello e nome del servizio cloud dalla visualizzazione hello di hello **Get-AzureVM** comando.
> 
> $svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< unità e la cartella toostore hello download RDP file del percorso, ad esempio: c:\temp >" $localFile = $localPath + "\" $vmname +"RDP"Get-AzureRemoteDesktopFile - ServiceName $svcName-nome $vmName - LocalPath $localFile-avvio
> 
> 

## <a name="stop-a-vm"></a>Arrestare una macchina virtuale
Eseguire questo comando:

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> Utilizzare questo hello tookeep parametro IP virtuale (VIP) del cloud hello del servizio nel caso in cui è hello ultima VM nel servizio cloud. <br><br> Se si usa il parametro StayProvisioned hello, ancora verrà addebitato per hello macchina virtuale.
> 
> 

## <a name="start-a-vm"></a>Avviare una macchina virtuale
Eseguire questo comando:

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>Collegamento di un disco dati
Questa operazione richiede alcuni passaggi. Innanzitutto, utilizzare hello * * * Add-AzureDataDisk * * * cmdlet tooadd hello toohello $vm oggetto disco. Utilizzare quindi **Update-AzureVM** configurazione hello tooupdate di cmdlet di hello macchina virtuale.

È anche necessario toodecide se tooattach un nuovo disco o uno che contiene dati. Per un nuovo disco, il comando di hello crea file con estensione vhd hello e lo collega.

tooattach un nuovo disco, eseguire questo comando:

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

tooattach un disco dati esistente, eseguire questo comando:

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

tooattach dischi di dati da un file con estensione vhd esistente nell'archiviazione blob, eseguire questo comando:

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Creare una macchina virtuale basata su Windows
una nuova macchina virtuale basato su Windows in Azure, hello seguire le istruzioni riportate in toocreate [toocreate usare Azure PowerShell e preconfigurare macchine virtuali basate su Windows](create-powershell.md). Questo argomento descrive i passaggi di creazione di hello di un set di comandi di Azure PowerShell crea una macchina virtuale basata su Windows che può essere preconfigurata:

* Con l’appartenenza al dominio di Active Directory
* Con Dischi aggiuntivi
* Come membro di un set esistente con carico bilanciato
* Con un indirizzo IP statico

