---
title: aaaPowerShell per la gestione dei dispositivi StorSimple | Documenti Microsoft
description: Informazioni su come toouse Windows PowerShell per StorSimple toomanage dispositivo StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0ff3bb0d-897a-4676-bdcb-402c2628dac5
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: alkohli@microsoft.com
ms.openlocfilehash: 1adcbb8bb89e3e3b4f328aac198690476c2a78cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>Usare Windows PowerShell per StorSimple tooadminister il dispositivo
## <a name="overview"></a>Panoramica
Windows PowerShell per StorSimple offre un'interfaccia della riga di comando che è possibile utilizzare toomanage dispositivo StorSimple di Microsoft Azure. Come suggerisce il nome di hello, è un'interfaccia della riga di comando basata su Windows PowerShell che viene compilata in uno spazio di esecuzione vincolato. Dal punto di vista hello dell'utente hello nella riga di comando hello, spazio di esecuzione vincolato appare come una versione di Windows PowerShell con restrizioni. Pur mantenendo alcune delle funzionalità di base hello di Windows PowerShell, questa interfaccia ha altri cmdlet dedicati che sono pensati per la gestione del dispositivo StorSimple di Microsoft Azure. 

In questo articolo descrive hello Windows PowerShell per StorSimple caratteristiche e come è possibile connettere l'interfaccia toothis e contiene le procedure dettagliate toostep collegamenti o flussi di lavoro che è possibile eseguire mediante questa interfaccia. flussi di lavoro Hello includono come tooregister il dispositivo, configurare l'interfaccia di rete hello sul dispositivo, installare gli aggiornamenti che richiedono hello toobe di dispositivo in modalità manutenzione, modificare lo stato del dispositivo, hello e risolvere eventuali problemi che potrebbero verificarsi.

Dopo aver letto l'articolo, l'utente sarà in grado di:

* Connettere il dispositivo di StorSimple tooyour tramite Windows PowerShell per StorSimple.
* Amministrazione del dispositivo StorSimple utilizzando Windows PowerShell per StorSimple
* Ottenere la guida in Windows PowerShell per StorSimple

