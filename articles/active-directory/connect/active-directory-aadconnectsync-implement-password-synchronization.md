---
title: sincronizzazione delle password aaaImplement con sincronizzazione di Azure AD Connect | Documenti Microsoft
description: "Vengono fornite informazioni sul funzionamento della sincronizzazione delle password e la modalità tooset backup."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: a0401640f2a4d914419ee4446f923bb3a972389d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a>Implementare la sincronizzazione password con il servizio di sincronizzazione Azure AD Connect
Questo articolo fornisce informazioni che è necessario toosynchronize le password utente da un'istanza locale di Active Directory istanza tooa basato su cloud Azure Active Directory (Azure AD).

## <a name="what-is-password-synchronization"></a>Informazioni sulla sincronizzazione password
Hello probabilità che sta impedito lavorare scadenza tooa dimenticato la password è correlato toohello numero di password diverse è necessario tooremember. Hello altre password, è necessario tooremember, hello superiore hello probabilità tooforget uno. Domande e le chiamate sulla reimpostazione della password e un'altra richiesta di problemi relativi alle password hello la maggior parte delle risorse di supporto tecnico.

Sincronizzazione password è una funzionalità che consente le password utente toosynchronize da un'istanza di tooa basato su cloud di Azure AD istanza di Active Directory locale.
Utilizzare questo toosign funzionalità tooAzure AD servizi come Office 365, Microsoft Intune, CRM Online e servizi di dominio Active Directory Azure (Azure AD DS). Accesso al servizio toohello utilizzando hello stessa password usata toosign in tooyour locale dell'istanza di Active Directory.

