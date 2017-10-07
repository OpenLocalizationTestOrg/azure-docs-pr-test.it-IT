---
title: aaaCreate un'App Web in Azure App Service utilizzando hello Azure SDK per Java
description: Informazioni su come un'App Web nel servizio App di Azure a livello di programmazione utilizzando toocreate hello Azure SDK per Java.
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a>Creare un'App Web in Azure App Service utilizzando hello Azure SDK per Java
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a>Panoramica
Questa procedura dettagliata illustra come toocreate un SDK di Azure per l'applicazione Java che crea un'App Web nel [Azure App Service][Azure App Service], quindi distribuire tooit un'applicazione. È costituita da due parti:

* Parte 1 viene illustrato come toobuild un'applicazione Java che crea un'app web.
* Parte 2 di seguito viene illustrato come toocreate un JSP semplice "Hello World" applicazione, quindi utilizzare un FTP client toodeploy codice tooApp servizio.

## <a name="prerequisites"></a>Prerequisiti
### <a name="software-installations"></a>Installazioni software
Hello AzureWebDemo codice dell'applicazione in questo articolo è stato scritto con Azure Java SDK 0.7.0, che è possibile installare utilizzando hello [installazione guidata piattaforma Web] [ Web Platform Installer] (WebPI). Inoltre, assicurarsi che toouse hello ultima versione di hello [Azure Toolkit per Eclipse][Azure Toolkit for Eclipse]. Dopo aver installato il SDK di hello, aggiornare le dipendenze di hello nel progetto Eclipse eseguendo **Aggiorna** in **repository Maven**, quindi aggiungere di nuovo più recente di ogni pacchetto in hello hello  **Dipendenze** finestra. È possibile verificare la versione hello del software installato in Eclipse, fare clic su **Guida > Dettagli installazione**; deve avere almeno hello seguenti versioni:

* Pacchetto per Librerie di Microsoft Azure per Java 0.7.0.20150309
* Eclipse IDE per sviluppatori Java EE 4.4.2.20150219

### <a name="create-and-configure-cloud-resources-in-azure"></a>Creare e configurare risorse cloud in Azure
Prima di iniziare questa procedura, è necessario toohave una sottoscrizione Azure attiva e impostare un valore predefinito di Active Directory (AD) in Azure.

### <a name="create-an-active-directory-ad-in-azure"></a>Creare una directory di Active Directory (AD) in Azure
Se non hai già un Active Directory (AD) per la sottoscrizione di Azure, accedere a hello [portale di Azure classico] [ Azure classic portal] con l'account Microsoft. Se si dispone di più sottoscrizioni, fare clic su **sottoscrizioni** directory predefinita selezionare hello e per la sottoscrizione di hello desiderato toouse per questo progetto. Quindi fare clic su **applica** tooswitch toothat la vista delle sottoscrizioni.

1. Selezionare **Active Directory** dal menu hello sinistro. **Fare clic su Nuovo > Directory > Creazione personalizzata**.
2. In **Aggiungi directory** selezionare **Crea nuova directory**.
3. In **Nome**immettere il nome della directory.
4. In **Dominio**immettere il nome del dominio. Si tratta di un nome di dominio di base che è incluso per impostazione predefinita con la directory. ha il formato di hello `<domain_name>.onmicrosoft.com`. È possibile assegnare un nome in base al nome di directory hello o un altro nome di dominio che si è proprietari. In un secondo tempo è possibile aggiungere un altro nome di dominio già usato dall'organizzazione.
5. In **Paese o area geografica**selezionare le impostazioni locali.

