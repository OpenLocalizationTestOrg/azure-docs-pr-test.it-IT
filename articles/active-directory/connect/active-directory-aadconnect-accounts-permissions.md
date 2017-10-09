---
title: Account e autorizzazioni di Azure AD Connect | Documentazione Microsoft
description: In questo argomento viene utilizzato e creato gli account di hello e le autorizzazioni necessarie.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.reviewer: cychua
ms.assetid: b93e595b-354a-479d-85ec-a95553dd9cc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 70a7013e0353d74714ec8a3ff54b3e811789a0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-accounts-and-permissions"></a>Azure AD Connect: account e autorizzazioni
installazione guidata di Hello Azure AD Connect offre due diversi percorsi:

* In impostazioni Express, la procedura guidata hello è necessari più privilegi.  Si tratta in modo che è possibile impostare la configurazione facilmente, senza richiedere agli utenti di toocreate o configurare le autorizzazioni.
* In impostazioni personalizzate, la procedura guidata hello offre altre opzioni e scelte. Tuttavia, esistono alcune situazioni in cui è necessario tooensure si dispone delle autorizzazioni corrette hello manualmente.

## <a name="related-documentation"></a>Documentazione correlata
Se non è stato letto documentazione hello in [integrazione delle identità locali con Azure Active Directory](../active-directory-aadconnect.md), hello nella tabella seguente vengono forniti i collegamenti toorelated argomenti.

