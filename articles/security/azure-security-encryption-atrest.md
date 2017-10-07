---
title: Dati di Azure--crittografia aaaMicrosoft | Documenti Microsoft
description: "In questo articolo viene fornita una panoramica della crittografia dei dati di Microsoft Azure a riposo, hello funzionalità generali e considerazioni generali."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: TomSh
ms.assetid: 9dcb190e-e534-4787-bf82-8ce73bf47dba
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: yurid
ms.openlocfilehash: d74d103e4fd7585543b4f039877af7d742a6b2e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-encryption-at-rest"></a>Crittografia dei dati inattivi di Azure
Sono disponibili più strumenti all'interno dei dati di Microsoft Azure toosafeguard in base alle esigenze di sicurezza e conformità tooyour della società. Questo documento è incentrato su come dati sarà protetto inattivi in Microsoft Azure, vengono illustrati i vari componenti partecipa all'implementazione di protezione dati hello di hello e revisioni di approcci di protezione di gestione delle chiavi diverso hello positivi e negativi. 

La crittografia dei dati inattivi è un requisito di sicurezza comune. Il vantaggio di Microsoft Azure è che le organizzazioni possono raggiungere crittografia inattivi senza costi hello dell'implementazione e al rischio di hello e gestione di una soluzione di gestione delle chiavi personalizzate. Le organizzazioni possibile hello consentendo di gestire completamente la crittografia inattivi Azure. Inoltre, le organizzazioni hanno diverse opzioni tooclosely gestire crittografia o le chiavi di crittografia.

## <a name="what-is-encryption-at-rest"></a>Che cos'è la crittografia dei dati inattivi?
Crittografia fa riferimento toohello crittografia codifica (crittografia) dei dati quando viene resa persistente. Hello crittografia progettazioni di Rest in Azure usare tooencrypt crittografia simmetrica e decrittografare grandi quantità di dati rapidamente secondo il modello concettuale semplice di tooa:

- Una chiave di crittografia simmetrica è tooencrypt utilizzati dati viene resa persistente 
- Hello stessa chiave di crittografia è utilizzata toodecrypt che i dati come preparato per l'utilizzo in memoria
- I dati possono essere partizionati ed è possibile usare chiavi differenti per ogni partizione.
- Le chiavi devono essere archiviate in un luogo sicuro con i criteri di controllo di accesso limitare le identità toocertain di accesso e utilizzo della chiave di registrazione. Le chiavi di crittografia dati spesso vengono crittografate con la crittografia asimmetrica toofurther limitare l'accesso (descritto in hello *chiave gerarchia*, più avanti in questo articolo)

Hello precedente vengono descritti gli elementi ad alto livello comune hello di crittografia. A livello pratico, gli scenari di gestione e di controllo delle chiavi, nonché le garanzie di scalabilità e disponibilità, richiedono costrutti aggiuntivi. Di seguito sono descritti i concetti e i componenti relativi alla crittografia dei dati inattivi di Microsoft Azure.

## <a name="hello-purpose-of-encryption-at-rest"></a>scopo di Hello di crittografia
Crittografia inattivi è previsto tooprovide protezione dei dati per dati a riposo (come descritto in precedenza.) Gli attacchi contro dati a riposo includono hardware di tentativi tooobtain accesso fisico toohello su quali hello dati vengono archiviati, e quindi compromissione hello contiene dati. In un attacco, unità disco rigido del server potrebbe avere manipolazioni durante la manutenzione, consentendo a un utente malintenzionato unità disco rigido tooremove hello. Autore dell'attacco hello successive dovrà inserire l'unità disco rigido hello in un computer con i dati di controllo tooattempt tooaccess hello. 

Crittografia inattivi è l'autore dell'attacco hello tooprevent progettato l'accesso ai dati di non crittografato hello garantendo hello dati vengono crittografati quando nel disco. Se un utente malintenzionato tooobtain crittografare un disco rigido con tali dati e chiavi di crittografia toohello alcun accesso, utente malintenzionato di hello non comprometterebbe dati hello senza difficoltà ottimale. In tale scenario, un utente malintenzionato dovrebbe tooattempt attacchi dati crittografati che sono molto più complessi e il consumo di risorse di accesso ai dati su un disco rigido non crittografati. Per questo motivo, la crittografia dei dati inattivi è estremamente utile e costituisce un requisito di alta priorità per molte organizzazioni. 

