---
title: "un Listener esterno per gruppi di disponibilità AlwaysOn aaaConfigure | Documenti Microsoft"
description: "Questa esercitazione viene illustrato sono illustrati i passaggi della creazione di un sempre nel gruppo di disponibilità in Azure che è accessibile dall'esterno tramite hello indirizzo IP virtuale pubblico di hello servizio cloud associato."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>Configurare un listener esterno per i gruppi di disponibilità AlwaysOn in Azure
> [!div class="op_single_selector"]
> * [Listener interno](../classic/ps-sql-int-listener.md)
> * [Listener esterno](../classic/ps-sql-ext-listener.md)
> 
> 

In questo argomento viene illustrato come tooconfigure un listener per un gruppo di disponibilità AlwaysOn esternamente accessibile su hello internet. Ciò viene realizzato mediante l'associazione del servizio cloud hello **IP virtuale pubblico (VIP)** indirizzo con il listener hello.

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

Il gruppo di disponibilità può contenere repliche solo locali, solo di Azure oppure sia locali che di Azure per le configurazioni ibride. Le repliche di Azure possono risiedere all'interno di hello stessa area o in più aree tramite più reti virtuali (Vnet). procedura di Hello seguente si supponga di avere già [configurato un gruppo di disponibilità](../classic/portal-sql-alwayson-availability-groups.md) ma non è stato configurato un listener.

## <a name="guidelines-and-limitations-for-external-listeners"></a>Linee guida e limitazioni per listener esterni
Si noti hello indicazioni sui listener del gruppo di disponibilità di hello in Azure durante la distribuzione utilizzando hello pubbliche VIP indirizzo del servizio cloud:

