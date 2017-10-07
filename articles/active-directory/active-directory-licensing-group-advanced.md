---
title: Active Directory in base al gruppo licenze scenari aggiuntivi aaaAzure | Documenti Microsoft
description: Altri scenari relativi alle licenze basate sui gruppi in Azure Active Directory
services: active-directory
keywords: Licenze di Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: piotrci
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/02/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 782b7c9aa1c062a55c1241d69af673466f7a849c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-toomanage-licensing-in-azure-active-directory"></a>Gli scenari, limitazioni e problemi noti con gruppi toomanage licenze in Azure Active Directory

Utilizzare hello seguente toogain informazioni ed esempi di Azure Active Directory (Azure AD) in base al gruppo di licenze di conoscenze più avanzate.

## <a name="usage-location"></a>Località di utilizzo

Alcuni servizi Microsoft non sono disponibili in tutte le posizioni. Prima che può essere assegnata una licenza utente tooa, amministratore di hello ha hello toospecify **località di utilizzo** proprietà utente hello. In [hello Azure portal](https://portal.azure.com), è possibile specificare in **utente** &gt; **profilo** &gt; **impostazioni**.

Per l'assegnazione del gruppo di licenze, tutti gli utenti senza specificata una località di utilizzo erediterà percorso hello della directory di hello. Se sono presenti utenti in più posizioni, assicurarsi che tooreflect che correttamente negli oggetti utente prima di aggiungere utenti toogroups con le licenze.

> [!NOTE]
> L'assegnazione di licenze ai gruppi non modificherà mai un valore di località di utilizzo esistente per un utente. È consigliabile impostare sempre la località di utilizzo come parte del flusso di creazione utente in Azure Active Directory (ad esempio, tramite configurazione di AAD Connect) - che garantirà il risultato di hello dell'assegnazione delle licenze sempre sia corretto e gli utenti non ricevono in posizioni che non sono servizi è consentito.

## <a name="use-group-based-licensing-with-dynamic-groups"></a>Usare licenze basate sui gruppi con i gruppi dinamici

È possibile usare le licenze basate sui gruppi con qualsiasi gruppo di sicurezza, ovvero anche in associazione ai gruppi dinamici di Azure AD. Gruppi dinamici eseguiti regole tooautomatically di attributi oggetto utente di aggiungere e rimuovere utenti dai gruppi.

Ad esempio, è possibile creare un gruppo dinamico per alcuni set di prodotti desiderato tooassign toousers. Ogni gruppo è popolato da una regola di aggiunta di utenti per i relativi attributi e ogni gruppo di licenze di hello assegnato in cui si desidera tooreceive è. È possibile assegnare l'attributo hello in locale e sincronizzarlo con Azure AD, oppure è possibile gestire attributo hello direttamente nel cloud di hello.

Assegnazione delle licenze utente toohello subito dopo essere stati aggiunti toohello gruppo. Quando viene modificato l'attributo hello, utente hello lascia gruppi hello e licenze hello vengono rimossi.

### <a name="example"></a>Esempio

Considerare l'esempio hello di una soluzione di gestione di identità locale che decide quali utenti devono avere accesso tooMicrosoft web services. Usa **extensionAttribute1** toostore un valore stringa che rappresenta le licenze di hello hello utente dovrebbe essere. Azure AD Connect sincronizza questo valore con Azure AD.

Gli utenti potrebbero avere bisogno di una licenza invece di un'altra o potrebbero avere bisogno di entrambe. Di seguito è riportato un esempio, in cui si sta distribuendo Office 365 Enterprise E5 ed Enterprise Mobility + Security (EMS) toousers nei gruppi di licenze:

#### <a name="office-365-enterprise-e5-base-services"></a>Office 365 Enterprise E5: servizi di base

![Schermata di Office 365 Enterprise E5 servizi di base](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a>Enterprise Mobility + Security: utenti con licenza

![Schermata di Enterprise Mobility + Security utenti con licenza](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

Per questo esempio, un utente di modificare e impostare il valore di toohello extensionAttribute1 di `EMS;E5_baseservices;` se si desidera hello utente toohave entrambe le licenze. È possibile apportare questa modifica in locale. Dopo aver hello modificare esegue la sincronizzazione con il cloud hello, hello viene automaticamente aggiunto gruppi tooboth e assegnazione delle licenze.

![Screenshot che illustra come tooset hello extensionAttribute1 dell'utente](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> Prestare attenzione quando si modifica la regola di appartenenza di un gruppo esistente. Quando viene modificata una regola di appartenenza hello hello gruppo verrà valutate nuovamente e gli utenti che non corrispondono più ai hello new rule verrà rimossa (gli utenti che soddisfano ancora nuova regola hello non saranno interessati durante questo processo). Gli utenti avranno le licenze rimosse durante il processo di hello che potrebbe comportare la perdita di servizio o in alcuni casi, la perdita di dati.

> Se si dispone di un gruppo dinamico grandi che dipendono per l'assegnazione delle licenze, è consigliabile convalidare le modifiche principali in un gruppo di test più piccola prima di applicarli toohello principale gruppo.

## <a name="multiple-groups-and-multiple-licenses"></a>Più gruppi e più licenze

Un utente può essere membro di più gruppi con licenze. Ecco alcuni tooconsider operazioni:

- Più licenze per hello stesso prodotto può sovrapporsi e restituiscono tutti abilitati toohello applicato utente dei servizi. Hello riportato di seguito due gruppi di gestione delle licenze: *servizi di base E3* contiene hello foundation toodeploy innanzitutto tooall utenti di servizi. E *E3 estesi servizi* contiene servizi aggiuntivi (oscillazione e pianificazione) toodeploy solo toosome gli utenti. In questo esempio, utente hello è stato aggiunto tooboth gruppi:

  ![Schermata dei servizi abilitati](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  Di conseguenza, hello utente potrà 7 dei 12 servizi hello prodotto hello abilitato, quando si utilizza solo una licenza per questo prodotto.

- Se si seleziona hello *E3* licenza Mostra informazioni dettagliate, incluse le informazioni sui gruppi causato toobe quali servizi abilitati per l'utente hello.

  ![Schermata dei servizi abilitati per gruppo](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a>Le licenze dirette coesistono con le licenze di gruppo

Quando un utente eredita una licenza da un gruppo, è non è possibile rimuovere o modificare direttamente tale assegnazione delle licenze nelle proprietà dell'utente hello. Le modifiche devono essere effettuate nel gruppo hello e quindi propagato tooall utenti.

È possibile, tuttavia, tooassign hello licenza del prodotto stesso direttamente toohello utente, in aggiunta toohello ereditata licenza. È possibile attivare servizi aggiuntivi dal prodotto hello solo per un utente, senza influire su altri utenti.

Le licenze assegnate direttamente possono essere rimosse senza alterare le licenze ereditate. Prendere in considerazione gli utenti hello eredita una licenza di Office 365 Enterprise E3 da un gruppo.

1. Inizialmente, utente hello eredita la licenza hello solo hello *servizi di base E3* gruppo, che consente ai quattro piani di servizio, come illustrato:

  ![Schermata dei servizi abilitati del gruppo E3](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. È possibile selezionare **assegnare** toodirectly assegnare un utente di toohello licenza E3. In questo caso, si sta toodisable piani di servizio tutti ad eccezione di Yammer Enterprise:

  ![Schermata della procedura tooassign una licenza utente di tooa direttamente](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. Di conseguenza, hello utente usa una sola licenza del prodotto di hello E3. Ma assegnazione diretta hello consente hello Yammer Enterprise service solo per tale utente. È possibile visualizzare i servizi sono abilitati per l'appartenenza al gruppo hello e assegnazione diretta hello:

  ![Schermata dell'assegnazione ereditata rispetto all'assegnazione diretta](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. Quando si utilizza l'assegnazione diretta, è consentita hello seguenti operazioni:

  - Yammer che aziendale può essere disattivata oggetto user hello direttamente. Hello **On/Off** attiva/disattiva nella figura hello è stata abilitata per questo servizio, come anziché toohello altri elementi Toggle del servizio. Poiché il servizio di hello è abilitato direttamente in utente hello, può essere modificata.
  - Servizi aggiuntivi possono essere abilitati anche, come parte di hello direttamente dispone di licenza.
  - Hello **rimuovere** pulsante può essere utilizzato tooremove hello diretto licenza utente hello. È possibile vedere che hello utente ora può solo licenza gruppo ereditato hello e solo i servizi originale hello lasciare abilitati:

    ![Screenshot che illustra come indirizzare il tooremove assegnazione](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-tooproducts"></a>La gestione dei servizi di nuovo aggiunto tooproducts
Quando Microsoft aggiunge un nuovo prodotto tooa servizio, verrà abilitata per impostazione predefinita in tutti i gruppi toowhich assegnati licenza del prodotto hello. Gli utenti nel tenant che hanno sottoscritto toonotifications sulle modifiche apportate al prodotto riceveranno messaggi di posta elettronica anticipatamente informarli sulle aggiunte prossimo service hello.

Come amministratore, è possibile esaminare tutti i gruppi interessati dalla modifica hello e adottare azioni quali la disabilitazione di hello nuovo servizio di ogni gruppo. Se ad esempio sono stati creati gruppi interessati solo ai servizi specifici per la distribuzione, è possibile rivedere tali gruppi e assicurarsi di disabilitare i servizi appena aggiunti.

Ecco un esempio di come potrebbe presentarsi questo processo:

1. Originariamente assegnato hello *Office 365 Enterprise E5* tooseveral categorie. Uno di questi gruppi, denominati *O365 E5 - solo Exchange* è stato progettato tooenable solo hello *Exchange Online (pianificare 2)* servizio per i relativi membri.

2. Si ha ricevuto una notifica di Microsoft che hello E5 prodotto verrà esteso con un nuovo servizio - *Stream Microsoft*. Quando il servizio hello diventa disponibile nel tenant, è possibile eseguire il seguente hello:

3. Passare toohello [ **Azure Active Directory > licenze > tutti i prodotti** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) pannello e selezionare *Office 365 Enterprise E5*, quindi selezionare **gruppi di licenza**  tooview un elenco di tutti i gruppi con tale prodotto.

4. Fare clic sul gruppo hello desiderato tooreview (in questo caso, *O365 E5 - solo Exchange*). Verrà aperta hello **licenze** scheda. Facendo clic su licenza E5 hello verrà aperto un pannello elenca tutti i servizi abilitati.
> [!NOTE]
> Hello *Microsoft Stream* servizio è stato automaticamente aggiunto e abilitato in questo gruppo, in aggiunta toohello *Exchange Online* servizio:

  ![Schermata del nuovo servizio aggiunto licenza gruppo tooa](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. Se si desidera toodisable hello nuovo servizio di questo gruppo, fare clic su hello **On/Off** attivare o disattivare il servizio toohello successivo e fare clic su hello **salvare** pulsante Modifica hello tooconfirm. Azure AD verrà ora elaborare tutti gli utenti di modifica di hello tooapply gruppo hello. tutti i nuovi utenti aggiungono toohello gruppo non avrà hello *Microsoft Stream* il servizio è abilitato.

  > [!NOTE]
  > Gli utenti possono ancora servizio hello abilitato tramite alcuni altri assegnazione delle licenze (un altro gruppo sono i membri di o un'assegnazione della licenza diretto).

6. Se necessario, eseguire hello assegnati stessi passaggi per altri gruppi con questo prodotto.

## <a name="use-powershell-toosee-who-has-inherited-and-direct-licenses"></a>Utilizzare PowerShell toosee che ha ereditato e indirizzare le licenze
Se gli utenti dispongono di una licenza assegnata direttamente o ereditate da un gruppo, è possibile utilizzare un toocheck di script di PowerShell.

1. Eseguire hello `connect-msolservice` tooauthenticate cmdlet e connettere tooyour tenant.

2. `Get-MsolAccountSku`può essere utilizzato toodiscover tutte le licenze prodotto sottoposto a provisioning nel tenant di hello.

  ![Schermata del cmdlet Get-Msolaccountsku hello](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. Hello utilizzare *AccountSkuId* valore di licenza hello si è interessati con [questo script di PowerShell](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group). Verrà restituito un elenco di utenti che dispongono di questa licenza con informazioni hello sulla modalità di assegnazione di licenza hello.

## <a name="use-audit-logs-toomonitor-group-based-licensing-activity"></a>Attività di gestione delle licenze in base al gruppo toomonitor i log di controllo di utilizzo

È possibile utilizzare [log di controllo di Azure AD](./active-directory-reporting-activity-audit-logs.md#audit-logs) toosee tutte le attività correlate licenze basate su toogroup, tra cui:
- l'utente che ha modificato le licenze nei gruppi
- Quando il sistema hello avviato l'elaborazione di una modifica di licenza di gruppo e termine
- le modifiche di licenza sono state apportate tooa utente come risultato di un'assegnazione del gruppo di licenze.

>[!NOTE]
> I log di controllo sono disponibili nella maggior parte dei pannelli nella sezione di Azure Active Directory del portale hello hello. A seconda di dove si accedere ad essi, i filtri potrebbero essere contesto toohello rilevanti dell'attività Mostra tooonly pre-applicato del pannello hello. Se non vengono visualizzati i risultati di hello previsti, esaminare [hello opzioni di filtro](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs) o accedere ai log di controllo non filtrato hello in [ **Azure Active Directory > attività > log di controllo** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).

### <a name="find-out-who-modified-a-group-license"></a>Individuare chi ha modificato una licenza di gruppo

1. Set hello **attività** filtrare troppo*Set gruppo licenza* e fare clic su **applica**.
2. i risultati di Hello includono tutti i casi di licenze viene impostato o modificato nei gruppi.
>[!TIP]
> È anche possibile digitare il nome di hello del gruppo di hello in hello *destinazione* tooscope hello risultati filtro.

3. Fare clic su un elemento hello elenco toosee hello dettagli di cosa è cambiato. In *proprietà modificate* sono elencati i valori vecchi e nuovi per l'assegnazione delle licenze hello.

Di seguito è riportato un esempio di modifiche recenti alle licenze di gruppo con i dettagli:

![Schermata delle modifiche alle licenze di gruppo](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a>Sapere quando è iniziata e terminata l'elaborazione delle modifiche al gruppo

Quando una licenza di un gruppo, Azure AD verrà avviata l'applicazione hello modifiche tooall utenti.

1. toosee quando gruppi è stato avviato l'elaborazione, impostare hello **attività** filtrare troppo*avviare l'applicazione di gruppo basato su licenza toousers*. Si noti che attore hello per operazione hello è *Microsoft Azure AD in base al gruppo di licenze* -account di un sistema che viene utilizzato tooexecute tutte le modifiche di licenza di gruppo.
>[!TIP]
> Fare clic su un elemento hello di hello elenco toosee *proprietà modificate* field - Mostra modifiche alle licenze hello che sono stati selezionati per l'elaborazione. Ciò è utile se sono state apportate più le modifiche tooa gruppo e non si è certi che uno è stato elaborato.

2. In modo analogo, toosee al termine dell'elaborazione, Usa il valore filtro hello gruppi *terminare l'applicazione di gruppo basato su licenza toousers*.
>[!TIP]
> In questo caso, hello *proprietà modificate* campo contiene un riepilogo dei risultati di hello - si tratta di controllo tooquickly utile se l'elaborazione ha restituito gli eventuali errori. Output di esempio:
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. toosee hello completo del registro per la modalità in cui è stato elaborato un gruppo, incluse tutte le modifiche degli utenti, imposta hello seguenti filtri:
  - **Azione avviata da (attore)**: "Microsoft Azure AD Group-Based Licensing"
  - **Intervallo di date** (facoltativo): intervallo personalizzato per quando si conosce l'inizio e la fine dell'elaborazione di un gruppo specifico

Questo output di esempio mostra avvio hello di elaborazione, risultante tutte le modifiche dell'utente e hello di fine dell'elaborazione.

![Schermata delle modifiche alle licenze di gruppo](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> Fare clic su elementi correlati troppo*licenza utente di modifica* per visualizzare i dettagli per licenza modifiche applicate tooeach singolo utente.

## <a name="limitations-and-known-issues"></a>Limitazioni e problemi noti

Se si utilizza licenze basate su gruppo, è toofamiliarize una buona familiarità con hello segue l'elenco delle limitazioni e problemi noti.

- La gestione delle licenze basate sui gruppi attualmente non supporta i "gruppi annidati", ovvero i gruppi che contengono altri gruppi. Se si applica a un gruppo nidificato tooa di licenza, solo i membri immediato utente di primo livello hello del gruppo di hello hanno licenze hello applicate.

- funzionalità di Hello è utilizzabile solo con gruppi di sicurezza. Gruppi di Office non sono attualmente supportati e non sarà in grado di toouse nel processo di assegnazione delle licenze hello.

- Hello [il portale di amministrazione di Office 365](https://portal.office.com ) attualmente non supporta le licenze basate su gruppo. Se un utente eredita una licenza da un gruppo, la licenza viene visualizzato nel portale di amministrazione di Office hello come una licenza utente normale. Se si tenta di toomodify di licenza o provare a licenza hello tooremove, portale hello restituisce un messaggio di errore. Le licenze di gruppo ereditate non possono essere modificate direttamente per un utente.

- Quando un utente viene rimosso da un gruppo e perde la licenza di hello, piani di servizio hello da tale licenza (ad esempio, SharePoint Online) vengono impostati tooa **Suspended** stato. Hello i piani di servizio non sono impostati tooa finale, nello stato disabilitato. Questa precauzione evita la rimozione accidentale di dati dell'utente se un amministratore commette un errore nella gestione delle appartenenze al gruppo.

- L'assegnazione o la modifica delle licenze di un gruppo di grandi dimensioni (ad esempio 100.000 utenti) potrebbe influire sulle prestazioni. In particolare, il volume di hello delle modifiche generato mediante l'automazione di Azure AD potrebbe compromettere le prestazioni di hello della sincronizzazione tra Azure Active directory e dei sistemi locali.

- Automazione della gestione licenze non reagisce automaticamente tooall tipi di modifiche nell'ambiente di hello. Ad esempio, è possibile avere eseguire privo di licenze, causando toobe alcuni utenti in uno stato di errore. toofree conteggio posto disponibile hello, è possibile rimuovere alcune licenze assegnate direttamente ad altri utenti. Tuttavia, sistema hello automaticamente reagire toothis modifica e risolvere gli utenti in tale stato di errore.

  Come tipi di toothese una soluzione di limitazioni, è possibile passare toohello **gruppo** pannello in Azure AD, fare clic su **rielaborare**. Questo comando elabora tutti gli utenti in tale gruppo e risolve gli stati di errore hello, se possibile.

- In base al gruppo di licenze non registra gli errori quando una licenza non è possibile assegnare tooa utente a causa di configurazione degli indirizzi proxy duplicati tooa in Exchange Online; tali utenti verranno ignorati durante l'assegnazione delle licenze. Per ulteriori informazioni su come tooidentify e risolvere il problema, vedere [in questa sezione](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online).

## <a name="next-steps"></a>Passaggi successivi

toolearn più informazioni sugli altri scenari per la gestione delle licenze tramite in base al gruppo di licenze, vedere:

* [Che cosa sono le licenze basate sui gruppi in Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [L'assegnazione gruppo di licenze tooa in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Identificazione e risoluzione dei problemi relativi alle licenze per un gruppo in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Come singoli toomigrate concesso in licenza agli utenti in base toogroup licenze in Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
