---
title: risoluzione dei problemi Site Recovery aaaAzure da VMware tooAzure | Documenti Microsoft
description: Risoluzione degli errori durante la replica di macchine virtuali di Azure
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Risoluzione dei problemi di installazione push del servizio Mobility

In questo articolo illustra in dettaglio hello comuni problemi durante il tentativo di hello tooinstall servizio di mobilità nel server toosource per abilitare la protezione.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(Codice di errore 95107) Non è stato possibile abilitare la protezione.
**Codice errore** | **Possibili cause** | **Indicazioni specifiche per l'errore**
--- | --- | ---
95107 </br>***Messaggio -*** l'installazione Push del computer di origine toohello servizio mobility hello non riuscita con codice di errore ***EP0858***. <br> Le credenziali di hello fornito tooinstall servizio di mobilità non è corretto o account utente di hello dispone di privilegi sufficienti | Le credenziali dell'utente fornito tooinstall di servizio di mobilità nel computer di origine non è corretto | Verificare le credenziali utente hello fornite per il computer di origine hello nel server di configurazione siano corrette. <br> le credenziali utente tooadd/modifica: passare tooconfiguration server > Cspsconfigtool icona > Gestisci account. </br> Assicurarsi inoltre seguito i prerequisiti sono selezionati toosuccessfully completa l'installazione push.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(Codice di errore 95015) Non è stato possibile abilitare la protezione.
**Codice errore** | **Possibili cause** | **Indicazioni specifiche per l'errore**
--- | --- | ---
95105 </br>***Messaggio -*** l'installazione Push del computer di origine toohello servizio mobility hello non riuscita con codice di errore ***EP0856***. <br> "Condivisione File e stampanti" non è consentita nel computer di origine hello oppure sono presenti problemi di connettività di rete tra il server di elaborazione hello e computer di origine hello| Condivisione file e stampanti non è abilitato | Consenti "Condivisione File e stampanti" nel computer di origine hello in Windows Firewall, computer di origine toohello Go hello > impostazioni in Windows Firewall > "Consenti app o funzionalità attraverso Firewall" > selezionare "Condivisione File e stampanti per tutti i profili". </br> Assicurarsi inoltre seguito i prerequisiti sono selezionati toosuccessfully completa l'installazione push.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(Codice di errore 95117) Non è stato possibile abilitare la protezione.
**Codice errore** | **Possibili cause** | **Indicazioni specifiche per l'errore**
--- | --- | ---
95117 </br>***Messaggio -*** l'installazione Push del computer di origine toohello servizio mobility hello non riuscita con codice di errore ***EP0865***. <br> Il computer di origine hello non è in esecuzione o sono presenti problemi di connettività di rete tra il server di elaborazione hello e computer di origine hello | Connettività di rete tra il server di elaborazione e il server di origine | Controllare la connettività di rete tra il server di elaborazione e il server di origine. </br> Assicurarsi inoltre seguito i prerequisiti sono selezionati toosuccessfully completa l'installazione push.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(Codice di errore 95103) Non è stato possibile abilitare la protezione.
**Codice errore** | **Possibili cause** | **Indicazioni specifiche per l'errore**
--- | --- | ---
95103 </br>***Messaggio -*** l'installazione Push del computer di origine toohello servizio mobility hello non riuscita con codice di errore ***EP0854***. <br> "Strumentazione gestione Windows (WMI)" non è consentita nel computer di origine hello oppure sono presenti problemi di connettività di rete tra il server di elaborazione hello e computer di origine hello| Strumentazione gestione Windows (WMI) è bloccato in hello Windows Firewall | Consente di Strumentazione gestione Windows (WMI) in Windows Firewall hello. In Impostazioni di Windows Firewall > "Consenti app o funzionalità attraverso Windows Firewall" > selezionare "WMI per tutti i profili". </br> Assicurarsi inoltre seguito i prerequisiti sono selezionati toosuccessfully completa l'installazione push.

## <a name="check-push-install-logs-for-errors"></a>Controllare gli errori nei log di installazione push

