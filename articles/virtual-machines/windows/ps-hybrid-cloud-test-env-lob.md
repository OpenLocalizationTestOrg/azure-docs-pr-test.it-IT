---
title: ambiente di test dell'applicazione aaaLOB | Documenti Microsoft
description: Informazioni di ambiente per cloud toocreate una basata sul web, applicazione line of business in un ambiente ibrido IT pro o il test di sviluppo.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>Configurazione di un'applicazione LOB basata sul Web in un cloud ibrido per l'esecuzione di test
Questo argomento descrive la creazione di un ambiente cloud ibrido simulato per testare un'applicazione line-of-business basata su Web ospitata in Microsoft Azure. Di seguito è riportata la configurazione risultante hello.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Questa configurazione è costituita da:

* Una rete locale simulato ospitata in Azure (Buongiorno TestLab VNet).
* Una rete virtuale cross-premise ospitata in Azure (TestVNET).
* Una connessione VPN da rete virtuale a rete virtuale.
* Un server LOB basato su web, SQL server e il controller di dominio secondario nella rete virtuale di hello TestVNET.

Questa configurazione rappresenta una base e un punto di partenza comune da cui è possibile:

* Sviluppare e testare le applicazioni LOB ospitate in Internet Information Services (IIS) con un back-end del database di SQL Server 2014 in Azure.
* Eseguire il test di questo carico di lavoro IT basato sul cloud ibrido simulato.

Esistono tre fasi principali toosetting un ambiente di testing cloud ibrida:

1. Configurare l'ambiente di cloud ibrido simulato hello.
2. Configurare i computer hello SQL server (SQL1).
3. Configurare server LOB hello (LOB1).

Questo carico di lavoro richiede una sottoscrizione di Azure. Se si ha una sottoscrizione di MSDN o di Visual Studio, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

