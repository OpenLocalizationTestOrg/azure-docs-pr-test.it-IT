---
title: aaaSet di proxy web per un dispositivo StorSimple | Documenti Microsoft
description: Informazioni su come toouse Windows PowerShell per StorSimple tooconfigure web le impostazioni proxy per il dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6c2ca351-a7c6-4da6-ab5e-c081e6d08261
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: c0213eb2a1902ff994147bb16593f0ff300eb70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>Configurare il proxy web per il dispositivo StorSimple
## <a name="overview"></a>Panoramica
Questa esercitazione viene descritto come toouse Windows PowerShell per StorSimple tooconfigure e visualizzazione web le impostazioni proxy per il dispositivo StorSimple. impostazioni del proxy web Hello vengono usate dal dispositivo di StorSimple hello durante la comunicazione con il cloud hello. Un server proxy web è tooadd utilizzato un altro livello di sicurezza, filtrare il contenuto, memorizzare nella cache i requisiti di larghezza di banda tooease o addirittura con analitica.

Il proxy Web è una configurazione facoltativa per il dispositivo StorSimple. È possibile configurare il proxy Web solo tramite Windows PowerShell per StorSimple. configurazione Hello è un processo in due fasi, come indicato di seguito:

1. È innanzitutto necessario configurare le impostazioni di proxy web tramite installazione guidata di hello o Windows PowerShell per i cmdlet di StorSimple.
2. È quindi possibile abilitare le impostazioni di proxy web hello configurato tramite Windows PowerShell per StorSimple cmdlet.

Dopo la configurazione del proxy web hello è stata completata, è possibile visualizzare impostazioni del proxy web hello configurato nel servizio di Microsoft Azure StorSimple Manager hello sia hello Windows PowerShell per StorSimple. 

Dopo aver letto questa esercitazione, si sarà in grado di:

* Configurare il proxy Web utilizzando i cmdlet e l'installazione guidata
* Abilitare il proxy Web utilizzando i cmdlet
* Visualizzare le impostazioni di proxy web nel portale di Azure classico hello
* Risolvere gli errori durante la configurazione del proxy Web

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>Configurare il proxy Web tramite Windows PowerShell per StorSimple
Utilizzare una delle seguenti impostazioni del proxy web tooconfigure hello:

* Installazione guidata tooguide sono illustrati i passaggi di configurazione hello.
* Cmdlet di Windows PowerShell per StorSimple.

Ognuno di questi metodi viene trattata in hello le sezioni seguenti.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Configurare il proxy web tramite installazione guidata di hello
È possibile utilizzare hello l'installazione guidata tooguide che tramite hello i passaggi di configurazione del proxy web. Eseguire hello seguenti proxy web tooconfigure di passaggi nel dispositivo.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>proxy web tooconfigure tramite installazione guidata di hello
1. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo** e fornire hello **password amministratore del dispositivo**. Comando che segue di hello tipo toostart una sessione di installazione guidata:
   
    `Invoke-HcsSetupWizard`
