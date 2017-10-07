---
title: gateway dati locale aaaOn | Documenti Microsoft
description: "Un gateway locale è necessario se il server Analysis Services in Azure si connetta a origini dati locali tooon."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a>La connessione a origini dati locali tooon con Gateway dati locale in Azure
gateway dati locale di Hello funge da bridge per consentire il trasferimento protetto dei dati tra origini dati locali e i server di Analysis Services di Azure nel cloud hello. In aggiunta tooworking con più server di Azure Analysis Services in hello stessa area, una versione più recente di hello del gateway hello funziona anche con Microsoft Flow, Power BI, le app di Power e App Azure per la logica. È possibile associare più servizi in hello stessa area con un singolo gateway. 

 Azure Analysis Services richiede una risorsa per il gateway in hello stessa area. Ad esempio, se sono presenti server di Analysis Services di Azure nell'area Stati Uniti orientali 2 hello, è necessario una risorsa gateway nell'area Stati Uniti orientali 2 hello. Più server negli Stati Uniti orientali 2 possono utilizzare hello stesso gateway.

Ottenere il programma di installazione con hello gateway hello prima volta è un processo composto da quattro parti:

- **Scaricare ed eseguire il programma di installazione**: questo passaggio consente di installare un servizio gateway su un computer all'interno dell'organizzazione.

- **Registrare il gateway** : In questo passaggio, si specifica un nome e la chiave per il gateway, ripristino e selezionare un'area, registrare il gateway con hello servizio Cloud Gateway.

- **Creare una risorsa per il gateway in Azure**: in questo passaggio, si crea una risorsa per il gateway nella sottoscrizione di Azure.

- **Connettere il server gateway tooyour** -dopo aver creato una risorsa gateway nella sottoscrizione, è possibile avviare la connessione tooit del server.

Dopo aver creato una risorsa per il gateway configurata per la sottoscrizione, è possibile connettersi a più server e tooit altri servizi. Solo necessario tooinstall un diverso gateway e creare risorse aggiuntive gateway se si dispone di server o altri servizi in un'area diversa.

tooget adesso, vedere [installare e configurare il gateway dati locale](analysis-services-gateway-install.md).

## <a name="how-it-works"> </a>Funzionamento
gateway Hello installare in un computer dell'organizzazione viene eseguito come un servizio Windows, **gateway dati locale**. Questo servizio locale è registrato con il servizio Cloud Gateway tramite Azure Service Bus hello. È quindi possibile creare una servizio Cloud della risorsa per il gateway per la sottoscrizione di Azure. I servizi di Azure Analysis Server vengono quindi connessi tooyour risorsa per il gateway. Quando i modelli in tooyour di tooconnect necessario il server locale origini dati per le query o elaborazione, una query e i dati del flusso attraversa hello gateway risorsa, Azure Service Bus, hello il servizio gateway dati locale e le origini dati. 

![Funzionamento](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

Query e flusso di dati:

1. Una query viene creata dal servizio cloud di hello con credenziali crittografato hello per l'origine dati locale di hello. È quindi inviato coda tooa per tooprocess gateway hello.
2. il servizio cloud gateway Hello analizza query hello e inserisce hello richiesta toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).
3. gateway dati locale di Hello esegue il polling hello Azure Service Bus per le richieste in sospeso.
4. gateway Hello Ottiene hello query, decrittografa le credenziali di hello e si connette a origini dati toohello con tali credenziali.
5. gateway Hello invia hello query toohello origine per l'esecuzione.
6. Hello risultati vengono inviati dall'origine dati hello, gateway toohello nascosto e quindi al servizio cloud hello e il server.

## <a name="windows-service-account"></a>Account del servizio Windows
gateway dati locale Hello è configurato toouse *NT SERVICE\PBIEgwService* per le credenziali di accesso servizio Windows hello. Per impostazione predefinita, ha hello diritto di accesso come servizio; nel contesto di hello del computer hello che si sta installando il gateway di hello in. Questa credenziale non è hello stesso account utilizzato tooconnect tooon locale origini o l'account di Azure.  

Se si verificano problemi con il server proxy scadenza tooauthentication, potrebbe essere necessario toochange utente di dominio tooa account del servizio di Windows hello o gestiti account del servizio.

## <a name="ports"> </a>Porte
gateway Hello crea un tooAzure di connessione in uscita Bus di servizio. Comunica sulle porte in uscita seguenti: TCP 443 (impostazione predefinita), 5671, 5672 e da 9350 a 9354.  gateway Hello non richiede porte in ingresso.