Per un esempio di un'applicazione LOB ospitata in Azure di produzione, vedere hello **applicazioni Line of business** progetto iniziale di architettura in [diagrammi dell'architettura Software Microsoft e i disegni](http://msdn.microsoft.com/dn630664).

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>Fase 1: Configurare l'ambiente di cloud ibrido simulato hello
Creare hello [ambiente di test di cloud ibrido simulato](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Perché questo ambiente di test non richiede la presenza di hello del server di hello APP1 in subnet Corpnet hello, è possibile arrestarlo per ora.

Questa è la configurazione corrente.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>Fase 2: Configurare i computer hello SQL server (SQL1)
Dal portale di Azure hello, avviare il computer di DC2 hello se necessario.

Successivamente, creare una macchina virtuale per SQL1 con questi comandi in un prompt dei comandi di Azure PowerShell nel computer locale. Toorunning precedenti questi comandi, immettere hello i valori delle variabili e Rimuovi hello < e > caratteri.

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Utilizzare hello tooSQL1 tooconnect portale Azure utilizzando l'account amministratore locale hello di SQL1.

A questo punto, configurare il test di connettività di base di Windows Firewall regole tooallow e traffico di SQL Server. Da un prompt dei comandi di Windows PowerShell a livello di amministratore in SQL1 eseguire questi comandi.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

comando ping Hello dovrebbe restituire quattro risposte dall'indirizzo IP 192.168.0.4.

Successivamente, aggiungere hello disco dati supplementare in SQL1 come un nuovo volume con lettera dell'unità f: hello.

1. Nel riquadro sinistro hello di Server Manager, fare clic su **servizi File e archiviazione**, quindi fare clic su **dischi**.
2. Nel riquadro contenuti hello in hello **dischi** gruppo, fare clic su **disco 2** (con hello **partizione** impostare troppo**sconosciuto**).
3. Fare clic su **Attività**, quindi su **Nuovo volume**.
4. Hello prima pagina della creazione guidata nuovo Volume hello, scegliere **Avanti**.
5. Nel server di selezionare hello hello e pagina su disco, fare clic su **disco 2**, quindi fare clic su **Avanti**. Quando richiesto, fare clic su **OK**.
6. Specifica dimensioni hello della pagina volume hello hello, scegliere **Avanti**.
7. Pagina hello assegnare tooa unità lettera o una cartella, fare clic su **Avanti**.
8. Nella pagina Impostazioni di hello selezionare il file system, fare clic su **Avanti**.
9. Nella pagina Conferma selezioni per hello, fare clic su **crea**.
10. Al termine, fare clic su **Chiudi**.

Eseguire questi comandi al prompt dei comandi di Windows PowerShell hello in SQL1:

    md f:\Data
    md f:\Log
    md f:\Backup

Successivamente, dominio SQL1 toohello CORP Windows Server Active Directory con i comandi al prompt di Windows PowerShell hello in SQL1.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Account hello CORP\User1 quando viene richiesto di utilizzare le credenziali dell'account di dominio toosupply per hello **Add-Computer** comando.

Dopo il riavvio, usare hello tooconnect portale Azure tooSQL1 *con account di amministratore locale hello di SQL1*.

A questo punto, configurare SQL Server 2014 toouse hello unità f per i nuovi database e le autorizzazioni dell'account utente.

1. Dalla schermata Start hello digitare **SQL Server Management**, quindi fare clic su **SQL Server 2014 Management Studio**.
2. In **connettersi tooServer**, fare clic su **Connetti**.
3. Nel riquadro dell'albero di Esplora oggetti hello, fare doppio clic su **SQL1**, quindi fare clic su **proprietà**.
4. In hello **le proprietà del Server** finestra, fare clic su **le impostazioni del Database**.
5. Individuare hello **percorsi predefiniti Database** e impostare i valori sono i seguenti: 
   * Per **dati**, digitare il percorso hello **f:\Data**.
   * Per **Log**, digitare il percorso hello **f:\Log**.
   * Per **Backup**, digitare il percorso hello **f:\Backup**.
   * Nota: Solo i nuovi database utilizzeranno questi percorsi.
6. Fare clic su hello **OK** finestra hello tooclose.
7. In hello **Esplora oggetti** riquadro dell'albero, aprire **sicurezza**.
8. Fare clic con il pulsante destro del mouse su **Account di accesso**, quindi scegliere **Nuovo account di accesso**.
9. In **Nome account di accesso** digitare **CORP\User1**.
10. In hello **i ruoli del Server** pagina, fare clic su **sysadmin**, quindi fare clic su **OK**.
11. Chiudere Microsoft SQL Server Management Studio.

Questa è la configurazione corrente.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>Fase 3: Configurare il server LOB hello (LOB1)
Innanzitutto, creare una macchina virtuale per LOB1 con questi comandi al prompt dei comandi di Azure PowerShell hello nel computer locale.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Usare quindi hello tooconnect portale Azure tooLOB1 con le credenziali di hello dell'account di amministratore locale hello del LOB1.

Configurare quindi il traffico tooallow una regola Windows Firewall per verificare la connettività di base. Da un prompt dei comandi di Windows PowerShell a livello di amministratore in LOB1 eseguire questi comandi.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

comando ping Hello dovrebbe restituire quattro risposte dall'indirizzo IP 192.168.0.4.

Aggiungere quindi LOB1 toohello CORP dominio Active Directory con questi comandi al prompt di Windows PowerShell hello.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Account hello CORP\User1 quando viene richiesto di utilizzare le credenziali dell'account di dominio toosupply per hello **Add-Computer** comando.

Dopo il riavvio, usare hello tooconnect portale Azure tooLOB1 con hello CORP\User1 account e password.

Configurare LOB1 per IIS e verificare l'accesso da CLIENT1.

1. In Server Manager fare clic su **Aggiungi ruoli e funzionalità**.
2. In hello **prima di iniziare** pagina, fare clic su **Avanti**.
3. In hello **Selezione tipo di installazione** pagina, fare clic su **Avanti**.
4. In hello **Selezione server di destinazione** pagina, fare clic su **Avanti**.
5. In hello **i ruoli del Server** pagina, fare clic su **Server Web (IIS)** nell'elenco di hello di **ruoli**.
6. Quando richiesto, fare clic su **Aggiungi funzionalità**, quindi su **Avanti**.
7. In hello **Selezione funzionalità** pagina, fare clic su **Avanti**.
8. In hello **Server Web (IIS)** pagina, fare clic su **Avanti**.
9. In hello **Selezione servizi ruolo** pagina, selezionare o deselezionare le caselle di controllo hello per i servizi di hello è necessario per il test dell'applicazione LOB e quindi fare clic su **Avanti**.
10. In hello **Conferma selezioni per l'installazione** pagina, fare clic su **installare**.
11. Attendere finché non viene completata l'installazione di hello dei componenti e quindi fare clic su **Chiudi**.
12. Dal portale di Azure hello, connettere computer CLIENT1 toohello con le credenziali dell'account di hello CORP\User1 e quindi avviare Internet Explorer.
13. Nella barra degli indirizzi hello digitare **http://lob1/** e quindi premere INVIO. Si dovrebbe vedere pagina web di IIS 8 predefinita hello.

Questa è la configurazione corrente.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Questo ambiente è ora pronto per toodeploy è basata sul web applicazione sulle funzionalità LOB1 e i test da CLIENT1 nella subnet Corpnet hello.

## <a name="next-step"></a>Passaggio successivo
* Aggiungere una nuova macchina virtuale utilizzando hello [portale di Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