In alcuni casi, la crittografia dei dati inattivi è anche necessaria per i requisiti di conformità e governance dei dati dell'organizzazione. Regolamenti governativi e di settore, come HIPAA, PCI e FedRAMP, e requisiti normativi internazionali definiscono specifiche misure di sicurezza tramite processi e criteri relativi ai requisiti di protezione e crittografia dei dati. Per molte di queste normative, la crittografia dei dati inattivi è una misura obbligatoria necessaria per la conformità della protezione e la gestione dei dati. 

Inoltre toocompliance e requisiti normativi, crittografia deve essere interpretata come una funzionalità di piattaforma di difesa in profondità. Microsoft offre una piattaforma conforme per i servizi, applicazioni e dati, la funzionalità completa e la sicurezza fisica, accesso ai dati di controllo e di controllo, ma è importante tooprovide aggiuntive "sovrapposta" misure di sicurezza nel caso uno dei hello protezione di altre misure ha esito negativo. La crittografia dei dati inattivi fornisce un meccanismo di difesa aggiuntivo di questo tipo.

Microsoft è impegnata tooproviding di crittografia opzioni rest in servizi cloud e tooprovide clienti adatto facilità di gestione delle chiavi di crittografia e toologs accesso indicando quando vengono utilizzate le chiavi di crittografia. Inoltre, Microsoft è impegnata verso obiettivo hello di rendere tutti i dati cliente crittografati a riposo per impostazione predefinita.

## <a name="azure-encryption-at-rest-components"></a>Componenti della crittografia dei dati inattivi di Azure

Come descritto in precedenza, l'obiettivo di hello di crittografia è che i dati che sono persistente su disco sono crittografati con una chiave di crittografia segreta. tooachieve tale obiettivo proteggere la creazione della chiave, archiviazione, il controllo di accesso e la gestione della crittografia hello è necessario specificare le chiavi. Anche se i dettagli possono variare, servizi di Azure la crittografia in implementazioni di Rest possono essere descritti in termini di hello di sotto di concetti che vengono quindi illustrate nel seguente diagramma hello.

![Componenti](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig1.png)

### <a name="azure-key-vault"></a>Insieme di credenziali chiave Azure

percorso di archiviazione Hello di chiavi di crittografia hello e chiavi di accesso controllo toothose è tooan centrale crittografia modello rest. le chiavi di Hello devono toobe elevata protetta ma gestibile da servizi di toospecific disponibili e gli utenti specificati. Per servizi di Azure, insieme di credenziali chiave di Azure è hello la soluzione di archiviazione chiavi consigliata e fornisce un'esperienza di gestione comuni in tutti i servizi. Chiavi archiviate e gestite in insiemi di credenziali chiave e dell'insieme di credenziali di accesso tooa chiave possono essere forniti toousers o servizi. Azure Key Vault supporta la creazione di chiavi da parte dei clienti o l'importazione di chiavi dei clienti per l'uso in scenari con chiavi di crittografia gestite dal cliente.

### <a name="azure-active-directory"></a>Azure Active Directory

Le chiavi di hello toouse autorizzazioni archiviate in Azure insieme di credenziali chiave toomanage o tooaccess li per la crittografia al resto crittografia e decrittografia, è possibile assegnare account di Active Directory tooAzure. 

### <a name="key-hierarchy"></a>Gerarchia delle chiavi

In genere viene usata più di una chiave di crittografia in un'implementazione della crittografia dei dati inattivi. La crittografia asimmetrica è utile per stabilire l'attendibilità hello e l'autenticazione necessaria per la gestione e l'accesso alla chiave. La crittografia simmetrica è più efficiente per la crittografia e la decrittografia in blocco, perché consente una crittografia più avanzata e prestazioni migliori. Inoltre, limitare l'utilizzo di hello di un diminuisce chiave di crittografia unico rischio hello che hello chiave verrà compromessi e hello costo di riesecuzione della crittografia quando una chiave deve essere sostituita. vantaggi di hello tooleverage di crittografia asimmetrica e simmetrica e limite hello utilizzo e l'esposizione di una chiave singola, la crittografia Azure modelli rest usare hello seguenti tipi di chiavi composta da una gerarchia delle chiavi:

