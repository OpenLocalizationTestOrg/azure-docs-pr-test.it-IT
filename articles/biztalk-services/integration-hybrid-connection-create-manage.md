---
title: aaaCreate e gestire connessioni ibride | Documenti Microsoft
description: Informazioni come la gestione connessione hello toocreate una connessione ibrida e installare hello Hybrid Connection Manager. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a>Creare e gestire connessioni ibride

> [!IMPORTANT]
> La funzionalità Connessioni ibride di BizTalk è stata ritirata e sostituita dalla funzionalità Connessioni ibride del Servizio app. Per ulteriori informazioni, incluso come toomanage le connessioni ibride di BizTalk esistente, vedere [le connessioni ibride di servizio App di Azure](../app-service/app-service-hybrid-connections.md).


## <a name="overview-of-hello-steps"></a>Panoramica dei passaggi di hello
1. Creare una connessione ibrida immettendo hello **nome host** o **FQDN** della risorsa locale hello nella rete privata.
2. Collegare App web di Azure o App per dispositivi mobili Azure toohello connessione ibrida.
3. Installare hello Hybrid Connection Manager nella risorsa locale e connettere toohello connessione ibrida. Hello portale di Azure fornisce un tooinstall esperienza con clic singolo e connettersi.
4. Gestire le connessioni ibride e le relative chiavi di connessione.

Questi passaggi sono illustrati in questo argomento. 

> [!IMPORTANT]
> È possibile tooset un indirizzo IP di connessione ibrida endpoint tooan. Se si utilizza un indirizzo IP, è possibile o potrebbero non raggiungere risorsa locale hello, a seconda del client. la connessione ibrida Hello dipende da client hello eseguendo una ricerca DNS. Nella maggior parte dei casi, hello **client** è il codice dell'applicazione. Se hello client non esegue una ricerca DNS, (non tenta l'indirizzo IP hello tooresolve come se fosse un nome di dominio (x.x.x. x)), quindi il traffico non verrà inviato tramite la connessione ibrida hello.
> 
> Ad esempio (pseudocodice), è possibile definire **10.4.5.6** come host locale:
> 
> **Hello works scenario seguente:**  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> **non funziona Hello seguente scenario:**  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <a name="CreateHybridConnection"></a>Creare una connessione ibrida
Una connessione ibrida può essere creata in hello portale Azure usando le app Web **o** utilizzo dei servizi BizTalk. 

**le connessioni ibride con le applicazioni Web toocreate**, vedere [tooan App Web di Azure connettersi risorsa locale](../app-service-web/web-sites-hybrid-connection-get-started.md). È anche possibile installare hello Hybrid Connection Manager (HCM) dall'app web, che rappresenta il metodo preferito di hello. 

**le connessioni ibride in servizi BizTalk toocreate**:

