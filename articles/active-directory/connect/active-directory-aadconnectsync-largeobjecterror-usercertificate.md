---
title: 'Sincronizzazione di Azure AD Connect: gestione degli errori LargeObject causati dall''attributo userCertificate | Microsoft Docs'
description: In questo argomento fornisce i passaggi correttivi hello per gli errori LargeObject causati dall'attributo userCertificate.
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 146ad5b3-74d9-4a83-b9e8-0973a19828d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e547fb5f601b92f6f5154de9997651b1f28c51b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-handling-largeobject-errors-caused-by-usercertificate-attribute"></a>Sincronizzazione di Azure AD Connect: gestione degli errori LargeObject causati dall'attributo userCertificate

Azure AD applica un limite massimo di **15** certificato valori hello **userCertificate** attributo. Se Azure AD Connect consente di esportare un oggetto con più di 15 valori tooAzure AD, Azure AD restituisce un **LargeObject** errore con il messaggio:

>*"l'oggetto sottoposto a provisioning hello è troppo grande. Trim numero hello dei valori di attributo per questo oggetto. Hello operazione verrà ritentata in hello successivo ciclo di sincronizzazione..."*

Hello LargeObject errore potrebbe essere causato da altri attributi di Active Directory. tooconfirm effettivamente è provocato da attributo userCertificate hello, è necessario tooverify oggetto hello in AD locale o in hello [ricerca Metaverse Synchronization Service Manager](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-mvsearch).