- **Chiave DEK (Data Encryption)** : una chiave simmetrica di AES256 utilizzato tooencrypt una partizione o un blocco di dati.  Una singola risorsa può avere diverse partizioni e più chiavi DEK. La crittografia di ogni blocco di dati con una chiave diversa rende più complessi gli attacchi di crittoanalisi. Accesso tooDEKs è richiesta da hello provider o applicazione istanza di risorsa che è la crittografia e decrittografia di un blocco specifico. Quando una chiave DEK viene sostituita con una nuova chiave solo hello dati nel relativo blocco associato devono essere nuovamente crittografati con chiave nuova hello.
- **Chiave di crittografia delle chiavi** : una chiave di crittografia asimmetrica utilizzato hello tooencrypt le chiavi di crittografia di dati. Utilizzo di una chiave di crittografia consente di hello chiavi di crittografia dei dati stessi toobe crittografati e controllato. entità Hello che dispone di accesso toohello KEK potrebbero essere diversi da entità hello che richiede hello chiave di Decrittografia. In questo modo un toohello entità toobroker accesso DEK a scopo di hello garantire l'accesso limitato di ogni partizione toospecific chiave di Decrittografia. Poiché hello KEK è obbligatorio toodecrypt hello DEK, hello KEK è in effetti un singolo punto da cui DEK può essere eliminato in modo efficace dall'eliminazione di hello KEK.

Chiavi di crittografia dati Hello, crittografati con chiavi di crittografia chiave hello vengono archiviate separatamente e solo un'entità con accesso toohello che chiave di crittografia è possibile ottenere le chiavi di crittografia dei dati crittografati con tale chiave. Sono supportati diversi modelli di archiviazione delle chiavi. Si parlerà in dettaglio più avanti nella sezione successiva di hello ogni modello.

## <a name="data-encryption-models"></a>Modelli di crittografia dei dati

Informazioni sui diversi modelli di crittografia di hello e i vantaggi e svantaggi è essenziale per informazioni sulle modalità hello diversi provider di risorse in Azure implementa crittografia. Queste definizioni sono condivise da tutti i provider di risorse in una tassonomia e Azure tooensure common language. 

Esistono tre scenari per la crittografia sul lato server:

- Crittografia lato server con chiavi gestite dal servizio
    - I provider di risorse Azure eseguire operazioni di crittografia e decrittografia hello
    - Microsoft gestisce le chiavi di hello
    - Funzionalità cloud complete

- Crittografia lato server con chiavi gestite dal cliente in Azure Key Vault
    - I provider di risorse Azure eseguire operazioni di crittografia e decrittografia hello
    - Il cliente controlla le chiavi tramite Azure Key Vault
    - Funzionalità cloud complete

- Crittografia lato server con chiavi gestite dal cliente su hardware controllato dal cliente
    - I provider di risorse Azure eseguire operazioni di crittografia e decrittografia hello
    - Il cliente controlla le chiavi su hardware controllato dal cliente
    - Funzionalità cloud complete

Per la crittografia lato client, prendere in considerazione i seguenti hello:

- I servizi di Azure non possono visualizzare i dati decrittografati
- I clienti mantengono e archiviano le chiavi in locale o in altri archivi sicuri. Le chiavi non sono servizi disponibili tooAzure
- Funzionalità cloud ridotte

modelli di crittografia Hello è supportato in Azure suddividere in due gruppi principali: "Crittografia Client" e "lato Server la crittografia" come indicato in precedenza. Nota che, indipendentemente dal modello rest crittografia hello servizi utilizzati, Azure sempre è consigliabile utilizzare hello di un trasporto protetto, ad esempio TLS o HTTPS. Pertanto, la crittografia nel trasporto deve essere risolti dal protocollo di trasporto hello e non deve essere un fattore determinante per determinare quali crittografia toouse modello rest.

### <a name="client-encryption-model"></a>Modello di crittografia client

Modello di crittografia client fa riferimento tooencryption che viene eseguita all'esterno di hello Provider di risorse o Azure dal servizio hello o applicazione chiamante. crittografia Hello può essere eseguita dall'applicazione di servizio hello in Azure o da un'applicazione in esecuzione in data center di hello cliente. In entrambi i casi, quando si sfruttando questo modello di crittografia, hello Provider di risorse di Azure riceve un blob crittografato dei dati senza dati hello toodecrypt possibilità di hello in alcun modo o dispone di chiavi di crittografia toohello di accesso. In questo modello, la gestione delle chiavi hello avviene mediante la chiamata di servizio o dell'applicazione hello ed è completamente opaco toohello servizio di Azure.

