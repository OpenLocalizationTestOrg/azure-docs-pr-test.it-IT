---
title: elenchi di controllo di accesso all'endpoint Azure aaaManage | PowerShell | Classico | Documenti Microsoft
description: Informazioni su come toomanage ACL con PowerShell
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a>Gestire elenchi di controllo di accesso endpoint tramite PowerShell nel modello di distribuzione classica hello
È possibile creare e gestire elenchi controllo accesso rete (ACL) per gli endpoint tramite Azure PowerShell o nel portale di gestione di hello. Questo argomento illustra le procedure per le attività comuni che è possibile eseguire per tali elenchi usando PowerShell. Per l'elenco hello di Azure PowerShell cmdlet vedere [cmdlet di gestione di Azure](http://go.microsoft.com/fwlink/?LinkId=317721). Per altre informazioni sugli elenchi di controllo di accesso, vedere l'articolo relativo alla [definizione di un elenco di controllo di accesso di rete](virtual-networks-acl.md). Se si desidera toomanage gli ACL usando hello portale di gestione, vedere [come configurare gli endpoint di tooSet tooa macchina virtuale](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="manage-network-acls-by-using-azure-powershell"></a>Gestire gli elenchi di controllo di accesso di rete tramite Azure PowerShell
È possibile utilizzare toocreate cmdlet PowerShell di Azure, rimuovere e configurare (set) elenchi controllo accesso rete (ACL). Sono stati inclusi alcuni esempi di alcuni dei modi hello che è possibile configurare un ACL tramite PowerShell.

un elenco completo dei cmdlet di PowerShell ACL hello tooretrieve, è possibile utilizzare uno dei seguenti hello:

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a>Creare un elenco di controllo di accesso di rete con regole che consentano l'accesso da una subnet remota
esempio Hello riportato di seguito viene illustrato un toocreate modo un nuovo ACL contenente regole. Viene quindi applicato l'ACL tooa endpoint della macchina virtuale. regole ACL Hello nel seguente esempio hello consentirà l'accesso da una subnet remota. toocreate un nuovo ACL di rete con regole Consenti per una subnet remota, aprire Azure PowerShell ISE. Copiare e incollare hello script seguente, configurando script hello con i valori desiderati e quindi eseguire script hello.

1. Creare hello nuovo oggetto ACL di rete.
   
        $acl1 = New-AzureAclConfig
2. Impostare una regola che consenta l'accesso da una subnet remota. Nell'esempio hello seguente, si imposta regola *100* (che ha la priorità sulla regola 200 e versioni successiva) della subnet remota hello tooallow *10.0.0.0/8* accedere toohello endpoint della macchina virtuale. Sostituire i valori hello con requisiti di configurazione. nome Hello "SharePoint ACL config" deve essere sostituito con un nome di hello che si desidera toocall questa regola.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. Per altre regole, ripetere il cmdlet hello, sostituendo i valori hello con requisiti di configurazione. Essere certi toochange hello regola numero tooreflect hello ordine in cui si desidera hello regole toobe applicato. Hello regola più basso ha la precedenza sul numero più alto hello.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. Successivamente, è possibile creare un nuovo endpoint (Add) o impostare hello ACL per un endpoint esistente (Set). In questo esempio, si aggiungerà che un nuovo endpoint della macchina virtuale denominata "web" e aggiornamento endpoint della macchina virtuale hello con hello impostazioni ACL.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. Successivamente, combinare i cmdlet di hello ed eseguire script hello. In questo esempio hello cmdlet combinati sarebbe simile al seguente:
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a>Rimuovere una regola dell'elenco di controllo di accesso che consente l'accesso da una subnet remota
esempio Hello riportato di seguito viene illustrato un tooremove modo una regola ACL di rete.  le regole di tooremove una regola ACL di rete con l'autorizzazione per una subnet remota, aprire Azure PowerShell ISE. Copiare e incollare hello script seguente, configurando script hello con i valori desiderati e quindi eseguire script hello.

1. Primo passaggio è l'oggetto ACL di rete di hello tooget per l'endpoint della macchina virtuale hello. Verrà rimossa regola ACL hello. In questo caso, la si rimuoverà in base all'ID regola. Questo verrà rimosso solo hello l'ID regola 0 dall'ACL hello. Non rimuove oggetto ACL hello dall'endpoint della macchina virtuale hello.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. Successivamente, è necessario applicare l'endpoint della macchina virtuale toohello oggetto ACL di rete hello e aggiornare la macchina virtuale hello.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a>Rimuovere un elenco di controllo di accesso di rete dall'endpoint di una macchina virtuale
In alcuni scenari, è possibile tooremove un oggetto ACL di rete da un endpoint della macchina virtuale. toodo che, aprire Azure PowerShell ISE. Copiare e incollare hello script seguente, configurando script hello con i valori desiderati e quindi eseguire script hello.

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a>Passaggi successivi
[Che cos'è un elenco di controllo di accesso di rete?](virtual-networks-acl.md)

