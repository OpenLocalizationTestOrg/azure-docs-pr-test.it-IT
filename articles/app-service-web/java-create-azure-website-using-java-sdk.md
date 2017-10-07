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
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a><span data-ttu-id="89f34-103">Creare un'App Web in Azure App Service utilizzando hello Azure SDK per Java</span><span class="sxs-lookup"><span data-stu-id="89f34-103">Create a Web App in Azure App Service using hello Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a><span data-ttu-id="89f34-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="89f34-104">Overview</span></span>
<span data-ttu-id="89f34-105">Questa procedura dettagliata illustra come toocreate un SDK di Azure per l'applicazione Java che crea un'App Web nel [Azure App Service][Azure App Service], quindi distribuire tooit un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="89f34-105">This walkthrough shows you how toocreate an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application tooit.</span></span> <span data-ttu-id="89f34-106">È costituita da due parti:</span><span class="sxs-lookup"><span data-stu-id="89f34-106">It consists of two parts:</span></span>

* <span data-ttu-id="89f34-107">Parte 1 viene illustrato come toobuild un'applicazione Java che crea un'app web.</span><span class="sxs-lookup"><span data-stu-id="89f34-107">Part 1 demonstrates how toobuild a Java application that creates a web app.</span></span>
* <span data-ttu-id="89f34-108">Parte 2 di seguito viene illustrato come toocreate un JSP semplice "Hello World" applicazione, quindi utilizzare un FTP client toodeploy codice tooApp servizio.</span><span class="sxs-lookup"><span data-stu-id="89f34-108">Part 2 demonstrates how toocreate a simple JSP "Hello World" application, then use an FTP client toodeploy code tooApp Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89f34-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="89f34-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="89f34-110">Installazioni software</span><span class="sxs-lookup"><span data-stu-id="89f34-110">Software Installations</span></span>
<span data-ttu-id="89f34-111">Hello AzureWebDemo codice dell'applicazione in questo articolo è stato scritto con Azure Java SDK 0.7.0, che è possibile installare utilizzando hello [installazione guidata piattaforma Web] [ Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="89f34-111">hello AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using hello [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="89f34-112">Inoltre, assicurarsi che toouse hello ultima versione di hello [Azure Toolkit per Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="89f34-112">In addition, make sure toouse hello latest version of hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="89f34-113">Dopo aver installato il SDK di hello, aggiornare le dipendenze di hello nel progetto Eclipse eseguendo **Aggiorna** in **repository Maven**, quindi aggiungere di nuovo più recente di ogni pacchetto in hello hello  **Dipendenze** finestra.</span><span class="sxs-lookup"><span data-stu-id="89f34-113">After you install hello SDK, update hello dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add hello latest version of each package in hello **Dependencies** window.</span></span> <span data-ttu-id="89f34-114">È possibile verificare la versione hello del software installato in Eclipse, fare clic su **Guida > Dettagli installazione**; deve avere almeno hello seguenti versioni:</span><span class="sxs-lookup"><span data-stu-id="89f34-114">You can verify hello version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least hello following versions:</span></span>

* <span data-ttu-id="89f34-115">Pacchetto per Librerie di Microsoft Azure per Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="89f34-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="89f34-116">Eclipse IDE per sviluppatori Java EE 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="89f34-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="89f34-117">Creare e configurare risorse cloud in Azure</span><span class="sxs-lookup"><span data-stu-id="89f34-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="89f34-118">Prima di iniziare questa procedura, è necessario toohave una sottoscrizione Azure attiva e impostare un valore predefinito di Active Directory (AD) in Azure.</span><span class="sxs-lookup"><span data-stu-id="89f34-118">Before you begin this procedure, you need toohave an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="89f34-119">Creare una directory di Active Directory (AD) in Azure</span><span class="sxs-lookup"><span data-stu-id="89f34-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="89f34-120">Se non hai già un Active Directory (AD) per la sottoscrizione di Azure, accedere a hello [portale di Azure classico] [ Azure classic portal] con l'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="89f34-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into hello [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="89f34-121">Se si dispone di più sottoscrizioni, fare clic su **sottoscrizioni** directory predefinita selezionare hello e per la sottoscrizione di hello desiderato toouse per questo progetto.</span><span class="sxs-lookup"><span data-stu-id="89f34-121">If you have multiple subscriptions, click **Subscriptions** and select hello default directory for hello subscription you want toouse for this project.</span></span> <span data-ttu-id="89f34-122">Quindi fare clic su **applica** tooswitch toothat la vista delle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="89f34-122">Then click **Apply** tooswitch toothat subscription view.</span></span>