![Client](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig2.png)

### <a name="server-side-encryption-model"></a>Modello di crittografia lato server

I modelli di crittografia lato server, vedere tooencryption eseguite dal servizio di Azure hello. In questo modello, hello Provider di risorse esegue hello crittografare e decrittografare le operazioni. Ad esempio, l'archiviazione di Azure può ricevere i dati nelle operazioni di testo normale ed eseguirà la decrittografia e crittografia hello internamente. Hello Provider di risorse è possibile utilizzare le chiavi di crittografia vengono gestite da Microsoft o dal cliente hello a seconda di hello configurazione fornita. 

![Server](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig3.png)

### <a name="server-side-encryption-key-management-models"></a>Modelli di gestione delle chiavi per la crittografia lato server

Ognuno di crittografia lato server hello modelli rest implica caratteristiche distintive della gestione delle chiavi. Includono e come chiavi di crittografia vengono create e archiviate come nonché modelli di accesso hello e hello procedure rotazione delle chiavi. 

#### <a name="server-side-encryption-using-service-managed-keys"></a>Crittografia lato server con chiavi gestite dal servizio

Per molti clienti, requisito essenziale hello è tooensure che hello dati viene crittografato ogni volta che sono inattivi. Grazie alla crittografia lato server utilizzando le chiavi del servizio gestito, questo modello consentendo ai clienti toomark hello di risorse (Account di archiviazione, database SQL, e così via) per la crittografia e lasciando tutti gli aspetti di gestione delle chiavi, ad esempio backup, rotazione e rilascio di una chiave tooMicrosoft. La maggior parte dei servizi di Azure che supportano la crittografia inattivi in genere supporta questo modello di offload gestione hello di tooAzure le chiavi di crittografia hello. provider di risorse di Azure Hello crea chiavi hello, li inserisce nel servizio di archiviazione sicura e vengono recuperati quando necessario. Ciò significa che il servizio di hello dispone di chiavi di accesso completo toohello e servizio hello abbia il pieno controllo sulla gestione del ciclo di vita delle credenziali di hello.

![gestito](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig4.png)

La crittografia lato server utilizzando le chiavi del servizio gestito pertanto rapidamente indirizzi hello necessità toohave crittografia con bassa toohello overhead cliente. Quando è disponibile un cliente viene in genere apre hello portale di Azure per la sottoscrizione di destinazione hello e provider di risorse e verifica di una casella che indica che preferiscono hello toobe di dati crittografati. In alcuni provider di risorse, la crittografia lato server con chiavi gestite dal servizio è attiva per impostazione predefinita. 

Crittografia server-side con le chiavi gestite Microsoft implica servizio hello ha accesso completo toostore e gestisce le chiavi di hello. Mentre alcuni clienti desidera che le chiavi di hello toomanage perché pensano che può garantire una maggiore protezione, hello costi e i rischi associati a una soluzione di archiviazione chiavi personalizzate da considerare durante la valutazione di questo modello. In molti casi, un'organizzazione può stabilire che i vincoli di risorse o i rischi di una soluzione locale potrebbero maggiore rischio di hello di gestione del cloud di crittografia hello in chiavi rest.  Tuttavia, questo modello potrebbe non essere sufficiente per le organizzazioni che dispongono di creazione di requisiti toocontrol hello o ciclo di vita di chiavi di crittografia hello o personale diverso toohave gestire chiavi di crittografia di un servizio rispetto a quelle di gestione del servizio hello (ad esempio, separazione della gestione delle chiavi da hello modello generale di gestione per il servizio hello).

##### <a name="key-access"></a>Accesso alle chiavi

Quando viene utilizzata la crittografia lato Server con le chiavi del servizio gestito, hello la creazione della chiave, archiviazione e il servizio di accesso vengono gestiti dal servizio hello. In genere, i provider di risorse di Azure fondamentali di hello archivierà le chiavi di crittografia dati hello in un archivio dati toohello chiudere e rapidamente disponibile e accessibile durante le chiavi di crittografia chiave hello vengono archiviati in un archivio protetto interno.

**Vantaggi**