Per altre informazioni su AD, vedere [Che cos'è una directory di Azure AD][What is an Azure AD directory]?

### <a name="create-a-management-certificate-for-azure"></a>Creare un certificato di gestione per Azure
Hello Azure SDK per Java Usa tooauthenticate certificati di gestione con le sottoscrizioni di Azure. Si tratta di x. 509 v3 che è utilizzare tooauthenticate un'applicazione client che utilizza hello tooact di API di gestione del servizio per conto di risorse di sottoscrizione toomanage hello sottoscrizione proprietario.

codice Hello in questa procedura utilizza tooauthenticate un certificato autofirmato con Azure. Per questa procedura, è necessario un certificato toocreate e caricarlo toohello [portale di Azure classico] [ Azure classic portal] in anticipo. Questa operazione comporta hello alla procedura seguente:

* Generare un file PFX che rappresenta il certificato client e salvarlo in locale.
* Generare un certificato di gestione (file CER) dal file PFX hello.
* Caricare hello CER file tooyour sottoscrizione di Azure.
* Convertire i file PFX hello in JKS, poiché Java utilizza tale tooauthenticate formato utilizzando i certificati.
* Scrivere il codice di autenticazione dell'applicazione hello, che fa riferimento a file JKS locale toohello.

Dopo aver completato questa procedura, si troverà certificato CER hello nella sottoscrizione di Azure e certificato JKS hello si trova nell'unità locale. Per altre informazioni sui certificati di gestione, vedere [Creare e caricare un certificato di gestione per Azure][Create and Upload a Management Certificate for Azure].

#### <a name="create-a-certificate"></a>Creare un certificato
toocreate il proprio certificato autofirmato, aprire una console dei comandi del sistema operativo ed eseguire hello i comandi seguenti.

> **Nota:** hello in cui si esegue questo comando deve essere installato hello JDK installato. Inoltre, hello percorso toohello keytool dipende dal percorso di hello in cui si installa hello JDK. Per ulteriori informazioni, vedere [chiave e strumento di gestione certificati (keytool)] [ Key and Certificate Management Tool (keytool)] nella documentazione online di hello Java.
> 
> 

file con estensione pfx toocreate hello:

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

file con estensione cer toocreate hello:

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

dove:

* `<java-install-dir>`è hello percorso toohello directory in cui è installato Java.
* `<keystore-id>`è l'identificatore della voce keystore hello (ad esempio, `AzureRemoteAccess`).
* `<cert-store-dir>`hello percorso toohello directory in cui si desiderano toostore certificati (ad esempio `C:/Certificates`).
* `<cert-file-name>`è il nome di hello hello del file di certificato (ad esempio `AzureWebDemoCert`).
* `<password>`password hello si sceglie tooprotect hello certificato; deve essere lunga almeno 6 caratteri. È possibile non immettere alcuna password, anche se non è consigliato.
* `<dname>`è hello nome distinto x. 500 toobe associata alias e viene usato come autorità emittente hello e campi soggetto nel certificato autofirmato hello.

Per altre informazioni, vedere [Creare e caricare un certificato di gestione per Azure][Create and Upload a Management Certificate for Azure].

#### <a name="upload-hello-certificate"></a>Caricare il certificato di hello
tooupload tooAzure un certificato autofirmato, andare toohello **impostazioni** pagina nel portale classico hello e quindi fare clic su hello **i certificati di gestione** scheda. Fare clic su **caricare** nella parte inferiore di hello di hello pagina e passare toohello percorso del file CER hello creato.

#### <a name="convert-hello-pfx-file-into-jks"></a>Convertire i file PFX hello in JKS
Hello prompt dei comandi di Windows (in esecuzione come amministratore), cd toohello directory contenente i certificati di hello ed eseguire hello seguente comando, in cui `<java-install-dir>` hello directory in cui è installato Java nel computer in uso:

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. Quando richiesto, immettere la password di hello destinazione keystore. Questo sarà password hello per file JKS hello.
2. Quando richiesto, immettere la password di hello origine keystore. si tratta hello password specificata per il file PFX hello.

due password Hello non è necessario toobe hello stesso. È possibile non immettere alcuna password, anche se non è consigliato.

## <a name="build-a-web-app-creation-application"></a>Compilare un'applicazione per la creazione di app Web
### <a name="create-hello-eclipse-workspace-and-maven-project"></a>Creare hello Eclipse dell'area di lavoro e progetti Maven
In questa sezione creare un'area di lavoro e un progetto di Maven per hello app creazione applicazione web denominata AzureWebDemo.

1. Creare un nuovo progetto Maven. Fare clic su **File > New > Maven Project** (File > Nuovo > Progetto Maven). In **New Maven Project** (Nuovo progetto Maven) selezionare **Create a simple project** (Crea progetto semplice) e **Use default workspace location** (Usa percorso area di lavoro predefinito).
2. Nella seconda hello di **nuovo progetto di Maven**, specificare hello seguenti:
   
   * Group ID: `com.<username>.azure.webdemo`
   * Artifact ID: AzureWebDemo
   * Version: 0.0.1-SNAPSHOT
   * Packaging: jar
   * Name: AzureWebDemo
     
     Fare clic su **Finish**.
3. Aprire il file di pom.xml hello del nuovo progetto in Esplora progetti. Seleziona hello **dipendenze** scheda. Essendo un nuovo progetto, non è ancora elencato nessun pacchetto.
4. Consente di visualizzare repository Maven hello aperto. Fare clic su **Window > Show View > Other > Maven > Maven Repositories** (Finestra > Mostra vista > Altro > Maven > Repository Maven) e fare clic su **OK**. Hello **repository Maven** visualizzazione verrà visualizzata nella parte inferiore di hello di hello IDE.
5. Aprire **repository globale**, hello rapida **centrale** repository e selezionare **Ricompila indice**.
   
    ![][1]
   
    Questo passaggio può richiedere alcuni minuti a seconda della velocità di hello della connessione. Quando la ricostruzione dell'indice di hello, si dovrebbero vedere pacchetti di Microsoft Azure hello in hello **centrale** repository Maven.
6. In **Dependencies** (Dipendenze) fare clic su **Add** (Aggiungi). In **Enter Group ID...** (Immettere ID gruppo...) immettere `azure-management`. Selezionare i pacchetti hello per la gestione di App del servizio Web App e gestione di base:
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **Nota:** se si siano aggiornando le dipendenze di hello dopo una nuova versione, è necessario toore-aggiungere ognuna delle dipendenze hello in questo elenco.
   > Dopo aver fatto clic **Aggiungi** e selezionare ogni dipendenza, viene visualizzato con hello nuovo numero di versione di hello **dipendenze** elenco.
   > 
   > 

Fare clic su **OK**. Hello Azure pacchetti, quindi vengono visualizzati in hello **dipendenze** elenco.

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a>Scrittura di codice Java tooCreate un'App Web da chiamare hello Azure SDK
Successivamente, scrivere codice hello chiamate le API in hello Azure SDK per hello toocreate Java App del servizio web app.

1. Creare un codice di punto di ingresso principale Java classe toocontain hello. In Esplora progetti, fare clic sul nodo del progetto hello e selezionare **nuovo > classe**.
2. In **nuova classe Java**, nome classe hello `WebCreator` e controllare hello **principale di void statico pubblico** casella di controllo. le selezioni Hello visualizzata come indicato di seguito:
   
    ![][2]
3. Fare clic su **Finish**. file di WebCreator.java Hello viene visualizzato in Esplora progetti.

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a>La chiamata di un'applicazione servizio Web App hello Azure API tooCreate
#### <a name="add-necessary-imports"></a>Aggiungere le importazioni necessarie
In WebCreator.java, aggiungere hello seguente importazioni; tali importazioni forniscono accesso tooclasses in hello delle raccolte di gestione per l'utilizzo di API di Azure:

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a>Definire una classe del punto di ingresso principale hello
Poiché hello hello AzureWebDemo applicazione mira toocreate un'App del servizio Web App, nome classe principale hello per questa applicazione `WebAppCreator`. Questa classe fornisce il codice di punto di ingresso principale hello che chiama hello Azure Service Management API toocreate hello web app.

Aggiungere hello seguenti definizioni di parametro hello web app e dello spazio Web. Sarà necessario tooprovide le proprie informazioni di ID e il certificato di sottoscrizione di Azure.

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

dove:

* `<subscription-id>`è l'ID sottoscrizione di Azure hello in cui si desiderano risorse hello toocreate.
* `<certificate-store-path>`è hello percorso e nome file toohello JKS file nella directory dell'archivio certificati locale. Ad esempio, `C:/Certificates/CertificateName.jks` per Linux e `C:\Certificates\CertificateName.jks` per Windows.
* `<certificate-password>`è la password di hello specificato al momento della creazione del certificato JKS.
* `webAppName`può essere qualsiasi nome desiderato; Questa procedura utilizza nome hello `WebDemoWebApp`. il nome di dominio completo di Hello è hello `webAppName` con hello `domainName` aggiunto, pertanto in questo caso hello completo dominio è `webdemowebapp.azurewebsites.net`.
* `domainName` deve essere specificato come indicato sopra.
* `webSpaceName`deve essere uno dei valori hello definiti in hello [WebSpaceNames] [ WebSpaceNames] classe.
* `appServicePlanName` deve essere specificato come indicato sopra.

> **Nota:** ogni volta che si esegue l'applicazione, è necessario toochange hello valore `webAppName` e `appServicePlanName` (o eliminare l'app web hello nel portale di Azure hello) prima di eseguire nuovamente l'applicazione hello. In caso contrario, viene eseguito perché hello stessa risorsa già esistente in Azure.
> 
> 

