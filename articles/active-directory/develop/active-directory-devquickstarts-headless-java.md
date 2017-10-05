---
title: Introduzione alla riga di comando Java per Azure AD | Microsoft Docs
description: Come compilare un'app della riga di comando Java che faccia accedere gli utenti a un'API.
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
ms.openlocfilehash: 91e4a7b2ac454465d5cce4948a4d5f0b542d2b55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-java-command-line-app-to-access-an-api-with-azure-ad"></a><span data-ttu-id="cef74-103">Uso dell'app della riga di comando Java per accedere a un'API con Azure AD</span><span class="sxs-lookup"><span data-stu-id="cef74-103">Using Java Command Line App To Access An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="cef74-104">Azure AD facilita e semplifica l'outsourcing della gestione delle identità delle app Web, fornendo un unico account di accesso e disconnessione solo con poche righe di codice.</span><span class="sxs-lookup"><span data-stu-id="cef74-104">Azure AD makes it simple and straightforward to outsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="cef74-105">Nelle app Web Java, è possibile eseguire questa operazione utilizzando l’implementazione Microsoft di ADAL4J basato sulla community.</span><span class="sxs-lookup"><span data-stu-id="cef74-105">In Java web apps, you can accomplish this using Microsoft's implementation of the community-driven ADAL4J.</span></span>

  <span data-ttu-id="cef74-106">ADAL4J verrà usato per:</span><span class="sxs-lookup"><span data-stu-id="cef74-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="cef74-107">Connettere l'utente all'app usando Azure AD come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="cef74-107">Sign the user into the app using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="cef74-108">Visualizzare alcune informazioni relative all'utente.</span><span class="sxs-lookup"><span data-stu-id="cef74-108">Display some information about the user.</span></span>
* <span data-ttu-id="cef74-109">Disconnettere l'utente dall'app.</span><span class="sxs-lookup"><span data-stu-id="cef74-109">Sign the user out of the app.</span></span>

<span data-ttu-id="cef74-110">A questo scopo è necessario:</span><span class="sxs-lookup"><span data-stu-id="cef74-110">In order to do this, you'll need to:</span></span>

1. <span data-ttu-id="cef74-111">Registrare un'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cef74-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="cef74-112">Configurare l'app per usare la libreria ADAL per Java (ADAL4J).</span><span class="sxs-lookup"><span data-stu-id="cef74-112">Set up your app to use the ADAL4J library.</span></span>
3. <span data-ttu-id="cef74-113">Usare la libreria ADAL4J per inviare le richieste di accesso e disconnessione ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cef74-113">Use the ADAL4J library to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="cef74-114">Visualizzare dati relativi all'utente.</span><span class="sxs-lookup"><span data-stu-id="cef74-114">Print out data about the user.</span></span>

