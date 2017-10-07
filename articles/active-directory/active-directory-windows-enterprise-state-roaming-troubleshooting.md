---
title: Risoluzione dei problemi di Enterprise State Roaming in Azure Active Directory | Documentazione Microsoft
description: Fornisce le risposte toosome domande gli amministratori IT potrebbero essere sulle impostazioni e sincronizzazione dei dati di app.
services: active-directory
keywords: impostazioni di enterprise state roaming, cloud windows, domande frequenti su enterprise state roaming
documentationcenter: 
author: tanning
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4636d016983426e30d696459f54167b8ad2babcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a>Risoluzione dei problemi di Enterprise State Roaming in Azure Active Directory

In questo argomento vengono fornite informazioni su come tootroubleshoot e diagnosticare i problemi con Enterprise State Roaming e fornisce un elenco di problemi noti.

## <a name="preliminary-steps-for-troubleshooting"></a>Operazioni preliminari per la risoluzione dei problemi 
Prima di iniziare la risoluzione dei problemi, verificare che hello utenti e dispositivi sono stati configurati correttamente e che vengono soddisfatti tutti i requisiti di hello di Enterprise State Roaming hello e del dispositivo utente hello. 

1. Windows 10, con gli aggiornamenti più recenti di hello e un minimo di versione 1511 (Build del sistema operativo 10586 o successiva) è installato nel dispositivo hello. 
2. dispositivo di Hello è unita in join, o di dominio e registrato con Azure AD di Azure AD.
3. Nel portale di Azure Active Directory hello **Enterprise State Roaming** è abilitata per la directory di hello sotto **configura** > **dispositivi**  >  **Gli utenti possono sincronizzare le impostazioni e dati delle App aziendali**. Tutti gli utenti selezionati oppure hello utente è abilitato per la sincronizzazione tramite l'opzione selezionata hello e incluso nel gruppo di sicurezza hello.
4. utente Hello dispone di una sottoscrizione di Azure Active Directory Premium toothem assegnata.  
5. è stato riavviato dispositivo Hello e hello utente è connesso dopo l'abilitazione di Enterprise State Roaming.

## <a name="information-tooinclude-when-you-need-help"></a>Tooinclude informazioni quando si richiede assistenza
Se non si riesce a risolvere il problema con le guide di hello indicate di seguito, è possibile contattare il supporto tecnico Microsoft. Quando si contatta il loro, è consigliabile hello tooinclude le seguenti informazioni:

- **Descrizione generale dell'errore hello** : sono presenti messaggi di errore visualizzati dall'utente hello? Se si è verificato alcun messaggio di errore, descrivere hello comportamento imprevisto riscontrato, in modo dettagliato. Quali funzionalità sono abilitate per la sincronizzazione e cosa è utente hello previsto toosync? Sono più funzionalità di sincronizzazione non o è tooone it isolato?
- **Utenti interessati**: la sincronizzazione sta funzionando o non sta funzionando per uno o più utenti? Quanti sono i dispositivi interessati per utente? Nessuno viene sincronizzato o ne vengono sincronizzati alcuni e non altri?
- **Informazioni sull'utente hello** : le identità è hello utente utilizzando toolog toohello dispositivo? Come la registrazione utente hello toohello dispositivo? Sono parte di un gruppo di sicurezza selezionati consentito toosync? 
- **Informazioni sul dispositivo hello** : dispositivo aggiunti ad Azure AD o dominio? Quale compilazione è dispositivo hello? Quali sono gli aggiornamenti più recenti di hello?
- **Data / ora / fuso orario** – animale hello data e l'ora esatte di visualizzazione errore hello (fuso orario hello includono)?
- Queste informazioni consentiranno di risolvere il problema nel più breve tempo possibile.

## <a name="troubleshooting-and-diagnosing-issues"></a>Diagnosi e risoluzione dei problemi
In questa sezione fornisce suggerimenti su come tootroubleshoot e diagnosticare i problemi correlati i tooEnterprise stato Roaming.

## <a name="verify-sync-and-hello-sync-your-settings-settings-page"></a>Verificare la sincronizzazione e hello "Sincronizza le impostazioni" pagina Impostazioni 

