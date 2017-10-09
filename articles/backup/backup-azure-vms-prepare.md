---
title: aaaPreparing tooback l'ambiente di macchine virtuali di Azure | Documenti Microsoft
description: Assicurarsi che l'ambiente sia pronto per il backup di macchine virtuali in Azure
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: backup; eseguire il backup;
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a>Preparare l'ambiente tooback le macchine virtuali di Azure
> [!div class="op_single_selector"]
> * [Modello di Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Modello classico](backup-azure-vms-prepare.md)
>
>

Prima di eseguire il backup di una macchina virtuale (VM) di Azure, devono verificarsi tre condizioni.

* È necessario un insieme di credenziali backup toocreate o identificare un insieme di credenziali di backup esistente *in hello stessa regione della macchina virtuale*.
* Stabilire la connettività di rete tra hello Azure rete Internet pubblica gli indirizzi e hello gli endpoint di archiviazione di Azure.
* Installare l'agente VM hello in hello macchina virtuale.

Se si è certi di queste condizioni già esistono nell'ambiente in uso e quindi toohello [eseguire il backup di un articolo di macchine virtuali](backup-azure-vms.md). In caso contrario, continuare a leggere, questo articolo consentirà attraverso hello passaggi tooprepare tooback l'ambiente di una macchina virtuale di Azure.

##<a name="supported-operating-system-for-backup"></a>Sistema operativo supportato per il backup
 * **Linux**: Backup di Azure supporta [un elenco di distribuzioni approvate da Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , ad eccezione di CoreOS Linux. _Altri Bring-Your-proprietari-distribuzioni di Linux potrebbe essere inoltre funzionare, purché sia disponibile nella macchina virtuale hello agente VM hello e il supporto per Python esiste. Microsoft tuttavia non consiglia queste distribuzioni per il backup._
 * **Windows Server**: le versioni precedenti a Windows Server 2008 R2 non sono supportate.


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Limitazioni durante il backup e il ripristino di una VM
> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). Hello seguente elenco include le limitazioni di hello durante la distribuzione nel modello classico hello.
>
>