- Configurazione semplice
- Microsoft gestisce la rotazione, il backup e la ridondanza delle chiavi
- Utente non dispone di hello costo associato all'implementazione o hello il rischio di uno schema di gestione delle chiavi personalizzate.

**Svantaggi**

- Nessun controllo cliente sulle chiavi di crittografia hello (specifica della chiave del ciclo di vita, revoca, e così via.)
- Nessuna possibilità toosegregate la gestione delle chiavi dal modello generale di gestione per il servizio hello

#### <a name="server-side-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Crittografia lato server con chiavi gestite dal cliente in Azure Key Vault 

Per gli scenari in cui il requisito di hello è tooencrypt dati hello inattivi e i clienti le chiavi di crittografia hello di controllo è possono utilizzare la crittografia lato server utilizzando chiavi gestite dal cliente nell'insieme di credenziali chiave. Alcuni servizi possono essere archiviate solo radice di hello chiave di crittografia nell'insieme di credenziali chiave di Azure e hello archivio crittografato chiave di crittografia dei dati in dati di toohello più vicino un percorso interno. In che i clienti di scenario possono portare i propri tooKey (BYOK-portare il propria chiave), insieme di credenziali delle chiavi o generare nuove chiavi e usarli tooencrypt risorse di hello desiderato. Mentre hello Provider di risorse esegue operazioni di crittografia e decrittografia hello utilizza chiave hello configurato come chiave di hello radice per tutte le operazioni di crittografia. 

##### <a name="key-access"></a>Accesso alle chiavi

Hello crittografia lato server modello con le chiavi di gestito dal cliente nell'insieme di credenziali chiave di Azure prevede hello servizio l'accesso ai hello chiavi tooencrypt e decrittografia come necessario. Crittografia a chiavi rest vengono effettuate servizio tooa accessibile tramite un criterio di controllo di accesso concessione di tale servizio identità tooreceive hello tasto. Un servizio di Azure in esecuzione per conto di una sottoscrizione associata può essere configurato con un'identità per tale servizio all'interno della sottoscrizione. servizio Hello può eseguire l'autenticazione di Azure Active Directory e ricevere un token di autenticazione identificare se stesso come il servizio che agisce per conto di sottoscrizione hello. Token possono essere presentati tooKey insieme di credenziali tooobtain una chiave è consentito l'accesso a.

Per le operazioni con chiavi di crittografia, un'identità del servizio è possibile concedere accesso tooany di hello seguenti operazioni: decrittografare, crittografare, unwrapKey, wrapKey, verificare, accedere, ottenere, elenco, aggiornare, creare, importare, eliminare, eseguire il backup e ripristino.

tooobtain una chiave per la crittografia o decrittografia dei dati all'identità del servizio rest hello che hello Gestione risorse di istanza del servizio verrà eseguito come deve essere UnwrapKey (chiave tooget hello per la decrittografia) e WrapKey (tooinsert chiave nell'insieme di credenziali chiave quando si crea una nuova chiave).


>[!NOTE] 
>Per ulteriori dettagli sull'insieme di credenziali chiave autorizzazione vedere hello secure pagina insieme di credenziali chiave hello [documentazione insieme credenziali chiavi Azure](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault). 

**Vantaggi**

- Controllo completo sulle chiavi hello utilizzato: crittografia le chiavi vengono gestite nell'insieme di credenziali chiave hello cliente nel controllo del codice del cliente hello.
- Capacità tooencrypt master di tooone più servizi
- Possibile separare la gestione delle chiavi dal modello generale di gestione per il servizio hello
- Possibilità di definire il servizio e la posizione delle chiavi tra diverse aree geografiche

**Svantaggi**

- Il cliente ha la piena responsabilità per la gestione dell'accesso alle chiavi
- Il cliente ha la piena responsabilità per la gestione del ciclo di vita delle chiavi
- Sovraccarico aggiuntivo per l'installazione e la configurazione

#### <a name="server-side-encryption-using-service-managed-keys-in-customer-controlled-hardware"></a>Crittografia lato server con chiavi gestite dal servizio su hardware controllato dal cliente

