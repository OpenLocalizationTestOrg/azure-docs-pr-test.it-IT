---
title: aaaCannot connettersi con RDP tooa macchina virtuale Windows in Azure | Documenti Microsoft
description: "Risolvere i problemi quando non è possibile connettersi tooyour macchina virtuale di Windows in Azure tramite Desktop remoto"
keywords: "Errore di desktop remoto, errore di connessione desktop remoto, non è possibile connettersi tooVM, risoluzione dei desktop remoto"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a>Risolvere i problemi relativi a connessioni di Desktop remoto tooan macchina virtuale di Azure
Hello Remote Desktop Protocol (RDP) connessione tooyour basati su Windows Azure macchina virtuale (VM) può non riuscire per vari motivi, lasciando è Impossibile tooaccess la macchina virtuale. problema di Hello può essere hello servizio Desktop remoto su hello macchina virtuale, la connessione di rete hello o hello client di Desktop remoto nel computer host. In questo articolo descrive alcuni aspetti hello più comuni metodi tooresolve RDP connessione. 

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/support/forums/). In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**.

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a>Passaggi rapidi per la risoluzione dei problemi
Dopo ogni passaggio della risoluzione dei problemi, provare a riconnettersi toohello VM:

1. Ripristinare la configurazione del desktop remoto.
2. Controllare le regole degli endpoint del gruppo di sicurezza di rete/Servizi cloud.
3. Esaminare i log della console della VM.
4. Reimpostare hello NIC per hello macchina virtuale.
5. Hello controllo integrità delle risorse di macchina virtuale.
6. Reimpostare la password della VM.
7. Riavviare la VM.
8. Ripetere la distribuzione della VM.