Nel server di configurazione o il processo di hello, passare toofile 'PushinstallService' si trova in <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand hello origine problema hello e utilizzare seguito problema hello tooresolve di passaggi di risoluzione dei problemi.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Prerequisiti per l'installazione push per Windows
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>Verificare che "Condivisione file e stampanti" sia abilitato
Consenti "Condivisione File e stampanti" e "Strumentazione gestione Windows" nel computer di origine hello in hello Windows Firewall </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Se il computer di origine è aggiunto a un dominio: </br>
Configurare le impostazioni del firewall mediante la Console Gestione Criteri di gruppo.
1. Dominio di accesso tooActive directory computer come amministratore e aprire Console Gestione criteri di gruppo (GPMC. MSC, eseguire da un avvio > eseguire).</br>
3. Se non è installato Gestione criteri di gruppo, seguire il collegamento hello troppo[hello installazione Gestione criteri di gruppo](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. Nella finestra di console Gestione criteri di gruppo di hello, fare doppio clic su oggetti Criteri di gruppo nella foresta hello e nel dominio e passare troppo "Criterio dominio predefinito". </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. Fare clic con il pulsante destro del mouse su "Default Domain Policy" (Criterio di dominio predefinito) > Modifica > verrà aperta una nuova finestra "Editor Gestione Criteri di gruppo ". </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. In Editor Gestione criteri di gruppo hello passare tooComputer configurazione > Criteri > modelli amministrativi > rete > connessioni di rete > Windows Firewall. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Abilitare hello seguendo le impostazioni per il profilo di dominio e profilo Standard </br>
a) Fare doppio clic sull'eccezione "Windows Firewall: consenti eccezione per condivisione file e stampanti in ingresso". Selezionare Abilitato e fare clic su OK. </br>
a) Fare doppio clic sull'eccezione "Windows Firewall: consenti eccezione amministrazione remota in ingresso". Selezionare Abilitato e fare clic su OK. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Se il computer di origine non è aggiunto a un dominio e non fa parte del gruppo di lavoro </br>
Configurare le impostazioni del firewall nel computer remoto per il gruppo di lavoro:
1. Passare il computer di origine toohello,</br>
2. in Impostazioni di Windows Firewall > "Consenti app o funzionalità attraverso Windows Firewall" > selezionare "Condivisione file e stampanti per tutti i profili". </br>
3. In Impostazioni di Windows Firewall > "Consenti app o funzionalità attraverso Windows Firewall" > selezionare "WMI per tutti i profili". </br>

#### <a name="disable-remote-user-account-control-uac"></a>Disabilitare il controllo dell'account utente remoto
Disabilitare il controllo dell'account utente tramite servizio di mobilità hello toopush chiave del Registro di sistema.
1. Fare clic su Start > Esegui > digitare regedit > INVIO
2. Individuare e quindi fare clic su hello seguente sottochiave del Registro di sistema: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. Se non esiste una voce del Registro di sistema LocalAccountTokenFilterPolicy hello, seguire questi passaggi:
4. Menu Modifica hello > Nuovo > fare clic su valore DWORD.
5. Digitare LocalAccountTokenFilterPolicy e quindi premere INVIO.
6. Fare clic con il pulsante destro del mouse su LocalAccountTokenFilterPolicy e quindi fare clic su Modifica.
7. Nella casella dati valore hello digitare 1 e quindi fare clic su OK.
8. Uscire da Editor del Registro di sistema.


## <a name="push-install-pre-requisites-for-linux"></a>Prerequisiti per l'installazione push per Linux:

