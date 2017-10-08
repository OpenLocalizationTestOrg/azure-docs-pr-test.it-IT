---
title: "aaaConfigure hello sempre nel gruppo di disponibilità su una macchina virtuale di Azure tramite PowerShell | Documenti Microsoft"
description: "In questa esercitazione Usa risorse che sono state create con il modello di distribuzione classica hello. Utilizzare PowerShell toocreate un gruppo di disponibilità AlwaysOn in Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a>Configurare hello sempre nel gruppo di disponibilità su una macchina virtuale di Azure con PowerShell
> [!div class="op_single_selector"]
> * [Classica: interfaccia utente](../classic/portal-sql-alwayson-availability-groups.md)
> * [Classica: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Prima di iniziare, considerare che ora è possibile completare questa attività nel modello di gestione risorse di Azure. Per le nuove distribuzioni è consigliabile usare il modello di Azure Resource Manager. Vedere [gruppi di disponibilità Always On di SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT]
> È consigliabile che più nuove distribuzioni di usare il modello di gestione risorse hello. Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.

Macchine virtuali di Azure (VM) consente di costo toolower hello gli amministratori del database di un sistema di SQL Server a disponibilità elevata. Questa esercitazione viene illustrato come tooimplement una disponibilità gruppo utilizzando SQL Server Always On end-to-end in un ambiente Azure. Al fine di hello dell'esercitazione hello, la soluzione SQL Server Always On in Azure sarà composta dagli hello seguenti elementi:

* Una rete virtuale contenente più subnet, tra cui una subnet front-end e una back-end.
* Un controller di dominio con un dominio di Active Directory.
* Due macchine virtuali di Server SQL che sono distribuiti toohello subnet di back-end e toohello aggiunti a un dominio di Active Directory.
* Un cluster di failover Windows tre nodi con modello di quorum maggioranza dei nodi di hello.
* Un gruppo di disponibilità con due repliche con commit sincrono di un database di disponibilità.

Questo scenario viene scelto per la semplicità, non per la convenienza o altri fattori di Azure. Ad esempio, è possibile ridurre numero hello di macchine virtuali per un toosave gruppo di disponibilità con due repliche sulle ore di calcolo in Azure tramite il controller di dominio hello come hello quorum condivisione file di controllo in un cluster di failover a due nodi. Questo metodo riduce il numero VM hello rispetto hello di sopra di configurazione.

Questa esercitazione è destinata hello passaggi che sono necessari tooset backup hello tooshow descritto soluzione precedente, senza approfondire i dettagli di hello di ogni passaggio. Di conseguenza, invece che fornisce i passaggi di configurazione GUI hello, viene utilizzato PowerShell scripting tootake si rapidamente tramite ogni passaggio. Questa esercitazione si presuppone l'esempio hello:

* Si dispone già di un account Azure con sottoscrizione di hello macchina virtuale.
* È stato installato hello [cmdlet di Azure PowerShell](/powershell/azure/overview).
* Si ha già una conoscenza approfondita dei gruppi di disponibilità Always On per soluzioni locali. Per altre informazioni, vedere [Gruppi di disponibilità AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a>Connettere tooyour sottoscrizione di Azure e creare la rete virtuale hello
1. In una finestra di PowerShell nel computer locale, importare hello modulo Azure, scaricare hello macchina tooyour file di impostazioni di pubblicazione e connettere il tooyour sessione PowerShell sottoscrizione di Azure importando le impostazioni di pubblicazione scaricato hello.

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    Hello **Get-AzurePublishSettingsFile** comando genera automaticamente un certificato di gestione con Azure e lo scarica tooyour macchina. Viene automaticamente aperto un browser e sei le credenziali dell'account Microsoft hello tooenter richiesta per la sottoscrizione di Azure. Hello scaricato **publishsettings** file contiene tutte le informazioni di hello necessario toomanage la sottoscrizione di Azure. Dopo aver salvato la directory di file tooa locale, importarlo tramite hello **Import-AzurePublishSettingsFile** comando.

   > [!NOTE]
   > file con estensione publishsettings Hello contiene le credenziali (non codificate) vengono utilizzati tooadminister i servizi e le sottoscrizioni di Azure. Hello protezione consigliata per questo file è toostore viene temporaneamente all'esterno delle directory di origine (ad esempio, nella cartella di raccolte\documenti hello) e quindi eliminarlo una volta terminata l'importazione di hello. Un utente malintenzionato ottiene il file con estensione publishsettings toohello di accesso possa modificare, creare ed eliminare i servizi di Azure.

2. Definire una serie di variabili che si userà toocreate l'infrastruttura IT cloud.

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    Prestare attenzione toohello seguente tooensure che i comandi funzionino correttamente in un secondo momento:

   * Le variabili **$storageAccountName** e **$dcServiceName** deve essere univoco perché sono utilizzati tooidentify l'account di archiviazione cloud e il server del cloud, rispettivamente, su hello Internet.
   * i nomi specificati per le variabili di Hello **$affinityGroupName** e **$virtualNetworkName** configurati nel documento di configurazione di rete virtuale hello che verrà utilizzato in un secondo momento.
   * **$sqlImageName** specifica il nome di hello aggiornato dell'immagine di macchina virtuale hello contenente SQL Server 2012 Service Pack 1 Enterprise Edition.
   * Per semplicità, **Contoso! 000** è hello stessa password utilizzata nel corso esercitazione intera hello.

3. Creare un set di affinità.

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. Creare una rete virtuale importando un file di configurazione.

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    file di configurazione Hello contiene hello seguente documento XML. In breve, specifica una rete virtuale denominata **ContosoNET** nel gruppo di affinità hello chiamato **ContosoAG**. Dispone di spazio degli indirizzi hello **10.10.0.0/16** e dispone di due subnet, **10.10.1.0/24** e **10.10.2.0/24**, che sono subnet di hello anteriore e posteriore, rispettivamente. subnet front-Hello è dove è possibile inserire applicazioni client quali Microsoft SharePoint. subnet di back-Hello è in cui inserire le macchine virtuali di hello SQL Server. Se si modifica hello **$affinityGroupName** e **$virtualNetworkName** variabili in precedenza, è necessario modificare anche hello corrispondenti ai nomi.

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. Creare un account di archiviazione associato hello gruppo di affinità creato e impostarlo come account di archiviazione corrente hello nella sottoscrizione.

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. Creare server di controller di dominio hello in hello nuovo cloud service e set di disponibilità.

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    Questi comandi reindirizzati hello seguenti operazioni:

   * **New-AzureVMConfig** consente di creare una configurazione di macchina virtuale.
   * **Aggiungere-AzureProvisioningConfig** offre hello parametri di configurazione di un server Windows autonomo.
   * **Aggiungere-AzureDataDisk** aggiunge il disco dati hello che verrà utilizzato per archiviare i dati di Active Directory, con l'opzione set tooNone di memorizzazione nella cache di hello.
   * **New-AzureVM** crea un nuovo servizio cloud e hello nuova macchina virtuale di Azure nel nuovo servizio cloud di hello.

7. Attendere hello nuova VM toobe stato effettuato il provisioning e scaricare directory di lavoro tooyour hello file desktop remoto. Poiché hello nuova macchina virtuale di Azure accetta un tooprovision molto tempo, hello `while` ciclo continua toopoll hello nuova macchina virtuale finché è pronto per l'utilizzo.

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

server del controller di dominio Hello ora correttamente il provisioning. Successivamente, si configurerà il dominio di Active Directory hello in questo server di controller di dominio. Lasciare aperta la finestra di PowerShell hello nel computer locale. Si userà nuovamente toocreate successive hello due macchine virtuali di SQL Server.

## <a name="configure-hello-domain-controller"></a>Configurare il controller di dominio hello
1. Connessione server di controller di dominio toohello avviando i file del desktop remoto hello. Utilizzare AzureAdmin di nome utente e la password dell'amministratore del computer hello **Contoso! 000**, specificato al momento della creazione hello nuova macchina virtuale.
2. Aprire una finestra di PowerShell in modalità amministratore.
3. Eseguire il seguente hello **DCPROMO. EXE** tooset comando backup hello **corp.contoso.com** dominio, con directory dei dati hello sull'unità M.

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    Al termine del comando hello, hello VM viene riavviato automaticamente.

4. Connettere nuovamente toohello server controller di dominio avviando i file del desktop remoto hello. Questa volta accedere come **CORP\Administrator**.
5. Aprire una finestra di PowerShell in modalità amministratore e importare il modulo di Active Directory PowerShell hello utilizzando hello comando seguente:

        Import-Module ActiveDirectory

6. Eseguire hello seguente dominio di toohello di comandi tooadd tre utenti.

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    **CORP\Install** è tooconfigure utilizzati tutti gli elementi correlati toohello le istanze del servizio SQL Server, il cluster di failover di hello e gruppo di disponibilità hello. **CORP\SQLSvc1** e **CORP\SQLSvc2** vengono utilizzati come account del servizio SQL Server hello per le macchine virtuali di hello due SQL Server.
7. Esempio hello successivo, eseguire i comandi toogive **CORP\Install** hello oggetti computer toocreate di autorizzazioni nel dominio hello.

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    Hello GUID specificato in precedenza è hello GUID per il tipo di oggetto computer hello. Hello **CORP\Install** account deve hello **Leggi tutte le proprietà** e **crea oggetti Computer** hello toocreate autorizzazione Active Directory gli oggetti per il failover hello cluster. Hello **Leggi tutte le proprietà** già autorizzazione tooCORP\Install per impostazione predefinita, pertanto non è necessario toogrant, in modo esplicito. Per ulteriori informazioni sulle autorizzazioni che sono necessari il cluster di failover di toocreate hello, vedere [Guida dettagliata al Cluster di Failover: configurazione di account in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).

    Ora che è stata completata la configurazione di Active Directory e gli oggetti utente hello, viene creata due macchine virtuali di SQL Server e aggiungerle toothis dominio.

## <a name="create-hello-sql-server-vms"></a>Creare macchine virtuali di hello SQL Server
1. Continuare toouse hello PowerShell finestra aperta sul computer locale. Definire hello variabili aggiuntive seguenti:

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    indirizzo IP di Hello **10.10.0.4** viene in genere assegnata toohello prima VM creati in hello **10.10.0.0/16** subnet della rete virtuale di Azure. È necessario verificare che sia questo indirizzo hello del server del controller di dominio eseguendo **IPCONFIG**.
2. Esecuzione hello seguente hello toocreate comandi reindirizzati prima macchina virtuale in cluster di failover hello, denominato **ContosoQuorum**:

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    Si noti segue hello riguardanti hello comando precedente:

   * **Nuovo AzureVMConfig** crea una configurazione della macchina virtuale con nome del set di disponibilità desiderato hello. Hello macchine virtuali successive verranno create con hello stesso nome set di disponibilità in modo che si è aggiunto toohello stesso set di disponibilità.
   * **Aggiungere-AzureProvisioningConfig** join hello dominio di Active Directory toohello macchina virtuale creata.
   * **Set-AzureSubnet** posizioni hello VM nella subnet back-hello.
   * **New-AzureVM** crea un nuovo servizio cloud e hello nuova macchina virtuale di Azure nel nuovo servizio cloud di hello. Hello **DnsSettings** parametro specifica il server DNS hello per i server nel nuovo servizio cloud di hello hello è l'indirizzo IP hello **10.10.0.4**. Questo è l'indirizzo IP di hello del server di controller di dominio hello. Questo parametro è necessario tooenable hello nuove macchine virtuali nel dominio di Active Directory toohello toojoin servizio cloud hello correttamente. Senza questo parametro, è necessario impostare manualmente le impostazioni IPv4 hello del server controller di dominio VM toouse hello come server DNS primario hello dopo hello VM viene eseguito il provisioning e quindi accedere al dominio Active Directory toohello VM hello.
3. Esecuzione hello seguente reindirizzato comandi toocreate hello macchine virtuali di SQL Server, denominata **ContosoSQL1** e **ContosoSQL2**.

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    Si noti segue hello riguardanti hello comandi precedenti:

   * **Nuovo AzureVMConfig** utilizza hello stesso nome di set di disponibilità come server del controller di dominio hello e utilizza hello immagine di SQL Server 2012 Service Pack 1 Enterprise Edition nella raccolta di macchine virtuali hello. Imposta inoltre hello operativo sistema disco tooread sola cache (scrittura non consentita). Si consiglia di migrare hello database file tooa disco dati separato toohello macchina virtuale, collegare e configurarlo senza lettura né scrittura nella cache. Tuttavia, hello successivo consigliato consiste tooremove cache in scrittura sul disco del sistema operativo hello perché non è possibile rimuovere lettura della cache su disco del sistema operativo hello.
   * **Aggiungere-AzureProvisioningConfig** join hello dominio di Active Directory toohello macchina virtuale creata.
   * **Set-AzureSubnet** posizioni hello VM nella subnet back-hello.
   * **Aggiungere-AzureEndpoint** aggiunge endpoint di accesso in modo che le applicazioni client possono accedere a queste istanze di servizi di SQL Server su Internet hello. TooContosoSQL1 e ContosoSQL2, vengono assegnate diverse porte.
   * **New-AzureVM** crea hello nuova VM SQL Server in hello stesso servizio cloud in cui ContosoQuorum. È necessario inserire le macchine virtuali hello in hello stesso servizio cloud se si desidera toobe in hello stesso set di disponibilità.
4. Attendere la directory di lavoro di file del desktop remoto tooyour toobe ogni macchina virtuale completamente il provisioning e toodownload ogni macchina virtuale. Hello `for` ciclo scorre hello tre nuove macchine virtuali ed esegue i comandi di hello all'interno delle parentesi graffe principale hello per ognuno di essi.

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    macchine virtuali di Hello SQL Server viene ora eseguito il provisioning e in esecuzione, ma sono installati con SQL Server con le opzioni predefinite.

## <a name="initialize-hello-failover-cluster-vms"></a>Inizializzare il cluster di failover hello macchine virtuali
In questa sezione, è necessario toomodify hello e tre i server che verrà utilizzato nel cluster di failover hello e installazione di SQL Server hello. In particolare:

* Tutti i server: È necessario hello tooinstall **Clustering di Failover** funzionalità.
* Tutti i server: È necessario tooadd **CORP\Install** come macchina hello **amministratore**.
* Solo ContosoSQL1 e ContosoSQL2: È necessario tooadd **CORP\Install** come un **sysadmin** ruolo nel database predefinito hello.
* Solo ContosoSQL1 e ContosoSQL2: È necessario tooadd **NT AUTHORITY\System** come accesso aggiuntivo con hello queste autorizzazioni:

  * Alterare eventuali gruppi di disponibilità
  * Connettersi a SQL
  * Visualizzare lo stato del server
* Solo ContosoSQL1 e ContosoSQL2: hello **TCP** è già abilitato nella macchina virtuale SQL Server hello. Tuttavia, è comunque necessario firewall hello tooopen per l'accesso remoto di SQL Server.

A questo punto, sei pronto toostart. A partire da **ContosoQuorum**, attenersi alla procedura hello riportata di seguito:

1. Connettersi troppo**ContosoQuorum** avviando i file del desktop remoto hello. Utilizzare nome utente dell'amministratore del computer hello **AzureAdmin** e la password **Contoso! 000**, specificata durante la creazione di macchine virtuali hello.
2. Verificare che i computer hello siano stati aggiunti correttamente troppo**corp.contoso.com**.
3. Attendere hello toofinish di installazione di SQL Server che esegue attività di inizializzazione hello automatizzata prima di procedere.
4. Aprire una finestra di PowerShell in modalità amministratore.
5. Installare la funzionalità Clustering di Failover di Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Aggiungere **CORP\Install** come amministratore locale.

        net localgroup administrators "CORP\Install" /Add
7. Disconnettersi da ContosoQuorum. Le operazioni relative a questo server sono state completate.

        logoff.exe

Inizializzare quindi **ContosoSQL1** e **ContosoSQL2**. Attenersi alla procedura hello seguente, che è identici per entrambe le macchine virtuali di SQL Server.

1. Connettere le macchine virtuali di toohello due SQL Server avviando i file del desktop remoto hello. Utilizzare nome utente dell'amministratore del computer hello **AzureAdmin** e la password **Contoso! 000**, specificata durante la creazione di macchine virtuali hello.
2. Verificare che i computer hello siano stati aggiunti correttamente troppo**corp.contoso.com**.
3. Attendere hello toofinish di installazione di SQL Server che esegue attività di inizializzazione hello automatizzata prima di procedere.
4. Aprire una finestra di PowerShell in modalità amministratore.
5. Installare la funzionalità Clustering di Failover di Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Aggiungere **CORP\Install** come amministratore locale.

        net localgroup administrators "CORP\Install" /Add
7. Importare hello PowerShell Provider per SQL Server.

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. Aggiungere **CORP\Install** come ruolo sysadmin hello per istanza di SQL Server predefinita hello.

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. Aggiungere **NT AUTHORITY\System** come accesso aggiuntivo con autorizzazioni di hello tre descritto in precedenza.

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. Aprire il firewall hello per l'accesso remoto di SQL Server.

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. Disconnettersi da entrambe le macchine virtuali.

         logoff.exe

Infine, si è il gruppo di disponibilità hello tooconfigure pronto. Si userà hello PowerShell Provider per SQL Server tooperform di hello usati per **ContosoSQL1**.

## <a name="configure-hello-availability-group"></a>Configurare il gruppo di disponibilità hello
1. Connettersi troppo**ContosoSQL1** nuovamente avviando i file del desktop remoto hello. Anziché effettuato l'accesso utilizzando l'account del computer hello, accedere utilizzando **CORP\Install**.
2. Aprire una finestra di PowerShell in modalità amministratore.
3. Definire hello seguenti variabili:

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. Importare hello PowerShell Provider per SQL Server.

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. Modificare l'account del servizio SQL Server hello per ContosoSQL1 tooCORP\SQLSvc1.

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. Modificare l'account del servizio SQL Server hello per ContosoSQL2 tooCORP\SQLSvc2.

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. Scaricare **CreateAzureFailoverCluster.ps1** da [creare Cluster di Failover per gruppi di disponibilità AlwaysOn nella macchina virtuale di Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello directory di lavoro locale. Si utilizzerà questo toohelp script creare un cluster di failover funzionale. Per informazioni importanti sull'interazione del Clustering di Failover di Windows con hello Azure di rete, vedere [elevata disponibilità e ripristino di emergenza per SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).
8. Modificare la directory di lavoro tooyour e creare il cluster di failover di hello con script hello scaricato.

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. Abilitare sempre gruppi di disponibilità per le istanze di SQL Server predefinite hello in **ContosoSQL1** e **ContosoSQL2**.

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. Creare una directory di backup e concedere le autorizzazioni per gli account del servizio SQL Server hello. Utilizzare questo database di disponibilità hello tooprepare directory sulla replica secondaria hello.

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. Creare un database in **ContosoSQL1** chiamato **MyDB1**, eseguire un backup completo e un backup del log e ripristinarli su **ContosoSQL2** con hello **WITH NORECOVERY** opzione.

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. Creare endpoint dei gruppi disponibilità hello in hello macchine virtuali di SQL Server e impostare autorizzazioni appropriate di hello sugli endpoint hello.

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. Creare hello repliche di disponibilità.

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. Infine, creare il gruppo di disponibilità hello e gruppo di disponibilità toohello join hello replica secondaria.

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a>Passaggi successivi
SQL Server Always On è stato correttamente implementato mediante la creazione di un gruppo di disponibilità in Azure. tooconfigure un listener per questo gruppo di disponibilità, vedere [configurare un listener del bilanciamento del carico interno per gruppi di disponibilità AlwaysOn in Azure](../classic/ps-sql-int-listener.md).

Per altre informazioni sull'uso di SQL Server in Azure, vedere [Panoramica di SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
