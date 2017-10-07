---
title: Server aaaRemove e disabilitare la protezione | Documenti Microsoft
description: In questo articolo descrive come insieme di credenziali server toounregister da un ripristino del sito e protezione toodisable per le macchine virtuali e server fisici.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>Rimuovere server e disabilitare la protezione

servizio Azure Site Recovery Hello contribuisce tooyour continuità aziendale e strategia di ripristino di emergenza. servizio Hello Orchestra la replica, failover e il ripristino delle macchine virtuali e server fisici. Macchine possono essere replicati tooAzure o tooa locale secondario data center. Per una rapida panoramica, leggere [Che cos'è Azure Site Recovery?](site-recovery-overview.md)

In questo articolo viene descritto come server toounregister da servizi di ripristino di un insieme di credenziali nel portale di Azure hello e come toodisable protezione per i computer protetti da Site Recovery.

Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="unregister-a-connected-configuration-server"></a>Annullare la registrazione di un server di configurazione connesso

Se si replica le macchine virtuali VMware o tooAzure server fisici Windows/Linux, è possibile annullare la registrazione di un server di configurazione connessa da un insieme di credenziali come indicato di seguito:

1. Disabilitare la protezione delle macchine. In **elementi protetti** > **elementi replicati**, macchina hello rapida > **eliminare**.
2. Annullare l'associazione di tutti i criteri. In **infrastruttura di Site Recovery** > **per VMWare & macchine fisiche** > **criteri di replica**, fare doppio clic su hello criteri associati. Server di configurazione rapida hello > **Dissocia**.
3. Rimuovere qualsiasi server di destinazione master o di elaborazione locale aggiuntivo. In **infrastruttura di Site Recovery** > **per VMWare & macchine fisiche** > **server di configurazione**, server hello pulsante destro del mouse > **Eliminare**.
4. Eliminare il server di configurazione di hello.
5. Disinstallare manualmente il servizio di mobilità hello in esecuzione nel server di destinazione master hello (sarà entrambi un apposito server o in esecuzione nel server di configurazione hello).
6. Disinstallare eventuali server di elaborazione aggiuntivi.
7. Disinstallare il server di configurazione di hello.
8. Nel server di configurazione hello, disinstallare l'istanza di hello di MySQL che è stata installata mediante il ripristino del sito.
9. Nel Registro di sistema di hello hello del server di configurazione eliminare la chiave di hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Annullare la registrazione di un server di configurazione non connesso

Se si replica le macchine virtuali VMware o tooAzure server fisici Windows/Linux, è possibile annullare la registrazione di un server di configurazione non è connesso da un insieme di credenziali come indicato di seguito:

1. Disabilitare la protezione delle macchine. In **elementi protetti** > **elementi replicati**, macchina hello rapida > **eliminare**. Selezionare **Interrompi gestione macchina hello**.
2. Rimuovere qualsiasi server di destinazione master o di elaborazione locale aggiuntivo. In **infrastruttura di Site Recovery** > **per VMWare & macchine fisiche** > **server di configurazione**, server hello pulsante destro del mouse > **Eliminare**.
3. Eliminare il server di configurazione di hello.
4. Disinstallare manualmente il servizio di mobilità hello in esecuzione nel server di destinazione master hello (sarà entrambi un apposito server o in esecuzione nel server di configurazione hello).
5. Disinstallare eventuali server di elaborazione aggiuntivi.
6. Disinstallare il server di configurazione di hello.
7. Nel server di configurazione hello, disinstallare l'istanza di hello di MySQL che è stata installata mediante il ripristino del sito.
8. Nel Registro di sistema di hello hello del server di configurazione eliminare la chiave di hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Annullare la registrazione di un server VMM connesso

Come procedura consigliata, è consigliabile annullare la registrazione server VMM hello quando è connesso tooAzure. In questo modo si garantisce che le impostazioni nel server VMM hello (e su altri server VMM con i cloud associati) vengano pulite correttamente. Si consiglia di rimuovere un server non connesso solo in caso di problema di connettività permanente. Se non è connesso il server VMM hello, sarà necessario toomanually un tooclean script le impostazioni di esecuzione.

1. Arrestare la replica delle macchine virtuali nel cloud nel server VMM si desidera tooremove hello.
2. Eliminare tutti i mapping di rete utilizzati dal cloud nel server VMM si desidera toodelete hello. In **infrastruttura di Site Recovery** > **per System Center VMM** > **Mapping di rete**, fare doppio clic su mapping di rete hello >  **Eliminare**.
3. Annullare l'associazione dei criteri di replica dal cloud nel server VMM si desidera tooremove hello.  In **infrastruttura di Site Recovery** > **per System Center VMM** >  **criteri di replica**, fare doppio clic sul criterio hello associata. Fare doppio clic su cloud hello > **Dissocia**.
4. Eliminare il server VMM hello o nodo attivo di VMM. In **infrastruttura di Site Recovery** > **per System Center VMM** > **server VMM**, server hello rapida >  **Eliminare**.
5. Disinstallare hello Provider manualmente nel server VMM di hello. Se si dispone di un cluster, eseguire la rimozione da tutti i nodi.
6. Se si esegue la replica tooAzure, rimuovere manualmente l'agente di servizi di ripristino di Microsoft hello dagli host Hyper-V nei cloud hello eliminato.



### <a name="unregister-an-unconnected-vmm-server"></a>Annullare la registrazione di un server VMM non connesso

1. Arrestare la replica delle macchine virtuali nel cloud nel server VMM si desidera tooremove hello.
2. Eliminare tutti i mapping di rete utilizzati dal cloud nel server VMM hello che si desidera toodelete. In **infrastruttura di Site Recovery** > **per System Center VMM** > **Mapping di rete**, fare doppio clic su mapping di rete hello >  **Eliminare**.
3. Annotare l'ID di hello del server VMM hello.
4. Annullare l'associazione dei criteri di replica dal cloud nel server VMM si desidera tooremove hello.  In **infrastruttura di Site Recovery** > **per System Center VMM** >  **criteri di replica**, fare doppio clic sul criterio hello associata. Fare doppio clic su cloud hello > **Dissocia**.
5. Eliminare il server VMM hello o nodo attivo. In **infrastruttura di Site Recovery** > **per System Center VMM** > **server VMM**, server hello rapida >  **Eliminare**.
6. Scaricare ed eseguire hello [script di pulizia](http://aka.ms/asr-cleanup-script-vmm) nel server VMM hello. Aprire PowerShell con hello **Esegui come amministratore** opzione criteri di esecuzione hello toochange per l'ambito predefinito (LocalMachine) hello. Nello script hello, specificare ID hello del server VMM si desidera tooremove hello. script Hello rimuove la registrazione e le informazioni dal server hello associazione cloud.
5. Eseguire script di pulizia hello in qualsiasi altro server VMM che contengono cloud che vengono associati a cloud nel server VMM si desidera tooremove hello.
6. Eseguire script di pulizia hello in qualsiasi altro passivi nodi cluster VMM contenenti hello che provider installato.
7. Disinstallare hello Provider manualmente nel server VMM di hello. Se si dispone di un cluster, eseguire la rimozione da tutti i nodi.
8. Se si replica tooAzure, è possibile rimuovere l'agente di servizi di ripristino di Microsoft hello dagli host Hyper-V nei cloud hello eliminato.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Annullare la registrazione di un host Hyper-V in un sito di Hyper-V

Gli host Hyper-V non gestiti da VMM vengono raccolti in un sito di Hyper-V. Rimuovere un host in un sito di Hyper-V nel modo seguente:

1. Disabilitare la replica per le macchine virtuali Hyper-V nell'host di hello.
2. Annullare l'associazione di criteri per il sito Hyper-V hello. In **infrastruttura di Site Recovery** > **per i siti Hyper-V** >  **criteri di replica**, fare doppio clic sul criterio hello associata. Sito hello rapida > **Dissocia**.
3. Eliminare gli host Hyper-V. In **infrastruttura di Site Recovery** > **per System Center VMM** > **host Hyper-V**, server hello rapida >  **Eliminare**.
4. Eliminare il sito Hyper-V hello dopo tutti gli host sono state rimosse da quest'ultimo. In **infrastruttura di Site Recovery** > **per System Center VMM** > **siti Hyper-V**, sito hello rapida >  **Eliminare**.
5. Eseguire lo script seguente in ogni host Hyper-V che è stata rimossa hello. script di Hello pulisce le impostazioni nel server di hello e ne annulla la registrazione dell'insieme di credenziali di hello.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>Disabilitare la protezione per una VM VMware o un server fisico

1. In **elementi protetti** > **elementi replicati**, macchina hello rapida > **eliminare**.
2. In **Rimuovi macchina virtuale** selezionare una delle opzioni seguenti:
    - **Disabilitare la protezione per macchina hello (scelta consigliata)**. Utilizzare questa opzione toostop replica macchina hello. Le impostazioni di Site Recovery verranno rimosse automaticamente. Viene visualizzata solo l'opzione hello seguenti circostanze:
        - **È stato ridimensionato volume VM hello**: quando si ridimensiona un hello volume virtuale computer entra in uno stato critico. Selezionare questa protezione toodisables opzione mantenendo i punti di ripristino in Azure. Quando si abilita di nuovo la protezione per macchina hello, i dati per il volume ridimensionato hello hello sono tooAzure trasferiti.
        - **Eseguire un failover recente**, dopo aver eseguito un failover tootest l'ambiente, selezionare questa opzione toostart proteggere nuovamente il computer locale. Disabilita ogni macchina virtuale e quindi è necessario tooenable protezione per tali nuovamente. Disabilitazione macchina hello con questa impostazione non influisce sulla macchina virtuale di replica hello in Azure. Non disinstallare il servizio di mobilità hello dalla macchina di hello.
    - **Interrompi gestione macchina hello**. Se si seleziona questa opzione, verrà rimossa solo macchina hello dall'insieme di credenziali hello. Le impostazioni di protezione locali per la macchina hello non saranno interessate. impostazioni tooremove macchina hello e tooremove hello macchina da hello sottoscrizione di Azure, è necessario impostazioni hello tooclean, disinstallare il servizio di mobilità hello.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>Disabilitare la protezione per una VM Hyper-V in un cloud VMM

1. In **elementi protetti** > **elementi replicati**, macchina hello rapida > **eliminare**.
2. In **Rimuovi macchina virtuale** selezionare una delle opzioni seguenti:

    - **Disabilitare la protezione per macchina hello (scelta consigliata)**. Utilizzare questa opzione toostop replica macchina hello. Le impostazioni di Site Recovery verranno rimosse automaticamente.
    - **Interrompi gestione macchina hello**. Se si seleziona questa opzione, verrà rimossa solo macchina hello dall'insieme di credenziali hello. Le impostazioni di protezione locali per la macchina hello non saranno interessate. impostazioni tooremove macchina hello e tooremove hello macchina da hello sottoscrizione di Azure, sono necessarie tooclean hello impostazioni backup manualmente, usando le istruzioni di hello seguenti. Si noti che se si seleziona macchina virtuale di toodelete hello e relativi dischi rigidi, essi verranno essere rimosso dal percorso di destinazione hello.

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>Pulire le impostazioni di protezione - sito di replica tooa secondario VMM

Se si seleziona **Interrompi gestione macchina hello** ed è la replica tooa sito secondario, eseguire questo script su hello server primario tooclean le impostazioni di hello per una macchina virtuale primaria hello. Nella console VMM hello fare clic sulla console di VMM PowerShell hello hello PowerShell pulsante tooopen. Sostituire SQLVM1 con nome hello della macchina virtuale.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Nel server VMM secondario hello eseguire questo script tooclean le impostazioni di hello per una macchina virtuale secondaria hello:

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. Nel server VMM secondario hello, aggiornare hello le macchine virtuali nel server host Hyper-V di hello, in modo che hello secondario VM Ottiene rilevato nuovamente nella console VMM hello.
4. cancellare le impostazioni di replica hello nel server VMM hello Hello sopra passaggi. Se si desidera che la replica per la macchina virtuale hello, eseguire lo script seguente oh hello toostop hello macchine virtuali primarie e secondarie. Sostituire SQLVM1 con nome hello della macchina virtuale.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>Pulire le impostazioni di protezione dati - replica tooAzure

1. Se si seleziona **Interrompi gestione macchina hello** e replicare tooAzure, eseguire questo script nel server VMM di origine hello, usando PowerShell dalla console VMM hello.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Hello sopra passaggi cancellare le impostazioni di replica hello nel server VMM hello. replica toostop per la macchina virtuale hello in esecuzione nel server host Hyper-V di hello, eseguire lo script. Sostituire SQLVM1 con nome hello di macchina virtuale e host01.contoso.com con nome hello del server host Hyper-V di hello.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Disabilitare la protezione per una VM Hyper-V in un sito Hyper-V

Utilizzare questa procedura se si esegue la replica di macchine virtuali Hyper-V tooAzure senza un server VMM.

1. In **elementi protetti** > **elementi replicati**, macchina hello rapida > **eliminare**.
2. In **Rimuovi macchina**, è possibile selezionare hello le opzioni seguenti:

   - **Disabilitare la protezione per macchina hello (scelta consigliata)**. Utilizzare questa opzione toostop replica macchina hello. Le impostazioni di Site Recovery verranno rimosse automaticamente.
   - **Interrompi gestione macchina hello**. Se si seleziona questa opzione solo macchina hello verrà rimosso dall'insieme di credenziali hello. Le impostazioni di protezione locali per la macchina hello non saranno interessate. impostazioni tooremove macchina hello e tooremove hello della macchina virtuale da hello sottoscrizione di Azure, sono necessarie tooclean hello impostazioni backup manualmente. Se si seleziona macchina virtuale di toodelete hello e relativi dischi rigidi che verranno rimossi dal percorso di destinazione hello.
3. Se si seleziona **Interrompi gestione macchina hello**, eseguire questo script nel server host Hyper-V di origine di hello, tooremove replica per la macchina virtuale hello. Sostituire SQLVM1 con nome hello della macchina virtuale.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