Continuare la lettura per procedure dettagliate e altre informazioni. Verificare che le apparecchiature di rete locali quali router e firewall non blocchino la porta TCP in uscita 3389, come indicato negli [scenari dettagliati di risoluzione dei problemi RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!TIP]
> Se hello **Connetti** pulsante per la macchina virtuale è disattivate nel portale di hello e non si è connessi tooAzure tramite un [Express Route](../../expressroute/expressroute-introduction.md) o [VPN Site-to-Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connessione, è necessario toocreate e assegnare l'indirizzo di un indirizzo IP pubblico di una macchina virtuale prima è possibile utilizzare il protocollo RDP. Altre informazioni sono disponibili in [Indirizzi IP pubblici in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).


## <a name="ways-tootroubleshoot-rdp-issues"></a>Problemi di modi tootroubleshoot RDP
È possibile risolvere i problemi di macchine virtuali create con modello di distribuzione di gestione risorse di hello utilizzando uno dei seguenti metodi hello:

* [Portale di Azure](#using-the-azure-portal) : eccellente se è necessario tooquickly reimpostare le credenziali utente o configurazione RDP hello e non avere hello installati gli strumenti di Azure.
* [Azure PowerShell](#using-azure-powershell) : se si ha familiarità con un prompt di PowerShell rapidamente reimpostazione hello RDP configurazione le credenziali utente o tramite i cmdlet di PowerShell di Azure hello.

È anche possibile trovare i passaggi per la risoluzione dei problemi delle macchine virtuali create utilizzando hello [il modello di distribuzione classica](#troubleshoot-vms-created-using-the-classic-deployment-model).

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a>Risoluzione dei problemi mediante hello portale di Azure
Dopo ogni passaggio della risoluzione dei problemi, provare a riconnettersi tooyour macchina virtuale. Se non è possibile connettersi, provare a passaggio successivo hello.

1. **Ripristinare la connessione RDP**. Quando le connessioni Remote sono disabilitate o regole di Windows Firewall bloccano RDP, ad esempio, questo passaggio della risoluzione dei problemi Reimposta configurazione RDP hello.
   
    Selezionare la macchina virtuale nel portale di Azure hello. Scorrere verso il basso hello impostazioni riquadro toohello **supporto + Troubleshooting** sezione nella parte inferiore dell'elenco di hello. Fare clic su hello **reimpostazione password** pulsante. Set hello **modalità** troppo**configurazione per la reimpostazione solo** e quindi fare clic su hello **aggiornamento** pulsante:
   
    ![Reimposta configurazione RDP hello in hello portale di Azure](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. **Verificare le regole del gruppo di sicurezza di rete**. Utilizzare [flusso IP verificare](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm se una regola in un gruppo di sicurezza di rete sta bloccando il traffico tooor da una macchina virtuale. È anche possibile esaminare il gruppo di sicurezza efficace tooensure in ingresso "Consenti" gruppo di regole regole esiste e viene assegnata la priorità per la porta RDP (impostazione predefinita 3389). Per ulteriori informazioni, vedere [tootroubleshoot utilizzando regole di sicurezza efficace VM traffico](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

3. **Rivedere la diagnostica di avvio della macchina virtuale**. Questo passaggio della risoluzione dei problemi esamina hello VM console registri toodetermine se hello VM segnala un problema. Poiché la diagnostica di avvio non è abilitata su tutte le macchine virtuali, la procedura può essere facoltativa.
   
    Passaggi di risoluzione dei problemi specifici esulano hello ambito di questo articolo, ma potrebbero indicare un problema più ampio che influisce sulle connettività RDP. Per ulteriori informazioni sull'analisi dei log della console hello e screenshot della macchina virtuale, vedere [la diagnostica di avvio per le macchine virtuali](boot-diagnostics.md).

4. **Reimpostazione hello NIC per hello VM**. Per ulteriori informazioni, vedere [come schede di rete per la macchina virtuale Windows Azure tooreset](reset-network-interface.md).
5. **Controllare l'integrità delle risorse di VM hello**. Questo passaggio della risoluzione dei problemi di verifica non siano presenti problemi noti con hello piattaforma Azure che potrebbe influire sulla connettività toohello macchina virtuale.
   
    Selezionare la macchina virtuale nel portale di Azure hello. Scorrere verso il basso hello impostazioni riquadro toohello **supporto + Troubleshooting** sezione nella parte inferiore dell'elenco di hello. Fare clic su hello **integrità delle risorse** pulsante. Una macchina virtuale integra viene indicata come **Disponibile**:
   
    ![Controllare l'integrità delle risorse di macchina virtuale nel portale di Azure hello](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. **Reimpostare le credenziali utente**. Questo passaggio della risoluzione dei problemi Reimposta password hello in un account amministratore locale quando si è certi o dimenticato credenziali hello.
   
    Selezionare la macchina virtuale nel portale di Azure hello. Scorrere verso il basso hello impostazioni riquadro toohello **supporto + Troubleshooting** sezione nella parte inferiore dell'elenco di hello. Fare clic su hello **reimpostazione password** pulsante. Verificare che hello **modalità** è troppo**reimpostazione password** e quindi immettere il nome utente e una nuova password. Infine, fare clic su hello **aggiornamento** pulsante:
   
    ![Reimpostare le credenziali utente hello in hello portale di Azure](./media/troubleshoot-rdp-connection/reset-password.png)
7. **Riavviare la VM**. Questo passaggio della risoluzione dei problemi è possibile correggere eventuali problemi sottostanti in caso di hello macchina virtuale stessa.
   
    Selezionare la macchina virtuale nel portale di Azure hello e fare clic su hello **Panoramica** scheda. Fare clic su hello **riavviare** pulsante:
   
    ![Riavviare hello VM nel portale di Azure hello](./media/troubleshoot-rdp-connection/restart-vm.png)
8. **Ripetere la distribuzione della VM**. Questo passaggio della risoluzione dei problemi ridistribuisce l'host della macchina virtuale tooanother all'interno di Azure toocorrect eventuali problemi di rete o di piattaforma sottostante.
   
    Selezionare la macchina virtuale nel portale di Azure hello. Scorrere verso il basso hello impostazioni riquadro toohello **supporto + Troubleshooting** sezione nella parte inferiore dell'elenco di hello. Fare clic su hello **ridistribuire** pulsante e quindi fare clic su **ridistribuire**:
   
    ![Ridistribuire Ciao VM hello portale di Azure](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    Al termine di questa operazione, dati su disco temporaneo viene persi e dinamici indirizzi IP associati hello VM vengono aggiornati.

Se continuano a verificarsi errori RDP, è possibile [aprire una richiesta di supporto](https://azure.microsoft.com/support/options/) o leggere i [passaggi e concetti relativi alla risoluzione dettagliata dei problemi RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-using-azure-powershell"></a>Risoluzione dei problemi con Azure PowerShell
Se hai già fatto, [installare e configurare hello più recente di Azure PowerShell](/powershell/azure/overview).

Hello esempi seguenti vengono utilizzate le variabili, ad esempio `myResourceGroup`, `myVM`, e `myVMAccessExtension`. Sostituire i nomi e i percorsi delle variabili con i valori personalizzati.

> [!NOTE]
> Reimpostare le credenziali utente hello e la configurazione RDP hello utilizzando hello [Set AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet di PowerShell. In hello seguono esempi `myVMAccessExtension` è un nome specificato come parte del processo di hello. Se si è utilizzato in precedenza con hello VMAccessAgent, è possibile ottenere il nome di hello di estensione esistente hello utilizzando `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` proprietà hello toocheck di hello macchina virtuale. nome di hello tooview, aspetto nella sezione delle estensioni"hello" dell'output di hello.

Dopo ogni passaggio della risoluzione dei problemi, provare a riconnettersi tooyour macchina virtuale. Se non è possibile connettersi, provare a passaggio successivo hello.

1. **Ripristinare la connessione RDP**. Quando le connessioni Remote sono disabilitate o regole di Windows Firewall bloccano RDP, ad esempio, questo passaggio della risoluzione dei problemi Reimposta configurazione RDP hello.
   
    esempio riportato di seguito Hello Reimposta connessione RDP hello in una macchina virtuale denominata `myVM` in hello `WestUS` percorso e nel gruppo di risorse hello denominato `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. **Verificare le regole del gruppo di sicurezza di rete**. Questo passaggio della risoluzione dei problemi di verifica di disporre di una regola del traffico RDP toopermit il gruppo di sicurezza di rete. porta predefinita Hello per RDP è la porta TCP 3389. Il traffico RDP toopermit una regola potrebbe non essere creato automaticamente quando si crea la macchina virtuale.
   
    In primo luogo, assegnare tutti i dati di configurazione di hello per il gruppo di sicurezza di rete di toohello `$rules` variabile. esempio Hello Ottiene informazioni su gruppo di sicurezza di rete denominata hello `myNetworkSecurityGroup` nel gruppo di risorse hello denominato `myResourceGroup`:
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    A questo punto, hello alle regole della vista che sono configurate per questo gruppo di sicurezza di rete. Verificare che esiste una regola tooallow la porta TCP 3389 per le connessioni in ingresso come indicato di seguito:
   
    ```powershell
    $rules.SecurityRules
    ```
   
    Hello riportato di seguito una regola di sicurezza valido che consenta il traffico RDP. È visualizzata la corretta configurazione di `Protocol`, `DestinationPortRange`, `Direction` e `Access`:
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    Se non è presente una regola che consente il traffico RDP, [creare una regola del gruppo di sicurezza di rete](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Consentire il traffico sulla porta TCP 3389.
3. **Reimpostare le credenziali utente**. Questo passaggio della risoluzione dei problemi Reimposta password account amministratore locale hello specificato quando si è certi dell'o hanno dimenticato credenziali hello hello.
   
    Innanzitutto, specificare hello nome utente e una password tramite l'assegnazione di nuovo le credenziali toohello `$cred` variabile come indicato di seguito:
   
    ```powershell
    $cred=Get-Credential
    ```
   
    A questo punto, aggiornare le credenziali di hello nella VM. esempio Hello Aggiorna credenziali hello in una macchina virtuale denominata `myVM` in hello `WestUS` percorso e nel gruppo di risorse hello denominato `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. **Riavviare la VM**. Questo passaggio della risoluzione dei problemi è possibile correggere eventuali problemi sottostanti in caso di hello macchina virtuale stessa.
   
    Dopo il riavvio di esempio Hello hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. **Ripetere la distribuzione della VM**. Questo passaggio della risoluzione dei problemi ridistribuisce l'host della macchina virtuale tooanother all'interno di Azure toocorrect eventuali problemi di rete o di piattaforma sottostante.
   
    Hello seguenti distribuzioni di esempio hello macchina virtuale denominata `myVM` in hello `WestUS` percorso e nel gruppo di risorse hello denominato `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

Se continuano a verificarsi errori RDP, è possibile [aprire una richiesta di supporto](https://azure.microsoft.com/support/options/) o leggere i [passaggi e concetti relativi alla risoluzione dettagliata dei problemi RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a>Risolvere i problemi relativi a macchine virtuali create utilizzando hello modello di distribuzione classica
Dopo ogni passaggio della risoluzione dei problemi, provare a riconnettersi toohello macchina virtuale.

1. **Ripristinare la connessione RDP**. Quando le connessioni Remote sono disabilitate o regole di Windows Firewall bloccano RDP, ad esempio, questo passaggio della risoluzione dei problemi Reimposta configurazione RDP hello.
   
    Selezionare la macchina virtuale nel portale di Azure hello. Fare clic su hello **... Ulteriori** , quindi fare clic su **Reimposta accesso remoto**:
   
    ![Reimposta configurazione RDP hello in hello portale di Azure](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. **Controllare gli endpoint di Servizi cloud**. Questo passaggio della risoluzione dei problemi di verifica di disporre di endpoint nel traffico RDP toopermit di servizi Cloud. porta predefinita Hello per RDP è la porta TCP 3389. Il traffico RDP toopermit una regola potrebbe non essere creato automaticamente quando si crea la macchina virtuale.
   
   Selezionare la macchina virtuale nel portale di Azure hello. Fare clic su hello **endpoint** pulsante endpoint hello tooview attualmente configurato per la macchina virtuale. Verificare l'esistenza di endpoint che consentono il traffico RDP sulla porta TCP 3389.
   
   Hello di esempio seguente viene illustrato un endpoint valido che consentano il traffico RDP:
   
   ![Verificare gli endpoint di servizi Cloud nel portale di Azure hello](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   Se non è presente un endpoint che consente il traffico RDP, [creare un endpoint di Servizi cloud](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Consenti TCP tooprivate porta 3389.
3. **Rivedere la diagnostica di avvio della macchina virtuale**. Questo passaggio della risoluzione dei problemi esamina hello VM console registri toodetermine se hello VM segnala un problema. Poiché la diagnostica di avvio non è abilitata su tutte le macchine virtuali, la procedura può essere facoltativa.
   
    Passaggi di risoluzione dei problemi specifici esulano hello ambito di questo articolo, ma potrebbero indicare un problema più ampio che influisce sulle connettività RDP. Per ulteriori informazioni sull'analisi dei log della console hello e screenshot della macchina virtuale, vedere [la diagnostica di avvio per le macchine virtuali](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).
4. **Controllare l'integrità delle risorse di VM hello**. Questo passaggio della risoluzione dei problemi di verifica non siano presenti problemi noti con hello piattaforma Azure che potrebbe influire sulla connettività toohello macchina virtuale.
   
    Selezionare la macchina virtuale nel portale di Azure hello. Scorrere verso il basso hello impostazioni riquadro toohello **supporto + Troubleshooting** sezione nella parte inferiore dell'elenco di hello. Fare clic su hello **integrità delle risorse** pulsante. Una macchina virtuale integra viene indicata come **Disponibile**:
   
    ![Controllare l'integrità delle risorse di macchina virtuale nel portale di Azure hello](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. **Reimpostare le credenziali utente**. Questo passaggio della risoluzione dei problemi Reimposta password hello in account di amministratore locale hello specificato quando si è certi o dimenticato credenziali hello.
   
    Selezionare la macchina virtuale nel portale di Azure hello. Scorrere verso il basso hello impostazioni riquadro toohello **supporto + Troubleshooting** sezione nella parte inferiore dell'elenco di hello. Fare clic su hello **reimpostazione password** pulsante. Immettere il nome utente e una nuova password. Infine, fare clic su hello **salvare** pulsante:
   
    ![Reimpostare le credenziali utente hello in hello portale di Azure](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. **Riavviare la VM**. Questo passaggio della risoluzione dei problemi è possibile correggere eventuali problemi sottostanti in caso di hello macchina virtuale stessa.
   
    Selezionare la macchina virtuale nel portale di Azure hello e fare clic su hello **Panoramica** scheda. Fare clic su hello **riavviare** pulsante:
   
    ![Riavviare hello VM nel portale di Azure hello](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

Se continuano a verificarsi errori RDP, è possibile [aprire una richiesta di supporto](https://azure.microsoft.com/support/options/) o leggere i [passaggi e concetti relativi alla risoluzione dettagliata dei problemi RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-specific-rdp-errors"></a>Risolvere errori specifici della connessione RDP
Quando si tenta di tooconnect tooyour macchina virtuale tramite RDP, è possibile riscontrare un messaggio di errore specifico. di seguito Hello sono messaggi di errore più comuni di hello:

* [la sessione remota di Hello è stata disconnessa perché sono non presenti una licenza tooprovide disponibili server licenze di Desktop remoto](troubleshoot-specific-rdp-errors.md#rdplicense).
* [Desktop remoto non è possibile trovare hello "nome computer"](troubleshoot-specific-rdp-errors.md#rdpname).
* [Si è verificato un errore di autenticazione. Hello autorità di protezione locale non può essere contattato](troubleshoot-specific-rdp-errors.md#rdpauth).
* [Errore di sicurezza di Windows: Le credenziali specificate non funzionano](troubleshoot-specific-rdp-errors.md#wincred).
* [Impossibile connettersi computer remoto toohello](troubleshoot-specific-rdp-errors.md#rdpconnect).

## <a name="additional-resources"></a>Risorse aggiuntive
Se nessuno di questi errori si sono verificati e non è possibile connettersi toohello macchina virtuale tramite Desktop remoto, leggere hello dettagliata [risoluzione dei problemi di Guida per il Desktop remoto](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Per la risoluzione dei problemi nell'accesso alle applicazioni in esecuzione in una macchina virtuale, vedere [applicazione tooan accesso di risoluzione dei problemi in esecuzione in una macchina virtuale di Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Se si sono verificati problemi di utilizzo di Secure Shell (SSH) tooconnect tooa VM Linux in Azure, vedere [tooa connessioni risolvere SSH VM Linux di Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