|Argomento |Collegamento|  
| --- | --- |
|Scaricare Azure AD Connect | [Scaricare Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Eseguire l'installazione con le Impostazioni rapide | [Installazione rapida di Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Eseguire l'installazione mediante le impostazioni personalizzate | [Installazione personalizzata di Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Aggiornamento da DirSync | [Aggiornamento dallo strumento di sincronizzazione di Azure AD (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Dopo l'installazione | [Verificare l'installazione di hello e assegnare le licenze](active-directory-aadconnect-whats-next.md)|

## <a name="express-settings-installation"></a>Installazione mediante le impostazioni rapide
Nelle impostazioni Express, installazione guidata di hello richiede le credenziali di amministratore di Active Directory di dominio Active Directory dell'organizzazione.  Si tratta quindi dell'istanza locale di Active Directory che è possibile configurare con le autorizzazioni necessarie per Azure AD Connect. Se esegue l'aggiornamento da DirSync, le credenziali di dominio Active Directory Enterprise Admins hello AD sono password hello tooreset utilizzato per l'account di hello usato da DirSync. Sono necessarie anche le credenziali di amministratore globale di Azure AD.

| Pagina della procedura guidata | Credenziali raccolte | Autorizzazioni necessarie | Utilizzo |
| --- | --- | --- | --- |
| N/D |Installazione guidata di utente in esecuzione hello |Amministratore del server locale hello |<li>Crea account locale hello che viene utilizzato come hello [account del servizio motore di sincronizzazione](#azure-ad-connect-sync-service-account). |
| Connettersi AD tooAzure |Credenziali di directory di Azure AD |Ruolo di amministratore in Azure AD |<li>Abilitazione della sincronizzazione nella directory di Azure AD hello.</li>  <li>Creazione di hello [account Azure AD](#azure-ad-service-account) che viene utilizzato per operazioni di sincronizzazione in corso in Azure AD.</li> |
| Connettersi tooAD di dominio Active Directory |Credenziali Active Directory locali |Membro del gruppo Enterprise Admins (EA) hello in Active Directory |<li>Crea un [account](#active-directory-account) in Active Directory e concede autorizzazioni tooit. Questo account creato è tooread e scrittura directory informazioni di uso durante la sincronizzazione.</li> |

### <a name="enterprise-admin-credentials"></a>Credenziali di amministratore dell'organizzazione
Queste credenziali vengono utilizzate solo durante l'installazione di hello e non vengono utilizzate una volta completata l'installazione di hello. Hello Enterprise Admin, non hello amministratore di dominio deve verificare che le autorizzazioni di hello in Active Directory possono essere impostate in tutti i domini.

### <a name="global-admin-credentials"></a>Credenziali di amministratore globale
Queste credenziali vengono utilizzate solo durante l'installazione di hello e non vengono utilizzate una volta completata l'installazione di hello. È utilizzato toocreate hello [account Azure AD](#azure-ad-service-account) usati per la sincronizzazione delle modifiche tooAzure Active Directory. account Hello permette anche di sincronizzazione come funzionalità in Azure AD.

### <a name="permissions-for-hello-created-ad-ds-account-for-express-settings"></a>Le autorizzazioni per hello creazione dell'account di dominio Active Directory per le impostazioni express
Hello [account](#active-directory-account) creato per leggere e scrivere tooAD di dominio Active Directory sono hello queste autorizzazioni quando creato da impostazioni express:

| Autorizzazione | Usato per |
| --- | --- |
| <li>Replica modifiche directory</li><li>Replica modifiche directory - Tutto |Sincronizzazione delle password |
| Lettura/scrittura di tutte le proprietà - Utente |Importazione ed Exchange ibrido |
| Lettura/scrittura di tutte le proprietà - iNetOrgPerson |Importazione ed Exchange ibrido |
| Lettura/scrittura di tutte le proprietà - Gruppo |Importazione ed Exchange ibrido |
| Lettura/scrittura di tutte le proprietà - Contatto |Importazione ed Exchange ibrido |
| Reimpostazione delle password |Preparazione per l'abilitazione del writeback delle password |

## <a name="custom-settings-installation"></a>Installazione mediante le impostazioni personalizzate
Azure AD Connect versione 1.1.524.0 e versioni successive con procedura guidata di hello opzione toolet hello Azure AD Connect creare hello account utilizzato tooconnect tooActive Directory.  Le versioni precedenti richiedono account hello viene creato prima dell'installazione di hello. è necessario concedere questo account le autorizzazioni di Hello sono reperibile [creare account di dominio Active Directory hello](#create-the-ad-ds-account). 

| Pagina della procedura guidata | Credenziali raccolte | Autorizzazioni necessarie | Utilizzo |
| --- | --- | --- | --- |
| N/D |Installazione guidata di utente in esecuzione hello |<li>Amministratore del server locale hello</li><li>Se si utilizza una versione completa di SQL Server, utente hello deve essere l'amministratore di sistema (SA) in SQL</li> |Per impostazione predefinita, crea l'account locale hello che viene utilizzato come hello [account del servizio motore di sincronizzazione](#azure-ad-connect-sync-service-account). account Hello viene creato solo quando salve non specifica un account specifico. |
| Installazione dei servizi di sincronizzazione, opzione Account di servizio |Active Directory o credenziali dell'account utente locale |Utente, le autorizzazioni vengono concesse mediante Installazione guidata di hello |Se salve specifica un account, questo account viene utilizzato come account del servizio hello per il servizio di sincronizzazione hello. |
| Connettersi AD tooAzure |Credenziali di directory di Azure AD |Ruolo di amministratore in Azure AD |<li>Abilitazione della sincronizzazione nella directory di Azure AD hello.</li>  <li>Creazione di hello [account Azure AD](#azure-ad-service-account) che viene utilizzato per operazioni di sincronizzazione in corso in Azure AD.</li> |
| Connessione delle directory |Credenziali di Active Directory locale per ogni foresta di cui è connesso tooAzure AD |autorizzazioni Hello dipendono dalle funzionalità di cui attiva e possono trovarsi in [creare account di dominio Active Directory hello](#create-the-ad-ds-account) |Questo account è utilizzate informazioni directory tooread e di scrittura durante la sincronizzazione. |
| Server ADFS |Per ogni server nell'elenco di hello, procedura guidata hello raccoglie le credenziali quando le credenziali di accesso hello dell'utente hello guidata hello sono tooconnect insufficiente |Amministratore di dominio |Installazione e configurazione del ruolo del server hello AD FS. |
| Server Proxy applicazione Web |Per ogni server nell'elenco di hello, procedura guidata hello raccoglie le credenziali quando le credenziali di accesso hello dell'utente hello guidata hello sono tooconnect insufficiente |Amministratore locale nel computer di destinazione hello |Installazione e configurazione del ruolo del server WAP. |
| Credenziali di attendibilità del proxy |Credenziali del servizio federativo trust (hello credenziali hello proxy utilizza tooenroll per un certificato di trust da ADFS hello |Account di dominio che sia un amministratore locale del server di hello AD FS |Registrazione iniziale del certificato di attendibilità di FS-WAP. |
| Pagina Account del servizio ADFS, "Utilizzare un'opzione account utente di dominio" |Credenziali dell'account utente di Active Directory |Utente di dominio |account utente di Hello AD vengono specificate le cui credenziali viene utilizzato come account di accesso hello del servizio ADFS hello. |

### <a name="create-hello-ad-ds-account"></a>Creare account di dominio Active Directory hello
l'account specificato in hello Hello **connettere le directory** pagina deve essere presente in Active Directory precedenti tooinstallation.  È necessario che abbia autorizzazioni hello necessario. installazione guidata di Hello non verifica le autorizzazioni di hello e agli eventuali problemi sono presenti solo durante la sincronizzazione.

Le autorizzazioni necessarie dipende dalle funzionalità facoltative di hello attiva. Se si hanno più domini, è necessario concedere le autorizzazioni di hello per tutti i domini nella foresta hello. Se non si abilita una di queste funzionalità, hello predefinito **utente di dominio** le autorizzazioni sono sufficienti.

| Funzionalità | Autorizzazioni |
| --- | --- |
| Funzionalità msDS-ConsistencyGuid |Le autorizzazioni di scrittura, l'attributo msDS-ConsistencyGuid toohello documentato in [concetti sulla progettazione - utilizzando l'attributo msDS-ConsistencyGuid come sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). | 
| Sincronizzazione delle password |<li>Replica modifiche directory</li>  <li>Replica modifiche directory - Tutto |
| Distribuzione ibrida di Exchange |Scrivere gli attributi di autorizzazioni toohello descritti in [writeback ibrida di Exchange](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) per gli utenti, gruppi e contatti. |
| Cartelle pubbliche della posta di Exchange |Gli attributi toohello le autorizzazioni di lettura descritti in [cartella pubblica di posta elettronica di Exchange](active-directory-aadconnectsync-attributes-synchronized.md#exchange-mail-public-folder) per le cartelle pubbliche. | 
| Writeback delle password |Scrivere gli attributi di autorizzazioni toohello descritti in [Introduzione a password management](../active-directory-passwords-writeback.md) per gli utenti. |
| Writeback dispositivi |Autorizzazioni concesse con uno script di PowerShell come descritto in [Writeback dei dispositivi](active-directory-aadconnect-feature-device-writeback.md). |
| Writeback dei gruppi |Lettura, creazione, aggiornamento ed eliminazione di oggetti di gruppo per i **gruppi di Office 365** sincronizzati.  Per altre informazioni, vedere [Writeback dei gruppi](active-directory-aadconnect-feature-preview.md#group-writeback).|

## <a name="upgrade"></a>Aggiornamento
Quando esegue l'aggiornamento da una versione di Azure AD Connect tooa nuova versione, è necessario hello queste autorizzazioni:

| Entità | Autorizzazioni necessarie | Utilizzo |
| --- | --- | --- |
| Installazione guidata di utente in esecuzione hello |Amministratore del server locale hello |Aggiornare i file binari. |
| Installazione guidata di utente in esecuzione hello |Membro di ADSyncAdmins |Apportare le modifiche tooSync regole e altre operazioni di configurazione. |
| Installazione guidata di utente in esecuzione hello |Se si utilizza una versione completa di SQL server: DBO (o simile) del database del motore di sincronizzazione hello |Apportare modifiche a livello di database, ad esempio l'aggiornamento di tabelle con nuove colonne. |

## <a name="more-about-hello-created-accounts"></a>Ulteriori informazioni su hello account creato
### <a name="active-directory-account"></a>Account Active Directory
Se si usano le impostazioni rapide, viene creato un account in Active Directory usato per la sincronizzazione. account Hello creato si trova nel dominio radice della foresta hello nel contenitore utenti hello e ha il nome preceduto da **MSOL_**. Hello account viene creato con una password complessa lunghe che non ha scadenza. Se nel dominio sono presenti criteri di password, assicurarsi che per tale account siano consentite password lunghe e complesse.

![Account AD](./media/active-directory-aadconnect-accounts-permissions/adsyncserviceaccount.png)

Se si utilizzano le impostazioni personalizzate, è responsabile per la creazione di account hello prima di iniziare l'installazione di hello.

### <a name="azure-ad-connect-sync-service-account"></a>Account del servizio di sincronizzazione Azure AD Connect
il servizio di sincronizzazione Hello può eseguire in account diversi. ad esempio con un **account del servizio virtuale** (VSA), un **account del servizio gestito del gruppo** (gMSA/sMSA) o un normale account utente. Opzioni Hello supportato sono state modificate con hello il rilascio di aprile 2017 di connessione quando si esegue una nuova installazione. Se si esegue un aggiornamento da una versione precedente di Azure AD Connect, tali opzioni non sono disponibili.

| Tipo di account | Opzione di installazione | Descrizione |
| --- | --- | --- |
| [Account del servizio virtuale](#virtual-service-account) | Rapida e personalizzata, aprile 2017 e versioni successive | Questa è l'opzione di hello utilizzato per tutte le installazioni di express, ad eccezione delle installazioni in un Controller di dominio. Per personalizzato, è opzione predefinita hello a meno che non viene utilizzata un'altra opzione. |
| [Account del servizio gestito del gruppo](#group-managed-service-account) | Personalizzata, aprile 2017 e versioni successive | Se si utilizza un server SQL remoto, si consiglia di toouse un gruppo di account del servizio gestito. |
| [Account utente](#user-account) | Rapida e personalizzata, aprile 2017 e versioni successive | Un account utente con il prefisso AAD_ viene creato durante l'installazione solo se è installato in Windows Server 2008 e in un controller di dominio. |
| [Account utente](#user-account) | Rapida e personalizzata, marzo 2017 e versioni precedenti | Durante l'installazione viene creato un account locale con prefisso AAD_. Se si usa l'installazione personalizzata, è possibile specificare un altro account. |

Se si utilizzano Connetti a una compilazione di marzo 2017 o precedente, si deve reimpostare la password di hello nell'account di servizio hello poiché Microsoft Elimina le chiavi di crittografia hello per motivi di sicurezza. È possibile modificare altri account hello account tooany senza reinstallare Azure AD Connect. Se si esegue l'aggiornamento compilazione tooa da 2017 aprile o in un secondo momento, quindi è password hello toochange supportati nell'account di servizio hello ma non è possibile modificare l'account di hello utilizzato.

> [!Important]
> È possibile impostare solo l'account del servizio hello durante la prima installazione. Non è supportato l'account del servizio hello toochange una volta completata l'installazione di hello.

Si tratta di una tabella di hello predefinita consigliata, e le opzioni supportate per hello sincronizzazione account del servizio.

Legenda:

- **Grassetto** indica l'opzione predefinita hello e in hello casi la maggior parte delle opzione consigliata.
- *Corsivo* indica hello opzione consigliata quando non è predefinita hello.
- 2008: opzione predefinita se installata in Windows Server 2008
- Non in grassetto: opzione supportata
- Account locale, dell'account utente locale sul server hello
- Account di dominio: account utente di dominio
- sMSA: [account del servizio gestito autonomo](https://technet.microsoft.com/library/dd548356.aspx)
- gMSA: [account del servizio gestito del gruppo](https://technet.microsoft.com/library/hh831782.aspx)

| | DB locale</br>Express | DB/SQL locale</br>Personalizzate | SQL remoto</br>Personalizzate |
| --- | --- | --- | --- |
| **computer autonomo o di gruppo di lavoro** | Non supportate | **VSA**</br>Account locale (2008)</br>Account locale |  Non supportate |
| **computer aggiunto a un dominio** | **VSA**</br>Account locale (2008) | **VSA**</br>Account locale (2008)</br>Account locale</br>Account di dominio</br>sMSA, gMSA | **gMSA**</br>Account di dominio |
| **Controller di dominio** | **Account di dominio** | *gMSA*</br>**Account di dominio**</br>sMSA| *gMSA*</br>**Account di dominio**|

#### <a name="virtual-service-account"></a>Account del servizio virtuale
Un account del servizio virtuale è un tipo speciale di account che non ha una password ed è gestito da Windows.

![VSA](./media/active-directory-aadconnect-accounts-permissions/aadsyncvsa.png)

Hello VSA è previsto toobe utilizzata con gli scenari in cui il motore di sincronizzazione hello e SQL si trovano in hello nello stesso server. Se si utilizza SQL remoto, si consiglia di toouse un [Account del servizio gestito del gruppo](#managed-service-account) invece.

Questa funzionalità richiede Windows Server 2008 R2 o versioni successive. Se si installa Azure AD Connect in Windows Server 2008, l'installazione hello fallback toousing un [account utente](#user-account) invece.

#### <a name="group-managed-service-account"></a>Account del servizio gestito del gruppo
Se si utilizza un server SQL remoto, si consiglia di toousing un **account del servizio gestito di gruppo**. Per ulteriori informazioni su come tooprepare in Active Directory per l'account del servizio gestito di gruppo, vedere [gruppo Managed Service Accounts Overview](https://technet.microsoft.com/library/hh831782.aspx).

Questa opzione, hello toouse [installare i componenti richiesti](active-directory-aadconnect-get-started-custom.md#install-required-components) selezionare **usare un account di servizio esistente**e selezionare **Account del servizio gestito**.  
![VSA](./media/active-directory-aadconnect-accounts-permissions/serviceaccount.png)  
È inoltre supportato toouse un [account del servizio gestito autonomo](https://technet.microsoft.com/library/dd548356.aspx). Tuttavia, possono essere usati solo nel computer locale hello e non vi è alcun toouse vantaggio loro tramite l'account del servizio virtuale hello predefinito.

Questa funzionalità richiede Windows Server 2012 o versioni successive. Se è necessario toouse un sistema operativo precedente e usare SQL remoto, quindi è necessario utilizzare un [account utente](#user-account).

#### <a name="user-account"></a>Account utente
Viene creato un account di servizio locale mediante Installazione guidata di hello (se non si specifica hello account toouse impostazioni personalizzate). account Hello è il prefisso **AAD_** e utilizzato per toorun servizio di sincronizzazione effettivo hello come. Se si installa Azure AD Connect in un Controller di dominio, account di hello viene creato nel dominio hello. Hello **AAD_** account del servizio deve essere presente nel dominio hello se:
   - si usa un server remoto che esegue SQL Server
   - si usa un proxy che richiede l'autenticazione

![Account del servizio di sincronizzazione](./media/active-directory-aadconnect-accounts-permissions/syncserviceaccount.png)

Hello account viene creato con una password complessa lunghe che non ha scadenza.

Questo account viene utilizzato toostore hello password per hello altri account in modo sicuro. Queste altre password di account vengono archiviate crittografate nel database di hello. le chiavi private Hello hello le chiavi di crittografia sono protetti con crittografia a chiave segreta di servizi di crittografia hello utilizzando Windows Data Protection API (DPAPI).

Se si utilizza una versione completa di SQL Server, account del servizio hello è hello DBO del database hello creato per il motore di sincronizzazione hello. servizio Hello non funzionerà come previsto con tutte le altre autorizzazioni. Viene inoltre creato l'accesso a SQL.

account Hello viene inoltre concessa toofiles autorizzazioni, le chiavi del Registro di sistema e altri toohello correlati oggetti motore di sincronizzazione.

### <a name="azure-ad-service-account"></a>Account del servizio Azure AD
Viene creato un account di Azure AD per l'utilizzo del servizio di sincronizzazione hello. Questo account può essere identificato in base al relativo nome visualizzato.

![Account AD](./media/active-directory-aadconnect-accounts-permissions/aadsyncserviceaccount.png)

viene utilizzato il nome di Hello hello hello dell'account di server in cui può essere identificata in hello seconda parte nome utente hello. Nell'immagine di hello, nome del server hello è FABRIKAMCON. Se si dispone di server di gestione temporanea, ogni server avrà il proprio account.

account del servizio Hello viene creato con una password complessa lunghe che non ha scadenza. Dispone un ruolo speciale **gli account di sincronizzazione della Directory** che ha solo le attività di sincronizzazione della directory di autorizzazioni tooperform. Questo ruolo incorporato e speciale non è possibile concedere di fuori di procedura guidata di Azure AD Connect hello. portale di Azure Hello Mostra questo account con ruolo hello **utente**.

In Azure AD esiste un limite di 20 account del servizio di sincronizzazione. elenco di hello tooget esistente Azure AD account del servizio in Azure AD, eseguire hello cmdlet di Azure AD PowerShell seguente:`Get-AzureADDirectoryRole | where {$_.DisplayName -eq "Directory Synchronization Accounts"} | Get-AzureADDirectoryRoleMember`

tooremove inutilizzati account del servizio Azure AD, eseguire hello cmdlet di Azure AD PowerShell seguente:`Remove-AzureADUser -ObjectId <ObjectId-of-the-account-you-wish-to-remove>`

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](../active-directory-aadconnect.md).