È consigliabile indirizzi IP whitelist hello per l'area dati nel firewall. È possibile scaricare hello [dell'elenco indirizzi IP di Data Center di Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). L'elenco viene aggiornato ogni settimana.

> [!NOTE]
> gli indirizzi IP di Hello nell'elenco di IP dei Data Center Azure hello sono in notazione CIDR. Ad esempio, 10.0.0.0/24 non significa da 10.0.0.0 a 10.0.0.24. Altre informazioni su hello [la notazione CIDR](http://whatismyipaddress.com/cidr).
>
>

di seguito Hello sono nomi di dominio completo hello usati dal gateway hello.

| Nomi di dominio | Porte in uscita | Descrizione |
| --- | --- | --- |
| *.powerbi.com |80 |Programma di installazione hello toodownload usato HTTP. |
| *.powerbi.com |443 |HTTPS |
| *. analysis.windows.net |443 |HTTPS |
| *.login.windows.net |443 |HTTPS |
| *.servicebus.windows.net |5671-5672 |Advanced Message Queuing Protocol (AMQP) |
| *.servicebus.windows.net |443, 9350-9354 |Listener in Inoltro del Bus di servizio su TCP (richiede 443 per l'acquisizione del token di Controllo di accesso) |
| *.frontend.clouddatahub.net |443 |HTTPS |
| *.core.windows.net |443 |HTTPS |
| login.microsoftonline.com |443 |HTTPS |
| *.msftncsi.com |443 |Utilizzare la connettività internet tootest se hello gateway non è raggiungibile dal servizio Power BI hello. |
| *.microsoftonline-p.com |443 |Usato per l'autenticazione, a seconda della configurazione. |

### <a name="force-https"></a>Forzare la comunicazione HTTPS con il bus di servizio di Azure
È possibile forzare hello gateway toocommunicate con il Bus di servizio di Azure tramite HTTPS anziché diretta TCP; Tuttavia, in tal modo possono rallentare le prestazioni. È possibile modificare hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file modificando il valore di hello da `AutoDetect` troppo`Https`. Questo file si trova solitamente in *C:\Programmi\On-premises data gateway*.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <a name="faq"></a>Domande frequenti

### <a name="general"></a>Generale

**Domande e**: è necessario un gateway per le origini dati nel cloud hello, ad esempio Database di SQL Azure? <br/>
**R**: No. Un gateway si connette a origini dati locali tooon solo.

**Domande e**: gateway hello dispone toobe installato hello stesso computer come origine dati hello? <br/>
**R**: No. gateway Hello stabilisce la connessione origine dati toohello utilizzando le informazioni di connessione hello fornito. Prendere in considerazione gateway hello come un'applicazione client in questo senso. Hello gateway deve semplicemente hello funzionalità tooconnect toohello nome del server che è stato specificato, in genere su hello stessa rete.

<a name="why-azure-work-school-account"></a>

**Domande e**: perché è necessario un lavoro toouse o dell'istituto di istruzione toosign account in? <br/>
**Oggetto**: È possibile utilizzare un lavoro di Azure o scuola account quando si installa gateway dati locale di hello. L'account di accesso viene archiviato in un tenant gestito da Azure Active Directory (Azure AD). Nome dell'entità utente dell'account di Azure AD (UPN) corrisponde in genere, indirizzo di posta elettronica hello.

**D**: Dove sono archiviate le credenziali? <br/>
**Oggetto**: credenziali hello immesse per un'origine dati vengono crittografate e archiviate nel servizio Cloud Gateway hello. le credenziali di Hello vengono decrittografate nel gateway dati locale di hello.

**D**: Sono previsti requisiti per la larghezza di banda della rete? <br/>
**R**: È consigliabile che la connessione di rete abbia una buona velocità effettiva. Ogni ambiente è diverso e quantità hello di invio di dati influisce sui risultati di hello. Uso di ExpressRoute può contribuire a tooguarantee un livello di velocità effettiva tra sedi locali e hello Data Center di Azure.
È possibile utilizzare hello dello strumento di terze parti Azure Speed Test app toohelp misuratore la velocità effettiva.

**Domande e**: che cos'è la latenza di hello per le query tooa dati di origine in esecuzione dal gateway hello? Che cos'è l'architettura migliore hello? <br/>
**Oggetto**: tooreduce latenza di rete, installare hello gateway come origine dati toohello Chiudi possibili. Se è possibile installare il gateway di hello sull'origine dati effettivi hello, la prossimità riduce la latenza di hello introdotta. Prendere in considerazione i Data Center hello troppo. Ad esempio, se il servizio utilizza hello Data Center di Stati Uniti occidentali e SQL Server è ospitato in una macchina virtuale di Azure, la macchina virtuale di Azure deve essere in Stati Uniti occidentali hello troppo. Questo prossimità riduce la latenza ed evitare addebiti in uscita sulla macchina virtuale di Azure hello.

**Domande e**: come vengono inviati risultati toohello indietro cloud? <br/>
**Oggetto**: risultati vengono inviati tramite hello Azure Service Bus.

**Domande e**: sono presenti eventuali gateway toohello le connessioni in ingresso dal cloud hello? <br/>
**R**: No. gateway di Hello Usa le connessioni in uscita tooAzure Bus di servizio.

**D**: Cosa accade se si bloccano le connessioni in uscita? Cosa devo tooopen? <br/>
**Oggetto**: Vedere porte hello e gli host che hello Usa gateway.

**Domande e**: ciò che viene chiamato il servizio Windows effettivo di hello?<br/>
**Oggetto**: In servizi, gateway hello viene chiamato il servizio gateway dati locale.

**Domande e**: possibile hello servizio gateway di Windows eseguito con un account Azure Active Directory? <br/>
**R**: No. servizio Windows Hello deve avere un account Windows valido. Per impostazione predefinita, il servizio di hello viene eseguito con hello SID del servizio, NT SERVICE\PBIEgwService.

### <a name="high-availability"></a>Disponibilità elevata e ripristino di emergenza

**D**: Quali opzioni sono disponibili per il ripristino di emergenza? <br/>
**Oggetto**: È possibile utilizzare toorestore chiave di ripristino hello o spostare un gateway. Quando si installa il gateway di hello, specificare la chiave di ripristino hello.

**Domande e**: che cos'è il vantaggio di hello della chiave di ripristino hello? <br/>
**Oggetto**: chiave di ripristino hello fornisce un modo toomigrate o ripristinare le impostazioni del gateway dopo un'emergenza.

## <a name="troubleshooting"> </a>Risoluzione dei problemi

**Domande e**: come è possibile vedere quali sono le query vengono inviate toohello origine di dati locale? <br/>
**Oggetto**: È possibile abilitare la traccia di query, che include le query hello che vengono inviate. Tenere presente che query toochange risalendo toohello valore originale al termine della risoluzione dei problemi. Se il tracciamento delle query non viene disabilitato, si creeranno dei log più grandi.

È anche possibile usare gli strumenti per il tracciamento delle query di cui è dotata l'origine dati. Ad esempio, è possibile usare Eventi estesi o SQL Profiler per SQL Server e Analysis Services.

**Domande e**: dove sono i registri di gateway hello? <br/>
**R**: Vedere la sezione Registri più avanti in questo argomento.

### <a name="update"></a>Aggiornare la versione più recente di toohello

Molti problemi possono verificarsi quando la versione di gateway hello diventa obsoleta. Come buona pratica, assicurarsi di utilizzare la versione più recente di hello. Se è stato aggiornato gateway hello per un mese o più, si potrebbe si consiglia di installare una versione più recente di hello del gateway hello e verificare se è possibile riprodurre il problema di hello.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Errore: Impossibile tooadd utente toogroup. (Utenti log delle prestazioni -2147463168 PBIEgwService)

È possibile che venga visualizzato questo errore se si tenta di gateway di hello tooinstall in un controller di dominio che non è supportato. Assicurarsi di distribuire gateway hello in un computer che non è un controller di dominio.

## <a name="logs"></a>Log

I file di log sono di fondamentale importanza per la risoluzione dei problemi.

#### <a name="enterprise-gateway-service-logs"></a>Log del servizio gateway Enterprise

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a>Log di configurazione

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a>Log eventi

È possibile trovare il Gateway di gestione di dati e PowerBIGateway registri in hello **registri applicazioni e servizi**.


## <a name="telemetry"></a>Telemetria
La telemetria può essere usata per il monitoraggio e la risoluzione dei problemi. Per impostazione predefinita

**tooturn telemetria**

1.  Controllare hello On-premises data gateway nella directory sul hello computer. In genere è **%unitàsistema%\Programmi\Gateway dati locale**. Oppure, è possibile aprire una console dei servizi e verificare hello percorso tooexecutable: una proprietà del servizio gateway dati locale di hello.
2.  Nel file di Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config hello dalla directory del client. Modificare hello SendTelemetry impostazione tootrue.
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  Salvare le modifiche e riavviare il servizio di Windows hello: il servizio gateway dati locale.




## <a name="next-steps"></a>Passaggi successivi
* [Gestire Analysis Services](analysis-services-manage.md)
* [Ottenere dati da Azure Analysis Services](analysis-services-connect.md)
