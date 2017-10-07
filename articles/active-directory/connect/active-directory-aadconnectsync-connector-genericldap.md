---
title: Connettore LDAP aaaGeneric | Documenti Microsoft
description: Questo articolo viene descritto come connettore LDAP generico tooconfigure Microsoft.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 984beeb0-4d91-4908-ad81-c19797c4891b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 25031b4da196bd073902b04b0705762bfa0118b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="generic-ldap-connector-technical-reference"></a>Documentazione tecnica sul connettore Generic LDAP
Questo articolo descrive hello connettore LDAP generico. articolo Hello applica toohello i seguenti prodotti:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * È necessario usare l'hotfix 4.1.3671.0 o versione successiva ( [KB3092178](https://support.microsoft.com/kb/3092178)).

Per MIM2016 e FIM2010R2, è disponibile come download hello hello connettore [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

Quando si fa riferimento RFC tooIETF, questo documento viene utilizzato il formato di hello (RFC [RFC number] / [sezione nel documento RFC]), ad esempio (RFC 4512/4.3).
Per ulteriori informazioni in http://tools.ietf.org/html/rfc4500 (necessario tooreplace 4500 con numero RFC corretto hello).

## <a name="overview-of-hello-generic-ldap-connector"></a>Panoramica di hello connettore LDAP generico
Connettore LDAP generico Hello consente si toointegrate hello servizio di sincronizzazione con un server LDAP v3.

Determinate operazioni e gli elementi dello schema, ad esempio quelli necessari importazione delta tooperform, non sono specificati in hello IETF RFC. Per queste operazioni sono supportate solo le directory LDAP specificate in modo esplicito.

Dal punto di vista di alto livello, hello seguenti caratteristiche è supportata dalla versione corrente di hello del connettore hello:

| Funzionalità | Supporto |
| --- | --- |
| Origine dati connessa |Connettore Hello è supportato con tutti i server di v3 LDAP (compatibile con RFC 4510). È stato testato con seguenti hello: <li>Microsoft Active Directory Lightweight Directory Services (AD LDS)</li><li>Catalogo globale Microsoft Active Directory</li><li>389 Directory Server</li><li>Apache Directory Server</li><li>IBM Tivoli DS</li><li>Isode Directory</li><li>NetIQ eDirectory</li><li>Novell eDirectory</li><li>Open DJ</li><li>Open DS</li><li>Open LDAP (openldap.org)</li><li>Oracle (in precedenza Sun) Directory Server Enterprise Edition</li><li>RadiantOne Virtual Directory Server (VDS)</li><li>Sun One Directory Server</li>**Directory rilevanti non supportate:** <li>Servizi di dominio Active Directory Microsoft (AD DS) [utilizzare hello predefinite di Active Directory Connector invece]</li><li>Oracle Internet Directory (OID)</li> |
| Scenari |<li>Gestione del ciclo di vita degli oggetti</li><li>Gestione di gruppi</li><li>Gestione delle password</li> |
| Operazioni |Hello dopo le operazioni è supportata in tutte le directory LDAP: <li>Importazione completa</li><li>Esporta</li>Hello dopo le operazioni è supportata solo nelle directory specificate:<li>Importazione delta</li><li>Imposta password, Cambia password</li> |
| Schema |<li>Schema viene rilevato dallo schema LDAP hello (RFC3673 e RFC4512/4.2)</li><li>Supporta classi strutturali, classi aux e la classe di oggetti extensibleObject (RFC4512/4.3)</li> |

### <a name="delta-import-and-password-management-support"></a>Supporto per l'importazione delta e la gestione delle password
Directory supportate per l'importazione delta e la gestione delle password:

* Microsoft Active Directory Lightweight Directory Services (AD LDS)
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione della password
* Catalogo globale Microsoft Active Directory
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione della password
* 389 Directory Server
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione e la modifica delle password
* Apache Directory Server
  * Non supporta l'importazione delta perché questa directory non ha un registro delle modifiche persistenti
  * Supporta l'impostazione della password
* IBM Tivoli DS
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione e la modifica delle password
* Isode Directory
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione e la modifica delle password
* Novell eDirectory e NetIQ eDirectory
  * Supporta le operazioni di aggiunta, aggiornamento e ridenominazione per l'importazione delta
  * Non supporta le operazioni di eliminazione per l'importazione delta
  * Supporta l'impostazione e la modifica delle password
* Open DJ
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione e la modifica delle password
* Open DS
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione e la modifica delle password
* Open LDAP (openldap.org)
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione della password
  * Non supporta la modifica della password
* Oracle (in precedenza Sun) Directory Server Enterprise Edition
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione e la modifica delle password
* RadiantOne Virtual Directory Server (VDS)
  * È necessario usare la versione 7.1.1 o successiva
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione e la modifica delle password
* Sun One Directory Server
  * Supporta tutte le operazioni per l'importazione delta
  * Supporta l'impostazione e la modifica delle password

### <a name="prerequisites"></a>Prerequisiti
Prima di utilizzare connettore hello, verificare di che aver seguito hello sul server di sincronizzazione hello:

* Microsoft .NET 4.5.2 Framework o versione successiva

### <a name="detecting-hello-ldap-server"></a>Rilevamento server LDAP hello
Hello connettore si basa su varie tecniche toodetect e identificare i server LDAP hello. Usa connettore Hello hello DSE radice, nome/versione del fornitore, e analizza gli oggetti univoci hello dello schema toofind attributi noti tooexist in alcuni server LDAP. Questi dati, se trovato, viene utilizzato toopre-opzioni di configurazione hello in hello connettore compilate.

### <a name="connected-data-source-permissions"></a>Autorizzazioni dell'origine dati connessa
tooperform importare ed esportare le operazioni sugli oggetti hello directory connessa hello, l'account del connettore hello necessario disporre delle autorizzazioni sufficienti. connettore di Hello deve tooexport in grado di toobe di autorizzazioni di scrittura e lettura autorizzazioni toobe in grado di tooimport. Configurazione di autorizzazioni viene eseguita all'interno delle esperienze di gestione di hello della directory di destinazione hello stesso.

### <a name="ports-and-protocols"></a>Porte e protocolli
connettore Hello utilizza il numero di porta hello specificato nella configurazione di hello, che per impostazione predefinita è 389 per LDAP e 636 per LDAP.

Per LDAPS è necessario usare SSL 3.0 o TLS. SSL 2.0 non è supportato e non può essere attivato.

### <a name="required-controls-and-features"></a>Funzionalità e controlli necessari
Hello LDAP seguenti controlli o le funzionalità devono essere disponibili nel server LDAP hello per hello connettore toowork correttamente:  
`1.3.6.1.4.1.4203.1.5.3` Filtri True/False

filtro True/False Hello spesso non viene segnalato supportata dalla directory LDAP e potrebbe essere visualizzata in hello **pagina globale** in **obbligatorio non trovate funzionalità**. È utilizzato toocreate **o** filtri nella query LDAP, ad esempio durante l'importazione di più tipi di oggetto. Se è possibile importare più di un tipo di oggetto, il server LDAP supporta questa funzionalità.

Se si utilizza una directory in cui un identificatore univoco è seguente hello di hello ancoraggio deve essere disponibile (per ulteriori informazioni, vedere hello [configurare Anchor](#configure-anchors) sezione):  
`1.3.6.1.4.1.4203.1.5.1` Tutti gli attributi operativi

Se la directory hello dispone di più oggetti di ciò che è possibile inserire in una chiamata toohello directory, è consigliabile toouse paging. Per il paging toowork, è necessario uno degli hello le opzioni seguenti:

**Opzione 1:**  
`1.2.840.113556.1.4.319` pagedResultsControl

**Opzione 2:**  
`2.16.840.1.113730.3.4.9` VLVControl  
`1.2.840.113556.1.4.473` SortControl

Se entrambe le opzioni sono abilitate nella configurazione del connettore hello, pagedResultsControl viene utilizzato.

`1.2.840.113556.1.4.417` ShowDeletedControl

ShowDeletedControl viene utilizzato solo con hello USNChanged delta Importa metodo toobe toosee in grado di eliminare oggetti.

connettore Hello tenta opzioni hello toodetect presente nel server di hello. Se le opzioni di hello non possono essere rilevate, un avviso è presente nella pagina globale hello proprietà connettore hello. Non tutti i server LDAP presenti tutti i controlli o le funzionalità supportano e anche se questo avviso non è presente, hello connettore potrebbe funzionare senza problemi.

### <a name="delta-import"></a>Importazione delta
L'importazione delta è disponibile solo quando è stata rilevata una directory di supporto. è attualmente in uso Hello dei seguenti metodi:

* LDAP Accesslog. Vedere [http://www.openldap.org/doc/admin24/overlays.html#Access Logging](http://www.openldap.org/doc/admin24/overlays.html#Access Logging)
* LDAP Changelog. Vedere [http://tools.ietf.org/html/draft-good-ldap-changelog-04](http://tools.ietf.org/html/draft-good-ldap-changelog-04)
* TimeStamp. Per/NetIQ Novell eDirectory, hello connettore utilizza ultima data/ora tooget creati e aggiornati gli oggetti. / NetIQ Novell eDirectory non fornisce che un equivalente significa tooretrieve eliminate oggetti. Questa opzione può essere utilizzata anche se nessun altro metodo di importazione delta è attivo nel server LDAP hello. Questa opzione non è in grado di tooimport eliminate oggetti.
* USNChanged. Vedere: [https://msdn.microsoft.com/library/ms677627.aspx](https://msdn.microsoft.com/library/ms677627.aspx)

### <a name="not-supported"></a>Non supportate
Hello seguenti LDAP caratteristiche non è supportato:

* Riferimenti LDAP tra server (RFC 4511/4.1.10)

## <a name="create-a-new-connector"></a>Creare un nuovo connettore
tooCreate un connettore LDAP generico, in **servizio di sincronizzazione** selezionare **agente di gestione** e **crea**. Seleziona hello **LDAP generico (Microsoft)** connettore.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericldap/createconnector.png)

### <a name="connectivity"></a>Connettività
Nella pagina connettività hello, è necessario specificare hello Host, porta e informazioni di associazione. A seconda di quale associazione è selezionata, ulteriori informazioni potrebbero essere fornite nell'hello le sezioni seguenti.

![Connettività](./media/active-directory-aadconnectsync-connector-genericldap/connectivity.png)

* impostazione di Timeout della connessione di Hello viene utilizzata solo per il primo server di toohello connessione di hello quando vengono rilevati schema hello.
* Se il valore di Binding è Anonymous, non vengono usati né nome utente/password né il certificato.
* Per gli altri valori di Binding immettere le informazioni in nome utente/password o selezionare un certificato.
* Se si utilizza Kerberos tooauthenticate, quindi fornire anche hello dell'area di autenticazione o dominio dell'utente hello.

Hello **attributo alias** casella di testo viene utilizzata per gli attributi definiti nello schema di hello con sintassi RFC4522. Questi attributi non possono essere rilevati durante il rilevamento dello schema e hello connettore deve consentire tooidentify tali attributi. Ad esempio hello seguenti devono essere immessi in hello attributo alias casella toocorrectly identificare attributo userCertificate hello come un attributo binario.

`userCertificate;binary`

esempio Hello è un esempio di come questa configurazione potrebbe essere simile:

![Connettività](./media/active-directory-aadconnectsync-connector-genericldap/connectivityattributes.png)

Seleziona hello **includono attributi operativi nello schema** tooalso casella di controllo includono gli attributi creati dal server hello. Tra gli attributi, ad esempio quando l'oggetto hello è stato creato e ora dell'ultimo aggiornamento.

Selezionare **includono attributi estendibili nello schema** se vengono utilizzati gli oggetti estensibili (RFC4512/4.3) e l'abilitazione di questa opzione consente a toobe ogni attributo utilizzato in tutti gli oggetti. Se si seleziona questa opzione rende schema hello molto grandi in modo a meno che non utilizza directory connessa hello questa funzionalità hello si consiglia di opzione hello tookeep deselezionata.

### <a name="global-parameters"></a>Global Parameters
Nella pagina parametri globali hello, configurare funzionalità aggiuntive di LDAP e di registro delle modifiche delta toohello hello DN. pagina Hello è già popolato con informazioni hello fornite dai server LDAP hello.

![Connettività](./media/active-directory-aadconnectsync-connector-genericldap/globalparameters.png)

Nella sezione superiore Hello Mostra le informazioni fornite da server hello stesso, ad esempio nome hello del server di hello. Hello connettore verifica inoltre che i controlli obbligatorio hello siano presenti in hello DSE radice. Se questi controlli non sono elencati, viene visualizzato un avviso. Alcune directory LDAP non elencare tutte le funzioni hello DSE radice e è possibile che hello senza problemi di funzionamento del connettore anche se è presente un avviso.

Hello **supportati controlli** caselle di controllo controllano il comportamento di hello per alcune operazioni:

* Se si seleziona l'eliminazione di un albero, viene eliminata una gerarchia con una chiamata LDAP. Con l'opzione Elimina albero deselezionato, connettore hello non un'eliminazione ricorsiva se necessario.
* Con i risultati di paging selezionati, hello connettore non un'importazione di paging con dimensioni hello specificate in passaggi hello eseguire.
* Hello VLVControl e SortControl è un dati di tooread pagedResultsControl toohello alternativa dalla directory LDAP hello.
* Se tutte le opzioni disponibili (pagedResultsControl VLVControl e SortControl) sono deselezionate quindi hello connettore Importa tutti gli oggetti in un'unica operazione, che potrebbe non riuscire se è una directory di grandi dimensioni.
* ShowDeletedControl viene utilizzato solo quando il metodo di importazione Delta hello è USNChanged.

registro delle modifiche Hello DN è il contesto di denominazione hello utilizzato dal log delle modifiche delta hello, ad esempio **cn = changelog**. Questo valore deve essere specificato importazione delta toodo in grado di toobe.

Hello seguito è riportato un elenco di log di modifica predefinito DNs:

| Directory | Log delle modifiche delta |
| --- | --- |
| Microsoft AD LDS e Catalogo globale Active Directory |Rilevato automaticamente. USNChanged. |
| Apache Directory Server |Non disponibile. |
| Directory 389 |Log delle modifiche. Valore toouse predefinito: **cn = log delle modifiche** |
| IBM Tivoli DS |Log delle modifiche. Valore toouse predefinito: **cn = log delle modifiche** |
| Isode Directory |Log delle modifiche. Valore toouse predefinito: **cn = log delle modifiche** |
| Novell/NetIQ eDirectory |Non disponibile. TimeStamp. Hello connettore utilizza ultima data/ora aggiornate tooget aggiunti e aggiornati i record. |
| Open DJ/DS |Log delle modifiche.  Valore toouse predefinito: **cn = log delle modifiche** |
| Open LDAP |Log di accesso. Valore toouse predefinito: **cn = accesslog** |
| Oracle DSEE |Log delle modifiche. Valore toouse predefinito: **cn = log delle modifiche** |
| RadiantOne VDS |Directory virtuale. Dipende tooVDS directory connessa hello. |
| Sun One Directory Server |Log delle modifiche. Valore toouse predefinito: **cn = log delle modifiche** |

l'attributo password Hello è il nome di hello di hello attributo hello connettore deve utilizzare password hello tooset modifica della password e le operazioni di impostazione di password.
Questo valore è per impostazione predefinita impostato troppo**userPassword** ma può essere modificata quando sono necessari per un determinato sistema LDAP.

Nell'elenco partizioni aggiuntive hello è tooadd possibili spazi dei nomi aggiuntivi rilevati automaticamente. Ad esempio, questa impostazione può essere utilizzata se diversi server costituiscono un cluster logico, che deve essere importato in hello contemporaneamente. Come Active Directory può avere più domini in una foresta, ma tutti i domini di condividono uno schema, hello stesso può essere simulato immettendo hello altri spazi dei nomi in questa casella. Ogni spazio dei nomi è possibile importare da server diversi e viene ulteriormente configurata nella pagina Configura partizioni e gerarchie di hello. Utilizzare Ctrl + Invio tooget una nuova riga.

### <a name="configure-provisioning-hierarchy"></a>Configurare una gerarchia di provisioning
Questa pagina è toomap utilizzati hello DN componente, ad esempio unità Organizzativa, toohello tipo di oggetto che deve essere effettuato il provisioning, ad esempio organizationalUnit.

![Gerarchia di provisioning](./media/active-directory-aadconnectsync-connector-genericldap/provisioninghierarchy.png)

Configurando una gerarchia di provisioning, è possibile configurare hello connettore tooautomatically creare una struttura quando necessario. Ad esempio, se è presente un controller di dominio dello spazio dei nomi = contoso, dc = com e un nuovo oggetto cn = Joe, ou = Seattle, c = US, dc = contoso, dc = com viene eseguito il provisioning, quindi hello connettore è possibile creare un oggetto del paese di tipo per gli Stati Uniti e un'unità organizzativa per Seattle se non sono già presente nella directory hello.

### <a name="configure-partitions-and-hierarchies"></a>Configurare partizioni e gerarchie
Nella pagina partizioni e gerarchie hello selezionare tutti gli spazi dei nomi con oggetti Prevedi tooimport ed esportazione.

![Partitions](./media/active-directory-aadconnectsync-connector-genericldap/partitions.png)

Per ogni spazio dei nomi, è anche possibile tooconfigure le impostazioni di connettività che sostituirebbe valori hello specificati nella schermata di connettività hello. Se questi valori vengono lasciati tootheir immettere un valore vuoto, hello dalla schermata di connettività hello vengono utilizzate.

È inoltre possibile tooselect i contenitori e unità organizzative hello connettore deve importare ed esportare per.

Quando si esegue una ricerca di che questa operazione viene eseguita in tutti i contenitori nella partizione hello. Nei casi in cui sono presenti un numero elevato di contenitori di questo comportamento provoca una riduzione delle tooperformance.

>[!NOTE]
A partire da toohello di aggiornamento di marzo 2017 hello LDAP generico ricerche connettore possono essere limitate in contenitori di ambito tooonly hello selezionato. Questa operazione può essere eseguita selezionando la casella di controllo hello "Cerca solo nei contenitori selezionati" come illustrato nell'immagine di hello riportata di seguito.

![Eseguire la ricerca solo in contenitori selezionati](./media/active-directory-aadconnectsync-connector-genericldap/partitions-only-selected-containers.png)

### <a name="configure-anchors"></a>Configurare gli ancoraggi
Questa pagina ha  sempre un valore preconfigurato e non può essere modificato. Se è stato identificato fornitore hello del server, ancoraggio hello potrebbe essere popolato con un attributo non modificabile, hello esempio GUID per un oggetto. Se non è stata rilevata o se è noto toonot hanno un attributo non modificabile, quindi il connettore di hello utilizza nome distinto (DN) del punto di ancoraggio hello.

![ancoraggi](./media/active-directory-aadconnectsync-connector-genericldap/anchors.png)


di seguito Hello è un elenco di server LDAP e ancoraggio hello in uso:

| Directory | Attributo di ancoraggio |
| --- | --- |
| Microsoft AD LDS e Catalogo globale Active Directory |objectGUID |
| 389 Directory Server |dn |
| Apache Directory |dn |
| IBM Tivoli DS |dn |
| Isode Directory |dn |
| Novell/NetIQ eDirectory |GUID |
| Open DJ/DS |dn |
| Open LDAP |dn |
| Oracle ODSEE |dn |
| RadiantOne VDS |dn |
| Sun One Directory Server |dn |

## <a name="other-notes"></a>Altre note
In questa sezione fornisce informazioni di aspetti specifici toothis connettore o per altri motivi tooknow importanti.

### <a name="delta-import"></a>Importazione delta
filigrana delta Hello in LDAP Open è data/ora UTC. Per questo motivo, gli orologi di hello tra il servizio di sincronizzazione FIM e hello aprire LDAP devono essere sincronizzati. In caso contrario, potrebbero essere omesse alcune voci nel log delle modifiche delta hello.

Per Novell eDirectory, importazione delta hello è rilevate non elimina qualsiasi oggetto. Per questo motivo, è necessario toorun una procedura completa di importare periodicamente gli oggetti eliminati toofind tutti.

Per le directory con un delta log basato su data e ora di modifica, è altamente consigliabile toorun un'importazione completa in periodici momenti. Questo processo consente toofind motore di sincronizzazione hello e dissimilarities tra server LDAP hello e novità nello spazio connettore hello.

## <a name="troubleshooting"></a>Risoluzione dei problemi
* Per informazioni su come tootroubleshoot tooenable registrazione hello connettore, vedere hello [come tooEnable traccia ETW per i connettori](http://go.microsoft.com/fwlink/?LinkId=335731).