Per gli scenari in cui il requisito di hello tooencrypt hello dati inattivi e gestione delle chiavi in un repository di proprietario all'esterno del controllo di Microsoft hello, alcuni servizi Azure Abilita modello di gestione delle chiavi di hello Host di un tasto (HYOK). In questo modello servizio hello deve recuperare la chiave hello da un sito esterno e pertanto sono interessate le garanzie di disponibilità e prestazioni e configurazione è più complessa. Inoltre, poiché servizio hello dispone di accesso toohello DEK durante la crittografia hello e operazioni di decrittografia hello garanzie di sicurezza globale di questo modello sono simili hello toowhen chiavi sono cliente gestiti nell'insieme di credenziali chiave di Azure.  Di conseguenza, questo modello non è appropriato per la maggior parte delle organizzazioni, a meno che specifici requisiti di gestione delle chiavi non lo rendano necessario. A causa di limitazioni toothese, la maggior parte dei servizi di Azure non supportano la crittografia lato server utilizzando le chiavi di server gestito in hardware del cliente controllato.

##### <a name="key-access"></a>Accesso alle chiavi

Quando viene utilizzata la crittografia lato server utilizzando le chiavi del servizio gestito in hardware del cliente controllata chiavi hello vengono mantenute in un sistema configurato dal cliente hello. Servizi di Azure che supportano questo modello forniscono un mezzo per stabilire un cliente tooa connessione protetta specificato archivio chiavi.

**Vantaggi**

- Controllo completo sulla chiave radice hello utilizzati: le chiavi vengono gestite da un archivio forniti dai clienti di crittografia
- Capacità tooencrypt master di tooone più servizi
- Possibile separare la gestione delle chiavi dal modello generale di gestione per il servizio hello
- Possibilità di definire il servizio e la posizione delle chiavi tra diverse aree geografiche

**Svantaggi**

- Piena responsabilità per l'archiviazione delle chiavi, la sicurezza, le prestazioni e la disponibilità
- Piena responsabilità per la gestione dell'accesso alle chiavi
- Piena responsabilità per la gestione del ciclo di vita delle chiavi
- Significativi costi di installazione, configurazione e manutenzione
- Dipendenza da una maggiore disponibilità di rete tra Data Center cliente hello e Data Center di Azure.

## <a name="encryption-at-rest-in-microsoft-cloud-services"></a>Crittografia dei dati inattivi nei servizi cloud Microsoft

I servizi cloud Microsoft vengono usati in tutti e tre i modelli cloud: IaaS, PaaS e SaaS. Di seguito sono riportati alcuni esempi di come si integrano in ciascun modello:

- Servizi software, cui viene fatto riferimento tooas Software come un Server o SaaS, quale applicazione forniti dal cloud hello, ad esempio Office 365.
- Servizi della piattaforma dei clienti che sfruttano cloud hello nelle proprie applicazioni, tramite il cloud di hello per operazioni come la funzionalità del bus di archiviazione, analitica e servizio.
- Servizi di infrastruttura o infrastruttura come servizio (IaaS) in cui i clienti di distribuire i sistemi operativi e applicazioni che sono ospitate in hello cloud e possibilmente sfruttando altri servizi cloud.

### <a name="encryption-at-rest-for-saas-customers"></a>Crittografia dei dati inattivi per i clienti SaaS

Per i clienti SaaS (Software as a Service) in genere la crittografia dei dati inattivi è abilitata o disponibile in ogni servizio. Servizi di Office 365 offre diverse opzioni per la crittografia dei clienti tooverify o abilitare inattivi. Per informazioni sui servizi di Office 365, vedere le tecnologie di crittografia dei dati per Office 365.

### <a name="encryption-at-rest-for-paas-customers"></a>Crittografia dei dati inattivi per i clienti PaaS

Piattaforma distribuita come servizio (PaaS) dati di un cliente si trova in genere in un ambiente di esecuzione di applicazioni e qualsiasi provider di risorse di Azure utilizzato toostore i dati dei clienti. crittografia hello toosee altre opzioni disponibili tooyou esamina la tabella di hello sotto per le piattaforme di archiviazione e l'applicazione hello in uso. Quando è supportato, vengono forniti collegamenti tooinstructions sull'abilitazione di crittografia per ogni provider di risorse. 

### <a name="encryption-at-rest-for-iaas-customers"></a>Crittografia dei dati inattivi per i clienti IaaS

I clienti IaaS (Infrastructure as a Service) possono avere un'ampia gamma di servizi e applicazioni in uso. I servizi IaaS possono abilitare la crittografia dei dati inattivi nelle macchine virtuali e nei dischi rigidi virtuali ospitati in Azure usando Crittografia dischi di Azure. 

