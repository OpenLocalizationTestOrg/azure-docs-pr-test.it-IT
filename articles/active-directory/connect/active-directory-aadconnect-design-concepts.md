---
title: Concetti relativi alla progettazione per Azure AD Connect | Documentazione Microsoft
description: Questo argomento illustra alcune aree di progettazione dell'implementazione.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>Azure AD Connect: Concetti relativi alla progettazione
scopo di Hello di questo argomento è toodescribe aree che devono essere considerate durante la progettazione e implementazione hello di Azure AD Connect. Si tratta di un'analisi approfondita di determinate aree e questi concetti vengono illustrati brevemente anche in altri argomenti.

## <a name="sourceanchor"></a>sourceAnchor
attributo sourceAnchor Hello è definito come *un attributo non è modificabile nel corso della durata hello di un oggetto*. Identifica in modo univoco un oggetto come hello stesso oggetto locale e in Azure AD. attributo di Hello viene anche chiamato **immutableId** e i nomi di hello due vengono usati intercambiabili.

parola Hello non modificabile, ovvero "non può essere modificato", è importante toothis argomento. Poiché il valore dell'attributo non può essere modificato dopo che è stata impostata, è importante toopick una progettazione che supporta lo scenario.

attributo di Hello viene usato per hello seguenti scenari:

* Quando viene compilato un nuovo motore di sincronizzazione o quando il motore viene ricompilato dopo uno scenario di ripristino di emergenza, questo attributo collega gli oggetti esistenti in Azure AD con gli oggetti locali.
* Se si sposta da un modello di identità sincronizzato tooa identità solo cloud, quindi questo attributo consente agli oggetti troppo "associazione fissa" oggetti esistenti in Azure AD con oggetti locali.
* Se si utilizza la federazione, questo attributo insieme hello **userPrincipalName** viene utilizzata in hello attestazione toouniquely identificare un utente.

In questo argomento solo parla sourceAnchor in relazione toousers. Hello stesse regole si applicano i tipi di oggetto tooall, ma è solo per gli utenti che il problema è in genere un problema.

### <a name="selecting-a-good-sourceanchor-attribute"></a>Selezione di un attributo sourceAnchor valido
valore dell'attributo Hello deve seguire hello seguenti regole:

* La lunghezza del testo deve essere inferiore a 60 caratteri
  * I caratteri diversi da a-z, A-Z o 0-9 vengono codificati e conteggiati come 3 caratteri
* Non deve contenere un carattere speciale: &#92; ! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ' ; : , [ ] " @ _
* Deve essere globalmente univoco
* Deve essere una stringa, un valore intero o un numero binario
* Non deve essere basato sul nome dell'utente, queste modifiche
* Non devono fare distinzione tra maiuscole e minuscole e devono evitare valori che possono variare in base alle maiuscole/minuscole
* Deve essere assegnato quando viene creato l'oggetto hello

Se hello seleziona sourceAnchor non è di tipo stringa, quindi vengono visualizzati i caratteri speciali non tooensure di valore attributo hello Base64Encode di connettersi AD Azure. Se si utilizza un altro server federativo di ADFS, verificare che il server può anche attributo hello Base64Encode.

attributo sourceAnchor Hello è tra maiuscole e minuscole. Il valore "JohnDoe" non è hello uguale a "johndoe". Non è tuttavia consigliabile creare due oggetti che si differenziano solo per la distinzione tra maiuscole e minuscole.

Se si dispone di una singola foresta locale, quindi attributo hello è consigliabile utilizzare è **objectGUID**. È anche attributo hello utilizzato quando si Usa impostazioni rapide in Azure AD Connect e hello anche l'attributo utilizzato da DirSync.

Se si dispone di più foreste e non trasferire gli utenti tra insiemi di strutture e domini, quindi **objectGUID** è un attributo valido di toouse anche in questo caso.