#### <a name="define-hello-web-creation-method"></a>Definizione di metodo di creazione di hello web
Successivamente, definire un'app web di metodo toocreate hello. Questo metodo, `createWebApp`, specifica i parametri di hello di hello web app e uno spazio Web hello. Inoltre crea e configura i client di gestione App Web del servizio App di hello, che è definito da hello [WebSiteManagementClient] [ WebSiteManagementClient] oggetto. il client di gestione di Hello è toocreating chiave Web App. Fornisce i servizi web RESTful che consente applicazioni toomanage web App (esecuzione di operazioni, ad esempio la creazione, aggiornamento ed eliminazione) chiamando l'API di Gestione servizio hello.

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

il codice Hello sarà l'output hello di stato HTTP della risposta hello che indica l'esito positivo o negativo e se ha esito positivo, verrà output nome hello di hello app web creata.

#### <a name="define-hello-main-method"></a>Definire il metodo Main () hello
Fornire il codice del metodo Main () hello chiamate createWebApp() toocreate hello web app.

Infine chiamare `createWebApp` da `main`:

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a>Eseguire un'applicazione hello e verificare la creazione di app web
Fare clic su tooverify che l'applicazione viene eseguita, **eseguire > eseguire**. Al termine dell'esecuzione dell'applicazione hello, dovrebbe essere hello seguente output nella console di Eclipse hello:

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