1. <span data-ttu-id="89f34-123">Selezionare **Active Directory** dal menu hello sinistro.</span><span class="sxs-lookup"><span data-stu-id="89f34-123">Select **Active Directory** from hello menu at left.</span></span> <span data-ttu-id="89f34-124">**Fare clic su Nuovo > Directory > Creazione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="89f34-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="89f34-125">In **Aggiungi directory** selezionare **Crea nuova directory**.</span><span class="sxs-lookup"><span data-stu-id="89f34-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="89f34-126">In **Nome**immettere il nome della directory.</span><span class="sxs-lookup"><span data-stu-id="89f34-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="89f34-127">In **Dominio**immettere il nome del dominio.</span><span class="sxs-lookup"><span data-stu-id="89f34-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="89f34-128">Si tratta di un nome di dominio di base che è incluso per impostazione predefinita con la directory. ha il formato di hello `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="89f34-128">This is a basic domain name that is included by default with your directory; it has hello form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="89f34-129">È possibile assegnare un nome in base al nome di directory hello o un altro nome di dominio che si è proprietari.</span><span class="sxs-lookup"><span data-stu-id="89f34-129">You can name it based on hello directory name or another domain name that you own.</span></span> <span data-ttu-id="89f34-130">In un secondo tempo è possibile aggiungere un altro nome di dominio già usato dall'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="89f34-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="89f34-131">In **Paese o area geografica**selezionare le impostazioni locali.</span><span class="sxs-lookup"><span data-stu-id="89f34-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="89f34-132">Per altre informazioni su AD, vedere [Che cos'è una directory di Azure AD][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="89f34-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="89f34-133">Creare un certificato di gestione per Azure</span><span class="sxs-lookup"><span data-stu-id="89f34-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="89f34-134">Hello Azure SDK per Java Usa tooauthenticate certificati di gestione con le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="89f34-134">hello Azure SDK for Java uses management certificates tooauthenticate with Azure subscriptions.</span></span> <span data-ttu-id="89f34-135">Si tratta di x. 509 v3 che è utilizzare tooauthenticate un'applicazione client che utilizza hello tooact di API di gestione del servizio per conto di risorse di sottoscrizione toomanage hello sottoscrizione proprietario.</span><span class="sxs-lookup"><span data-stu-id="89f34-135">These are X.509 v3 certificates you use tooauthenticate a client application that uses hello Service Management API tooact on behalf of hello subscription owner toomanage subscription resources.</span></span>

<span data-ttu-id="89f34-136">codice Hello in questa procedura utilizza tooauthenticate un certificato autofirmato con Azure.</span><span class="sxs-lookup"><span data-stu-id="89f34-136">hello code in this procedure uses a self-signed certificate tooauthenticate with Azure.</span></span> <span data-ttu-id="89f34-137">Per questa procedura, è necessario un certificato toocreate e caricarlo toohello [portale di Azure classico] [ Azure classic portal] in anticipo.</span><span class="sxs-lookup"><span data-stu-id="89f34-137">For this procedure, you need toocreate a certificate and upload it toohello [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="89f34-138">Questa operazione comporta hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="89f34-138">This involves hello following steps:</span></span>

* <span data-ttu-id="89f34-139">Generare un file PFX che rappresenta il certificato client e salvarlo in locale.</span><span class="sxs-lookup"><span data-stu-id="89f34-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="89f34-140">Generare un certificato di gestione (file CER) dal file PFX hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-140">Generate a management certificate (CER file) from hello PFX file.</span></span>
* <span data-ttu-id="89f34-141">Caricare hello CER file tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="89f34-141">Upload hello CER file tooyour Azure subscription.</span></span>
* <span data-ttu-id="89f34-142">Convertire i file PFX hello in JKS, poiché Java utilizza tale tooauthenticate formato utilizzando i certificati.</span><span class="sxs-lookup"><span data-stu-id="89f34-142">Convert hello PFX file into JKS, because Java uses that format tooauthenticate using certificates.</span></span>
* <span data-ttu-id="89f34-143">Scrivere il codice di autenticazione dell'applicazione hello, che fa riferimento a file JKS locale toohello.</span><span class="sxs-lookup"><span data-stu-id="89f34-143">Write hello application's authentication code, which refers toohello local JKS file.</span></span>

<span data-ttu-id="89f34-144">Dopo aver completato questa procedura, si troverà certificato CER hello nella sottoscrizione di Azure e certificato JKS hello si trova nell'unità locale.</span><span class="sxs-lookup"><span data-stu-id="89f34-144">When you complete this procedure, hello CER certificate will reside in your Azure subscription and hello JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="89f34-145">Per altre informazioni sui certificati di gestione, vedere [Creare e caricare un certificato di gestione per Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="89f34-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="89f34-146">Creare un certificato</span><span class="sxs-lookup"><span data-stu-id="89f34-146">Create a certificate</span></span>
<span data-ttu-id="89f34-147">toocreate il proprio certificato autofirmato, aprire una console dei comandi del sistema operativo ed eseguire hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="89f34-147">toocreate your own self-signed certificate, open a command console on your operating system and run hello following commands.</span></span>

> <span data-ttu-id="89f34-148">**Nota:** hello in cui si esegue questo comando deve essere installato hello JDK installato.</span><span class="sxs-lookup"><span data-stu-id="89f34-148">**Note:**  hello computer on which you run this command must have hello JDK installed.</span></span> <span data-ttu-id="89f34-149">Inoltre, hello percorso toohello keytool dipende dal percorso di hello in cui si installa hello JDK.</span><span class="sxs-lookup"><span data-stu-id="89f34-149">Also, hello path toohello keytool depends on hello location in which you install hello JDK.</span></span> <span data-ttu-id="89f34-150">Per ulteriori informazioni, vedere [chiave e strumento di gestione certificati (keytool)] [ Key and Certificate Management Tool (keytool)] nella documentazione online di hello Java.</span><span class="sxs-lookup"><span data-stu-id="89f34-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in hello Java online docs.</span></span>
> 
> 

<span data-ttu-id="89f34-151">file con estensione pfx toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="89f34-151">toocreate hello .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="89f34-152">file con estensione cer toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="89f34-152">toocreate hello .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="89f34-153">dove:</span><span class="sxs-lookup"><span data-stu-id="89f34-153">where:</span></span>

* <span data-ttu-id="89f34-154">`<java-install-dir>`è hello percorso toohello directory in cui è installato Java.</span><span class="sxs-lookup"><span data-stu-id="89f34-154">`<java-install-dir>` is hello path toohello directory in which you installed Java.</span></span>
* <span data-ttu-id="89f34-155">`<keystore-id>`è l'identificatore della voce keystore hello (ad esempio, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="89f34-155">`<keystore-id>` is hello keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="89f34-156">`<cert-store-dir>`hello percorso toohello directory in cui si desiderano toostore certificati (ad esempio `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="89f34-156">`<cert-store-dir>` is hello path toohello directory in which you want toostore certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="89f34-157">`<cert-file-name>`è il nome di hello hello del file di certificato (ad esempio `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="89f34-157">`<cert-file-name>` is hello name of hello certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="89f34-158">`<password>`password hello si sceglie tooprotect hello certificato; deve essere lunga almeno 6 caratteri.</span><span class="sxs-lookup"><span data-stu-id="89f34-158">`<password>` is hello password you choose tooprotect hello certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="89f34-159">È possibile non immettere alcuna password, anche se non è consigliato.</span><span class="sxs-lookup"><span data-stu-id="89f34-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="89f34-160">`<dname>`è hello nome distinto x. 500 toobe associata alias e viene usato come autorità emittente hello e campi soggetto nel certificato autofirmato hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-160">`<dname>` is hello X.500 Distinguished Name toobe associated with alias, and is used as hello issuer and subject fields in hello self-signed certificate.</span></span>

<span data-ttu-id="89f34-161">Per altre informazioni, vedere [Creare e caricare un certificato di gestione per Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="89f34-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-hello-certificate"></a><span data-ttu-id="89f34-162">Caricare il certificato di hello</span><span class="sxs-lookup"><span data-stu-id="89f34-162">Upload hello certificate</span></span>
<span data-ttu-id="89f34-163">tooupload tooAzure un certificato autofirmato, andare toohello **impostazioni** pagina nel portale classico hello e quindi fare clic su hello **i certificati di gestione** scheda. Fare clic su **caricare** nella parte inferiore di hello di hello pagina e passare toohello percorso del file CER hello creato.</span><span class="sxs-lookup"><span data-stu-id="89f34-163">tooupload a self-signed certificate tooAzure, go toohello **Settings** page in hello classic portal, then click hello **Management Certificates** tab. Click **Upload** at hello bottom of hello page and navigate toohello location of hello CER file you created.</span></span>

#### <a name="convert-hello-pfx-file-into-jks"></a><span data-ttu-id="89f34-164">Convertire i file PFX hello in JKS</span><span class="sxs-lookup"><span data-stu-id="89f34-164">Convert hello PFX file into JKS</span></span>
<span data-ttu-id="89f34-165">Hello prompt dei comandi di Windows (in esecuzione come amministratore), cd toohello directory contenente i certificati di hello ed eseguire hello seguente comando, in cui `<java-install-dir>` hello directory in cui è installato Java nel computer in uso:</span><span class="sxs-lookup"><span data-stu-id="89f34-165">In hello Windows Command Prompt (running as admin), cd toohello directory containing hello certificates and run hello following command, where `<java-install-dir>` is hello directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="89f34-166">Quando richiesto, immettere la password di hello destinazione keystore. Questo sarà password hello per file JKS hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-166">When prompted, enter hello destination keystore password; this will be hello password for hello JKS file.</span></span>
2. <span data-ttu-id="89f34-167">Quando richiesto, immettere la password di hello origine keystore. si tratta hello password specificata per il file PFX hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-167">When prompted, enter hello source keystore password; this is hello password you specified for hello PFX file.</span></span>

<span data-ttu-id="89f34-168">due password Hello non è necessario toobe hello stesso.</span><span class="sxs-lookup"><span data-stu-id="89f34-168">hello two passwords do not have toobe hello same.</span></span> <span data-ttu-id="89f34-169">È possibile non immettere alcuna password, anche se non è consigliato.</span><span class="sxs-lookup"><span data-stu-id="89f34-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="89f34-170">Compilare un'applicazione per la creazione di app Web</span><span class="sxs-lookup"><span data-stu-id="89f34-170">Build a Web App creation application</span></span>
### <a name="create-hello-eclipse-workspace-and-maven-project"></a><span data-ttu-id="89f34-171">Creare hello Eclipse dell'area di lavoro e progetti Maven</span><span class="sxs-lookup"><span data-stu-id="89f34-171">Create hello Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="89f34-172">In questa sezione creare un'area di lavoro e un progetto di Maven per hello app creazione applicazione web denominata AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="89f34-172">In this section you create a workspace and a Maven project for hello web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="89f34-173">Creare un nuovo progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="89f34-173">Create a new Maven project.</span></span> <span data-ttu-id="89f34-174">Fare clic su **File > New > Maven Project** (File > Nuovo > Progetto Maven).</span><span class="sxs-lookup"><span data-stu-id="89f34-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="89f34-175">In **New Maven Project** (Nuovo progetto Maven) selezionare **Create a simple project** (Crea progetto semplice) e **Use default workspace location** (Usa percorso area di lavoro predefinito).</span><span class="sxs-lookup"><span data-stu-id="89f34-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="89f34-176">Nella seconda hello di **nuovo progetto di Maven**, specificare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="89f34-176">On hello second page of **New Maven Project**, specify hello following:</span></span>
   
   * <span data-ttu-id="89f34-177">Group ID: `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="89f34-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="89f34-178">Artifact ID: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="89f34-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="89f34-179">Version: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="89f34-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="89f34-180">Packaging: jar</span><span class="sxs-lookup"><span data-stu-id="89f34-180">Packaging: jar</span></span>
   * <span data-ttu-id="89f34-181">Name: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="89f34-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="89f34-182">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="89f34-182">Click **Finish**.</span></span>
3. <span data-ttu-id="89f34-183">Aprire il file di pom.xml hello del nuovo progetto in Esplora progetti.</span><span class="sxs-lookup"><span data-stu-id="89f34-183">Open hello new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="89f34-184">Seleziona hello **dipendenze** scheda. Essendo un nuovo progetto, non è ancora elencato nessun pacchetto.</span><span class="sxs-lookup"><span data-stu-id="89f34-184">Select hello **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="89f34-185">Consente di visualizzare repository Maven hello aperto.</span><span class="sxs-lookup"><span data-stu-id="89f34-185">Open hello Maven Repositories view.</span></span> <span data-ttu-id="89f34-186">Fare clic su **Window > Show View > Other > Maven > Maven Repositories** (Finestra > Mostra vista > Altro > Maven > Repository Maven) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="89f34-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="89f34-187">Hello **repository Maven** visualizzazione verrà visualizzata nella parte inferiore di hello di hello IDE.</span><span class="sxs-lookup"><span data-stu-id="89f34-187">hello **Maven Repositories** view will appear at hello bottom of hello IDE.</span></span>
5. <span data-ttu-id="89f34-188">Aprire **repository globale**, hello rapida **centrale** repository e selezionare **Ricompila indice**.</span><span class="sxs-lookup"><span data-stu-id="89f34-188">Open **Global Repositories**, right-click hello **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="89f34-189">Questo passaggio può richiedere alcuni minuti a seconda della velocità di hello della connessione.</span><span class="sxs-lookup"><span data-stu-id="89f34-189">This step can take several minutes depending on hello speed of your connection.</span></span> <span data-ttu-id="89f34-190">Quando la ricostruzione dell'indice di hello, si dovrebbero vedere pacchetti di Microsoft Azure hello in hello **centrale** repository Maven.</span><span class="sxs-lookup"><span data-stu-id="89f34-190">When hello index rebuilds, you should see hello Microsoft Azure packages in hello **central** Maven repository.</span></span>
6. <span data-ttu-id="89f34-191">In **Dependencies** (Dipendenze) fare clic su **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="89f34-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="89f34-192">In **Enter Group ID...** (Immettere ID gruppo...) immettere `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="89f34-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="89f34-193">Selezionare i pacchetti hello per la gestione di App del servizio Web App e gestione di base:</span><span class="sxs-lookup"><span data-stu-id="89f34-193">Select hello packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="89f34-194">**Nota:** se si siano aggiornando le dipendenze di hello dopo una nuova versione, è necessario toore-aggiungere ognuna delle dipendenze hello in questo elenco.</span><span class="sxs-lookup"><span data-stu-id="89f34-194">**Note:** If you are updating hello dependencies after a new version release, you need toore-add each of hello dependencies in this list.</span></span>
   > <span data-ttu-id="89f34-195">Dopo aver fatto clic **Aggiungi** e selezionare ogni dipendenza, viene visualizzato con hello nuovo numero di versione di hello **dipendenze** elenco.</span><span class="sxs-lookup"><span data-stu-id="89f34-195">After you click **Add** and select each dependency, it appears with hello new version number in hello **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="89f34-196">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="89f34-196">Click **OK**.</span></span> <span data-ttu-id="89f34-197">Hello Azure pacchetti, quindi vengono visualizzati in hello **dipendenze** elenco.</span><span class="sxs-lookup"><span data-stu-id="89f34-197">hello Azure packages then appear in hello **Dependencies** list.</span></span>

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a><span data-ttu-id="89f34-198">Scrittura di codice Java tooCreate un'App Web da chiamare hello Azure SDK</span><span class="sxs-lookup"><span data-stu-id="89f34-198">Writing Java Code tooCreate a Web App by Calling hello Azure SDK</span></span>
<span data-ttu-id="89f34-199">Successivamente, scrivere codice hello chiamate le API in hello Azure SDK per hello toocreate Java App del servizio web app.</span><span class="sxs-lookup"><span data-stu-id="89f34-199">Next, write hello code that calls APIs in hello Azure SDK for Java toocreate hello App Service web app.</span></span>

1. <span data-ttu-id="89f34-200">Creare un codice di punto di ingresso principale Java classe toocontain hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-200">Create a Java class toocontain hello main entry point code.</span></span> <span data-ttu-id="89f34-201">In Esplora progetti, fare clic sul nodo del progetto hello e selezionare **nuovo > classe**.</span><span class="sxs-lookup"><span data-stu-id="89f34-201">In Project Explorer, right-click on hello project node and select **New > Class**.</span></span>
2. <span data-ttu-id="89f34-202">In **nuova classe Java**, nome classe hello `WebCreator` e controllare hello **principale di void statico pubblico** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="89f34-202">In **New Java Class**, name hello class `WebCreator` and check hello **public static void main** checkbox.</span></span> <span data-ttu-id="89f34-203">le selezioni Hello visualizzata come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="89f34-203">hello selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="89f34-204">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="89f34-204">Click **Finish**.</span></span> <span data-ttu-id="89f34-205">file di WebCreator.java Hello viene visualizzato in Esplora progetti.</span><span class="sxs-lookup"><span data-stu-id="89f34-205">hello WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a><span data-ttu-id="89f34-206">La chiamata di un'applicazione servizio Web App hello Azure API tooCreate</span><span class="sxs-lookup"><span data-stu-id="89f34-206">Calling hello Azure API tooCreate an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="89f34-207">Aggiungere le importazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="89f34-207">Add necessary imports</span></span>
<span data-ttu-id="89f34-208">In WebCreator.java, aggiungere hello seguente importazioni; tali importazioni forniscono accesso tooclasses in hello delle raccolte di gestione per l'utilizzo di API di Azure:</span><span class="sxs-lookup"><span data-stu-id="89f34-208">In WebCreator.java, add hello following imports; these imports provide access tooclasses in hello management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-hello-main-entry-point-class"></a><span data-ttu-id="89f34-209">Definire una classe del punto di ingresso principale hello</span><span class="sxs-lookup"><span data-stu-id="89f34-209">Define hello main entry point class</span></span>
<span data-ttu-id="89f34-210">Poiché hello hello AzureWebDemo applicazione mira toocreate un'App del servizio Web App, nome classe principale hello per questa applicazione `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="89f34-210">Because hello purpose of hello AzureWebDemo application is toocreate an App Service Web App, name hello main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="89f34-211">Questa classe fornisce il codice di punto di ingresso principale hello che chiama hello Azure Service Management API toocreate hello web app.</span><span class="sxs-lookup"><span data-stu-id="89f34-211">This class provides hello main entry point code that calls hello Azure Service Management API toocreate hello web app.</span></span>

<span data-ttu-id="89f34-212">Aggiungere hello seguenti definizioni di parametro hello web app e dello spazio Web.</span><span class="sxs-lookup"><span data-stu-id="89f34-212">Add hello following parameter definitions for hello web app and webspace.</span></span> <span data-ttu-id="89f34-213">Sarà necessario tooprovide le proprie informazioni di ID e il certificato di sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="89f34-213">You will need tooprovide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="89f34-214">dove:</span><span class="sxs-lookup"><span data-stu-id="89f34-214">where:</span></span>

* <span data-ttu-id="89f34-215">`<subscription-id>`è l'ID sottoscrizione di Azure hello in cui si desiderano risorse hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="89f34-215">`<subscription-id>` is hello Azure subscription ID in which you want toocreate hello resource.</span></span>
* <span data-ttu-id="89f34-216">`<certificate-store-path>`è hello percorso e nome file toohello JKS file nella directory dell'archivio certificati locale.</span><span class="sxs-lookup"><span data-stu-id="89f34-216">`<certificate-store-path>` is hello path and filename toohello JKS file in your local certificate store directory.</span></span> <span data-ttu-id="89f34-217">Ad esempio, `C:/Certificates/CertificateName.jks` per Linux e `C:\Certificates\CertificateName.jks` per Windows.</span><span class="sxs-lookup"><span data-stu-id="89f34-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="89f34-218">`<certificate-password>`è la password di hello specificato al momento della creazione del certificato JKS.</span><span class="sxs-lookup"><span data-stu-id="89f34-218">`<certificate-password>` is hello password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="89f34-219">`webAppName`può essere qualsiasi nome desiderato; Questa procedura utilizza nome hello `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="89f34-219">`webAppName` can be any name you choose; this procedure uses hello name `WebDemoWebApp`.</span></span> <span data-ttu-id="89f34-220">il nome di dominio completo di Hello è hello `webAppName` con hello `domainName` aggiunto, pertanto in questo caso hello completo dominio è `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="89f34-220">hello full domain name is hello `webAppName` with hello `domainName` appended, so in this case hello full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="89f34-221">`domainName` deve essere specificato come indicato sopra.</span><span class="sxs-lookup"><span data-stu-id="89f34-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="89f34-222">`webSpaceName`deve essere uno dei valori hello definiti in hello [WebSpaceNames] [ WebSpaceNames] classe.</span><span class="sxs-lookup"><span data-stu-id="89f34-222">`webSpaceName` should be one of hello values defined in hello [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="89f34-223">`appServicePlanName` deve essere specificato come indicato sopra.</span><span class="sxs-lookup"><span data-stu-id="89f34-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="89f34-224">**Nota:** ogni volta che si esegue l'applicazione, è necessario toochange hello valore `webAppName` e `appServicePlanName` (o eliminare l'app web hello nel portale di Azure hello) prima di eseguire nuovamente l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-224">**Note:** Each time you run this application, you need toochange hello value of `webAppName` and `appServicePlanName` (or delete hello web app on hello Azure Portal) before running hello application again.</span></span> <span data-ttu-id="89f34-225">In caso contrario, viene eseguito perché hello stessa risorsa già esistente in Azure.</span><span class="sxs-lookup"><span data-stu-id="89f34-225">Otherwise, execution will fail because hello same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-hello-web-creation-method"></a><span data-ttu-id="89f34-226">Definizione di metodo di creazione di hello web</span><span class="sxs-lookup"><span data-stu-id="89f34-226">Define hello web creation method</span></span>
<span data-ttu-id="89f34-227">Successivamente, definire un'app web di metodo toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-227">Next, define a method toocreate hello web app.</span></span> <span data-ttu-id="89f34-228">Questo metodo, `createWebApp`, specifica i parametri di hello di hello web app e uno spazio Web hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-228">This method, `createWebApp`, specifies hello parameters of hello web app and hello webspace.</span></span> <span data-ttu-id="89f34-229">Inoltre crea e configura i client di gestione App Web del servizio App di hello, che è definito da hello [WebSiteManagementClient] [ WebSiteManagementClient] oggetto.</span><span class="sxs-lookup"><span data-stu-id="89f34-229">It also creates and configures hello App Service Web Apps management client, which is defined by hello [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="89f34-230">il client di gestione di Hello è toocreating chiave Web App.</span><span class="sxs-lookup"><span data-stu-id="89f34-230">hello management client is key toocreating Web Apps.</span></span> <span data-ttu-id="89f34-231">Fornisce i servizi web RESTful che consente applicazioni toomanage web App (esecuzione di operazioni, ad esempio la creazione, aggiornamento ed eliminazione) chiamando l'API di Gestione servizio hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-231">It provides RESTful web services that allow applications toomanage web apps (performing operations such as create, update, and delete) by calling hello service management API.</span></span>

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

<span data-ttu-id="89f34-232">il codice Hello sarà l'output hello di stato HTTP della risposta hello che indica l'esito positivo o negativo e se ha esito positivo, verrà output nome hello di hello app web creata.</span><span class="sxs-lookup"><span data-stu-id="89f34-232">hello code will output hello HTTP status of hello response indicating success or failure, and if successful, will output hello name of hello created web app.</span></span>

#### <a name="define-hello-main-method"></a><span data-ttu-id="89f34-233">Definire il metodo Main () hello</span><span class="sxs-lookup"><span data-stu-id="89f34-233">Define hello main() method</span></span>
<span data-ttu-id="89f34-234">Fornire il codice del metodo Main () hello chiamate createWebApp() toocreate hello web app.</span><span class="sxs-lookup"><span data-stu-id="89f34-234">Provide hello main() method code that calls createWebApp() toocreate hello web app.</span></span>

<span data-ttu-id="89f34-235">Infine chiamare `createWebApp` da `main`:</span><span class="sxs-lookup"><span data-stu-id="89f34-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a><span data-ttu-id="89f34-236">Eseguire un'applicazione hello e verificare la creazione di app web</span><span class="sxs-lookup"><span data-stu-id="89f34-236">Run hello application and verify web app creation</span></span>
<span data-ttu-id="89f34-237">Fare clic su tooverify che l'applicazione viene eseguita, **eseguire > eseguire**.</span><span class="sxs-lookup"><span data-stu-id="89f34-237">tooverify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="89f34-238">Al termine dell'esecuzione dell'applicazione hello, dovrebbe essere hello seguente output nella console di Eclipse hello:</span><span class="sxs-lookup"><span data-stu-id="89f34-238">When hello application completes running, you should see hello following output in hello Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="89f34-239">Accedere al portale di Azure classico hello e fare clic su **App Web**.</span><span class="sxs-lookup"><span data-stu-id="89f34-239">Log into hello Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="89f34-240">Hello nuova app web verrà visualizzato nell'elenco di App Web hello entro pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="89f34-240">hello new web app should appear in hello Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-toohello-web-app"></a><span data-ttu-id="89f34-241">Distribuzione di un'App Web di toohello di applicazione</span><span class="sxs-lookup"><span data-stu-id="89f34-241">Deploying an Application toohello Web App</span></span>
<span data-ttu-id="89f34-242">Dopo aver eseguito AzureWebDemo si create hello nuova app web, accedere al portale classico hello, fare clic su **App Web**e selezionare **WebDemoWebApp** in hello **App Web** elenco.</span><span class="sxs-lookup"><span data-stu-id="89f34-242">After you have run AzureWebDemo and created hello new web app, log into hello classic portal, click **Web Apps**, and select **WebDemoWebApp** in hello **Web Apps** list.</span></span> <span data-ttu-id="89f34-243">Nella pagina dashboard dell'app web hello, fare clic su **Sfoglia** (oppure fare clic su URL hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span><span class="sxs-lookup"><span data-stu-id="89f34-243">In hello web app's dashboard page, click **Browse** (or click hello URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span></span> <span data-ttu-id="89f34-244">Una pagina di segnaposto vuoto, verrà visualizzato perché nessun contenuto è ancora stato pubblicato toohello web app.</span><span class="sxs-lookup"><span data-stu-id="89f34-244">You will see a blank placeholder page, because no content has been published toohello web app yet.</span></span>

<span data-ttu-id="89f34-245">Successivamente si verrà creare un'applicazione "Hello World" e distribuirlo toohello web app.</span><span class="sxs-lookup"><span data-stu-id="89f34-245">Next you will create a "Hello World" application and deploy it toohello web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="89f34-246">Creare un'applicazione Hello World JSP</span><span class="sxs-lookup"><span data-stu-id="89f34-246">Create a JSP Hello World application</span></span>
#### <a name="create-hello-application"></a><span data-ttu-id="89f34-247">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="89f34-247">Create hello application</span></span>
<span data-ttu-id="89f34-248">In ordine toodemonstrate come toodeploy web toohello un'applicazione, hello seguente procedura illustra come toocreate una semplice applicazione "Hello World" Java e caricarlo toohello App del servizio Web App che ha creato l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="89f34-248">In order toodemonstrate how toodeploy an application toohello web, hello following procedure shows you how toocreate a simple "Hello World" Java application and upload it toohello App Service Web App that your application created.</span></span>

1. <span data-ttu-id="89f34-249">Fare clic su **File > New > Dynamic Web Project** (File > Nuovo > Progetto Web dinamico).</span><span class="sxs-lookup"><span data-stu-id="89f34-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="89f34-250">Denominarlo `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="89f34-250">Name it `JSPHello`.</span></span> <span data-ttu-id="89f34-251">Non è necessario toochange tutte le altre impostazioni in questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="89f34-251">You do not need toochange any other settings in this dialog.</span></span> <span data-ttu-id="89f34-252">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="89f34-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="89f34-253">In Esplora progetti espandere hello **JSPHello** del progetto, fare doppio clic su **WebContent**, quindi fare clic su **nuovo > File JSP**.</span><span class="sxs-lookup"><span data-stu-id="89f34-253">In Project Explorer, expand hello **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="89f34-254">Nella finestra di dialogo New JSP File hello, assegnare un nome nuovo file hello `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="89f34-254">In hello New JSP File dialog, name hello new file `index.jsp`.</span></span> <span data-ttu-id="89f34-255">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="89f34-255">Click **Next**.</span></span>
3. <span data-ttu-id="89f34-256">In hello **Select JSP Template** selezionare **New JSP File (html)** e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="89f34-256">In hello **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="89f34-257">In index.jsp, aggiungere hello seguente di codice hello `<head>` e `<body>` tag sezioni:</span><span class="sxs-lookup"><span data-stu-id="89f34-257">In index.jsp, add hello following code in hello `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a><span data-ttu-id="89f34-258">Eseguire un'applicazione Hello World hello in localhost</span><span class="sxs-lookup"><span data-stu-id="89f34-258">Run hello Hello World application in localhost</span></span>
<span data-ttu-id="89f34-259">Prima di eseguire questa applicazione, è necessario tooconfigure alcune proprietà.</span><span class="sxs-lookup"><span data-stu-id="89f34-259">Before you run this application, you need tooconfigure a few properties.</span></span>

1. <span data-ttu-id="89f34-260">Pulsante destro del mouse hello **JSPHello** del progetto e selezionare **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="89f34-260">Right-click hello **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="89f34-261">In hello **proprietà** finestra di dialogo: selezionare **Java Build Path**selezionare hello **ordinare ed esportare** scheda **JRE sistema libreria**, quindi fare clic su **Backup** toomove è toohello parte superiore dell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-261">In hello **Properties** dialog: select **Java Build Path**, select hello **Order and Export** tab, check **JRE System Library**, then click **Up** toomove it toohello top of hello list.</span></span>
   
    ![][4]
3. <span data-ttu-id="89f34-262">Anche in hello **proprietà** finestra di dialogo: selezionare **destinazione runtime** e fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="89f34-262">Also in hello **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="89f34-263">In hello **nuovo ambiente di Runtime Server** finestra di dialogo, selezionare un server, ad esempio **versione 7.0 Apache Tomcat** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="89f34-263">In hello **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="89f34-264">In hello **Server Tomcat** finestra di dialogo, impostare **nome** troppo`Apache Tomcat v7.0`e impostare **Directory di installazione di Tomcat** toohello directory in cui è installata la versione hello di Server Tomcat da toouse.</span><span class="sxs-lookup"><span data-stu-id="89f34-264">In hello **Tomcat Server** dialog, set **Name** too`Apache Tomcat v7.0`, and set **Tomcat Installation Directory** toohello directory in which you installed hello version of Tomcat server you want toouse.</span></span>
   
    ![][5]
   
    <span data-ttu-id="89f34-265">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="89f34-265">Click **Finish**.</span></span>
5. <span data-ttu-id="89f34-266">È quindi restituire toohello **destinazione runtime** pagina di hello **proprietà** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="89f34-266">You then return toohello **Targeted Runtimes** page of hello **Properties** dialog.</span></span> <span data-ttu-id="89f34-267">Selezionare **Apache Tomcat v7.0**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="89f34-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="89f34-268">In Eclipse hello **eseguire** menu, fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="89f34-268">In hello Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="89f34-269">In hello **runas** finestra di dialogo Seleziona **eseguire sul Server**.</span><span class="sxs-lookup"><span data-stu-id="89f34-269">In hello **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="89f34-270">In hello **eseguire sul Server** finestra di dialogo Seleziona **Tomcat versione 7.0 Server**:</span><span class="sxs-lookup"><span data-stu-id="89f34-270">In hello **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="89f34-271">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="89f34-271">Click **Finish**.</span></span>
7. <span data-ttu-id="89f34-272">Hello quando l'esecuzione dell'applicazione, si dovrebbe vedere hello **JSPHello** pagina visualizzata in una finestra localhost in Eclipse (`http://localhost:8080/JSPHello/`), visualizzazione hello il seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="89f34-272">When hello application runs, you should see hello **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying hello following message:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a><span data-ttu-id="89f34-273">Esportare un'applicazione hello come un WAR</span><span class="sxs-lookup"><span data-stu-id="89f34-273">Export hello application as a WAR</span></span>
<span data-ttu-id="89f34-274">Esportare il file di progetto web hello come un file web archive (WAR) in modo che è possibile distribuire app web toohello.</span><span class="sxs-lookup"><span data-stu-id="89f34-274">Export hello web project files as a web archive (WAR) file so that you can deploy it toohello web app.</span></span> <span data-ttu-id="89f34-275">Hello seguente file di progetto web si trovano nella cartella WebContent hello:</span><span class="sxs-lookup"><span data-stu-id="89f34-275">hello following web project files reside in hello WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="89f34-276">Fare clic sulla cartella WebContent hello e selezionare **esportare**.</span><span class="sxs-lookup"><span data-stu-id="89f34-276">Right-click hello WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="89f34-277">In hello **esportare selezionare** finestra di dialogo, fare clic su **Web > WAR** file, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="89f34-277">In hello **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="89f34-278">In hello **WAR esportare** finestra di dialogo, selezionare directory src hello nel progetto corrente di hello e includere hello nome di file WAR hello alla fine di hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-278">In hello **WAR Export** dialog, select hello src directory in hello current project, and include hello name of hello WAR file at hello end.</span></span> <span data-ttu-id="89f34-279">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="89f34-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="89f34-280">Per ulteriori informazioni sulla distribuzione dei file WAR, vedere [aggiungere un tooAzure applicazione Java App del servizio Web App](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="89f34-280">For more information on deploying WAR files, see [Add a Java application tooAzure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-hello-hello-world-application-using-ftp"></a><span data-ttu-id="89f34-281">Distribuzione di hello Hello World applicazione tramite FTP</span><span class="sxs-lookup"><span data-stu-id="89f34-281">Deploying hello Hello World Application Using FTP</span></span>
<span data-ttu-id="89f34-282">Selezionare un'applicazione di terze parti FTP client toopublish hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-282">Select a third-party FTP client toopublish hello application.</span></span> <span data-ttu-id="89f34-283">Questa procedura vengono illustrate due opzioni: console Kudu hello compilato in Azure. e FileZilla, uno strumento largamente usato con un'interfaccia utente grafica, pratico.</span><span class="sxs-lookup"><span data-stu-id="89f34-283">This procedure describes two options: hello Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="89f34-284">**Nota:** hello Azure Toolkit per Eclipse supporta gli account di toostorage di distribuzione e cloud services, ma non supporta attualmente App tooweb di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="89f34-284">**Note:** hello Azure Toolkit for Eclipse supports deployment toostorage accounts and cloud services, but does not currently support deployment tooweb apps.</span></span> <span data-ttu-id="89f34-285">È possibile distribuire gli account toostorage e usando un progetto di distribuzione di Azure, come descritto in servizi cloud [creando un'applicazione Hello World per Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), ma non tooweb app.</span><span class="sxs-lookup"><span data-stu-id="89f34-285">You can deploy toostorage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not tooweb apps.</span></span> <span data-ttu-id="89f34-286">Utilizzare altri metodi, ad esempio FTP o GitHub tootransfer file tooyour app web.</span><span class="sxs-lookup"><span data-stu-id="89f34-286">Use other methods such as FTP or GitHub tootransfer files tooyour web app.</span></span>
> 
> <span data-ttu-id="89f34-287">**Nota:** non è consigliabile utilizzare FTP dal prompt dei comandi di Windows hello (hello utilità riga di comando FTP.EXE fornito con Windows).</span><span class="sxs-lookup"><span data-stu-id="89f34-287">**Note:** We do not recommend using FTP from hello Windows command prompt (hello command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="89f34-288">I client FTP che utilizzano active FTP, ad esempio FTP.EXE, spesso failover toowork firewall.</span><span class="sxs-lookup"><span data-stu-id="89f34-288">FTP clients that use active FTP, such as FTP.EXE, often fail toowork over firewalls.</span></span> <span data-ttu-id="89f34-289">FTP Active specifica un indirizzo interno basato su LAN, toowhich un FTP server probabilmente avrà esito negativo tooconnect.</span><span class="sxs-lookup"><span data-stu-id="89f34-289">Active FTP specifies an internal LAN-based address, toowhich an FTP server will likely fail tooconnect.</span></span>
> 
> 

<span data-ttu-id="89f34-290">Per ulteriori informazioni sulla distribuzione tooan App del servizio web app tramite FTP, vedere hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="89f34-290">For more information on deployment tooan App Service web app using FTP, see hello following topics:</span></span>

* [<span data-ttu-id="89f34-291">Distribuire mediante un'utilità FTP</span><span class="sxs-lookup"><span data-stu-id="89f34-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="89f34-292">Imposta credenziali di distribuzione</span><span class="sxs-lookup"><span data-stu-id="89f34-292">Set up deployment credentials</span></span>
<span data-ttu-id="89f34-293">Assicurarsi di aver eseguito hello **AzureWebDemo** toocreate applicazione un'app web.</span><span class="sxs-lookup"><span data-stu-id="89f34-293">Make sure you have run hello **AzureWebDemo** application toocreate a web app.</span></span> <span data-ttu-id="89f34-294">Percorso dei file di toothis verrà trasferita.</span><span class="sxs-lookup"><span data-stu-id="89f34-294">You will transfer files toothis location.</span></span>

1. <span data-ttu-id="89f34-295">Accedere al portale classico di hello e fare clic su **App Web**.</span><span class="sxs-lookup"><span data-stu-id="89f34-295">Log into hello classic portal and click **Web Apps**.</span></span> <span data-ttu-id="89f34-296">Assicurarsi che **WebDemoWebApp** viene visualizzato nell'elenco di hello di App web e assicurarsi che sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="89f34-296">Make sure **WebDemoWebApp** appears in hello list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="89f34-297">Fare clic su **WebDemoWebApp** tooopen relativo **Dashboard** pagina.</span><span class="sxs-lookup"><span data-stu-id="89f34-297">Click **WebDemoWebApp** tooopen its **Dashboard** page.</span></span>
2. <span data-ttu-id="89f34-298">In hello **Dashboard** pagina **Quick Glance**, fare clic su **impostare le credenziali di distribuzione** (se già si dispone di credenziali di distribuzione, legge  **Reimpostare le credenziali di distribuzione**).</span><span class="sxs-lookup"><span data-stu-id="89f34-298">On hello **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="89f34-299">Le credenziali di distribuzione sono associate a un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="89f34-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="89f34-300">È necessario toospecify un nome utente e password che è possibile utilizzare toodeploy utilizzando Git e FTP.</span><span class="sxs-lookup"><span data-stu-id="89f34-300">You need toospecify a username and password that you can use toodeploy using Git and FTP.</span></span> <span data-ttu-id="89f34-301">È possibile utilizzare queste app di web tooany toodeploy credenziali in tutte le sottoscrizioni di Azure associate all'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="89f34-301">You can use these credentials toodeploy tooany web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="89f34-302">Fornire le credenziali di distribuzione Git e FTP nella finestra di dialogo, hello e hello record username e password per un utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="89f34-302">Provide Git and FTP deployment credentials in hello dialog, and record hello username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="89f34-303">Ottenere informazioni di connessione a FTP</span><span class="sxs-lookup"><span data-stu-id="89f34-303">Get FTP connection information</span></span>
<span data-ttu-id="89f34-304">toouse FTP toodeploy applicazione file appena creato toohello app web, è necessario tooobtain le informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="89f34-304">toouse FTP toodeploy application files toohello newly created web app, you need tooobtain connection information.</span></span> <span data-ttu-id="89f34-305">Esistono due modi tooobtain informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="89f34-305">There are two ways tooobtain connection information.</span></span> <span data-ttu-id="89f34-306">Un modo consiste toovisit hello web app **Dashboard** pagina; hello altro consiste toodownload hello web app profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="89f34-306">One way is toovisit hello web app's **Dashboard** page; hello other way is toodownload hello web app's publish profile.</span></span> <span data-ttu-id="89f34-307">profilo di pubblicazione Hello è un file XML che fornisce informazioni quali le credenziali di accesso e del nome host FTP per le app web nel servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="89f34-307">hello publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="89f34-308">È possibile utilizzare questa app web di tooany toodeploy di nome utente e password in tutte le sottoscrizioni associate hello account Azure, non solo questo.</span><span class="sxs-lookup"><span data-stu-id="89f34-308">You can use this username and password toodeploy tooany web app in all subscriptions associated with hello Azure account, not only this one.</span></span>

<span data-ttu-id="89f34-309">le informazioni di connessione FTP tooobtain pannello dell'app web hello in hello [portale Azure][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="89f34-309">tooobtain FTP connection information from hello web app's blade in hello [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="89f34-310">In **Essentials**, trovare e copiare hello **nome host FTP**.</span><span class="sxs-lookup"><span data-stu-id="89f34-310">Under **Essentials**, find and copy hello **FTP hostname**.</span></span> <span data-ttu-id="89f34-311">Questo è un URI simile troppo`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="89f34-311">This is a URI similar too`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="89f34-312">In **Essentials** trovare e copiare il **Nome utente FTP/distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="89f34-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="89f34-313">Questo avrà un formato hello *webappname\deployment-username*, ad esempio `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="89f34-313">This will have hello form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="89f34-314">profilo di pubblicazione tooobtain hello le informazioni di connessione FTP:</span><span class="sxs-lookup"><span data-stu-id="89f34-314">tooobtain FTP connection information from hello publish profile:</span></span>

1. <span data-ttu-id="89f34-315">Nel pannello dell'app web hello, fare clic su **profilo di pubblicazione Get**.</span><span class="sxs-lookup"><span data-stu-id="89f34-315">In hello web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="89f34-316">Questo verrà scaricato un file con estensione publishsettings tooyour un'unità locale.</span><span class="sxs-lookup"><span data-stu-id="89f34-316">This will download a .publishsettings file tooyour local drive.</span></span>
2. <span data-ttu-id="89f34-317">Aprire file con estensione publishsettings hello in un editor XML o un editor di testo e individuare hello `<publishProfile>` elemento contenente `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="89f34-317">Open hello .publishsettings file in an XML editor or text editor and find hello `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="89f34-318">Che dovrebbe essere simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="89f34-318">It should look like hello following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="89f34-319">Si noti che app web hello `publishProfile` le impostazioni di eseguire il mapping di impostazioni di gestione del sito FileZilla toohello come segue:</span><span class="sxs-lookup"><span data-stu-id="89f34-319">Note that hello web app's `publishProfile` settings map toohello FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="89f34-320">`publishUrl`è hello identico **nome host FTP**, hello valore impostato in **Host**.</span><span class="sxs-lookup"><span data-stu-id="89f34-320">`publishUrl` is hello same as **FTP host name**, hello value you set in **Host**.</span></span>
* <span data-ttu-id="89f34-321">`publishMethod="FTP"`indica che è stata impostata **protocollo** troppo**FTP - File Transfer Protocol**, e **crittografia** troppo**utilizzare FTP normale**.</span><span class="sxs-lookup"><span data-stu-id="89f34-321">`publishMethod="FTP"` means that you set **Protocol** too**FTP - File Transfer Protocol**, and **Encryption** too**Use plain FTP**.</span></span>
* <span data-ttu-id="89f34-322">`userName`e `userPWD` sono chiavi per hello valori effettivi di nome utente e password specificata quando si reimposta le credenziali di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-322">`userName` and `userPWD` are keys for hello actual username and password values you specified when you reset hello deployment credentials.</span></span> <span data-ttu-id="89f34-323">`userName`è hello identico **distribuzione / utente FTP**.</span><span class="sxs-lookup"><span data-stu-id="89f34-323">`userName` is hello same as **Deployment / FTP user**.</span></span> <span data-ttu-id="89f34-324">Viene eseguito il mapping troppo**utente** e **Password** in FileZilla.</span><span class="sxs-lookup"><span data-stu-id="89f34-324">They map too**User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="89f34-325">`ftpPassiveMode="True"`indica il che utilizzo di tale sito FTP hello trasferimento FTP passivo. Selezionare **passivo** su hello **le impostazioni del trasferimento** scheda.</span><span class="sxs-lookup"><span data-stu-id="89f34-325">`ftpPassiveMode="True"` means that hello FTP site uses passive FTP transfer; select **Passive** on hello **Transfer Settings** tab.</span></span>

#### <a name="configure-hello-web-app-toohost-a-java-application"></a><span data-ttu-id="89f34-326">Configurare l'App Web di hello toohost un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="89f34-326">Configure hello Web App toohost a Java application</span></span>
<span data-ttu-id="89f34-327">Prima di pubblicare un'applicazione hello, è necessario toochange alcune impostazioni di configurazione in modo che hello app web può ospitare un'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="89f34-327">Before you publish hello application, you need toochange a few configuration settings so that hello web app can host a Java application.</span></span>

1. <span data-ttu-id="89f34-328">Nel portale classico hello andare dell'app web toohello **Dashboard** pagina e fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="89f34-328">In hello classic portal, go toohello web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="89f34-329">In hello **configura** specificare hello seguenti impostazioni.</span><span class="sxs-lookup"><span data-stu-id="89f34-329">On hello **Configure** page, specify hello following settings.</span></span>
2. <span data-ttu-id="89f34-330">In **versione Java** predefinito hello è **Off**; selezionare la versione di Java hello destinata l'applicazione, ad esempio 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="89f34-330">In **Java version** hello default is **Off**; select hello Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="89f34-331">Al termine dell'operazione, assicurarsi anche che **contenitore Web** è impostato tooa versione del Server Tomcat.</span><span class="sxs-lookup"><span data-stu-id="89f34-331">After you do this, also make sure that **Web container** is set tooa version of Tomcat Server.</span></span>
3. <span data-ttu-id="89f34-332">In **documenti predefiniti**, aggiungere index.jsp e spostarlo toohello parte superiore dell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-332">In **Default Documents**, add index.jsp and move it up toohello top of hello list.</span></span> <span data-ttu-id="89f34-333">(il file predefinito hello per le app web è hostingstart.html).</span><span class="sxs-lookup"><span data-stu-id="89f34-333">(hello default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="89f34-334">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="89f34-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="89f34-335">Pubblicare l'applicazione con Kudu</span><span class="sxs-lookup"><span data-stu-id="89f34-335">Publish your application using Kudu</span></span>
<span data-ttu-id="89f34-336">Un'applicazione hello toopublish unidirezionale è hello toouse che kudu debug console integrata in Azure.</span><span class="sxs-lookup"><span data-stu-id="89f34-336">One way toopublish hello application is toouse hello Kudu debug console built into Azure.</span></span> <span data-ttu-id="89f34-337">Kudu è noto toobe stabile e coerente con l'App del servizio Web App e il Server Tomcat.</span><span class="sxs-lookup"><span data-stu-id="89f34-337">Kudu is known toobe stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="89f34-338">Console hello per l'app web hello è accedere esplorando tooa URL di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="89f34-338">You access hello console for hello web app by browsing tooa URL of hello following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="89f34-339">Per questa procedura, si trova nel seguente URL; hello console Kudu hello Cerca nel percorso toothis:</span><span class="sxs-lookup"><span data-stu-id="89f34-339">For this procedure, hello Kudu console is located at hello following URL; browse toothis location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="89f34-340">Scegliere dal menu in alto hello **Console Debug > CMD**.</span><span class="sxs-lookup"><span data-stu-id="89f34-340">From hello top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="89f34-341">Nella riga di comando hello console passare troppo`/site/wwwroot` (oppure fare clic su `site`, quindi `wwwroot` nella visualizzazione directory hello nella parte superiore di hello della pagina hello):</span><span class="sxs-lookup"><span data-stu-id="89f34-341">In hello console command line, navigate too`/site/wwwroot` (or click `site`, then `wwwroot` in hello directory view at hello top of hello page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="89f34-342">Dopo aver specificato **Java version**, il server Tomcat dovrebbe creare una directory webapps.</span><span class="sxs-lookup"><span data-stu-id="89f34-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="89f34-343">Nella riga di comando console hello, passare toohello WebApp directory:</span><span class="sxs-lookup"><span data-stu-id="89f34-343">In hello console command line, navigate toohello webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="89f34-344">Trascinare JSPHello.war da `<project-path>/JSPHello/src/` e rilasciarlo in visualizzazione di directory Kudu hello in `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="89f34-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into hello Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="89f34-345">Non trascinarla area "Trascinare qui tooupload e zip" toohello, perché verrà decomprimerlo Tomcat.</span><span class="sxs-lookup"><span data-stu-id="89f34-345">Do not drag it toohello "Drag here tooupload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="89f34-346">Nel primo JSPHello.war viene visualizzata nell'area di directory di hello da se stessa:</span><span class="sxs-lookup"><span data-stu-id="89f34-346">At first JSPHello.war appears in hello directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="89f34-347">In un breve periodo di tempo (probabilmente meno di 5 minuti) il Server Tomcat verrà decomprimere file WAR hello in una directory JSPHello decompressa.</span><span class="sxs-lookup"><span data-stu-id="89f34-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip hello WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="89f34-348">Fare clic su toosee directory radice di hello se index.jsp è stato decompresso e copiati in tale posizione.</span><span class="sxs-lookup"><span data-stu-id="89f34-348">Click hello ROOT directory toosee whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="89f34-349">In caso affermativo, spostarsi indietro toohello WebApp directory toosee se hello decompressi JSPHello directory è stata creata.</span><span class="sxs-lookup"><span data-stu-id="89f34-349">If so, navigate back toohello webapps directory toosee whether hello unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="89f34-350">Se questi elementi non sono visibili, attendere e riprovare.</span><span class="sxs-lookup"><span data-stu-id="89f34-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="89f34-351">Pubblicare l'applicazione con FileZilla (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="89f34-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="89f34-352">Un altro strumento, è possibile utilizzare un'applicazione hello toopublish è FileZilla, un client FTP comune di terze parti con un'interfaccia utente grafica, pratico.</span><span class="sxs-lookup"><span data-stu-id="89f34-352">Another tool you can use toopublish hello application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="89f34-353">È possibile scaricare e installare FileZilla da [http://filezilla-project.org/](http://filezilla-project.org/) se non lo si ha già.</span><span class="sxs-lookup"><span data-stu-id="89f34-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="89f34-354">Per ulteriori informazioni sull'utilizzo di client hello, vedere hello [FileZilla documentazione](https://wiki.filezilla-project.org/Documentation) e questo post di blog su [client FTP - parte 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="89f34-354">For more information on using hello client, see hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="89f34-355">In FileZilla fare clic su **File > Gestore siti**.</span><span class="sxs-lookup"><span data-stu-id="89f34-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="89f34-356">In hello **di gestione del sito** finestra di dialogo, fare clic su **nuovo sito**.</span><span class="sxs-lookup"><span data-stu-id="89f34-356">In hello **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="89f34-357">Verrà visualizzato un nuovo sito FTP vuoto **voce selezionare** chiesto tooprovide un nome.</span><span class="sxs-lookup"><span data-stu-id="89f34-357">A new blank FTP site will appear in **Select Entry** prompting you tooprovide a name.</span></span> <span data-ttu-id="89f34-358">Per questa procedura, denominarlo `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="89f34-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="89f34-359">In hello **generale** , specificare hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="89f34-359">On hello **General** tab, specify hello following settings:</span></span>
   
   * <span data-ttu-id="89f34-360">**Host:** invio hello **nome Host FTP** copiata dal dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-360">**Host:** Enter hello **FTP Host Name** that you copied from hello dashboard.</span></span>
   * <span data-ttu-id="89f34-361">**Porta:** (lasciare vuoto questo campo perché si tratta di un trasferimento passivo e server hello determinerà hello porta toouse.)</span><span class="sxs-lookup"><span data-stu-id="89f34-361">**Port:** (Leave this blank, as this is a passive transfer and hello server will determine hello port toouse.)</span></span>
   * <span data-ttu-id="89f34-362">**Protocollo:** protocollo per il trasferimento del file FTP</span><span class="sxs-lookup"><span data-stu-id="89f34-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="89f34-363">**Crittografia:** usare FTP semplice</span><span class="sxs-lookup"><span data-stu-id="89f34-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="89f34-364">**Tipo di accesso:** normale</span><span class="sxs-lookup"><span data-stu-id="89f34-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="89f34-365">**Utente:** invio hello distribuzione / FTP utente copiato dal dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-365">**User:** Enter hello Deployment / FTP user that you copied from hello dashboard.</span></span> <span data-ttu-id="89f34-366">Si tratta di hello FTP nome utente completo, che ha un formato hello *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="89f34-366">This is hello full FTP username, which has hello form *webappname\username*.</span></span>
   * <span data-ttu-id="89f34-367">**Password:** immettere la password di hello specificato quando si imposta le credenziali di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-367">**Password:** Enter hello password that you specified when you set hello deployment credentials.</span></span>
     
     <span data-ttu-id="89f34-368">In hello **le impostazioni del trasferimento** , selezionare **passivo**.</span><span class="sxs-lookup"><span data-stu-id="89f34-368">On hello **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="89f34-369">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="89f34-369">Click **Connect**.</span></span> <span data-ttu-id="89f34-370">Se ha esito positivo, la console del FileZilla visualizzerà un `Status: Connected` messaggio ed emettere un `LIST` comando contenuto della directory toolist hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command toolist hello directory contents.</span></span>
4. <span data-ttu-id="89f34-371">In hello **locale** pannello sito, la directory di origine selezionare hello in cui i file JSPHello.war hello risiede; percorso hello sarà simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="89f34-371">In hello **Local** site panel, select hello source directory in which hello JSPHello.war file resides; hello path will be similar toohello following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="89f34-372">In hello **remoto** pannello sito, la cartella di destinazione selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-372">In hello **Remote** site panel, select hello destination folder.</span></span> <span data-ttu-id="89f34-373">Si distribuirà toohello di file WAR hello `webapps` directory radice dell'applicazione web hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-373">You will deploy hello WAR file toohello `webapps` directory under hello web app's root.</span></span> <span data-ttu-id="89f34-374">Passare troppo`/site/wwwroot`, fare clic su `wwwroot`e selezionare **Crea directory**.</span><span class="sxs-lookup"><span data-stu-id="89f34-374">Navigate too`/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="89f34-375">Directory di hello nome `webapps` e immettere una directory.</span><span class="sxs-lookup"><span data-stu-id="89f34-375">Name hello directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="89f34-376">Trasferimento JSPHello.war troppo`/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="89f34-376">Transfer JSPHello.war too`/site/wwwroot/webapps`.</span></span> <span data-ttu-id="89f34-377">Selezionare JSPHello.war hello **locale** elenco dei file, fare clic su di esso e selezionare **caricare**.</span><span class="sxs-lookup"><span data-stu-id="89f34-377">Select JSPHello.war in hello **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="89f34-378">Dovrebbe venire visualizzato in `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="89f34-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="89f34-379">Dopo aver copiato JSPHello.war toohello webapps directory, Server Tomcat verranno automaticamente installati (decomprimere) hello file nel file WAR hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-379">After you copy JSPHello.war toohello webapps directory, Tomcat Server will automatically unpack (unzip) hello files in hello WAR file.</span></span> <span data-ttu-id="89f34-380">Anche se il Server Tomcat inizia disimballaggio quasi immediatamente, potrebbe richiedere troppo tempo (possibilmente ore) per tooappear file hello client hello FTP.</span><span class="sxs-lookup"><span data-stu-id="89f34-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for hello files tooappear in hello FTP client.</span></span>

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a><span data-ttu-id="89f34-381">Eseguire un'applicazione Hello World hello in hello App Web</span><span class="sxs-lookup"><span data-stu-id="89f34-381">Run hello Hello World application on hello Web App</span></span>
1. <span data-ttu-id="89f34-382">Dopo aver caricato i file WAR hello e verificare che il server Tomcat è creato un decompressi `JSPHello` directory Sfoglia troppo`http://webdemowebapp.azurewebsites.net/JSPHello` toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-382">After you have uploaded hello WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse too`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello application.</span></span>
   
   > <span data-ttu-id="89f34-383">**Nota:** se si fa clic **Sfoglia** dal portale classico hello, si potrebbero ottenere pagina Web predefinita hello, indicante che "l'applicazione web Java in base è stata creata."</span><span class="sxs-lookup"><span data-stu-id="89f34-383">**Note:** If you click **Browse** from hello classic portal, you might get hello default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="89f34-384">Pagina Web hello toorefresh potrebbe essere in output dell'applicazione hello tooview ordine anziché la pagina Web predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="89f34-384">You might have toorefresh hello webpage in order tooview hello application output instead of hello default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="89f34-385">Quando viene eseguita l'applicazione hello, vedrai una pagina web con hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="89f34-385">When hello application runs, you should see a web page with hello following output:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="89f34-386">Pulire le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="89f34-386">Clean up Azure resources</span></span>
<span data-ttu-id="89f34-387">Questa procedura crea un'app web del servizio app.</span><span class="sxs-lookup"><span data-stu-id="89f34-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="89f34-388">Verrà fatturato per la risorsa hello, purché esista.</span><span class="sxs-lookup"><span data-stu-id="89f34-388">You will be billed for hello resource as long as it exists.</span></span> <span data-ttu-id="89f34-389">A meno che non si prevede di toocontinue tramite hello web app per il testing o di sviluppo, è necessario considerare l'arresto o l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="89f34-389">Unless you plan toocontinue using hello web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="89f34-390">Anche se un'app Web viene arrestata, è ugualmente prevista una piccola spesa, ma è possibile riavviarla in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="89f34-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="89f34-391">L'eliminazione di un'app web Cancella tutti i dati caricati tooit.</span><span class="sxs-lookup"><span data-stu-id="89f34-391">Deleting a web app erases all data you have uploaded tooit.</span></span>

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