![Cos'è Azure AD Connect](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

Riducendo il numero di hello delle password, gli utenti devono toojust toomaintain uno. La sincronizzazione password permette di:

* Migliorare la produttività hello degli utenti.
* Ridurre i costi del supporto tecnico.  

Inoltre, se si decide di toouse [federazione con Active Directory Federation Services (ADFS)](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), è facoltativamente possibile configurare la sincronizzazione delle password come backup in caso di errore di infrastruttura di ADFS.

Sincronizzazione password è una funzionalità di sincronizzazione directory di toohello estensione implementata tramite la sincronizzazione di Azure AD Connect. toouse la sincronizzazione delle password nell'ambiente in uso, è necessario:

* Installare Azure AD Connect.  
* Configurare la sincronizzazione della directory tra l'istanza di Active Directory locale e l'istanza di Azure Active Directory.
* Abilitare la sincronizzazione password.

Per altri dettagli, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

> [!NOTE]
> Per altre informazioni su Azure Active Directory Domain Services configurato per FIPS e la sincronizzazione password, vedere "Sincronizzazione password e FIPS" più avanti in questo articolo.
>
>

## <a name="how-password-synchronization-works"></a>Funzionamento della sincronizzazione password
Hello servizi di dominio Active Directory archivia le password in forma di hello di una rappresentazione del valore hash della password utente effettiva hello. Un valore hash è un risultato di una funzione matematica unidirezionale (hello *algoritmo hash*). Non vi è alcun risultato hello toorevert del metodo di una versione di testo normale toohello funzione unidirezionale di una password. Non è possibile utilizzare un toosign hash password nella rete locale tooyour.

la password, Azure AD Connect sync estrae l'hash della password da toosynchronize hello istanza locale di Active Directory. Viene applicata un'elaborazione aggiuntiva di sicurezza toohello hash della password prima che venga sincronizzato toohello servizio di autenticazione di Azure Active Directory. Le password vengono sincronizzate per ogni singolo utente e in ordine cronologico.

Hello effettivo flusso di dati del processo di sincronizzazione password hello è simile toohello la sincronizzazione dei dati utente, ad esempio DisplayName o indirizzi di posta elettronica. Tuttavia, le password vengono sincronizzate più frequentemente di una finestra di sincronizzazione della directory standard hello per altri attributi. processo di sincronizzazione password Hello viene eseguita ogni 2 minuti. È possibile modificare la frequenza di hello di questo processo. Quando si sincronizza una password, sovrascrive password esistente nel cloud hello.

Hello prima che abilitare la funzionalità di sincronizzazione password hello, effettua una sincronizzazione iniziale delle password hello di tutti gli utenti nell'ambito. È possibile definire in modo esplicito un subset delle password degli utenti che si desidera toosynchronize.

Quando si modifica una password locale, hello aggiornato password viene sincronizzata, spesso in pochi minuti.
funzionalità di sincronizzazione password Hello tenterà automaticamente di tentativi di sincronizzazione non riuscita. Se si verifica un errore durante un tentativo toosynchronize una password, viene registrato un errore nel Visualizzatore eventi.

sincronizzazione Hello di una password non ha alcun impatto sull'utente hello attualmente connesso.
La sessione corrente del servizio cloud non è interessata da una modifica della password sincronizzata che si verifica quando si è connessi nel servizio cloud tooa immediatamente in. Tuttavia, quando il servizio cloud hello richiede tooauthenticate nuovamente, è necessario tooprovide la nuova password.

Un utente deve immettere le proprie credenziali aziendali un tooAzure di tooauthenticate tempo di secondo Active Directory, indipendentemente dal fatto che sono firmati nella rete aziendale tootheir. Queste serie può essere ridotto, tuttavia, se l'utente di hello seleziona hello Mantieni l'accesso nella casella di controllo (KMSI) all'accesso. La selezione di questa opzione imposta un cookie di sessione che permette di ignorare l'autenticazione per un breve periodo. Comportamento KMSI può essere abilitato o disabilitato dall'amministratore di Azure AD hello.

> [!NOTE]
> La sincronizzazione delle password è supportata solo per l'utente di tipo di oggetto hello in Active Directory. Non è supportata per il tipo di oggetto iNetOrgPerson hello.

### <a name="detailed-description-of-how-password-synchronization-works"></a>Descrizione dettagliata del funzionamento della sincronizzazione password
esempio Hello viene descritto nei dettagli il funzionamento della sincronizzazione password tra Active Directory e Azure AD.

![Flusso dettagliato della sincronizzazione password](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. Ogni due minuti, agente di sincronizzazione password hello nel server di connessione hello Active Directory richiede gli hash di password memorizzate (attributo unicodePwd hello) da un controller di dominio tramite hello standard [MS-DRSR](https://msdn.microsoft.com/library/cc228086.aspx) protocollo di replica utilizzato toosynchronize dati tra i controller di dominio. account del servizio Hello necessario replicare le modifiche di Directory e di replica Directory Changes All AD autorizzazioni (per impostazione predefinita nell'installazione) tooobtain hello gli hash delle password.
2. Prima dell'invio, hello controller di dominio esegue la crittografia hash della password hello MD4 tramite una chiave che è un [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) hash della chiave di sessione di hello RPC e un valore salt. Invia quindi l'agente di sincronizzazione password toohello hello risultato tramite RPC. Hello controller di dominio passa anche l'agente di sincronizzazione toohello salt hello utilizzando il protocollo di replica hello controller di dominio, pertanto busta hello in grado di toodecrypt agente hello.
3.  Dopo che l'agente di sincronizzazione password hello dispone di busta crittografato hello, Usa [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) e hello salt toogenerate un toodecrypt chiave hello ha ricevuto dati tooits indietro MD4 formato originale. In nessun punto l'agente di sincronizzazione password hello privo di password di accesso toohello come testo non crittografato. Hello uso dell'agente di sincronizzazione password di MD5 esclusivamente per la compatibilità di protocollo di replica con hello controller di dominio, e viene utilizzato solo in locale tra hello controller di dominio e l'agente di sincronizzazione password hello.
4.  l'agente di sincronizzazione password Hello espande byte too64 hash password binari a 16 byte di hello dal primo conversione hello tooa 32 byte esadecimali stringa hash, la conversione di questa stringa nuovamente in binario con codifica UTF-16.
5.  l'agente di sincronizzazione password Hello aggiunge un valore salt, costituito da un valore salt alla lunghezza di 10 byte, toohello 64 byte binari toofurther proteggere hash originale hello.
6.  l'agente di sincronizzazione password Hello combina hash MD4 hello e il salt e l'input nella hello [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) (funzione). 1000 le iterazioni di hello [HMAC-SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) viene utilizzato l'algoritmo hash con chiave. 
7.  l'agente di sincronizzazione password Hello accetta hash a 32 byte risultante hello, concatena entrambi salt hello hello svariate SHA256 iterazioni tooit (per l'utilizzo da Azure AD), quindi trasmette stringa hello da Azure AD Connect tooAzure AD tramite SSL.</br> 
8.  Quando un utente tenta di toosign in tooAzure AD e delle password, una password hello viene eseguito tramite hello MD4 stesso + salt + PBKDF2 + HMAC-SHA256 processo. Se l'hash risultante hello corrisponde hash hello archiviati in Azure AD, hello ha immesso la password corretta di hello ed è autenticato. 

>[!Note] 
>hash MD4 originale Hello non trasmessi tooAzure Active Directory. Al contrario, viene trasmessa hello hash SHA256 dell'algoritmo hash MD4 hello originale. Di conseguenza, se si ottiene l'hash hello archiviati in Azure AD, non è utilizzabile in un attacco pass-the-hash in locale.

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a>Funzionamento della sincronizzazione password con Azure Active Directory Domain Services
È inoltre possibile utilizzare toosynchronize funzionalità sincronizzazione password di hello le password locali troppo[Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-overview.md). In questo scenario, istanza di Azure Active Directory Domain Services hello autentica gli utenti nel cloud hello con tutti i metodi di hello disponibili nell'istanza di Active Directory locale. esperienza di Hello di questo scenario è simile toousing hello dello strumento di migrazione Active Directory (ADMT) in un ambiente locale.

### <a name="security-considerations"></a>Considerazioni relative alla sicurezza
Durante la sincronizzazione delle password, versione di hello testo della password non è esposto toohello funzionalità di sincronizzazione password, tooAzure Active Directory o i servizi associato hello.

Autenticazione utente avviene tramite Azure AD invece che sull'istanza di Active Directory dell'organizzazione hello. Se l'organizzazione ha problemi sui dati delle password in qualsiasi forma lasciando hello locale, si consiglia di fatto hello che hello dati password SHA256 archiviati in Azure AD, un hash dell'hash MD4 originale di hello - è notevolmente più sicura il contenuto archiviato in Active Directory. Inoltre, perché questo hash SHA256 non può essere decrittografato, non verranno nuovamente inclusi ambiente Active Directory dell'organizzazione toohello e presentato come una password utente validi in un attacco pass-the-hash.





### <a name="password-policy-considerations"></a>Considerazioni relative ai criteri password
L'abilitazione della sincronizzazione password influisce su due tipi di criteri password:

* Criteri di complessità delle password
* Criteri di scadenza delle password

#### <a name="password-complexity-policy"></a>Criteri di complessità delle password  
Quando è abilitata la sincronizzazione delle password, criteri di complessità delle password hello nell'istanza di Active Directory locale sostituiscono i criteri di complessità nel cloud hello per gli utenti sincronizzati. È possibile utilizzare tutte le password validi hello dal tooaccess istanza di Active Directory locale i servizi di Azure AD.

> [!NOTE]
> Le password degli utenti create direttamente in un cloud hello sono comunque criteri toopassword di oggetto come definito nel cloud hello.

#### <a name="password-expiration-policy"></a>Criteri di scadenza delle password  
Se un utente è nell'ambito di hello della sincronizzazione delle password, password dell'account cloud hello viene impostata troppo*non scadano mai*.

È possibile continuare toosign in servizi cloud tooyour tramite una password sincronizzata scaduti nell'ambiente locale. La password cloud verrà aggiornata hello successivo si modifica la password hello in hello nell'ambiente locale.

#### <a name="account-expiration"></a>Scadenza dell'account
Se l'organizzazione utilizza l'attributo accountExpires hello come parte della gestione degli account utente, tenere presente che questo attributo non è sincronizzata tooAzure Active Directory. Di conseguenza, un account Active Directory scaduto in un ambiente configurato per la sincronizzazione password continuerà a essere attivo in Azure AD. È consigliabile che se l'account hello è scaduto, un'azione del flusso di lavoro deve attivare uno script di PowerShell che disabilita hello Azure AD account utente. Al contrario, quando l'account di hello è attivata, istanza di Azure AD hello deve essere attivata.

### <a name="overwrite-synchronized-passwords"></a>Sovrascrivere password sincronizzate
Un amministratore può reimpostare manualmente la password usando Windows PowerShell.

In questo caso, nuova password hello sostituisce la password sincronizzata e tutti i criteri password definiti nel cloud hello vengono applicati toohello nuova password.

Se si modifica la password locale nuovamente, nuova password hello viene sincronizzato toohello cloud e viene eseguito l'override di password hello aggiornato manualmente.

sincronizzazione Hello di una password non ha alcun impatto su hello Azure utente che ha effettuato l'accesso. La sessione corrente del servizio cloud non è interessata da una modifica della password sincronizzata che si verifica dopo avere effettuato nel servizio cloud tooa immediatamente in. KMSI estende la durata di hello questa differenza. Quando il servizio cloud hello richiede tooauthenticate nuovamente, è necessario tooprovide la nuova password.

### <a name="additional-advantages"></a>Vantaggi aggiuntivi

- In genere, la sincronizzazione delle password è tooimplement più semplice rispetto a un servizio federativo. Non richiede altri server ed Elimina dipendenza da un utente di tooauthenticate servizio federativo a disponibilità elevata. 
- La sincronizzazione delle password può anche essere attivata in toofederation aggiunta. Può inoltre essere usata come fallback in caso di interruzione del servizio federativo.












## <a name="enable-password-synchronization"></a>Abilitare la sincronizzazione password
Quando si installa Azure AD Connect usando hello **impostazioni Express** opzione, la sincronizzazione delle password è abilitata automaticamente. Per altre informazioni dettagliate, vedere [Introduzione alle impostazioni rapide per Azure AD Connect](active-directory-aadconnect-get-started-express.md).

Se si utilizzano le impostazioni personalizzate quando si installa Azure AD Connect, la sincronizzazione delle password è disponibile nella pagina di accesso utente hello. Per altre informazioni dettagliate, vedere [Installazione personalizzata di Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

![Abilitazione della sincronizzazione password](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a>Sincronizzazione password e FIPS
Se il server è stato bloccato in base tooFederal Information Processing Standard (FIPS), MD5 è disabilitata.

**tooenable MD5 per la sincronizzazione delle password, eseguire hello alla procedura seguente:**

1. Passare too%programfiles%\Azure AD Sync\Bin.
2. Aprire miiserver.exe.config.
3. Passare toohello configuration/runtime nodo alla fine hello file hello.
4. Aggiungere hello nodo seguente:`<enforceFIPSPolicy enabled="false"/>`
5. Salvare le modifiche.

Come riferimento, il frammento di codice dovrà essere simile al seguente:

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

Per informazioni sulla sicurezza e su FIPS, vedere [AAD Password Sync, encryption and FIPS compliance](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/) (Sincronizzazione password, crittografia e conformità con FIPS di Azure AD).

## <a name="troubleshoot-password-synchronization"></a>Risolvere i problemi di sincronizzazione password
In caso di problemi di sincronizzazione password, vedere [Risolvere i problemi di sincronizzazione delle password](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="next-steps"></a>Passaggi successivi
* [Servizio di sincronizzazione Azure AD Connect: personalizzazione delle opzioni di sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
