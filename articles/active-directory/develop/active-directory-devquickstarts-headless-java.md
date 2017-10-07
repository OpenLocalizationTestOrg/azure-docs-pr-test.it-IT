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
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a>Tramite l'applicazione della riga di comando Java tooAccess un'API con Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory rende semplice e diretto toooutsource gestione delle identità dell'applicazione web, fornisce single sign-in e la disconnessione con poche righe di codice.  Nelle App web Java, è possibile eseguire questa operazione utilizzando implementazione Microsoft di hello ADAL4J basato sulla community.

  ADAL4J verrà usato per:

* Utente di hello Sign in hello app usando Azure AD come provider di identità hello.
* Visualizzare alcune informazioni sull'utente hello.
* Sign hello utente all'esterno dell'app hello.

In ordine toodo questo, è necessario:

1. Registrare un'applicazione con Azure AD.
2. Consente di impostare la raccolta di app toouse hello ADAL4J.
3. Utilizzare hello ADAL4J libreria tooissue Accedi e richieste di disconnessione tooAzure Active Directory.
4. Stampare dati sull'utente hello.

tooget avviato, [scaricare scheletro app hello](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).  È inoltre necessario un tenant di Azure Active Directory in cui tooregister l'applicazione.  Se non hai già fatto, [informazioni su come tooget uno](active-directory-howto-tenant.md).

## <a name="1--register-an-application-with-azure-ad"></a>1.  Registrare un'applicazione con Azure AD
tooenable utenti tooauthenticate app, è prima necessario tooregister una nuova applicazione nel tenant.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account e in hello **Directory** elenco, scegliere hello tenant di Active Directory in cui si desidera tooregister l'applicazione.
3. Fare clic su **più servizi** in hello barra di spostamento a sinistra, quindi scegliere **Azure Active Directory**.
4. Fare clic su **App registrations (Registrazioni app)** e scegliere **Aggiungi**.
5. Seguire le istruzioni di hello e creare un nuovo **applicazione Web e/o WebAPI**.
  * Hello **nome** di hello applicazione descriverà tooend utenti applicazione
  * Hello **Sign-On URL** hello URL di base dell'app.  valore predefinito dell'ossatura Hello è `http://localhost:8080/adal4jsample/`.
6. Dopo avere completato la registrazione, AAD assegnerà all'app un ID app univoco.  È necessario che questo valore in hello nelle sezioni seguenti, quindi copiarlo dalla scheda applicazione hello.
7. Da hello **impostazioni** -> **proprietà** pagina per l'applicazione, aggiornare hello URI ID App. Hello **URI ID App** è un identificatore univoco per l'applicazione.  convenzione di Hello è toouse `https://<tenant-domain>/<app-name>`, ad esempio `http://localhost:8080/adal4jsample/`.

Una volta nel portale di hello per le app di creare un **chiave** da hello **impostazioni** pagina per l'applicazione e copiarlo.  Verrà richiesto a breve.

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a>2. Configurare la libreria di app toouse ADAL4J e prerequisiti utilizzando Maven
In questo caso, è possibile configurare il protocollo di autenticazione OpenID Connect di ADAL4J toouse hello.  ADAL4J verrà essere tooissue utilizzato le richieste di accesso e disconnessione, gestire la sessione dell'utente hello e ottenere informazioni sull'utente hello, tra l'altro.

* Nella directory radice di hello del progetto, aprire/creare `pom.xml` e individuare hello `// TODO: provide dependencies for Maven` e sostituire con hello seguente:

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



## <a name="3-create-hello-java-publicclient-file"></a>3. Creare file Java PublicClient hello
Come indicato in precedenza, verrà usato hello dati tooget API Graph su hello utente connesso. Per questo toobe semplificherà è dovrebbe creare sia un file toorepresent un **oggetto Directory** e hello di toorepresent un singolo file **utente** in modo che hello OO di Java può essere utilizzato.

* Creare un file denominato `DirectoryObject.java` che si utilizzerà i dati di base toostore su qualsiasi DirectoryObject (è possibile toouse disponibile questo in un secondo momento per altre query grafico è possibile eseguire). È possibile tagliare e incollare dal codice seguente:

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


## <a name="compile-and-run-hello-sample"></a>Compilare ed eseguire l'esempio hello
Modificare nuovamente le directory radice tooyour ed eseguire hello seguente esempio di comando toobuild hello sufficiente inserire tra loro tramite `maven`. Verranno utilizzate hello `pom.xml` file è stato scritto per le dipendenze.

`$ mvn package`

Nella directory `/targets` dovrebbe essere presente un file `adal4jsample.war`. È possibile che la distribuzione nel contenitore di Tomcat e visitare hello URL 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> È molto semplice toodeploy un WAR con i server Tomcat hello più recenti. Passare semplicemente troppo`http://localhost:8080/manager/` e seguire le istruzioni di hello sul caricamento del ' adal4jsample.war' file. Si verifica un autodeploy automaticamente con l'endpoint corretto hello.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Congratulazioni. È ora un'applicazione Java che sono presenti utenti tooauthenticate possibilità di hello funzionante, in modo sicuro chiamare le API Web mediante OAuth 2.0 e ottenere le informazioni di base utente hello.  Se hai già fatto, è ora hello ora toopopulate tenant con alcuni utenti.

Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file ZIP qui](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), oppure duplicarlo da GitHub:

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

