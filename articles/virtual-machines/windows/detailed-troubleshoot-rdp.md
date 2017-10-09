---
title: desktop remoto di aaaDetailed risoluzione dei problemi in Azure | Documenti Microsoft
description: "Rivedere la procedura dettagliata sulla risoluzione dei problemi per gli errori di desktop remoti in cui non è possibile tooa macchine virtuali di Windows in Azure"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "non è possibile connettersi a desktop tooremote, risolvere i problemi relativi a desktop remoto, non è possibile connettere desktop remoto, errori di desktop remoti, remote desktop Risoluzione dei problemi, problemi relativi al desktop remoti"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a>La procedura dettagliata sulla risoluzione dei problemi di connessione desktop remoto genera tooWindows macchine virtuali in Azure
In questo articolo vengono fornite procedure dettagliate sulla risoluzione dei problemi di toodiagnose e correggere gli errori di Desktop remoto complessi per le macchine virtuali basate su Windows Azure.

> [!IMPORTANT]
> tooeliminate hello errori più comuni di Desktop remoto, assicurarsi che tooread [base articolo sulla risoluzione dei problemi di hello per Desktop remoto](troubleshoot-rdp-connection.md) prima di procedere.

Potrebbero verificarsi un Desktop remoto, il messaggio di errore che non sono simili a uno qualsiasi dei messaggi di errore specifici hello analizzato in [hello base Desktop remoto, risoluzione dei problemi guida](troubleshoot-rdp-connection.md). Seguire questi passaggi toodetermine perché il client di Desktop remoto (RDP) hello è Impossibile tooconnect toohello RDP servizio hello macchina virtuale di Azure.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello MSDN di Azure e forum di Overflow dello Stack di hello](https://azure.microsoft.com/support/forums/). In alternativa, è anche possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e fare clic su **supporto**. Per informazioni sull'utilizzo di supporto tecnico di Azure, leggere hello [domande frequenti sul supporto di Microsoft Azure](https://azure.microsoft.com/support/faq/).

## <a name="components-of-a-remote-desktop-connection"></a>Componenti di una connessione Desktop remoto
Hello seguenti componenti coinvolti in una connessione RDP:

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

Prima di procedere, può essere utile toomentally verificare cosa è cambiato rispetto hello ultima ha esito positivo Desktop remoto connessione toohello macchina virtuale. ad esempio:

* indirizzo IP pubblico del hello hello macchina virtuale o un servizio cloud contenente hello VM Hello (detto anche l'indirizzo IP virtuale hello [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) è stato modificato. Errore RDP Hello potrebbe essere che la cache del client DNS presenta ancora hello *indirizzo IP precedente* registrato per il nome DNS hello. Svuotare la cache del client DNS e provare a riconnettersi hello macchina virtuale. O provare a connettersi direttamente con hello nuovo VIP.
* Si siano utilizzando le connessioni Desktop remoto toomanage un'applicazione di terze parti invece di utilizzare connessione hello generati da hello portale di Azure. Verificare che la configurazione dell'applicazione hello include hello corretto la porta TCP per hello traffico Desktop remoto. È possibile controllare questa porta per una macchina virtuale classica in hello [portale di Azure](https://portal.azure.com), fare clic su impostazioni della macchina virtuale di hello > endpoint.

## <a name="preliminary-steps"></a>Operazioni preliminari
Prima di procedere toohello risoluzione dei problemi dettagliata,

* Controllare lo stato di hello della macchina virtuale hello in hello portale di Azure per eventuali problemi.
* Seguire hello [passaggi correzione rapida per gli errori comuni di RDP in hello risoluzione dei problemi per](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).

Provare a riconnettersi toohello macchina virtuale tramite Desktop remoto dopo questi passaggi.

## <a name="detailed-troubleshooting-steps"></a>Procedura di risoluzione dei problemi dettagliata
client Desktop remoto Hello potrebbe non essere il servizio tooreach in grado di hello Desktop remoto nella macchina virtuale di Azure hello tooissues scadenza in hello seguenti origini:

* [Computer client Desktop remoto](#source-1-remote-desktop-client-computer)
* [Dispositivo periferico dell’Intranet dell’organizzazione](#source-2-organization-intranet-edge-device)
* [Endpoint del servizio cloud ed elenco di controllo di accesso (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Gruppi di sicurezza di rete](#source-4-network-security-groups)
* [Macchina virtuale di Azure basata su Windows](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a>Origine 1: computer client Desktop remoto
Verificare che il computer è possibile rendere Desktop remoto connessioni tooanother locale, i computer basati su Windows.

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

Se non è possibile, cercare hello seguendo le impostazioni nel computer in uso:

* Un'impostazione firewall locale che blocca il traffico di Desktop remoto.
* Software proxy client installato localmente che impedisce le connessioni Desktop remoto.
* Software di monitoraggio della rete installato localmente che impedisce le connessioni Desktop remoto.
* Altri tipi di software di sicurezza che effettuano il monitoraggio del traffico o consentono/non consentono tipi di traffico che impediscano le connessioni Desktop remoto.

In questi casi, disattivare il software hello temporaneamente e provare tooconnect tooan locale computer tramite Desktop remoto. Se è possibile scoprire la causa effettiva hello in questo modo, con connessioni di rete amministratore toocorrect hello software impostazioni tooallow Desktop remoto.

## <a name="source-2-organization-intranet-edge-device"></a>Origine 2: dispositivo periferico dell’Intranet dell’organizzazione
Verificare che un computer connesso direttamente toohello che Internet può rendere tooyour connessioni Desktop remoto macchina virtuale di Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

Se non si dispone di un computer che è direttamente connesso toohello Internet, creare e testare con una nuova macchina virtuale di Azure in un servizio cloud o di gruppo di risorse. Per ulteriori informazioni, vedere [Creare una macchina virtuale con Windows in Azure](../virtual-machines-windows-hero-tutorial.md). È possibile eliminare macchine virtuali hello e gruppo di risorse hello o servizio cloud hello, dopo hello test.

Se è possibile creare una connessione Desktop remoto con un computer collegato direttamente toohello Internet, controllare il dispositivo perimetrale intranet di organizzazione per:

* Un firewall interno blocco toohello connessioni HTTPS Internet.
* Server proxy che impedisce le connessioni Desktop remoto.
* Software di rilevamento delle intrusioni o software per il monitoraggio della rete in esecuzione sui dispositivi nella rete perimetrale che impedisce le connessioni Desktop remoto.

Funziona con le impostazioni di rete amministratore toocorrect hello dell'organizzazione intranet edge dispositivo tooallow Desktop remoto basato su HTTPS connessioni toohello Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Origine 3: endpoint del servizio cloud e ACL
Per macchine virtuali create con modello di distribuzione classica hello, verificare che un'altra macchina virtuale di Azure che sia in hello stesso servizio cloud o rete virtuale è possibile apportare tooyour connessioni Desktop remoto macchina virtuale di Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> Per le macchine virtuali create in Gestione risorse, ignorare troppo[origine 4: gruppi di sicurezza di rete](#source-4-network-security-groups).

Se è un'altra macchina virtuale non hello nello stesso servizio cloud o rete virtuale, crearne uno. Seguire i passaggi di hello in [creare una macchina virtuale Windows in esecuzione in Azure](../virtual-machines-windows-hero-tutorial.md). Eliminare la macchina virtuale di test hello dopo aver completato il test di hello.

Se è possibile connettersi tramite Desktop remoto tooa macchina virtuale di hello stesso cloud servizio o della rete virtuale, verificare la presenza di queste impostazioni:

* configurazione dell'endpoint per il traffico di Desktop remoto nella destinazione hello VM Hello: hello privata la porta TCP dell'endpoint hello deve corrispondere la porta TCP hello su quale hello servizio Desktop remoto della macchina virtuale è in ascolto (valore predefinito è 3389).
* Hello ACL per l'endpoint di traffico hello Desktop remoto nella destinazione hello VM: gli ACL consentono di toospecify consentito o negato il traffico in ingresso da Internet in base al relativo indirizzo IP di origine hello. ACL configurato in modo errato può impedire l'endpoint di toohello traffico Desktop remoto in ingresso. Controllare il tooensure ACL che è consentito il traffico in ingresso dagli indirizzi IP pubblici di proxy o un altro server edge. Per altre informazioni, vedere [Che cos'è un elenco di controllo di accesso di rete (ACL)?](../../virtual-network/virtual-networks-acl.md)

Se endpoint hello è hello di origine del problema in hello toocheck rimuovere endpoint corrente hello e crearne uno nuovo, la scelta di una porta casuale nell'intervallo hello 49152 e 65535 per numero di porta esterna hello. Per ulteriori informazioni, vedere [come tooset endpoint della macchina virtuale tooa](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="source-4-network-security-groups"></a>Origine 4: gruppi di sicurezza di rete
I gruppi di sicurezza di rete consentono un controllo più granulare del traffico in entrata e in uscita consentito. È possibile creare regole che si estendono alle subnet e ai servizi cloud in una rete virtuale di Azure.

Utilizzare [flusso IP verificare](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm se una regola in un gruppo di sicurezza di rete sta bloccando il traffico tooor da una macchina virtuale. È anche possibile esaminare il gruppo di sicurezza efficace tooensure in ingresso "Consenti" gruppo di regole regole esiste e viene assegnata la priorità per la porta RDP (impostazione predefinita 3389). Per ulteriori informazioni, vedere [tootroubleshoot utilizzando regole di sicurezza efficace VM traffico](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

## <a name="source-5-windows-based-azure-vm"></a>Origine 5: Macchina virtuale di Azure basata su Windows
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

Seguire le istruzioni hello [questo articolo](reset-rdp.md). In questo articolo consente di reimpostare il servizio di Desktop remoto sulla macchina virtuale hello hello:

* Abilitare la regola predefinita di hello "Desktop remoto" Windows Firewall (porta TCP 3389).
* Abilitare le connessioni Desktop remoto impostando hello HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections del Registro di sistema valore too0.

Riprovare hello connessione dal computer. Se si è ancora impossibile tooconnect tramite Desktop remoto, verificare la presenza hello possibili problemi seguenti:

* Hello servizio Desktop remoto non è in esecuzione sulla destinazione hello macchina virtuale.
* Hello servizio Desktop remoto non è in ascolto sulla porta TCP 3389.
* Windows Firewall o un altro firewall locale dispone di una regola in uscita che impedisce il traffico di Desktop remoto.
* Rilevamento delle intrusioni o software in esecuzione nella macchina virtuale di Azure hello di monitoraggio della rete impedisce le connessioni Desktop remoto.

Per le macchine virtuali create utilizzando il modello di distribuzione classica hello, è possibile utilizzare un toohello di sessione di PowerShell di Azure remoto macchina virtuale di Azure. In primo luogo, è necessario tooinstall un certificato di servizio cloud di hosting della macchina virtuale hello. Andare troppo[tooAzure configurare Secure PowerShell l'accesso remoto le macchine virtuali](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) e scaricare hello **InstallWinRMCertAzureVM.ps1** computer locale tooyour file di script.

Successivamente, installare Azure PowerShell, se non è stato già installato. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

Successivamente, aprire un prompt dei comandi di Azure PowerShell e modificare hello toohello percorso della cartella corrente di hello **InstallWinRMCertAzureVM.ps1** file di script. toorun uno script di PowerShell di Azure, è necessario impostare i criteri di esecuzione corretta di hello. Eseguire hello **Get-ExecutionPolicy** comando toodetermine il livello corrente di criteri. Per informazioni sull'impostazione livello appropriato di hello, vedere [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).

Successivamente, compilare il nome della sottoscrizione di Azure, nome del servizio cloud hello e il nome della macchina virtuale (con rimozione hello < e > caratteri) e quindi eseguire i comandi.

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

È possibile ottenere il nome di sottoscrizione corretta hello da hello *SubscriptionName* proprietà di visualizzazione hello di hello **Get-AzureSubscription** comando. È possibile ottenere un nome del servizio cloud hello per la macchina virtuale hello da hello *ServiceName* colonna nell'area di visualizzazione di hello hello **Get-AzureVM** comando.

Controllare se si dispone di hello nuovo certificato. Aprire uno snap-in certificati per l'utente corrente hello e cercare nella hello **autorità di certificazione radice attendibili** cartella. Verrà visualizzato un certificato con il nome DNS hello del servizio cloud in hello toocolumn rilasciato (esempio: cloudservice4testing.cloudapp.net).

Successivamente, avviare una sessione remota di Azure PowerShell utilizzando questi comandi.

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

Dopo aver immesso le credenziali di amministratore valido, verrà visualizzato un codice simile toohello dopo il prompt di PowerShell di Azure:

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

Hello prima parte di questo messaggio è il nome del servizio cloud che contiene la destinazione hello macchina virtuale, che può essere diverso da "cloudservice4testing.cloudapp.net". È possibile emettere comandi Azure PowerShell per il cloud problemi di hello tooinvestigate servizio indicati e correggere la configurazione hello.

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a>hello corretto toomanually porta TCP in ascolto di Servizi Desktop remoto
Al prompt di sessione PowerShell di Azure remoto hello, eseguire questo comando.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

proprietà PortNumber Hello Mostra il numero di porta corrente hello. Se necessario, modificare hello Desktop remoto porta numero tooits indietro valore predefinito (3389) tramite questo comando.

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

Verificare che porta hello sia stato modificato too3389 tramite questo comando.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Uscire dalla sessione remota di PowerShell di Azure hello tramite questo comando.

```powershell
Exit-PSSession
```

Verificare che hello endpoint Desktop remoto per la macchina virtuale di Azure hello utilizzata anche la porta TCP 3398 come la porta interna. Riavviare hello Azure VM e riprovare hello connessione Desktop remoto.

## <a name="additional-resources"></a>Risorse aggiuntive
[Come tooreset una password o hello Desktop remoto il servizio per le macchine virtuali Windows](reset-rdp.md)

[Come tooinstall e configurare Azure PowerShell](/powershell/azure/overview)

[Risoluzione dei problemi di Secure Shell (SSH) connessioni tooa basati su Linux macchina virtuale di Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Risoluzione dei problemi di accesso tooan applicazione in esecuzione in una macchina virtuale di Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