1. Dopo l'aggiunta di tooa i PC Windows 10 dominio in cui è configurato tooallow Enterprise State Roaming, l'accesso con l'account aziendale. Andare troppo**impostazioni** > **account** > **Impostazioni sincronizzazione** e confermare che le singole impostazioni hello e di sincronizzazione sono e che la parte superiore di hello di pagina Impostazioni Hello indica che sono la sincronizzazione con l'account aziendale. Conferma hello stesso account viene usato anche come account di accesso in **impostazioni** > **account** > **Info Your**. 
2. Verificare che la sincronizzazione funzioni tra più computer apportandovi alcune modifiche nel computer originale hello, ad esempio lo spostamento di hello barra delle applicazioni toohello lato destro o superiore della schermata di hello. Espressioni di controllo modifica hello propagare toohello secondo computer entro cinque minuti. 
 - Blocco e sblocco schermo hello (Win + L) consente di attivare una sincronizzazione.
 - È necessario utilizzare hello stesso account di accesso su entrambi i computer per la sincronizzazione toowork – Enterprise State Roaming è abbinato toohello account utente e non hello macchina.

**Potenziale problema**: pagina di impostazioni hello è attiva o disattiva hello in grigio e anziché visualizzare un account, viene visualizzato testo hello "alcune funzionalità di Windows sono disponibili solo se si utilizza un account Microsoft o account aziendale". Questo problema può verificarsi per i dispositivi che sono stati impostati toobe appartenenti a un dominio e registrato tooAzure Active Directory, ma dispositivo hello ha non autenticato tooAzure Active Directory. Una possibile causa è necessario applicare i criteri del dispositivo hello, ma l'applicazione viene eseguito in modo asincrono e può essere posticipata da alcune ore. in caso di hello, tooverify verificare questo problema, seguire la procedura seguente hello in hello toocheck lo stato di registrazione dispositivo.

### <a name="verify-hello-device-registration-status"></a>Verificare lo stato della registrazione dispositivo hello
Enterprise State Roaming richiede hello dispositivo toobe registrato con Azure AD. Sebbene non specifiche tooEnterprise stato Roaming, attenendosi alle istruzioni hello seguente consente di verificare che hello del Client Windows 10 è registrato e confermare lo stato NGC identificazione personale, URL, impostazioni di Azure AD e altre informazioni.

1.  Prompt dei comandi aprire hello uno. toodo in Windows, aprire hello esecuzione dell'utilità di avvio (Win + R) e digitare "cmd" tooopen.
2.  Una volta aperto hello il prompt dei comandi, digitare "*dsregcmd.exe /status*".
3.  Per l'output previsto, hello **AzureAdJoined** valore del campo deve essere "YES", **WamDefaultSet** valore del campo deve essere "YES" e hello **WamDefaultGUID** valore del campo deve essere un GUID con "(AzureAd)" alla fine di hello.

**Potenziale problema**: **WamDefaultSet** e **AzureAdJoined** sia stato "NO" nel valore del campo hello, dispositivo hello è stato aggiunto al dominio e sia registrato con Azure AD e dispositivo hello non vengono sincronizzati. Se questo è visualizzato, il dispositivo hello potrebbe necessario toowait per toobe criteri applicati o hello autenticazione per il dispositivo di hello non riuscito durante la connessione AD tooAzure. utente di Hello può avere toowait alcune ore per hello criteri toobe applicato. Altre procedure di risoluzione dei problemi possono includere nuovo tentativo in corso la registrazione automatica di firma e nuovamente o avvio attività hello nell'utilità di pianificazione. In alcuni casi eseguendo "*dsregcmd.exe /leave*" in una finestra del prompt dei comandi con privilegi elevati, riavviando e ripetendo il tentativo di registrazione si può risolvere il problema.