1. Accedi toohello [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Nel riquadro di spostamento a sinistra di hello, selezionare **servizi BizTalk** e quindi selezionare il BizTalk Service. 
   
    Se non ne esiste già uno, è possibile [creare un servizio BizTalk](biztalk-provision-services.md).
3. Seleziona hello **connessioni ibride** scheda:  
   ![scheda per le connessioni ibride][HybridConnectionTab]
4. Selezionare **creare una connessione ibrida** o seleziona hello **aggiungere** pulsante nella barra delle applicazioni hello. Immettere hello seguente:
   
   | Proprietà | Descrizione |
   | --- | --- |
   | Nome |Hello connessione ibrida nome deve essere univoco e non può essere hello stesso nome come hello BizTalk Service. È possibile inserire qualsiasi nome, ma è consigliabile sceglierne uno che descriva lo scopo specifico. Ecco alcuni esempi: <br/><br/>Payroll*SQLServer*<br/>SupplyList*SharepointServer*<br/>Customers*OracleServer* |
   | Nome host |Immettere nome host completo hello, solo hello nome host o indirizzo IPv4 della risorsa locale hello hello. Tra gli esempi sono inclusi:<br/><br/>SQLServerUtente<br/>*mySQLServer*.*Domain*.corp.*yourCompany*.com<br/>*myHTTPSharePointServer*<br/>*myHTTPSharePointServer*.*yourCompany*.com<br/>10.100.10.10<br/><br/>Se si usa l'indirizzo IPv4 hello, si noti che il codice client o un'applicazione potrebbe non risolvere l'indirizzo IP hello. Vedere hello importante nota nella parte superiore di hello di questo argomento. |
   | Porta |Immettere il numero di porta hello della risorsa locale hello. Ad esempio, se si usa App Web, immettere la porta 80 o 443. Se si usa SQL Server, immettere la porta 1433. |
5. Selezionare il programma di installazione di hello segno di spunta toocomplete hello. 

#### <a name="additional"></a>Informazioni aggiuntive
* È possibile creare più connessioni ibride. Vedere hello [servizi BizTalk: grafico edizioni](biztalk-editions-feature-chart.md) per il numero di connessioni consentite hello. 
* Ogni connessione ibrida viene creata con una coppia di stringhe di connessione: chiavi dell’applicazione per SEND e chiavi locali per LISTEN. Ogni coppia ha una chiave primaria e una chiave secondaria. 

## <a name="LinkWebSite"></a>Collegare un'app per dispositivi mobili o un'App Web del Servizio app di Azure
Selezionare toolink un'App Web o App per dispositivi mobili in Azure App Service tooan esistente, la connessione ibrida **utilizzare una connessione ibrida esistente** nel Pannello di hello connessioni ibride. Vedere [Accesso alle risorse locali usando connessioni ibride nel Servizio app di Azure](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="InstallHCM"></a>Installare hello Hybrid Connection Manager locale
Dopo aver creata una connessione ibrida, è possibile installare hello Hybrid Connection Manager nella risorsa locale hello. disponibile per il download dalle App Web di Azure o dal servizio BizTalk. Passaggi dei servizi BizTalk: 

1. Accedi toohello [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Nel riquadro di spostamento a sinistra di hello, selezionare **servizi BizTalk** e quindi selezionare il BizTalk Service. 
3. Seleziona hello **connessioni ibride** scheda:  
   ![scheda per le connessioni ibride][HybridConnectionTab]
4. Nella barra delle applicazioni hello, selezionare **il programma di installazione di On-Premise**:  
   ![Installazione locale][HCOnPremSetup]
5. Selezionare **installare e configurare** toorun o download hello Hybrid Connection Manager in hello locali del sistema. 
6. Selezionare installazione hello toostart di hello segno di spunta. 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a>Informazioni aggiuntive
* Hybrid Connection Manager possono essere installati hello sistemi operativi seguenti:
  
  * Windows Server 2008 R2 (.NET Framework 4.5 + e Windows Management Framework 4.0 + richiesti)
  * Windows Server 2012 (Windows Management Framework 4.0 + richiesto)
  * Windows Server 2012 R2
* Dopo aver installato hello Hybrid Connection Manager, si verifica hello segue: 
  
  * Hello connessione ibrida ospitato in Azure viene configurato automaticamente toouse hello stringa di connessione primaria applicazione. 
  * risorsa locale Hello viene configurata automaticamente toouse hello stringa di connessione primaria locale.
* Hello Hybrid Connection Manager è necessario utilizzare una stringa di connessione locale valido per l'autorizzazione. Hello Azure App Web o App per dispositivi mobili è necessario utilizzare una stringa di connessione di applicazione valido per l'autorizzazione.
* È possibile ridimensionare le connessioni ibride mediante l'installazione di un'altra istanza di hello Hybrid Connection Manager in un altro server. Configurare hello toouse listener locale di hello uguale indirizzo come listener locale prima di hello. In questo caso, il traffico di hello è distribuiti in modo casuale (round robin) tra i listener locale active hello. 

## <a name="ManageHybridConnection"></a>Gestire le connessioni ibride
toomanage le connessioni ibride, è possibile:

* Utilizzare hello portale di Azure e passare tooyour BizTalk Service. 
* Usare le [API REST](http://msdn.microsoft.com/library/azure/dn232347.aspx).

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a>Copiare/rigenerare le stringhe di connessione ibrida hello
1. Accedi toohello [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Nel riquadro di spostamento a sinistra di hello, selezionare **servizi BizTalk** e quindi selezionare il BizTalk Service. 
3. Seleziona hello **connessioni ibride** scheda:  
   ![scheda per le connessioni ibride][HybridConnectionTab]
4. Selezionare la connessione ibrida hello. Nella barra delle applicazioni hello, selezionare **Gestisci connessione**:  
   ![Gestione delle opzioni][HCManageConnection]
   
    **Gestione connessione** elenchi hello stringhe di connessione dell'applicazione e in locale. È possibile copiare hello stringhe di connessione o rigenerare la chiave di accesso utilizzata nella stringa di connessione hello hello. 
   
    **Se si seleziona Regenerate**, hello chiave di accesso condiviso utilizzata all'interno di hello stringa di connessione è stata modificata. Hello seguenti:
   
   * Nel portale di Azure classico hello, selezionare **sincronizzazione delle chiavi** in hello applicazione Azure.
   * Eseguire di nuovo hello **il programma di installazione di On-Premise**. Quando si esegue nuovamente hello l'installazione di On-Premise, hello risorsa locale viene automaticamente configurato toouse stringa di connessione primaria hello aggiornato.

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a>Hello toocontrol criteri di gruppo locali le risorse utilizzate da una connessione ibrida
1. Scaricare hello [modelli amministrativi di Hybrid Connection Manager](http://www.microsoft.com/download/details.aspx?id=42963).
2. Estrarre il file hello.
3. Nel computer di hello che modifica i criteri di gruppo, hello seguenti:  
   
   * Copiare hello. File ADMX toohello *%WINROOT%\PolicyDefinitions* cartella.
   * Copiare hello. ADML file toohello *%WINROOT%\PolicyDefinitions\en-us* cartella.

Una volta la copia, è possibile utilizzare criteri di hello Editor criteri di gruppo toochange.

## <a name="next"></a>Avanti
[Connettere le app Web di Azure tooan risorsa locale](../app-service-web/web-sites-hybrid-connection-get-started.md)  
[Connessione di SQL Server locale tooon da app Web di Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)   
[Panoramica delle connessioni ibride](integration-hybrid-connection-overview.md)

## <a name="see-also"></a>Vedere anche
[REST API for Managing BizTalk Services on Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx) (API REST per la gestione dei servizi BizTalk in Microsoft Azure)  
[Servizi BizTalk: tabella delle edizioni](biztalk-editions-feature-chart.md)  
[Creare un servizio BizTalk mediante il portale di Azure classico](biztalk-provision-services.md)  
[Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
