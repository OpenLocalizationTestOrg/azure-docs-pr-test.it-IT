---
title: un controller di dominio Active Directory di replica in Azure aaaInstall | Documenti Microsoft
description: Un'esercitazione che illustra come tooinstall un controller di dominio da un server di Active Directory locale dell'insieme di strutture in una macchina virtuale di Azure.
services: virtual-network
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8c9ebf1b-289a-4dd6-9567-a946450005c0
ms.service: virtual-network
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 74876fce2ca2a29f02c2828f9b3a21227248233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-replica-active-directory-domain-controller-in-an-azure-virtual-network"></a>Installazione di un controller di dominio Active Directory di replica in una rete virtuale di Azure
Questo argomento viene illustrato come controller di dominio aggiuntivi tooinstall (noto anche come replica controller di dominio) per un dominio di Active Directory locale in macchine virtuali di Azure (VM) in una rete virtuale di Azure.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.

Altri argomenti di interesse:

* È possibile, se lo si desidera, installare una nuova foresta Active Directory in una rete virtuale di Azure. Per questa procedura, vedere [Installazione di una nuova foresta Active Directory in una rete virtuale di Azure](active-directory-new-forest-virtual-machine.md).
* Per le linee guida concettuali sull'installazione di Servizi di dominio Active Directory in una rete virtuale di Azure, vedere [Linee guida per la distribuzione di Active Directory di Windows Server in macchine virtuali di Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Diagramma dello scenario
In questo scenario, gli utenti esterni devono tooaccess di applicazioni per i server di dominio. Hello macchine virtuali che eseguono Server applicazione hello e hello i controller di dominio di replica vengono installati in una rete virtuale di Azure. Hello rete virtuale può essere connesso toohello rete locale da un [VPN site-to-site](../vpn-gateway/vpn-gateway-site-to-site-create.md) connessione, come illustrato nell'esempio hello diagramma oppure è possibile utilizzare [ExpressRoute](../expressroute/expressroute-locations-providers.md) per una connessione più veloce.

hello controller di dominio e server applicazioni Hello vengono distribuiti all'interno di servizi cloud separato toodistribute calcolo l'elaborazione e all'interno [set di disponibilità](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) per una migliore tolleranza di errore.
i controller di dominio di Hello replicare tra loro e con i controller di dominio locale utilizzando la replica di Active Directory. Non sono necessari strumenti di sincronizzazione.

![Diagramma di un controller di dominio Active Directory di replica in una rete virtuale di Azure][1]

## <a name="create-an-active-directory-site-for-hello-azure-virtual-network"></a>Creare un sito di Active Directory per hello rete virtuale di Azure
È un toocreate buona un sito in Active Directory che rappresenta hello rete area toohello della rete virtuale corrispondente. Ciò contribuisce a ottimizzare l'autenticazione, la replica e altre operazioni del percorso del controller di dominio. Hello passaggi seguenti illustrano come toocreate un sito e per ulteriori informazioni, vedere [aggiunta di un nuovo sito](https://technet.microsoft.com/library/cc781496.aspx).

1. Aprire Siti e servizi di Active Directory: **Server Manager** > **Strumenti** > **Siti e servizi di Active Directory**.
2. Creare un'area di hello toorepresent sito creato in una rete virtuale di Azure: fare clic su **siti** > **azione** > **nuovo sito** > tipo nome Hello del nuovo sito hello, ad esempio Azure Stati Uniti occidentali > selezionare un collegamento di sito > **OK**.
3. Creare una subnet e associare al nuovo sito hello: fare doppio clic su **siti** > destro **subnet** > **nuova subnet** > digitare l'intervallo di indirizzi IP di hello rete virtuale di Hello (ad esempio 10.1.0.0/16 nel diagramma dello scenario hello) > Seleziona hello nuovo sito di Azure > **OK**.