<span data-ttu-id="cef74-115">Per iniziare, [scaricare la struttura dell'app](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) o [scaricare l'esempio completato](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="cef74-115">To get started, [download the app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download the completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="cef74-116">Sarà necessario anche un tenant di Azure AD in cui registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cef74-116">You'll also need an Azure AD tenant in which to register your application.</span></span>  <span data-ttu-id="cef74-117">Se non si ha già un tenant, vedere le [informazioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="cef74-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="cef74-118">1.  Registrare un'applicazione con Azure AD</span><span class="sxs-lookup"><span data-stu-id="cef74-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="cef74-119">Per consentire all'app di autenticare gli utenti, sarà innanzitutto necessario registrare una nuova applicazione nel tenant.</span><span class="sxs-lookup"><span data-stu-id="cef74-119">To enable your app to authenticate users, you'll first need to register a new application in your tenant.</span></span>

1. <span data-ttu-id="cef74-120">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cef74-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cef74-121">Nella barra in alto fare clic sull'account e nell'elenco **Directory** scegliere il tenant di Active Directory in cui si vuole registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cef74-121">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="cef74-122">Fare clic su **Altri servizi** nella barra di spostamento a sinistra e scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cef74-122">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="cef74-123">Fare clic su **App registrations (Registrazioni app)** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cef74-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="cef74-124">Seguire le istruzioni e creare una nuova **Applicazione Web e/o API Web**.</span><span class="sxs-lookup"><span data-stu-id="cef74-124">Follow the prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="cef74-125">Il **nome** dell'applicazione deve essere una descrizione per gli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="cef74-125">The **name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="cef74-126">L' **URL accesso** è l'URL di base dell'app.</span><span class="sxs-lookup"><span data-stu-id="cef74-126">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="cef74-127">Il valore predefinito della struttura è `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="cef74-127">The skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="cef74-128">Dopo avere completato la registrazione, AAD assegnerà all'app un ID app univoco.</span><span class="sxs-lookup"><span data-stu-id="cef74-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="cef74-129">Poiché questo valore sarà necessario nelle sezioni successive, copiarlo dalla scheda dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cef74-129">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="cef74-130">Dalla pagina **Impostazioni** -> **Proprietà** dell'applicazione aggiornare l'URI dell'ID app.</span><span class="sxs-lookup"><span data-stu-id="cef74-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="cef74-131">L' **URI ID app** è un identificatore univoco dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cef74-131">The **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="cef74-132">Per convenzione si usa `https://<tenant-domain>/<app-name>`, ad esempio `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="cef74-132">The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="cef74-133">Dopo aver eseguito l'accesso al portale per l'app, creare una **Chiave** dalla pagina **Impostazioni** per l'applicazione e copiarla.</span><span class="sxs-lookup"><span data-stu-id="cef74-133">Once in the portal for your app create a **Key** from the **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="cef74-134">Verrà richiesto a breve.</span><span class="sxs-lookup"><span data-stu-id="cef74-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-to-use-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="cef74-135">2. Configurare l'app per usare la libreria ADAL4J e i prerequisiti tramite Maven</span><span class="sxs-lookup"><span data-stu-id="cef74-135">2. Set up your app to use ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="cef74-136">In questo caso, verrà configurata la libreria ADAL4J per l'uso del protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="cef74-136">Here, we'll configure ADAL4J to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="cef74-137">La libreria ADAL4J verrà usata, tra le altre cose, per inviare le richieste di accesso e disconnessione, gestire la sessione dell'utente e ottenere informazioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="cef74-137">ADAL4J will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

* <span data-ttu-id="cef74-138">Nella directory radice del progetto aprire o creare `pom.xml`, individuare `// TODO: provide dependencies for Maven` e sostituirlo con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="cef74-138">In the root directory of your project, open/create `pom.xml` and locate the `// TODO: provide dependencies for Maven` and replace with the following:</span></span>

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



## <a name="3-create-the-java-publicclient-file"></a><span data-ttu-id="cef74-139">3. Creare il file Java PublicClient</span><span class="sxs-lookup"><span data-stu-id="cef74-139">3. Create the Java PublicClient file</span></span>
<span data-ttu-id="cef74-140">Come indicato sopra, verrà usata l'API Graph per ottenere i dati relativi all'utente connesso.</span><span class="sxs-lookup"><span data-stu-id="cef74-140">As indicated above, we will be using the Graph API to get data about the logged in user.</span></span> <span data-ttu-id="cef74-141">Per semplificare la procedura, sarà necessario creare un file per rappresentare un **Oggetto directory** e un singolo file per rappresentare l'**Utente**, affinché sia possibile usare il modello orientato a oggetti di Java.</span><span class="sxs-lookup"><span data-stu-id="cef74-141">For this to be easy for us we should create both a file to represent a **Directory Object** and an individual file to represent the **User** so that the OO pattern of Java can be used.</span></span>

* <span data-ttu-id="cef74-142">Creare un file denominato `DirectoryObject.java` che verrà usato per archiviare i dati relativi a qualsiasi oggetto directory (sarà possibile riutilizzarlo in seguito per eventuali altre query dell'API Graph).</span><span class="sxs-lookup"><span data-stu-id="cef74-142">Create a file called `DirectoryObject.java` which we will use to store basic data about any DirectoryObject (you can feel free to use this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="cef74-143">È possibile tagliare e incollare dal codice seguente:</span><span class="sxs-lookup"><span data-stu-id="cef74-143">You can cut/paste this from below:</span></span>

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


## <a name="compile-and-run-the-sample"></a><span data-ttu-id="cef74-144">Compilare ed eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="cef74-144">Compile and run the sample</span></span>
<span data-ttu-id="cef74-145">Passare alla directory radice ed eseguire il comando seguente per compilare l'esempio appena creato con `maven`.</span><span class="sxs-lookup"><span data-stu-id="cef74-145">Change back out to your root directory and run the following command to build the sample you just put together using `maven`.</span></span> <span data-ttu-id="cef74-146">Verrà usato il file `pom.xml` scritto per le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="cef74-146">This will use the `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="cef74-147">Nella directory `/targets` dovrebbe essere presente un file `adal4jsample.war`.</span><span class="sxs-lookup"><span data-stu-id="cef74-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="cef74-148">È possibile eseguire la distribuzione nel contenitore Tomcat e visitare l'URL</span><span class="sxs-lookup"><span data-stu-id="cef74-148">You may deploy that in your Tomcat container and visit the URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="cef74-149">La distribuzione di un file WAR con i server Tomcat più recenti è un'operazione semplice.</span><span class="sxs-lookup"><span data-stu-id="cef74-149">It is very easy to deploy a WAR with the latest Tomcat servers.</span></span> <span data-ttu-id="cef74-150">È sufficiente passare a `http://localhost:8080/manager/` e seguire le istruzioni per caricare il file "adal4jsample.war".</span><span class="sxs-lookup"><span data-stu-id="cef74-150">Simply navigate to `http://localhost:8080/manager/` and follow the instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="cef74-151">Verrà eseguita la distribuzione automatica con l'endpoint corretto.</span><span class="sxs-lookup"><span data-stu-id="cef74-151">It will autodeploy for you with the correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cef74-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cef74-152">Next Steps</span></span>
<span data-ttu-id="cef74-153">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="cef74-153">Congratulations!</span></span> <span data-ttu-id="cef74-154">È stata compilata un'applicazione Java funzionante che può autenticare gli utenti, chiamare in modo sicuro le API Web usando OAuth 2.0 e ottenere informazioni di base sull'utente.</span><span class="sxs-lookup"><span data-stu-id="cef74-154">You now have a working Java application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="cef74-155">Se non si è ancora popolato il tenant con alcuni utenti, ora è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="cef74-155">If you haven't already, now is the time to populate your tenant with some users.</span></span>

<span data-ttu-id="cef74-156">Come riferimento, l'esempio completato (senza i valori di configurazione) [è disponibile in un file con estensione .zip qui](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip). In alternativa, è possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="cef74-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