Accedere al portale di Azure classico hello e fare clic su **App Web**. Hello nuova app web verrà visualizzato nell'elenco di App Web hello entro pochi minuti.

## <a name="deploying-an-application-toohello-web-app"></a>Distribuzione di un'App Web di toohello di applicazione
Dopo aver eseguito AzureWebDemo si create hello nuova app web, accedere al portale classico hello, fare clic su **App Web**e selezionare **WebDemoWebApp** in hello **App Web** elenco. Nella pagina dashboard dell'app web hello, fare clic su **Sfoglia** (oppure fare clic su URL hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit. Una pagina di segnaposto vuoto, verrà visualizzato perché nessun contenuto è ancora stato pubblicato toohello web app.

Successivamente si verrà creare un'applicazione "Hello World" e distribuirlo toohello web app.

### <a name="create-a-jsp-hello-world-application"></a>Creare un'applicazione Hello World JSP
#### <a name="create-hello-application"></a>Creare un'applicazione hello
In ordine toodemonstrate come toodeploy web toohello un'applicazione, hello seguente procedura illustra come toocreate una semplice applicazione "Hello World" Java e caricarlo toohello App del servizio Web App che ha creato l'applicazione.

1. Fare clic su **File > New > Dynamic Web Project** (File > Nuovo > Progetto Web dinamico). Denominarlo `JSPHello`. Non è necessario toochange tutte le altre impostazioni in questa finestra di dialogo. Fare clic su **Finish**.
   
    ![][3]
