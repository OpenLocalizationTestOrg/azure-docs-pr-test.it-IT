---
title: aaaInstall una foresta di Active Directory in una rete virtuale di Azure | Documenti Microsoft
description: Un'esercitazione che illustra come insieme di strutture toocreate un nuovo ambiente Active Directory in una macchina virtuale (VM) in una rete virtuale di Azure.
services: active-directory, virtual-network
keywords: 'macchina virtuale active directory, installazione di una foresta active directory, video su azure active directory  '
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
tags: 
ms.assetid: eb7170d0-266a-4caa-adce-1855589d65d1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: joflore
ms.openlocfilehash: 08121130777cc3c206d7b5b38974982884dca1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-new-active-directory-forest-on-an-azure-virtual-network"></a>Installazione di una nuova foresta Active Directory in una rete virtuale di Azure
Questo argomento viene illustrato come toocreate un nuovo Windows Server Active Directory dell'ambiente in una rete virtuale di Azure in una macchina virtuale (VM) su un [rete virtuale di Azure](../virtual-network/virtual-networks-overview.md). In questo caso, hello rete virtuale di Azure non è rete locale connesso tooan.

Altri argomenti di interesse:

* Per un video che illustra questa procedura, vedere [come tooinstall un nuovo ambiente Active Directory della foresta in una rete virtuale di Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* È possibile facoltativamente [configurare una VPN site-to-site](../vpn-gateway/vpn-gateway-site-to-site-create.md) e quindi installare una nuova foresta o estendere un tooan foresta locale rete virtuale di Azure. Per la procedura, vedere [Installazione di un controller di dominio Active Directory di replica in una rete virtuale di Azure](active-directory-install-replica-active-directory-domain-controller.md).
* Per le linee guida concettuali sull'installazione di Servizi di dominio Active Directory in una rete virtuale di Azure, vedere [Linee guida per la distribuzione di Active Directory di Windows Server in macchine virtuali di Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Diagramma dello scenario
In questo scenario, gli utenti esterni devono tooaccess di applicazioni per i server di dominio. macchine virtuali di Hello che eseguono Server applicazione hello e le macchine virtuali hello che eseguono i controller di dominio vengono installate installato nel proprio servizio cloud in una rete virtuale di Azure. Sono anche incluse in un set di disponibilità per una migliore tolleranza di errore.

![Foresta Active Directory in una macchina virtuale in Rete virtuale di Azure ][1] 7

## <a name="how-does-this-differ-from-on-premises"></a>Differenze rispetto all'installazione locale
Non esistono molte differenze tra l'installazione locale di un controller di dominio e l'installazione in Azure. Nella hello nella tabella seguente sono elencate le differenze principali Hello.

| tooconfigure... | Locale | rete virtuale di Azure |
| --- | --- | --- |
| **Indirizzo IP per il controller di dominio hello** |Assegnare l'indirizzo IP statico nelle proprietà scheda di rete hello |Eseguire tooassign cmdlet Set-AzureStaticVNetIP di hello un indirizzo IP statico |
| **Resolver del client DNS** |Impostare l'indirizzo di server preferito e alternativo DNS su hello proprietà scheda di rete dei membri del dominio |Impostare l'indirizzo del server DNS nella proprietà della rete virtuale hello hello |
| **Archiviazione del database di Active Directory** |Facoltativamente, modificare il percorso di archiviazione predefinito hello da C:\ |È necessario toochange percorso di archiviazione predefinito da c:\. |

## <a name="create-an-azure-virtual-network"></a>Creare una rete virtuale di Azure
1. Accedi toohello portale di Azure classico.
2. Creare una rete virtuale. Fare clic su **Reti** > **Crea rete virtuale**. Utilizzare i valori hello hello tabella toocomplete hello guidata.

   | Pagina della procedura guidata | Valori da specificare |
   | --- | --- |
   |  **Dettagli della rete virtuale** |<p>Nome: immettere un nome per la rete virtuale</p><p>Regione: Scegliere l'area più vicina hello</p> |
   |  **DNS e VPN** |<p>Lasciare il campo relativo al server DNS vuoto</p><p>Non selezionare alcuna opzione VPN</p> |
   |  **Spazi degli indirizzi della rete virtuale** |<p>Nome subnet: immettere un nome per la subnet</p><p>IP iniziale: <b>10.0.0.0</b></p><p>CIDR: <b>/24 (256)</b></p> |

## <a name="create-vms-toorun-hello-domain-controller-and-dns-server-roles"></a>Creare controller di dominio hello toorun macchine virtuali e i ruoli del server DNS
Ripetere hello seguendo i passaggi toocreate macchine virtuali toohost hello ruolo controller di dominio in base alle esigenze. È consigliabile distribuire almeno due controller di dominio tooprovide la tolleranza di errore e la ridondanza virtuale. Se hello rete virtuale di Azure include almeno due controller di dominio che sono configurati in modo analogo (vale a dire, sono entrambi cataloghi globali, eseguire i server DNS, e non contiene alcun ruolo FSMO e così via) quindi posizionare le macchine virtuali hello che eseguono tali controller di dominio in un set di disponibilità per migliore tolleranza di errore.

toocreate hello macchine virtuali tramite Windows PowerShell anziché hello dell'interfaccia utente, vedere [toocreate usare Azure PowerShell e preconfigurare macchine virtuali basate su Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. Nel portale classico hello, fare clic su **New** > **calcolo** > **macchina virtuale** > **dalla raccolta**. Utilizzare i valori toocomplete hello guidata hello. Accettare il valore predefinito hello per un'impostazione a meno che non è necessaria o suggerito un altro valore.

   | Pagina della procedura guidata | Valori da specificare |
   | --- | --- |
   |  **Scegli un'immagine** |Windows Server 2012 R2 Datacenter |
   |  **Configurazione macchina virtuale** |<p>Nome macchina virtuale: digitare un nome con etichetta singola (ad esempio AzureDC1).</p><p>Nuovo nome utente: Hello nome di un utente. Questo utente sarà un membro del gruppo Administrators locale di hello in hello macchina virtuale. Sarà necessario toosign questo nome in toohello VM per hello prima volta. account predefinito di Hello denominato Administrator non funzionerà.</p><p>Nuova password/conferma: digitare una password</p> |
   |  **Configurazione macchina virtuale** |<p>Il servizio cloud: Scegliere <b>creare un nuovo servizio cloud</b> per hello prima macchina virtuale e selezionare che lo stesso nome del servizio di cloud quando si creano più macchine virtuali che ospiteranno il ruolo di controller di dominio hello.</p><p>Nome DNS del servizio cloud: specificare un nome globalmente univoco</p><p>Regione/gruppo di affinità/rete virtuale: specificare il nome di rete virtuale hello (ad esempio WestUSVNet).</p><p>Account di archiviazione: Scegliere <b>utilizzare un account di archiviazione generato automaticamente</b> per hello prima macchina virtuale e quindi selezionare account di archiviazione stesso nome quando si creano più macchine virtuali che ospiteranno il ruolo di controller di dominio hello.</p><p>Set di disponibilità: scegliere <b>Crea set di disponibilità</b>.</p><p>Nome set di disponibilità: tipo di un nome per la disponibilità di hello impostato quando si crea hello prima macchina virtuale e quindi selezionare stesso nome di quando si creano più macchine virtuali.</p> |
   |  **Configurazione macchina virtuale** |<p>Selezionare <b>hello installa agente VM</b> e tutte le altre estensioni, è necessario.</p> |
2. Collegare un tooeach disco macchina virtuale che verrà eseguito hello ruolo di server controller di dominio. disco aggiuntivo Hello è necessario toostore hello AD database, registri e SYSVOL. Specificare le dimensioni del disco hello (ad esempio, 10 GB) e lasciare hello **preferenze Cache dell'Host** impostare troppo**Nessuno**. Per i passaggi di hello, vedere [come tooAttach tooa un disco dati macchina virtuale Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Dopo il primo accesso toohello macchina virtuale, aprire **Server Manager** > **servizi File e archiviazione** toocreate un volume su disco con NTFS.
4. Riservare un indirizzo IP statico per le macchine virtuali che eseguiranno il ruolo di controller di dominio hello. tooreserve un indirizzo IP statico, scaricare installazione guidata piattaforma Web di Microsoft hello e [installare Azure PowerShell](/powershell/azure/overview) ed eseguire il cmdlet Set-AzureStaticVNetIP hello. ad esempio:

    `Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM`

Per altre informazioni sull'impostazione di un indirizzo IP statico, vedere [Configurare un indirizzo IP interno statico per una macchina virtuale](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-windows-server-active-directory"></a>Installare Windows Server Active Directory
Utilizzare hello stessa routine troppo[installare di dominio Active Directory](https://technet.microsoft.com/library/jj574166.aspx) utilizzare locale (ovvero, è possibile utilizzare Windows PowerShell, un file di risposte o hello dell'interfaccia utente). È necessario tooinstall le credenziali di amministratore tooprovide una nuova foresta. percorso di hello toospecify per hello database di Active Directory, i registri e SYSVOL, modificare il percorso di archiviazione predefinito hello da hello unità toohello dati aggiuntivi disco del sistema operativo che è collegato toohello macchina virtuale.

Al termine dell'installazione di controller di dominio hello, riconnettersi toohello macchina virtuale e accedere toohello controller di dominio. Memorizza le credenziali di dominio toospecify.

## <a name="reset-hello-dns-server-for-hello-azure-virtual-network"></a>Reimpostare il server DNS hello per hello rete virtuale di Azure
1. Reimpostare l'impostazione di server d'inoltro DNS hello su hello nuovo controller di dominio/server DNS.
   1. In Server Manager fare clic su **Strumenti**  > **DNS**.
   2. In **gestore DNS**, fare doppio clic su nome hello del server DNS hello e fare clic su **proprietà**.
   3. In hello **server d'inoltro** scheda e scegliere l'indirizzo IP hello del server d'inoltro hello **modifica**.  Selezionare l'indirizzo IP hello e fare clic su **eliminare**.
   4. Fare clic su **OK** editor hello tooclose e **Ok** nuovamente le proprietà di server DNS di tooclose hello.
2. Aggiornare impostazioni hello del server DNS per la rete virtuale hello.
   1. Fare clic su **reti virtuali** > fare doppio clic sulla rete virtuale di hello creata > **configura** > **server DNS**, digitare il nome di hello e hello DIP di uno di Hello macchine virtuali che esegue il ruolo di server controller di dominio/DNS hello e fare clic su **salvare**.
   2. Selezionare hello macchina virtuale e fare clic su **riavviare** tootrigger hello VM tooconfigure impostazioni del resolver DNS con indirizzo IP di hello del server DNS nuovo hello.

## <a name="create-vms-for-domain-members"></a>Creare macchine virtuali per i membri del dominio
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

## <a name="see-also"></a>Vedere anche
* [La modalità della foresta tooinstall un nuovo ambiente Active Directory in una rete virtuale di Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* [Linee guida per la distribuzione di Active Directory di Windows Server in macchine virtuali di Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Configura una VPN da sito a sito](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Installazione di un controller di dominio Active Directory di replica in una rete virtuale di Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IaaS per professionisti IT: (01) Dati fondamentali delle macchine virtuali](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS per professionisti IT: (05) Creazione di reti virtuali e connettività cross-premise](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Panoramica di Rete virtuale.](../virtual-network/virtual-networks-overview.md)
* [Come tooinstall e configurare Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Informazioni di riferimento sui cmdlet di Azure](/powershell/azure/get-started-azureps)
* [Impostare un indirizzo IP statico per una macchina virtuale di Azure](http://windowsitpro.com/windows-azure/set-azure-vm-static-ip-address)
* [Come indirizzo IP statico di tooassign tooAzure VM](http://www.bhargavs.com/index.php/2014/03/13/how-to-assign-static-ip-to-azure-vm/)
* [Installare una nuova foresta Active Directory](https://technet.microsoft.com/library/jj574166.aspx)
* [Introduzione tooActive Directory Domain Services (AD DS) Virtualization (Level 100)](https://technet.microsoft.com/library/hh831734.aspx)

<!--Image references-->
[1]: ./media/active-directory-new-forest-virtual-machine/AD_Forest.png
