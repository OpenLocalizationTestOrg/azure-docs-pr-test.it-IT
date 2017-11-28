---
title: riga di comando AD Java introduttiva aaaAzure | Documenti Microsoft
description: Come toobuild un linguaggio di comando riga app che gli utenti in tooaccess un'API di firma.
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a><span data-ttu-id="0c3f8-103">Tramite l'applicazione della riga di comando Java tooAccess un'API con Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c3f8-103">Using Java Command Line App tooAccess An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="0c3f8-104">Azure Active Directory rende semplice e diretto toooutsource gestione delle identità dell'applicazione web, fornisce single sign-in e la disconnessione con poche righe di codice.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-104">Azure AD makes it simple and straightforward toooutsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="0c3f8-105">Nelle App web Java, è possibile eseguire questa operazione utilizzando implementazione Microsoft di hello ADAL4J basato sulla community.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-105">In Java web apps, you can accomplish this using Microsoft's implementation of hello community-driven ADAL4J.</span></span>

  <span data-ttu-id="0c3f8-106">ADAL4J verrà usato per:</span><span class="sxs-lookup"><span data-stu-id="0c3f8-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="0c3f8-107">Utente di hello Sign in hello app usando Azure AD come provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-107">Sign hello user into hello app using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="0c3f8-108">Visualizzare alcune informazioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-108">Display some information about hello user.</span></span>
* <span data-ttu-id="0c3f8-109">Sign hello utente all'esterno dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="0c3f8-110">In ordine toodo questo, è necessario:</span><span class="sxs-lookup"><span data-stu-id="0c3f8-110">In order toodo this, you'll need to:</span></span>

1. <span data-ttu-id="0c3f8-111">Registrare un'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="0c3f8-112">Consente di impostare la raccolta di app toouse hello ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-112">Set up your app toouse hello ADAL4J library.</span></span>
3. <span data-ttu-id="0c3f8-113">Utilizzare hello ADAL4J libreria tooissue Accedi e richieste di disconnessione tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-113">Use hello ADAL4J library tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="0c3f8-114">Stampare dati sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-114">Print out data about hello user.</span></span>