* Il backup di macchine virtuali con più di 16 dischi dati non è supportato.
* Il backup di macchine virtuali con un indirizzo IP riservato e nessun endpoint definito non è supportato.
* Dati di backup non includono tooVM unità collegate rete montato.
* La sostituzione di una macchina virtuale esistente durante il ripristino non è supportata. Eliminare tutti i dischi associati e macchina virtuale esistente hello e quindi ripristinare i dati di hello dal backup.
* L'operazione di backup e ripristino tra aree geografiche diverse non è supportata.
* Backup di macchine virtuali tramite il servizio di Azure Backup hello è supportato in tutte le aree pubbliche di Azure (vedere hello [checklist](https://azure.microsoft.com/regions/#services) delle aree geografiche supportate). Se l'area hello che si sta cercando è attualmente supportata, non verrà visualizzato nell'elenco a discesa hello durante la creazione dell'insieme di credenziali.
* Backup di macchine virtuali tramite il servizio di Azure Backup hello è supportato solo per le versioni del sistema operativo selezionare:
* Il ripristino di un controller di dominio di VM che fa parte di una configurazione con controller di dominio è supportato solo tramite PowerShell. Altre informazioni sul [ripristino di un controller di dominio con più controller di dominio](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Ripristino delle macchine virtuali che dispongono delle seguenti configurazioni di rete speciali hello è supportato solo tramite PowerShell. Macchine virtuali create tramite flusso di lavoro ripristino hello in hello dell'interfaccia utente non avrà queste configurazioni di rete al termine dell'operazione di ripristino hello. vedere, più toolearn [il ripristino di macchine virtuali con configurazioni di rete speciali](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Macchine virtuali con configurazione del servizio di bilanciamento del carico (interno ed esterno)
  * Macchine virtuali con più indirizzi IP riservati
  * Macchine virtuali con più schede di rete

## <a name="create-a-backup-vault-for-a-vm"></a>Creare un insieme di credenziali di backup per una VM
Un insieme di credenziali di backup è un'entità contenente tutti i backup di hello e i punti di ripristino che sono stati creati nel corso del tempo. insieme di credenziali backup Hello contiene anche i criteri di backup hello che verrà applicato toohello le macchine virtuali viene eseguito il backup.

> [!IMPORTANT]
> A partire da marzo 2017, è possibile utilizzare non è più insiemi di credenziali Backup hello toocreate portale classico. Insiemi di credenziali di Backup esistenti siano ancora supportati ed è possibile troppo[utilizzare gli insiemi di credenziali di Azure PowerShell toocreate Backup](./backup-client-automation-classic.md#create-a-backup-vault). Tuttavia, Microsoft consiglia che creare insiemi di credenziali di servizi di ripristino per tutte le distribuzioni perché miglioramenti futuri applicano tooRecovery servizi insiemi di credenziali, solo.


La seguente immagine illustra le relazioni di hello tra hello varie entità di Backup di Azure: ![relazioni ed entità di Backup di Azure](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>Connettività di rete
In snapshot VM hello toomanage ordine, estensione backup hello deve toohello connettività Azure gli indirizzi IP pubblici. Senza hello destra la connettività Internet, HTTP richieste hello e timeout operazione di backup della macchina virtuale hello non riesce. Se la distribuzione ha restrizioni di accesso, ad esempio, un gruppo di sicurezza di rete (NSG), scegliere una delle opzioni seguenti per specificare un percorso chiaro per il traffico di backup:

* [Gli intervalli di IP whitelist hello Data Center di Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -vedere hello per le istruzioni su come toowhitelist hello gli indirizzi IP.
* Distribuire un server proxy HTTP per eseguire il routing del traffico

Quando si decide quale toouse opzione, hello compromessi sono compresi tra gestibilità, un controllo granulare e costi.

| Opzione | Vantaggi | Svantaggi: |
| --- | --- | --- |
| Aggiungere gli intervalli IP all'elenco elementi consentiti  |Senza costi aggiuntivi.<br><br>Per l'apertura in un gruppo di accesso, utilizzare hello <i>Set AzureNetworkSecurityRule</i> cmdlet. |Toomanage complesse come cambiano di intervalli IP hello interessato nel tempo.<br><br>Fornisce l'intero toohello di accesso di Azure e non solo l'archiviazione. |
| Proxy HTTP |Un controllo granulare proxy hello archiviazione hello URL consentiti. un controllo granulare toosetup proxy hello, https://\*.blob.core.windows.net/\* modello di URL deve toobe consentito. toowhitelist hello solo account di archiviazione utilizzato dalla macchina virtuale, hello https://\<storageAccount\>.blob.core.windows.net/\* modello di URL deve toobe consentito. <br>TooVMs accesso singolo punto di Internet.<br>Non soggetto tooAzure modifiche all'indirizzo IP. |Costi aggiuntivi per l'esecuzione di una macchina virtuale con il software proxy hello. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Intervalli di IP whitelist hello Data Center di Azure
intervalli IP toowhitelist hello Data Center di Azure, vedere hello [sito Web di Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) per informazioni dettagliate su intervalli IP hello e le istruzioni.

### <a name="using-an-http-proxy-for-vm-backups"></a>Uso di un proxy HTTP per i backup delle VM
Per eseguire il backup di una macchina virtuale, estensione di backup hello in hello VM invia tooAzure i comandi di gestione snapshot hello archiviazione mediante un'API di HTTPS. Instradare il traffico di estensione del backup hello mediante il proxy HTTP hello poiché è l'unico componente hello configurato per l'accesso toohello rete Internet pubblica.

> [!NOTE]
> Non è consigliato per il software proxy hello che deve essere utilizzato. Assicurarsi di selezionare un proxy dotato aderenza in uscita e che è compatibile con i passaggi di configurazione hello riportato di seguito. Assicurarsi che i prodotti software di terze parti non modificano le impostazioni del proxy hello
>
>

immagine di esempio Hello riportata di seguito viene illustrato come passaggi di configurazione tre hello necessarie toouse HTTP proxy:

* Tutto il traffico HTTP associato per le route di VM App hello pubblica Internet tramite Proxy VM.
* Proxy VM consente il traffico in ingresso da macchine virtuali nella rete virtuale hello.
* Sicurezza gruppo (rete) denominato Scoperto lockdown Hello deve un sicurezza regola consentire Internet il traffico in uscita dalla macchina virtuale di Proxy.

![Diagramma della distribuzione gruppo di sicurezza di rete con proxy HTTP](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse HTTP proxy toocommunicating toohello rete Internet pubblica, seguire questi passaggi:

#### <a name="step-1-configure-outgoing-network-connections"></a>Passaggio 1. Configurare le connessioni di rete in uscita
###### <a name="for-windows-machines"></a>Per macchine Windows
Questa procedura consente di impostare la configurazione del server proxy per l'account del sistema locale.

1. Scaricare [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Eseguire il comando seguente dal prompt dei comandi con privilegi elevati,

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Si apre la finestra di Explorer.
3. Passare tooTools -> Opzioni Internet -> connessioni -> Impostazioni LAN.
4. Verificare le impostazioni del proxy per l'account di sistema. Impostare l'IP del Proxy e la porta.
5. Chiudere Internet Explorer.

Questo comando esegue una configurazione proxy a livello di computer e verrà usato per tutto il traffico HTTP/HTTPS in uscita.

Se è stato impostato un server proxy in un account utente corrente (non un Account di sistema locale), utilizzare hello seguenti script tooapply li tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Se si nota il messaggio "(407) Autenticazione proxy obbligatoria" nel log del server proxy, verificare che l'autenticazione sia impostata correttamente.
>
>

###### <a name="for-linux-machines"></a>Per macchine Linux
Aggiungere hello seguente riga toohello ```/etc/environment``` file:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Aggiungere hello seguenti righe toohello ```/etc/waagent.conf``` file:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Passaggio 2. Consenti connessioni in ingresso nel server proxy hello:
1. Nel server proxy hello, aprire Windows Firewall. firewall Hello più semplice modo tooaccess hello è toosearch per Windows Firewall con sicurezza avanzata.

    ![Aprire hello Firewall](./media/backup-azure-vms-prepare/firewall-01.png)
2. Nella finestra di dialogo Windows Firewall hello destro **regole connessioni in entrata** e fare clic su **nuova regola...** .

    ![Creare una nuova regola](./media/backup-azure-vms-prepare/firewall-02.png)
3. In hello **in ingresso Creazione guidata nuova regola**, scegliere hello **personalizzato** opzione per hello **tipo di regola** e fare clic su **Avanti**.
4. In hello di hello pagina tooselect **programma**, scegliere **tutti i programmi** e fare clic su **Avanti**.
5. In hello **protocollo e porte** immettere hello le seguenti informazioni e fare clic su **Avanti**:

    ![Creare una nuova regola](./media/backup-azure-vms-prepare/firewall-03.png)

   * Nel campo *Tipo di protocollo* scegliere *TCP*.
   * per *porta locale* scegliere *porte specifiche*, nel campo hello specificare hello ```<Proxy Port>``` che è stato configurato.
   * Nel campo *Porta remota* selezionare *Tutte le porte*.

     Per rest hello della procedura guidata hello, fare clic su fine di toohello modo hello tutti e assegnare un nome di questa regola.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Passaggio 3. Aggiungere un toohello regola eccezione gruppo:
In un prompt dei comandi di Azure PowerShell, immettere hello comando seguente:

Hello comando seguente consente di aggiungere un gruppo di toohello di eccezione. Questa eccezione consente il traffico TCP da qualsiasi porta 10.0.0.5 tooany indirizzo Internet sulla porta 80 (HTTP) o 443 (HTTPS). Se è necessaria una porta specifica in hello rete Internet pubblica, essere tooadd assicurarsi che la porta toohello ```-DestinationPortRange``` anche.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

*Assicurarsi di sostituire i nomi di hello nell'esempio hello con la distribuzione di hello dettagli tooyour appropriato.*

## <a name="vm-agent"></a>Agente di macchine virtuali
Prima di eseguire il backup hello macchina virtuale di Azure, è necessario assicurarsi che l'agente VM di Azure hello è correttamente installato nella macchina virtuale hello. Poiché l'agente VM hello viene creato un componente facoltativo in fase di hello hello macchina virtuale, verificare la casella di controllo hello per agente VM hello è selezionato prima di provisioning della macchina virtuale hello.

### <a name="manual-installation-and-update"></a>Installazione e aggiornamento manuali
agente VM Hello è già presente nelle macchine virtuali create da hello raccolta di Azure. Tuttavia, le macchine virtuali vengono migrate da Data Center locale non avrebbero agente VM hello installato. Per tali macchine virtuali, l'agente VM hello deve toobe installato in modo esplicito. Altre informazioni sui [l'installazione dell'agente VM hello in una macchina virtuale esistente](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

| **Operazione** | **Windows** | **Linux** |
| --- | --- | --- |
| L'installazione dell'agente VM hello |<li>Scaricare e installare hello [agente MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Sarà necessario installazione hello toocomplete privilegi di amministratore. <li>[Aggiorna proprietà macchina virtuale hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate che hello agente è installato. |<li> Installare più recente hello [agente Linux](https://github.com/Azure/WALinuxAgent) da GitHub. Sarà necessario installazione hello toocomplete privilegi di amministratore. <li> [Aggiorna proprietà macchina virtuale hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate che hello agente è installato. |
| Aggiornamento agente VM hello |Aggiornamento agente VM di hello è semplice come reinstallare hello [binari agente VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br><br>Verificare che non venga eseguita alcuna operazione di backup durante l'aggiornamento dell'agente VM hello. |Seguire le istruzioni di hello [aggiornamento hello agente VM Linux ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br><br>Verificare che non venga eseguita alcuna operazione di backup durante l'aggiornamento dell'agente VM hello. |
| Convalida di installazione dell'agente VM hello |<li>Passare toohello *C:\WindowsAzure\Packages* cartella hello macchina virtuale di Azure. <li>È necessario trovare un file WaAppAgent.exe hello presentano.<li> Fare clic sul file hello, andare troppo**proprietà**, quindi selezionare hello **dettagli** campo versione prodotto di hello scheda deve essere 2.6.1198.718 o versione successiva. |N/D |

Informazioni su hello [agente VM](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) e [come tooinstall è](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).

### <a name="backup-extension"></a>Estensione di backup
tooback la macchina virtuale hello, hello servizio Azure Backup installa un agente di macchine Virtuali toohello estensione. Hello servizio Azure Backup facilmente vengono aggiornati e le patch di estensione del backup hello senza l'intervento dell'utente.

estensione del backup Hello viene installato se hello macchina virtuale è in esecuzione. Una macchina virtuale in esecuzione nonché hello maggiore probabilità di riuscire a ottenere un punto di ripristino coerenti con l'applicazione. Tuttavia, hello Azure Backup servizio continuerà tooback backup hello VM, anche se è stato disattivato e non è stato possibile estensione hello installato (noto anche come Offline VM). In questo caso, si sarà il punto di ripristino hello *anomalo* come illustrato in precedenza.

## <a name="questions"></a>Domande?
Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato preparato l'ambiente per il backup di una macchina virtuale, il passaggio successivo logico è toocreate una copia di backup. Hello pianificazione articolo fornisce informazioni più dettagliate sul backup di macchine virtuali.

* [Eseguire il backup di macchine virtuali](backup-azure-vms.md)
* [Pianificare l'infrastruttura di backup delle VM](backup-azure-vms-introduction.md)
* [Gestire backup di macchine virtuali](backup-azure-manage-vms.md)
