---
title: Creare un'app Web in Azure App Service con Azure SDK per Java
description: Informazioni su come creare un'app Web in Azure App Service a livello di codice usando Azure SDK per Java.
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
ms.openlocfilehash: 08bb53de8cf437a5a2b1c3b38bce9f81b8349493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a><span data-ttu-id="cc46a-103">Creare un'app Web in Azure App Service con Azure SDK per Java</span><span class="sxs-lookup"><span data-stu-id="cc46a-103">Create a Web App in Azure App Service using the Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a><span data-ttu-id="cc46a-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cc46a-104">Overview</span></span>
<span data-ttu-id="cc46a-105">Questa procedura dettagliata mostra come creare un'applicazione con Azure SDK per Java per la creazione di un'app Web nel [Servizio app di Azure][Azure App Service] e la distribuzione di un'applicazione nel servizio.</span><span class="sxs-lookup"><span data-stu-id="cc46a-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span></span> <span data-ttu-id="cc46a-106">È costituita da due parti:</span><span class="sxs-lookup"><span data-stu-id="cc46a-106">It consists of two parts:</span></span>

* <span data-ttu-id="cc46a-107">La parte 1 illustra come compilare un'applicazione Java per la creazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-107">Part 1 demonstrates how to build a Java application that creates a web app.</span></span>
* <span data-ttu-id="cc46a-108">La parte 2 illustra come creare una semplice applicazione "Hello World" JSP e quindi usare un client FTP per distribuire il codice al servizio app.</span><span class="sxs-lookup"><span data-stu-id="cc46a-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc46a-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cc46a-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="cc46a-110">Installazioni software</span><span class="sxs-lookup"><span data-stu-id="cc46a-110">Software Installations</span></span>
<span data-ttu-id="cc46a-111">Il codice dell'applicazione AzureWebDemo in questo articolo è stato scritto con Azure Java SDK 0.7.0, che è possibile installare usando l'[Installazione guidata piattaforma Web][Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="cc46a-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="cc46a-112">Accertarsi anche di usare l'ultima versione di [Azure Toolkit per Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="cc46a-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="cc46a-113">Dopo avere installato l'SDK, aggiornare le dipendenze nel progetto Eclipse eseguendo **Update Index** (Aggiorna indice) in **Maven Repositories** (Repository Maven), quindi aggiungere nuovamente l'ultima versione di ogni pacchetto nella finestra **Dependencies** (Dependencies).</span><span class="sxs-lookup"><span data-stu-id="cc46a-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span></span> <span data-ttu-id="cc46a-114">È possibile verificare la versione del software installato in Eclipse facendo clic su **Help > Installation Details** (? > Dettagli installazione). Sono necessarie almeno le versioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc46a-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span></span>

* <span data-ttu-id="cc46a-115">Pacchetto per Librerie di Microsoft Azure per Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="cc46a-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="cc46a-116">Eclipse IDE per sviluppatori Java EE 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="cc46a-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="cc46a-117">Creare e configurare risorse cloud in Azure</span><span class="sxs-lookup"><span data-stu-id="cc46a-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="cc46a-118">Prima di iniziare questa procedura, è necessario disporre di una sottoscrizione attiva di Azure e configurare una directory predefinita di Active Directory (AD) in Azure.</span><span class="sxs-lookup"><span data-stu-id="cc46a-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="cc46a-119">Creare una directory di Active Directory (AD) in Azure</span><span class="sxs-lookup"><span data-stu-id="cc46a-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="cc46a-120">Se non si dispone già di una directory di Active Directory (AD) nella sottoscrizione di Azure, accedere al [portale di Azure classico][Azure classic portal] con l'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cc46a-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="cc46a-121">Se si dispone di più sottoscrizioni, fare clic su **Sottoscrizioni** e selezionare la directory predefinita della sottoscrizione da usare per questo progetto.</span><span class="sxs-lookup"><span data-stu-id="cc46a-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span></span> <span data-ttu-id="cc46a-122">Quindi fare clic su **Applica** per passare alla vista di quella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-122">Then click **Apply** to switch to that subscription view.</span></span>

1. <span data-ttu-id="cc46a-123">Selezionare **Active Directory** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="cc46a-123">Select **Active Directory** from the menu at left.</span></span> <span data-ttu-id="cc46a-124">**Fare clic su Nuovo > Directory > Creazione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="cc46a-125">In **Aggiungi directory** selezionare **Crea nuova directory**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="cc46a-126">In **Nome**immettere il nome della directory.</span><span class="sxs-lookup"><span data-stu-id="cc46a-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="cc46a-127">In **Dominio**immettere il nome del dominio.</span><span class="sxs-lookup"><span data-stu-id="cc46a-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="cc46a-128">È un nome di dominio di base che viene incluso nella directory per impostazione predefinita, nel seguente formato: `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="cc46a-129">È possibile assegnargli un nome basato su quello della directory o di un altro dominio di cui si è proprietari.</span><span class="sxs-lookup"><span data-stu-id="cc46a-129">You can name it based on the directory name or another domain name that you own.</span></span> <span data-ttu-id="cc46a-130">In un secondo tempo è possibile aggiungere un altro nome di dominio già usato dall'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="cc46a-131">In **Paese o area geografica**selezionare le impostazioni locali.</span><span class="sxs-lookup"><span data-stu-id="cc46a-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="cc46a-132">Per altre informazioni su AD, vedere [Che cos'è una directory di Azure AD][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="cc46a-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="cc46a-133">Creare un certificato di gestione per Azure</span><span class="sxs-lookup"><span data-stu-id="cc46a-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="cc46a-134">Azure SDK per Java usa i certificati di gestione per l'autenticazione con le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc46a-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span></span> <span data-ttu-id="cc46a-135">Sono certificati X.509 v3 usati per autenticare un'applicazione client che usa l'API di gestione dei servizi per agire per conto del proprietario della sottoscrizione e poter gestire le risorse della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span></span>

<span data-ttu-id="cc46a-136">Il codice in questa procedura usa un certificato autofirmato per l'autenticazione con Azure.</span><span class="sxs-lookup"><span data-stu-id="cc46a-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span></span> <span data-ttu-id="cc46a-137">Per questa procedura, prima è necessario creare un certificato e caricarlo nel [portale di Azure classico][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="cc46a-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="cc46a-138">Questo include i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc46a-138">This involves the following steps:</span></span>

* <span data-ttu-id="cc46a-139">Generare un file PFX che rappresenta il certificato client e salvarlo in locale.</span><span class="sxs-lookup"><span data-stu-id="cc46a-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="cc46a-140">Generare un certificato di gestione (file CER) dal file PFX.</span><span class="sxs-lookup"><span data-stu-id="cc46a-140">Generate a management certificate (CER file) from the PFX file.</span></span>
* <span data-ttu-id="cc46a-141">Caricare il file CER nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc46a-141">Upload the CER file to your Azure subscription.</span></span>
* <span data-ttu-id="cc46a-142">Convertire il file PFX in JKS, perché Java usa questo formato per l'autenticazione con i certificati.</span><span class="sxs-lookup"><span data-stu-id="cc46a-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span></span>
* <span data-ttu-id="cc46a-143">Scrivere il codice di autenticazione dell'applicazione, che fa riferimento al file JKS locale.</span><span class="sxs-lookup"><span data-stu-id="cc46a-143">Write the application's authentication code, which refers to the local JKS file.</span></span>

<span data-ttu-id="cc46a-144">Al termine di questa procedura, il certificato CER si troverà nella sottoscrizione di Azure, mentre il certificato JKS si troverà nell'unità locale.</span><span class="sxs-lookup"><span data-stu-id="cc46a-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="cc46a-145">Per altre informazioni sui certificati di gestione, vedere [Creare e caricare un certificato di gestione per Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="cc46a-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="cc46a-146">Creare un certificato</span><span class="sxs-lookup"><span data-stu-id="cc46a-146">Create a certificate</span></span>
<span data-ttu-id="cc46a-147">Per creare il proprio certificato autofirmato, aprire una console dei comandi nel sistema operativo ed eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="cc46a-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span></span>

> <span data-ttu-id="cc46a-148">**Nota:** nel computer in cui si esegue questo comando deve essere installato JDK.</span><span class="sxs-lookup"><span data-stu-id="cc46a-148">**Note:**  The computer on which you run this command must have the JDK installed.</span></span> <span data-ttu-id="cc46a-149">Inoltre, il percorso dello strumento Keytool dipende dalla posizione in cui si installa JDK.</span><span class="sxs-lookup"><span data-stu-id="cc46a-149">Also, the path to the keytool depends on the location in which you install the JDK.</span></span> <span data-ttu-id="cc46a-150">Per altre informazioni, vedere l'articolo relativo allo [strumento di gestione di chiavi e certificati (Keytool)][Key and Certificate Management Tool (keytool)] nella documentazione online di Java.</span><span class="sxs-lookup"><span data-stu-id="cc46a-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span></span>
> 
> 

<span data-ttu-id="cc46a-151">Per creare il file pfx:</span><span class="sxs-lookup"><span data-stu-id="cc46a-151">To create the .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="cc46a-152">Per creare il file cer:</span><span class="sxs-lookup"><span data-stu-id="cc46a-152">To create the .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="cc46a-153">dove:</span><span class="sxs-lookup"><span data-stu-id="cc46a-153">where:</span></span>

* <span data-ttu-id="cc46a-154">`<java-install-dir>` è il percorso della directory in cui è installato Java.</span><span class="sxs-lookup"><span data-stu-id="cc46a-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span></span>
* <span data-ttu-id="cc46a-155">`<keystore-id>` è l'identificatore della voce dell'archivio chiavi (ad esempio, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="cc46a-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="cc46a-156">`<cert-store-dir>` è il percorso della directory in cui archiviare i certificati (ad esempio, `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="cc46a-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="cc46a-157">`<cert-file-name>` è il nome del file del certificato (ad esempio `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="cc46a-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="cc46a-158">`<password>` è la password che si sceglie per proteggere il certificato. Deve essere di almeno 6 caratteri.</span><span class="sxs-lookup"><span data-stu-id="cc46a-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="cc46a-159">È possibile non immettere alcuna password, anche se non è consigliato.</span><span class="sxs-lookup"><span data-stu-id="cc46a-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="cc46a-160">`<dname>` è il nome distinto X.500 da associare all'alias e viene usato come campo dell'autorità di certificazione e dell'oggetto nel certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="cc46a-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span></span>

<span data-ttu-id="cc46a-161">Per altre informazioni, vedere [Creare e caricare un certificato di gestione per Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="cc46a-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-the-certificate"></a><span data-ttu-id="cc46a-162">Caricare il certificato</span><span class="sxs-lookup"><span data-stu-id="cc46a-162">Upload the certificate</span></span>
<span data-ttu-id="cc46a-163">Per caricare un certificato autofirmato in Azure, visitare la pagina **Impostazioni** del portale classico, quindi fare clic sulla scheda **Certificati di gestione**. Fare clic su **Carica** nella pagina in basso e passare alla posizione del file CER creato.</span><span class="sxs-lookup"><span data-stu-id="cc46a-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span></span>

#### <a name="convert-the-pfx-file-into-jks"></a><span data-ttu-id="cc46a-164">Convertire il file PFX in JKS</span><span class="sxs-lookup"><span data-stu-id="cc46a-164">Convert the PFX file into JKS</span></span>
<span data-ttu-id="cc46a-165">Nel prompt dei comandi di Windows (in esecuzione come amministratore) passare alla directory contenente i certificati ed eseguire il comando seguente, dove `<java-install-dir>` è la directory del computer in cui si è installato Java:</span><span class="sxs-lookup"><span data-stu-id="cc46a-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="cc46a-166">Quando richiesto, immettere la password keystore di destinazione. Sarà la password per il file JKS.</span><span class="sxs-lookup"><span data-stu-id="cc46a-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span></span>
2. <span data-ttu-id="cc46a-167">Quando richiesto, immettere la password keystore di origine. È la password specificata per il file PFX.</span><span class="sxs-lookup"><span data-stu-id="cc46a-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span></span>

<span data-ttu-id="cc46a-168">Le due password non devono essere uguali.</span><span class="sxs-lookup"><span data-stu-id="cc46a-168">The two passwords do not have to be the same.</span></span> <span data-ttu-id="cc46a-169">È possibile non immettere alcuna password, anche se non è consigliato.</span><span class="sxs-lookup"><span data-stu-id="cc46a-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="cc46a-170">Compilare un'applicazione per la creazione di app Web</span><span class="sxs-lookup"><span data-stu-id="cc46a-170">Build a Web App creation application</span></span>
### <a name="create-the-eclipse-workspace-and-maven-project"></a><span data-ttu-id="cc46a-171">Creare l'area di lavoro di Eclipse e il progetto Maven</span><span class="sxs-lookup"><span data-stu-id="cc46a-171">Create the Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="cc46a-172">In questa sezione si creano un'area di lavoro e un progetto Maven per l'applicazione per la creazione di app Web, denominata AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="cc46a-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="cc46a-173">Creare un nuovo progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="cc46a-173">Create a new Maven project.</span></span> <span data-ttu-id="cc46a-174">Fare clic su **File > New > Maven Project** (File > Nuovo > Progetto Maven).</span><span class="sxs-lookup"><span data-stu-id="cc46a-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="cc46a-175">In **New Maven Project** (Nuovo progetto Maven) selezionare **Create a simple project** (Crea progetto semplice) e **Use default workspace location** (Usa percorso area di lavoro predefinito).</span><span class="sxs-lookup"><span data-stu-id="cc46a-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="cc46a-176">Nella seconda pagina di **New Maven Project**specificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="cc46a-176">On the second page of **New Maven Project**, specify the following:</span></span>
   
   * <span data-ttu-id="cc46a-177">Group ID: `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="cc46a-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="cc46a-178">Artifact ID: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="cc46a-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="cc46a-179">Version: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="cc46a-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="cc46a-180">Packaging: jar</span><span class="sxs-lookup"><span data-stu-id="cc46a-180">Packaging: jar</span></span>
   * <span data-ttu-id="cc46a-181">Name: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="cc46a-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="cc46a-182">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-182">Click **Finish**.</span></span>
3. <span data-ttu-id="cc46a-183">Aprire il file pom.xml del nuovo progetto in Project Explorer.</span><span class="sxs-lookup"><span data-stu-id="cc46a-183">Open the new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="cc46a-184">Selezionare la scheda **Dependencies** . Essendo un nuovo progetto, non è ancora elencato nessun pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cc46a-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="cc46a-185">Aprire la visualizzazione Maven Repositories.</span><span class="sxs-lookup"><span data-stu-id="cc46a-185">Open the Maven Repositories view.</span></span> <span data-ttu-id="cc46a-186">Fare clic su **Window > Show View > Other > Maven > Maven Repositories** (Finestra > Mostra vista > Altro > Maven > Repository Maven) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="cc46a-187">La visualizzazione **Maven Repositories** apparirà in basso nell'IDE.</span><span class="sxs-lookup"><span data-stu-id="cc46a-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span></span>
5. <span data-ttu-id="cc46a-188">Aprire **Global Repositories** (Repository globali), fare clic con il pulsante destro del mouse sull'archivio **centralizzato** e scegliere **Rebuild Index** (Ricompila indice).</span><span class="sxs-lookup"><span data-stu-id="cc46a-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="cc46a-189">Questo passaggio può richiedere alcuni minuti a seconda della velocità della connessione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-189">This step can take several minutes depending on the speed of your connection.</span></span> <span data-ttu-id="cc46a-190">Quando l'indice viene ricompilato, si dovrebbero vedere i pacchetti di Microsoft Azure nell'archivio Maven **central** .</span><span class="sxs-lookup"><span data-stu-id="cc46a-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span></span>
6. <span data-ttu-id="cc46a-191">In **Dependencies** (Dipendenze) fare clic su **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="cc46a-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="cc46a-192">In **Enter Group ID...** (Immettere ID gruppo...) immettere `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="cc46a-193">Selezionare i pacchetti per la gestione di base e la gestione di app Web del servizio app:</span><span class="sxs-lookup"><span data-stu-id="cc46a-193">Select the packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="cc46a-194">**Nota:** se si stanno aggiornando le dipendenze in seguito al rilascio di una nuova versione, è necessario riaggiungere ogni dipendenza di questo elenco.</span><span class="sxs-lookup"><span data-stu-id="cc46a-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span></span>
   > <span data-ttu-id="cc46a-195">Dopo avere fatto clic su **Add** (Aggiungi) e selezionato ogni dipendenza, le dipendenze appaiono con il nuovo numero di versione nell'elenco **Dependencies** (Dipendenze).</span><span class="sxs-lookup"><span data-stu-id="cc46a-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="cc46a-196">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-196">Click **OK**.</span></span> <span data-ttu-id="cc46a-197">I pacchetti di Azure appaiono quindi nell'elenco **Dependencies** .</span><span class="sxs-lookup"><span data-stu-id="cc46a-197">The Azure packages then appear in the **Dependencies** list.</span></span>

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a><span data-ttu-id="cc46a-198">Scrittura di codice Java per creare un'app Web chiamando Azure SDK</span><span class="sxs-lookup"><span data-stu-id="cc46a-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span></span>
<span data-ttu-id="cc46a-199">Scrivere ora il codice che chiama le API in Azure SDK in modo che Java crei l'app Web del servizio app.</span><span class="sxs-lookup"><span data-stu-id="cc46a-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span></span>

1. <span data-ttu-id="cc46a-200">Creare una classe Java in cui includere il codice del punto di ingresso principale.</span><span class="sxs-lookup"><span data-stu-id="cc46a-200">Create a Java class to contain the main entry point code.</span></span> <span data-ttu-id="cc46a-201">In Project Explorer fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **New > Class** (Nuovo > Classe).</span><span class="sxs-lookup"><span data-stu-id="cc46a-201">In Project Explorer, right-click on the project node and select **New > Class**.</span></span>
2. <span data-ttu-id="cc46a-202">In **New Java Class`WebCreator` (Nuova classe Java) assegnare alla classe il nome** e selezionare la casella di controllo **public static void main**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span></span> <span data-ttu-id="cc46a-203">Le selezioni dovrebbero essere come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc46a-203">The selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="cc46a-204">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-204">Click **Finish**.</span></span> <span data-ttu-id="cc46a-205">Il file WebCreator.java appare in Project Explorer.</span><span class="sxs-lookup"><span data-stu-id="cc46a-205">The WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a><span data-ttu-id="cc46a-206">Chiamata all'API di Azure per creare un app Web del servizio app</span><span class="sxs-lookup"><span data-stu-id="cc46a-206">Calling the Azure API to Create an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="cc46a-207">Aggiungere le importazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="cc46a-207">Add necessary imports</span></span>
<span data-ttu-id="cc46a-208">In WebCreator.java aggiungere le importazioni seguenti. Queste importazioni forniscono l'accesso alle classi nelle librerie di gestione per usare le API di Azure:</span><span class="sxs-lookup"><span data-stu-id="cc46a-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-the-main-entry-point-class"></a><span data-ttu-id="cc46a-209">Definire la classe del punto di ingresso principale</span><span class="sxs-lookup"><span data-stu-id="cc46a-209">Define the main entry point class</span></span>
<span data-ttu-id="cc46a-210">Poiché lo scopo dell'applicazione AzureWebDemo è la creazione di un'app Web del servizio app, assegnare alla classe principale di questa applicazione il nome `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="cc46a-211">Questa classe fornisce il codice del punto di ingresso principale che chiama l'API di gestione del servizio Azure per creare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span></span>

<span data-ttu-id="cc46a-212">Aggiungere le seguenti definizioni dei parametri per l'app Web e lo spazio Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-212">Add the following parameter definitions for the web app and webspace.</span></span> <span data-ttu-id="cc46a-213">Sarà necessario fornire l'ID sottoscrizione di Azure e le informazioni certificato.</span><span class="sxs-lookup"><span data-stu-id="cc46a-213">You will need to provide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="cc46a-214">dove:</span><span class="sxs-lookup"><span data-stu-id="cc46a-214">where:</span></span>

* <span data-ttu-id="cc46a-215">`<subscription-id>` è l'ID sottoscrizione di Azure in cui creare la risorsa.</span><span class="sxs-lookup"><span data-stu-id="cc46a-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span></span>
* <span data-ttu-id="cc46a-216">`<certificate-store-path>` è il percorso e il nome del file JKS nella directory dell'archivio certificati locale.</span><span class="sxs-lookup"><span data-stu-id="cc46a-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span></span> <span data-ttu-id="cc46a-217">Ad esempio, `C:/Certificates/CertificateName.jks` per Linux e `C:\Certificates\CertificateName.jks` per Windows.</span><span class="sxs-lookup"><span data-stu-id="cc46a-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="cc46a-218">`<certificate-password>` è la password specificata quando si è creato il certificato JKS.</span><span class="sxs-lookup"><span data-stu-id="cc46a-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="cc46a-219">`webAppName` può essere un nome qualsiasi. In questa procedura si usa il nome `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span></span> <span data-ttu-id="cc46a-220">Il nome di dominio completo è `webAppName` a cui viene aggiunto `domainName`, quindi in questo caso il dominio completo è `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="cc46a-221">`domainName` deve essere specificato come indicato sopra.</span><span class="sxs-lookup"><span data-stu-id="cc46a-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="cc46a-222">`webSpaceName` deve essere uno dei valori definiti nella classe [WebSpaceNames][WebSpaceNames].</span><span class="sxs-lookup"><span data-stu-id="cc46a-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="cc46a-223">`appServicePlanName` deve essere specificato come indicato sopra.</span><span class="sxs-lookup"><span data-stu-id="cc46a-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="cc46a-224">**Nota:`appServicePlanName` ogni volta che si esegue questa applicazione, è necessario cambiare il valore di** e `webAppName` (o eliminare l'app Web nel portale di Azure) prima di eseguire di nuovo l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span></span> <span data-ttu-id="cc46a-225">In caso contrario, l'esecuzione non riuscirà perché la stessa risorsa esiste già in Azure.</span><span class="sxs-lookup"><span data-stu-id="cc46a-225">Otherwise, execution will fail because the same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-the-web-creation-method"></a><span data-ttu-id="cc46a-226">Definire il metodo di creazione web</span><span class="sxs-lookup"><span data-stu-id="cc46a-226">Define the web creation method</span></span>
<span data-ttu-id="cc46a-227">Definire ora un metodo per creare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-227">Next, define a method to create the web app.</span></span> <span data-ttu-id="cc46a-228">Questo metodo, `createWebApp`, specifica i parametri dell'app Web e dello spazio Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span></span> <span data-ttu-id="cc46a-229">Il metodo crea e configura anche il client di gestione delle app Web del servizio app, definito dall'oggetto [WebSiteManagementClient][WebSiteManagementClient].</span><span class="sxs-lookup"><span data-stu-id="cc46a-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="cc46a-230">Il client di gestione è fondamentale per la creazione di app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-230">The management client is key to creating Web Apps.</span></span> <span data-ttu-id="cc46a-231">Fornisce i servizi Web RESTful che consentono alle applicazioni di gestire le app Web (eseguendo operazioni come la creazione, l'aggiornamento e l'eliminazione) chiamando l'API di gestione dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cc46a-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
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
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="cc46a-232">Il codice restituirà lo stato HTTP della risposta indicante l'esito positivo o negativo e, se positivo, restituirà il nome dell'app Web creata.</span><span class="sxs-lookup"><span data-stu-id="cc46a-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span></span>

#### <a name="define-the-main-method"></a><span data-ttu-id="cc46a-233">Definire il metodo main()</span><span class="sxs-lookup"><span data-stu-id="cc46a-233">Define the main() method</span></span>
<span data-ttu-id="cc46a-234">Fornire il codice del metodo main() che chiama createWebApp() per creare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-234">Provide the main() method code that calls createWebApp() to create the web app.</span></span>

<span data-ttu-id="cc46a-235">Infine chiamare `createWebApp` da `main`:</span><span class="sxs-lookup"><span data-stu-id="cc46a-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a><span data-ttu-id="cc46a-236">Eseguire l'applicazione e verificare la creazione dell'app Web</span><span class="sxs-lookup"><span data-stu-id="cc46a-236">Run the application and verify web app creation</span></span>
<span data-ttu-id="cc46a-237">Per verificare che l'applicazione venga eseguita, fare clic su **Run > Run** (Esegui > Esegui).</span><span class="sxs-lookup"><span data-stu-id="cc46a-237">To verify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="cc46a-238">Quando l'esecuzione dell'applicazione termina, si dovrebbe vedere il seguente output nella console di Eclipse:</span><span class="sxs-lookup"><span data-stu-id="cc46a-238">When the application completes running, you should see the following output in the Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="cc46a-239">Accedere al portale di Azure classico e fare clic su **App Web**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-239">Log into the Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="cc46a-240">La nuova app Web dovrebbe apparire nell'elenco App Web in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="cc46a-240">The new web app should appear in the Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-to-the-web-app"></a><span data-ttu-id="cc46a-241">Distribuzione di un'applicazione nell'app Web</span><span class="sxs-lookup"><span data-stu-id="cc46a-241">Deploying an Application to the Web App</span></span>
<span data-ttu-id="cc46a-242">Dopo avere eseguito AzureWebDemo e creato la nuova app Web, accedere al portale classico, fare clic su **App Web**e scegliere **WebDemoWebApp** in the **App Web** .</span><span class="sxs-lookup"><span data-stu-id="cc46a-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span></span> <span data-ttu-id="cc46a-243">Nella pagina del dashboard dell'app Web fare clic su **Sfoglia** (o fare clic sull'URL, `webdemowebapp.azurewebsites.net`) per aprirla.</span><span class="sxs-lookup"><span data-stu-id="cc46a-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span></span> <span data-ttu-id="cc46a-244">Si vedrà una pagina segnaposto vuota, perché nell'app Web non è ancora stato pubblicato nulla.</span><span class="sxs-lookup"><span data-stu-id="cc46a-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span></span>

<span data-ttu-id="cc46a-245">Ora si creerà un'applicazione "Hello World" e la si distribuirà nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-245">Next you will create a "Hello World" application and deploy it to the web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="cc46a-246">Creare un'applicazione Hello World JSP</span><span class="sxs-lookup"><span data-stu-id="cc46a-246">Create a JSP Hello World application</span></span>
#### <a name="create-the-application"></a><span data-ttu-id="cc46a-247">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="cc46a-247">Create the application</span></span>
<span data-ttu-id="cc46a-248">Per illustrare la distribuzione di un'applicazione sul Web, la seguente procedura mostra come creare una semplice applicazione Java "Hello World" e come caricarla nell'app Web del servizio app creata dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span></span>

1. <span data-ttu-id="cc46a-249">Fare clic su **File > New > Dynamic Web Project** (File > Nuovo > Progetto Web dinamico).</span><span class="sxs-lookup"><span data-stu-id="cc46a-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="cc46a-250">Denominarlo `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-250">Name it `JSPHello`.</span></span> <span data-ttu-id="cc46a-251">Non è necessario cambiare nessuna altra impostazione di questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cc46a-251">You do not need to change any other settings in this dialog.</span></span> <span data-ttu-id="cc46a-252">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="cc46a-253">In Project Explorer espandere il progetto **JSPHello**, fare clic con il pulsante destro del mouse su **WebContent**, quindi fare clic su **New > JSP File** (Nuovo > File JSP).</span><span class="sxs-lookup"><span data-stu-id="cc46a-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="cc46a-254">Nella finestra di dialogo New JSP File denominare il nuovo file `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-254">In the New JSP File dialog, name the new file `index.jsp`.</span></span> <span data-ttu-id="cc46a-255">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-255">Click **Next**.</span></span>
3. <span data-ttu-id="cc46a-256">Nella finestra di dialogo **Select JSP Template** (Seleziona modello JSP) selezionare **New JSP File (html)** (Nuovo file JSP (html)) e fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="cc46a-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="cc46a-257">In index.jsp aggiungere il seguente codice nelle sezioni dei tag `<head>` e `<body>`:</span><span class="sxs-lookup"><span data-stu-id="cc46a-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a><span data-ttu-id="cc46a-258">Eseguire l'applicazione Hello World in localhost</span><span class="sxs-lookup"><span data-stu-id="cc46a-258">Run the Hello World application in localhost</span></span>
<span data-ttu-id="cc46a-259">Prima di eseguire questa applicazione, è necessario configurare alcune proprietà.</span><span class="sxs-lookup"><span data-stu-id="cc46a-259">Before you run this application, you need to configure a few properties.</span></span>

1. <span data-ttu-id="cc46a-260">Fare clic con il pulsante destro del mouse sul progetto **JSPHello**, quindi scegliere **Properties** (Proprietà).</span><span class="sxs-lookup"><span data-stu-id="cc46a-260">Right-click the **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="cc46a-261">Nella finestra di dialogo **Properties** (Proprietà) selezionare **Java Build Path** (Percorso build Java), selezionare la scheda **Order and Export** (Ordina ed esporta), scegliere **JRE System Library** (Libreria di sistema JRE), quindi fare clic su **Up** (Su) per spostarla all'inizio dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="cc46a-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span></span>
   
    ![][4]
3. <span data-ttu-id="cc46a-262">Sempre nella finestra di dialogo **Properties** (Proprietà) selezionare **Targeted Runtimes** (Runtime mirati) e fare clic su **New** (Nuovo).</span><span class="sxs-lookup"><span data-stu-id="cc46a-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="cc46a-263">Nella finestra di dialogo **New Server Runtime Environment** (Nuovo ambiente di runtime server) selezionare un server, ad esempio **Apache Tomcat v7.0**, e fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="cc46a-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="cc46a-264">Nella finestra di dialogo **Tomcat Server** (Server Tomcat) impostare **Name** (Nome) su **e impostare `Apache Tomcat v7.0`Tomcat Installation Directory** (Directory di installazione Tomcat) sulla directory in cui è stata installata la versione del server Tomcat da usare.</span><span class="sxs-lookup"><span data-stu-id="cc46a-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span></span>
   
    ![][5]
   
    <span data-ttu-id="cc46a-265">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-265">Click **Finish**.</span></span>
5. <span data-ttu-id="cc46a-266">Si torna quindi alla pagina **Targeted Runtimes** (Runtime mirati) della finestra di dialogo **Properties** (Proprietà).</span><span class="sxs-lookup"><span data-stu-id="cc46a-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span></span> <span data-ttu-id="cc46a-267">Selezionare **Apache Tomcat v7.0**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="cc46a-268">Nel menu **Run** (Esegui) di Eclipse fare clic su **Run** (Esegui).</span><span class="sxs-lookup"><span data-stu-id="cc46a-268">In the Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="cc46a-269">Nella finestra di dialogo **Run As** (Esegui come) selezionare **Run on Server** (Esegui su server).</span><span class="sxs-lookup"><span data-stu-id="cc46a-269">In the **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="cc46a-270">Nella finestra di dialogo **Run on Server** (Esegui su server) selezionare **Tomcat v7.0 Server** (Server Tomcat v7.0):</span><span class="sxs-lookup"><span data-stu-id="cc46a-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="cc46a-271">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-271">Click **Finish**.</span></span>
7. <span data-ttu-id="cc46a-272">Quando l'applicazione viene eseguita, la pagina **JSPHello** dovrebbe apparire in una finestra localhost di Eclipse (`http://localhost:8080/JSPHello/`), con il messaggio seguente:</span><span class="sxs-lookup"><span data-stu-id="cc46a-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a><span data-ttu-id="cc46a-273">Esportare l'applicazione come file WAR</span><span class="sxs-lookup"><span data-stu-id="cc46a-273">Export the application as a WAR</span></span>
<span data-ttu-id="cc46a-274">Esportare i file di progetto Web come file di archivio Web (WAR) per poterli distribuire nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span></span> <span data-ttu-id="cc46a-275">I seguenti file di progetto Web si trovano nella cartella WebContent:</span><span class="sxs-lookup"><span data-stu-id="cc46a-275">The following web project files reside in the WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="cc46a-276">Fare clic con il pulsante destro del mouse sulla cartella WebContent e scegliere **Export**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-276">Right-click the WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="cc46a-277">Nella finestra di dialogo **Export Select** (Esporta selezione) fare clic sul file **Web > WAR**, quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="cc46a-278">Nella finestra di dialogo **WAR Export** selezionare la directory src nel progetto corrente e includere il nome del file WAR alla fine.</span><span class="sxs-lookup"><span data-stu-id="cc46a-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span></span> <span data-ttu-id="cc46a-279">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cc46a-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="cc46a-280">Per altre informazioni sulla distribuzione di file WAR, vedere [Aggiungere un'applicazione Java alle app Web del servizio app di Azure](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="cc46a-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-the-hello-world-application-using-ftp"></a><span data-ttu-id="cc46a-281">Distribuzione dell'applicazione Hello World tramite FTP</span><span class="sxs-lookup"><span data-stu-id="cc46a-281">Deploying the Hello World Application Using FTP</span></span>
<span data-ttu-id="cc46a-282">Selezionare un client FTP di terze parti per pubblicare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-282">Select a third-party FTP client to publish the application.</span></span> <span data-ttu-id="cc46a-283">Questa procedura descrive due opzioni: la console Kudu, integrata in Azure, e FileZilla, uno strumento di ampia diffusione con un'interfaccia utente grafica e intuitiva.</span><span class="sxs-lookup"><span data-stu-id="cc46a-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="cc46a-284">**Nota:** il Toolkit Azure per Eclipse supporta la distribuzione in account di archiviazione e servizi cloud, ma attualmente non supporta la distribuzione nelle app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span></span> <span data-ttu-id="cc46a-285">Per la distribuzione negli account di archiviazione e nei servizi cloud, è possibile usare un progetto di distribuzione di Azure, come spiegato in [Creazione di un'applicazione Hello World per Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), ma non per la distribuzione nelle app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span></span> <span data-ttu-id="cc46a-286">Per trasferire i file nelle app Web, usare altri metodi come FTP o GitHub.</span><span class="sxs-lookup"><span data-stu-id="cc46a-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span></span>
> 
> <span data-ttu-id="cc46a-287">**Nota:** non è consigliabile usare FTP dal prompt dei comandi di Windows (l'utilità FTP.EXE della riga di comando fornita con Windows).</span><span class="sxs-lookup"><span data-stu-id="cc46a-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="cc46a-288">I client FTP che usano un FTP attivo, ad esempio FTP.EXE, spesso non riescono a superare i firewall.</span><span class="sxs-lookup"><span data-stu-id="cc46a-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span></span> <span data-ttu-id="cc46a-289">FTP attivo specifica un indirizzo interno basato su LAN, a cui è probabile che un server FTP non riesca a connettersi.</span><span class="sxs-lookup"><span data-stu-id="cc46a-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span></span>
> 
> 

<span data-ttu-id="cc46a-290">Per altre informazioni sulla distribuzione in un'app Web del servizio app tramite FTP, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc46a-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span></span>

* [<span data-ttu-id="cc46a-291">Distribuire mediante un'utilità FTP</span><span class="sxs-lookup"><span data-stu-id="cc46a-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="cc46a-292">Imposta credenziali di distribuzione</span><span class="sxs-lookup"><span data-stu-id="cc46a-292">Set up deployment credentials</span></span>
<span data-ttu-id="cc46a-293">Assicurarsi di aver eseguito l'applicazione **AzureWebDemo** per creare un'app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span></span> <span data-ttu-id="cc46a-294">I file verranno trasferiti in questa posizione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-294">You will transfer files to this location.</span></span>

1. <span data-ttu-id="cc46a-295">Accedere al portale classico e fare clic su **App Web**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-295">Log into the classic portal and click **Web Apps**.</span></span> <span data-ttu-id="cc46a-296">Assicurarsi che **WebDemoWebApp** sia presente nell'elenco di app Web e che sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="cc46a-297">Fare clic su **WebDemoWebApp** per aprire la pagina **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span></span>
2. <span data-ttu-id="cc46a-298">Nella pagina **Dashboard**, in **Riepilogo rapido** fare clic su **Set up your deployment credentials** (Imposta credenziali di distribuzione). Se si dispone già di credenziali di distribuzione, questa opzione sarà sostituita da **Reimposta le credenziali di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="cc46a-299">Le credenziali di distribuzione sono associate a un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cc46a-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="cc46a-300">È necessario specificare un nome utente e una password da usare per la distribuzione tramite Git ed FTP.</span><span class="sxs-lookup"><span data-stu-id="cc46a-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span></span> <span data-ttu-id="cc46a-301">È possibile usare queste credenziali per la distribuzione in qualsiasi app Web in tutte le sottoscrizioni di Azure associate all'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cc46a-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="cc46a-302">Specificare le credenziali di distribuzione tramite Git ed FTP nella finestra di dialogo e prendere nota del nome utente e della password per un uso futuro.</span><span class="sxs-lookup"><span data-stu-id="cc46a-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="cc46a-303">Ottenere informazioni di connessione a FTP</span><span class="sxs-lookup"><span data-stu-id="cc46a-303">Get FTP connection information</span></span>
<span data-ttu-id="cc46a-304">Per usare FTP per distribuire i file dell'applicazione nell'app Web appena creata, è necessario ottenere le informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span></span> <span data-ttu-id="cc46a-305">Per ottenere le informazioni di connessione, è possibile procedere in due modi.</span><span class="sxs-lookup"><span data-stu-id="cc46a-305">There are two ways to obtain connection information.</span></span> <span data-ttu-id="cc46a-306">Il primo consiste nel visitare la pagina **Dashboard** dell'app Web, il secondo nello scaricare il profilo di pubblicazione dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span></span> <span data-ttu-id="cc46a-307">Il profilo di pubblicazione è un file XML che fornisce informazioni, ad esempio il nome host FTP e le credenziali di accesso per le app Web in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="cc46a-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="cc46a-308">È possibile usare il nome utente e la password per la distribuzione in qualsiasi app Web in tutte le sottoscrizioni associate all'account di Azure, non solo in questa.</span><span class="sxs-lookup"><span data-stu-id="cc46a-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span></span>

<span data-ttu-id="cc46a-309">Per ottenere le informazioni di connessione a FTP dal pannello dell'app Web nel [portale di Azure][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="cc46a-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="cc46a-310">In **Essentials** trovare e copiare il **Nome host FTP**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-310">Under **Essentials**, find and copy the **FTP hostname**.</span></span> <span data-ttu-id="cc46a-311">È un URI simile a `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="cc46a-312">In **Essentials** trovare e copiare il **Nome utente FTP/distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="cc46a-313">Il formato sarà *nomeappweb\nomeutente-distribuzione*, ad esempio `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="cc46a-314">Per ottenere le informazioni di connessione a FTP dal profilo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="cc46a-314">To obtain FTP connection information from the publish profile:</span></span>

1. <span data-ttu-id="cc46a-315">Nel pannello dell'app Web fare clic su **Recupera profilo**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-315">In the web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="cc46a-316">Verrà scaricato un file publishsettings nell'unità locale.</span><span class="sxs-lookup"><span data-stu-id="cc46a-316">This will download a .publishsettings file to your local drive.</span></span>
2. <span data-ttu-id="cc46a-317">Aprire il file publishsettings in un editor XML o nell'editor di testo e trovare l'elemento `<publishProfile>` contenente `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="cc46a-318">Il codice sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cc46a-318">It should look like the following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="cc46a-319">Si noti che le impostazioni `publishProfile` dell'app Web corrispondono alle impostazioni di FileZilla Site Manager indicate di seguito:</span><span class="sxs-lookup"><span data-stu-id="cc46a-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="cc46a-320">`publishUrl` equivale a **Nome host FTP**, il valore impostato in **Host**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span></span>
* <span data-ttu-id="cc46a-321">`publishMethod="FTP"` indica che **Protocollo** è stato impostato su **FTP - File Transfer Protocol** e **Criptazione** su **Usa solo FTP non sicuro**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span></span>
* <span data-ttu-id="cc46a-322">`userName` e `userPWD` sono le chiavi dei valori effettivi di nome utente e password specificati quando sono state reimpostate le credenziali di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span></span> <span data-ttu-id="cc46a-323">`userName` equivale a **Utente FTP/distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-323">`userName` is the same as **Deployment / FTP user**.</span></span> <span data-ttu-id="cc46a-324">Corrispondono a **Nome utente** e **Password** in FileZilla.</span><span class="sxs-lookup"><span data-stu-id="cc46a-324">They map to **User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="cc46a-325">`ftpPassiveMode="True"` indica che il sito FTP usa il trasferimento FTP passivo. Selezionare **Passiva** nella scheda **Impostazioni trasferimento**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span></span>

#### <a name="configure-the-web-app-to-host-a-java-application"></a><span data-ttu-id="cc46a-326">Configurare l'app Web per ospitare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="cc46a-326">Configure the Web App to host a Java application</span></span>
<span data-ttu-id="cc46a-327">Prima di pubblicare l'applicazione, è necessario cambiare alcune impostazioni di configurazione in modo che l'app Web possa ospitare un'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="cc46a-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span></span>

1. <span data-ttu-id="cc46a-328">Nel portale classico accedere alla pagina **Dashboard** dell'app Web e fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="cc46a-329">Nella pagina **Configura** specificare le impostazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="cc46a-329">On the **Configure** page, specify the following settings.</span></span>
2. <span data-ttu-id="cc46a-330">In **Versione Java** l'impostazione predefinita è **Off**. Selezionare la versione di Java per l'applicazione, ad esempio 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="cc46a-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="cc46a-331">Dopodiché, verificare anche che **Contenitore Web** sia impostato su una versione di Tomcat Server.</span><span class="sxs-lookup"><span data-stu-id="cc46a-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span></span>
3. <span data-ttu-id="cc46a-332">In **Documenti predefiniti**aggiungere index.jsp e spostarlo all'inizio dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="cc46a-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span></span> <span data-ttu-id="cc46a-333">Il file predefinito per le app Web è hostingstart.html.</span><span class="sxs-lookup"><span data-stu-id="cc46a-333">(The default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="cc46a-334">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="cc46a-335">Pubblicare l'applicazione con Kudu</span><span class="sxs-lookup"><span data-stu-id="cc46a-335">Publish your application using Kudu</span></span>
<span data-ttu-id="cc46a-336">Un modo per pubblicare l'applicazione consiste nell'usare la console di debug Kudu integrata in Azure.</span><span class="sxs-lookup"><span data-stu-id="cc46a-336">One way to publish the application is to use the Kudu debug console built into Azure.</span></span> <span data-ttu-id="cc46a-337">Kudu è stabile e coerente con le app Web del servizio app e Server Tomcat.</span><span class="sxs-lookup"><span data-stu-id="cc46a-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="cc46a-338">Per accedere alla console per l'app Web, passare a un URL nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="cc46a-338">You access the console for the web app by browsing to a URL of the following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="cc46a-339">Per questa procedura, la console Kudu si trova all'URL seguente. Passare a questa posizione:</span><span class="sxs-lookup"><span data-stu-id="cc46a-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="cc46a-340">Nel menu in alto selezionare **Debug Console > CMD** (Console di debug > CMD).</span><span class="sxs-lookup"><span data-stu-id="cc46a-340">From the top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="cc46a-341">Nella riga di comando della console andare a `/site/wwwroot` (o fare clic su `site`, quindi su `wwwroot` nella visualizzazione directory in alto nella pagina):</span><span class="sxs-lookup"><span data-stu-id="cc46a-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="cc46a-342">Dopo aver specificato **Java version**, il server Tomcat dovrebbe creare una directory webapps.</span><span class="sxs-lookup"><span data-stu-id="cc46a-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="cc46a-343">Nella riga di comando della console andare alla directory webapps:</span><span class="sxs-lookup"><span data-stu-id="cc46a-343">In the console command line, navigate to the webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="cc46a-344">Trascinare Drag JSPHello.war da `<project-path>/JSPHello/src/` e rilasciarlo nella visualizzazione directory di Kudu in `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="cc46a-345">Non trascinarlo nell'area "Drag here to upload and zip", perché Tomcat lo decomprimerà.</span><span class="sxs-lookup"><span data-stu-id="cc46a-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="cc46a-346">All'inizio JSPHello.war appare da solo nell'area delle directory:</span><span class="sxs-lookup"><span data-stu-id="cc46a-346">At first JSPHello.war appears in the directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="cc46a-347">In poco tempo (probabilmente meno di 5 minuti) Tomcat Server decomprimerà il file WAR in una directory JSPHello decompressa.</span><span class="sxs-lookup"><span data-stu-id="cc46a-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="cc46a-348">Fare clic sulla directory ROOT per verificare se index.jsp è stato decompresso e copiato qui.</span><span class="sxs-lookup"><span data-stu-id="cc46a-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="cc46a-349">In tal caso, tornare alla directory webapps per verificare se è stata creata la directory JSPHello decompressa.</span><span class="sxs-lookup"><span data-stu-id="cc46a-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="cc46a-350">Se questi elementi non sono visibili, attendere e riprovare.</span><span class="sxs-lookup"><span data-stu-id="cc46a-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="cc46a-351">Pubblicare l'applicazione con FileZilla (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="cc46a-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="cc46a-352">Un altro strumento che è possibile usare per pubblicare l'applicazione è FileZilla, un diffuso client FTP di terze parti con un' interfaccia utente grafica e intuitiva.</span><span class="sxs-lookup"><span data-stu-id="cc46a-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="cc46a-353">È possibile scaricare e installare FileZilla da [http://filezilla-project.org/](http://filezilla-project.org/) se non lo si ha già.</span><span class="sxs-lookup"><span data-stu-id="cc46a-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="cc46a-354">Per altre informazioni sull'uso del client, vedere la [documentazione di FileZilla](https://wiki.filezilla-project.org/Documentation) e questo post del blog in [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx) (Client FTP - Parte 4: FileZilla).</span><span class="sxs-lookup"><span data-stu-id="cc46a-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="cc46a-355">In FileZilla fare clic su **File > Gestore siti**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="cc46a-356">Nella finestra di dialogo **Gestore siti** fare clic su **Nuovo sito**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-356">In the **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="cc46a-357">In **Select Entry** apparirà un nuovo sito FTP vuoto a cui assegnare un nome.</span><span class="sxs-lookup"><span data-stu-id="cc46a-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span></span> <span data-ttu-id="cc46a-358">Per questa procedura, denominarlo `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="cc46a-359">Nella pagina **Generale** specificare le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc46a-359">On the **General** tab, specify the following settings:</span></span>
   
   * <span data-ttu-id="cc46a-360">**Host:** immettere il **nome dell'host FTP** copiato dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc46a-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span></span>
   * <span data-ttu-id="cc46a-361">**Porta:** lasciarla non configurata, poiché si tratta di un trasferimento passivo per il quale il server determinerà la porta da usare.</span><span class="sxs-lookup"><span data-stu-id="cc46a-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span></span>
   * <span data-ttu-id="cc46a-362">**Protocollo:** protocollo per il trasferimento del file FTP</span><span class="sxs-lookup"><span data-stu-id="cc46a-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="cc46a-363">**Crittografia:** usare FTP semplice</span><span class="sxs-lookup"><span data-stu-id="cc46a-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="cc46a-364">**Tipo di accesso:** normale</span><span class="sxs-lookup"><span data-stu-id="cc46a-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="cc46a-365">**Utente:** immettere l'utente FTP/distribuzione copiato dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc46a-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span></span> <span data-ttu-id="cc46a-366">Si tratta del nome completo dell'utente dell'FTP, che presenta il l formato *nomeappweb\nomeutente*.</span><span class="sxs-lookup"><span data-stu-id="cc46a-366">This is the full FTP username, which has the form *webappname\username*.</span></span>
   * <span data-ttu-id="cc46a-367">**Password:** immettere la password specificata quando si sono impostate le credenziali di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span></span>
     
     <span data-ttu-id="cc46a-368">Nella scheda **Impostazioni di trasferimento** selezionare **Passiva**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-368">On the **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="cc46a-369">Fare clic su **Connect**.</span><span class="sxs-lookup"><span data-stu-id="cc46a-369">Click **Connect**.</span></span> <span data-ttu-id="cc46a-370">Se l'esito è positivo, la console di FileZilla visualizzerà un messaggio `Status: Connected` ed eseguirà un comando `LIST` per elencare il contenuto della directory.</span><span class="sxs-lookup"><span data-stu-id="cc46a-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span></span>
4. <span data-ttu-id="cc46a-371">Nel pannello del sito **Local** (Locale) selezionare la directory di origine in cui si trova il file JSPHello.war. Il percorso sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cc46a-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="cc46a-372">Nel pannello del sito **Remote** selezionare la cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-372">In the **Remote** site panel, select the destination folder.</span></span> <span data-ttu-id="cc46a-373">Il file WAR verrà distribuito nella directory `webapps` sotto la radice dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="cc46a-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span></span> <span data-ttu-id="cc46a-374">Passare a **, fare clic con il pulsante destro del mouse su** e scegliere `/site/wwwroot`Create directory`wwwroot` (Crea directory).</span><span class="sxs-lookup"><span data-stu-id="cc46a-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="cc46a-375">Assegnare alla directory il nome `webapps` e aprirla.</span><span class="sxs-lookup"><span data-stu-id="cc46a-375">Name the directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="cc46a-376">Trasferire JSPHello.war in `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="cc46a-377">Selezionare JSPHello.war nell'elenco di file **Local** (Locale), fare clic con il pulsante destro del mouse su di esso e scegliere **Upload** (Carica).</span><span class="sxs-lookup"><span data-stu-id="cc46a-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="cc46a-378">Dovrebbe venire visualizzato in `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="cc46a-379">Dopo avere copiato JSPHello.war nella directory webapps, Tomcat Server decomprimerà automaticamente i file del file WAR.</span><span class="sxs-lookup"><span data-stu-id="cc46a-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span></span> <span data-ttu-id="cc46a-380">Anche se Tomcat Server inizia la decompressione quasi immediatamente, potrebbe volerci molto tempo (anche ore) prima che i file vengano visualizzati nel client FTP.</span><span class="sxs-lookup"><span data-stu-id="cc46a-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span></span>

#### <a name="run-the-hello-world-application-on-the-web-app"></a><span data-ttu-id="cc46a-381">Eseguire l'applicazione Hello World nell'app Web</span><span class="sxs-lookup"><span data-stu-id="cc46a-381">Run the Hello World application on the Web App</span></span>
1. <span data-ttu-id="cc46a-382">Dopo avere caricato il file WAR e verificato che il server Tomcat abbia creato una directory `JSPHello` decompressa, passare a `http://webdemowebapp.azurewebsites.net/JSPHello` per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cc46a-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span></span>
   
   > <span data-ttu-id="cc46a-383">**Nota:** se si fa clic su **Esplora risorse** nel portale classico, è possibile che si apra la pagina Web predefinita, che indica che l'applicazione Web basata su Java è stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="cc46a-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="cc46a-384">Potrebbe essere necessario aggiornare la pagina Web per visualizzare l'output dell'applicazione invece della pagina Web predefinita.</span><span class="sxs-lookup"><span data-stu-id="cc46a-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="cc46a-385">Quando viene eseguita l'applicazione, si dovrebbe aprire una pagina web con il seguente output:</span><span class="sxs-lookup"><span data-stu-id="cc46a-385">When the application runs, you should see a web page with the following output:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="cc46a-386">Pulire le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="cc46a-386">Clean up Azure resources</span></span>
<span data-ttu-id="cc46a-387">Questa procedura crea un'app web del servizio app.</span><span class="sxs-lookup"><span data-stu-id="cc46a-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="cc46a-388">Finché la risorsa esiste, i relativi costi verranno fatturati.</span><span class="sxs-lookup"><span data-stu-id="cc46a-388">You will be billed for the resource as long as it exists.</span></span> <span data-ttu-id="cc46a-389">A meno che non si preveda di continuare a usare l'app Web per il test o lo sviluppo, è consigliabile arrestarla o eliminarla.</span><span class="sxs-lookup"><span data-stu-id="cc46a-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="cc46a-390">Anche se un'app Web viene arrestata, è ugualmente prevista una piccola spesa, ma è possibile riavviarla in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="cc46a-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="cc46a-391">Con l'eliminazione di un'app Web vengono cancellati tutti i dati che erano stati caricati.</span><span class="sxs-lookup"><span data-stu-id="cc46a-391">Deleting a web app erases all data you have uploaded to it.</span></span>

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