2. Se si tratta di hello prima volta che si usa installazione guidata di hello per la registrazione del dispositivo, è necessario tooconfigure tutte le impostazioni di rete hello necessarie fino a raggiungere configurazione del proxy web hello. Se il dispositivo è già registrato, è possibile accettare tutte le impostazioni di rete configurato hello fino a raggiungere configurazione del proxy web hello. Nella connessione guidata hello quando tooconfigure richiesta web le impostazioni del proxy, digitare **Sì**.
3. Per hello **URL del Proxy Web**, specificare l'indirizzo IP hello o il nome di dominio completo (FQDN) del proxy server e hello TCP numero di porta web che si desidera toouse il dispositivo durante la comunicazione con il cloud hello hello. Utilizzare hello seguente formato:
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    Per impostazione predefinita, viene specificato il numero di porta TCP 8080.
4. Scegliere il tipo di autenticazione hello come **NTLM**, **base**, o **Nessuno**. Basic è l'autenticazione meno sicura per la configurazione del server proxy hello hello. NT LAN Manager (NTLM) è un protocollo di autenticazione estremamente sicuro e complesso che utilizza un sistema di messaggistica a tre vie (talvolta a quattro se è richiesta maggiore integrità) tooauthenticate un utente. autenticazione predefinita Hello è NTLM. Per altre informazioni, vedere l'autenticazione [di base](http://hc.apache.org/httpclient-3.x/authentication.html) e [NTLM](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **Nel servizio StorSimple Manager hello, grafici di monitoraggio del dispositivo hello non funzionano quando base o l'autenticazione NTLM è abilitata nella configurazione del server proxy hello per dispositivo hello. Per hello toowork grafici di monitoraggio, sarà necessario tooensure impostare tooNONE autenticazione.**
   > 
   > 
5. Se si usa l'autenticazione, fornire un **nome utente del proxy Web** e la **password del proxy Web**. È necessario anche password hello tooconfirm.
   
    ![Configurare il proxy Web nel dispositivo StorSimple 1](./media/storsimple-configure-web-proxy/IC751830.png)

Se si registra il dispositivo per hello prima volta, continuare con la registrazione di hello. Se il dispositivo è stato già registrato, la procedura guidata hello verrà chiuso. Hello configurata impostazioni verranno salvate.

Verrà abilitato anche il proxy Web. È possibile ignorare hello [abilitare il proxy web](#enable-web-proxy) passaggio e passare direttamente troppo[visualizzare impostazioni del proxy web nel portale di Azure classico hello](#view-web-proxy-settings-in-the-azure-classic-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>Configurare il proxy Web tramite i cmdlet di Windows PowerShell per StorSimple
Impostazioni del proxy web tooconfigure un modo alternativo è tramite hello Windows PowerShell per i cmdlet di StorSimple. Eseguire hello proxy web di tooconfigure i passaggi seguenti.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>proxy web tooconfigure tramite i cmdlet
1. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**. Quando richiesto, specificare hello **password amministratore del dispositivo**. password predefinita Hello è `Password1`.
2. Al prompt dei comandi di hello, digitare:
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Specificare e confermare la password di hello quando richiesto, come illustrato di seguito.
   
    ![Configurare il proxy Web nel dispositivo StorSimple 3](./media/storsimple-configure-web-proxy/IC751831.png)

proxy web Hello è ora configurato e deve toobe abilitato.

## <a name="enable-web-proxy"></a>Abilitare il proxy Web
Il proxy Web è disabilitato per impostazione predefinita. Dopo aver configurato le impostazioni di proxy web hello nel dispositivo StorSimple, è necessario toouse hello Windows PowerShell per StorSimple tooenable impostazioni del proxy web hello.

> [!NOTE]
> **Questo passaggio non è necessario se è stato utilizzato il proxy web tooconfigure di hello l'installazione guidata. Il proxy Web viene abilitato automaticamente per impostazione predefinita dopo una sessione dell'installazione guidata.**
> 
> 

Eseguire hello seguire i passaggi descritti in Windows PowerShell per il proxy web tooenable StorSimple nel dispositivo:

#### <a name="tooenable-web-proxy"></a>proxy web tooenable
1. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**. Quando richiesto, specificare hello **password amministratore del dispositivo**. password predefinita Hello è `Password1`.
2. Al prompt dei comandi di hello, digitare:
   
    `Enable-HcsWebProxy`
   
    Nel dispositivo StorSimple sono ora abilitati configurazione del proxy web hello.
   
    ![Configurare il proxy Web nel dispositivo StorSimple 4](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-classic-portal"></a>Visualizzare le impostazioni di proxy web nel portale di Azure classico hello
impostazioni del proxy web Hello configurate tramite l'interfaccia di Windows PowerShell hello e non possono essere modificate da nel portale classico hello. È tuttavia possibile, visualizzare le impostazioni configurate nel portale classico hello. Eseguire hello proxy web di tooview i passaggi seguenti.

#### <a name="tooview-web-proxy-settings"></a>impostazioni del proxy web tooview
1. Passare troppo**servizio StorSimple Manager > dispositivi**. Selezionare e fare clic su un dispositivo e quindi andare troppo**configura**.
2. Scorrere verso il basso in hello **configura** pagina troppo**le impostazioni del proxy Web** sezione. È possibile visualizzare impostazioni del proxy web hello configurato nel dispositivo StorSimple, come illustrato di seguito.
   
    ![Visualizzare il proxy Web nel portale di gestione](./media/storsimple-configure-web-proxy/ViewWebProxyPortal_M.png)

## <a name="errors-during-web-proxy-configuration"></a>Errori durante la configurazione del proxy Web
Se le impostazioni di proxy web hello sono state configurate in modo non corretto, i messaggi di errore sarà visualizzato toohello utente in Windows PowerShell per StorSimple. Hello nella tabella seguente illustra alcuni di questi messaggi di errore, le possibili cause e le azioni consigliate.

| N. di serie | Codice di errore HRESULT | Possibile causa principale | Azione consigliata |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Comando viene eseguito dal controller passivo hello e non è in grado di toocommunicate con controller attivo hello. |Eseguire il comando di hello sul controller attivo hello. comando di hello toorun dal controller passivo hello, sarà necessario connettività hello toofix dal controller passivo tooactive. Se la connettività è interrotta, sarà necessario tooengage supporto Microsoft. |
| 2. |0x800710dd - identificatore operazione hello non è valido |Le impostazioni proxy non sono supportate dal dispositivo virtuale StorSimple. |Le impostazioni proxy non sono supportate dal dispositivo virtuale StorSimple. Possono essere configurate solo in un dispositivo fisico StorSimple. |
| 3. |0x80070057 - Parametro non valido |Uno dei parametri di hello specificati per le impostazioni del proxy hello non è valido. |Hello URI non è specificato nel formato corretto. Utilizzare hello seguente formato:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706ba - Server RPC non disponibile |causa radice di Hello è uno dei seguenti hello:</br></br>Il cluster non è attivo.</br></br>Il servizio Datapath non è in esecuzione.</br></br>comando Hello viene eseguito dal controller passivo e non è in grado di toocommunicate con controller attivo hello. |Per effettuare tooensure di supporto Microsoft che hello cluster sia attivo il servizio relativo al percorso dati sia in esecuzione.</br></br>Eseguire il comando di hello dal controller attivo hello. Se si desidera toorun hello comando dal controller passivo hello, sarà necessario tooensure controller passivo hello può comunicare con controller attivo hello. Se la connettività è interrotta, sarà necessario tooengage supporto Microsoft. |
| 5. |0X800706be - Chiamata RPC non riuscita |Cluster non attivo. |Contattare il supporto Microsoft tooensure che hello cluster sia attivo. |
| 6. |0x8007138f - Risorsa cluster non trovata |La risorsa cluster del servizio di piattaforma non è stata trovata. Questa situazione può verificarsi quando l'installazione di hello non corretto. |Potrebbe essere necessario tooperform impostazioni di fabbrica del dispositivo. Potrebbe essere necessario toocreate una risorsa di piattaforma. Contattare il supporto tecnico Microsoft per i passaggi successivi. |
| 7. |0x8007138c - Risorsa cluster non online |Le risorse cluster del servizio di percorso dati o piattaforma non sono online. |Contattare il supporto Microsoft toohelp verificare che risorsa del servizio relativo al percorso dati e la piattaforma hello siano online. |

> [!NOTE]
> * Hello sopra l'elenco dei messaggi di errore non è completo. 
> * Gli errori correlati tooweb le impostazioni del proxy non verrà visualizzate nel portale di Azure classico nel servizio StorSimple Manager hello. Se si verifica un problema con il proxy web dopo aver completata la configurazione hello, lo stato del dispositivo hello cambierà troppo**Offline** nel portale classico hello. |
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Se si verificano problemi durante la distribuzione di un dispositivo o la configurazione delle impostazioni del proxy web, fare riferimento troppo[risoluzione dei problemi della distribuzione del dispositivo StorSimple](storsimple-troubleshoot-deployment.md).
* toolearn come toouse hello servizio StorSimple Manager, andare troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