Se gli utenti si spostano tra foreste e domini, è necessario trovare un attributo che non modifica o può essere spostato con utenti hello durante lo spostamento di hello. Un approccio consigliato è un attributo sintetico toointroduce. È possibile usare un attributo che include un elemento analogo a un GUID. Durante la creazione dell'oggetto, un nuovo GUID la creazione e sulla utente hello. Una regola di sincronizzazione personalizzate è possibile crearle in hello sincronizzazione motore server toocreate questo valore in base a hello **objectGUID** e aggiornamento hello selezionato attributo. Quando si sposta oggetto hello, rendere il contenuto di hello tooalso che copia di questo valore.

Un'altra soluzione consiste toopick un attributo esistente, si è certi di non modificare. Uno degli attributi più comunemente usati è **employeeID**. Se si considera un attributo che contiene lettere, assicurarsi che vi sia che alcun caso hello possibilità (lettere maiuscole e minuscole) è non possibile modificare il valore dell'attributo hello. Attributi non validi che non devono essere usati includere questi attributi con nome hello dell'utente di hello. In un matrimonio o divorzio, nome hello è previsto toochange, che non è consentita per questo attributo. Questo è anche un motivo per cui gli attributi, ad esempio **userPrincipalName**, **posta**, e **targetAddress** non sono possibili anche tooselect nell'installazione di hello Azure AD Connect procedura guidata. Tali attributi contengono anche hello "@" carattere non consentito in hello sourceAnchor.

### <a name="changing-hello-sourceanchor-attribute"></a>Modifica attributo sourceAnchor hello
Impossibile modificare il valore dell'attributo sourceAnchor Hello dopo hello oggetto è stato creato in Azure Active Directory e identità hello è sincronizzato.

Per questo motivo, hello le restrizioni seguenti si applica tooAzure AD Connect:

* attributo sourceAnchor Hello può essere impostata solo durante l'installazione iniziale. Se si esegue nuovamente Installazione guidata di hello, questa opzione è di sola lettura. Se è necessario toochange questa impostazione, è necessario disinstallare e reinstallare.
* Se si installa un altro server di Azure AD Connect, sarà necessario selezionare hello stesso attributo sourceAnchor utilizzato in precedenza. Se in precedenza mediante DirSync e di spostare tooAzure AD connettersi, è necessario utilizzare **objectGUID** poiché questo è l'attributo hello usato da DirSync.
* Se il valore di hello per sourceAnchor è stato modificato dopo l'oggetto hello esportata tooAzure Active Directory, quindi Azure AD Connect, genera un errore di sincronizzazione e non consente ulteriori modifiche su tale oggetto prima di risolvere il problema di hello e sourceAnchor hello viene modificato in hello directory di origine.

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>Uso di msDS-ConsistencyGuid come sourceAnchor
Per impostazione predefinita, Azure AD Connect (versione 1.1.486.0 e precedenti) Usa objectGUID come attributo sourceAnchor hello. ObjectGUID è generato dal sistema. Non è possibile specificare il relativo valore durante la creazione di oggetti di AD locale. Come illustrato nella sezione [sourceAnchor](#sourceanchor), esistono scenari in cui è necessario valore di sourceAnchor toospecify hello. Se gli scenari di hello tooyou applicabile, è necessario utilizzare un attributo di Active Directory (ad esempio, msDS-ConsistencyGuid) può essere configurato come attributo sourceAnchor hello.

Azure AD Connect (versione 1.1.524.0 e dopo) ora facilita l'uso di hello di msDS-ConsistencyGuid come attributo sourceAnchor. Quando si utilizza questa funzionalità, Azure AD Connect consente di configurare automaticamente le regole di sincronizzazione hello per:

1. Utilizzare msDS-ConsistencyGuid come attributo sourceAnchor hello per gli oggetti utente. ObjectGUID è usato per altri tipi di oggetto.

2. Per un dato locale utente AD oggetto il cui attributo msDS-ConsistencyGuid non è popolato, Azure AD Connect scrive l'attributo msDS-ConsistencyGuid toohello indietro di objectGUID valore in Active Directory locale. Dopo aver compilato l'attributo msDS-ConsistencyGuid hello, Azure AD Connect quindi Esporta hello oggetto tooAzure Active Directory.

>[!NOTE]
> Una volta una locale oggetto Active Directory viene importato in Azure AD Connect (che viene importato nel hello spazio connettore di Active Directory e proiettati in hello Metaverse), non è non possibile modificare il valore di sourceAnchor più. valore di sourceAnchor hello toospecify per un dato locale AD oggetto, configurare l'attributo msDS-ConsistencyGuid prima viene importato in Azure AD Connect.

### <a name="permission-required"></a>È necessaria l'autorizzazione
Per toowork questa funzionalità, è necessario concedere a hello AD DS account utilizzato toosynchronize con Active Directory locale attributo msDS-ConsistencyGuid toohello di autorizzazione scrittura in Active Directory locale.

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>Come tooenable hello funzionalità ConsistencyGuid - nuova installazione
È possibile abilitare l'utilizzo di hello di ConsistencyGuid come sourceAnchor durante l'installazione di nuovo. Questa sezione descrive dettagliatamente sia l'installazione rapida che quella personalizzata.

  >[!NOTE]
  > Solo versioni più recenti di Azure AD Connect (1.1.524.0 e dopo) supporta hello come ConsistencyGuid sourceAnchor durante l'installazione di nuovo.

### <a name="how-tooenable-hello-consistencyguid-feature"></a>Come tooenable hello ConsistencyGuid funzionalità
Attualmente, la funzione hello può essere abilitata solo durante l'installazione di Azure AD Connect di nuovo solo.

#### <a name="express-installation"></a>Installazione rapida
Quando si installa Azure AD Connect con la modalità di Express, procedura guidata di Azure AD Connect hello determina automaticamente toouse attributo hello Active Directory più appropriato come attributo sourceAnchor hello utilizzando hello seguente logica:

* In primo luogo, hello Azure AD Connect guidata query attributo hello AD tooretrieve tenant Azure AD come hello attributo sourceAnchor nell'installazione di hello precedente Azure AD Connect (se presente). Se queste informazioni sono disponibili, Azure AD Connect utilizza l'attributo hello stesso Active Directory.

  >[!NOTE]
  > Solo versioni più recenti di Azure AD Connect (1.1.524.0 e dopo) archivia le informazioni nel tenant di Azure AD sull'attributo sourceAnchor hello utilizzato durante l'installazione. Le versioni precedenti di Azure AD Connect non lo consentono.

* Se le informazioni sull'attributo sourceAnchor hello utilizzato non sono disponibile, la procedura guidata hello Controlla stato di hello dell'attributo msDS-ConsistencyGuid hello in Active Directory locale. Se l'attributo hello non è configurato su qualsiasi oggetto nella directory di hello, guidata hello utilizza hello msDS-ConsistencyGuid come attributo sourceAnchor hello. Se l'attributo hello è configurato per uno o più oggetti di directory di hello, la procedura guidata hello conclude attributo hello è utilizzato da altre applicazioni e non è adatto come attributo sourceAnchor...

* In questo caso, la procedura guidata hello fallback toousing objectGUID come attributo sourceAnchor hello.

* Una volta che viene stabilito l'attributo sourceAnchor hello, la procedura guidata hello archivia le informazioni di hello nel tenant di Azure AD. Hello informazioni verranno utilizzate da un'installazione di future di Azure AD Connect.

Al termine dell'installazione rapida, la procedura guidata hello informa l'utente è stato selezionato l'attributo come attributo di ancoraggio di origine hello.

![La procedura guidata segnala l'attributo di AD selezionato come sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>Installazione personalizzata
Quando si installa Azure AD Connect con modalità personalizzata, la procedura guidata di Azure AD Connect hello fornisce due opzioni quando si configura l'attributo sourceAnchor:

![Installazione personalizzata - Configurazione di sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| Impostazione | Descrizione |
| --- | --- |
| Consentire ad Azure di gestire l'ancoraggio di origine hello per me | Selezionare questa opzione se si desidera attributo hello toopick di Azure AD per l'utente. Se si seleziona questa opzione, Azure AD Connect guidata applica hello stesso [la logica di selezione attributo sourceAnchor utilizzata durante l'installazione di Express](#express-installation). Installazione tooExpress simile, la procedura guidata hello informa l'attributo è stato selezionato come hello attributo di ancoraggio di origine al termine dell'installazione personalizzata. |
| Attributo specifico | Selezionare questa opzione se si desidera toospecify un attributo di Active Directory esistente come attributo sourceAnchor hello. |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>Come tooenable hello funzionalità ConsistencyGuid - distribuzione esistente
Se si dispone di una distribuzione di Azure AD Connect esistente che utilizza objectGUID come attributo di ancoraggio di origine hello, è possibile tornare toousing ConsistencyGuid invece.

>[!NOTE]
> Solo versioni più recenti di Azure AD Connect (1.1.552.0 e dopo) supporta il passaggio da tooConsistencyGuid ObjectGuid come attributo di ancoraggio di origine hello.

tooswitch da tooConsistencyGuid objectGUID come attributo di ancoraggio di origine hello:

1. Avviare la procedura guidata Connect hello Azure AD e fare clic su **configura** schermata di toogo toohello attività.

2. Seleziona hello **configurare ancoraggio di origine** attività opzione e fare clic su **Avanti**.

   ![Abilitare ConsistencyGuid per una distribuzione esistente: passaggio 2](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. Immettere le credenziali di amministratore di Azure AD e fare clic su **Avanti**.

4. Procedura guidata di Azure AD Connect consente di analizzare lo stato di hello dell'attributo msDS-ConsistencyGuid hello in Active Directory locale. Se l'attributo hello non è configurato su qualsiasi oggetto nella directory, Azure AD Connect conclude che altre applicazioni non sono attualmente in uso attributo hello ed sono sicuro toouse hello come attributo di ancoraggio di origine hello. Fare clic su **Avanti** toocontinue.

   ![Abilitare ConsistencyGuid per una distribuzione esistente: passaggio 4](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. In hello **tooConfigure pronto** schermata, fare clic su **configura** modifica della configurazione toomake hello.

   ![Abilitare ConsistencyGuid per una distribuzione esistente: passaggio 5](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. Una volta completata la configurazione di hello, la procedura guidata hello indica che msDS-ConsistencyGuid ora viene utilizzata come attributo di ancoraggio di origine hello.

   ![Abilitare ConsistencyGuid per una distribuzione esistente: passaggio 6](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Durante l'analisi di hello (passaggio 4), se l'attributo hello è configurato per uno o più oggetti di directory di hello, la procedura guidata hello conclude attributo hello è utilizzato da un'altra applicazione e restituisce un errore, come illustrato nel seguente diagramma hello. Se si è certi che tale attributo hello non sia utilizzato da applicazioni esistenti, è necessario toocontact il supporto per informazioni su come toosuppress hello errore.

![Abilitare ConsistencyGuid per una distribuzione esistente: errore](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>Impatto su AD FS o configurazione della federazione di terze parti
Se si usa Azure AD Connect toomanage distribuzione di ADFS in locale, Azure AD Connect hello Aggiorna automaticamente l'attributo hello attestazione rules toouse hello stesso Active Directory come sourceAnchor. In questo modo tale attestazione ImmutableID hello generato da ADFS è coerente con hello sourceAnchor valori esportati tooAzure Active Directory.

Se si sta gestendo ADFS all'esterno di Azure AD Connect o si utilizzano server federativi di terze parti per l'autenticazione, è necessario aggiornare manualmente le regole attestazioni hello per ImmutableID toobe attestazione coerente con i valori di attributo sourceAnchor hello esportata tooAzure Active Directory come descritto nella sezione articolo [modifica AD FS regole attestazione](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims). la procedura guidata Hello restituisce hello seguente avviso al termine dell'installazione:

![Configurazione della federazione di terze parti](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>Aggiungendo la distribuzione tooexisting le directory nuova
Si supponga di che aver distribuito Azure AD Connect con abilitata la funzionalità ConsistencyGuid hello e si desidera tooadd un'altra distribuzione toohello di directory. Quando si tenta di directory hello tooadd, procedura guidata di Azure AD Connect Controlla stato hello dell'attributo mSDS-ConsistencyGuid hello nella directory hello. Se l'attributo hello è configurato per uno o più oggetti di directory di hello, la procedura guidata hello conclude attributo hello è utilizzato da altre applicazioni e restituisce un errore, come illustrato nel seguente diagramma hello. Se si è certi che tale attributo hello non sia utilizzato da applicazioni esistenti, è necessario toocontact il supporto per informazioni su come toosuppress hello errore.

![Aggiungendo la distribuzione tooexisting le directory nuova](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Accesso ad Azure AD
Durante l'integrazione della directory locale con Azure AD, è importante toounderstand come le impostazioni di sincronizzazione hello possono influire sul utente modo hello autentica. Azure AD Usa utente di hello tooauthenticate userPrincipalName (UPN). Tuttavia, quando si sincronizzano gli utenti, è necessario scegliere hello attributo toobe utilizzata per il valore di userPrincipalName con attenzione.

### <a name="choosing-hello-attribute-for-userprincipalname"></a>Attributo hello per userPrincipalName
Quando si seleziona attributo hello per fornire valore hello toobe UPN usato in uno di Azure deve verificare

* i valori di attributo Hello conforme toohello UPN sintassi (RFC 822) deve essere formato hellousername@domain
* suffisso Hello in hello valori corrispondenze tooone di hello i domini personalizzati verificati in Azure AD

In Impostazioni rapide, hello presuppone scelta per l'attributo hello è userPrincipalName. Se l'attributo userPrincipalName hello non contiene il valore di hello del toosign gli utenti in tooAzure, sarà quindi è necessario scegliere **installazione personalizzata**.

### <a name="custom-domain-state-and-upn"></a>Stato del dominio personalizzato e UPN
È importante tooensure che vi sia un dominio verificato per un suffisso UPN hello.

John è un utente di contoso.com. Si desidera John toouse hello locale UPN john@contoso.com toosign in tooAzure dopo aver siano stati sincronizzati utenti tooyour Azure Active directory contoso.onmicrosoft.com. toodo, pertanto, è necessario tooadd e verificare contoso.com come un dominio personalizzato in Azure AD prima di iniziare esegue la sincronizzazione degli utenti hello. Se il suffisso UPN hello John, ad esempio contoso.com, non corrisponde a un dominio verificato in Azure AD, Azure Active Directory sostituisce suffisso UPN hello con contoso.onmicrosoft.com.

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>Domini locali non instradabili e UPN per Azure AD
Alcune organizzazioni usano domini non instradabili, ad esempio contoso.local, o domini semplici con etichetta singola come contoso. Non è in grado di tooverify un dominio non è instradabile in Azure AD. Azure AD Connect è possibile sincronizzare tooonly un dominio verificato in Azure AD. Quando si crea una directory di Azure AD, viene creato un dominio instradabile che diventa dominio predefinito per Azure AD, ad esempio contoso.onmicrosoft.com. Pertanto, diventa necessario tooverify qualsiasi altro dominio instradabile in tale scenario nel caso in cui si desidera dominio onmicrosoft.com predefinito di toosync toohello.

Lettura [aggiungere tooAzure di nome Active Directory del dominio personalizzato](../active-directory-add-domain.md) per ulteriori informazioni sull'aggiunta e verifica i domini.

Azure AD Connect rileva se l'esecuzione avviene in un ambiente di dominio non instradabile e avvisa che è opportuno non proseguire con le impostazioni rapide. Se si sta operando in un dominio non è instradabile, quindi è probabile che l'UPN degli utenti hello hello è troppo suffissi non instradabile. Ad esempio, se si eseguono in contoso. Local, Azure AD Connect suggerito è toouse impostazioni personalizzate, invece di usare impostazioni rapide. Con le impostazioni personalizzate, si è l'attributo hello in grado di toospecify che deve essere utilizzato come toosign UPN in tooAzure dopo che gli utenti di hello sono sincronizzati tooAzure AD.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