1. Creare un utente radice nel server di hello origine Linux. (Utilizzare questo account solo per gli aggiornamenti e l'installazione push hello)</br>
2. Controllare il file /etc/hosts hello sull'origine hello Linux server dispone di voci che eseguono il mapping di indirizzi di tooIP hello nome host locale associati a tutte le schede di rete. </br>
3. Verificare che hello più recente openssh, il server di openssh e openssl pacchetti installati nel server di origine Linux. </br>
Controllare che la porta 22 SSH sia abilitata e in esecuzione. </br>
4. Controllare se le voci non aggiornate di agenti sono già presenti nel server di origine hello, disinstallare gli agenti precedenti hello e riavviare il server di hello, reinstallare l'agente. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>Abilitare l'autenticazione SFTP di sottosistema e la password nel file sshd_config hello
1. Nel server di origine accedere come utente ROOT. </br>
2. Nel file hello file /etc/ssh/sshd_config</br> trovare hello riga che inizia con PasswordAuthentication. </br>
3. d.   Rimuovere il commento riga hello e hello valore da "no" troppo "yes". </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. Rimuovere il commento riga hello trovare riga hello che inizia con "Sottosistema". </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Salvare le modifiche di hello e riavviare il servizio di sshd hello. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>Controlli dell'installazione push nel server di configurazione o del processo.
#### <a name="validate-credentials-for-discovery-and-installation"></a>Convalidare le credenziali per l'individuazione e l'installazione

1. Nel server di configurazione avviare Cspsconfigtool</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Assicurarsi che l'account hello utilizzato per la protezione con diritti di amministratore nel computer di origine hello. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>Controllare la connettività tra il server di elaborazione e il server di origine
1. Verificare che il server di elaborazione disponga di una connessione Internet.
2. Verificare la connessione WMI tramite wbemtest.exe. </br>
Nel server di elaborazione hello, fare clic su Start > eseguire > wbemtest.exe > verrà aperta la finestra Tester di Strumentazione gestione Windows come illustrato.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Fare clic su Connetti > Immettere IP di server di origine hello hello Namespace Input utente nome e Password (se il computer di origine è aggiunto a un dominio, specificare il nome di dominio hello insieme a nome utente come "Nomedominio\nomeutente". Se il computer di origine si trova in workgroup, specificare solo il nome di utente hello.) Selezionare il livello di autenticazione hello come riservatezza pacchetto. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Fare clic su Connetti. Ora connessione WMI hello dovrebbe essere completata con hello ha fornito dati e deve essere visualizzata la finestra di Tester di Strumentazione gestione Windows hello come illustrato di seguito: </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   Se la connessione WMI non è riuscita verrà visualizzato un messaggio di errore. Hello seguente schermata mostra un tentativo non riuscito se amministrazione WMI/remota non è abilitato in consentiti di app di Windows firewall. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Controllare lo stato WMI hello e connettività.</br>
Nel server di configurazione o il processo di hello, </br>
Fare clic su start > eseguire > wmimgmt.msc > Azioni > più azioni > connettere tooanother computer (computer di origine). </br>
Immettere le credenziali di hello di hello account utilizzato per la protezione e controllo se la connettività è appropriata. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Verificare che le cartelle condivise in rete del computer di origine siano accessibili dal server di elaborazione in modalità remota con le credenziali specificate.
  1. Computer di accesso tooProcess Server (PS), aprire Esplora File > nel tipo di barra indirizzo hello > "\\\source-machine-ip\C$" > fare clic su INVIO. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. Esplora file richiederà le credenziali. Immettere nome utente hello e una password > fare clic su OK.</br>
   Se il computer di origine è aggiunto a un dominio, è possibile specificare il nome di dominio hello insieme a nome utente come "Nomedominio\nomeutente".</br>
   Se il computer di origine si trova in workgroup, fornire solo hello "username". </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Se la connessione riesce, è possibile visualizzare le cartelle di hello del computer di origine in modalità remota dal processo Server (PS) </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Se la connessione ha esito negativo, verificare che tutti i prerequisiti siano soddisfatti.
>

Se non si desidera tooopen "Strumentazione gestione Windows", è anche possibile installare il servizio di mobilità a manualmente nel computer di origine hello.</br> [Installare manualmente il Servizio Mobility tramite la GUI](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Installazione tramite Configuration manager](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Passaggi successivi
- [Abilitare la replica delle macchine virtuali VMware](vmware-walkthrough-enable-replication.md)