#### <a name="encrypted-storage"></a>Archiviazione crittografata

Come le soluzioni PaaS, quelle IaaS possono sfruttare altri servizi di Azure che archiviano dati inattivi crittografati. In questi casi, è possibile abilitare hello crittografia al supporto tecnico di Rest fornito da ogni servizio di Azure utilizzato. Hello sotto la tabella enumera archiviazione principali hello, servizi e le piattaforme di applicazione e modello hello di crittografia supportato. Se supportato, vengono forniti collegamenti tooinstructions sull'abilitazione di crittografia. 

#### <a name="encrypted-compute"></a>Calcolo crittografato

Una crittografia completa soluzione di Rest richiede tale hello dati non vengono mai mantenuti in formato non crittografato. Mentre è in uso, in un hello caricamento server dati in memoria, dei dati possono essere persistente in locale in vari modi, tra cui file di paging di Windows hello, un dump di arresto anomalo del sistema e qualsiasi hello registrazione applicazione può eseguire. tooensure questi dati vengono crittografati a riposo IaaS utilizzabili dalle applicazioni Azure crittografia del disco su una macchina virtuale di Azure IaaS (Windows o Linux) e un disco virtuale. 

#### <a name="custom-encryption-at-rest"></a>Crittografia dei dati inattivi personalizzata

È consigliabile che, quando possibile, le applicazioni IaaS sfruttino Crittografia dischi di Azure e le opzioni di crittografia dei dati inattivi fornite da qualsiasi servizio di Azure in uso. In alcuni casi, ad esempio i requisiti di crittografia irregolari o archiviazione basato su non Azure, uno sviluppatore di un'applicazione IaaS potrebbe essere necessario crittografia tooimplement rest autonomamente. Gli sviluppatori di soluzioni IaaS possono ottimizzare l'integrazione con la gestione di Azure le aspettative dei clienti sfruttando determinati componenti di Azure. In particolare, gli sviluppatori devono usare hello insieme credenziali chiavi Azure servizio tooprovide chiave archiviazione protetta, nonché fornire ai clienti con le opzioni di gestione delle chiavi coerente con quella di Azure più servizi della piattaforma. Inoltre, soluzioni personalizzate devono utilizzare le chiavi di crittografia tooaccess account servizio tooenable Azure identità del servizio gestito. Per informazioni su Azure Key Vault e le identità dei servizi gestiti, vedere i rispettivi SDK.

## <a name="azure-resource-providers-encryption-model-support"></a>Supporto per il modello di crittografia dei provider di risorse di Azure

Servizi di Microsoft Azure ogni supportare uno o più di crittografia hello modelli rest. Per alcuni servizi, tuttavia, uno o più modelli di hello crittografia potrebbe non essere applicabili. I servizi possono inoltre rilasciare il supporto per questi scenari con pianificazioni diverse. In questa sezione descrive la crittografia di hello al supporto tecnico di rest in fase di hello della redazione del presente documento per ognuno dei servizi di archiviazione di dati di Azure principali hello.

### <a name="azure-disk-encryption"></a>Crittografia dischi di Azure

