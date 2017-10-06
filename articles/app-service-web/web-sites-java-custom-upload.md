---
title: aaaUpload un tooAzure di app web Java personalizzate
description: Questa esercitazione viene illustrato come un linguaggio personalizzato tooupload web app tooAzure App del servizio Web App.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a>Caricare un tooAzure di app web Java personalizzate
Questo argomento viene illustrato come un linguaggio personalizzato tooupload app web troppo[Azure App Service] App Web. Sono inoltre incluse informazioni che si applicano anche alcuni esempi per applicazioni specifiche o app web e sito Web Java tooany.

Si noti che Azure fornisce un mezzo per la creazione di applicazioni web Java utilizzando l'interfaccia utente di configurazione del portale di Azure hello e hello Azure Marketplace, come illustrato in [creare un'app web Java in Azure App Service](web-sites-java-get-started.md). In questa esercitazione è per gli scenari in cui non si desidera una configurazione del portale di Azure hello toouse dell'interfaccia utente o hello Azure Marketplace.  

## <a name="configuration-guidelines"></a>Linee guida per la configurazione
Hello di seguito è riportate le impostazioni di hello previste per l'App web Java personalizzate in Azure.

* porta HTTP Hello utilizzata da hello processo Java viene assegnata dinamicamente.  il processo di Hello deve usare la porta hello dalla variabile di ambiente hello `HTTP_PLATFORM_PORT`.
* Tutti porte in ascolto diverso listener HTTP singolo hello deve essere disabilitato.  In Tomcat, che include l'arresto di hello, HTTPS e AJP porte.
* contenitore di Hello deve toobe configurato per il solo traffico IPv4.
* Hello **avvio** comando per un'applicazione hello deve toobe impostato nella configurazione di hello.
* Le applicazioni che richiedono directory con l'autorizzazione di scrittura devono toobe si trova nella directory del contenuto dell'applicazione web di Azure hello, che è **d:\home.**.  variabile di ambiente Hello `HOME` fa riferimento tooD:\home.  

È possibile impostare le variabili di ambiente necessarie nel file Web. config hello.

## <a name="webconfig-httpplatform-configuration"></a>Configurazione httpPlatform in web.config
Hello informazioni seguenti vengono descritte hello **httpplatform in** formato all'interno di Web. config.

**arguments** (impostazione predefinita ""). Argomenti toohello eseguibile o script specificato nella hello **processPath** impostazione.

Esempi (con **processPath** incluso):

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -toohello percorso eseguibile o uno script che verrà avviato un processo in ascolto delle richieste HTTP.

Esempi:

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (impostazione predefinita 10) Numero di volte specificato nel processo di hello **processPath** è consentito toocrash al minuto. Se questo limite viene superato, **HttpPlatformHandler** smetterà di avviare il processo di hello per il resto di hello di minuto hello.

**requestTimeout** (impostazione predefinita "00:02:00") Durata per cui **HttpPlatformHandler** rimarrà in attesa di una risposta dal processo hello in ascolto su `%HTTP_PLATFORM_PORT%`.

**startupRetryCount** (impostazione predefinita = 10 secondi) Numero di volte in cui **HttpPlatformHandler** tenterà il processo di hello toolaunch specificato **processPath**. Per informazioni più dettagliate, vedere **startupTimeLimit**.

**startupTimeLimit** (impostazione predefinita = 10 secondi) Durata per cui **HttpPlatformHandler** rimarrà in attesa di hello eseguibile o script toostart un processo in ascolto sulla porta hello.  Se viene superato questo limite di tempo, **HttpPlatformHandler** verrà terminare il processo di hello e provare toolaunch nuovamente **startupRetryCount** volte.

**stdoutLogEnabled** (impostazione predefinita "true") Se true, **stdout** e **stderr** per processo hello specificato in hello **processPath** impostazione sarà reindirizzato toohello file specificato in  **stdoutLogFile** (vedere **stdoutLogFile** sezione).

**stdoutLogFile** (impostazione predefinita "d:\home\LogFiles\httpPlatformStdout.log") Percorso file assoluto per il quale **stdout** e **stderr** dal processo hello specificato in **processPath** verranno registrati.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`è un segnaposto speciale che deve toospecified o come parte di **argomenti** o come parte di hello **httpplatform in** **environmentVariables** elenco. Questo verrà sostituito da una porta generata internamente da **HttpPlatformHandler** in modo che il processo di hello specificato dalla **processPath** può restare in ascolto su questa porta.
> 
> 

## <a name="deployment"></a>Distribuzione
Le applicazioni web Java in base possono essere distribuite facilmente la maggior parte di hello che stesso indica che vengono utilizzata con le applicazioni web di hello basato su Internet Information Services (IIS).  FTP, Git e Kudu sono tutte supportate come meccanismo di distribuzione, come è hello funzionalità SCM integrata per le applicazioni web. WebDeploy è supportato come protocollo ma non è adatto negli scenari di utilizzo che prevedono la distribuzione di un sito Web Java poiché Java non è sviluppato in Visual Studio.

## <a name="application-configuration-examples"></a>Esempi di configurazione delle applicazioni
Per hello seguenti applicazioni, un file Web. config e hello configurazione dell'applicazione viene fornita come esempi tooshow come tooenable l'applicazione Java in App del servizio Web App.

### <a name="tomcat"></a>Tomcat
Esistono due varianti nel Tomcat che vengono fornite con l'App del servizio Web App, è comunque possibile tooupload istanze specifiche di clienti. Di seguito è riportato un esempio di installazione di Tomcat con una Java Virtual Machine (JVM) diversa.

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

Hello lato Tomcat, esistono alcune modifiche di configurazione necessarie toobe apportate. Hello server.xml deve tooset toobe modificato:

* Porta di arresto = -1
* Porta connettore HTTP = ${port.http}
* Indirizzo connettore HTTP = "127.0.0.1"
* Impostare come commento i connettori HTTPS e AJP
* Hello IPv4 può anche essere impostata nel file catalina hello in cui è possibile aggiungere`java.net.preferIPv4Stack=true`

Chiamate Direct3d non sono supportate in applicazione servizio Web App. toodisable, aggiungere hello seguente opzione Java deve applicazione effettuare tali chiamate:`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Come accade hello per Tomcat, i clienti possono caricare relative istanze per Jetty. Nel caso di hello di in esecuzione hello eseguire l'installazione completa di Jetty, configurazione di hello dovrebbe essere simile al seguente:

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