<span data-ttu-id="0c3f8-115">tooget avviato, [scaricare scheletro app hello](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="0c3f8-115">tooget started, [download hello app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download hello completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="0c3f8-116">È inoltre necessario un tenant di Azure Active Directory in cui tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-116">You'll also need an Azure AD tenant in which tooregister your application.</span></span>  <span data-ttu-id="0c3f8-117">Se non hai già fatto, [informazioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="0c3f8-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="0c3f8-118">1.  Registrare un'applicazione con Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c3f8-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="0c3f8-119">tooenable utenti tooauthenticate app, è prima necessario tooregister una nuova applicazione nel tenant.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-119">tooenable your app tooauthenticate users, you'll first need tooregister a new application in your tenant.</span></span>

1. <span data-ttu-id="0c3f8-120">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c3f8-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c3f8-121">Nella barra superiore hello, fare clic sull'account e in hello **Directory** elenco, scegliere hello tenant di Active Directory in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-121">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="0c3f8-122">Fare clic su **più servizi** in hello barra di spostamento a sinistra, quindi scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-122">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="0c3f8-123">Fare clic su **App registrations (Registrazioni app)** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="0c3f8-124">Seguire le istruzioni di hello e creare un nuovo **applicazione Web e/o WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-124">Follow hello prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="0c3f8-125">Hello **nome** di hello applicazione descriverà tooend utenti applicazione</span><span class="sxs-lookup"><span data-stu-id="0c3f8-125">hello **name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="0c3f8-126">Hello **Sign-On URL** hello URL di base dell'app.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-126">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="0c3f8-127">valore predefinito dell'ossatura Hello è `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-127">hello skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="0c3f8-128">Dopo avere completato la registrazione, AAD assegnerà all'app un ID app univoco.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="0c3f8-129">È necessario che questo valore in hello nelle sezioni seguenti, quindi copiarlo dalla scheda applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-129">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="0c3f8-130">Da hello **impostazioni** -> **proprietà** pagina per l'applicazione, aggiornare hello URI ID App.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="0c3f8-131">Hello **URI ID App** è un identificatore univoco per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-131">hello **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="0c3f8-132">convenzione di Hello è toouse `https://<tenant-domain>/<app-name>`, ad esempio `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-132">hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="0c3f8-133">Una volta nel portale di hello per le app di creare un **chiave** da hello **impostazioni** pagina per l'applicazione e copiarlo.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-133">Once in hello portal for your app create a **Key** from hello **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="0c3f8-134">Verrà richiesto a breve.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="0c3f8-135">2. Configurare la libreria di app toouse ADAL4J e prerequisiti utilizzando Maven</span><span class="sxs-lookup"><span data-stu-id="0c3f8-135">2. Set up your app toouse ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="0c3f8-136">In questo caso, è possibile configurare il protocollo di autenticazione OpenID Connect di ADAL4J toouse hello.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-136">Here, we'll configure ADAL4J toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="0c3f8-137">ADAL4J verrà essere tooissue utilizzato le richieste di accesso e disconnessione, gestire la sessione dell'utente hello e ottenere informazioni sull'utente hello, tra l'altro.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-137">ADAL4J will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

* <span data-ttu-id="0c3f8-138">Nella directory radice di hello del progetto, aprire/creare `pom.xml` e individuare hello `// TODO: provide dependencies for Maven` e sostituire con hello seguente:</span><span class="sxs-lookup"><span data-stu-id="0c3f8-138">In hello root directory of your project, open/create `pom.xml` and locate hello `// TODO: provide dependencies for Maven` and replace with hello following:</span></span>

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-hello-java-publicclient-file"></a><span data-ttu-id="0c3f8-139">3. Creare file Java PublicClient hello</span><span class="sxs-lookup"><span data-stu-id="0c3f8-139">3. Create hello Java PublicClient file</span></span>
<span data-ttu-id="0c3f8-140">Come indicato in precedenza, verrà usato hello dati tooget API Graph su hello utente connesso.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-140">As indicated above, we will be using hello Graph API tooget data about hello logged in user.</span></span> <span data-ttu-id="0c3f8-141">Per questo toobe semplificherà è dovrebbe creare sia un file toorepresent un **oggetto Directory** e hello di toorepresent un singolo file **utente** in modo che hello OO di Java può essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-141">For this toobe easy for us we should create both a file toorepresent a **Directory Object** and an individual file toorepresent hello **User** so that hello OO pattern of Java can be used.</span></span>

* <span data-ttu-id="0c3f8-142">Creare un file denominato `DirectoryObject.java` che si utilizzerà i dati di base toostore su qualsiasi DirectoryObject (è possibile toouse disponibile questo in un secondo momento per altre query grafico è possibile eseguire).</span><span class="sxs-lookup"><span data-stu-id="0c3f8-142">Create a file called `DirectoryObject.java` which we will use toostore basic data about any DirectoryObject (you can feel free toouse this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="0c3f8-143">È possibile tagliare e incollare dal codice seguente:</span><span class="sxs-lookup"><span data-stu-id="0c3f8-143">You can cut/paste this from below:</span></span>

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-hello-sample"></a><span data-ttu-id="0c3f8-144">Compilare ed eseguire l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="0c3f8-144">Compile and run hello sample</span></span>
<span data-ttu-id="0c3f8-145">Modificare nuovamente le directory radice tooyour ed eseguire hello seguente esempio di comando toobuild hello sufficiente inserire tra loro tramite `maven`.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-145">Change back out tooyour root directory and run hello following command toobuild hello sample you just put together using `maven`.</span></span> <span data-ttu-id="0c3f8-146">Verranno utilizzate hello `pom.xml` file è stato scritto per le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-146">This will use hello `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="0c3f8-147">Nella directory `/targets` dovrebbe essere presente un file `adal4jsample.war`.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="0c3f8-148">È possibile che la distribuzione nel contenitore di Tomcat e visitare hello URL</span><span class="sxs-lookup"><span data-stu-id="0c3f8-148">You may deploy that in your Tomcat container and visit hello URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="0c3f8-149">È molto semplice toodeploy un WAR con i server Tomcat hello più recenti.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-149">It is very easy toodeploy a WAR with hello latest Tomcat servers.</span></span> <span data-ttu-id="0c3f8-150">Passare semplicemente troppo`http://localhost:8080/manager/` e seguire le istruzioni di hello sul caricamento del ' adal4jsample.war' file.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-150">Simply navigate too`http://localhost:8080/manager/` and follow hello instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="0c3f8-151">Si verifica un autodeploy automaticamente con l'endpoint corretto hello.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-151">It will autodeploy for you with hello correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0c3f8-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c3f8-152">Next Steps</span></span>
<span data-ttu-id="0c3f8-153">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-153">Congratulations!</span></span> <span data-ttu-id="0c3f8-154">È ora un'applicazione Java che sono presenti utenti tooauthenticate possibilità di hello funzionante, in modo sicuro chiamare le API Web mediante OAuth 2.0 e ottenere le informazioni di base utente hello.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-154">You now have a working Java application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="0c3f8-155">Se hai già fatto, è ora hello ora toopopulate tenant con alcuni utenti.</span><span class="sxs-lookup"><span data-stu-id="0c3f8-155">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>

<span data-ttu-id="0c3f8-156">Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file ZIP qui](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), oppure duplicarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="0c3f8-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