**Potenziale problema**: campo hello per **AzureAdSettingsUrl** sia vuota e hello periferica non sincronizzazione. utente hello è possibile che ultima connesso toohello dispositivo prima di Enterprise State Roaming è stato abilitato in Azure Active hello Portale di directory. Riavviare il dispositivo hello e dispongono di accesso utente hello. Facoltativamente, nel portale di hello, provare con hello amministratore IT, disabilitare e riabilitare le impostazioni di sincronizzazione possono gli utenti e i dati di App aziendali. Una volta riattivato, riavvio hello dispositivo e dispongono di accesso utente hello. Se non viene risolto il problema di hello, **AzureAdSettingsUrl** può essere vuoto in caso di hello di un certificato del dispositivo non valido. In questo caso eseguendo "*dsregcmd.exe /leave*" in una finestra del prompt dei comandi con privilegi elevati, riavviando e ripetendo il tentativo di registrazione si può risolvere il problema.

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a>Enterprise State Roaming e Multi-Factor Authentication 
In determinate condizioni, Enterprise State Roaming può non riuscire toosync dati se Azure multi-Factor Authentication è configurato. Per altre informazioni su questi problemi, vedere il documento di supporto hello [KB3193683](https://support.microsoft.com/kb/3193683). 

**Potenziale problema**: se il dispositivo è configurato toorequire multi-Factor Authentication nel portale di Azure Active Directory hello, si potrebbero non riuscire toosync impostazioni durante la firma nel dispositivo Windows 10 tooa utilizzando una password. Questo tipo di configurazione di multi-Factor Authentication è previsto tooprotect un account amministratore di Azure. Gli utenti amministratori potrebbero essere ancora in grado di toosync effettuando l'accesso a dispositivi Windows 10 tootheir con i Microsoft Passport per il PIN di lavoro o completando multi-Factor Authentication durante l'accesso di altri servizi di Azure come Office 365.

**Potenziale problema**: sincronizzazione può non riuscire se salve Configura criteri di accesso condizionale di Active Directory Federation Services multi-Factor Authentication hello e token di accesso hello sul dispositivo hello scade. Assicurarsi di accedere e disconnettersi utilizzando hello Microsoft Passport per il PIN di lavoro o completare multi-Factor Authentication durante l'accesso di altri servizi di Azure come Office 365.

###<a name="event-viewer"></a>Aprire il Visualizzatore eventi
Avanzati di risoluzione dei problemi, il Visualizzatore eventi può essere utilizzato toofind specifici errori. Questi scenari sono documentati nella tabella hello riportata di seguito. sono disponibili eventi di Hello in Visualizzatore eventi > registri applicazioni e servizi > **Microsoft** > **Windows** > **SettingSync** e per problemi di identità con sincronizzazione **Microsoft** > **Windows** > **Azure AD**.


## <a name="known-issues"></a>Problemi noti

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a>La sincronizzazione non funziona sui dispositivi che hanno app caricate in sideload con software MDM

Interessa i dispositivi che eseguono hello aggiornamento Aniversary di Windows 10 (versione 1607). Nel Visualizzatore eventi in registri SettingSync Azure hello hello 6013 ID evento errore 80070259 è frequentemente.

**Azione consigliata**  
Assicurarsi che i client v1607 hello Windows 10 è hello 23 agosto 2016 aggiornamento cumulativo ([KB3176934](https://support.microsoft.com/kb/3176934) 14393.82 compilare del sistema operativo). 

---

### <a name="internet-explorer-favorites-do-not-sync"></a>I preferiti di Internet Explorer non vengono sincronizzati

Interessa i dispositivi che eseguono hello aggiornamento di novembre di Windows 10 (versione 1511).

**Azione consigliata**  
Assicurarsi che i client v1511 hello Windows 10 è hello luglio 2016 aggiornamento cumulativo ([KB3172985](https://support.microsoft.com/kb/3172985) 10586.494 compilare del sistema operativo).

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a>Il tema non viene sincronizzato e neppure i dati protetti con Windows Information Protection 

perdita di dati tooprevent, dati protetti con [Windows Information Protection](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) non verranno sincronizzate tramite Enterprise State Roaming per i dispositivi usando hello aggiornamento Aniversary di Windows 10.



**Azione consigliata**  
Nessuna. Gli aggiornamenti futuri tooWindows potrebbe risolvere il problema.

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a>Le impostazioni di data, ora e area non vengono sincronizzate in un dispositivo aggiunto a un dominio 
  
I dispositivi che appartengono a un dominio non si verifica la sincronizzazione per l'impostazione di Date, Time e area hello: ora automatica. Utilizzando l'ora automatica potrebbe override hello altre impostazioni di data, ora e di area e causare tali impostazioni non toosync. 

**Azione consigliata**  
Nessuna. 

---

### <a name="uac-prompts-when-syncing-passwords"></a>Richieste di Controllo dell'account utente durante la sincronizzazione delle password

Influisce sul server che eseguono hello Windows 10 aggiornamento di novembre (versione 1511) con una scheda di rete wireless che viene configurato toosync password.

**Azione consigliata**  
Verificare che disponga di client v1511 hello Windows 10 hello aggiornamento cumulativo ([KB3140743](https://support.microsoft.com/kb/3140743) 10586.494 compilare del sistema operativo).

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a>La sincronizzazione non funziona sui dispositivi che usano smart card per l'accesso
Se si tenta di toosign nel dispositivo Windows tooyour utilizzando una smart card o smart card virtuale, la sincronizzazione delle impostazioni smetterà di funzionare.     

**Azione consigliata**  
Nessuna. Gli aggiornamenti futuri tooWindows potrebbe risolvere il problema.

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a>Un dispositivo aggiunto a un dominio non viene sincronizzato dopo che è uscito dalla rete aziendale     
I dispositivi appartenenti a un dominio registrato tooAzure che Active Directory possono generare un errore di sincronizzazione, se il dispositivo di hello è fuori sede per periodi prolungati di tempo e non è possibile completare l'autenticazione di domini.

**Azione consigliata**  
Connettersi alla rete aziendale hello dispositivo tooa in modo che sia possibile riprendere la sincronizzazione.

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-hello-user-has-a-mixed-case-user-principal-name"></a>I dispositivi aggiunti AD Azure non esegue la sincronizzazione e hello utente dispone di un nome dell'entità utente case misto.
 Se in un dispositivo aggiunti ad Azure AD che ha eseguito l'aggiornamento da Windows 10 compilare 10586 too14393 hello utente dispone di un UPN (ad esempio nome utente anziché nome utente) maiuscole e minuscole e utente hello, il dispositivo dell'utente hello potrebbe non riuscire toosync. 

**Azione consigliata**  
utente Hello sarà anche necessario toounjoin e aggiunto nuovamente cloud toohello di hello dispositivo. toodo, questo account di accesso come utente di amministratore locale hello e separarsi dispositivo hello passando troppo**impostazioni** > **sistema** > **su** e selezionare " Gestire o disconnettersi dal lavoro o dell'istituto di istruzione". Pulizia dei file hello seguenti e quindi aggiunta ad Azure AD hello dispositivo nuovamente in **impostazioni** > **sistema** > **su** e selezionando "connessione tooWork o dell'istituto di istruzione". Continuare toojoin hello dispositivo tooAzure Active Directory e il flusso completo hello.

In fase di pulizia hello, hello pulizia i seguenti file:
- Settings.dat in `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\`
- Tutti i file nella cartella hello hello`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a>ID evento 6065: 80070533 L'utente non può eseguire l'accesso perché questo account è attualmente disabilitato  
Nel Visualizzatore eventi in registri SettingSync/Debug hello, questo errore può essere visualizzato quando le credenziali dell'utente hello scaduti. Inoltre, può verificarsi quando il tenant di hello non aveva automaticamente AzureRMS il provisioning. 

**Azione consigliata**  
Nel primo caso hello, avere utente hello aggiornare le credenziali e un dispositivo toohello account di accesso con le nuove credenziali hello. hello toosolve AzureRMS problema, procedere con hello passaggi elencati in [KB3193791](https://support.microsoft.com/kb/3193791). 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a>ID evento 1098: Errore: 0xCAA5001C Operazione broker del token non riuscita  
Nel Visualizzatore eventi in registri AAD/Operational hello, questo errore può verificarsi con eventi 1104: chiamata di plug-in PA di Cloud di Azure ad ottenere il token ha restituito l'errore: 0xC000005F. Questo problema si verifica se mancano autorizzazioni o attributi di proprietà.    

**Azione consigliata**  
Procedere con i passaggi di hello elencati [KB3196528](https://support.microsoft.com/kb/3196528).  



## <a name="next-steps"></a>Passaggi successivi

- Hello utilizzare [forum dedicato agli utenti](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming) di tooprovide commenti e suggerimenti e verificare i suggerimenti su come Enterprise tooimprove stato Roaming.

- Per ulteriori informazioni, vedere hello [Enterprise State Roaming Panoramica](active-directory-windows-enterprise-state-roaming-overview.md). 

## <a name="related-topics"></a>Argomenti correlati
* [Panoramica di Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Abilitare Enterprise State Roaming in Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Domande frequenti su impostazioni e dati in roaming](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Criteri di gruppo e impostazioni del software MDM per la sincronizzazione delle impostazioni](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Riferimento alle impostazioni di roaming di Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