* listener del gruppo di disponibilità Hello è supportato in Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.
* un'applicazione Hello client deve trovarsi in un servizio cloud diverso da hello uno che contiene il gruppo di disponibilità, le macchine virtuali. Azure non supporta server diretto restituire con client e server in hello stesso servizio cloud.
* Per impostazione predefinita, hello passaggi in questo articolo viene illustrato come hello toouse di un listener tooconfigure cloud indirizzo IP virtuale (VIP) del servizio. Tuttavia, è possibile tooreserve e creare più indirizzi VIP per il servizio cloud. In questo modo i passaggi di hello toouse in questo articolo di toocreate più listener di ognuna delle quali è associato a un indirizzo IP virtuale diverso. Per informazioni su come toocreate più indirizzi VIP, vedere [più indirizzi VIP per il servizio cloud](../../../load-balancer/load-balancer-multivip.md).
* Se si sta creando un listener per un ambiente ibrido, rete locale hello deve avere connettività toohello rete Internet pubblica in aggiunta toohello VPN da sito a sito con rete virtuale di Azure hello. Quando in hello subnet di Azure, i listener del gruppo di disponibilità hello è raggiungibile solo tramite indirizzo IP pubblico hello di hello rispettivo servizio cloud.
* Non è supportato un listener esterno in hello stesso cloud in cui è anche un listener interno utilizzando servizio toocreate hello del servizio di bilanciamento del carico interno (ILB).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Determinare l'accessibilità di hello del listener hello
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Questo articolo illustra la creazione di un listener che usa il **bilanciamento del carico esterno**. Se si desidera che un listener di rete virtuale privata tooyour, vedere versione di hello di questo articolo viene descritta la procedura per la configurazione di un [listener con bilanciamento del carico interno](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Creare endpoint VM con bilanciamento del carico con Direct Server Return
Bilanciamento del carico esterno utilizza hello hello virtuale indirizzo IP virtuale pubblico del servizio cloud hello che ospita le macchine virtuali. È necessario toocreate né configurare il bilanciamento del carico di hello in questo caso.

È necessario creare un endpoint con carico bilanciato per ogni macchina virtuale che ospita una replica di Azure. Se si dispongono di repliche in più aree, ogni replica per tale area deve essere in hello stesso cloud servizio hello stessa rete virtuale. Le repliche di creazione del gruppo di disponibilità che si estendono su più aree di Azure richiedono la configurazione di più reti virtuali. Per ulteriori informazioni sulla configurazione della connettività di rete virtuale cross, vedere [tooVNet configurare connettività](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. Nel portale di Azure hello, passare tooeach macchina virtuale che ospita una replica e visualizzare i dettagli di hello.
2. Fare clic su hello **endpoint** scheda per ognuna delle macchine virtuali hello.
3. Verificare che hello **nome** e **porta pubblica** dell'endpoint di listener hello desiderato toouse non è già in uso. Nel seguente esempio hello hello nome è "MyEndpoint" e porta hello è "1433".
4. Nel client locale, scaricare e installare [modulo PowerShell più recente di hello](https://azure.microsoft.com/downloads/).
5. Avviare **Azure PowerShell**. Un nuovo PowerShell sessione viene aperto con hello moduli amministrativi di Azure caricati.
6. Eseguire **Get-AzurePublishSettingsFile**. Questo cmdlet conduce toodownload browser tooa pubblica Impostazioni tooa locale directory del file. Se richiesto, immettere le credenziali di accesso per la sottoscrizione di Azure.
7. Eseguire hello **Import-AzurePublishSettingsFile** comando con il percorso di hello di hello pubblicare file di impostazioni che è stato scaricato:
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    Dopo la pubblicazione hello viene importato il file di impostazioni, è possibile gestire la sottoscrizione di Azure nella sessione di PowerShell hello.
    
1. Copiare script di PowerShell hello seguente in un editor di testo e impostare hello i valori delle variabili toosuit ambiente (i valori predefiniti sono stati specificati per alcuni parametri). Si noti che se il gruppo di disponibilità si estende su aree di Azure, è necessario eseguire hello script una volta in ogni Data Center per servizio cloud hello e i nodi che si trovano in Data Center in questione.
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. Dopo aver impostato le variabili di hello, hello copia crearne uno script dall'editor di testo hello nel toorun sessione PowerShell di Azure. Se il messaggio hello viene comunque mostrata >>, digitare nuovamente script hello che toomake viene avviata l'esecuzione.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Se necessario, verificare che KB2854082 sia installato.
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Aprire le porte del firewall hello nei nodi di gruppo di disponibilità
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Creare listener del gruppo di disponibilità hello

Creare listener del gruppo di disponibilità hello in due passaggi. Innanzitutto, creare la risorsa di cluster punto di accesso client hello e configurare le dipendenze. In secondo luogo, è possibile configurare le risorse cluster hello con PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Creare il punto di accesso client hello e configurare le dipendenze di cluster hello
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Configurare le risorse di cluster hello in PowerShell
1. Per il bilanciamento del carico esterno, è necessario ottenere hello indirizzo IP virtuale pubblico del servizio cloud hello che contiene le repliche. Accedere hello portale di Azure. Passare servizio cloud toohello che contiene le VM del gruppo di disponibilità. Aprire hello **Dashboard** visualizzazione.
2. Indirizzo hello indicato nella nota **indirizzo IP virtuale pubblico (VIP)**. Se la soluzione interessa più reti virtuali, ripetere questo passaggio per ogni servizio cloud che contiene una macchina virtuale che ospita una replica.
3. In uno dei hello macchine virtuali, copiare hello script di PowerShell seguente in un editor di testo e impostare le variabili di hello toohello valori annotati in precedenza.
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. Una volta impostato le variabili di hello, aprire una finestra di Windows PowerShell con privilegi elevata, quindi copiare hello script dall'editor di testo hello e incollarlo nel toorun sessione PowerShell di Azure. Se il messaggio hello viene comunque mostrata >>, digitare nuovamente script hello che toomake viene avviata l'esecuzione.
5. Ripetere questo passaggio su ogni macchina virtuale. Questo script configura risorsa indirizzo IP hello con indirizzo IP di hello del servizio cloud hello e imposta altri parametri come porta probe hello. Quando hello risorsa indirizzo IP viene portata online, può quindi rispondere toohello polling sulla porta probe hello dall'endpoint con bilanciamento del carico hello creata precedentemente in questa esercitazione.

## <a name="bring-hello-listener-online"></a>Portare online listener hello
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Operazioni di completamento della procedura
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>Listener del gruppo di disponibilità hello test (hello nella stessa rete virtuale)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>Listener del gruppo di disponibilità hello test (su hello internet)
In ordine tooaccess hello listener dalla rete virtuale esterna hello, è necessario utilizzare il bilanciamento del carico esterno e public (descritto in questo argomento) invece di bilanciamento del carico interno, ovvero eseguire l'accesso solo all'interno di hello stessa rete virtuale. Nella stringa di connessione hello, specificare nome del servizio cloud hello. Ad esempio, se si dispone di un servizio cloud con nome hello *mycloudservice*, istruzione sqlcmd hello sarebbe come indicato di seguito:

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

A differenza di esempio precedente hello necessario utilizzare l'autenticazione di SQL, perché il chiamante di hello non è possibile utilizzare l'autenticazione di windows su hello internet. Per altre informazioni, vedere il blog relativo a un [gruppo di disponibilità AlwaysOn nelle VM di Azure: scenari di connettività client](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx). Quando si utilizza l'autenticazione di SQL, assicurarsi che crei hello stesso account di accesso in entrambe le repliche. Per ulteriori informazioni sulla risoluzione dei problemi degli account di accesso con gruppi di disponibilità, vedere [come account di accesso toomap o utilizzare contenuti SQL utente tooconnect tooother repliche di database ed eseguire il mapping database tooavailability](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).

Se hello AlwaysOn repliche si trovano in subnet diverse, i client devono specificare **MultisubnetFailover = True** nella stringa di connessione hello. Di conseguenza tooreplicas tentativi di connessione parallela in subnet diverse hello. Si noti che questo scenario include la distribuzione di un gruppo di disponibilità AlwaysOn tra più aree.

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

