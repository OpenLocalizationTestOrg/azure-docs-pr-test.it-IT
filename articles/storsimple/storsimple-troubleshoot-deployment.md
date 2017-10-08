---
title: problemi relativi alla distribuzione di StorSimple aaaTroubleshoot | Documenti Microsoft
description: Viene descritto come toodiagnose e correggere gli errori che si verificano quando viene distribuito per primo StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f8352eaa-193c-42d1-8818-0b8e02d8485d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 9a31a3cfb3be577500b226c2bc8172dd8664bad9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>Risoluzione dei problemi di distribuzione del dispositivo StorSimple
## <a name="overview"></a>Panoramica
In questo articolo viene fornita una guida alla risoluzione dei problemi riguardo la distribuzione di Microsoft Azure StorSimple. Vengono descritti i problemi comuni, possibili cause e toohelp di procedure consigliate che risolvere i problemi che potrebbero verificarsi durante la configurazione di StorSimple. Queste informazioni si applicano dispositivo fisico locale tooboth hello StorSimple e dispositivo virtuale StorSimple hello.

> [!NOTE]
> Quando si distribuisce dispositivo hello hello per la prima volta, o può verificarsi in un secondo momento, quando il dispositivo hello è operativo, possono verificarsi i problemi relativi alla configurazione dispositivo che si possono incontrare. Questo articolo è incentrato sulla risoluzione dei problemi durante la prima distribuzione. un dispositivo operativo, tootroubleshoot andare troppo[risolvere i problemi di dispositivo operativo](storsimple-troubleshoot-operational-device.md).
> 
> 

Inoltre, in questo articolo vengono descritti gli strumenti di hello per le distribuzioni di StorSimple di risoluzione dei problemi e fornisce un esempio dettagliato di risoluzione dei problemi.

## <a name="first-time-deployment-issues"></a>Problemi relativi alla prima distribuzione
Se verifica un problema durante la distribuzione del dispositivo per hello prima volta, considerare l'esempio hello:

* Se la risoluzione di un dispositivo fisico, assicurarsi che l'hardware hello è stato installato e configurato come descritto in [installare il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) o [installare il dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md).
* Controllare i prerequisiti per la distribuzione. Assicurarsi di disporre di tutte le informazioni descritte in hello hello [elenco di controllo configurazione distribuzione](storsimple-deployment-walkthrough.md#deployment-configuration-checklist).
* Esaminare hello note sulla versione di StorSimple toosee se il problema hello è descritto. note sulla versione di Hello includono soluzioni alternative per problemi di installazione noti. 

Durante la distribuzione del dispositivo, hello più comune problemi che possono verificarsi faccia quando eseguiranno l'installazione guidata di hello e quando si registra dispositivo hello tramite Windows PowerShell per StorSimple. (Si usa Windows PowerShell per StorSimple tooregister e configurare il dispositivo StorSimple. Per ulteriori informazioni sulla registrazione del dispositivo, vedere [passaggio 3: configurare e registrare il dispositivo tramite Windows PowerShell per StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)).

Hello le sezioni seguenti consentono di risolvere i problemi che si verificano quando si configura il dispositivo StorSimple hello hello per la prima volta.

## <a name="first-time-setup-wizard-process"></a>Procedura di configurazione guidata per la prima configurazione
processo di installazione guidata di hello riepiloga le Hello alla procedura seguente. Per informazioni dettagliate sull'installazione, vedere [Distribuire un dispositivo StorSimple locale](storsimple-deployment-walkthrough.md).

1. Eseguire hello [Invoke-HcsSetupWizard](https://technet.microsoft.com/library/dn688135.aspx) toostart hello l'installazione guidata dei cmdlet che guiderà hello rimanenti passaggi. 
2. Configurare la rete hello: hello procedura guidata consente di configurare le impostazioni di rete per l'interfaccia di rete 0 hello dati nel dispositivo StorSimple. Queste impostazioni includono i seguenti hello:
   * Virtual IP (VIP), la subnet mask e gateway: hello [Set-HcsNetInterface](https://technet.microsoft.com/library/dn688161.aspx) cmdlet viene eseguito in background hello. Configura indirizzo IP di hello, subnet mask e gateway per l'interfaccia di rete 0 hello dati nel dispositivo StorSimple.
   * Server DNS primario: hello [Set-HcsDnsClientServerAddress](https://technet.microsoft.com/library/dn688172.aspx) cmdlet viene eseguito in background hello. Configura le impostazioni DNS hello per la soluzione StorSimple.
   * Server NTP – hello [Set-HcsNtpClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet viene eseguito in background hello. Configura impostazioni hello del server NTP per la soluzione StorSimple.
   * Parametro facoltativo proxy web: hello [Set-HcsWebProxy](https://technet.microsoft.com/library/dn688154.aspx) cmdlet viene eseguito in background hello. Imposta e Abilita configurazione hello del proxy web per la soluzione StorSimple.
3. Impostare le password hello: hello è tooset di amministratore del dispositivo e le password gestione Snapshot StorSimple. Se si esegue l'aggiornamento 1, quindi non sarà necessario tooset password gestione Snapshot StorSimple hello.
   
   * password amministratore del dispositivo Hello è toolog usato nel dispositivo tooyour. password del dispositivo predefinito Hello è **Password1**.
   * password di StorSimple Snapshot Manager Hello è obbligatoria quando si configura un toouse dispositivo StorSimple Snapshot Manager. È necessario toofirst set hello password nella connessione guidata hello e quindi è possibile impostare e modificare l'hello servizio StorSimple Manager. Questa password autentica il dispositivo di hello StorSimple Snapshot Manager.
     
     > [!IMPORTANT]
     > Password vengono raccolte prima della registrazione, ma vengono applicate solo dopo la corretta registrazione dispositivo hello. Se si verifica un errore tooapply una password, sarà password hello toosupply richiesta nuovamente finché non hello obbligatorie password (che soddisfano i requisiti di complessità hello) vengono raccolti.
     > 
     > 
4. Registrare il dispositivo hello: hello è dispositivo hello tooregister con il servizio StorSimple Manager hello in esecuzione in Microsoft Azure. registrazione Hello richiede troppo[ottenere chiave di registrazione del servizio hello](storsimple-manage-service.md#get-the-service-registration-key) dal portale di Azure classico hello e fornirla nell'installazione guidata di hello. Dopo la corretta registrazione del dispositivo hello, una chiave DEK del servizio viene fornita tooyou. Assicurarsi che tookeep la crittografia della chiave in un luogo sicuro perché sarà necessaria tooregister tutti i dispositivi successivi con il servizio di hello.

## <a name="common-errors-during-device-deployment"></a>Errori comuni durante la distribuzione del dispositivo
Hello seguenti tabelle elenco hello errori comuni che possono verificarsi quando si:

* Configurare le impostazioni di rete hello necessario.
* Configurare impostazioni del proxy web facoltativo hello.
* Consente di impostare l'amministratore del dispositivo hello e le password gestione Snapshot StorSimple. 
* Registrazione del dispositivo hello. 

## <a name="errors-during-hello-required-network-settings"></a>Errori durante le impostazioni di rete hello richiesto
| No. | Messaggio di errore | Possibili cause | Azione consigliata |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: Questo comando può essere eseguito solo sul controller attivo hello. |L'esecuzione di configurazione su controller passivo hello. |Eseguire questo comando dal controller attivo hello. Per altre informazioni, vedere [Identificare un controller attivo sul dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device). |
| 2 |Invoke-HcsSetupWizard: dispositivo non pronto. |Esistono problemi di connettività di rete hello in DATA 0. |Verificare la connettività di rete fisica hello in DATA 0. |
| 3 |Invoke-HcsSetupWizard: È presente un conflitto di indirizzi IP con un altro sistema sulla rete hello (eccezione da HRESULT: 0x80070263). |indirizzo IP di Hello specificato per DATA 0 era già in uso da un altro sistema. |Fornire un nuovo IP non in uso. |
| 4 |Invoke-HcsSetupWizard: errore di risorsa cluster (eccezione da HRESULT: 0x800713AE). |Duplica VIP. IP Hello fornito è già in uso. |Fornire un nuovo IP non in uso. |
| 5 |Invoke-HcsSetupWizard: indirizzo IPv4 non valido. |indirizzo IP Hello viene fornito in un formato non corretto. |Controllare il formato di hello e specificare nuovamente l'indirizzo IP. Per altre informazioni, vedere [Ipv4 Addressing][1] (Indirizzamento Ipv4). |
| 6 |Invoke-HcsSetupWizard: indirizzo IPv6 non valido. |indirizzo IP Hello viene fornito in un formato non corretto. |Controllare il formato di hello e specificare nuovamente l'indirizzo IP. Per altre informazioni, vedere [Ipv6 Addressing][2] (Indirizzamento Ipv6). |
| 7 |Invoke-HcsSetupWizard: non esistono Nessun endpoint disponibile nel mapping di endpoint hello. (Eccezione da HRESULT: 0x800706D9) |la funzionalità cluster Hello non funziona. |[Contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md) per i passaggi successivi. |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Errori di impostazioni del proxy web facoltativo hello
| No. | Messaggio di errore | Possibili cause | Azione consigliata |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: parametro non valido (eccezione da HRESULT: 0x80070057) |Uno dei parametri di hello specificati per le impostazioni del proxy hello non è valido. |Hello URI non è specificato nel formato corretto hello. Hello utilizzare seguente formato: http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invoke-HcsSetupWizard: server RPC non disponibile (eccezione da HRESULT: 0x800706ba) |causa radice di Hello è uno dei seguenti hello:<ol><li>cluster Hello non è attivo.</li><li>controller passivo Hello non possono comunicare con il controller attivo hello e hello comando viene eseguito dal controller passivo.</li></ol> |A seconda della causa radice di hello:<ol><li>[Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) toomake che tale cluster hello è attivo.</li><li>Eseguire il comando di hello dal controller attivo hello. Se si desidera toorun hello comando dal controller passivo hello, sarà necessario tooensure tale controller passivo hello può comunicare con controller attivo hello. È necessario troppo[contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) se la connettività è interrotta.</li></ol> |
| 3 |Invoke-HcsSetupWizard: chiamata RPC non riuscita (eccezione da HRESULT: 0x800706be) |Cluster non attivo. |[Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) toomake che tale cluster hello è attivo. |
| 4 |Invoke-HcsSetupWizard: risorsa cluster non trovata (eccezione da HRESULT: 0x8007138f) |risorsa cluster Hello non è stato trovato. Questa situazione può verificarsi quando l'installazione di hello non è corretta. |Potrebbe essere necessario tooreset hello dispositivo toohello le impostazioni predefinite. [Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) toocreate una risorsa cluster. |
| 5 |Invoke-HcsSetupWizard: risorsa cluster non online (eccezione da HRESULT: 0x8007138c) |Le risorse del cluster non sono in linea. |[Contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md) per i passaggi successivi. |

## <a name="errors-related-toodevice-administrator-and-storsimple-snapshot-manager-passwords"></a>Errori correlati toodevice amministratore e le password gestione Snapshot StorSimple
password amministratore del dispositivo predefinito Hello è **Password1**. Questa password scade dopo il primo accesso hello; Pertanto, sarà necessario toouse hello l'installazione guidata toochange è. Quando si registra il dispositivo di hello per hello prima volta, è necessario fornire una nuova password amministratore del dispositivo. 

Se si usa il software di gestione Snapshot StorSimple hello in esecuzione sul dispositivo hello toomanage di hello Windows Server host, è necessario fornire anche una password di StorSimple Snapshot Manager durante la registrazione del primo. 

Assicurarsi che le password soddisfino hello seguenti requisiti:

* La password di amministratore del dispositivo deve avere una lunghezza compresa tra gli 8 e i 15 caratteri.
* La password di Gestione snapshot StorSimple deve avere una lunghezza compresa tra i 14 o i 15 caratteri.
* Le password devono contenere 3 dei seguenti 4 tipi di carattere hello: caratteri minuscoli, maiuscoli, numerici e speciali. 
* La password non può essere hello uguali a quelli hello ultime 24 password specificate.

Inoltre, tenere presente che le password scadono ogni anno e può essere modificato solo dopo la corretta registrazione dispositivo hello. Se la registrazione di hello non riesce per qualsiasi motivo, non verrà modificata password hello. Per ulteriori informazioni sull'amministratore del dispositivo e le password di StorSimple Snapshot Manager, andare troppo[utilizzare hello toochange servizio StorSimple Manager le password di StorSimple](storsimple-change-passwords.md).

È possibile riscontrare uno o più dei seguenti errori quando si configura l'amministratore del dispositivo hello e le password gestione Snapshot StorSimple hello.

| No. | Messaggio di errore | Azione consigliata |
| --- | --- | --- |
| 1 |password Hello supera la lunghezza massima di hello. |Utilizzare una password che soddisfi questi requisiti:<ul><li>La password di amministratore dispositivo deve avere una lunghezza compresa tra gli 8 e i 15 caratteri.</li><li>La password di StorSimple Snapshot Manager deve avere una lunghezza compresa tra i 14 o i 15 caratteri.</li></ul> |
| 2 |Hello password non soddisfa la lunghezza hello necessario. |Utilizzare una password che soddisfi questi requisiti:<ul><li>La password di amministratore dispositivo deve avere una lunghezza compresa tra gli 8 e i 15 caratteri.</li><li>La password di StorSimple Snapshot Manager deve avere una lunghezza compresa tra i 14 o i 15 caratteri.</lu></ul> |
| 3 |password di Hello deve contenere caratteri minuscoli. |Le password devono contenere 3 dei seguenti 4 tipi di carattere hello: caratteri minuscoli, maiuscoli, numerici e speciali. Assicurarsi che la password soddisfi tali requisiti. |
| 4 |password Hello deve contenere caratteri numerici. |Le password devono contenere 3 dei seguenti 4 tipi di carattere hello: caratteri minuscoli, maiuscoli, numerici e speciali. Assicurarsi che la password soddisfi tali requisiti. |
| 5 |password di Hello deve contenere caratteri speciali. |Le password devono contenere 3 dei seguenti 4 tipi di carattere hello: caratteri minuscoli, maiuscoli, numerici e speciali. Assicurarsi che la password soddisfi tali requisiti. |
| 6 |Hello password devono contenere 3 dei seguenti 4 tipi di carattere hello: maiuscoli, minuscoli, numerici e speciali. |La password non contiene hello necessario tipi di caratteri. Assicurarsi che la password soddisfi tali requisiti. |
| 7 |Il parametro non corrisponde alla conferma. |Assicurarsi che la password soddisfi tutti i requisiti e che sia stata immessa correttamente. |
| 8 |La password non può corrispondere predefinito hello. |password predefinita Hello è *Password1*. È necessario toochange la password dopo l'accesso per hello prima volta. |
| 9 |password Hello immessa non corrisponde a password del dispositivo hello. Immettere nuovamente la password hello. |Hello password e digitarla di nuovo. |

Le password vengono raccolte prima periferica hello è registrato, ma vengono applicate solo dopo la registrazione ha esito positivo. flusso di lavoro ripristino password Hello richiede hello dispositivo toobe registrato. 

> [!IMPORTANT]
> In generale, se un tentativo tooapply una password ha esito negativo, quindi software hello tenta ripetutamente di password hello toocollect fino a quando non è riuscita. In rari casi, non può essere applicata una password hello. In questo caso, è possibile registrare il dispositivo hello e procedere, tuttavia le password hello non verranno modificate. Non si riceverà alcuna indicazione come toowhich password non è stata modificata, ovvero password amministratore del dispositivo hello o la password di StorSimple Snapshot Manager hello. Se si verifica questa situazione, si consiglia di modificare entrambe le password.
> 
> 

È possibile reimpostare le password hello in hello portale di Azure classico tramite hello servizio StorSimple Manager. Per altre informazioni, vedere: 

* [Password amministratore del dispositivo hello modifica](storsimple-change-passwords.md#change-the-device-administrator-password).
* [Modifica password di StorSimple Snapshot Manager hello](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

## <a name="errors-during-device-registration"></a>Errori durante la registrazione del dispositivo
Utilizzare il servizio di gestione StorSimple hello in esecuzione nel dispositivo hello tooregister di Microsoft Azure. Si potrebbero essere visualizzati uno o più dei seguenti problemi durante la registrazione del dispositivo hello.

| No. | Messaggio di errore | Possibili cause | Azione consigliata |
| --- | --- | --- | --- |
| 1 |Errore 350027: Impossibile dispositivo hello tooregister con hello StorSimple Manager. | |Attendere qualche minuto e quindi riprovare hello. Se hello problema persiste, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md). |
| 2 |Errore 350013: Errore durante la registrazione dispositivo hello. Potrebbe trattarsi di scadenza tooincorrect chiave di registrazione del servizio. | |Ripetere la registrazione dispositivo hello con chiave di registrazione del servizio corretto hello. Per ulteriori informazioni, vedere [chiave di registrazione del servizio Get hello.](storsimple-manage-service.md#get-the-service-registration-key) |
| 3 |Errore 350063: TooStorSimple l'autenticazione del servizio di gestione specificato ma registrazione non riuscita. Ripetere l'operazione hello in seguito. |Questo errore indica che l'autenticazione con ACS ha superato ma hello registro chiamata effettuata toohello servizio non è riuscita. Potrebbe trattarsi di un risultato di un problema di rete sporadico. |Se hello problema persiste, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md). |
| 4 |Errore 350049: non raggiungere il servizio di hello durante la registrazione. |Quando il servizio toohello effettua una chiamata di hello, viene ricevuta un'eccezione web. In alcuni casi, ciò potrebbe risolvere il problema ritentando l'operazione di hello in un secondo momento. |Verificare l'indirizzo IP e il nome DNS, quindi ripetere l'operazione hello. Se hello problema persiste, [contattare il supporto Microsoft.](storsimple-contact-microsoft-support.md) |
| 5 |Errore 350031: dispositivo hello già registrato. | |Nessuna azione necessaria. |
| 6 |Errore 350016: registrazione del dispositivo non riuscita. | |Verificare che la chiave di registrazione hello sia corretta. |
| 7 |Invoke-HcsSetupWizard: Errore durante la registrazione del dispositivo. potrebbe trattarsi di scadenza tooincorrect l'indirizzo IP o nome DNS. Verificare le impostazioni di rete e riprovare. Se hello problema persiste, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md). [ERROR] 350050 |Verificare che il dispositivo può eseguire il ping hello all'esterno di rete. Se non si dispone di rete toooutside connettività, registrazione hello potrebbe non riuscire con l'errore. Questo errore può essere una combinazione di uno o più dei seguenti hello:<ul><li>IP non corretto</li><li>Subnet non corretta</li><li>Gateway non corretto</li><li>Impostazioni DNS non corrette</li></ul> |Vedere i passaggi in hello hello [esempio dettagliato di risoluzione dei problemi](#step-by-step-storsimple-troubleshooting-example). |
| 8 |Invoke-HcsSetupWizard: hello corrente non riuscita a causa di errore interno del servizio tooan [0x1FBE2]. Ripetere l'operazione di hello dopo qualche minuto. Se hello problema persiste, contattare il supporto Microsoft. |Si tratta di un errore generico generato per tutti gli errori invisibili all'utente dal servizio o agente. potrebbe essere la causa più comune di Hello che di autenticazione hello ACS non riuscita. Una causa possibile dell'errore hello è che esistono problemi di configurazione del server NTP hello e ora nel dispositivo hello non impostata correttamente. |Correggere il tempo di hello (se sono presenti problemi) e quindi ripetere l'operazione di registrazione hello. Se si utilizza hello Set-HcsSystem - fuso orario comando tooadjust hello fuso orario, tutte iniziali maiuscole hello fuso orario (ad esempio "ora solare Pacifico").  Se il problema persiste, [contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md) per i passaggi successivi. |
| 9 |Avviso: Impossibile attivare il dispositivo hello. Le password di amministratore dispositivo e Gestione snapshot StorSimple non sono state modificate. |Se ha esito negativo registrazione hello, amministratore del dispositivo hello e le password gestione Snapshot StorSimple non vengono modificate. | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>Strumenti per la risoluzione dei problemi di distribuzioni di StorSimple
StorSimple include numerosi strumenti che è possibile utilizzare tootroubleshoot la soluzione StorSimple. incluse le seguenti:

* Pacchetti di supporto e registri del dispositivo 
* Cmdlet progettati appositamente per la risoluzione dei problemi 

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>Pacchetti di supporto e registri del dispositivo disponibili per la risoluzione dei problemi
Un pacchetto di supporto contiene tutti i log rilevanti hello che consentono ai team di supporto Microsoft hello alla risoluzione dei problemi dei dispositivi. È possibile utilizzare Windows PowerShell per StorSimple toogenerate un pacchetto di supporto crittografato che è quindi possibile condividere con il personale di supporto.

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>tooview hello log o il contenuto di hello del pacchetto di supporto hello
1. Utilizzare Windows PowerShell per StorSimple toogenerate un pacchetto di supporto come descritto in [creare e gestire un pacchetto di supporto](storsimple-create-manage-support-package.md).
2. Scaricare hello [script decrittografia](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) in locale nel computer client.
3. Utilizzare questo [procedura](storsimple-create-manage-support-package.md#edit-a-support-package) tooopen e decrittografia hello pacchetto per il supporto.
4. Hello decrittografata il pacchetto di supporto log sono in formato etw/etvx. È possibile eseguire questi file hello tooview i passaggi seguenti nel Visualizzatore eventi di Windows:
   
   1. Eseguire hello **eventvwr** comando nel client Windows. Verrà avviato il Visualizzatore eventi hello.
   2. In hello **azioni** riquadro, fare clic su **Apri registro salvato** e toohello punto i file di log in formato etvx/etw (pacchetto per il supporto hello). È ora possibile visualizzare file hello. Dopo aver aperto il file hello, è possibile fare doppio clic su e salvare il file hello come testo.
      
      > [!IMPORTANT]
      > È inoltre possibile utilizzare hello **Get-WinEvent** tooopen cmdlet questi file in Windows PowerShell. Per ulteriori informazioni, vedere [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx) in hello documentazione di riferimento di cmdlet di Windows PowerShell.
      > 
      > 
5. Quando hello log si aprono nel Visualizzatore eventi, cercare hello seguendo i registri che contengono i problemi relativi a toohello configurazione del dispositivo:
   
   * hcs_pfconfig/Operational Log
   * hcs_pfconfig/Config
6. Nei file di log hello, ricerca di stringhe cmdlet toohello correlati chiamati dall'installazione guidata di hello. Vedere [Configurazione guidata prima installazione](#first-time-setup-wizard-process) per un elenco di tali cmdlet. 
7. Se non si è in grado di toofigure causa hello del problema hello, è possibile [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) per i passaggi successivi. Hello di utilizzare i passaggi [creare una richiesta di supporto](storsimple-contact-microsoft-support.md#create-a-support-request) quando si contatta il supporto Microsoft per assistenza.

## <a name="cmdlets-available-for-troubleshooting"></a>Cmdlet disponibili per la risoluzione dei problemi
Utilizzare hello dopo errori di connettività toodetect i cmdlet di Windows PowerShell.

* `Get-NetAdapter`: Viene usato l'integrità di hello cmdlet toodetect delle interfacce di rete. 
* `Test-Connection`: Utilizzare questo cmdlet toocheck hello la connettività di rete all'interno e all'esterno delle rete hello.
* `Test-HcsmConnection`: Usare la connettività di hello toocheck questo cmdlet di un dispositivo registrato correttamente.

Se si esegue l'aggiornamento 1 nel dispositivo StorSimple, sono disponibile anche hello seguendo i cmdlet di diagnostica.

* `Sync-HcsTime`: Utilizzare questo cmdlet toodisplay dispositivo temporale e forzare la sincronizzazione dell'ora con il server NTP hello.
* `Enable-HcsPing`e `Disable-HcsPing`: usare questi cmdlet tooallow hello host tooping hello le interfacce di rete nel dispositivo StorSimple. Per impostazione predefinita, le interfacce di rete di hello StorSimple non rispondono tooping richieste.
* `Trace-HcsRoute`: Usare questo cmdlet come uno strumento di analisi della route. Invia i router tooeach pacchetti con destinazione finale di hello modo tooa in un periodo di tempo e calcola quindi i risultati in base ai pacchetti hello restituiti da ogni hop. Poiché `Trace-HcsRoute` Mostra livello hello di perdita di pacchetti in un dato router o un collegamento, è possibile associare con precisione quali router o collegamenti potrebbero causare problemi di rete. 
* `Get-HcsRoutingTable`: Utilizzare questo cmdlet toodisplay hello tabella routing IP locale.

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>Risoluzione dei problemi con i cmdlet Get-NetAdapter hello
Quando si configurano le interfacce di rete per una distribuzione del primo dispositivo, lo stato dell'hardware hello non è disponibile nell'interfaccia utente del servizio StorSimple Manager hello dispositivo hello non è ancora registrato con il servizio di hello. Inoltre, pagina stato dell'Hardware hello può non sempre riflette correttamente lo stato di hello del dispositivo hello, soprattutto se vi sono problemi che influiscono sulla sincronizzazione del servizio. In questi casi, è possibile utilizzare hello `Get-NetAdapter` toodetermine cmdlet hello integrità e lo stato delle interfacce di rete.

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>toosee un elenco di tutte le schede di rete hello sul dispositivo
1. Avviare Windows PowerShell per StorSimple e quindi digitare `Get-NetAdapter`. 
2. Utilizzare l'output di hello di hello `Get-NetAdapter` cmdlet e seguendo le linee guida toounderstand hello hello lo stato dell'interfaccia di rete.
   
   * Se l'interfaccia hello è integra e abilitato, hello **ifIndex** lo stato viene visualizzato come **backup**.
   * Se l'interfaccia di hello è integra ma non è fisicamente collegata (tramite un cavo di rete), hello **ifIndex** viene visualizzato come **disabilitato**.
   * Se l'interfaccia hello è integra ma non abilitata, hello **ifIndex** lo stato viene visualizzato come **NotPresent**.
   * Se l'interfaccia hello non esiste, non è visualizzato nell'elenco. interfaccia utente del servizio StorSimple Manager Hello risulterà comunque questa interfaccia in uno stato di errore.

Per ulteriori informazioni su come toouse questo cmdlet, andare troppo[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) in hello riferimento ai cmdlet di Windows PowerShell. 

Nelle sezioni seguenti Hello mostrano esempi di output hello `Get-NetAdapter` cmdlet. 

 In questi esempi, controller 0 era il controller passivo hello ed è stata configurata come segue:

* DATA 0, DATA 1, DATA 2 e DATA 3 rete interfacce erano presenti nel dispositivo hello.
* DATA 4 e schede di interfaccia di rete DATA 5 non erano presenti; Pertanto, non sono elencate nell'output di hello.
* DATI 0 era abilitata.

Controller 1 hello controller è attivo ed è stata configurata come segue:

* DATA 0, DATA 1, DATA 2, 3 di dati, DATA 4 e DATA 5 rete interfacce erano presenti nel dispositivo hello.
* DATI 0 era abilitata.

**Esempio di output – controller 0**

di seguito Hello è output di hello dal controller 0 (controller passivo hello). DATI 1, DATI 2 e DATI 3 non sono connessi. DATA 4 e DATA 5 non sono elencate perché non sono presenti nel dispositivo hello. 

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**Esempio di output – controller 1**

di seguito Hello è output di hello dal controller 1 (controller attivo hello). Solo DATA 0 è configurata l'interfaccia di rete sul dispositivo hello hello e funzionante.

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>Risoluzione dei problemi con i cmdlet Test-Connection hello
È possibile utilizzare hello `Test-Connection` toodetermine cmdlet se il dispositivo StorSimple può connettersi toohello all'esterno di rete. Se tutti i parametri di rete hello, tra cui hello DNS, sono configurati correttamente nell'installazione guidata di hello, è possibile utilizzare hello `Test-Connection` cmdlet tooping un indirizzo noto esterno rete hello, ad esempio outlook.com. 

Se il ping è disabilitato, è necessario abilitare i problemi di connettività tootroubleshoot ping con questo cmdlet.

Vedere i seguenti esempi di output di hello hello `Test-Connection` cmdlet. 

> [!NOTE]
> Nel primo esempio di hello, dispositivo hello è configurato con un DNS non corretto. Nel secondo esempio hello, hello DNS è corretto.
> 
> 

**Esempio di output – DNS non corretto**

Nel seguente esempio di hello, non sussiste alcun output per gli indirizzi IPV4 e IPV6 hello, che indica che hello che DNS non viene risolto. Ciò significa che non vi è alcun toohello connettività all'esterno di rete e un DNS corretto deve toobe fornito. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**Esempio di output – DNS corretto**

Nel seguente esempio di hello, hello DNS restituisce hello indirizzo IPV4, che indica che hello che DNS sia configurato correttamente. Questo conferma che vi sia connettività toohello all'esterno di rete. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>Risoluzione dei problemi con i cmdlet Test-HcsmConnection hello
Hello utilizzare `Test-HcsmConnection` cmdlet per un dispositivo che è già connesso tooand registrato con il servizio StorSimple Manager. Questo cmdlet consente di verificare la connettività di hello tra un dispositivo registrato e hello corrispondente servizio StorSimple Manager. È possibile eseguire questo comando su Windows PowerShell per StorSimple. 

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>cmdlet Test-HcsmConnection hello toorun
1. Verificare che il dispositivo hello è registrato.
2. Controllare lo stato del dispositivo hello. Se il dispositivo hello è disattivato, in modalità di manutenzione o offline, è possibile visualizzare hello gli errori seguenti: 
   
   * Cisdevicedecommissioned. indica che il dispositivo hello è disattivato.
   * Devicenotready. indica che il dispositivo hello è in modalità manutenzione.
   * Devicenotready. indica che il dispositivo hello non è online.
3. Verificare che il servizio StorSimple Manager hello sia in esecuzione (utilizzare hello [Get-ClusterResource](https://technet.microsoft.com/library/ee461004.aspx) cmdlet). Se il servizio di hello non è in esecuzione, si potrebbe riscontrare hello gli errori seguenti:
   
   * ErrorCode.CiSApplianceAgentNotOnline
   * ErrorCode.CisPowershellScriptHcsError – Indica che si è verificata un'eccezione durante l'esecuzione di Get-ClusterResource.
4. Controllare il token di servizio Access Control (ACS) hello. Se viene generata un'eccezione web, potrebbe essere il risultato di hello di un problema del gateway, un'autenticazione proxy mancante, un DNS non corretto o un errore di autenticazione. Verrà visualizzato hello gli errori seguenti:
   
   * Cisappliancegateway. indica un'eccezione HttpStatusCode BadGateway: servizio di sistema di risoluzione dei nomi hello Impossibile risolvere il nome host hello. 
   * Cisapplianceproxy. indica un'eccezione HttpStatusCode ProxyAuthenticationRequired (codice di stato HTTP 407): hello client potrebbe non per l'autenticazione server proxy hello. 
   * Cisappliancednserror. indica un'eccezione WebExceptionStatus: servizio di sistema di risoluzione dei nomi hello Impossibile risolvere il nome host hello.
   * Cisapplianceacserror – indica che il servizio hello ha restituito un errore di autenticazione, ma vi sia connettività.
     
     Se non genera un'eccezione Web, cercare ErrorCode.CiSApplianceFailure. Ciò indica applicazione hello non riuscita.
5. Controllare la connettività di servizi cloud hello. Se il servizio di hello genera un'eccezione web, si potrebbe riscontrare hello gli errori seguenti:
   
   * Cisappliancegateway. indica un'eccezione HttpStatusCode BadGateway: un server proxy intermedio ha ricevuto una richiesta non valida da un altro proxy o da server originale hello.
   * Cisapplianceproxy. indica un'eccezione HttpStatusCode ProxyAuthenticationRequired (codice di stato HTTP 407): hello client potrebbe non per l'autenticazione server proxy hello. 
   * Cisappliancednserror. indica un'eccezione WebExceptionStatus: servizio di sistema di risoluzione dei nomi hello Impossibile risolvere il nome host hello.
   * Cisapplianceacserror – indica che il servizio hello ha restituito un errore di autenticazione, ma vi sia connettività.
     
     Se non genera un'eccezione Web, cercare ErrorCode.CiSApplianceSaasServiceError. Questo indica un problema con hello servizio StorSimple Manager.
6. Verificare la connettività del bus di servizio di Azure. Cisapplianceservicebuserror indica che il dispositivo hello non può connettersi toohello Bus di servizio.

il file di log Ciscommandletlog0curr Hello e Cisagentsvc0curr saranno disponibili altre informazioni, ad esempio i dettagli dell'eccezione. 

Per ulteriori informazioni su come toouse hello cmdlet, vedere troppo[Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx) in Windows PowerShell hello documentazione di riferimento.

> [!IMPORTANT]
> È possibile eseguire questo cmdlet per hello attivo e il controller passivo hello. 
> 
> 

Vedere i seguenti esempi di output di hello hello `Test-HcsmConnection` cmdlet. 

**Esempio di output – Registrazione corretta di un dispositivo che esegue la versione di rilascio di StorSimple (luglio 2014)**

il primo esempio di Hello è da un dispositivo è registrato correttamente con hello servizio StorSimple Manager e non è presenti problemi di connettività. 

     Controller1>Test-HcsmConnection -verbose
     Checking device state  ... Success.
     Device registered successfully
     Checking device authentication.  ... This operation will take few minutes toocomplete....
     Checking device authentication.  ... Success.
     Checking connectivity from device tooStorSimple Manager service.  ... This operation will take few minutes toocomplete....
     Checking connectivity from device tooStorSimple Manager service.  ... Success.
     Checking connectivity from StorSimple Manager service tooStorSimple device. .... Success.
     Controller1>

**Esempio di output – Registrazione corretta di un dispositivo che esegue l'aggiornamento 1 di StorSimple**

Se si esegue Update 1 nel dispositivo StorSimple, non occorre toorun con l'opzione di visualizzazione dettagliata hello.

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**Esempio di output – Dispositivo offline che esegue la versione di rilascio di StorSimple (luglio 2014)**

In questo esempio si trova in un dispositivo con lo stato di **Offline** nel portale di Azure classico hello.

     Checking device state: Success 
     Device is registered successfully 
     Checking connectivity from device tooSaaS.. Failure

dispositivo Hello non è riuscito a connettersi usando hello configurazione del proxy web corrente. Potrebbe trattarsi di un problema di configurazione del proxy web hello o un problema di connettività di rete. In questo caso, assicurarsi che le impostazioni del proxy Web siano corrette e che i server proxy Web siano online e raggiungibili. 

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>Risoluzione dei problemi con i cmdlet di sincronizzazione HcsTime hello
Utilizzare l'ora del dispositivo hello toodisplay cmdlet. Se l'ora del dispositivo hello è associato un offset con il server NTP hello, è quindi possibile utilizzare questo cmdlet tooforce-sincronizzare hello ora con il server NTP. Se l'offset di hello tra hello dispositivo e il server NTP è maggiore di 5 minuti, verrà visualizzato un avviso. Se l'offset hello supera i 15 minuti, quindi dispositivo hello passerà alla modalità offline. È possibile utilizzare comunque questo tooforce cmdlet la sincronizzazione dell'ora. Tuttavia, se hello offset supera i 15 ore, quindi non sarà in grado di tooforce-sincronizzare l'ora hello e verrà visualizzato un messaggio di errore.

**Output di esempio - Sincronizzazione dell'ora forzata con Sync-HcsTime**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>Risoluzione dei problemi con i cmdlet Enable-HcsPing e Disable-HcsPing hello
Utilizzare queste tooensure cmdlet che nel dispositivo interfacce di rete hello rispondano a richieste di ping tooICMP. Per impostazione predefinita le interfacce di rete di hello StorSimple non rispondono tooping richieste. Questo cmdlet è tooknow modo più semplice hello se il dispositivo sia online e raggiungibile.  

**Output di esempio: Enable-HcsPing e Disable-HcsPing**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>Risoluzione dei problemi con i cmdlet di traccia HcsRoute hello
Usare questo cmdlet come uno strumento di analisi della route. Invia i router tooeach pacchetti con destinazione finale di hello modo tooa in un periodo di tempo e calcola quindi i risultati in base ai pacchetti hello restituiti da ogni hop. Poiché i cmdlet hello Mostra livello hello di perdita di pacchetti in un determinato router o un collegamento, è possibile associare con precisione quali router o collegamenti potrebbero causare problemi di rete.

**Output di esempio che illustra come tootrace hello route di un pacchetto con traccia HcsRoute**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>Risoluzione dei problemi con i cmdlet Get-HcsRoutingTable hello
Utilizzare questa tabella di routing hello tooview cmdlet per il dispositivo StorSimple. Una tabella di routing è un set di regole che consentono di determinare dove verranno indirizzati i pacchetti di dati che passano attraverso una rete IP (Internet Protocol). 

tabella di routing Hello Mostra interfacce di hello e gateway che le route hello toohello dati hello specificato reti. Offre inoltre hello routing metrica decisore hello per hello percorso seguito tooreach una determinata destinazione. Hello inferiore hello routing metrica, hello hello preferenza superiore. 

Ad esempio, se si dispone di 2 interfacce di rete, DATA 2 e DATA 3, connesso toohello Internet. Se le metriche di routing hello per DATA 2 e DATA 3 sono 15 e 261, DATA 2 con la metrica di routing inferiore di hello è utilizzata l'interfaccia preferito di hello hello tooreach Internet.

Se si esegue l'aggiornamento 1 nel dispositivo StorSimple, l'interfaccia di rete 0 dati è preferenza più elevato di hello per il traffico cloud hello. Ciò implica che anche se sono presenti altre interfacce basate su cloud, il traffico di hello cloud verrà indirizzato tramite DATA 0. 

Se si esegue hello `Get-HcsRoutingTable` senza specificare i parametri (come hello esempio illustrato di seguito), hello cmdlet output del cmdlet conterrà le tabelle di routing IPv4 e IPv6. In alternativa, è possibile specificare `Get-HcsRoutingTable -IPv4` o `Get-HcsRoutingTable -IPv6` tooget una tabella di routing pertinente.

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>Esempio dettagliato di risoluzione dei problemi
Hello riportato di seguito risoluzione dei problemi dettagliata di una distribuzione di StorSimple. Nello scenario di esempio hello, registrazione dispositivo ha esito negativo con un messaggio di errore che indica che le impostazioni di rete hello o il nome DNS hello è corretto.

messaggio di errore Hello restituito è:

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

Errore Hello potrebbe essere causato da uno qualsiasi dei seguenti hello:

* Installazione hardware non corretta
* Interfacce di rete difettose
* Indirizzo IP errato, subnet mask, gateway, server DNS primario o proxy Web
* Codice di registrazione non corretto
* Impostazioni del firewall non corrette

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>problema di registrazione dispositivo hello toolocate e correzione
1. Controllare la configurazione del dispositivo: sul controller attivo hello eseguire `Invoke-HcsSetupWizard`.
   
   > [!NOTE]
   > nel controller attivo hello deve eseguire l'installazione guidata di Hello. tooverify che si è connessi toohello controller attivo, esaminare il banner di hello visualizzato nella console seriale hello. banner Hello indica se si è connessi toocontroller 0 o controller 1, e se il controller hello è attivo o passivo. Per ulteriori informazioni, visitare troppo[identificare un controller attivo sul dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
   > 
   > 
2. Assicurarsi che il dispositivo hello sia cablato correttamente: controllare hello cablaggio di rete sul dispositivo hello retro. cablaggio Hello è un modello di dispositivo toohello specifico. Per ulteriori informazioni, visitare troppo[installare il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) o [installare del dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
   
   > [!NOTE]
   > Se si utilizza porte di rete 10 GbE, occorrerà hello toouse fornito adattatori QSFP-SFP e i cavi SFP. Per ulteriori informazioni, vedere hello [elenco di cavi, commutatori e ricetrasmettitori consigliati per le porte hello 10 GbE](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
   > 
   > 
3. Verificare l'integrità di hello hello dell'interfaccia di rete:
   
   * Utilizzare integrità hello Get-NetAdapter cmdlet toodetect hello hello delle interfacce di rete per DATA 0. 
   * Se il collegamento hello non funziona, hello **ifindex** stato indicherà tale interfaccia hello è inattivo. Connessione di rete di hello toocheck di hello porta toohello dispositivo e il commutatore toohello sarà quindi necessario. È necessario anche toorule i cavi che presentano problemi. 
   * Se si ritiene che hello DATA 0 porta sul controller attivo hello non è riuscita, è possibile verificarlo connettendosi toohello porta DATA 0 sul controller 1. tooconfirm, disconnettere il cavo di rete hello hello parte posteriore dispositivo hello dal controller 0, la connessione hello cavo toocontroller 1 e quindi eseguire di nuovo il cmdlet Get-NetAdapter hello. 
     Se hello DATA 0 porta in un controller non riesce, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) per i passaggi successivi. Potrebbe essere necessario controller hello tooreplace nel sistema.
4. Verificare commutatore toohello di hello connettività:
   
   * Assicurarsi che le interfacce di rete 0 dati sul controller 0 e controller 1 nell'enclosure principale si trovino in hello stessa subnet. 
   * Controllo hello hub o router. In genere, è consigliabile connettere entrambi i controller toohello stesso hub o router. 
   * Verificare che i commutatori hello usati per la connessione di hello abbiano DATA 0 per entrambi i controller in hello stessa vLAN.
5. Eliminare eventuali errori dell'utente:
   
   * Eseguire nuovamente l'installazione guidata di hello (eseguire **Invoke-HcsSetupWizard**), quindi immettere hello valori nuovamente toomake assicurarsi che non siano presenti errori. 
   * Verificare la registrazione di hello chiave utilizzata. Hello stessa chiave di registrazione può essere tooconnect utilizzati più dispositivi tooa servizio StorSimple Manager. Utilizzare la procedura hello in [chiave di registrazione del servizio Get hello](storsimple-manage-service.md#get-the-service-registration-key) tooensure che si sta utilizzando hello chiave di registrazione corretta.
     
     > [!IMPORTANT]
     > Se si dispone di più servizi in esecuzione, sarà necessario tooensure tale chiave di registrazione hello per servizio appropriato hello è dispositivo hello tooregister utilizzato. Se è stato registrato un dispositivo con il servizio StorSimple Manager non valido di hello, sarà necessario troppo[contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) per i passaggi successivi. È possibile tooperform ripristino delle impostazioni predefinite del dispositivo hello (che potrebbe causare la perdita di dati) toothen connetterlo toohello destinata service.
     > 
     > 
6. Utilizzare tooverify cmdlet Test-Connection hello di disporre di connettività toohello all'esterno di rete. Per ulteriori informazioni, visitare troppo[risoluzione dei problemi con il cmdlet Test-Connection hello](#troubleshoot-with-the-test-connection-cmdlet).
7. Controllare le interferenze del firewall. Se si verifica tale hello virtuale impostazioni IP (VIP), subnet, gateway e DNS siano tutti corrette, viene visualizzato ancora problemi di connettività, quindi è possibile che il firewall blocca le comunicazioni tra il dispositivo e hello all'esterno di rete. È necessario che le porte 80 e 443 siano disponibili nel dispositivo StorSimple per le comunicazioni in uscita tooensure. Per ulteriori informazioni, vedere [Requisiti di rete per il dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
8. Esaminare i registri di hello. Andare troppo[supportare pacchetti e i log del dispositivo disponibile per la risoluzione dei problemi](#support-packages-and-device-logs-available-for-troubleshooting).
9. Se hello passaggi precedenti non risolvono il problema di hello, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) per assistenza.

## <a name="next-steps"></a>Passaggi successivi
[Informazioni su come un dispositivo operativo tootroubleshoot](storsimple-troubleshoot-operational-device.md).

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 
