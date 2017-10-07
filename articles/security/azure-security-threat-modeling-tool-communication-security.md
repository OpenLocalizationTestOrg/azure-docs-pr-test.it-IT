---
title: Sicurezza - modellazione strumento Microsoft Threat - Azure aaaCommunication | Documenti Microsoft
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
ms.openlocfilehash: 667829c75123f4dbe0b383fdaf8cd899802f9b16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-communication-security--mitigations"></a>Infrastruttura di sicurezza: sicurezza della comunicazione - Procedure di mitigazione 
| Prodotto o servizio | Articolo |
| --------------- | ------- |
| **Hub eventi di Azure** | <ul><li>[Comunicazioni protette tooEvent Hub utilizzando SSL/TLS](#comm-ssltls)</li></ul> |
| **Dynamics CRM** | <ul><li>[Controllare i privilegi e verificare che hello personalizzato servizi o delle pagine ASP.NET rispettano sicurezza del CRM account del servizio](#priv-aspnet)</li></ul> |
| **Data factory di Azure** | <ul><li>[Utilizzare il gateway di gestione di dati durante la connessione sul Server SQL locale tooAzure Data Factory](#sqlserver-factory)</li></ul> |
| **Identity Server** | <ul><li>[Verificare che tutto il traffico tooIdentity Server con connessione HTTPS](#identity-https)</li></ul> |
| **Applicazione Web** | <ul><li>[Verificare i certificati x. 509 utilizzato le connessioni SSL, TLS e DTLS tooauthenticate](#x509-ssltls)</li><li>[Configurare il certificato SSL per un dominio personalizzato nel servizio app di Azure](#ssl-appservice)</li><li>[Forzare tutto il traffico tooAzure servizio App tramite connessione HTTPS](#appservice-https)</li><li>[Abilitare HTTP Strict Transport Security (HSTS)](#http-hsts)</li></ul> |
| **Database** | <ul><li>[Verificare la crittografia della connessione e la convalida dei certificati di SQL Server](#sqlserver-validation)</li><li>[Forzare Encrypted comunicazione tooSQL server](#encrypted-sqlserver)</li></ul> |
| **Archiviazione di Azure** | <ul><li>[Verificare che tooAzure comunicazione che spazio di archiviazione è su HTTPS](#comm-storage)</li><li>[Convalidare l'hash MD5 dopo il download di BLOB se non è possibile abilitare HTTPS](#md5-https)</li><li>[Utilizzare SMB 3.0 client compatibile tooensure tooAzure crittografia dati condivisioni File in transito](#smb-shares)</li></ul> |
| **Client per dispositivi mobili** | <ul><li>[Implementare l'associazione del certificato](#cert-pinning)</li></ul> |
| **WCF** | <ul><li>[Abilitare HTTPS: canale di trasporto sicuro](#https-transport)</li><li>[WCF: TooEncryptAndSign livello di protezione messaggio Set sicurezza](#message-protection)</li><li>[WCF: Utilizzare un account con privilegi minimi di toorun il servizio WCF](#least-account-wcf)</li></ul> |
| **API Web** | <ul><li>[Forzare tutto il traffico tooWeb API tramite connessione HTTPS](#webapi-https)</li></ul> |
| **Cache Redis di Azure** | <ul><li>[Verificare che tooAzure di comunicazione che della Cache Redis è su SSL](#redis-ssl)</li></ul> |
| **Gateway IoT sul campo** | <ul><li>[Proteggere le comunicazioni di Gateway tooField dispositivo](#device-field)</li></ul> |
| **Gateway IoT cloud** | <ul><li>[Proteggere i dispositivi tooCloud comunicazione Gateway mediante SSL/TLS](#device-cloud)</li></ul> |

## <a id="comm-ssltls"></a>Comunicazioni protette tooEvent Hub utilizzando SSL/TLS

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Hub eventi di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Panoramica del modello di sicurezza e autenticazione di Hub eventi](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Passaggi** | Proteggere le connessioni AMQP o HTTP tooEvent Hub utilizzando SSL/TLS |

## <a id="priv-aspnet"></a>Controllare i privilegi e verificare che hello personalizzato servizi o delle pagine ASP.NET rispettano sicurezza del CRM account del servizio

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Controllare i privilegi e verificare che hello personalizzato servizi o delle pagine ASP.NET rispettano sicurezza del CRM account del servizio |

## <a id="sqlserver-factory"></a>Utilizzare il gateway di gestione di dati durante la connessione sul Server SQL locale tooAzure Data Factory

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Data factory di Azure | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipi di servizio collegato: locale e Azure |
| **Riferimenti**              |[Spostamento di dati tra origini locali e Azure Data Factory](https://azure.microsoft.com/documentation/articles/data-factory-move-data-between-onprem-and-cloud/#create-gateway), [Gateway di gestione dati](https://azure.microsoft.com/documentation/articles/data-factory-data-management-gateway/) |
| **Passaggi** | <p>lo strumento di Gateway di gestione dati (DMG) Hello è obbligatorio tooconnect toodata origini protette dietro un firewall o corpnet.</p><ol><li>Il blocco macchina hello isola strumento DMG hello ed evita che programmi dannosi o snooping nel computer di origine dati hello non funziona correttamente. Ad esempio, in caso di installazione degli ultimi aggiornamenti, abilitazione delle porte necessarie minime, provisioning degli account controllati, abilitazione del controllo e della crittografia dei dischi e così via.</li><li>Chiave del Gateway dati deve essere ruotato a intervalli frequenti o ogni volta che rinnova password account del servizio DMG hello</li><li>I transiti di dati attraverso il servizio di collegamento devono essere crittografati.</li></ol> |

## <a id="identity-https"></a>Verificare che tutto il traffico tooIdentity Server con connessione HTTPS

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [IdentityServer3 - Keys, Signatures and Cryptography](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html) (IdentityServer3 - Chiavi, firme e crittografia), [IdentityServer3 - Deployment](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) (IdentityServer3 - Distribuzione) |
| **Passaggi** | Per impostazione predefinita, IdentityServer richiede tutti toocome le connessioni in ingresso tramite HTTPS. È assolutamente obbligatorio che per la comunicazione con IdentityServer vengano usati esclusivamente trasporti protetti. In alcuni scenari di distribuzione, come l'offload SSL, questo requisito può essere meno rigido. Hello identità pagina Server di distribuzione riferimenti hello per ulteriori informazioni, vedere. |

## <a id="x509-ssltls"></a>Verificare i certificati x. 509 utilizzato le connessioni SSL, TLS e DTLS tooauthenticate

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Le applicazioni che utilizzano SSL, TLS e DTLS devono verificare completamente i certificati x. 509 hello di entità hello a che si connettono. Ciò include la verifica dei certificati di hello per:</p><ul><li>Nome di dominio</li><li>Date di validità (date sia di inizio che di scadenza)</li><li>Stato di revoca</li><li>Utilizzo (ad esempio, autenticazione server per i server o autenticazione client per i client)</li><li>Catena di certificati. I certificati devono essere concatenato tooa autorità di certificazione radice (CA) attendibile dalla piattaforma hello o configurato in modo esplicito dall'amministratore di hello</li><li>La lunghezza della chiave pubblica del certificato deve essere superiore a 2048 bit</li><li>L'algoritmo di hash deve essere SHA256 o versione superiore |

## <a id="ssl-appservice"></a>Configurare il certificato SSL per un dominio personalizzato nel servizio app di Azure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipo di ambiente: Azure |
| **Riferimenti**              | [Abilitare HTTPS per un'app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/) |
| **Passaggi** | Per impostazione predefinita, Azure già Abilita HTTPS per tutte le applicazioni con un certificato con caratteri jolly per hello *. dominio azurewebsites.net. Come tutti i domini con caratteri jolly, tuttavia, non è sicuro quanto un dominio personalizzato con un proprio certificato ([riferimento](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/)). È consigliabile tooenable SSL per il dominio personalizzato di hello si accederà quale app hello distribuito tramite|

## <a id="appservice-https"></a>Forzare tutto il traffico tooAzure servizio App tramite connessione HTTPS

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipo di ambiente: Azure |
| **Riferimenti**              | [Abilitare HTTPS nel servizio app di Azure]https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/#4-enforce-https-on-your-app) |
| **Passaggi** | <p>Anche se Azure già Abilita HTTPS per i servizi di app di Azure con un certificato con caratteri jolly per il dominio hello *. azurewebsites.net, non applicano HTTPS. I visitatori possono comunque accedere app hello tramite HTTP, che può compromettere la sicurezza dell'applicazione hello e pertanto HTTPS ha toobe applicati in modo esplicito. Le applicazioni ASP.NET MVC devono utilizzare hello [filtro RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) che impone un toobe di richiesta HTTP non protette nuovamente inviate tramite HTTPS.</p><p>In alternativa, modulo URL Rewrite hello, incluso in Azure App Service può essere utilizzato tooenforce HTTPS. URL Rewrite module consente regole toodefine sviluppatori tooincoming applicato richieste prima che le richieste di hello passate tooyour applicazione. Regole di riscrittura dell'URL vengono definite in un file Web. config archiviato nella directory radice dell'applicazione hello hello</p>|

### <a name="example"></a>Esempio
esempio Hello contiene una regola di riscrittura dell'URL che forza tutti in ingresso toouse il traffico HTTPS
```XML
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
Questa regola funziona tramite la restituzione di un codice di stato HTTP di 301 (reindirizzamento permanente) quando utente hello richiede una pagina utilizzando HTTP. Hello reindirizzamenti 301 hello richiesta toohello stesso URL visitatore hello richiesto, ma sostituisce hello HTTP parte della richiesta di hello con HTTPS. Ad esempio, HTTP://contoso.com sarebbe tooHTTPS://contoso.com reindirizzato. 

## <a id="http-hsts"></a>Abilitare HTTP Strict Transport Security (HSTS)

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Foglio informativo di OWASP su HTTP Strict Transport Security](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) |
| **Passaggi** | <p>Sicurezza di trasporto Strict HTTP (HSTS) è un miglioramento della sicurezza opt-in specificato da un'applicazione web tramite l'utilizzo di hello di un'intestazione di risposta speciale. Una volta un browser supportato riceve questa intestazione tale browser impedirà tutte le comunicazioni tramite dominio specificato toohello HTTP e invierà invece tutte le comunicazioni tramite HTTPS. Impedisce anche i messaggi di richiesta con click-through HTTPS nei browser.</p><p>tooimplement HSTS, hello dopo l'intestazione della risposta è toobe configurato a livello globale, per un sito Web nel codice o nel file di configurazione. Sicurezza di trasporto Strict: max-age = 300; includeSubDomains HSTS concepito per hello seguenti rischi:</p><ul><li>Utente segnalibri o manualmente tipi http://example.com ed è l'autore dell'attacco man-in-the-middle tooa soggetto: HSTS reindirizza automaticamente tooHTTPS le richieste HTTP per il dominio di destinazione hello</li><li>Applicazione Web di è previsto toobe esclusivamente HTTPS inavvertitamente contiene collegamenti HTTP o serve contenuto su HTTP: HSTS reindirizza automaticamente tooHTTPS le richieste HTTP per il dominio di destinazione hello</li><li>Un attacco man-in-the-middle tenta toointercept traffico da un utente di vittima utilizzando un certificato non valido e spera utente hello accetterà certificato non valido di hello: HSTS non consente un messaggio di utente toooverride hello certificato non valido</li></ul>|

## <a id="sqlserver-validation"></a>Verificare la crittografia della connessione e la convalida dei certificati di SQL Server

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | SQL Azure  |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: 12 |
| **Riferimenti**              | [Best Practices on Writing Secure Connection Strings for SQL Database](http://social.technet.microsoft.com/wiki/contents/articles/2951.windows-azure-sql-database-connection-security.aspx#best) (Procedure consigliate per la scrittura di stringhe di connessione sicure per il database SQL) |
| **Passaggi** | <p>Tutte le comunicazioni tra il database SQL e un'applicazione client vengono crittografate usando sempre Secure Sockets Layer (SSL). Il database SQL non supporta connessioni non crittografate. i certificati toovalidate con il codice dell'applicazione o gli strumenti, in modo esplicito richiedere una connessione crittografata e non attendibili i certificati del server hello. Se il codice dell'applicazione o gli strumenti non richiedono una connessione crittografata, riceveranno comunque connessioni crittografate.</p><p>Tuttavia, potrebbero non convalidare i certificati del server hello e pertanto saranno soggetti ad troppo attacchi "man in intermedio hello". i certificati toovalidate con codice dell'applicazione ADO.NET, impostare `Encrypt=True` e `TrustServerCertificate=False` nella stringa di connessione database hello. certificati toovalidate tramite SQL Server Management Studio, aprire la finestra di dialogo di hello Connetti tooServer. Fare clic su Crittografa connessione nella scheda Proprietà connessione hello</p>|

## <a id="encrypted-sqlserver"></a>Forzare Encrypted comunicazione tooSQL server

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Locale |
| **Attributes (Attributi) (Attributi)**              | Versione SQL: MsSQL2016, MsSQL2012, MsSQL2014 |
| **Riferimenti**              | [Abilitare connessioni crittografate toohello motore di Database](https://msdn.microsoft.com/library/ms191192)  |
| **Passaggi** | Abilitazione di SSL crittografia aumenta la sicurezza hello dei dati trasmessi in rete tra le istanze di SQL Server e applicazioni. |

## <a id="comm-storage"></a>Verificare che tooAzure comunicazione che spazio di archiviazione è su HTTPS

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Crittografia a livello di trasporto in Archiviazione di Azure: uso di HTTPS](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_encryption-in-transit) |
| **Passaggi** | sicurezza hello tooensure di archiviazione di Azure dei dati in transito, utilizzare sempre il protocollo HTTPS hello quando la chiamata API REST hello o accede agli oggetti nel servizio di archiviazione. Inoltre, firme di accesso condiviso, che può essere utilizzato toodelegate accedere agli oggetti di archiviazione tooAzure, includono un'opzione toospecify tale hello solo quando si usano firme di accesso condiviso, assicurando che chiunque l'invio di collegamenti con i token di firma di accesso condiviso verrà è possibile utilizzare il protocollo HTTPS Utilizzare il protocollo corretto hello.|

## <a id="md5-https"></a>Convalidare l'hash MD5 dopo il download di BLOB se non è possibile abilitare HTTPS

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipo di archiviazione: BLOB |
| **Riferimenti**              | [Windows Azure Blob MD5 Overview](https://blogs.msdn.microsoft.com/windowsazurestorage/2011/02/17/windows-azure-blob-md5-overview/) (Panoramica di MD5 nel servizio BLOB di Microsoft Azure) |
| **Passaggi** | <p>Il servizio Blob di Windows Azure fornisce l'integrità dei dati tooensure meccanismi sia un'applicazione hello e livelli di trasporto. Se per qualsiasi motivo è necessario toouse HTTP anziché HTTPS e si lavora con i BLOB in blocchi, è possibile utilizzare il controllo MD5 toohelp verificare l'integrità di hello del BLOB hello trasferiti</p><p>Ciò contribuisce a proteggere dagli errori a livello di rete/trasporto, ma non necessariamente dalle violazioni. Se è possibile utilizzare HTTPS, che fornisce la protezione a livello di trasporto, il controllo MD5 è ridondante e superfluo.</p>|

## <a id="smb-shares"></a>Utilizzare le condivisioni File SMB 3.0 client compatibile tooensure dati in transito crittografia tooAzure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Client per dispositivi mobili | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipo di archiviazione: file |
| **Riferimenti**              | [Archiviazione file di Azure](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/#comment-2529238931), [Supporto di SMB in Archiviazione file di Azure per client Windows](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/#_mount-the-file-share) |
| **Passaggi** | Archiviazione di File di Azure supporta HTTPS, quando si utilizza l'API REST di hello, ma è più comunemente utilizzati come una condivisione file SMB collegato tooa macchina virtuale. SMB 2.1 non supporta la crittografia, pertanto le connessioni sono consentite solo all'interno di hello stessa area in Azure. Tuttavia, SMB 3.0 supporta la crittografia e può essere utilizzato con Windows Server 2012 R2, Windows 8, Windows 8.1 e Windows 10, consentendo tra aree di accesso e anche l'accesso sul desktop hello. |

## <a id="cert-pinning"></a>Implementare l'associazione del certificato

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, Windows Phone |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Associazione del certificato e della chiave pubblica](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#.Net) |
| **Passaggi** | <p>L'associazione del certificato protegge da attacchi man-in-the-middle. Il blocco è il processo di hello di associazione di un host con i relativi X509 previsto certificato o chiave pubblica. Una volta che un certificato o chiave pubblica è nota o visualizzata per un host, hello certificato o una chiave pubblica è toohello associato o 'bloccato' host. </p><p>Di conseguenza, quando un avversario tenta toodo attacco MITM SSL, durante la chiave di hello handshake SSL dal server dell'utente malintenzionato sarà diversa dalla hello aggiunto la chiave del certificato e verrà annullata richiesta hello, evitando pertanto certificato MITM il blocco può essere ottenuto implementazione del ServicePointManager `ServerCertificateValidationCallback` delegato.</p>|

### <a name="example"></a>Esempio
```C#
using System;
using System.Net;
using System.Net.Security;
using System.Security.Cryptography;

namespace CertificatePinningExample
{
    class CertificatePinningExample
    {
        /* Note: In this example, we're hardcoding a hello certificate's public key and algorithm for 
           demonstration purposes. In a real-world application, this should be stored in a secure
           configuration area that can be updated as needed. */

        private static readonly string PINNED_ALGORITHM = "RSA";

        private static readonly string PINNED_PUBLIC_KEY = "3082010A0282010100B0E75B7CBE56D31658EF79B3A1" +
            "294D506A88DFCDD603F6EF15E7F5BCBDF32291EC50B2B82BA158E905FE6A83EE044A48258B07FAC3D6356AF09B2" +
            "3EDAB15D00507B70DB08DB9A20C7D1201417B3071A346D663A241061C151B6EC5B5B4ECCCDCDBEA24F051962809" +
            "FEC499BF2D093C06E3BDA7D0BB83CDC1C2C6660B8ECB2EA30A685ADE2DC83C88314010FFC7F4F0F895EDDBE5C02" +
            "ABF78E50B708E0A0EB984A9AA536BCE61A0C31DB95425C6FEE5A564B158EE7C4F0693C439AE010EF83CA8155750" +
            "09B17537C29F86071E5DD8CA50EBD8A409494F479B07574D83EDCE6F68A8F7D40447471D05BC3F5EAD7862FA748" +
            "EA3C92A60A128344B1CEF7A0B0D94E50203010001";


        public static void Main(string[] args)
        {
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create("https://azure.microsoft.com");
            request.ServerCertificateValidationCallback = (sender, certificate, chain, sslPolicyErrors) =>
            {
                if (certificate == null || sslPolicyErrors != SslPolicyErrors.None)
                {
                    // Error getting certificate or hello certificate failed basic validation
                    return false;
                }

                var targetKeyAlgorithm = new Oid(certificate.GetKeyAlgorithm()).FriendlyName;
                var targetPublicKey = certificate.GetPublicKeyString();
                
                if (targetKeyAlgorithm == PINNED_ALGORITHM &&
                    targetPublicKey == PINNED_PUBLIC_KEY)
                {
                    // Success, hello certificate matches hello pinned value.
                    return true;
                }
                // Reject, either hello key or hello algorithm does not match hello expected value.
                return false;
            };

            try
            {
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine($"Success, HTTP status code: {response.StatusCode}");
            }
            catch(Exception ex)
            {
                Console.WriteLine($"Failure, {ex.Message}");
            }
            Console.WriteLine("Press any key tooend.");
            Console.ReadKey();
        }
    }
}
```

## <a id="https-transport"></a>Abilitare HTTPS: canale di trasporto sicuro

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | configurazione dell'applicazione Hello è necessario assicurarsi che per tutte le informazioni di accesso toosensitive viene utilizzato HTTPS.<ul><li>**Spiegazione:** se un'applicazione gestisce le informazioni riservate e non utilizza la crittografia a livello di messaggio, quindi deve essere consentito solo toocommunicate su un canale di trasporto crittografati.</li><li>**RACCOMANDAZIONI:** verificare che il trasporto HTTP sia disabilitato e abilitare invece il trasporto HTTPS. Ad esempio, sostituire hello `<httpTransport/>` con `<httpsTransport/>` tag. Non fare affidamento su un tooguarantee (firewall) di configurazione di rete che è possibile accedere all'applicazione hello solo tramite un canale sicuro. Da un punto di vista filosofiche, un'applicazione hello non deve dipendere rete hello per la protezione.</li></ul><p>Dal punto di vista pratico, persone hello responsabile per la protezione di rete hello non rileva sempre i requisiti di sicurezza hello di un'applicazione hello evoluzione.</p>|

## <a id="message-protection"></a>WCF: TooEncryptAndSign livello di protezione messaggio Set sicurezza

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff650862.aspx) |
| **Passaggi** | <ul><li>**Spiegazione:** quando il livello di protezione è impostato troppo "none", verrà disattivata la protezione dei messaggi. La riservatezza e l'integrità si ottengono con il livello di impostazione appropriato.</li><li>**RACCOMANDAZIONI:**<ul><li>Quando `Mode=None`, la protezione dei messaggi è disabilitata</li><li>Quando `Mode=Sign` -firma ma non consente di crittografare il messaggio hello; deve essere utilizzata quando l'integrità dei dati è importante</li><li>Quando `Mode=EncryptAndSign` -segni e crittografa il messaggio hello</li></ul></li></ul><p>Provare a disattivare la crittografia e solo quando è necessario solo l'integrità di hello toovalidate delle informazioni di hello senza preoccuparsi della riservatezza, la firma del messaggio. Questo può risultare utile per le operazioni o i contratti di servizio in cui è necessario mittente originale di hello toovalidate ma non contiene dati sensibili vengono trasmessi. Quando si riduce il livello di protezione hello, assicurarsi che il messaggio hello non contiene eventuali informazioni identificabili personalmente (PII).</p>|

### <a name="example"></a>Esempio
Configurazione servizio hello e hello operazione tooonly firma hello messaggio risulta hello seguono esempi. Esempio di contratto di servizio di `ProtectionLevel.Sign`: hello seguito è riportato un esempio di utilizzo ProtectionLevel.Sign a livello di contratto di servizio hello: 
```
[ServiceContract(Protection Level=ProtectionLevel.Sign] 
public interface IService 
  { 
  string GetData(int value); 
  } 
```

### <a name="example"></a>Esempio
Esempio di contratto di operazione di `ProtectionLevel.Sign` (per un controllo granulare): hello seguito è riportato un esempio di utilizzo `ProtectionLevel.Sign` in hello OperationContract livello:

```
[OperationContract(ProtectionLevel=ProtectionLevel.Sign] 
string GetData(int value);
``` 

## <a id="least-account-wcf"></a>WCF: Utilizzare un account con privilegi minimi di toorun il servizio WCF

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648826.aspx ) |
| **Passaggi** | <ul><li>**SPIEGAZIONE:** non eseguire i servizi WCF con un account amministratore o con privilegi elevati, che comporterebbe un alto impatto in caso di compromissione dei servizi.</li><li>**INDICAZIONI:** utilizzare un account con privilegi minimi di toohost il WCF service perché ridurre la superficie di attacco dell'applicazione e ridurre il danno potenziale hello se dell'attacco. Se l'account del servizio hello richiede ulteriori diritti di accesso sulle risorse di infrastruttura, ad esempio MSMQ, hello delle autorizzazioni appropriate del registro eventi, contatori delle prestazioni e hello file system, è necessario assegnare le risorse toothese in modo che sia possibile eseguire il servizio WCF hello correttamente.</li></ul><p>Se il servizio deve tooaccess specifiche risorse per conto del chiamante originale hello, utilizzare la rappresentazione e identità del chiamante hello tooflow di delega per un controllo delle autorizzazioni a valle. In uno scenario di sviluppo, utilizzare l'account del servizio di hello rete locale, ovvero un account predefinito speciale che dispone di privilegi ridotti. In uno scenario di produzione, creare un account di servizio del dominio personalizzato con privilegi minimi.</p>|

## <a id="webapi-https"></a>Forzare tutto il traffico tooWeb API tramite connessione HTTPS

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Imporre SSL in un controller di API Web](http://www.asp.net/web-api/overview/security/working-with-ssl-in-web-api) |
| **Passaggi** | Se un'applicazione è HTTPS sia un'associazione HTTP, i client possono comunque in grado di utilizzare HTTP tooaccess hello sito. tooprevent questa operazione, utilizzare un tooensure filtro azione che richiede tooprotected API sono sempre tramite HTTPS.|

### <a name="example"></a>Esempio 
Hello codice seguente viene illustrato un filtro di autenticazione API Web che verifica la presenza di SSL: 
```C#
public class RequireHttpsAttribute : AuthorizationFilterAttribute
{
    public override void OnAuthorization(HttpActionContext actionContext)
    {
        if (actionContext.Request.RequestUri.Scheme != Uri.UriSchemeHttps)
        {
            actionContext.Response = new HttpResponseMessage(System.Net.HttpStatusCode.Forbidden)
            {
                ReasonPhrase = "HTTPS Required"
            };
        }
        else
        {
            base.OnAuthorization(actionContext);
        }
    }
}
```
Aggiungere questo filtro tooany API Web le azioni che richiedono SSL: 
```C#
public class ValuesController : ApiController
{
    [RequireHttps]
    public HttpResponseMessage Get() { ... }
}
```
 
## <a id="redis-ssl"></a>Verificare che tooAzure di comunicazione che della Cache Redis è su SSL

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Cache Redis di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Supporto per SSL in Redis di Azure](https://azure.microsoft.com/documentation/articles/cache-faq/#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis) |
| **Passaggi** | Redis server non supporta SSL predefinito hello, a differenza Cache Redis di Azure. Se ci si connette tooAzure Cache Redis e il client supporta SSL, ad esempio stackexchange. Redis, è necessario utilizzare SSL. Per impostazione predefinita, la porta non SSL è disabilitata per le nuove istanze di Cache Redis di Azure. Verificare che le impostazioni predefinite protette hello non vengano modificate a meno che non è presente una dipendenza sul supporto SSL per i client redis. |

Si noti che Redis è progettato toobe accessibili ai client attendibili all'interno di ambienti attendibili. Ciò significa che in genere non è una buona idea hello tooexpose Redis istanza direttamente toohello internet o, in generale, ambiente tooan direttamente accessibile ai client non attendibili hello la porta TCP Redis o socket UNIX. 

## <a id="device-field"></a>Proteggere le comunicazioni di Gateway tooField dispositivo

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT sul campo | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Per i dispositivi basata su IP, il protocollo di comunicazione hello in genere può essere incapsulato in una data di tooprotect canale SSL/TLS in transito. Per altri protocolli che non supportano SSL/TLS, verificare se sono presenti versioni sicure di protocollo hello che forniscono la sicurezza a livello di trasporto o messaggio. |

## <a id="device-cloud"></a>Proteggere i dispositivi tooCloud comunicazione Gateway mediante SSL/TLS

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT cloud | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Scegliere il protocollo di comunicazione](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#messaging) |
| **Passaggi** | Proteggere i protocolli HTTP/AMQP e MQTT con SSL/TLS. |
