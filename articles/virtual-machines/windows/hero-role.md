---
title: IIS nella VM Windows prima di aaaInstall | Documenti Microsoft
description: Provare la prima macchina virtuale di Windows, l'installazione di IIS e aprire la porta 80 tramite hello portale di Azure.
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a>Sperimentare l'installazione di un ruolo in una VM Windows
Dopo aver creato il primo e la macchina virtuale (VM) di esecuzione, è possibile spostare in tooinstalling software e servizi. Per questa esercitazione, verrà toouse Server Manager su hello tooinstall di macchina virtuale Windows Server IIS. Quindi, si creerà un sicurezza gruppo (rete) utilizzando il traffico di hello tooopen portale Azure porta 80 tooIIS. 

Se è stata ancora creata la prima macchina virtuale, è necessario tornare troppo[creare la prima macchina virtuale di Windows nel portale di Azure hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di continuare con questa esercitazione.

## <a name="make-sure-hello-vm-is-running"></a>Verificare che hello che macchina virtuale è in esecuzione
1. Aprire hello [portale di Azure](https://portal.azure.com).
2. Nel menu hub hello, fare clic su **macchine virtuali**. Selezionare macchina virtuale hello hello elenco.
3. Se è stato hello **arrestato (deallocato)**, fare clic su hello **avviare** pulsante hello **Essentials** blade di hello macchina virtuale. Se è stato hello **esecuzione**, è possibile spostare nel passaggio successivo toohello.

## <a name="connect-toohello-virtual-machine-and-sign-in"></a>Connettere la macchina virtuale di toohello ed eseguire l'accesso
1. Nel menu hub hello, fare clic su **macchine virtuali**. Selezionare macchina virtuale hello hello elenco.
2. Nel Pannello di hello per la macchina virtuale hello, fare clic su **Connetti**. Viene creato e si scarica un file Remote Desktop Protocol (file con estensione rdp) che è simile a una macchina tooyour tooconnect di scelta rapida. È possibile desktop tooyour di toosave hello file per semplificare l'accesso. **Aprire** questo tooyour tooconnect file macchina virtuale.
   
    ![Schermata di hello che Mostra portale Azure come tooconnect tooyour VM](./media/hero-role/connect.png)
3. Viene visualizzato un avviso che RDP hello è da un editore sconosciuto. Si tratta di una situazione normale. Nella finestra di hello Desktop remoto, fare clic su **Connetti** toocontinue.
   
    ![Screenshot di un avviso relativo a un autore sconosciuto](./media/hero-role/rdp-warn.png)
4. Nella finestra sicurezza di Windows hello tipo hello username e password per l'account locale hello creato al momento della creazione hello macchina virtuale. nome utente Hello viene immesso come *vmname*&#92; *nome utente*, quindi fare clic su **OK**.
   
    ![Schermata di immissione di nome della macchina virtuale hello, nome utente e password](./media/hero-role/credentials.png)
5. Viene visualizzato un avviso non è possibile verificare che il certificato hello. Si tratta di una situazione normale. Fare clic su **Sì** tooverify hello identità della macchina virtuale hello e completare la registrazione.
   
   ![Screenshot che illustra un messaggio sul verifica identità hello di hello VM](./media/hero-role/cert-warning.png)

Se si esegue tootrouble quando si tenta di tooconnect, vedere [tooa connessioni Desktop remoto di risoluzione dei problemi basato su Windows Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="install-iis-on-your-vm"></a>Installare IIS nella macchina virtuale
Ora che si è connessi toohello macchina virtuale, verrà installato un ruolo del server in modo che è possibile provare più.

1. Aprire **Server Manager** se non è già aperto. Fare clic su hello **avviare** menu e quindi fare clic su **Server Manager**.
2. In **Server Manager**selezionare **Server locale** hello nel riquadro di sinistra. 
3. Selezionare menu hello **Gestisci** > **Aggiungi ruoli e funzionalità**.
4. In hello Aggiunta guidata ruoli e funzionalità, su hello **tipo di installazione** pagina, scegliere **installazione basata su ruoli o basata su funzionalità**, quindi fare clic su **Avanti**.
   
    ![Schermata che mostra hello Aggiunta guidata ruoli e funzionalità della scheda per tipo di installazione](./media/hero-role/role-wizard.png)
5. Selezionare hello VM dal pool di server hello e fare clic su **Avanti**.
6. In hello **i ruoli del Server** selezionare **Server Web (IIS)**.
   
    ![Schermata che mostra hello Aggiunta guidata ruoli e funzionalità della scheda per i ruoli del Server](./media/hero-role/add-iis.png)
7. In hello popup sull'aggiunta di funzionalità necessarie per IIS, verificare che **includono gli strumenti di gestione** è selezionata e quindi fare clic su **Aggiungi funzionalità**. Quando si chiude hello popup, fare clic su **Avanti** nella procedura guidata hello.
   
    ![Screenshot che illustra tooconfirm popup Aggiunta ruolo IIS hello](./media/hero-role/confirm-add-feature.png)
8. Nella pagina di funzionalità hello, fare clic su **Avanti**.
9. In hello **ruolo Server Web (IIS)** pagina, fare clic su **Avanti**. 
10. In hello **servizi ruolo** pagina, fare clic su **Avanti**. 
11. In hello **conferma** pagina, fare clic su **installare**. 
12. Installazione di hello termine, fare clic su **Chiudi** nella procedura guidata hello.

## <a name="open-port-80"></a>Aprire la porta 80
Affinché la macchina virtuale di tooaccept il traffico in ingresso sulla porta 80, è necessario tooadd un gruppo di sicurezza di rete toohello regola in ingresso. 

1. Aprire hello [portale di Azure](https://portal.azure.com).
2. In **macchine virtuali** selezionare hello macchina virtuale creata.
3. Nelle impostazioni di hello macchine virtuali, selezionare **interfacce di rete** e quindi selezionare hello interfaccia di rete esistente.
   
    ![Screenshot che illustra l'impostazione hello macchina virtuale per hello interfacce di rete](./media/hero-role/network-interface.png)
4. In **Essentials** per interfaccia di rete hello, fare clic su hello **il gruppo di sicurezza di rete**.
   
    ![Screenshot della sezione di Essentials hello per interfaccia di rete hello](./media/hero-role/select-nsg.png)
5. In hello **Essentials** pannello hello gruppo, è necessario disporre di un valore predefinito esistente regola in entrata per **predefinita-Consenti-rdp** che consentono di toolog in toohello macchina virtuale. Si aggiungerà un altro traffico IIS tooallow regola in ingresso. Fare clic su **Regole di sicurezza in ingresso**.
   
    ![Screenshot della sezione di Essentials hello per hello NSG](./media/hero-role/inbound.png)
6. In **Regole di sicurezza in ingresso** fare clic su **Aggiungi**.
   
    ![Screenshot che illustra hello pulsante tooadd una regola di sicurezza](./media/hero-role/add-rule.png)
7. In **Regole di sicurezza in ingresso** fare clic su **Aggiungi**. Tipo **80** in hello intervallo di porte e assicurarsi che **Consenti** è selezionata. Al termine, fare clic su **OK**.
   
    ![Screenshot che illustra hello pulsante tooadd una regola di sicurezza](./media/hero-role/port-80.png)

Per ulteriori informazioni su NSGs, le regole in entrata e in uscita, vedere [Consenti accesso esterno tooyour VM utilizzando hello portale di Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="connect-toohello-default-iis-website"></a>Connettere il sito Web IIS predefinito toohello
1. Nel portale di Azure hello, fare clic su **macchine virtuali** e quindi selezionare la macchina virtuale.
2. In hello **Essentials** blade, copia il **indirizzo IP pubblico**.
   
    ![Screenshot che illustra in toofind hello indirizzo IP pubblico della macchina virtuale](./media/hero-role/ipaddress.png)
3. Aprire un browser e nella barra degli indirizzi hello, digitare l'indirizzo IP pubblico simile al seguente: http://<publicIPaddress> e fare clic su **invio** toogo toothat indirizzo.
4. Il browser deve aprire una pagina web IIS predefinita hello. Verrà visualizzata una schermata simile alla seguente:
   
    ![Screenshot che illustra la pagina IIS predefinita hello è simile in un browser](./media/hero-role/iis-default.png)

## <a name="next-steps"></a>Passaggi successivi
* È inoltre possibile sperimentare [collegando un disco dati](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) macchina virtuale tooyour. I dischi dati forniscono più risorse di archiviazione per la macchina virtuale.

