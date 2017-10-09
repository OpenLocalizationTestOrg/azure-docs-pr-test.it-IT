---
title: aaaHow tootag una risorsa di macchina virtuale Windows in Azure | Documenti Microsoft
description: Informazioni sull'uso dei tag di una macchina virtuale Windows creata in Azure tramite il modello di distribuzione di gestione risorse di hello
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a>Come tootag una macchina virtuale Windows Azure
Questo articolo descrive diversi modi tootag una macchina virtuale Windows in Azure tramite il modello di distribuzione del hello Gestione risorse. I tag sono coppie chiave/valore definite dall'utente che possono essere inserite direttamente in una risorsa o un gruppo di risorse. Azure supporta attualmente i tag too15 per ogni risorsa e gruppo di risorse. Tag possono essere inseriti su una risorsa in fase di hello della creazione o aggiunta di risorse esistente tooan. Si noti che i tag sono supportati per le risorse create tramite solo modello di distribuzione di gestione delle risorse hello. Se si desidera tootag una macchina virtuale Linux, vedere [come una macchina virtuale di Linux in Azure tootag](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a>Assegnazione di tag tramite PowerShell
toocreate, aggiungere ed eliminare i tag mediante PowerShell, è necessario innanzitutto tooset backup il [ambiente di PowerShell con Gestione risorse di Azure][PowerShell environment with Azure Resource Manager]. Dopo aver completato l'installazione di hello, è possibile inserire tag sulle risorse di calcolo, rete e archiviazione al momento della creazione o dopo la creazione di risorse hello tramite PowerShell. Questo articolo si concentrerà su come visualizzare o modificare tag inseriti nelle macchine virtuali.

Passare innanzitutto tooa macchina virtuale tramite hello `Get-AzureRmVM` cmdlet.

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

Se la macchina virtuale contiene già i tag, tutti i tag di hello verrà quindi visualizzato nella risorsa:

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

Se si desidera tooadd tag tramite PowerShell, è possibile utilizzare hello `Set-AzureRmResource` comando. Nota: Quando si aggiornano i tag tramite PowerShell, i tag vengono aggiornati nel loro complesso. Pertanto se si aggiunge una risorsa tooa tag che dispone già di tag, sarà necessario tooinclude tutti i tag di hello che si desidera toobe posizionato sulla risorsa hello. Di seguito è riportato un esempio di come tooadd ulteriori tag risorsa tooa tramite Cmdlets di PowerShell.

Questo cmdlet prima imposta tutti i tag hello sul *MyTestVM* toohello *$tags* variabile, utilizzando hello `Get-AzureRmResource` e `Tags` proprietà.

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

Hello secondo comando Visualizza tag hello per hello condizione variabile.

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

Hello terzo comando aggiunge un toohello ulteriori tag *$tags* variabile. Si noti utilizzo hello di hello  **+=**  tooappend hello toohello di coppia chiave/valore nuovo *$tags* elenco.

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

quarto comando Hello imposta tutti i tag hello definiti in hello *$tags* toohello variabile assegnato risorsa. In questo caso, è MyTestVM.

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

Hello quinto comando Visualizza tutti i tag hello sulla risorsa hello. Come si può notare, *percorso* è ora definito come un tag con *MyLocation* come valore di hello.

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

toolearn altre informazioni sull'assegnazione di tag tramite PowerShell, estrarre hello [cmdlet delle risorse Azure][Azure Resource Cmdlets].

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni sull'assegnazione di tag delle risorse di Azure, vedere [Panoramica di gestione risorse di Azure] [ Azure Resource Manager Overview] e [tooorganize tag usando le risorse di Azure] [ Using Tags tooorganize your Azure Resources].
* toosee come tag consentono di gestire l'utilizzo delle risorse di Azure, vedere [comprendere la fattura di Azure] [ Understanding your Azure Bill] e [ottenere informazioni approfondite del consumo di risorse di Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
