---
title: Guida alla protezione di archiviazione aaaAzure | Documenti Microsoft
description: Dettagli hello molti metodi di sicurezza di archiviazione di Azure, inclusi, a titolo esemplificativo, tooRBAC, la crittografia del servizio di archiviazione, crittografia lato Client, SMB 3.0 e crittografia del disco di Azure.
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 6f931d94-ef5a-44c6-b1d9-8a3c9c327fb2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: d406ff0d6b45c6107d0276ad9e65c331078ce792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-guide"></a>Guida alla sicurezza di Archiviazione di Azure
## <a name="overview"></a>Panoramica
Archiviazione di Azure fornisce un set completo di funzionalità di sicurezza che insieme consentono agli sviluppatori di applicazioni sicure toobuild. account di archiviazione Hello stesso può essere protetto tramite controllo di accesso basato sui ruoli e Azure Active Directory. È possibile proteggere i dati in transito tra un'applicazione e Azure usando la [crittografia lato client](storage-client-side-encryption.md), HTTPS o SMB 3.0. Dati possono essere impostati toobe crittografato automaticamente quando scritto utilizzando archiviazione tooAzure [crittografia del servizio di archiviazione (SSE)](storage-service-encryption.md). I dischi del sistema operativo e i dati utilizzati dalle macchine virtuali possono essere impostati toobe crittografati utilizzando [crittografia del disco Azure](../security/azure-security-disk-encryption.md). È possono concedere l'accesso delegato toohello dati oggetti nell'archiviazione di Azure utilizzando [firme di accesso condiviso](storage-dotnet-shared-access-signature-part-1.md).

Questo articolo include una panoramica di ognuna di queste funzionalità di sicurezza che possono essere usate con Archiviazione di Azure. Vengono forniti i collegamenti tooarticles in grado di offrire dettagli di ogni funzionalità in modo da poter facilmente ulteriori indagini condotte su ogni argomento.

Di seguito sono illustrate in questo articolo di hello argomenti toobe:

