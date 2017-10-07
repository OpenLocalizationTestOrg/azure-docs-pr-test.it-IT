---
title: aaaSensitive - modellazione strumento Microsoft Threat - dati Azure | Documenti Microsoft
description: misure di attenuazione esposte in hello strumento di modellazione del rischio di minacce per la
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 8a18f43af439241ba193ccf668971ddc4655355f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-sensitive-data--mitigations"></a>Infrastruttura di sicurezza: dati sensibili - Procedure di mitigazione 
| Prodotto o servizio | Articolo |
| --------------- | ------- |
| **Limite di Trust del computer** | <ul><li>[Assicurarsi che i file binari che contengono informazioni riservate vengano offuscati](#binaries-info)</li><li>[Considerare la possibilità di Encrypted File System (EFS) con dati specifici dell'utente riservate tooprotect utilizzato](#efs-user)</li><li>[Assicurarsi che siano crittografati i dati sensibili archiviati dall'applicazione hello nel file system di hello](#filesystem)</li></ul> | 
| **Applicazione Web** | <ul><li>[Verificare che contenuto riservato non è memorizzati nella cache del browser hello](#cache-browser)</li><li>[Crittografare le sezioni dei file di configurazione dell'app Web contenenti dati sensibili](#encrypt-data)</li><li>[Disabilitare in modo esplicito l'attributo HTML di completamento automatico hello in form sensibili e di input](#autocomplete-input)</li><li>[Verificare che i dati sensibili visualizzati sullo schermo dell'utente hello sono nascosta](#data-mask)</li></ul> | 
| **Database** | <ul><li>[Utenti implementano dati dinamici maschera l'esposizione dei dati sensibili toolimit non privilegiato](#dynamic-users)</li><li>[Assicurarsi che le password vengano archiviate in formato hash con valori salt](#salted-hash)</li><li>[Assicurarsi che i dati sensibili nelle colonne di database vengano crittografati](#db-encrypted)</li><li>[Assicurarsi che venga abilitata la crittografia a livello di database (TDE)](#tde-enabled)</li><li>[Assicurarsi che i backup di database vengano crittografati](#backup)</li></ul> | 
| **API Web** | <ul><li>[Verificare che tooWeb pertinenti dati sensibili che API non viene archiviato nel servizio di archiviazione del browser](#api-browser)</li></ul> | 
| Azure DocumentDB | <ul><li>[Crittografare i dati sensibili archiviati in DocumentDB](#encrypt-docdb)</li></ul> | 
| **Limite di trust della macchina virtuale IaaS di Azure** | <ul><li>[Utilizzare dischi tooencrypt di crittografia del disco di Azure usati dalle macchine virtuali](#disk-vm)</li></ul> | 
| **Limite di trust di Service Fabric** | <ul><li>[Crittografare i segreti nelle applicazioni di Service Fabric](#fabric-apps)</li></ul> | 
| **Dynamics CRM** | <ul><li>[Eseguire la modellazione di sicurezza e usare team e unità aziendali quando richiesto](#modeling-teams)</li><li>[Ridurre al minimo la funzionalità di accesso tooshare sulle entità critico](#entities)</li><li>[Formazione degli utenti in hello rischi associati alla funzionalità di Dynamics CRM condivisione hello e procedure di protezione avanzata](#good-practices)</li><li>[Includere una regola sugli standard di sviluppo che vieta la visualizzazione dei dettagli di configurazione nella gestione delle eccezioni](#exception-mgmt)</li></ul> | 
| **Archiviazione di Azure** | <ul><li>[Usare Crittografia del servizio di archiviazione di Azure per dati inattivi (anteprima)](#sse-preview)</li><li>[Utilizzare i dati sensibili toostore crittografia lato Client in archiviazione di Azure](#client-storage)</li></ul> | 
| **Client per dispositivi mobili** | <ul><li>[Crittografare dati sensibili o informazioni personali scritti toophones di archiviazione locale](#pii-phones)</li><li>[Nascondendo i file binari generati prima di distribuire agli utenti di tooend](#binaries-end)</li></ul> | 
| **WCF** | <ul><li>[Set clientCredentialType tooCertificate o Windows](#cert)</li><li>[WCF: la modalità di sicurezza non è abilitata](#security)</li></ul> | 

## <a id="binaries-info"></a>Assicurarsi che i file binari che contengono informazioni riservate vengano offuscati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust dei computer | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Assicurarsi che vengano offuscati i file binari che contengono informazioni riservate, come segreti commerciali o logica di business riservata che non deve essere sottoposta a reverse engineering. Si tratta di toostop reverse engineering degli assembly. A questo scopo, è possibile usare strumenti come `CryptoObfuscator`. |

## <a id="efs-user"></a>Considerare la possibilità di Encrypted File System (EFS) con dati specifici dell'utente riservate tooprotect utilizzato

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust dei computer | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Considerare la possibilità di Encrypted File System (EFS) con dati specifici dell'utente riservati tooprotect utilizzati da avversari con computer toohello accesso fisico. |

## <a id="filesystem"></a>Assicurarsi che siano crittografati i dati sensibili archiviati dall'applicazione hello nel file system di hello

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust dei computer | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Assicurarsi che siano crittografati i dati sensibili archiviati dall'applicazione hello nel file system di hello (ad esempio, tramite DPAPI), se non è possibile applicare EFS |

## <a id="cache-browser"></a>Verificare che contenuto riservato non è memorizzati nella cache del browser hello

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, Web Form, MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | I browser possono archiviare informazioni per motivi di memorizzazione nella cache e cronologia. Questi file memorizzati nella cache vengono archiviati in una cartella, come cartella dei file temporanei Internet hello in caso di hello di Internet Explorer. Quando queste pagine sono definite nuovamente, browser hello leggerle dalla cache. Se le informazioni riservate sono visualizzato toohello utente (ad esempio, i relativi indirizzo, i dettagli della carta di credito, numero di previdenza sociale o nome utente), quindi queste informazioni potrebbero essere archiviate nella cache del browser e pertanto recuperabili tramite l'analisi della cache del browser hello o semplicemente premendo pulsante "Indietro" del browser hello. Imposta valore dell'intestazione cache-control risposta troppo "no-store" per tutte le pagine. |

### <a name="example"></a>Esempio
```XML
<configuration>
  <system.webServer>
   <httpProtocol>
    <customHeaders>
        <add name="Cache-Control" value="no-cache" />
        <add name="Pragma" value="no-cache" />
        <add name="Expires" value="-1" />
    </customHeaders>
  </httpProtocol>
 </system.webServer>
</configuration>
```

### <a name="example"></a>Esempio
Per l'implementazione è possibile usare un filtro. È possibile usare l'esempio seguente: 
```C#
public override void OnActionExecuting(ActionExecutingContext filterContext)
        {
            if (filterContext == null || (filterContext.HttpContext != null && filterContext.HttpContext.Response != null && filterContext.HttpContext.Response.IsRequestBeingRedirected))
            {
                //// Since this is MVC pipeline, this should never be null.
                return;
            }

            var attributes = filterContext.ActionDescriptor.GetCustomAttributes(typeof(System.Web.Mvc.OutputCacheAttribute), false);
            if (attributes == null || **Attributes**.Count() == 0)
            {
                filterContext.HttpContext.Response.Cache.SetNoStore();
                filterContext.HttpContext.Response.Cache.SetCacheability(HttpCacheability.NoCache);
                filterContext.HttpContext.Response.Cache.SetExpires(DateTime.UtcNow.AddHours(-1));
                if (!filterContext.IsChildAction)
                {
                    filterContext.HttpContext.Response.AppendHeader("Pragma", "no-cache");
                }
            }

            base.OnActionExecuting(filterContext);
        }
``` 

## <a id="encrypt-data"></a>Crittografare le sezioni dei file di configurazione dell'app Web contenenti dati sensibili

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Procedura: Crittografare sezioni di configurazione in ASP.NET 2.0 tramite DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [specificando un Provider di configurazione protetta](https://msdn.microsoft.com/library/68ze1hb2.aspx), [i segreti dell'applicazione di tooprotect utilizzando insieme credenziali chiavi di Azure](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Passaggi** | File di configurazione, ad esempio hello Web. config, sono spesso appSettings. JSON usato toohold informazioni sensibili, inclusi i nomi utente, password, le stringhe di connessione di database e le chiavi di crittografia. Se non proteggere queste informazioni, l'applicazione è vulnerabile tooattackers o gli utenti malintenzionati di ottenere informazioni riservate, ad esempio nomi di account utente e password, i nomi di database e server. Basato sul tipo di distribuzione hello (azure/locale), crittografare sezioni di sensibili hello del file di configurazione usando DPAPI o servizi come insieme di credenziali chiave di Azure. |

## <a id="autocomplete-input"></a>Disabilitare in modo esplicito l'attributo HTML di completamento automatico hello in form sensibili e di input

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN: autocomplete attribute](http://msdn.microsoft.com/library/ms533486(VS.85).aspx) (Attributo autocomplete), [Using AutoComplete in HTML Forms](http://msdn.microsoft.com/library/ms533032.aspx) (Uso di AutoComplete nei form HTML), [Vulnerabilità legata alla disinfezione del contenuto HTML](http://technet.microsoft.com/security/bulletin/MS10-071), [Autocomplete...again?!](http://blog.mindedsecurity.com/2011/10/autocompleteagain.html) (Ancora autocomplete?) |
| **Passaggi** | attributo autocomplete Hello specifica se un modulo deve avere il completamento automatico o disattivare. Quando il completamento automatico è attiva, hello browser completa automaticamente i valori in base ai valori utente hello immesso prima. Ad esempio, quando viene immesso un nuovo nome e una password in un form e form hello viene inviato, browser hello chiede se password hello deve essere salvata. Successivamente quando viene visualizzato il modulo di hello, hello nome e password vengono compilati automaticamente o vengono completati man mano che verrà immessi nome hello. Un utente malintenzionato con accesso locale è stato possibile ottenere la password come testo non crittografato hello dalla cache di hello browser. Il completamento automatico è abilitato per impostazione predefinita e deve essere disabilitato in modo esplicito. |

### <a name="example"></a>Esempio
```C#
<form action="Login.aspx" method="post " autocomplete="off" >
      Social Security Number: <input type="text" name="ssn" />
      <input type="submit" value="Submit" />    
</form>
```

## <a id="data-mask"></a>Verificare che i dati sensibili visualizzati sullo schermo dell'utente hello sono nascosta

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Dati sensibili, ad esempio password, numeri di carta di credito, SSN e così via. devono essere mascherati quando viene visualizzato nella schermata di hello. Si tratta di personale tooprevent non autorizzati di accedere ai dati hello (ad esempio, shoulder esplorazione password, il personale di supporto la visualizzazione di un numero di utenti SSN). Assicurarsi che questi elementi di dati non siano visibili come testo normale e vengano mascherati in modo appropriato. Ciò ha toobe preso in considerazione durante l'accettazione di essi come input (ad esempio. tipo di input = "password") e la visualizzazione torna nella schermata di hello (ad esempio, Visualizza solo hello ultime 4 cifre del numero di carta di credito hello). |

## <a id="dynamic-users"></a>Utenti implementano dati dinamici maschera l'esposizione dei dati sensibili toolimit non privilegiato

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | SQL Azure, locale |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: 12, versione SQL: MSSQL2016 |
| **Riferimenti**              | [Maschera dati dinamica](https://msdn.microsoft.com/library/mt130841) |
| **Passaggi** | scopo di Hello della maschera dati dinamica è toolimit l'esposizione dei dati sensibili, impedendo agli utenti che non dovrebbero avere accesso ai dati toohello visualizzazione. La maschera dati dinamica non mira agli utenti del database tooprevent la connessione diretta toohello database ed eseguire query complete che espongano parti dei dati sensibili hello. La maschera dati dinamica è complementare tooother funzionalità sicurezza di SQL Server (il controllo, crittografia, protezione livello di riga...) e si consiglia di toouse questa funzionalità in combinazione con le inoltre in ordine toobetter proteggere i dati sensibili hello hello database. Si noti che questa funzionalità è supportata unicamente da SQL Server, a partire dalla versione 2016, e dal database SQL di Azure. |

## <a id="salted-hash"></a>Assicurarsi che le password vengano archiviate in formato hash con valori salt

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Hash delle password con le API di crittografia di .NET](http://docs.asp.net/en/latest/security/data-protection/consumer-apis/password-hashing.html) |
| **Passaggi** | Le password non devono essere archiviate in database dell'archivio utenti personalizzati. Gli hash delle password devono invece essere archiviati con valori salt. Verificare che il salt hello utente hello è sempre univoco e si applica b crypt, s crypt o PBKDF2 prima di archiviare password hello, con un conteggio di iterazione minimo lavoro fattore di 150.000 cicli il possibilità hello tooeliminate dell'utilizzo forzato del bruta.| 

## <a id="db-encrypted"></a>Assicurarsi che i dati sensibili nelle colonne di database vengano crittografati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: tutte |
| **Riferimenti**              | [Crittografia di dati sensibili in SQL Server](https://technet.microsoft.com/library/ff848751(v=sql.105).aspx), [Procedura: Crittografare una colonna di dati in SQL Server](https://msdn.microsoft.com/library/ms179331), [Crittografare con un certificato](https://msdn.microsoft.com/library/ms188061) |
| **Passaggi** | I dati sensibili, ad esempio numeri di carta di credito sono crittografato nel database di hello toobe. Dati possono essere crittografati usando la crittografia a livello di colonna o da una funzione di applicazione utilizzando funzioni di crittografia hello. |

## <a id="tde-enabled"></a>Assicurarsi che venga abilitata la crittografia a livello di database (TDE)

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Informazioni su Transparent Data Encryption (TDE) in SQL Server](https://technet.microsoft.com/library/bb934049(v=sql.105).aspx) |
| **Passaggi** | Transparent Data Encryption (TDE) funzionalità in SQL server consente di crittografare i dati sensibili in un database e proteggere le chiavi di hello che vengono utilizzati tooencrypt hello dati con un certificato. Ciò consente di evitare senza chiavi hello utilizzando i dati di hello. Transparent Data Encryption protegge i dati "non operativi", vale a dire il file di log e dati hello. Fornisce hello possibilità toocomply con numerose leggi, normative e linee guida stabilite in vari settori. |

## <a id="backup"></a>Assicurarsi che i backup di database vengano crittografati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | SQL Azure, locale |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: 12, versione SQL: MSSQL2014 |
| **Riferimenti**              | [Crittografia dei backup del database SQL](https://msdn.microsoft.com/library/dn449489) |
| **Passaggi** | SQL Server dispone di dati di hello possibilità tooencrypt hello durante la creazione di un backup. Specificando l'algoritmo di crittografia hello e hello di componente di crittografia (certificato o chiave asimmetrica) durante la creazione di un backup, uno può creare un file di backup crittografato. |

## <a id="api-browser"></a>Verificare che tooWeb pertinenti dati sensibili che API non viene archiviato nel servizio di archiviazione del browser

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | Provider di identità: AD FS, provider di identità: Azure AD |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>In alcune implementazioni, autenticazione tooWeb pertinenti elementi sensibili dell'API vengono archiviati nella memoria locale del browser. Si tratta, ad esempio, di elementi di autenticazione di Azure AD come adal.idtoken, adal.nonce.idtoken, adal.access.token.key, adal.token.keys, adal.state.login, adal.session.state, adal.expiration.key e così via.</p><p>Tutti questi elementi sono disponibili anche dopo la disconnessione o la chiusura del browser. Un avversario ottiene accesso elementi toothese, se possibile riutilizzare le risorse protetta hello tooaccess (API). Assicurarsi che tutti gli elementi sensibili correlati tooWeb API non è archiviato nel servizio di archiviazione del browser. Nei casi in cui è inevitabile archiviazione lato client (ad esempio, singola pagina applicazioni (SPA) che sfruttano i flussi implicita OpenIdConnect/OAuth necessario toostore localmente i token di accesso), utilizzare le opzioni di archiviazione con non hanno una persistenza. ad esempio, preferire SessionStorage tooLocalStorage.</p>| 

### <a name="example"></a>Esempio
Hello frammento di codice JavaScript proviene da una libreria di autenticazione personalizzato che archivia elementi di autenticazione nel servizio di archiviazione locale. Evitare le implementazioni di questo tipo. 
```javascript
ns.AuthHelper.Authenticate = function () {
window.config = {
instance: 'https://login.microsoftonline.com/',
tenant: ns.Configurations.Tenant,
clientId: ns.Configurations.AADApplicationClientID,
postLogoutRedirectUri: window.location.origin,
cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
};
```

## <a id="encrypt-docdb"></a>Crittografare i dati sensibili archiviati in Cosmos DB

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Azure DocumentDB | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Crittografare i dati sensibili a livello dell'applicazione prima di archiviarli in DocumentDB o in altre soluzioni di archiviazione come Archiviazione di Azure o SQL Azure.| 

## <a id="disk-vm"></a>Utilizzare dischi tooencrypt di crittografia del disco di Azure usati dalle macchine virtuali

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust della macchina virtuale IaaS di Azure | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Utilizzando la crittografia del disco di Azure tooencrypt dischi utilizzano da macchine virtuali](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) |
| **Passaggi** | <p>Crittografia dischi di Azure è una nuova funzionalità attualmente in anteprima. Questa funzionalità permette di dischi del sistema operativo di tooencrypt hello e i dischi di dati utilizzati da una macchina virtuale IaaS. Per Windows, hello unità vengono crittografate mediante la tecnologia di crittografia BitLocker standard del settore. Per Linux, dischi hello vengono crittografati mediante la tecnologia hello Crypt di data mining. Questo è integrato con insieme credenziali chiavi Azure tooallow è toocontrol e gestire chiavi di crittografia disco hello. Hello soluzioni di crittografia del disco di Azure supporta hello tre scenari di crittografia seguenti:</p><ul><li>Abilitare la crittografia in nuove VM IaaS create da file VHD crittografati dal cliente e chiavi di crittografia fornite dal cliente, che vengono archiviate nell'insieme di credenziali delle chiavi di Azure.</li><li>Abilitare la crittografia in nuove macchine virtuali IaaS creato da hello Azure Marketplace.</li><li>Abilitare la crittografia delle VM IaaS esistenti già in esecuzione in Azure.</li></ul>| 

## <a id="fabric-apps"></a>Crittografare i segreti nelle applicazioni di Service Fabric

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust di Service Fabric | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Ambiente: Azure |
| **Riferimenti**              | [Gestione dei segreti nelle applicazioni di Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-application-secret-management/) |
| **Passaggi** | I segreti possono essere informazioni riservate, ad esempio le stringhe di connessione di archiviazione, le password o altri valori che non devono essere gestiti in testo normale. Utilizzare insieme credenziali chiavi Azure toomanage chiavi e segreti applicazioni di servizio dell'infrastruttura. |

## <a id="modeling-teams"></a>Eseguire la modellazione di sicurezza e usare team e unità aziendali quando richiesto

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Eseguire la modellazione di sicurezza e usare team e unità aziendali quando richiesto. |

## <a id="entities"></a>Ridurre al minimo la funzionalità di accesso tooshare sulle entità critico

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Ridurre al minimo la funzionalità di accesso tooshare sulle entità critico |

## <a id="good-practices"></a>Formazione degli utenti in hello rischi associati alla funzionalità di Dynamics CRM condivisione hello e procedure di protezione avanzata

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Formazione degli utenti in hello rischi associati alla funzionalità di Dynamics CRM condivisione hello e procedure di protezione avanzata |

## <a id="exception-mgmt"></a>Includere una regola sugli standard di sviluppo che vieta la visualizzazione dei dettagli di configurazione nella gestione delle eccezioni

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Includere una regola sugli standard di sviluppo che vieta la visualizzazione dei dettagli di configurazione nella gestione delle eccezioni al di fuori del contesto di sviluppo. Testare tale regola come parte di revisioni del codice o ispezioni periodiche.|

## <a id="sse-preview"></a>Usare Crittografia del servizio di archiviazione di Azure per dati inattivi (anteprima)

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipo di archiviazione: BLOB |
| **Riferimenti**              | [Crittografia del servizio di archiviazione di Azure per dati inattivi (anteprima)](https://azure.microsoft.com/documentation/articles/storage-service-encryption/) |
| **Passaggi** | <p>Azure Storage Service crittografia (SSE) per i dati inattivi consente di proteggere e tutelare toomeet i dati, la sicurezza dell'organizzazione e impegni di conformità. Con questa funzionalità, di archiviazione di Azure automaticamente crittografa il toostorage toopersisting precedente dei dati e decrittografa tooretrieval precedente. Hello crittografia, decrittografia e gestione chiavi toousers completamente trasparente. SSE si applica solo tooblock i BLOB, BLOB di pagine e BLOB di aggiunta. Hello altri tipi di dati, inclusi tabelle, code e i file, non verranno crittografati.</p><p>Flusso di lavoro di crittografia e decrittografia:</p><ul><li>cliente Hello abilita la crittografia sull'account di archiviazione hello</li><li>Quando il cliente hello scrive nuova archiviazione tooBlob dei dati (PUT Blob, inserire blocco, PUT Page e così via); ogni operazione di scrittura viene crittografato con crittografia AES a 256 bit, uno dei hello più forti crittografie a blocchi disponibili</li><li>Quando il cliente hello deve dati tooaccess (GET Blob e così via), dati vengono automaticamente decrittografati prima della restituzione toohello utente</li><li>Se la crittografia è disabilitata, nuove scritture non vengono più crittografate e i dati crittografati esistenti rimangano crittografati fino a quando non riscritto da utente hello. Mentre la crittografia è abilitata, verrà crittografati scritture tooBlob archiviazione. non modifica lo stato di Hello dei dati utente hello passando tra l'abilitazione/disabilitazione della crittografia per l'account di archiviazione hello</li><li>Tutte le chiavi di crittografia vengono archiviate, crittografate e gestite da Microsoft.</li></ul><p>Si noti che in questo momento, chiavi di crittografia di hello hello siano gestite da Microsoft. Microsoft genera chiavi di hello originariamente e gestire l'archiviazione sicura hello di chiavi hello nonché rotazione regolare hello come definito dai criteri di Microsoft interno. In futuro hello, clienti otterranno hello possibilità toomanage i propri > chiavi di crittografia e fornire un percorso di migrazione dalle chiavi di gestione di Microsoft gestito toocustomer le chiavi.</p>| 

## <a id="client-storage"></a>Utilizzare i dati sensibili toostore crittografia lato Client in archiviazione di Azure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Crittografia lato client e Azure Key Vault per Archiviazione di Microsoft Azure](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/), [Esercitazione: Crittografare e decrittografare i BLOB in Archiviazione di Microsoft Azure tramite Azure Key Vault](https://azure.microsoft.com/documentation/articles/storage-encrypt-decrypt-blobs-key-vault/), [Storing Data Securely in Azure Blob Storage with Azure Encryption Extensions](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/06/17/storing-data-securely-in-azure-blob-storage-with-azure-encryption-extensions/) (Archiviazione protetta dei dati nell'archivio BLOB di Azure con le estensioni di crittografia di Azure) |
| **Passaggi** | <p>Hello Azure Storage Client Library per il pacchetto Nuget .NET supporta la crittografia dei dati all'interno delle applicazioni client prima di caricare tooAzure Storage e la decrittografia dei dati durante il download toohello client. libreria Hello supporta inoltre l'integrazione con l'insieme di credenziali chiave di Azure per la gestione di chiave account di archiviazione. Ecco una breve descrizione del funzionamento della crittografia lato client:</p><ul><li>Hello Azure Storage client SDK genera una chiave di crittografia del contenuto (CEK), che è una chiave simmetrica con un utilizzo</li><li>I dati del cliente vengono crittografati con la chiave CEK.</li><li>Hello CEK viene eseguito il wrapping (crittografata) con chiave di crittografia della chiave hello (CHIAVI). Hello KEK è identificato da un identificatore di chiave e può essere una coppia di chiavi asimmetriche o di una chiave simmetrica e possono essere gestito in locale o memorizzato nell'insieme di credenziali chiave di Azure. client di archiviazione Hello stesso non ha mai accesso toohello KEK. Richiama solo l'algoritmo di wrapping delle chiavi hello fornito dall'insieme di credenziali chiave. I clienti possono scegliere toouse provider personalizzati per la chiave di ritorno a capo/annullamento del wrapping se desiderano</li><li>Hello dati crittografati viene quindi caricato toohello servizio di archiviazione di Azure. Controllo dei collegamenti hello nella sezione dei riferimenti hello per i dettagli di implementazione di basso livello.</li></ul>|

## <a id="pii-phones"></a>Crittografare dati sensibili o informazioni personali scritti toophones di archiviazione locale

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Client per dispositivi mobili | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, Xamarin  |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Gestire impostazioni e funzionalità nei dispositivi con i criteri di Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#create-a-configuration-policy), [Keychain Valet](https://components.xamarin.com/view/square.valet) |
| **Passaggi** | <p>Se un'applicazione hello scrive informazioni riservate, ad esempio informazioni personali dell'utente (posta elettronica, numero di telefono, nome, cognome, preferenze e così via) -nel file system di mobile, quindi deve essere crittografato prima della scrittura toohello file system locale. Se un'applicazione hello è un'applicazione aziendale, quindi esaminare il possibilità di hello di pubblicazione dell'applicazione con Windows Intune.</p>|

### <a name="example"></a>Esempio
È possibile configurare Intune con i seguenti criteri toosafeguard dati riservati: 
```C#
Require encryption on mobile device    
Require encryption on storage cards
Allow screen capture
```

### <a name="example"></a>Esempio
Se non è un'applicazione aziendale, quindi utilizzare platform fornito keystore, un'applicazione hello portachiavi toostore chiavi di crittografia tramite l'operazione di crittografia possono eseguire nel file system di hello. Il codice seguente frammento di codice viene illustrato come chiave tooaccess keychain con xamarin: 
```C#
        protected static string EncryptionKey
        {
            get
            {
                if (String.IsNullOrEmpty(_Key))
                {
                    var query = new SecRecord(SecKind.GenericPassword);
                    query.Service = NSBundle.MainBundle.BundleIdentifier;
                    query.Account = "UniqueID";

                    NSData uniqueId = SecKeyChain.QueryAsData(query);
                    if (uniqueId == null)
                    {
                        query.ValueData = NSData.FromString(System.Guid.NewGuid().ToString());
                        var err = SecKeyChain.Add(query);
                        _Key = query.ValueData.ToString();
                    }
                    else
                    {
                        _Key = uniqueId.ToString();
                    }
                }

                return _Key;
            }
        }
```

## <a id="binaries-end"></a>Nascondendo i file binari generati prima di distribuire agli utenti di tooend

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Client per dispositivi mobili | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Crypto Obfuscation For .Net](http://www.ssware.com/cryptoobfuscator/obfuscator-net.htm) |
| **Passaggi** | Generato i file binari (assembly all'interno di file apk) devono essere offuscato toostop reverse engineering degli assembly. Strumenti come `CryptoObfuscator` possono essere utilizzati per questo scopo. |

## <a id="cert"></a>Set clientCredentialType tooCertificate o Windows

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | Mediante un UsernameToken con una password non crittografata tramite un canale non crittografato espone hello password tooattackers che possono individuare i messaggi SOAP hello. I provider di servizi che utilizzano hello UsernameToken potrebbe accettare le password inviate in testo non crittografato. Invio password non crittografate tramite un canale non crittografato, è possibile esporre hello credenziali tooattackers che è possibile analizzare il messaggio SOAP hello. | 

### <a name="example"></a>Esempio
Hello seguente configurazione di provider del servizio WCF utilizza hello UsernameToken: 
```
<security mode="Message"> 
<message clientCredentialType="UserName" />
``` 
Impostare clientCredentialType tooCertificate o Windows. 

## <a id="security"></a>WCF: la modalità di sicurezza non è abilitata

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | Modalità di sicurezza: trasporto, modalità di sicurezza: messaggio |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html), [CoDe Magazine: Fundamentals of WCF Security](http://www.codemag.com/article/0611051) (Concetti fondamentali sulla sicurezza in WCF) |
| **Passaggi** | Non è stata definita alcuna sicurezza del trasporto o del messaggio. Applicazioni che trasmettono messaggi senza trasporto o messaggio di sicurezza non può garantire l'integrità di hello e la riservatezza dei messaggi hello. Quando un'associazione di sicurezza WCF è impostata tooNone, trasporto e messaggio di sicurezza sono disabilitati. |

### <a name="example"></a>Esempio
Hello seguente set di configurazione tooNone modalità di sicurezza hello. 
```
<system.serviceModel> 
  <bindings> 
    <wsHttpBinding> 
      <binding name=""MyBinding""> 
        <security mode=""None""/> 
      </binding> 
  </bindings> 
</system.serviceModel> 
```

### <a name="example"></a>Esempio
Le associazioni ai servizi presentano cinque modalità di sicurezza possibili: 
* None. Disabilita la sicurezza. 
* Transport. Usa la sicurezza del trasporto per la protezione reciproca del messaggio e dell'autenticazione. 
* Message. Usa la sicurezza del messaggio per la protezione reciproca del messaggio e dell'autenticazione. 
* Both. Consente di toosupply impostazioni per il trasporto e sicurezza a livello di messaggio (solo MSMQ è supportata). 
* TransportWithMessageCredential. Le credenziali vengono passate con la protezione dei messaggi e il messaggio hello e autenticazione server sono fornite dal livello di trasporto hello. 
* TransportCredentialOnly. Le credenziali del client vengono passate con livello di trasporto hello e non viene applicata alcuna protezione del messaggio. Utilizzare il trasporto e messaggio di sicurezza tooprotect hello l'integrità e riservatezza dei messaggi. configurazione di Hello seguente indica sicurezza del trasporto hello servizio toouse con le credenziali del messaggio.
```
<system.serviceModel>
  <bindings>
    <wsHttpBinding>
    <binding name=""MyBinding""> 
    <security mode=""TransportWithMessageCredential""/> 
    <message clientCredentialType=""Windows""/> 
    </binding> 
  </bindings> 
</system.serviceModel> 
```