2. In Esplora progetti espandere hello **JSPHello** del progetto, fare doppio clic su **WebContent**, quindi fare clic su **nuovo > File JSP**. Nella finestra di dialogo New JSP File hello, assegnare un nome nuovo file hello `index.jsp`. Fare clic su **Avanti**.
3. In hello **Select JSP Template** selezionare **New JSP File (html)** e fare clic su **fine**.
4. In index.jsp, aggiungere hello seguente di codice hello `<head>` e `<body>` tag sezioni:
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a>Eseguire un'applicazione Hello World hello in localhost
Prima di eseguire questa applicazione, è necessario tooconfigure alcune proprietà.

1. Pulsante destro del mouse hello **JSPHello** del progetto e selezionare **proprietà**.
2. In hello **proprietà** finestra di dialogo: selezionare **Java Build Path**selezionare hello **ordinare ed esportare** scheda **JRE sistema libreria**, quindi fare clic su **Backup** toomove è toohello parte superiore dell'elenco di hello.
   
    ![][4]
3. Anche in hello **proprietà** finestra di dialogo: selezionare **destinazione runtime** e fare clic su **New**.
4. In hello **nuovo ambiente di Runtime Server** finestra di dialogo, selezionare un server, ad esempio **versione 7.0 Apache Tomcat** e fare clic su **Avanti**. In hello **Server Tomcat** finestra di dialogo, impostare **nome** troppo`Apache Tomcat v7.0`e impostare **Directory di installazione di Tomcat** toohello directory in cui è installata la versione hello di Server Tomcat da toouse.
   
    ![][5]
   
    Fare clic su **Finish**.
5. È quindi restituire toohello **destinazione runtime** pagina di hello **proprietà** finestra di dialogo. Selezionare **Apache Tomcat v7.0**, quindi fare clic su **OK**.
   
    ![][6]
6. In Eclipse hello **eseguire** menu, fare clic su **eseguire**. In hello **runas** finestra di dialogo Seleziona **eseguire sul Server**. In hello **eseguire sul Server** finestra di dialogo Seleziona **Tomcat versione 7.0 Server**:
   
    ![][7]
   
    Fare clic su **Finish**.
7. Hello quando l'esecuzione dell'applicazione, si dovrebbe vedere hello **JSPHello** pagina visualizzata in una finestra localhost in Eclipse (`http://localhost:8080/JSPHello/`), visualizzazione hello il seguente messaggio:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a>Esportare un'applicazione hello come un WAR
Esportare il file di progetto web hello come un file web archive (WAR) in modo che è possibile distribuire app web toohello. Hello seguente file di progetto web si trovano nella cartella WebContent hello:

    META-INF
    WEB-INF
    index.jsp

1. Fare clic sulla cartella WebContent hello e selezionare **esportare**.
2. In hello **esportare selezionare** finestra di dialogo, fare clic su **Web > WAR** file, quindi fare clic su **Avanti**.
3. In hello **WAR esportare** finestra di dialogo, selezionare directory src hello nel progetto corrente di hello e includere hello nome di file WAR hello alla fine di hello. ad esempio:
   
    `<project-path>/JSPHello/src/JSPHello.war`

Per ulteriori informazioni sulla distribuzione dei file WAR, vedere [aggiungere un tooAzure applicazione Java App del servizio Web App](web-sites-java-add-app.md).

### <a name="deploying-hello-hello-world-application-using-ftp"></a>Distribuzione di hello Hello World applicazione tramite FTP
Selezionare un'applicazione di terze parti FTP client toopublish hello. Questa procedura vengono illustrate due opzioni: console Kudu hello compilato in Azure. e FileZilla, uno strumento largamente usato con un'interfaccia utente grafica, pratico.