* [Sicurezza del piano di gestione](#management-plane-security) : proteggere l'account di archiviazione

  il piano di gestione di Hello è costituito da toomanage le risorse usate hello account di archiviazione. In questa sezione verrà descritto come modello di distribuzione Azure Resource Manager hello e modalità di accesso di account di archiviazione tooyour toouse toocontrol di controllo di accesso basato sui ruoli (RBAC). Verranno inoltre presentati gestire le chiavi di account di archiviazione e come tooregenerate li.
* [Piano di sicurezza dei dati](#data-plane-security) – tooYour protezione dell'accesso ai dati

  In questa sezione verrà esaminato consentire l'accesso agli oggetti di dati effettivi di toohello nell'account di archiviazione, ad esempio BLOB, file, code e tabelle, tramite firme di accesso condiviso e criteri di accesso archiviati. Vengono trattate anche le firme di accesso condiviso sia a livello di servizio che di account. Si noterà anche come toolimit accedere tooa specifico indirizzo IP (o un intervallo di indirizzi IP), come protocollo di hello toolimit utilizzato tooHTTPS e come toorevoke una firma di accesso condiviso senza attendere che tooexpire.
* [Crittografia in transito](#encryption-in-transit)

  Questa sezione viene descritto come toosecure dati durante il trasferimento da o verso l'archiviazione di Azure. Parleremo hello consigliato l'utilizzo della crittografia hello e HTTPS utilizzata da SMB 3.0 per condivisioni File di Azure. È inoltre verrà dare un'occhiata crittografia lato Client, che consentono di tooencrypt hello prima di essere trasferiti nell'account di archiviazione in un'applicazione client e toodecrypt hello dati dopo che viene trasferita all'esterno di archiviazione.
* [Crittografia di dati inattivi](#encryption-at-rest)

  Si parlerà crittografia del servizio di archiviazione (SSE) e come è possibile abilitare la funzionalità per un account di archiviazione, pertanto i BLOB in blocchi, BLOB di pagine e aggiungere BLOB viene crittografato automaticamente quando scritti tooAzure archiviazione. Verranno inoltre esaminati come è possibile utilizzare la crittografia del disco di Azure e analizzare le differenze di base hello e casi di crittografia del disco e SSE e crittografia lato Client. Si esaminerà brevemente la conformità FIPS per i computer del Governo degli Stati Uniti.
* Utilizzando [archiviazione Analitica](#storage-analytics) tooaudit accesso di archiviazione di Azure

  Questa sezione illustra come informazioni di toofind in analitica archiviazione hello log per una richiesta. Verrà dare un'occhiata analitica archiviazione reale dati di log e vedere come toodiscern se viene effettuata una richiesta con hello archiviazione chiave, con una firma di accesso condiviso, account o in modo anonimo e se l'esito positivo o non è riuscita.
* [Abilitazione dei client basati su browser tramite CORS](#Cross-Origin-Resource-Sharing-CORS)

  In questa sezione si indica come risorse di tooallow multiorigine (CORS) di condivisione. Parleremo accesso tra domini, e come toohandle con funzionalità CORS hello compilata nell'archiviazione di Azure.

## <a name="management-plane-security"></a>Sicurezza del piano di gestione
il piano di gestione di Hello è costituita da operazioni che influiscono sull'account di archiviazione hello stesso. Ad esempio, è possibile creare o eliminare un account di archiviazione, ottenere un elenco di account di archiviazione in una sottoscrizione, recuperare chiavi dell'account di archiviazione hello o rigenerare chiavi di account di archiviazione hello.

Quando si crea un nuovo account di archiviazione, si seleziona un modello di distribuzione classica o di Azure Resource Manager. il modello classico Hello di creazione di risorse in Azure consente solo di sottoscrizione toohello accesso radicale e hello a sua volta, l'account di archiviazione.

Questa guida è incentrata sul modello di gestione delle risorse hello è hello consigliato mezzi per la creazione di account di archiviazione. Con gli account di archiviazione di gestione risorse di hello, invece che la sottoscrizione intera toohello accesso, è possibile controllare l'accesso su un piano di gestione toohello di livello più limitato tramite controllo di accesso basato sui ruoli (RBAC).

### <a name="how-toosecure-your-storage-account-with-role-based-access-control-rbac"></a>Come toosecure account di archiviazione con il controllo di accesso basato sui ruoli (RBAC)
Viene ora spiegato cos'è il controllo degli accessi in base al ruolo e come usarlo. Ogni sottoscrizione di Azure è associata a un'istanza di Azure Active Directory. Gli utenti, gruppi e applicazioni da tale directory possono essere concesse le risorse di toomanage accesso hello sottoscrizione di Azure che utilizzano modelli di distribuzione di gestione risorse hello. Si tratta di cui viene fatto riferimento tooas controllo di accesso basato sui ruoli (RBAC). toomanage accedere a questo, è possibile utilizzare hello [portale di Azure](https://portal.azure.com/), hello [strumenti di Azure CLI](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), o hello [API di REST di Provider di risorse di archiviazione di Azure ](https://msdn.microsoft.com/library/azure/mt163683.aspx).

Con il modello di gestione risorse hello, inserire l'account di archiviazione hello in una risorsa gruppo e controllo accesso toohello piano di gestione di account di archiviazione specifico tramite Azure Active Directory. Ad esempio, è possibile assegnare utenti specifici hello possibilità tooaccess hello chiavi account di archiviazione, mentre altri utenti possono visualizzare le informazioni sull'account di archiviazione hello, ma non è possibile accedere alle chiavi dell'account di archiviazione hello.

#### <a name="granting-access"></a>Concessione dell'accesso
Assegnando hello appropriato RBAC ruolo toousers, gruppi e applicazioni, nell'ambito corretto hello è concesso l'accesso. toogrant accesso toohello intera sottoscrizione, si assegna un ruolo a livello di sottoscrizione hello. È possibile concedere accesso tooall delle risorse di hello in un gruppo di risorse tramite la concessione di autorizzazioni toohello risorse gruppo. È inoltre possibile assegnare ruoli specifici toospecific risorse, ad esempio gli account di archiviazione.

Di seguito sono punti di hello principali che è necessario tooknow sull'utilizzo RBAC tooaccess hello le operazioni di gestione di un account di archiviazione di Azure:

* Quando si assegna l'accesso, è fondamentalmente assegnare un account di toohello di ruolo che si vuole toohave accesso. È possibile controllare l'accesso toohello operazioni toomanage tale account di archiviazione, ma non i dati toohello oggetti nell'account hello. Ad esempio, è possibile concedere l'autorizzazione proprietà hello tooretrieve dell'account di archiviazione di hello (ad esempio ridondanza), ma non tooa contenitore o dati all'interno di un contenitore all'interno dell'archiviazione Blob.
* Per un utente toohave autorizzazione tooaccess hello oggetti dati nell'account di archiviazione hello, è possibile assegnare le chiavi di account di archiviazione di autorizzazione tooread hello e tale utente può quindi utilizzare tali chiavi tooaccess hello BLOB, code, tabelle e i file.
* I ruoli possono essere assegnati tooa specifico account utente, un gruppo di utenti o tooa specifica applicazione.
* Per ogni ruolo è disponibile un elenco di azioni e non azioni. Ad esempio, il ruolo di collaboratore alla macchina virtuale hello ha un'azione di "elenco chiavi del" che consente di leggere hello storage account chiavi toobe. Hello Collaboratore dispone di "Non azioni", come l'aggiornamento di access hello per gli utenti hello Active Directory.
* Ruoli per l'archiviazione includono (ma non sono limitati a) seguente hello:

  * Proprietario: può gestire qualsiasi elemento, compreso l'accesso.
  * Collaboratore – è possibile eseguire alcuna operazione proprietario hello possibile tranne che assegna l'accesso. Un utente con questo ruolo può visualizzare e rigenerare chiavi di account di archiviazione hello. Con chiavi di account di archiviazione hello, possono accedere gli oggetti dati hello.
  * Lettore – possono visualizzare informazioni sull'account di archiviazione hello, tranne i segreti. Ad esempio, se si assegna un ruolo con autorizzazioni di lettura sul toosomeone account di archiviazione hello, possono visualizzare le proprietà di hello hello dell'account di archiviazione, ma non può apportare modifiche di proprietà toohello né visualizzare chiavi dell'account di archiviazione hello.
  * Collaboratore di Account di archiviazione: possano gestire account di archiviazione hello: possono leggere hello gruppi di risorse della sottoscrizione e risorse, creare e gestire le distribuzioni gruppo di risorse di sottoscrizione. Che può accedere anche alle chiavi dell'account archiviazione hello, che a sua volta significa che poter accedere piano dati hello.
  * Amministratore di accesso utente: possono gestire account di archiviazione toohello accesso utente. Ad esempio, possono concedere utente specifico tooa accesso di lettura.
  * Macchina virtuale collaboratore – possono gestire le macchine virtuali ma non hello storage account toowhich che sono connessi. Questo ruolo è possibile elencare chiavi dell'account di archiviazione hello, che significa che hello toowhom utente assegnare questo ruolo è possibile aggiornare piano dati hello.

    Affinché un toocreate utente una macchina virtuale, hanno toobe toocreate in grado di hello corrispondente file VHD in un account di archiviazione. toodo, necessità di archiviazione di hello in grado di tooretrieve toobe chiave account e passare l'API toohello hello VM di creazione. Pertanto, devono avere l'autorizzazione in modo che l'elenco di chiavi dell'account di archiviazione hello.
* ruoli personalizzati toodefine possibilità di Hello è una funzionalità che consente di toocompose un set di azioni da un elenco di azioni disponibili che possono essere eseguite su risorse di Azure.
* utente Hello è toobe configurare Azure Active Directory prima di poter assegnare toothem un ruolo.
* È possibile creare un report che ha concesso o revocato il tipo di accesso e a/da cui l'ambito di utilizzo di PowerShell o hello CLI di Azure.

#### <a name="resources"></a>Risorse
* [Controllo degli accessi in base al ruolo di Azure Active Directory](../active-directory/role-based-access-control-configure.md)

  Questo articolo spiega hello controllo di accesso basato sui ruoli di Azure Active Directory e il relativo funzionamento.
* [Controllo degli accessi in base al ruolo: Ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md)

  In questo articolo illustra in dettaglio tutti i ruoli predefiniti hello disponibili in RBAC.
* [Comprendere la distribuzione di Gestione delle risorse e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md)

  In questo articolo illustra la distribuzione di gestione risorse di hello e modelli di distribuzione classica e spiega hello vantaggi dell'utilizzo di gruppi di gestione risorse e risorse hello. Descrive il modo hello calcolo di Azure, rete e i provider di archiviazione nel modello di gestione risorse di hello.
* [Controllo degli accessi basato sui ruoli con hello API REST di gestione](../active-directory/role-based-access-control-manage-access-rest.md)

  Questo articolo illustra come toouse hello toomanage API REST sui ruoli.
* [Informazioni di riferimento sulle API REST del provider di risorse di archiviazione di Azure](https://msdn.microsoft.com/library/azure/mt163683.aspx)

  Si tratta di riferimento di hello per le API che è possibile utilizzare toomanage account di archiviazione a livello di codice hello.
* [Tooauth Guida per gli sviluppatori con API di gestione risorse di Azure](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)

  Questo articolo viene illustrato come tramite tooauthenticate hello le API di gestione risorse.
* [Controllo degli accessi in base al ruolo per Microsoft Azure da Ignite](https://channel9.msdn.com/events/Ignite/2015/BRK2707)

  Si tratta di un video su Channel 9 conferenza Ignite 2015 MS hello tooa di collegamento. In questa sessione, si parla di accedere alle funzionalità di reporting in Azure e gestione e l'esplorazione di procedure consigliate per la protezione dell'accesso tooAzure sottoscrizioni tramite Azure Active Directory.

### <a name="managing-your-storage-account-keys"></a>Rigenerazione delle chiavi dell'account di archiviazione
Account di archiviazione chiavi sono stringhe a 512 bit create da Azure che, insieme ai archiviazione hello, nome dell'account può essere tooaccess utilizzati hello dati archiviati nell'account di archiviazione hello, ad esempio BLOB, le entità all'interno di una tabella, i messaggi in coda e i file in una condivisione di File di Azure. Controlli di chiavi di controllo dell'accesso toohello archiviazione account di accesso piano dati toohello per tale account di archiviazione.

Ogni account di archiviazione dispone di due chiavi di cui tooas "Chiave 1" e "Chiave 2" in hello [portale di Azure](http://portal.azure.com/) e hello i cmdlet di PowerShell. Questi possono essere rigenerati manualmente utilizzando uno dei diversi metodi, inclusi, ma non limitata toousing hello [portale di Azure](https://portal.azure.com/), PowerShell, hello CLI di Azure o a livello di programmazione utilizzando hello libreria Client di archiviazione .NET o hello Azure API REST di servizi di archiviazione.

Esistono vari motivi tooregenerate le chiavi di account di archiviazione.

* Si possono rigenerarle a intervalli regolari per motivi di sicurezza.
* Si si rigenerano le chiavi di account di archiviazione se un utente gestito toohack in un'applicazione e recuperare chiave hello hardcoded o salvato in un file di configurazione, agli account di archiviazione tooyour accesso completo.
* Un altro caso di rigenerazione della chiave è se il team utilizza un'applicazione di esplorazione dell'archiviazione che mantiene una chiave dell'account di archiviazione hello e uno dei membri del team hello lascia. un'applicazione Hello continuerebbe toowork, agli account di archiviazione tooyour accesso dopo che sia troppo tardi. Questa è effettivamente hello principalmente che sono create firme di accesso condiviso a livello di account, è possibile utilizzare una firma di accesso condiviso a livello di account anziché l'archiviazione delle chiavi di accesso di hello in un file di configurazione.

#### <a name="key-regeneration-plan"></a>Piano di rigenerazione delle chiavi
Non si desidera chiave rigenerare hello toojust in uso senza una pianificazione. Se a tale scopo, è stato troncato tutti toothat storage account di accesso, che possono causare problemi principali. È per questo motivo che sono disponibili due chiavi ed è consigliabile rigenerarne una alla volta.

Prima di rigenerare le chiavi, assicurarsi di disporre di un elenco di tutte le applicazioni che dipendono da account di archiviazione hello, nonché tutti gli altri servizi in uso in Azure. Ad esempio, se si utilizza servizi multimediali di Azure che dipendono da account di archiviazione, è necessario risincronizzare le chiavi di accesso hello con il servizio multimediale dopo aver rigenerato la chiave hello. Se si utilizza tutte le applicazioni, ad esempio l'esplorazione dell'archiviazione, è necessario tooprovide hello nuove chiavi toothose applicazioni nonché. Si noti che se si dispone di macchine virtuali i cui file VHD vengono archiviati nell'account di archiviazione hello, non verrà influenzato da la rigenerazione delle chiavi dell'account di archiviazione hello.

È possibile rigenerare le chiavi di hello portale di Azure. Una volta che le chiavi vengono rigenerate possibile occupino too10 toobe minuti sincronizzati tra servizi di archiviazione.

Quando si è pronti, ecco processo generale di hello che riporta in dettaglio come si deve modificare la chiave. In questo caso, presupposto hello è che 1 chiave attualmente in uso e si sta toochange tutto toouse chiave invece di 2.

1. Rigenerare tooensure chiave 2 è sicuro. È possibile farlo in hello portale di Azure.
2. In tutte le applicazioni di hello in cui è archiviata la chiave di archiviazione hello, modificare il nuovo valore hello archiviazione toouse chiave chiave 2. Verificare e pubblicare un'applicazione hello.
3. Dopo che tutti di hello applicazioni e servizi siano e in esecuzione correttamente, rigenerare la chiave 1. In questo modo, chiunque toowhom non espressamente hanno nuova chiave hello non sarà più possibile accedere toohello account di archiviazione.

Se si utilizza attualmente 2 di chiave, è possibile utilizzare hello stessa procedura, ma i nomi delle chiavi di hello inversa.

È possibile eseguire la migrazione in un paio di giorni, ogni toouse hello nuovo tasto di modifica e la sua pubblicazione. Dopo tutti gli elementi, è necessario tornare indietro e rigenerare la chiave precedente hello in modo non funziona più.

Un'altra opzione consiste chiave account di archiviazione tooput hello in un [insieme credenziali chiavi Azure](https://azure.microsoft.com/services/key-vault/) come una chiave privata e dispone della chiave di hello recuperare di applicazioni da qui. Quando si rigenera la chiave hello e aggiorna hello insieme di credenziali chiave di Azure, quindi applicazioni hello non necessario toobe ridistribuito perché si selezionerà hello nuova chiave dall'insieme di credenziali chiave di Azure hello automaticamente. Si noti che è possibile disporre di un'applicazione hello leggere chiave hello ogni volta che è necessario, è possibile memorizzarlo nella cache in memoria e in caso di errore quando si utilizza, recuperare nuovamente chiave hello dal hello insieme credenziali chiavi Azure.

L'uso dell'insieme di credenziali delle chiavi di Azure aggiunge anche un altro livello di sicurezza per le chiavi di archiviazione. Se si utilizza questo metodo, che non è hardcoded chiave di archiviazione hello in un file di configurazione, che rimuove tale via di qualcuno riesca ad accedere chiavi toohello senza autorizzazione specifica.

Un altro vantaggio dell'utilizzo dell'insieme di credenziali chiave di Azure è che è inoltre possibile controllare le chiavi tooyour accesso tramite Azure Active Directory. Ciò significa che è possibile concedere alcuni toohello accesso delle applicazioni che necessitano di chiavi hello tooretrieve dall'insieme di credenziali chiave di Azure e sapere che altre applicazioni non saranno in grado di tooaccess le chiavi di hello senza concedere loro autorizzazioni in modo specifico.

Nota: è consigliabile toouse solo uno di hello chiavi in tutte le applicazioni in hello stesso tempo. Se si utilizza chiave 1 in alcune occasioni e 2 di chiave in altri, è necessario non essere in grado di toorotate delle chiavi senza un'applicazione di perdere l'accesso.

#### <a name="resources"></a>Risorse
* [Informazioni sugli account di archiviazione di Azure](storage-create-storage-account.md#regenerate-storage-access-keys)

  Questo articolo fornisce una panoramica degli account di archiviazione e illustra le operazioni di visualizzazione, copia e rigenerazione delle chiavi di accesso alle risorse di archiviazione.
* [Informazioni di riferimento sulle API REST del provider di risorse di archiviazione di Azure](https://msdn.microsoft.com/library/mt163683.aspx)

  Questo articolo contiene collegamenti toospecific di articoli sulle durante il recupero delle chiavi dell'account di archiviazione hello e la rigenerazione della chiavi dell'account di archiviazione hello per un Account di Azure mediante hello API REST. Nota: quanto detto vale per gli account di archiviazione di Resource Manager.
* [Operazioni sugli account di archiviazione](https://msdn.microsoft.com/library/ee460790.aspx)

  Questo articolo in Gestione servizi di archiviazione REST API Reference hello contiene articoli toospecific collegamenti sul recupero e la rigenerazione delle chiavi dell'account di archiviazione hello utilizzando hello API REST. Nota: Questa è per gli account di archiviazione di hello classica.
* [Ad esempio Gestione tookey goodbye: gestire i dati di archiviazione tooAzure accesso tramite Azure AD](http://www.dushyantgill.com/blog/2015/04/26/say-goodbye-to-key-management-manage-access-to-azure-storage-data-using-azure-ad/)

  Questo articolo illustra come toouse Active Directory toocontrol tooyour le chiavi di archiviazione di Azure nell'insieme di credenziali chiave di Azure di accesso. Viene inoltre illustrato come un'automazione di Azure toouse processo chiavi hello tooregenerate su base oraria.

## <a name="data-plane-security"></a>Sicurezza del piano dati
Piano di sicurezza dei dati fa riferimento a metodi toohello gli oggetti dati di hello toosecure utilizzati archiviati in archiviazione di Azure, file, code, tabelle e BLOB hello. Abbiamo visto metodi tooencrypt hello dati e sicurezza durante il transito dei dati di hello, ma come procedere per informazioni su come consentire l'accesso toohello oggetti?

Esistono due metodi per controllare gli oggetti dati toohello accesso autonomamente. da chiavi account di archiviazione toohello di controllo dell'accesso per primo è Hello e hello secondo utilizza gli oggetti dati toospecific di firme di accesso condiviso toogrant accesso per un periodo di tempo specifico.

Un'eccezione toonote è che è possibile consentire l'accesso pubblico tooyour BLOB impostando il livello di accesso hello per hello contenitore di BLOB hello di conseguenza. Se si imposta l'accesso per un contenitore tooBlob o il contenitore, sarà possibile l'accesso in lettura pubblico per i BLOB hello in tale contenitore. Ciò significa che qualsiasi utente con un URL che punta tooa blob presenti nel contenitore può aprire in un browser senza utilizzare una firma di accesso condiviso o disporre di chiavi di account di archiviazione hello.

### <a name="storage-account-keys"></a>Chiavi dell'account di archiviazione
Chiavi dell'account di archiviazione sono stringhe a 512 bit create da Azure che, insieme a nome di account di archiviazione hello, può essere tooaccess utilizzato hello dati archiviati nell'account di archiviazione hello.

Ad esempio, è possibile leggere i BLOB, scrivere tooqueues, creare tabelle e modificare file. Molte di queste azioni possono essere eseguite tramite hello Azure portal o utilizzando una delle numerose applicazioni di esplorazione dell'archiviazione. È anche possibile scrivere hello toouse codice API REST o uno dei hello le librerie Client di archiviazione tooperform queste operazioni.

Come illustrato nella sezione hello in hello [gestione piano di sicurezza](#management-plane-security), le chiavi di archiviazione toohello di accesso per un account di archiviazione classico può essere concesse fornendo accesso completo toohello sottoscrizione di Azure. È possibile controllare le chiavi di archiviazione toohello di accesso per un account di archiviazione utilizzando il modello di gestione risorse di Azure hello con il controllo dell'accesso basato sui ruoli (RBAC).

### <a name="how-toodelegate-access-tooobjects-in-your-account-using-shared-access-signatures-and-stored-access-policies"></a>Modalità di accesso tooobjects nell'account di utilizzo di firme di accesso condiviso e criteri di accesso archiviati toodelegate
Una firma di accesso condiviso è una stringa contenente un token di sicurezza che può essere collegati tooa URI che consente di accedere a toodelegate toostorage oggetti e specificare i vincoli, ad esempio le autorizzazioni di hello e hello un intervallo di data/ora di accesso.

È possibile concedere accesso tooblobs, contenitori, messaggi in coda, file e tabelle. Con le tabelle, è possibile effettivamente concedere autorizzazioni tooaccess un intervallo di entità nella tabella hello specificando hello riga e partizione intervalli di chiavi toowhich si desidera l'accesso utente toohave hello. Ad esempio, se si dispone di dati archiviati con una chiave di partizione dello stato geografica, si potrebbe concedere a un utente hello toojust di accedere ai dati della California.

In un altro esempio, potrebbe fornire un token di firma di accesso condiviso che consente a tale coda tooa di toowrite le voci di un'applicazione web e assegnare un processo di lavoro applicazione ruolo un messaggi tooget token SAS da hello coda e li elaborano. Oppure si può fornire un token di firma di accesso condiviso possono utilizzare contenitore tooa di immagini tooupload nell'archiviazione Blob e assegnare un tooread di autorizzazione dell'applicazione web di tali immagini a un cliente. In entrambi i casi, c'è una separazione delle problematiche: ogni applicazione è possibile assegnare solo hello di accesso necessario in ordine tooperform relativa attività. Questo è possibile tramite l'utilizzo di hello di firme di accesso condiviso.

#### <a name="why-you-want-toouse-shared-access-signatures"></a>Motivo per cui si desidera toouse firme di accesso condiviso
Perché è consigliabile toouse una firma di accesso condiviso anziché assegnare solo la chiave di account di archiviazione, è pertanto molto più semplice? Assegnare la chiave di account di archiviazione è simile a chiavi hello del unito archiviazione di condivisione. infatti concede l'accesso completo. È Impossibile usare le chiavi e caricare il proprio account di archiviazione di tutta la libreria tooyour. Può anche sostituire i file con versioni infette da virus o rubare i dati. Fornire account di accesso illimitato tooyour archiviazione è un elemento che non deve essere sottovalutare.

Con firme di accesso condiviso, è possibile assegnare un client solo le autorizzazioni di hello necessarie per un periodo di tempo limitato. Ad esempio, se un utente è il caricamento di un account tooyour blob, è possibile concedere loro l'accesso in scrittura per il blob di hello tooupload sufficiente tempo (in base alle dimensioni di hello del blob hello, naturalmente). Se si cambia idea, è possibile revocare l'accesso.

Inoltre, è possibile specificare che le richieste effettuate utilizzando una firma di accesso condiviso sono limitata tooa determinato tooAzure esterno intervallo di indirizzi IP o l'indirizzo IP. Si può anche specificare che le richieste devono essere eseguite con un protocollo specifico (HTTPS o HTTP/HTTPS). Ciò significa che se si desidera solo il traffico HTTPS tooallow, è possibile impostare hello necessario protocollo tooHTTPS solo e verrà bloccato il traffico HTTP.

#### <a name="definition-of-a-shared-access-signature"></a>Definizione di firma di accesso condiviso
Una firma di accesso condiviso è che un set di parametri di query aggiunto toohello URL che punta alla risorsa hello

che fornisce informazioni sull'accesso hello consentiti e hello periodo di tempo per cui hello è consentito l'accesso. Di seguito è riportato un esempio; Questo URI fornisce l'accesso in lettura tooa blob per cinque minuti. Si noti che i parametri di query della firma di accesso condiviso devono essere con codifica URL, ad esempio %3A per due punti (:) o %20 per lo spazio.

```
http://mystorage.blob.core.windows.net/mycontainer/myblob.txt (URL toohello blob)
?sv=2015-04-05 (storage service version)
&st=2015-12-10T22%3A18%3A26Z (start time, in UTC time and URL encoded)
&se=2015-12-10T22%3A23%3A26Z (end time, in UTC time and URL encoded)
&sr=b (resource is a blob)
&sp=r (read access)
&sip=168.1.5.60-168.1.5.70 (requests can only come from this range of IP addresses)
&spr=https (only allow HTTPS requests)
&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D (signature used for hello authentication of hello SAS)
```

#### <a name="how-hello-shared-access-signature-is-authenticated-by-hello-azure-storage-service"></a>Come hello firma di accesso condiviso è stata autenticata da hello il servizio di archiviazione di Azure
Quando il servizio di archiviazione hello riceve una richiesta di hello, accetta parametri di query di input hello e viene creata una firma utilizzando hello stesso metodo come hello programma chiamante. Consente quindi di confrontare due firme hello. Se si accetta, hello servizio di archiviazione è possibile verificare che sia valido toomake versione Servizio archiviazione hello, verificare che hello data e ora correnti all'interno di finestra specificato hello, verificare che accesso hello richiesto corrisponde toohello richiesta effettuata e così via.

Ad esempio, con l'URL precedente, se URL hello riferimento tooa file anziché un blob, la richiesta avrà esito negativo perché specifica tale hello che firma di accesso condiviso è per un blob. Se hello comando REST chiamato tooupdate un blob, avrà esito negativo perché hello firma di accesso condiviso consente di specificare che è consentito solo l'accesso in lettura.

#### <a name="types-of-shared-access-signatures"></a>Tipi di firme di accesso condiviso
* Una firma di accesso condiviso a livello di servizio può essere utilizzato tooaccess risorse specifiche in un account di archiviazione. Alcuni esempi di questo recuperato un elenco di BLOB in un contenitore, il download di un blob, aggiornamento di un'entità in una tabella, aggiunta tooa coda dei messaggi o caricamento di una condivisione di file tooa file.
* Una firma di accesso condiviso a livello di account può essere utilizzato tooaccess tutto ciò che può essere utilizzato una firma di accesso condiviso a livello di servizio per. Inoltre, può fornire tooresources opzioni che non sono consentite con una firma di accesso condiviso a livello di servizio, ad esempio hello possibilità toocreate contenitori, tabelle, code e le condivisioni di file. È anche possibile specificare toomultiple di access services in una sola volta. Ad esempio, è possibile assegnare un utente tooboth Accedi ai BLOB e i file nell'account di archiviazione.

#### <a name="creating-an-sas-uri"></a>Creazione di un URI di firma di accesso condiviso
1. È possibile creare un URI ad hoc su richiesta, definire tutti i parametri di query hello ogni volta.

   Questo approccio è molto flessibile, ma se è disponibile un set logico di parametri simili ogni volta, l'uso di criteri di accesso archiviati è preferibile.
2. È possibile creare criteri di accesso archiviati per un intero contenitore, una condivisione file, una tabella o una coda, Quindi è possibile utilizzare questo come base hello per hello crei gli URI di firma di accesso condiviso. Le autorizzazioni basate su criteri di accesso archiviati possono essere revocate facilmente. È possibile disporre di criteri too5 definiti in ogni contenitore, coda, tabella o una condivisione di backup.

   Ad esempio, se si prevede di toohave molte persone leggono BLOB hello in un contenitore specifico, è possibile creare un criterio di accesso archiviati che afferma "concedere l'accesso in lettura" e tutte le altre impostazioni che saranno hello stesso ogni volta. È quindi possibile creare un URI SAS utilizzando hello impostazioni di criteri di accesso archiviato hello e specificando hello data/ora di scadenza. Hello questo vantaggio è che non è necessario toospecify tutti hello parametri di query ogni volta.

#### <a name="revocation"></a>Revoca
Si supponga che sia stata compromessa la firma di accesso condiviso o si desidera toochange, a causa di requisiti normativi o di sicurezza aziendali. Come revocare l'accesso tooa risorsa utilizzando tale firma di accesso condiviso Dipende dal modo creato hello URI SAS.

Se si usa un URI ad hoc, sono disponibili tre opzioni. È possibile rilasciare token di firma di accesso condiviso con criteri di scadenza breve e attendere semplicemente tooexpire SAS hello. È possibile rinominare o eliminare la risorsa hello (supponendo che il token hello sia singolo oggetto con ambito tooa). È possibile modificare chiavi dell'account di archiviazione hello. Quest'ultima opzione può avere un impatto di grandi dimensioni, a seconda di quanti servizi utilizza tale account di archiviazione e probabilmente non è un elemento da toodo senza una pianificazione.

Se si utilizza una firma di accesso condiviso derivato da un criterio di accesso archiviati, è possibile rimuovere l'accesso revocando hello i criteri di accesso archiviato – è possibile modificare solo in modo che è già scaduta o rimuoverlo completamente. Questa operazione ha effetto immediato e invalida qualsiasi firma di accesso condiviso creata con tali criteri di accesso archiviati. L'aggiornamento o rimozione di hello criterio di accesso archiviato può influire sulle persone l'accesso a tale contenitore specifico, una condivisione file, una tabella o coda tramite firma di accesso condiviso, ma se hello client vengono scritti in modo che lo richiedono una nuova firma di accesso condiviso quando hello precedente diventa non valido, questo funzionerà correttamente.

Poiché l'utilizzo di una SAS derivata da un criterio di accesso archiviato offre toorevoke possibilità hello che firma di accesso condiviso immediatamente, è hello consigliata best practice tooalways utilizzare criteri di accesso archiviati quando possibile.

#### <a name="resources"></a>Risorse
Per informazioni più dettagliate sull'uso di firme di accesso condiviso e archiviati i criteri di accesso, vengono forniti esempi, fare riferimento toohello seguenti articoli:

* Questi sono gli articoli di riferimento hello.

  * [Firma di accesso condiviso del servizio.](https://msdn.microsoft.com/library/dn140256.aspx)

    Questo articolo fornisce esempi dell'uso di una firma di accesso condiviso a livello di servizio con BLOB, messaggi della coda, intervalli di tabelle e file.
  * [Creazione di una firma di accesso condiviso del servizio](https://msdn.microsoft.com/library/dn140255.aspx)
  * [Creazione di una firma di accesso condiviso dell'account](https://msdn.microsoft.com/library/mt584140.aspx)
* Si tratta di esercitazioni per l'utilizzo di hello .NET client libreria toocreate firme di accesso condiviso e criteri di accesso archiviati.

  * [Uso delle firme di accesso condiviso](storage-dotnet-shared-access-signature-part-1.md)
  * [Condiviso firme di accesso, parte 2: Creare e utilizzare una firma di accesso condiviso con hello servizio Blob](storage-dotnet-shared-access-signature-part-2.md)

    In questo articolo include una spiegazione del modello di firma di accesso condiviso hello, esempi di firme di accesso condiviso e indicazioni per la procedura consigliata hello di firma di accesso condiviso. Inoltre descritti è revoca hello di autorizzazione di hello.
* Limitazione dell'accesso con un indirizzo IP (ACL IP)

  * [Che cos'è un elenco di controllo di accesso (ACL) di endpoint?](../virtual-network/virtual-networks-acl.md)
  * [Creazione di una firma di accesso condiviso del servizio](https://msdn.microsoft.com/library/azure/dn140255.aspx)

    Si tratta di articolo di riferimento hello per la firma di accesso condiviso a livello di servizio; include un esempio di ACLing IP.
  * [Creazione di una firma di accesso condiviso dell'account](https://msdn.microsoft.com/library/azure/mt584140.aspx)

    Si tratta di articolo di riferimento hello per la firma di accesso condiviso a livello di account; include un esempio di ACLing IP.
* Autenticazione

  * [Autenticazione per hello servizi di archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* Esercitazione introduttiva sulle firme di accesso condiviso

  * [Esercitazione introduttiva sulle firme di accesso condiviso](https://github.com/Azure-Samples/storage-dotnet-sas-getting-started)

## <a name="encryption-in-transit"></a>Crittografia in transito
### <a name="transport-level-encryption--using-https"></a>Crittografia a livello di trasporto: uso di HTTPS
Un altro passaggio, è necessario intraprendere sicurezza hello tooensure dei dati di archiviazione di Azure è dati hello tooencrypt tra client hello e l'archiviazione di Azure. Hello prima si consiglia di tooalways utilizzare hello [HTTPS](https://en.wikipedia.org/wiki/HTTPS) hello di protocollo, che assicura una comunicazione protetta tramite Internet pubblico.

toohave un canale di comunicazione sicuro, è necessario utilizzare sempre HTTPS durante la chiamata API REST hello o accede agli oggetti nel servizio di archiviazione. Inoltre, **firme di accesso condiviso**, che può essere utilizzato toodelegate accedere agli oggetti di archiviazione tooAzure, includono un'opzione toospecify tale hello solo quando si usano firme di accesso condiviso, assicurando che chiunque è possibile utilizzare il protocollo HTTPS l'invio di collegamenti con i token di firma di accesso condiviso Usa protocollo corretto hello.

È possibile imporre l'uso di hello del protocollo HTTPS durante la chiamata di oggetti tooaccess API REST di hello negli account di archiviazione, consentendo [necessario trasferimento sicuro](storage-require-secure-transfer.md) hello account di archiviazione. Una volta abilitata l'opzione, le connessioni che usano il protocollo HTTP verranno rifiutate.

### <a name="using-encryption-during-transit-with-azure-file-shares"></a>Uso della crittografia durante la trasmissione con condivisioni file di Azure
Archiviazione di File di Azure supporta HTTPS, quando si utilizza l'API REST di hello, ma è più comunemente utilizzati come una condivisione file SMB collegato tooa macchina virtuale. SMB 2.1 non supporta la crittografia, pertanto le connessioni sono consentite solo all'interno di hello stessa area in Azure. Tuttavia, SMB 3.0 supporta la crittografia, è disponibile in Windows Server 2012 R2 e Windows 8, Windows 8.1 e Windows 10, consentendo tra aree di accesso e anche l'accesso sul desktop hello.

Si noti che mentre condivisioni File di Azure possono essere utilizzate con Unix, hello client SMB Linux non ancora supporta la crittografia, pertanto l'accesso è consentito solo all'interno di un'area di Azure. Supporto della crittografia per Linux è roadmap hello di sviluppatori Linux responsabili per la funzionalità SMB. Quando si aggiunge la crittografia, sarà necessario hello stesso possibilità per l'accesso a una condivisione di File di Azure in Linux, come avviene per Windows.

È possibile imporre l'uso di hello della crittografia con il servizio file di Azure hello abilitando [necessario trasferimento sicuro](storage-require-secure-transfer.md) hello account di archiviazione. Se tramite hello API REST, HTTPs è obbligatorio. Per SMB, solo le connessioni SMB che supportano la crittografia saranno stabilite correttamente.

#### <a name="resources"></a>Risorse
* [Come toouse archiviazione di File di Azure con Linux](storage-how-to-use-files-linux.md)

  Questo articolo illustra come un File di Azure toomount condividere in un sistema e caricare e scaricare i file di Linux.
* [Introduzione ad Archiviazione file di Azure in Windows](storage-dotnet-how-to-use-files.md)

  In questo articolo viene fornita una panoramica delle condivisioni File di Azure e come toomount e usarli tramite PowerShell e .NET.
* [Inside Azure File storage (Analisi di Archiviazione file di Azure)](https://azure.microsoft.com/blog/inside-azure-file-storage/)

  In questo articolo annuncia hello disponibilità generale di archiviazione di File di Azure e vengono forniti dettagli tecnici sulla crittografia hello SMB 3.0.

### <a name="using-client-side-encryption-toosecure-data-that-you-send-toostorage"></a>Utilizzando i dati di toosecure crittografia lato Client che si invia toostorage
Un'altra opzione che consente di assicurarsi che i dati siano protetti durante il trasferimento tra un'applicazione client e la risorsa di archiviazione è la crittografia lato client. Hello dati vengono crittografati prima di essere trasferiti nell'archiviazione di Azure. Quando si recuperano dati hello da archiviazione di Azure, dati hello viene decrittografati dopo la ricezione sul lato client hello. Anche se crittografia dei dati hello passare attraverso la rete hello, è consigliabile usare anche HTTPS, perché contiene i controlli di integrità dei dati incorporati che aiutano a ridurre gli errori di rete che interessano l'integrità dei dati hello hello.

Crittografia client-side è anche un metodo per la crittografia dei dati inattivi, hello vengono memorizzati in forma crittografata. Parleremo questo più dettagliatamente nella sezione hello in [crittografia](#encryption-at-rest).

## <a name="encryption-at-rest"></a>Crittografia di dati inattivi
Esistono tre funzionalità di Azure che consentono di crittografare dati inattivi. Azure crittografia del disco è utilizzato tooencrypt hello del sistema operativo e i dischi dati in macchine virtuali IaaS. altri due Hello di crittografia lato Client e SSE – tooencrypt utilizzati sia i dati in archiviazione di Azure. Si esaminerà ognuna di queste funzionalità, eseguendo quindi un confronto per vedere quando usare ognuna di esse.

Sebbene sia possibile utilizzare i dati di crittografia lato Client tooencrypt hello in transito (che viene inoltre archiviato in formato crittografato nel servizio di archiviazione), è possibile preferiscono utilizzare toosimply HTTPS durante il trasferimento di hello e ha un modo per toobe dati hello crittografato automaticamente quando è archiviati. Esistono due modi toodo questo - crittografia del disco di Azure e SSE. Viene utilizzato uno toodirectly crittografare i dati di hello nei dischi del sistema operativo e i dati utilizzati dalle macchine virtuali e hello altri dati utilizzati tooencrypt scritti tooAzure nell'archiviazione Blob.

### <a name="storage-service-encryption-sse"></a>Crittografia del servizio di archiviazione di Azure (SSE)
SSE consente che il servizio di archiviazione hello crittografa automaticamente i dati hello durante la scrittura di archiviazione tooAzure toorequest. Quando si leggono dati hello da archiviazione di Azure, verrà decrittografato dal servizio di archiviazione hello prima della restituzione. In questo modo toosecure i dati senza dovere toomodify codice o aggiungono codice tooany applicazioni.

Si tratta di un'impostazione che applica l'account di archiviazione intero toohello. È possibile abilitare e disabilitare questa funzionalità modificando il valore di hello dell'impostazione di hello. toodo, è possibile utilizzare hello portale di Azure PowerShell, hello CLI di Azure, hello API REST di Provider di risorse di archiviazione o hello libreria Client di archiviazione .NET. Per impostazione predefinita, la funzionalità SSE è disattivata.

In questo momento, chiavi di crittografia di hello hello vengono gestite da Microsoft. Si genera chiavi di hello originariamente e gestione l'archiviazione sicura hello di chiavi hello nonché rotazione regolare hello come definito dai criteri di Microsoft interno. In futuro hello, consente di ottenere hello possibilità toomanage proprie chiavi di crittografia e di fornire un percorso di migrazione dalle chiavi di gestione di Microsoft gestito toocustomer le chiavi.

Questa funzionalità è disponibile per gli account Standard e Premium archiviazione creati utilizzando hello modello di distribuzione di gestione delle risorse. SSE si applica solo tooblock i BLOB, BLOB di pagine e BLOB di aggiunta. Hello altri tipi di dati, inclusi tabelle, code e i file, non verranno crittografati.

Dati vengono crittografati solo quando è abilitata SSE e dati hello tooBlob archiviazione. L'abilitazione o la disabilitazione di SSE non influisce sui dati esistenti. In altre parole, quando si abilita la crittografia, non torna indietro né crittografare i dati che è già presente. né per decrittografare dati hello già presenti quando si disabilita SSE.

Se si desidera toouse questa funzionalità con un account di archiviazione classica, è possibile creare un nuovo account di archiviazione di gestione delle risorse e usare AzCopy toocopy hello toohello dati nuovo account.

### <a name="client-side-encryption"></a>crittografia lato client
Quando si parla di crittografia hello dei dati di hello in transito accennato crittografia lato client. Questa funzionalità consente tooprogrammatically per crittografare i dati in un'applicazione client prima di inviarlo in hello transito toobe scritto tooAzure archiviazione e tooprogrammatically decrittografare i dati dopo averli recuperati dall'archiviazione di Azure.

Questo fornisce la crittografia in transito, ma fornisce anche funzionalità hello di crittografia. Si noti che benché hello dati vengono crittografati in transito, è comunque consigliabile utilizzare controlli di integrità dei dati incorporati hello che aiutano a ridurre gli errori di rete che interessano l'integrità dei dati hello hello sfruttare tootake HTTPS.

Un esempio di in cui è possibile utilizzare questa opzione è se si dispone di un'applicazione web per l'archiviazione BLOB e recupera i BLOB e si desidera che un'applicazione hello e toobe dati il più sicuro possibile. In questo caso, si userà la crittografia lato client. il traffico tra hello client e il servizio Blob di Azure hello Hello contiene risorse crittografato hello e nessuno può interpretare dati hello in transito e viene ricostituire nei blob privati.

Crittografia lato client viene compilata in Java hello e hello archiviazione client librerie .NET, che a sua volta utilizza hello API insieme di credenziali chiave di Azure, rendendola un'operazione abbastanza semplice per è tooimplement. il processo di Hello di crittografare e decrittografare dati hello utilizza hello busta tecnica e archivia i metadati utilizzati da crittografia hello in ogni oggetto di archiviazione. Ad esempio, per i BLOB, li archivia in hello i metadati del blob, mentre per le code, viene aggiunto tooeach messaggio della coda.

Per la crittografia hello stesso, è possibile generare e gestire le proprie chiavi di crittografia. È inoltre possibile utilizzare le chiavi generate da hello Azure Storage Client Library oppure è possibile disporre di hello insieme credenziali chiavi Azure genera chiavi di hello. Si possono archiviare le chiavi di crittografia nell'archiviazione chiavi locale oppure in un insieme di credenziali delle chiavi di Azure. Insieme di credenziali chiave di Azure consente di segreti di toohello toogrant accesso degli utenti toospecific insieme credenziali chiavi Azure tramite Azure Active Directory. Ciò significa che non solo a chiunque può leggere hello insieme credenziali chiavi Azure e recuperare le chiavi di hello che si utilizza per la crittografia lato client.

#### <a name="resources"></a>Risorse
* [Crittografare e decrittografare i BLOB in Archiviazione di Microsoft Azure tramite l'insieme di credenziali chiave di Azure](storage-encrypt-decrypt-blobs-key-vault.md)

  Questo articolo viene illustrato come crittografia lato client toouse insieme di credenziali chiave di Azure, incluso come toocreate hello KEK e archiviarla nell'insieme di credenziali hello tramite PowerShell.
* [Crittografia lato client e Insieme di credenziali chiave Azure per Archiviazione di Microsoft Azure](storage-client-side-encryption.md)

  In questo articolo fornisce una spiegazione della crittografia lato client e vengono forniti esempi dell'utilizzo di hello client libreria tooencrypt e decrittografare le risorse di archiviazione da servizi di archiviazione quattro hello. Illustra anche l'insieme di credenziali delle chiavi di Azure.

### <a name="using-azure-disk-encryption-tooencrypt-disks-used-by-your-virtual-machines"></a>Utilizzando la crittografia del disco di Azure tooencrypt dischi utilizzano da macchine virtuali
Crittografia dischi di Azure è una nuova funzionalità. Questa funzionalità permette di dischi del sistema operativo di tooencrypt hello e i dischi di dati utilizzati da una macchina virtuale IaaS. Per Windows, hello unità vengono crittografate mediante la tecnologia di crittografia BitLocker standard del settore. Per Linux, dischi hello vengono crittografati mediante la tecnologia hello Crypt di data mining. Questo è integrato con insieme credenziali chiavi Azure tooallow è toocontrol e gestire chiavi di crittografia disco hello.

soluzione Hello supporta hello seguenti scenari per le macchine virtuali IaaS quando sono abilitati in Microsoft Azure:

* Integrazione dell'insieme di credenziali delle chiavi di Azure.
* Macchine virtuali di livello Standard: [serie A, D, DS, G, GS e così via per VM IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Abilitazione della crittografia nelle macchine virtuali IaaS Windows e Linux
* Disabilitazione della crittografia nel sistema operativo e nelle unità dati per le VM IaaS Windows
* Disabilitazione della crittografia nelle unità dati per le macchine virtuali IaaS Linux
* Abilitazione della crittografia in macchine virtuali IaaS in esecuzione nel sistema operativo client Windows
* Abilitazione della crittografia su volumi con percorsi di montaggio
* Abilitazione della crittografia nelle macchine virtuali Linux configurate con striping del disco (RAID) tramite mdadm
* Abilitazione della crittografia nelle macchine virtuali Linux usando LVM per i dischi dati
* Abilitazione della crittografia nelle macchine virtuali Windows configurate usando spazi di archiviazione
* Sono supportate tutte le aree geografiche pubbliche di Azure

soluzione Hello non supporta i seguenti scenari, le funzionalità e tecnologie in versione di hello hello:

* VM IaaS del piano Basic
* Disabilitazione della crittografia in un'unità del sistema operativo per le VM IaaS Linux
* Macchine virtuali IaaS che vengono creati utilizzando il metodo di creazione hello classico di VM
* Integrazione con il servizio di gestione delle chiavi locale.
* Archiviazione file di Azure (file system condiviso), file system di rete (NFS, Network File System), volumi dinamici e macchine virtuali Windows configurate con sistemi RAID basati su software


> [!NOTE]
> Crittografia del disco del sistema operativo Linux è attualmente supportata in hello seguenti distribuzioni Linux: RHEL 7.2, CentOS 7.2n e Ubuntu 16.04.
>
>

Questa funzionalità garantisce che tutti i dati presenti sui dischi delle macchine virtuali siano crittografati mentre sono inattivi in Archiviazione di Azure.

#### <a name="resources"></a>Risorse
* [Azure Disk Encryption per le macchine virtuali IaaS Windows e Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="comparison-of-azure-disk-encryption-sse-and-client-side-encryption"></a>Confronto tra Crittografia dischi di Azure, SSE e crittografia lato client
#### <a name="iaas-vms-and-their-vhd-files"></a>VM IaaS e i relativi file VHD
Per i dischi usati dalle VM IaaS è consigliabile usare Crittografia dischi di Azure. È possibile attivare SSE tooencrypt hello file VHD utilizzati tooback tali dischi nell'archiviazione di Azure, ma crittografa solo i dati appena scritti. Ciò significa che se si crea una macchina virtuale e quindi Abilita SSE nell'account di archiviazione hello che contiene i file VHD hello, solo le modifiche di hello verranno crittografate, non hello file disco rigido virtuale originale.

Se si crea una macchina virtuale usando un'immagine da hello Azure Marketplace, Azure esegue un [superficialmente copia](https://en.wikipedia.org/wiki/Object_copying) di hello immagine tooyour account di archiviazione in archiviazione di Azure e non crittografati anche se si dispone di SSE abilitato. Dopo aver hello VM crea e avvia l'aggiornamento di immagine hello, SSE inizierà la crittografia dei dati di hello. Per questo motivo, è migliore toouse che crittografia del disco di Azure nelle macchine virtuali creata da immagini in Azure Marketplace hello se si desidera completamente crittografato.

Se si sposta una macchina virtuale di pre-crittografata in Azure locale, si verrà tooAzure le chiavi di crittografia hello tooupload in grado di insieme di credenziali chiave e continuare a utilizzare la crittografia hello per la macchina virtuale che è stata usata in locale. Crittografia disco Azure viene abilitato toohandle questo scenario.

Se si dispone di file VHD non crittografati da on-premise, è possibile caricarlo nella raccolta di hello come un'immagine personalizzata e il provisioning di una macchina virtuale da esso. Se si esegue questa operazione utilizzando i modelli di gestione risorse di hello, è possibile chiedere la tooturn sulla crittografia del disco di Azure durante l'avvio hello macchina virtuale.

Quando si aggiunge un disco dati e montarlo in hello VM, è possibile attivare la crittografia del disco di Azure su tale disco dati. Da crittografare innanzitutto tale disco dati in locale e quindi livello di Gestione servizio hello eseguire un'operazione di scrittura Lazywriter nel servizio di archiviazione in modo hello archiviazione contenuto viene crittografato.

#### <a name="client-side-encryption"></a>Crittografia lato client
Crittografia lato client è un metodo più sicuro hello della crittografia dei dati, perché viene crittografata prima di transito e crittografa i dati di hello inattivi. È necessario aggiungere applicazioni tooyour codice utilizzando l'archiviazione, potrebbe non essere necessario toodo. In questi casi, è possibile utilizzare HTTPs per i dati in transito e SSE tooencrypt hello inattivi.

Grazie alla crittografia lato client, è possibile crittografare entità tabella, messaggi nella coda e BLOB. SSE consente di crittografare solo i BLOB. Se è necessaria una tabella e coda toobe dati crittografati, è consigliabile usare la crittografia lato client.

Crittografia lato client viene gestita interamente da un'applicazione hello. Questo è l'approccio più sicuro hello, ma richiede applicazione tooyour di toomake modifiche a livello di codice e implementare i processi di gestione delle chiavi. Utilizzare questo quando si desidera hello aggiuntiva di sicurezza durante il transito e si desidera toobe i dati archiviati crittografati.

Crittografia lato client è un carico maggiore sul client hello e si hanno tooaccount per questo nei piani di scalabilità, soprattutto se si ha la crittografia e il trasferimento di una grande quantità di dati.

#### <a name="storage-service-encryption-sse"></a>Crittografia del servizio di archiviazione di Azure (SSE)
La crittografia del servizio di archiviazione è gestita da Archiviazione di Azure. Utilizza SSE non fornisce sicurezza hello dei dati di hello in transito, ma esegue la crittografia dati hello durante la scrittura tooAzure archiviazione. Non è presente alcun impatto sulle prestazioni di hello quando si utilizza questa funzionalità.

SSE permette di crittografare solo BLOB in blocchi, BLOB di aggiunta e BLOB di pagine. Se è necessario tooencrypt dati della tabella o dati della coda, è consigliabile usare la crittografia lato client.

Se si dispone di un archivio o una raccolta di file di disco rigido virtuale utilizzato come base per la creazione di nuove macchine virtuali, creare un nuovo account di archiviazione, abilitare SSE e quindi caricare account toothat file VHD di hello. Questi file VHD saranno crittografati da Archiviazione di Azure.

Se si dispone di crittografia del disco di Azure abilitata per i dischi di hello in una macchina virtuale e SSE abilitato nell'account di archiviazione hello hello cui risiedono i file VHD, funzionerà correttamente; si verificherà in tutti i dati appena scritto da crittografati due volte.

## <a name="storage-analytics"></a>di Analisi archiviazione
### <a name="using-storage-analytics-toomonitor-authorization-type"></a>Utilizzando il tipo di autorizzazione toomonitor Analitica di archiviazione
Per ogni account di archiviazione, è possibile abilitare la registrazione tooperform Analitica di archiviazione di Azure e archiviare i dati di metrica. Questo è toouse un ottimo strumento quando si vuole che le metriche delle prestazioni di hello toocheck di un account di archiviazione o necessario tootroubleshoot un account di archiviazione perché si sono verificati problemi di prestazioni.

Un altro blocco di dati che è possibile visualizzare in hello archiviazione analitica log è il metodo di autenticazione hello utilizzato da un utente durante l'accesso di archiviazione. Ad esempio, con archiviazione Blob, è possibile vedere se utilizzati una firma di accesso condiviso o chiavi dell'account di archiviazione hello, o se il blob hello cui si accede è pubblico.

Può essere molto utile se si è strettamente protegge toostorage di accesso. Ad esempio, nell'archiviazione Blob, è possibile impostare tutte tooprivate contenitori hello e implementare l'utilizzo di hello di un servizio di firma di accesso condiviso all'interno delle applicazioni. È quindi possibile controllare hello registra regolarmente toosee se i BLOB sono accessibili tramite chiavi account di archiviazione di hello che potrebbero indicare una violazione della sicurezza, o se BLOB hello sono pubblici, ma non deve essere.

#### <a name="what-do-hello-logs-look-like"></a>Hello registri aspetto?
Dopo che si abilita metriche di account di archiviazione hello e la registrazione tramite il portale di Azure hello, analitica dei dati inizierà tooaccumulate rapidamente. registrazione di Hello e le metriche per ogni servizio è separato; registrazione di Hello viene scritto solo quando l'attività è in tale account di archiviazione, mentre le metriche hello verranno registrate ogni minuto, ogni ora o ogni giorno, a seconda della configurazione.

Hello log vengono archiviati in BLOB in blocchi in un contenitore denominato $logs nell'account di archiviazione hello. Questo contenitore viene creato automaticamente quando si abilita Analisi archiviazione. Dopo che il contenitore è stato creato, non sarà possibile eliminarlo, anche se si può eliminare il relativo contenuto.

Nel contenitore hello $logs è una cartella per ogni servizio e quindi esistono le sottocartelle per hello anno/mese/giorno/ora. In ore, i registri di hello semplicemente sono numerati. Si tratta di quali hello sarà simile a struttura di directory:

![Visualizzazione dei file di log](./media/storage-security-guide/image1.png)

Viene registrato ogni tooAzure richiesta archiviazione. Di seguito è riportato uno snapshot di un file di log, che mostra hello prima alcuni campi.

![Snapshot di un file di log](./media/storage-security-guide/image2.png)

È possibile vedere che è possibile utilizzare hello registri tootrack qualsiasi tipo di account di archiviazione tooa chiamate.

#### <a name="what-are-all-of-those-fields-for"></a>Scopo di tutti questi campi
C'è un articolo elencato in risorse hello seguenti che possono essere elencate hello di hello molti campi nei registri di hello e vengono utilizzati per. Ecco hello elenco di campi nell'ordine:

![Snapshot dei campi in un file di log](./media/storage-security-guide/image3.png)

Siamo interessati a voci hello per GetBlob, e come vengono autenticati, pertanto è necessario toolook per le voci con tipo di operazione "Get-Blob" e controllare la stato della richiesta di hello (4<sup>th</sup> colonna) e il tipo di autorizzazione hello (8<sup>th</sup> colonna).

Ad esempio, in hello innanzitutto alcune righe nell'elenco di hello sopra, stato della richiesta di hello è "Success" e il tipo di autorizzazione hello "autenticazione". Ciò significa che la richiesta hello è stata convalidata tramite chiave dell'account di archiviazione hello.

#### <a name="how-are-my-blobs-being-authenticated"></a>Modalità di autenticazione dei BLOB
Sono tre i casi interessanti in questo caso.

1. Hello blob sia pubblico e vi si accede tramite un URL senza una firma di accesso condiviso. In questo caso, stato della richiesta di hello è "AnonymousSuccess" e il tipo di autorizzazione hello è "anonimo".

   1.0;2015-11-17T02:01:29.0488963Z;GetBlob;**AnonymousSuccess**;200;124;37;**anonymous**;;mystorage…
2. blob Hello è privata ed è stata usata con una firma di accesso condiviso. In questo caso, stato della richiesta di hello è "SASSuccess" e il tipo di autorizzazione hello è "sa".

   1.0;2015-11-16T18:30:05.6556115Z;GetBlob;**SASSuccess**;200;416;64;**sas**;;mystorage…
3. blob Hello è privata e chiave di archiviazione hello tooaccess usato è. In questo caso, stato della richiesta di hello è "**successo**"e il tipo di autorizzazione hello è"**autenticato**".

   1.0;2015-11-16T18:32:24.3174537Z;GetBlob;**Success**;206;59;22;**authenticated**;mystorage…

È possibile utilizzare tooview Microsoft Message Analyzer hello e analizzare i log. Include funzionalità di ricerca e filtro. Ad esempio, è possibile toosearch per le istanze di toosee GetBlob se utilizzo hello è quello previsto, ad esempio toomake che un utente non accede a account di archiviazione non corretta.

#### <a name="resources"></a>Risorse
* [Analisi archiviazione](storage-analytics.md)

  In questo articolo viene fornita una panoramica di analitica di archiviazione e come tooenable li.
* [Formato log Analisi archiviazione](https://msdn.microsoft.com/library/azure/hh343259.aspx)

  Questo articolo illustra il formato di Log di archiviazione Analitica hello e dettagli hello campi disponibili al suo interno, tra cui tipo di autenticazione, che indica il tipo di hello di autenticazione utilizzato per la richiesta di hello.
* [Monitoraggio di un Account di archiviazione nel portale di Azure hello](storage-monitor-storage-account.md)

  Questo articolo viene illustrato come tooconfigure delle metriche di monitoraggio e registrazione per un account di archiviazione.
* [Risoluzione dei problemi end-to-end mediante le metriche e la registrazione di Archiviazione di Azure, AzCopy e Message Analyzer](storage-e2e-troubleshooting.md)

  In questo articolo parla di risoluzione dei problemi mediante hello archiviazione Analitica e Mostra come toouse hello Microsoft Message Analyzer.
* [Guida operativa di Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)

  In questo articolo è riferimento hello per hello Microsoft Message Analyzer e include esercitazione tooa collegamenti, avvio rapido e il riepilogo delle funzionalità.

## <a name="cross-origin-resource-sharing-cors"></a>Condivisione risorse tra le origini (CORS)
### <a name="cross-domain-access-of-resources"></a>Accesso tra domini alle risorse
Quando un Web browser in esecuzione in un dominio invia una richiesta HTTP per una risorsa da un dominio diverso, viene definita richiesta HTTP tra le origini. Ad esempio, una pagina HTML servita da contoso.com esegue una richiesta per un'immagine JPEG ospitata in fabrikam.blob.core.windows.net. Per motivi di sicurezza, i browser limitano le richieste HTTP tra le origini avviate da script, ad esempio JavaScript. Ciò significa che quando un codice JavaScript in una pagina web in contoso.com richiede tale jpeg su fabrikam.blob.core.windows.net, browser hello non consentirà hello richiesta.

Questa funzione sono toodo con archiviazione di Azure? Anche se si desidera archiviare risorse statiche, ad esempio i file di dati JSON o XML nell'archiviazione Blob utilizzando un account di archiviazione denominato Fabrikam dominio hello per le risorse di hello sarà fabrikam.blob.core.windows.net e un'applicazione web contoso.com hello non saranno in grado di tooaccess li utilizzo di JavaScript perché hello domini sono diversi. Questo vale anche se si sta toocall uno dei servizi di archiviazione di Azure, ad esempio archiviazione tabelle – hello che restituiscono JSON toobe di dati elaborati da client JavaScript hello.

#### <a name="possible-solutions"></a>Possibili soluzioni
Un modo tooresolve si tratta di un dominio personalizzato come "storage.contoso.com" toofabrikam.blob.core.windows.net tooassign. problema di Hello è che è possibile assegnare solo account di archiviazione tooone dominio personalizzato. Cosa accade se vengono archiviate le risorse di hello in più account di archiviazione?

Un altro modo tooresolve questo comporta toohave hello web dell'applicazione come proxy per le chiamate di archiviazione hello. Pertanto se si sta caricando un tooBlob file archiviazione, un'applicazione web hello sarebbe di scriverlo in locale e quindi copiarlo tooBlob archiviazione o sarebbe tutti i relativi letto in memoria e scrivere quindi tooBlob archiviazione. In alternativa, è possibile scrivere un'applicazione web dedicato (ad esempio un'API Web) che consente di caricare file hello in locale e li scrive tooBlob archiviazione. In entrambi i casi, è tooaccount per tale funzione quando è necessario determinare la scalabilità di hello.

#### <a name="how-can-cors-help"></a>Utilità di CORS
Archiviazione di Azure consente tooenable CORS – Cross Origin Resource Sharing. Per ogni account di archiviazione, è possibile specificare i domini che possono accedere alle risorse di hello in tale account di archiviazione. Ad esempio, in questo caso descritto in precedenza, è possibile attivare l'account di archiviazione fabrikam.blob.core.windows.net hello CORS e configurarlo tooallow toocontoso.com di accesso. Quindi hello web applicazione contoso.com può direttamente accedere alle risorse di hello in fabrikam.blob.core.windows.net.

Una cosa toonote è che CORS consente l'accesso, ma non fornisce autenticazione, è necessario per tutti i accesso non pubblico di risorse di archiviazione. Ciò significa che è possibile accedere solo BLOB se sono pubblici o se si include una firma di accesso condiviso è hello le autorizzazioni appropriate. Tabelle, code e i file non hanno accesso pubblico e richiedono una firma di accesso condiviso.

Per impostazione predefinita, CORS è disabilitato in tutti i servizi. È possibile abilitare CORS utilizzando hello API REST o hello storage client library toocall uno dei criteri del servizio hello tooset metodi hello. In questo caso, includere una regola CORS, in formato XML. Di seguito è riportato un esempio di una regola CORS che è stata impostata tramite l'operazione Set Service Properties hello per hello servizio Blob per un account di archiviazione. È possibile eseguire tale operazione utilizzando libreria client di archiviazione hello o hello API REST per l'archiviazione di Azure.

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Ecco il significato di ogni riga:

* **AllowedOrigins** indica quali domini senza corrispondenza è possono richiedere e ricevere dati dal servizio di archiviazione hello. Significa che contoso.com e fabrikam.com possono richiedere dati dall'archivio BLOB per un account di archiviazione specifico. È inoltre possibile impostare il carattere jolly tooa (\*) le richieste di tutti i domini tooaccess tooallow.
* **AllowedMethods** si tratta di hello elenco di metodi (verbi di richiesta HTTP) che può essere usato quando si effettua la richiesta hello. In questo esempio, sono consentiti solo PUT e GET. È possibile impostare il carattere jolly tooa (\*) tooallow toobe di tutti i metodi utilizzati.
* **AllowedHeaders** hello richiesta le intestazioni che hello dominio di origine è possono specificare quando si effettua la richiesta hello. In questo esempio, sono consentite tutte le intestazioni dei di metadati che iniziano con x-ms-meta-data, x-ms-meta-target e x-ms-meta-abc. Hello carattere jolly (\*) indica che qualsiasi intestazione che inizi con hello specificato è consentito un prefisso.
* **ExposedHeaders** in questo modo le intestazioni di risposta devono essere esposto dell'autorità di certificazione di hello browser toohello richiesta. In questo esempio vengono esposte tutte le intestazioni che iniziano con "x-ms-meta-".
* **MaxAgeInSeconds** ovvero hello quantità massima di tempo che un browser verrà memorizzati nella cache richiesta OPTIONS preliminare hello. (Per ulteriori informazioni sulla richiesta preliminare hello, controllare hello primo articolo riportato di seguito).

#### <a name="resources"></a>Risorse
Per ulteriori informazioni su CORS e la modalità tooenable, estrarre queste risorse.

* [Supporto di condivisione delle risorse Multiorigine (CORS) per servizi di archiviazione di Azure in Azure.com hello](storage-cors-support.md)

  In questo articolo viene fornita una panoramica di CORS e funzionamento delle regole per i servizi di archiviazione diversi hello tooset hello.
* [Supporto di condivisione delle risorse Multiorigine (CORS) per hello servizi di archiviazione di Azure su MSDN](https://msdn.microsoft.com/library/azure/dn535601.aspx)

  Si tratta di documentazione di riferimento hello per supporto CORS per servizi di archiviazione di Azure hello. Questo è l'applicazione di servizio di archiviazione tooeach tooarticles di collegamenti e viene illustrato un esempio e viene descritto ogni elemento nel file CORS hello.
* [Archiviazione di Microsoft Azure: Introduzione a CORS](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/02/03/windows-azure-storage-introducing-cors.aspx)

  Si tratta di un articolo di blog iniziale toohello collegamento annuncio CORS e la visualizzazione come toouse è.

## <a name="frequently-asked-questions-about-azure-storage-security"></a>Domande frequenti sulla sicurezza di Archiviazione di Azure
1. **Come è possibile verificare l'integrità di BLOB hello che consapevole trasferimento interno o all'esterno di archiviazione di Azure se non è possibile utilizzare il protocollo HTTPS hello hello?**

   Se per qualsiasi motivo è necessario toouse HTTP anziché HTTPS e si lavora con i BLOB in blocchi, è possibile utilizzare il controllo MD5 toohelp verificare l'integrità di hello del BLOB hello trasferiti. Ciò contribuisce a proteggere dagli errori a livello di rete/trasporto, ma non necessariamente dalle violazioni.

   Se è possibile utilizzare HTTPS, che fornisce la protezione a livello di trasporto, il controllo MD5 è ridondante e superfluo.

   Per ulteriori informazioni, vedere out hello [Panoramica MD5 del Blob di Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/02/18/windows-azure-blob-md5-overview.aspx).
2. **Per quanto riguarda la conformità FIPS per Stati Uniti hello Governo degli Stati Uniti?**

   Hello United States FIPS Federal Information Processing Standard () definisce gli algoritmi di crittografia approvati per l'utilizzo da Stati Uniti Sistemi di computer governo federale per la protezione dei dati sensibili hello. Abilitazione FIPS la modalità Windows server o desktop indica hello del sistema operativo che è necessario utilizzare gli algoritmi di crittografia FIPS convalidati solo. Se un'applicazione utilizza algoritmi non conformi, applicazioni hello verranno interrotti. Le versioni con.NET Framework 4.5.2 o versioni successive, un'applicazione hello passa automaticamente algoritmi conformi a FIPS toouse algoritmi di crittografia hello quando hello computer è in modalità FIPS.

   Microsoft lasciandolo backup tooeach cliente toodecide se tooenable la modalità FIPS. Riteniamo che vi è alcun motivo Impellente per i clienti che non sono modalità FIPS tooenable soggetto toogovernment normative per impostazione predefinita.

   **Risorse**

* [Perché non viene più consigliata la "Modalità FIPS"](http://blogs.technet.com/b/secguide/archive/2014/04/07/why-we-re-not-recommending-fips-mode-anymore.aspx)

  Questo articolo di blog fornisce una panoramica di FIPS e spiega perché non viene più abilitata la modalità FIPS per impostazione predefinita.
* [Convalida FIPS 140](https://technet.microsoft.com/library/cc750357.aspx)

  Questo articolo fornisce informazioni su come i prodotti Microsoft e i moduli di crittografia conformi allo standard FIPS hello per Stati Uniti hello Governo Federale degli Stati Uniti.
* [Effetti delle impostazioni di sicurezza "Crittografia di sistema: usa algoritmi FIPS conformi per crittografia, hash e firma" in Windows XP e versioni successive di Windows](https://support.microsoft.com/kb/811833)

  In questo articolo discute relative all'utilizzo di hello della modalità FIPS in computer Windows meno recenti.