elenco di hello tooobtain degli oggetti nel tenant di LargeObject errori, utilizzare uno dei seguenti metodi hello:

 * Se il tenant è abilitato per Azure AD Connect Health per la sincronizzazione, è possibile fare riferimento toohello [segnalazione di errori di sincronizzazione](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-sync#object-level-synchronization-error-report-preview) fornito.
 
 * Hello notifica tramite posta elettronica per gli errori di sincronizzazione di directory che viene inviato alla fine di hello di ogni ciclo di sincronizzazione ha elenco hello di oggetti con errori LargeObject. 
 * Hello [scheda operazioni Synchronization Service Manager](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-operations) Visualizza l'elenco di hello degli oggetti con LargeObject errori se si fa clic su operazione tooAzure AD esportazione più recente di hello.
 
## <a name="mitigation-options"></a>Opzioni di mitigazione
Fino a quando non viene risolto l'errore LargeObject hello, altri toohello modifiche attributo oggetto stesso non può essere esportato tooAzure Active Directory. Errore di hello tooresolve, è possibile prendere in considerazione hello le opzioni seguenti:

 * L'aggiornamento di Azure AD Connect toobuild 1.1.524.0 o successiva. In Azure AD Connect 1.1.524.0 di compilazione, le regole di sincronizzazione di out-of-box hello sono stati aggiornati toonot esportazione attributi userCertificate e userSMIMECertificate se gli attributi di hello hanno valori di più di 15. Per informazioni dettagliate su come tooupgrade Azure AD Connect, fare riferimento tooarticle [Azure AD Connect: l'aggiornamento da una precedente toohello versione più recente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version).

 * Implementare un **regola di sincronizzazione in uscita** in Azure AD Connect che consente di esportare un **valore anziché i valori effettivi hello per gli oggetti con valori di più di 15 certificato null**. Questa opzione è adatta se uno dei valori esportati toobe tooAzure AD di hello certificato non è necessario per gli oggetti con valori di più di 15. Per informazioni dettagliate su come la sincronizzazione delle regole, vedere la sezione toonext tooimplement [implementazione esportazione toolimit regola di sincronizzazione dell'attributo userCertificate](#implementing-sync-rule-to-limit-export-of-usercertificate-attribute).

 * Ridurre il numero di hello dei valori certificato hello oggetto Active Directory (15 o meno) in locale da rimuovere i valori che non sono più in uso da parte dell'organizzazione. Questo è appropriato se crescita attributo hello è determinato dai certificati scaduti o non utilizzati. È possibile utilizzare hello [qui disponibili script di PowerShell](https://gallery.technet.microsoft.com/Remove-Expired-Certificates-0517e34f) toohelp trovare, eseguire il backup ed eliminare i certificati scaduti in locale Active Directory. Prima di eliminare i certificati di hello, è consigliabile verificare gli amministratori di hello--infrastruttura a chiave pubblica dell'organizzazione.

 * Configurazione di Azure AD Connect tooexclude hello userCertificate attributo viene esportato tooAzure Active Directory. In generale, è consigliabile scegliere questa opzione non poiché hello attributo può essere utilizzato per scenari specifici di Microsoft Online Services tooenable. In particolare:
    * attributo userCertificate Hello oggetto User hello viene utilizzato da Exchange Online e i client di Outlook per la crittografia e firma dei messaggi. toolearn informazioni su questa funzionalità, vedere tooarticle [S/MIME per la crittografia e firma dei messaggi](https://technet.microsoft.com/library/dn626158(v=exchg.150).aspx).

    * attributo userCertificate Hello sull'oggetto Computer hello viene utilizzato per i dispositivi appartenenti a un dominio tooconnect tooAzure AD di Azure AD tooallow Windows 10 in locale. toolearn informazioni su questa funzionalità, consultare tooarticle [connessione tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10 esperienze](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy).

## <a name="implementing-sync-rule-toolimit-export-of-usercertificate-attribute"></a>Implementazione di esportazione toolimit regola di sincronizzazione dell'attributo userCertificate
Errore di LargeObject hello tooresolve causato dall'attributo userCertificate hello, è possibile implementare una regola di sincronizzazione in uscita in Azure AD Connect che consente di esportare un **valore anziché i valori effettivi hello per gli oggetti con i valori del certificato più di 15null**. In questa sezione descrive hello passaggi necessari tooimplement hello regola di sincronizzazione per **utente** oggetti. Hello passaggi possono essere adattati per **contatto** e **Computer** oggetti.

> [!IMPORTANT]
> Esportazione di un valore null rimuove i valori precedentemente esportato correttamente tooAzure AD certificato.

passaggi di Hello possono essere riepilogati come:

1. Disabilitare l'utilità di pianificazione della sincronizzazione e verificare che non ci sia alcuna sincronizzazione in corso.
3. Trovare la regola di sincronizzazione in uscita esistente hello per attributo userCertificate.
4. Crea regola di sincronizzazione in uscita hello necessario.
5. Verificare hello nuova regola di sincronizzazione in un oggetto esistente con l'errore LargeObject.
6. Applicare hello nuova sincronizzazione regola tooremaining oggetti errore LargeObject.
7. Verificare che non sono presenti modifiche impreviste in attesa toobe esportato tooAzure Active Directory.
8. Esportare hello modifiche tooAzure Active Directory.
9. Riattivare l'utilità di pianificazione della sincronizzazione.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Passaggio 1. Disabilitare l'utilità di pianificazione della sincronizzazione e verificare che non ci sia alcuna sincronizzazione in corso
Verificare che viene eseguita alcuna sincronizzazione mentre si è al centro hello dell'implementazione di una nuova sincronizzazione tooavoid regola impreviste cambia being esportato tooAzure AD. toodisable hello sincronizzazione predefinite dell'utilità di pianificazione:
1. Avviare una sessione di PowerShell nel server di Azure AD Connect hello.

2. Disabilitare la sincronizzazione pianificata eseguendo di cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $false`

> [!Note]
> Hello passaggi precedenti sono solo toonewer applicabile versioni (1.1.xxx.x) di Azure AD Connect con utilità di pianificazione integrata hello. Se si utilizzano versioni precedenti (1.0.xxx.x) di Azure AD Connect che utilizza l'utilità di pianificazione di Windows, o si utilizza la propria sincronizzazione periodica tootrigger di utilità di pianificazione personalizzata (non comune), è necessario toodisable li conseguenza.

3. Avviare hello **Synchronization Service Manager** da passare → tooSTART servizio di sincronizzazione.

4. Passare toohello **operazioni** scheda e verificare che nessuna operazione il cui stato è *"in"corso.*

### <a name="step-2-find-hello-existing-outbound-sync-rule-for-usercertificate-attribute"></a>Passaggio 2. Trovare la regola di sincronizzazione in uscita esistente hello per attributo userCertificate
Deve essere presente una regola di sincronizzazione esistente che è abilitata e configurato l'attributo userCertificate tooexport per tooAzure oggetti utente Active Directory. Individuare questo toofind regola di sincronizzazione out relativo **precedenza** e **filtro di ambito** configurazione:

1. Avviare hello **Editor regole di sincronizzazione** da passare tooSTART → Editor regole di sincronizzazione.

2. Configurare i filtri di ricerca hello con hello seguenti valori:

    | Attributo | Valore |
    | --- | --- |
    | Direzione |**Outbound** |
    | MV Object Type |**Person** |
    | Connettore |*nome del connettore Azure AD* |
    | Connector Object Type |**user** |
    | MV attribute |**userCertificate** |

3. Se si utilizza l'attributo OOB (out-of-box) sincronizzazione rules tooAzure Active Directory connector tooexport userCertficiate per gli oggetti utente, è necessario tornare hello *"Out tooAAD – utente ExchangeOnline"* regola.
4. Annotare hello **precedenza** valore di questa regola di sincronizzazione.
5. Selezionare la regola di sincronizzazione hello e fare clic su **modifica**.
6. In hello *"Modifica riservato conferma regola"* finestra di dialogo popup, fare clic su **n**. (Non occorre preoccuparsi, non verrà toomake qualsiasi regola di sincronizzazione toothis modifica).
7. Nella schermata Modifica hello selezionare hello **definizione ambito filtro** scheda.
8. Prendere nota delle hello dell'ambito di configurazione del filtro. Se si utilizza una regola di sincronizzazione OOB hello, esattamente occorre **un gruppo di filtri ambito contenente due clausole**, tra cui:

    | Attributo | operatore | Valore |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | Utente |
    | cloudMastered | NOTEQUAL | True  |

### <a name="step-3-create-hello-outbound-sync-rule-required"></a>Passaggio 3. Crea regola di sincronizzazione in uscita hello richiesta
Hello nuova regola di sincronizzazione deve avere hello stesso **filtro di ambito** e **una precedenza più alta** di hello regola di sincronizzazione esistente. In questo modo si garantisce che hello nuova regola di sincronizzazione si applica toohello stesso set di oggetti come regola di sincronizzazione esistente hello e sostituzioni hello esistente regola di sincronizzazione per l'attributo userCertificate hello. regola di sincronizzazione toocreate hello:
1. In hello Editor regole di sincronizzazione, fare clic su hello **Aggiungi nuova regola** pulsante.
2. In hello **scheda Descrizione**, fornire hello seguente configurazione:

    | Attributo | Valore | Dettagli |
    | --- | --- | --- |
    | Nome | *Specificare un nome* | Ad esempio, *"Out tooAAD – personalizzato eseguire l'override per userCertificate"* |
    | Descrizione | *Inserire una descrizione* | Ad esempio *"Se l'attributo userCertificate contiene più di 15 valori, esportare NULL".* |
    | Connected System | *Selezionare hello Azure Active Directory Connector* |
    | Connected System Object Type | **user** | |
    | Metaverse Object Type | **person** | |
    | Tipo di collegamento | **Join** | |
    | Precedenza | *Scegliere un numero compreso tra 1 e 99* | non deve essere utilizzato da alcuna regola di sincronizzazione esistente Hello numero scelto e ha un valore più basso (e, pertanto, una precedenza più alta) di hello regola di sincronizzazione esistente. |

3. Passare toohello **definizione ambito filtro** scheda e implementare hello utilizza stesso ambito filtro hello esistente regola di sincronizzazione.
4. Hello Skip **regole di unione** scheda.
5. Passare toohello **trasformazioni** scheda tooadd una nuova trasformazione tramite seguente configurazione:

    | Attributo | Valore |
    | --- | --- |
    | Flow Type |**Expression** |
    | Target Attribute |**userCertificate** |
    | Source Attribute |*Hello Usa espressione seguente*:`IIF(IsNullOrEmpty([userCertificate]), NULL, IIF((Count([userCertificate])> 15),AuthoritativeNull,[userCertificate]))` |
    
6. Fare clic su hello **Aggiungi** regola di sincronizzazione hello toocreate pulsante.

### <a name="step-4-verify-hello-new-sync-rule-on-an-existing-object-with-largeobject-error"></a>Passaggio 4. Verificare hello nuova regola di sincronizzazione in un oggetto esistente con l'errore LargeObject
Si tratta di tooverify che hello sincronizzazione regola creata funzioni correttamente su un oggetto di Active Directory esistente con l'errore LargeObject prima di applicare gli oggetti tooother:
1. Passare toohello **operazioni** scheda hello Synchronization Service Manager.
2. Selezionare l'operazione tooAzure AD esportazione più recente di hello e fare clic su uno degli oggetti hello con LargeObject errori.
3.  Nella schermata popup di hello proprietà oggetto spazio connettore, fare clic su hello **anteprima** pulsante.
4. Nella schermata di popup di anteprima hello selezionare **completo sincronizzazione** e fare clic su **anteprima Commit**.
5. Chiudere la schermata di anteprima hello e schermata proprietà oggetto spazio connettore hello.
6. Passare toohello **connettori** scheda hello Synchronization Service Manager.
7. Fare clic su hello **AD Azure** connettore e selezionare **Esegui...**
8. Nel menu a comparsa Run Connector hello, selezionare **esportare** passaggio e fare clic su **OK**.
9. Attendere per esportazione tooAzure AD toocomplete e confermare che non si è verificato alcun errore LargeObject più su questo oggetto specifico.

### <a name="step-5-apply-hello-new-sync-rule-tooremaining-objects-with-largeobject-error"></a>Passaggio 5. Applicare hello nuovi sincronizzazione regola tooremaining oggetti errore LargeObject
Dopo aver aggiunto la regola di sincronizzazione hello, è necessario un passaggio di sincronizzazione completa su Active Directory Connector hello toorun:
1. Passare toohello **connettori** scheda hello Synchronization Service Manager.
2. Fare clic su hello **AD** connettore e selezionare **Esegui...**
3. Nel menu a comparsa Run Connector hello, selezionare **sincronizzazione completa** passaggio e fare clic su **OK**.
4. Attendere toocomplete passaggio di hello sincronizzazione completa.
5. Ripetere hello sopra i passaggi per hello rimanente connettori di Active Directory se si dispone di più connettori di Active Directory. In genere, sono necessari più connettori se si dispone di più directory locali.

### <a name="step-6-verify-there-are-no-unexpected-changes-waiting-toobe-exported-tooazure-ad"></a>Passaggio 6. Verificare che non sono presenti modifiche non previsto in attesa toobe esportato tooAzure AD
1. Passare toohello **connettori** scheda hello Synchronization Service Manager.
2. Fare clic su hello **AD Azure** connettore e selezionare **spazio connettore ricerca**.
3. Nel menu a comparsa spazio connettore ricerca hello:
    1. Impostare l'ambito troppo**esportare in sospeso**.
    2. Selezionare tutte e 3 le caselle di controllo, tra cui **Aggiungi**, **Modifica** ed **Elimina**.
    3. Fare clic su **ricerca** tooreturn pulsante tutti gli oggetti con modifiche in attesa toobe esportato tooAzure Active Directory.
    4. Verificare che non siano presenti modifiche impreviste. le modifiche di hello tooexamine per un determinato oggetto, fare doppio clic sull'oggetto hello.

### <a name="step-7-export-hello-changes-tooazure-ad"></a>Passaggio 7. Esportazione hello modifiche tooAzure AD
le modifiche hello tooexport tooAzure AD:
1. Passare toohello **connettori** scheda hello Synchronization Service Manager.
2. Fare clic su hello **AD Azure** connettore e selezionare **Esegui...**
4. Nel menu a comparsa Run Connector hello, selezionare **esportare** passaggio e fare clic su **OK**.
5. Attendere esportazione tooAzure AD toocomplete e verificare che non sono presenti ulteriori errori LargeObject.

### <a name="step-8-re-enable-sync-scheduler"></a>Passaggio 8. Riattivare l'utilità di pianificazione della sincronizzazione
Ora che hello problema viene risolto, abilitare nuovamente l'utilità di pianificazione sincronizzazione predefinite hello:
1. Avviare una sessione di PowerShell.
2. Riabilitare la sincronizzazione pianificata eseguendo di cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $true`

> [!Note]
> Hello passaggi precedenti sono solo toonewer applicabile versioni (1.1.xxx.x) di Azure AD Connect con utilità di pianificazione integrata hello. Se si utilizzano versioni precedenti (1.0.xxx.x) di Azure AD Connect che utilizza l'utilità di pianificazione di Windows, o si utilizza la propria sincronizzazione periodica tootrigger di utilità di pianificazione personalizzata (non comune), è necessario toodisable li conseguenza.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