Tutti i clienti che usano le funzionalità IaaS (Infrastructure as a Service) di Azure possono ottenere la crittografia dei dati inattivi per le macchine virtuali IaaS e i dischi tramite Crittografia dischi di Azure. Per ulteriori informazioni sul disco di Azure crittografia vedere hello [documentazione di crittografia del disco Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

#### <a name="azure-storage"></a>Archiviazione di Azure

L'archiviazione BLOB e file di Azure supporta la crittografia dei dati inattivi per gli scenari di crittografia lato server, nonché i dati dei clienti crittografati (crittografia lato client).

- Lato server: i clienti che usano l'archiviazione BLOB di Azure possono abilitare la crittografia dei dati inattivi in ogni account della risorsa di archiviazione di Azure. Una volta abilitata la crittografia lato server viene eseguita in modo trasparente toohello applicazione. Per altre informazioni, vedere [Crittografia del servizio di archiviazione di Azure per dati inattivi](https://docs.microsoft.com/azure/storage/storage-service-encryption).
- Lato client: la crittografia lato client dei BLOB di Azure è supportata. Quando si utilizza la crittografia lato client clienti crittografare hello dati e caricare i dati blob crittografato hello. Gestione delle chiavi viene eseguita dal cliente hello. Per altre informazioni, vedere [Crittografia lato client e insieme di credenziali delle chiavi di Azure per Archiviazione di Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).


#### <a name="sql-azure"></a>SQL Azure

SQL Azure attualmente supporta la crittografia dei dati inattivi per gli scenari di crittografia sul lato client e sul lato del servizio gestito da Microsoft.

Server di supporto per la crittografia viene fornita tramite funzionalità SQL hello chiamato Transparent Data Encryption. Quando un cliente di SQL Azure abilita TDE, le chiavi vengono create e gestite automaticamente. Crittografia può essere abilitata a livello di database e server hello. A partire da giugno 2017, la funzionalità [Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx) sarà abilitata per impostazione predefinita nei nuovi database creati.

Crittografia client-side dei dati di SQL Azure è supportata tramite hello [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) funzionalità. Always Encrypted Usa una chiave creata e archiviata dal client hello. I clienti è possono archiviare la chiave master di hello in un archivio certificati di Windows, insieme di credenziali chiave di Azure o un modulo di protezione Hardware locale. Tramite SQL Server Management Studio, gli utenti SQL scelgono gli elementi chiave che preferiscono toouse tooencrypt la colonna.

|                                  |                |                     | **Modello di crittografia**             |                              |        |
|----------------------------------|----------------|---------------------|------------------------------|------------------------------|--------|
|                                  |                |                     |                              |                              | **Client** |
|                                  | **Gestione della chiave** | **Chiave gestita dal servizio** | **Gestita dal cliente nell'insieme di credenziali delle chiavi** | **Gestita dal cliente in locale** |        |
| **Archiviazione e database**            |                |                     |                              |                              |        |
| Disco (IaaS)                      |                | -                   | Sì                          | Sì*                         | -      |
| SQL Server (IaaS)                |                | Sì                 | Sì                          | Sì                          | Sì    |
| SQL Azure (PaaS)                 |                | Sì                 | Preview                      | -                            | Sì    |
| Archiviazione di Azure (BLOB di blocchi/pagine) |                | Sì                 | Preview                      | -                            | Sì    |
| Archiviazione di Azure (file)            |                | Sì                 | -                            | -                            | -      |
| Archiviazione di Azure (tabelle, code)   |                | -                   | -                            | -                            | Sì    |
| Cosmos DB (Document DB)          |                | Sì                 | -                            | -                            | -      |
| StorSimple                       |                | Sì                 | -                            | -                            | Sì    |
| Backup                           |                | -                   | -                            | -                            | Sì    |
| **Intelligence e analisi**       |                |                     |                              |                              |        |
| Data factory di Azure               |                | Sì                 | -                            | -                            | -      |
| Azure Machine Learning           |                | -                   | Preview                      | -                            | -      |
| Analisi di flusso di Azure           |                | Sì                 | -                            | -                            | -      |
| HDInsights (Archiviazione BLOB di Azure)  |                | Sì                 | -                            | -                            | -      |
| HDInsights (Archiviazione di Data Lake)   |                | Sì                 | -                            | -                            | -      |
| Archivio Azure Data Lake            |                | Sì                 | Sì                          | -                            | -      |
| Azure Data Catalog               |                | Sì                 | -                            | -                            | -      |
| Power BI                         |                | Sì                 | -                            | -                            | -      |
| **Servizi IoT**                     |                |                     |                              |                              |        |
| Hub IoT                          |                | -                   | -                            | -                            | Sì    |
| Bus di servizio                      |                | -              | -                            | -                            | Sì    |
| Hub eventi                       |                | -             | -                            | -                            | -      |


## <a name="conclusion"></a>Conclusioni

Protezione dei dati del cliente archiviati all'interno di servizi di Azure è di fondamentale importanza tooMicrosoft. Ospitato di Azure tutti i servizi sono commit tooproviding crittografia opzioni Rest. Servizi fondamentali come Archiviazione di Azure, SQL Azure e alcuni servizi di intelligence e analisi forniscono già opzioni di questo tipo. Alcuni di questi servizi supportano le chiavi controllate dal cliente e la crittografia lato client, nonché le chiavi e la crittografia gestite dal servizio. Servizi di Microsoft Azure sono ampiamente miglioramento della crittografia al momento della disponibilità Rest e nuove opzioni sono pianificate per l'anteprima e la disponibilità generale nei prossimi mesi di hello.