## <a name="create-an-azure-virtual-network"></a>Creare una rete virtuale di Azure
1. In hello [portale di Azure classico](https://manage.windowsazure.com), fare clic su **New** > **servizi di rete** > **rete virtuale**  >  **Creazione personalizzata** e guidata hello toocomplete i valori seguenti di hello di utilizzo.

   | Pagina della procedura guidata | Valori da specificare |
   | --- | --- |
   |  **Dettagli della rete virtuale** |<p>Nome: Digitare un nome per la rete virtuale hello, ad esempio WestUSVNet.</p><p>Regione: Scegliere l'area più vicina hello.</p> |
   |  **Server DNS e connettività VPN** |<p>Server DNS: Specificare il nome di hello e indirizzo IP di uno o più server DNS locale.</p><p>Connettività: selezionare **Configura una VPN Site-to-Site**.</p><p>Rete locale: specificare una nuova rete locale.</p><p>Se si usa ExpressRoute invece di una VPN, vedere [Configurare una connessione ExpressRoute tramite un provider di Exchange](../expressroute/expressroute-locations-providers.md).</p> |
   |  **Connettività da sito a sito** |<p>Nome: Digitare un nome per la rete locale hello.</p><p>Indirizzo IP del dispositivo VPN: specificare l'indirizzo IP pubblico hello del dispositivo hello che si connetterà toohello di rete virtuale. dispositivo VPN Hello non può trovarsi dietro un NAT.</p><p>Indirizzo: Specificare gli intervalli di indirizzi hello per la rete locale (ad esempio 192.168.0.0/16 nel diagramma dello scenario hello).</p> |
   |  **Spazi degli indirizzi della rete virtuale** |<p>Spazio degli indirizzi: Specificare l'intervallo di indirizzi IP hello per le macchine virtuali che si desidera toorun in hello rete virtuale di Azure (ad esempio 10.1.0.0/16 nel diagramma dello scenario hello). Questo intervallo di indirizzi non possa sovrapporsi a hello indirizzo di rete locale hello.</p><p>Subnet: Specificare un nome e un indirizzo per una subnet per i server applicazioni hello (ad esempio front-end, 10.1.1.0/24) e per i controller di dominio hello (ad esempio back-end, 10.1.2.0/24).</p><p>Fare clic su **Aggiungi subnet gateway**.</p> |
2. Successivamente, si configurerà toocreate gateway di rete virtuale hello una connessione VPN da sito a sito sicura. Vedere [configurare un Gateway di rete virtuale](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) per le istruzioni di hello.
3. Creare la connessione VPN site-to-site di hello tra nuova rete virtuale hello e il dispositivo VPN locale. Vedere [configurare un Gateway di rete virtuale](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) per le istruzioni di hello.

## <a name="create-azure-vms-for-hello-dc-roles"></a>Creare macchine virtuali di Azure per hello ruoli di controller di dominio
Ripetere hello seguendo i passaggi toocreate macchine virtuali toohost hello ruolo controller di dominio in base alle esigenze. È consigliabile distribuire almeno due controller di dominio tooprovide la tolleranza di errore e la ridondanza virtuale. Se hello rete virtuale di Azure include almeno due controller di dominio che sono configurati in modo analogo (vale a dire, sono entrambi cataloghi globali, eseguire i server DNS, e non contiene alcun ruolo FSMO e così via) quindi posizionare le macchine virtuali hello che eseguono tali controller di dominio in un set di disponibilità per migliore tolleranza di errore.
toocreate hello macchine virtuali tramite Windows PowerShell anziché hello dell'interfaccia utente, vedere [toocreate usare Azure PowerShell e preconfigurare macchine virtuali basate su Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. In hello [portale di Azure classico](https://manage.windowsazure.com), fare clic su **New** > **calcolo** > **macchina virtuale**  >  **Dalla raccolta**. Utilizzare i valori toocomplete hello guidata hello. Accettare il valore predefinito hello per un'impostazione a meno che non è necessaria o suggerito un altro valore.

   | Pagina della procedura guidata | Valori da specificare |
   | --- | --- |
   |  **Scegli un'immagine** |Windows Server 2012 R2 Datacenter |
   |  **Configurazione macchina virtuale** |<p>Nome macchina virtuale: digitare un nome con etichetta singola (ad esempio AzureDC1).</p><p>Nuovo nome utente: Hello nome di un utente. Questo utente sarà un membro del gruppo Administrators locale di hello in hello macchina virtuale. Sarà necessario toosign questo nome in toohello VM per hello prima volta. account predefinito di Hello denominato Administrator non funzionerà.</p><p>Nuova password/conferma: digitare una password</p> |
   |  **Configurazione macchina virtuale** |<p>Il servizio cloud: Scegliere <b>creare un nuovo servizio cloud</b> per hello prima macchina virtuale e selezionare che lo stesso nome del servizio di cloud quando si creano più macchine virtuali che ospiteranno il ruolo di controller di dominio hello.</p><p>Nome DNS del servizio cloud: specificare un nome globalmente univoco</p><p>Regione/gruppo di affinità/rete virtuale: specificare il nome di rete virtuale hello (ad esempio WestUSVNet).</p><p>Account di archiviazione: Scegliere <b>utilizzare un account di archiviazione generato automaticamente</b> per hello prima macchina virtuale e quindi selezionare account di archiviazione stesso nome quando si creano più macchine virtuali che ospiteranno il ruolo di controller di dominio hello.</p><p>Set di disponibilità: scegliere <b>Crea set di disponibilità</b>.</p><p>Nome set di disponibilità: tipo di un nome per la disponibilità di hello impostato quando si crea hello prima macchina virtuale e quindi selezionare stesso nome di quando si creano più macchine virtuali.</p> |
   |  **Configurazione macchina virtuale** |<p>Selezionare <b>hello installa agente VM</b> e tutte le altre estensioni, è necessario.</p> |
2. Collegare un tooeach disco macchina virtuale che verrà eseguito hello ruolo di server controller di dominio. disco aggiuntivo Hello è necessario toostore hello AD database, registri e SYSVOL. Specificare le dimensioni del disco hello (ad esempio, 10 GB) e lasciare hello **preferenze Cache dell'Host** impostare troppo**Nessuno**. Per i passaggi di hello, vedere [come tooAttach tooa un disco dati macchina virtuale Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Dopo il primo accesso toohello macchina virtuale, aprire **Server Manager** > **servizi File e archiviazione** toocreate un volume su disco con NTFS.
4. Riservare un indirizzo IP statico per le macchine virtuali che eseguiranno il ruolo di controller di dominio hello. tooreserve un indirizzo IP statico, scaricare installazione guidata piattaforma Web di Microsoft hello e [installare Azure PowerShell](/powershell/azure/overview) ed eseguire il cmdlet Set-AzureStaticVNetIP hello. ad esempio:

    'Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM

Per altre informazioni sull'impostazione di un indirizzo IP statico, vedere [Configurare un indirizzo IP interno statico per una macchina virtuale](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-ad-ds-on-azure-vms"></a>Installare Servizi di dominio Active Directory in macchine virtuali di Azure
Accedi tooa macchina virtuale e verificare di disporre della connettività tra hello site-to-site VPN o ExpressRoute connessione tooresources nella rete locale. Installare quindi di dominio Active Directory in hello macchine virtuali di Azure. È possibile utilizzare il processo stesso utilizzare tooinstall un controller di dominio aggiuntivo nella rete locale (interfaccia utente, Windows PowerShell o un file di risposta). Durante l'installazione di AD DS, assicurarsi di specificare di nuovo volume di hello per percorso hello del database di Active Directory, i log e SYSVOL hello. Se è necessario un aggiornamento nell'installazione di Active Directory Domain Services, vedere [Installazione di Active Directory Domain Services (Livello 100)](https://technet.microsoft.com/library/hh472162.aspx) o [Installare un Controller di dominio Windows Server 2012 Replica in un dominio esistente (livello 200)](https://technet.microsoft.com/library/jj574134.aspx).

## <a name="reconfigure-dns-server-for-hello-virtual-network"></a>Riconfigurare il server DNS per la rete virtuale hello
1. In hello [portale di Azure](https://portal.azure.com), in hello **individuare risorse** immettere *le reti virtuali*, quindi fare clic su **le reti virtuali (classico)** in risultati della ricerca Hello. Fare clic sul nome della rete virtuale hello, hello e quindi [riconfigurare gli indirizzi IP di hello DNS server per la rete virtuale](../virtual-network/virtual-network-manage-network.md#dns-servers) gli indirizzi IP statici di toouse hello assegnati toohello i controller di dominio di replica anziché agli indirizzi IP hello di un DNS locale Server.
2. Fare clic su tooensure che tutte le repliche di hello macchine virtuali di controller di dominio nella rete virtuale hello siano configurati con i server DNS di toouse nella rete virtuale hello, **macchine virtuali**, fare clic su nella colonna Stato hello per ogni macchina virtuale e quindi fare clic su **riavviare** . Attendere che mostri hello VM **esecuzione** stato prima di provare toosign al suo interno.

## <a name="create-vms-for-application-servers"></a>Creare macchine virtuali per server applicazioni
1. Ripetere hello seguendo i passaggi toocreate macchine virtuali toorun come server applicazioni. Accettare il valore predefinito hello per un'impostazione a meno che non è necessaria o suggerito un altro valore.

   | Pagina della procedura guidata | Valori da specificare |
   | --- | --- |
   |  **Scegli un'immagine** |Windows Server 2012 R2 Datacenter |
   |  **Configurazione macchina virtuale** |<p>Nome macchina virtuale: digitare un nome con etichetta singola (ad esempio AppServer1).</p><p>Nuovo nome utente: Hello nome di un utente. Questo utente sarà un membro del gruppo Administrators locale di hello in hello macchina virtuale. Sarà necessario toosign questo nome in toohello VM per hello prima volta. account predefinito di Hello denominato Administrator non funzionerà.</p><p>Nuova password/conferma: digitare una password</p> |
   |  **Configurazione macchina virtuale** |<p>Il servizio cloud: Scegliere **creare un nuovo servizio cloud** per hello prima VM e che il nome del servizio stesso cloud quando si creano più macchine virtuali selezionare ospiterà applicazione hello.</p><p>Nome DNS del servizio cloud: specificare un nome globalmente univoco</p><p>Regione/gruppo di affinità/rete virtuale: specificare il nome di rete virtuale hello (ad esempio WestUSVNet).</p><p>Account di archiviazione: Scegliere **utilizzare un account di archiviazione generato automaticamente** per hello prima macchina virtuale e quindi selezionare account di archiviazione stesso nome quando si crea più macchine virtuali che ospiterà applicazione hello.</p><p>Set di disponibilità: scegliere **Crea set di disponibilità**.</p><p>Nome set di disponibilità: tipo di un nome per la disponibilità di hello impostato quando si crea hello prima macchina virtuale e quindi selezionare stesso nome di quando si creano più macchine virtuali.</p> |
   |  **Configurazione macchina virtuale** |<p>Selezionare <b>hello installa agente VM</b> e tutte le altre estensioni, è necessario.</p> |
2. Dopo il provisioning di ogni macchina virtuale, accedere e creare un join toohello dominio. In **Server Manager** fare clic su **Server locale** > **GRUPPO DI LAVORO** > **Modifica...** e quindi selezionare **dominio** e nome del tipo hello del dominio locale. Fornire le credenziali di un utente di dominio e quindi riavviare hello VM toocomplete hello aggiunta a un dominio.

toocreate hello macchine virtuali tramite Windows PowerShell anziché hello dell'interfaccia utente, vedere [toocreate usare Azure PowerShell e preconfigurare macchine virtuali basate su Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Per altre informazioni su come usare Windows PowerShell, vedere [Iniziare a utilizzare i cmdlet di Azure](/powershell/azure/overview) e [Informazioni di riferimento sui cmdlet di Azure](/powershell/azure/get-started-azureps).

## <a name="additional-resources"></a>Risorse aggiuntive
* [Linee guida per la distribuzione di Active Directory di Windows Server in macchine virtuali di Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Come tooupload locali esistenti tooAzure i controller di dominio Hyper-V tramite Azure PowerShell](http://support.microsoft.com/kb/2904015)
* [Installazione di una nuova foresta Active Directory in una rete virtuale di Azure](active-directory-new-forest-virtual-machine.md)
* [Rete virtuale di Azure](../virtual-network/virtual-networks-overview.md)
* [Microsoft Azure IaaS per professionisti IT: (01) Dati fondamentali delle macchine virtuali](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS per professionisti IT: (05) Creazione di reti virtuali e connettività cross-premise](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Azure PowerShell](/powershell/azure/overview)
* [Cmdlet di gestione di Azure](/powershell/module/azurerm.compute/#virtual_machines)

<!--Image references-->
[1]: ./media/active-directory-install-replica-active-directory-domain-controller/ReplicaDCsOnAzureVNet.png