> **Nota:** hello Azure Toolkit per Eclipse supporta gli account di toostorage di distribuzione e cloud services, ma non supporta attualmente App tooweb di distribuzione. È possibile distribuire gli account toostorage e usando un progetto di distribuzione di Azure, come descritto in servizi cloud [creando un'applicazione Hello World per Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), ma non tooweb app. Utilizzare altri metodi, ad esempio FTP o GitHub tootransfer file tooyour app web.
> 
> **Nota:** non è consigliabile utilizzare FTP dal prompt dei comandi di Windows hello (hello utilità riga di comando FTP.EXE fornito con Windows). I client FTP che utilizzano active FTP, ad esempio FTP.EXE, spesso failover toowork firewall. FTP Active specifica un indirizzo interno basato su LAN, toowhich un FTP server probabilmente avrà esito negativo tooconnect.
> 
> 

Per ulteriori informazioni sulla distribuzione tooan App del servizio web app tramite FTP, vedere hello seguenti argomenti:

* [Distribuire mediante un'utilità FTP](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>Imposta credenziali di distribuzione
Assicurarsi di aver eseguito hello **AzureWebDemo** toocreate applicazione un'app web. Percorso dei file di toothis verrà trasferita.

1. Accedere al portale classico di hello e fare clic su **App Web**. Assicurarsi che **WebDemoWebApp** viene visualizzato nell'elenco di hello di App web e assicurarsi che sia in esecuzione. Fare clic su **WebDemoWebApp** tooopen relativo **Dashboard** pagina.
2. In hello **Dashboard** pagina **Quick Glance**, fare clic su **impostare le credenziali di distribuzione** (se già si dispone di credenziali di distribuzione, legge  **Reimpostare le credenziali di distribuzione**).
   
    Le credenziali di distribuzione sono associate a un account Microsoft. È necessario toospecify un nome utente e password che è possibile utilizzare toodeploy utilizzando Git e FTP. È possibile utilizzare queste app di web tooany toodeploy credenziali in tutte le sottoscrizioni di Azure associate all'account Microsoft. Fornire le credenziali di distribuzione Git e FTP nella finestra di dialogo, hello e hello record username e password per un utilizzo futuro.

#### <a name="get-ftp-connection-information"></a>Ottenere informazioni di connessione a FTP
toouse FTP toodeploy applicazione file appena creato toohello app web, è necessario tooobtain le informazioni di connessione. Esistono due modi tooobtain informazioni di connessione. Un modo consiste toovisit hello web app **Dashboard** pagina; hello altro consiste toodownload hello web app profilo di pubblicazione. profilo di pubblicazione Hello è un file XML che fornisce informazioni quali le credenziali di accesso e del nome host FTP per le app web nel servizio App di Azure. È possibile utilizzare questa app web di tooany toodeploy di nome utente e password in tutte le sottoscrizioni associate hello account Azure, non solo questo.

le informazioni di connessione FTP tooobtain pannello dell'app web hello in hello [portale Azure][Azure Portal]:

1. In **Essentials**, trovare e copiare hello **nome host FTP**. Questo è un URI simile troppo`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.
2. In **Essentials** trovare e copiare il **Nome utente FTP/distribuzione**. Questo avrà un formato hello *webappname\deployment-username*, ad esempio `WebDemoWebApp\deployer77`.

profilo di pubblicazione tooobtain hello le informazioni di connessione FTP:

1. Nel pannello dell'app web hello, fare clic su **profilo di pubblicazione Get**. Questo verrà scaricato un file con estensione publishsettings tooyour un'unità locale.
2. Aprire file con estensione publishsettings hello in un editor XML o un editor di testo e individuare hello `<publishProfile>` elemento contenente `publishMethod="FTP"`. Che dovrebbe essere simile hello seguente:
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. Si noti che app web hello `publishProfile` le impostazioni di eseguire il mapping di impostazioni di gestione del sito FileZilla toohello come segue:

* `publishUrl`è hello identico **nome host FTP**, hello valore impostato in **Host**.
* `publishMethod="FTP"`indica che è stata impostata **protocollo** troppo**FTP - File Transfer Protocol**, e **crittografia** troppo**utilizzare FTP normale**.
* `userName`e `userPWD` sono chiavi per hello valori effettivi di nome utente e password specificata quando si reimposta le credenziali di distribuzione hello. `userName`è hello identico **distribuzione / utente FTP**. Viene eseguito il mapping troppo**utente** e **Password** in FileZilla.
* `ftpPassiveMode="True"`indica il che utilizzo di tale sito FTP hello trasferimento FTP passivo. Selezionare **passivo** su hello **le impostazioni del trasferimento** scheda.

#### <a name="configure-hello-web-app-toohost-a-java-application"></a>Configurare l'App Web di hello toohost un'applicazione Java
Prima di pubblicare un'applicazione hello, è necessario toochange alcune impostazioni di configurazione in modo che hello app web può ospitare un'applicazione Java.

1. Nel portale classico hello andare dell'app web toohello **Dashboard** pagina e fare clic su **configura**. In hello **configura** specificare hello seguenti impostazioni.
2. In **versione Java** predefinito hello è **Off**; selezionare la versione di Java hello destinata l'applicazione, ad esempio 1.7.0_51. Al termine dell'operazione, assicurarsi anche che **contenitore Web** è impostato tooa versione del Server Tomcat.
3. In **documenti predefiniti**, aggiungere index.jsp e spostarlo toohello parte superiore dell'elenco di hello. (il file predefinito hello per le app web è hostingstart.html).
4. Fare clic su **Salva**.

#### <a name="publish-your-application-using-kudu"></a>Pubblicare l'applicazione con Kudu
Un'applicazione hello toopublish unidirezionale è hello toouse che kudu debug console integrata in Azure. Kudu è noto toobe stabile e coerente con l'App del servizio Web App e il Server Tomcat. Console hello per l'app web hello è accedere esplorando tooa URL di hello seguente formato:

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. Per questa procedura, si trova nel seguente URL; hello console Kudu hello Cerca nel percorso toothis:
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. Scegliere dal menu in alto hello **Console Debug > CMD**.
3. Nella riga di comando hello console passare troppo`/site/wwwroot` (oppure fare clic su `site`, quindi `wwwroot` nella visualizzazione directory hello nella parte superiore di hello della pagina hello):
   
    `cd /site/wwwroot`
4. Dopo aver specificato **Java version**, il server Tomcat dovrebbe creare una directory webapps. Nella riga di comando console hello, passare toohello WebApp directory:
   
    `mkdir webapps`
   
    `cd webapps`
5. Trascinare JSPHello.war da `<project-path>/JSPHello/src/` e rilasciarlo in visualizzazione di directory Kudu hello in `/site/wwwroot/webapps`. Non trascinarla area "Trascinare qui tooupload e zip" toohello, perché verrà decomprimerlo Tomcat.
   
   ![][8]

Nel primo JSPHello.war viene visualizzata nell'area di directory di hello da se stessa:

  ![][9]

In un breve periodo di tempo (probabilmente meno di 5 minuti) il Server Tomcat verrà decomprimere file WAR hello in una directory JSPHello decompressa. Fare clic su toosee directory radice di hello se index.jsp è stato decompresso e copiati in tale posizione. In caso affermativo, spostarsi indietro toohello WebApp directory toosee se hello decompressi JSPHello directory è stata creata. Se questi elementi non sono visibili, attendere e riprovare.

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>Pubblicare l'applicazione con FileZilla (facoltativo)
Un altro strumento, è possibile utilizzare un'applicazione hello toopublish è FileZilla, un client FTP comune di terze parti con un'interfaccia utente grafica, pratico. È possibile scaricare e installare FileZilla da [http://filezilla-project.org/](http://filezilla-project.org/) se non lo si ha già. Per ulteriori informazioni sull'utilizzo di client hello, vedere hello [FileZilla documentazione](https://wiki.filezilla-project.org/Documentation) e questo post di blog su [client FTP - parte 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).

1. In FileZilla fare clic su **File > Gestore siti**.
2. In hello **di gestione del sito** finestra di dialogo, fare clic su **nuovo sito**. Verrà visualizzato un nuovo sito FTP vuoto **voce selezionare** chiesto tooprovide un nome. Per questa procedura, denominarlo `AzureWebDemo-FTP`.
   
    In hello **generale** , specificare hello seguenti impostazioni:
   
   * **Host:** invio hello **nome Host FTP** copiata dal dashboard hello.
   * **Porta:** (lasciare vuoto questo campo perché si tratta di un trasferimento passivo e server hello determinerà hello porta toouse.)
   * **Protocollo:** protocollo per il trasferimento del file FTP
   * **Crittografia:** usare FTP semplice
   * **Tipo di accesso:** normale
   * **Utente:** invio hello distribuzione / FTP utente copiato dal dashboard hello. Si tratta di hello FTP nome utente completo, che ha un formato hello *webappname\username*.
   * **Password:** immettere la password di hello specificato quando si imposta le credenziali di distribuzione hello.
     
     In hello **le impostazioni del trasferimento** , selezionare **passivo**.
3. Fare clic su **Connetti**. Se ha esito positivo, la console del FileZilla visualizzerà un `Status: Connected` messaggio ed emettere un `LIST` comando contenuto della directory toolist hello.
4. In hello **locale** pannello sito, la directory di origine selezionare hello in cui i file JSPHello.war hello risiede; percorso hello sarà simile toohello seguenti:
   
    `<project-path>/JSPHello/src/`
5. In hello **remoto** pannello sito, la cartella di destinazione selezionare hello. Si distribuirà toohello di file WAR hello `webapps` directory radice dell'applicazione web hello. Passare troppo`/site/wwwroot`, fare clic su `wwwroot`e selezionare **Crea directory**. Directory di hello nome `webapps` e immettere una directory.
6. Trasferimento JSPHello.war troppo`/site/wwwroot/webapps`. Selezionare JSPHello.war hello **locale** elenco dei file, fare clic su di esso e selezionare **caricare**. Dovrebbe venire visualizzato in `/site/wwwroot/webapps`.
7. Dopo aver copiato JSPHello.war toohello webapps directory, Server Tomcat verranno automaticamente installati (decomprimere) hello file nel file WAR hello. Anche se il Server Tomcat inizia disimballaggio quasi immediatamente, potrebbe richiedere troppo tempo (possibilmente ore) per tooappear file hello client hello FTP.

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a>Eseguire un'applicazione Hello World hello in hello App Web
1. Dopo aver caricato i file WAR hello e verificare che il server Tomcat è creato un decompressi `JSPHello` directory Sfoglia troppo`http://webdemowebapp.azurewebsites.net/JSPHello` toorun un'applicazione hello.
   
   > **Nota:** se si fa clic **Sfoglia** dal portale classico hello, si potrebbero ottenere pagina Web predefinita hello, indicante che "l'applicazione web Java in base è stata creata." Pagina Web hello toorefresh potrebbe essere in output dell'applicazione hello tooview ordine anziché la pagina Web predefinita hello.
   > 
   > 
2. Quando viene eseguita l'applicazione hello, vedrai una pagina web con hello seguente output:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>Pulire le risorse di Azure
Questa procedura crea un'app web del servizio app. Verrà fatturato per la risorsa hello, purché esista. A meno che non si prevede di toocontinue tramite hello web app per il testing o di sviluppo, è necessario considerare l'arresto o l'eliminazione. Anche se un'app Web viene arrestata, è ugualmente prevista una piccola spesa, ma è possibile riavviarla in qualsiasi momento. L'eliminazione di un'app web Cancella tutti i dati caricati tooit.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