configurazione di Jetty Hello deve toobe modificato in hello start.ini tooset `java.net.preferIPv4Stack=true`.

### <a name="springboot"></a>Springboot
In ordine tooget un Springboot applicazione in esecuzione è necessario tooupload il file JAR o azioni di GUERRA e aggiunta hello seguenti il file Web. config. file Web. config Hello inseriti nella cartella wwwroot hello. In Web. config hello regolare file JAR di hello argomenti toopoint tooyour, hello seguenti il file JAR di esempio hello si trova nella cartella wwwroot di hello anche.  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a>Hudson
Test utilizzato hello war Hudson 3.1.2 e hello istanza Tomcat 7.0.50 predefinita ma senza l'utilizzo di operazioni tooset dell'interfaccia utente di hello.  Poiché Hudson è uno strumento di compilazione di software, è consigliato tooinstall sul dedicato istanze in cui hello **AlwaysOn** flag può essere impostato su hello web app.

1. Nella radice del sito Web di Azure, ad esempio **d:\home\site\wwwroot**, creare una directory **webapps**, se non è già presente, quindi inserire Hudson.war in **d:\home\site\wwwroot\webapps**.
2. Scaricare apache maven 3.0.5 (compatibile con Hudson) e posizionarlo in **d:\home\site\wwwroot**.
3. Creazione di Web. config in **d:\home\site\wwwroot** e Incolla hello seguente contenuto:
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    A questo punto hello web app può essere riavviato tootake hello modifiche.  Connettersi toohttp://yourwebapp/hudson toostart Hudson.
4. Al termine Hudson viene configurato, verrà visualizzato hello seguente schermata:
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. Hello accesso pagina configuration di Hudson: fare clic su **gestire Hudson**, quindi fare clic su **Configura sistema**.
6. Configurare hello JDK, come illustrato di seguito:
   
    ![Configurazione di Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. Configurare Maven come mostrato di seguito:
   
    ![Configurazione di Maven](./media/web-sites-java-custom-upload/maven.png)
8. Salvare le impostazioni di hello. A questo punto Hudson dovrebbe essere configurato e pronto per l'uso.

Per ulteriori informazioni su Hudson, vedere [http://hudson-ci.org](http://hudson-ci.org).

### <a name="liferay"></a>Liferay
Liferay è supportato in applicazione servizio Web App. Poiché Liferay possono richiedere notevole di memoria, l'app web hello deve toorun su un lavoro dedicato medio o grandi dimensioni, che può fornire memoria sufficiente. Liferay anche richiede diversi minuti toostart. Per questo motivo, è consigliabile impostare app web hello troppo**Always On**.  

Usa Liferay 6.1.2 che Community Edition GA3 in bundle con Tomcat, hello seguenti file sono stati modificati dopo il download Liferay:

**Server.xml**

* Modificare arresto porta troppo-1.
* Modificare anche il connettore HTTP`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* Connettore AJP hello come commento.

In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** cartella, creare un file denominato **portale ext.properties**. Questo file deve toocontain una riga, come illustrato di seguito:

    liferay.home=%HOME%/site/wwwroot/liferay

Hello stesso livello di directory come cartella tomcat 7.0.40 hello, creare un file denominato **Web. config** con hello seguente contenuto:

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

In hello **httpplatform in** blocco, hello **requestTimeout** è troppo "00: 10:00".  Quest'ultimo può essere ridotto ma si è probabilmente toosee alcuni errori di timeout durante il Liferay è l'avvio.  Se questo valore viene modificato, hello **connectionTimeout** in tomcat hello server.xml dovrebbe essere modificato.  

Vale la pena notare che varariable di ambiente JRE_HOME hello è specificato in hello di sopra di Web. config toopoint toohello JDK a 64 bit. valore predefinito di Hello è a 32 bit, ma poiché Liferay potrebbe richiedono livelli elevati di memoria, è consigliabile toouse hello JDK a 64 bit.

Dopo avere apportato le modifiche indicate, riavviare l'app Web che esegue Liferay, quindi aprire http://yourwebapp. portale Liferay Hello è disponibile dalla radice di app web hello. 

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su Liferay, vedere [http://www.liferay.com](http://www.liferay.com).

Per altre informazioni su Java, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