> [!NOTE]
> * Windows PowerShell per StorSimple cmdlet consentono di toomanage dispositivo StorSimple da una console seriale oppure in modalità remota tramite comunicazione remota di Windows PowerShell. Per ulteriori informazioni su ognuna di hello singoli cmdlet che possono essere usati in questa interfaccia, andare troppo[riferimento ai cmdlet di Windows PowerShell per StorSimple](https://technet.microsoft.com/library/dn688168.aspx).
> * i cmdlet di PowerShell Azure StorSimple Hello sono un diverso insieme di cmdlet che consentono di tooautomate StorSimple a livello di servizio e le attività di migrazione dalla riga di comando hello. Per ulteriori informazioni su hello cmdlet di Azure PowerShell per StorSimple, visitare toohello [riferimento ai cmdlet di Azure StorSimple](/powershell/module/azure/?view=azuresmps-3.7.0).
> 
> 

È possibile accedere hello Windows PowerShell per StorSimple utilizzando uno dei seguenti metodi hello:

* [Connettersi tooStorSimple console seriale del dispositivo](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [La connessione remota tooStorSimple tramite Windows PowerShell](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>Connessione tooWindows PowerShell per StorSimple tramite console seriale del dispositivo hello
È possibile [scaricare PuTTY](http://www.putty.org/) o simile tooWindows di tooconnect software di emulazione di terminale PowerShell per StorSimple. È necessario tooconfigure PuTTY in modo specifico tooaccess hello dispositivo Microsoft Azure StorSimple. Hello argomenti seguenti sono contenute istruzioni dettagliate su come tooconfigure PuTTy e connettere il dispositivo toohello. Vengono anche illustrate nella console seriale hello diverse opzioni di menu.

### <a name="putty-settings"></a>Impostazioni puTTY
Assicurarsi di utilizzare hello seguendo l'interfaccia di Windows PowerShell di impostazioni di PuTTY tooconnect toohello dalla console seriale hello.

#### <a name="tooconfigure-putty"></a>tooconfigure PuTTY
1. In hello PuTTY **riconfigurazione** della finestra di dialogo hello **categoria** riquadro, selezionare **tastiera**.
2. Assicurarsi che tale hello le opzioni seguenti siano selezionati (queste sono le impostazioni predefinite di hello quando si avvia una nuova sessione). 
   
   | Elemento tastiera | Selezionare |
   | --- | --- |
   | Tasto backspace |Ctrl-? (127) |
   | Tasti home o fine |Standard |
   | Tasti e tastierino funzione |ESC[n~ |
   | Stato iniziale dei tasti cursore |Normale |
   | Stato iniziale del tastierino numerico |Normale |
   | Abilitare le funzionalità di tastiera aggiuntive |Ctrl-Alt è diverso da AltGr |
   
    ![Impostazioni PuTTY supportate](./media/storsimple-windows-powershell-administration/IC740877.png)
3. Fare clic su **Apply**.
4. In hello **categoria** riquadro, selezionare **traduzione**.
5. In hello **set di caratteri remota** casella di riepilogo, seleziona **UTF-8**.
6. Sotto **Gestione dei caratteri lineette** selezionare **Usa punti di codice lineette Unicode**. Hello figura seguente mostra selezioni PuTTY corrette hello.
   
    ![Impostazioni PuTTY UTF](./media/storsimple-windows-powershell-administration/IC740878.png)
7. Fare clic su **Apply**.

È ora possibile utilizzare console seriale del dispositivo toohello tooconnect PuTTY attenendosi alla procedura seguente hello.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>Informazioni sulla console seriale hello
Quando si accede di interfaccia di Windows PowerShell hello del dispositivo StorSimple tramite la console seriale hello, viene visualizzato un messaggio banner seguito da opzioni di menu. 

messaggio banner contiene informazioni di dispositivo StorSimple base, ad esempio modello hello, nome, versione del software installata e stato del controller hello che si accede. Hello seguente immagine mostra un esempio di un messaggio banner.

![Messaggio di intestazione seriale](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> È possibile utilizzare hello intestazione messaggio tooidentify se hello controller si è connessi toois attivo o passivo.
> 
> 

Hello seguente immagine Mostra hello varie opzioni di spazio di esecuzione che sono disponibili nel menu della console seriale hello.

![Registrare il dispositivo 2](./media/storsimple-windows-powershell-administration/IC740906.png)

È possibile scegliere tra hello seguenti impostazioni:

1. **Accedi con accesso completo** questa opzione consente di tooconnect (con credenziali appropriate hello) toohello **SSAdminConsole** spazio di esecuzione sul controller locale hello. (hello locale è hello controller che si accede attualmente tramite la console seriale di hello del dispositivo StorSimple.) Questa opzione può essere usata anche tooallow tooaccess supporto illimitato tootroubleshoot spazio di esecuzione (una sessione di supporto) eventuali problemi di periferica possibili. Dopo aver utilizzato l'opzione 1 toolog in, è possibile consentire tecnico del supporto Microsoft hello runspace tooaccess senza restrizioni eseguendo un cmdlet specifico. Per informazioni dettagliate, vedere troppo[avviare una sessione di supporto](storsimple-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple).
2. **Accedi al controller toopeer con accesso completo** questa opzione è hello uguale all'opzione 1, ad eccezione del fatto che sia possibile connettersi (con credenziali appropriate hello) toohello **SSAdminConsole** spazio di esecuzione sul controller peer hello. Poiché il dispositivo di StorSimple hello è un dispositivo a disponibilità elevata con due controller in una configurazione attiva-passiva, peer si riferisce toohello altri controller di dispositivo hello che si accede tramite la console seriale hello).
   Toooption simile 1, questa opzione può essere anche usato tooallow supporto Microsoft tooaccess illimitato runspace in un controller peer.
3. **Connetti con accesso limitato** questa opzione è utilizzata tooaccess interfaccia Windows PowerShell in modalità limited. Non vengono richieste le credenziali di accesso. Questa opzione consente di connettersi tooa più limitato rispetto allo spazio di esecuzione toooptions 1 e 2.  Alcune delle attività hello che sono disponibili tramite l'opzione 1 che **Impossibile* essere eseguite in questo spazio di esecuzione sono:
   
   * Ripristinare le impostazioni di fabbrica toohello
   * Modificare la password hello
   * Abilitazione o disabilitazione dell'accesso del supporto
   * Applicazione degli aggiornamenti
   * Installazione degli aggiornamenti rapidi 

    > [!NOTE]
    > Questo è l'opzione hello preferito se si dimentica la password di amministratore dispositivo hello e non può connettersi tramite l'opzione 1 o 2.

4. **Modifica lingua** questa opzione consente di lingua di visualizzazione toochange hello nell'interfaccia di Windows PowerShell hello. lingue Hello supportate sono inglese, giapponese, russo, francese, Sud-coreano, spagnolo, italiano, tedesco, cinese e portoghese (Brasile).

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>Connettersi in remoto mediante Windows PowerShell per StorSimple tooStorSimple
È possibile utilizzare il dispositivo StorSimple tooyour di Windows PowerShell remoting tooconnect. Quando ci si connette in questo modo, non verrà visualizzato un menu. (Menu viene visualizzato solo se si utilizza la console seriale hello in tooconnect dispositivo hello. Connessione remota consente di passare direttamente toohello equivalente di "opzione 1: accesso completo" sulla console seriale hello.) Con la comunicazione remota di Windows PowerShell, è connettersi tooa spazio di esecuzione specifico. È inoltre possibile specificare la lingua di visualizzazione hello. 

Hello lingua di visualizzazione è indipendente dalla lingua hello impostate tramite hello **Cambia lingua** opzione nel menu della console seriale hello. PowerShell remoto rileverà automaticamente dalle impostazioni locali hello del dispositivo hello che ci si connette da se non è specificato.

> [!NOTE]
> Se si lavora con gli host virtuali di Microsoft Azure e i dispositivi virtuali StorSimple, è possibile utilizzare Windows PowerShell remoting e hello host virtuale tooconnect toohello dispositivo virtuale. Se configuri un percorso di condivisione in host hello in quali informazioni toosave dalla sessione di Windows PowerShell hello, è necessario tenere presente che hello che Everyone principale include solo gli utenti autenticati. Pertanto, se è stato configurato l'accesso tooallow hello condivisione da parte degli utenti e si connette senza specificare le credenziali, verrà utilizzata l'entità anonimi non autenticati hello e verrà visualizzato un errore. toofix questo problema, in hello condividere host è necessario abilitare l'account Guest hello e quindi consentire la condivisione toohello hello Guest account accesso completo oppure è necessario specificare credenziali valide con hello cmdlet di Windows PowerShell.
> 
> 

È possibile utilizzare HTTP o HTTPS tooconnect tramite comunicazione remota di Windows PowerShell. Utilizzare le istruzioni di hello in hello seguenti esercitazioni:

* [Connessione tramite HTTP](storsimple-remote-connect.md#connect-through-http)
* [Connessione tramite HTTPS](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>Considerazioni sulla sicurezza di connessione
Quando si decide come tooconnect tooWindows PowerShell per StorSimple, considerare l'esempio hello:

* La connessione diretta toohello console seriale del dispositivo è protetto, ma connessione toohello console seriale tramite commutatori di rete non è. Prestare attenzione hello rischi di sicurezza durante la connessione seriale toodevice tramite commutatori di rete.
* Connessione tramite una sessione HTTP può offrire maggiore sicurezza rispetto alla connessione tramite la console seriale hello in rete. Anche se non si tratta metodo più sicuro hello, è accettabile su reti attendibili.
* Connessione tramite una sessione HTTPS è hello più sicura e hello opzione consigliata.

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>Amministrazione del dispositivo StorSimple tramite Windows PowerShell per StorSimple
Hello nella tabella seguente mostra un riepilogo di tutte le attività di gestione comuni hello e flussi di lavoro complessi che possono essere eseguite nell'interfaccia di Windows PowerShell hello del dispositivo StorSimple. Per ulteriori informazioni su ogni flusso di lavoro, fare clic sulla voce appropriata di hello nella tabella hello.

#### <a name="windows-powershell-for-storsimple-workflows"></a>Flussi di lavoro di Windows PowerShell per StorSimple
| Se si desidera toodo... | Usare questa procedura. |
| --- | --- |
| Registrazione del dispositivo |[Configurare e registrare il dispositivo hello tramite Windows PowerShell per StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| Configurare il proxy web </br>Visualizzare le impostazioni del proxy web |[Configurare il proxy web per il dispositivo StorSimple](storsimple-configure-web-proxy.md) |
| Modifica delle impostazioni dell'interfaccia di rete DATA 0 sul dispositivo |[Modificare le impostazioni dell'interfaccia di rete DATA 0 per il dispositivo StorSimple](storsimple-modify-data-0.md) |
| Arrestare un controller  </br> Riavviare o arrestare un controller </br> Arrestare un dispositivo</br>Ripristinare le impostazioni predefinite di hello dispositivo toofactory |[Gestire i controller dei dispositivi](storsimple-manage-device-controller.md) |
| Installazione degli aggiornamenti in modalità di manutenzione e rapidi |[Aggiornare il dispositivo](storsimple-update-device.md) |
| Inserire la modalità di manutenzione  </br>Uscire dalla modalità di manutenzione |[Modalità del dispositivo StorSimple](storsimple-device-modes.md) |
| Creare un pacchetto di supporto</br>Decrittografare e modificare un pacchetto di supporto |[Creare e gestire un pacchetto di supporto](storsimple-create-manage-support-package.md) |
| Avviare una sessione di supporto </br> |[Avviare una sessione di supporto in Windows PowerShell per StorSimple](storsimple-create-manage-support-package.md#manually-create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>Ottenimento della guida in Windows PowerShell per StorSimple
In Windows PowerShell per StorSimple è disponibile la guida per i cmdlet. Una versione online aggiornata di tale Guida è disponibile anche che è possibile utilizzare tooupdate hello della Guida nel sistema.

Ottenere informazioni della Guida in questa interfaccia è toothat simili in Windows PowerShell e la maggior parte dei cmdlet correlati della Guida hello funzionerà. È possibile trovare della Guida di Windows PowerShell online nella libreria TechNet hello: [Scripting con Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=108518).

di seguito Hello è una breve descrizione dei tipi di hello della Guida per l'interfaccia di Windows PowerShell, incluso come tooupdate hello della Guida.

#### <a name="tooget-help-for-a-cmdlet"></a>tooget della Guida per un cmdlet
* tooget della Guida per qualsiasi cmdlet o una funzione, utilizzare hello comando seguente:`Get-Help <cmdlet-name>`
* tooget Guida online per qualsiasi cmdlet, usare i cmdlet precedente hello con hello `-Online` parametro:`Get-Help <cmdlet-name> -Online`
* Per informazioni complete, è possibile utilizzare hello `–Full` parametro e per esempi, utilizzare hello `–Examples` parametro.

#### <a name="tooupdate-help"></a>tooupdate della Guida
È possibile aggiornare facilmente la Guida di interfaccia di Windows PowerShell hello hello. Eseguire hello seguendo i passaggi tooupdate hello della Guida nel sistema.

#### <a name="tooupdate-cmdlet-help"></a>Guida dei cmdlet tooupdate
1. Avviare Windows PowerShell con hello **Esegui come amministratore** opzione.
2. Al prompt dei comandi di hello, digitare:`Update-Help`
3. Hello aggiornati della Guida verranno installati i file.
4. Una volta installati i file della Guida di hello, digitare: `Get-Help Get-Command`. Verrà visualizzato un elenco dei cmdlet per cui è disponibile la guida.

> [!NOTE]
> un elenco di tutti i cmdlet disponibili hello in uno spazio di esecuzione tooget accedere toohello voce di menu corrispondente ed eseguire hello `Get-Command` cmdlet.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Se si verificano problemi con il dispositivo StorSimple durante l'esecuzione di uno di hello sopra i flussi di lavoro, fare riferimento troppo[strumenti per la risoluzione dei problemi delle distribuzioni di StorSimple](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments).

