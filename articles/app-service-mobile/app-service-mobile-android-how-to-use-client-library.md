---
title: aaaHow toouse hello Azure Mobile App SDK per Android | Documenti Microsoft
description: Come toouse hello App Mobile di Azure SDK per Android
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="4777e-103">Come toouse hello App Mobile di Azure SDK per Android</span><span class="sxs-lookup"><span data-stu-id="4777e-103">How toouse hello Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="4777e-104">Questa guida viene spiegato come toouse hello client SDK per Android per scenari comuni tooimplement App per dispositivi mobili, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4777e-104">This guide shows you how toouse hello Android client SDK for Mobile Apps tooimplement common scenarios, such as:</span></span>

* <span data-ttu-id="4777e-105">L'esecuzione di query sui dati, come inserimento, aggiornamento ed eliminazione.</span><span class="sxs-lookup"><span data-stu-id="4777e-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="4777e-106">L'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4777e-106">Authentication.</span></span>
* <span data-ttu-id="4777e-107">La gestione degli errori.</span><span class="sxs-lookup"><span data-stu-id="4777e-107">Handling errors.</span></span>
* <span data-ttu-id="4777e-108">Personalizzazione client hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-108">Customizing hello client.</span></span>

<span data-ttu-id="4777e-109">Questa guida è incentrata su hello sul lato client Android SDK.</span><span class="sxs-lookup"><span data-stu-id="4777e-109">This guide focuses on hello client-side Android SDK.</span></span>  <span data-ttu-id="4777e-110">toolearn hello SDK lato server per le App per dispositivi mobili, vedere altre informazioni sulle [utilizzano back-end .NET SDK] [ 10] o [come toouse hello back-end Node.js SDK] [ 11].</span><span class="sxs-lookup"><span data-stu-id="4777e-110">toolearn more about hello server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How toouse hello Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="4777e-111">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="4777e-111">Reference Documentation</span></span>

<span data-ttu-id="4777e-112">È possibile trovare hello [riferimento all'API Javadocs] [ 12] per la libreria client per Android hello su GitHub.</span><span class="sxs-lookup"><span data-stu-id="4777e-112">You can find hello [Javadocs API reference][12] for hello Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4777e-113">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="4777e-113">Supported Platforms</span></span>

<span data-ttu-id="4777e-114">le applicazioni mobili di Azure SDK per Android Hello supporta livelli API 19 e 24 (KitKat tramite Nougat) per fattori di forma tablet e telefoni.</span><span class="sxs-lookup"><span data-stu-id="4777e-114">hello Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="4777e-115">L'autenticazione, in particolare, utilizza delle credenziali toogather approccio framework web comuni.</span><span class="sxs-lookup"><span data-stu-id="4777e-115">Authentication, in particular, utilizes a common web framework approach toogather credentials.</span></span>  <span data-ttu-id="4777e-116">L'autenticazione basata sul flusso server non funziona con dispositivi con fattore di forma piccolo, ad esempio gli orologi.</span><span class="sxs-lookup"><span data-stu-id="4777e-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="4777e-117">Installazione e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4777e-117">Setup and Prerequisites</span></span>

<span data-ttu-id="4777e-118">Hello completo [avvio rapido di applicazioni per dispositivi mobili](app-service-mobile-android-get-started.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4777e-118">Complete hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="4777e-119">Questa attività garantisce che vengano soddisfatti tutti i prerequisiti per lo sviluppo di App per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="4777e-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="4777e-120">Guida introduttiva Hello consente inoltre di configurare l'account e creare il prima App per dispositivi mobili di back-end.</span><span class="sxs-lookup"><span data-stu-id="4777e-120">hello Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="4777e-121">Se si decide di non toocomplete hello conosca, completare hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="4777e-121">If you decide not toocomplete hello Quickstart tutorial, complete hello following tasks:</span></span>

* <span data-ttu-id="4777e-122">[creare un back-end dell'App Mobile] [ 13] toouse con l'app Android.</span><span class="sxs-lookup"><span data-stu-id="4777e-122">[create a Mobile App backend][13] toouse with your Android app.</span></span>
* <span data-ttu-id="4777e-123">In Android Studio [compilare i file di aggiornamento hello Gradle](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="4777e-123">In Android Studio, [update hello Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="4777e-124">[Abilitare l'autorizzazione per Internet](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="4777e-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="4777e-125"><a name="gradle-build"></a>Aggiornare i file di compilazione Gradle hello</span><span class="sxs-lookup"><span data-stu-id="4777e-125"><a name="gradle-build"></a>Update hello Gradle build file</span></span>

<span data-ttu-id="4777e-126">Modificare entrambi i file **build.gradle** :</span><span class="sxs-lookup"><span data-stu-id="4777e-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="4777e-127">Aggiungere questo codice toohello *progetto* livello **gradle** file all'interno di hello *buildscript* tag:</span><span class="sxs-lookup"><span data-stu-id="4777e-127">Add this code toohello *Project* level **build.gradle** file inside hello *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="4777e-128">Aggiungere questo codice toohello *modulo app* livello **gradle** file all'interno di hello *dipendenze* tag:</span><span class="sxs-lookup"><span data-stu-id="4777e-128">Add this code toohello *Module app* level **build.gradle** file inside hello *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="4777e-129">Attualmente la versione più recente di hello è 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="4777e-129">Currently hello latest version is 3.3.0.</span></span> <span data-ttu-id="4777e-130">sono elencate le versioni supportata di Hello [su bintray][14].</span><span class="sxs-lookup"><span data-stu-id="4777e-130">hello supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="4777e-131"><a name="enable-internet"></a>Abilitare l'autorizzazione per Internet</span><span class="sxs-lookup"><span data-stu-id="4777e-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="4777e-132">tooaccess Azure, l'applicazione deve disporre di autorizzazioni INTERNET hello abilitato.</span><span class="sxs-lookup"><span data-stu-id="4777e-132">tooaccess Azure, your app must have hello INTERNET permission enabled.</span></span> <span data-ttu-id="4777e-133">Se non è già abilitato, aggiungere hello successiva riga di codice tooyour **AndroidManifest.xml** file:</span><span class="sxs-lookup"><span data-stu-id="4777e-133">If it's not already enabled, add hello following line of code tooyour **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="4777e-134">Creare una connessione client</span><span class="sxs-lookup"><span data-stu-id="4777e-134">Create a Client Connection</span></span>

<span data-ttu-id="4777e-135">Azure App per dispositivi mobili sono disponibili quattro funzioni tooyour applicazioni per dispositivi mobili:</span><span class="sxs-lookup"><span data-stu-id="4777e-135">Azure Mobile Apps provides four functions tooyour mobile application:</span></span>

* <span data-ttu-id="4777e-136">Accesso ai dati e sincronizzazione offline con un servizio di App per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="4777e-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="4777e-137">Chiamare le API personalizzate scritte con hello Azure Mobile App Server SDK.</span><span class="sxs-lookup"><span data-stu-id="4777e-137">Call Custom APIs written with hello Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="4777e-138">Autenticazione con autenticazione e autorizzazione nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="4777e-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="4777e-139">Registrazione di notifiche push con Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="4777e-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="4777e-140">Per ogni funzione prima di tutto è necessario creare un oggetto `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="4777e-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="4777e-141">È consigliabile creare un solo oggetto `MobileServiceClient` nel client per dispositivi mobili, ovvero il modello deve essere singleton.</span><span class="sxs-lookup"><span data-stu-id="4777e-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="4777e-142">toocreate un `MobileServiceClient` oggetto:</span><span class="sxs-lookup"><span data-stu-id="4777e-142">toocreate a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

<span data-ttu-id="4777e-143">Hello `<MobileAppUrl>` è una stringa o un oggetto di URL che punta back-end mobile tooyour.</span><span class="sxs-lookup"><span data-stu-id="4777e-143">hello `<MobileAppUrl>` is either a string or a URL object that points tooyour mobile backend.</span></span>  <span data-ttu-id="4777e-144">Se si utilizza Azure App Service toohost back-end per dispositivi mobili, quindi accertarsi di utilizzare hello sicura `https://` versione di hello URL.</span><span class="sxs-lookup"><span data-stu-id="4777e-144">If you are using Azure App Service toohost your mobile backend, then ensure you use hello secure `https://` version of hello URL.</span></span>

<span data-ttu-id="4777e-145">Hello client inoltre richiede accesso toohello attività o il contesto - hello `this` parametro nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-145">hello client also requires access toohello Activity or Context - hello `this` parameter in hello example.</span></span>  <span data-ttu-id="4777e-146">Hello MobileServiceClient costruzione deve verificarsi all'interno di hello `onCreate()` metodo dell'attività a cui fa riferimento a hello hello `AndroidManifest.xml` file.</span><span class="sxs-lookup"><span data-stu-id="4777e-146">hello MobileServiceClient construction should happen within hello `onCreate()` method of hello Activity referenced in hello `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="4777e-147">Come procedura consigliata, è opportuno astrarre le comunicazioni del server nella relativa classe (modello singleton).</span><span class="sxs-lookup"><span data-stu-id="4777e-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="4777e-148">In questo caso, è necessario passare hello attività all'interno di hello costruttore tooappropriately configurare servizio hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-148">In this case, you should pass hello Activity within hello constructor tooappropriately configure hello service.</span></span>  <span data-ttu-id="4777e-149">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4777e-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="4777e-150">È ora possibile chiamare `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` metodo dell'attività principale.</span><span class="sxs-lookup"><span data-stu-id="4777e-150">You can now call `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="4777e-151">Utilizzano altri metodi che necessitano di client di accesso toohello `AzureServiceAdapter.getInstance();` tooobtain un adattatore del servizio toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="4777e-151">Any other methods needing access toohello client use `AzureServiceAdapter.getInstance();` tooobtain a reference toohello service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="4777e-152">Operazioni dati</span><span class="sxs-lookup"><span data-stu-id="4777e-152">Data Operations</span></span>

<span data-ttu-id="4777e-153">core Hello di hello App Mobile di Azure SDK è tooprovide toodata di accesso archiviato in SQL Azure nel back-end di hello App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4777e-153">hello core of hello Azure Mobile Apps SDK is tooprovide access toodata stored within SQL Azure on hello Mobile App backend.</span></span>  <span data-ttu-id="4777e-154">È possibile accedere a questi dati usando classi fortemente tipizzate (preferibile) o query non tipizzate (non consigliato).</span><span class="sxs-lookup"><span data-stu-id="4777e-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="4777e-155">bulk Hello in questa sezione riguarda l'utilizzo di classi fortemente tipizzate.</span><span class="sxs-lookup"><span data-stu-id="4777e-155">hello bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="4777e-156">Definire le classi di dati client</span><span class="sxs-lookup"><span data-stu-id="4777e-156">Define client data classes</span></span>

<span data-ttu-id="4777e-157">tooaccess dati dalle tabelle di SQL Azure, definire classi di dati client corrispondenti tabelle toohello nel back-end di hello App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4777e-157">tooaccess data from SQL Azure tables, define client data classes that correspond toohello tables in hello Mobile App backend.</span></span> <span data-ttu-id="4777e-158">Negli esempi in questo argomento si presuppone una tabella denominata **MyDataTable**, che dispone di hello seguenti colonne:</span><span class="sxs-lookup"><span data-stu-id="4777e-158">Examples in this topic assume a table named **MyDataTable**, which has hello following columns:</span></span>

* <span data-ttu-id="4777e-159">id</span><span class="sxs-lookup"><span data-stu-id="4777e-159">id</span></span>
* <span data-ttu-id="4777e-160">text</span><span class="sxs-lookup"><span data-stu-id="4777e-160">text</span></span>
* <span data-ttu-id="4777e-161">complete</span><span class="sxs-lookup"><span data-stu-id="4777e-161">complete</span></span>

<span data-ttu-id="4777e-162">Hello oggetto sul lato client tipizzato corrispondente si trova in un file denominato **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="4777e-162">hello corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="4777e-163">Aggiungere i metodi getter e setter per ogni campo aggiunto.</span><span class="sxs-lookup"><span data-stu-id="4777e-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="4777e-164">Se la tabella di SQL Azure contiene più colonne, è possibile aggiungere classe toothis campi corrispondenti di hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-164">If your SQL Azure table contains more columns, you would add hello corresponding fields toothis class.</span></span>  <span data-ttu-id="4777e-165">Ad esempio, se hello DTO (oggetto di trasferimento di dati) è una colonna di tipo integer priorità, quindi è possibile aggiungere questo campo, insieme ai relativi metodi get e set:</span><span class="sxs-lookup"><span data-stu-id="4777e-165">For example, if hello DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="4777e-166">toolearn toocreate tabelle aggiuntive nel back-end App per dispositivi mobili, vedere [procedura: definire un controller di tabella] [ 15] (back-end .NET) o [definire tabelle utilizzando uno Schema dinamico] [ 16] (Back-end di Node. js).</span><span class="sxs-lookup"><span data-stu-id="4777e-166">toolearn how toocreate additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="4777e-167">Una tabella di back-end delle App mobili di Azure definisce cinque campi speciali, quattro delle quali sono disponibili tooclients:</span><span class="sxs-lookup"><span data-stu-id="4777e-167">An Azure Mobile Apps backend table defines five special fields, four of which are available tooclients:</span></span>

* <span data-ttu-id="4777e-168">`String id`: ID univoco globale per il record di hello hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-168">`String id`: hello globally unique ID for hello record.</span></span>  <span data-ttu-id="4777e-169">Come procedura consigliata, assicurarsi di rappresentazione di stringa di hello hello id di un [UUID] [ 17] oggetto.</span><span class="sxs-lookup"><span data-stu-id="4777e-169">As a best practice, make hello id hello String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="4777e-170">`DateTimeOffset updatedAt`: hello data/ora dell'ultimo aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-170">`DateTimeOffset updatedAt`: hello date/time of hello last update.</span></span>  <span data-ttu-id="4777e-171">campo updatedAt Hello è impostato dal server hello e non deve essere mai impostata dal codice client.</span><span class="sxs-lookup"><span data-stu-id="4777e-171">hello updatedAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="4777e-172">`DateTimeOffset createdAt`: hello data/ora è stato creato l'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-172">`DateTimeOffset createdAt`: hello date/time that hello object was created.</span></span>  <span data-ttu-id="4777e-173">campo createdAt Hello è impostato dal server hello e non deve essere mai impostata dal codice client.</span><span class="sxs-lookup"><span data-stu-id="4777e-173">hello createdAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="4777e-174">`byte[] version`: In genere è rappresentato come stringa, versione di hello anche viene impostato dal server hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-174">`byte[] version`: Normally represented as a string, hello version is also set by hello server.</span></span>
* <span data-ttu-id="4777e-175">`boolean deleted`: Indica che i record di hello è stato eliminato ma non ancora eliminati.</span><span class="sxs-lookup"><span data-stu-id="4777e-175">`boolean deleted`: Indicates that hello record has been deleted but not purged yet.</span></span>  <span data-ttu-id="4777e-176">Non usare `deleted` come proprietà nella classe.</span><span class="sxs-lookup"><span data-stu-id="4777e-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="4777e-177">Hello `id` campo è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="4777e-177">hello `id` field is required.</span></span>  <span data-ttu-id="4777e-178">Hello `updatedAt` campo e `version` campo vengono utilizzati per la sincronizzazione non in linea (per la risoluzione dei conflitti e di sincronizzazione incrementale rispettivamente).</span><span class="sxs-lookup"><span data-stu-id="4777e-178">hello `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="4777e-179">Hello `createdAt` campo è un campo di riferimento e non viene utilizzato dal client hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-179">hello `createdAt` field is a reference field and is not used by hello client.</span></span>  <span data-ttu-id="4777e-180">i nomi di Hello "in transito" come nome di proprietà hello e non sono modificabili.</span><span class="sxs-lookup"><span data-stu-id="4777e-180">hello names are "across-the-wire" names of hello properties and are not adjustable.</span></span>  <span data-ttu-id="4777e-181">Tuttavia, è possibile creare un mapping tra l'oggetto e hello "in transito" nomi utilizzando hello [gson] [ 3] libreria.</span><span class="sxs-lookup"><span data-stu-id="4777e-181">However, you can create a mapping between your object and hello "across-the-wire" names using hello [gson][3] library.</span></span>  <span data-ttu-id="4777e-182">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4777e-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="4777e-183">Creare un riferimento alla tabella</span><span class="sxs-lookup"><span data-stu-id="4777e-183">Create a Table Reference</span></span>

<span data-ttu-id="4777e-184">tooaccess una tabella, creare innanzitutto un [MobileServiceTable] [ 8] oggetto chiamante hello **getTable** metodo hello [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="4777e-184">tooaccess a table, first create a [MobileServiceTable][8] object by calling hello **getTable** method on hello [MobileServiceClient][9].</span></span>  <span data-ttu-id="4777e-185">Questo metodo presenta due overload:</span><span class="sxs-lookup"><span data-stu-id="4777e-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="4777e-186">Nel seguente codice, hello **mClient** è un oggetto MobileServiceClient tooyour di riferimento.</span><span class="sxs-lookup"><span data-stu-id="4777e-186">In hello following code, **mClient** is a reference tooyour MobileServiceClient object.</span></span>  <span data-ttu-id="4777e-187">Hello primo overload viene utilizzato in cui il nome di classe hello e nome della tabella hello sono hello stesso e hello uno utilizzato nella Guida introduttiva hello:</span><span class="sxs-lookup"><span data-stu-id="4777e-187">hello first overload is used where hello class name and hello table name are hello same, and is hello one used in hello Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="4777e-188">Hello secondo overload viene utilizzato il nome di tabella hello è diverso dal nome di classe hello: hello primo parametro è il nome di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-188">hello second overload is used when hello table name is different from hello class name: hello first parameter is hello table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="4777e-189"><a name="query"></a>Eseguire una query su una tabella del back-end</span><span class="sxs-lookup"><span data-stu-id="4777e-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="4777e-190">Ottenere prima di tutto un riferimento alla tabella.</span><span class="sxs-lookup"><span data-stu-id="4777e-190">First, obtain a table reference.</span></span>  <span data-ttu-id="4777e-191">Eseguire una query in riferimento alla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-191">Then execute a query on hello table reference.</span></span>  <span data-ttu-id="4777e-192">Una query è qualsiasi combinazione di:</span><span class="sxs-lookup"><span data-stu-id="4777e-192">A query is any combination of:</span></span>

* <span data-ttu-id="4777e-193">Una [clausola di filtro](#filtering) `.where()`.</span><span class="sxs-lookup"><span data-stu-id="4777e-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="4777e-194">Una [clausola di ordinamento](#sorting) `.orderBy()`.</span><span class="sxs-lookup"><span data-stu-id="4777e-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="4777e-195">Una [clausola di selezione campo](#selection) `.select()`.</span><span class="sxs-lookup"><span data-stu-id="4777e-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="4777e-196">`.skip()` e `.top()` per i [risultati di paging](#paging).</span><span class="sxs-lookup"><span data-stu-id="4777e-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="4777e-197">clausole Hello devono essere presentate in hello ordine precedente.</span><span class="sxs-lookup"><span data-stu-id="4777e-197">hello clauses must be presented in hello preceding order.</span></span>

### <span data-ttu-id="4777e-198"><a name="filter"></a> Applicazione di filtri ai risultati</span><span class="sxs-lookup"><span data-stu-id="4777e-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="4777e-199">Hello forma generale di una query è:</span><span class="sxs-lookup"><span data-stu-id="4777e-199">hello general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

<span data-ttu-id="4777e-200">Hello esempio precedente restituisce tutti i risultati (le dimensioni massime della pagina toohello impostato dal server hello).</span><span class="sxs-lookup"><span data-stu-id="4777e-200">hello preceding example returns all results (up toohello maximum page size set by hello server).</span></span>  <span data-ttu-id="4777e-201">Hello `.execute()` metodo esegue query hello sul back-end hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-201">hello `.execute()` method executes hello query on hello backend.</span></span>  <span data-ttu-id="4777e-202">query Hello è convertito tooan [OData v3] [ 19] query prima di back-end di trasmissione toohello App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4777e-202">hello query is converted tooan [OData v3][19] query before transmission toohello Mobile Apps backend.</span></span>  <span data-ttu-id="4777e-203">Al momento della ricezione, back-end App per dispositivi mobili hello converte query hello in un'istruzione SQL prima dell'esecuzione nell'istanza di SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-203">On receipt, hello Mobile Apps backend converts hello query into an SQL statement before executing it on hello SQL Azure instance.</span></span>  <span data-ttu-id="4777e-204">Poiché l'attività di rete può richiedere tempo, hello `.execute()` metodo restituisce un [ `ListenableFuture<E>` ] [ 18].</span><span class="sxs-lookup"><span data-stu-id="4777e-204">Since network activity takes some time, hello `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="4777e-205"><a name="filtering"></a>Filtrare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="4777e-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="4777e-206">Hello dopo l'esecuzione di query restituisce tutti gli elementi da hello **ToDoItem** tabella in cui **completo** è uguale a **false**.</span><span class="sxs-lookup"><span data-stu-id="4777e-206">hello following query execution returns all items from hello **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="4777e-207">**mToDoTable** hello riferimento toohello servizio mobile tabella creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4777e-207">**mToDoTable** is hello reference toohello mobile service table that we created previously.</span></span>

<span data-ttu-id="4777e-208">Definire un filtro utilizzando hello **dove** chiamata al metodo nel riferimento alla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-208">Define a filter using hello **where** method call on hello table reference.</span></span> <span data-ttu-id="4777e-209">Hello **in** metodo è seguito da un **campo** metodo seguito da un metodo che specifica hello logico predicato.</span><span class="sxs-lookup"><span data-stu-id="4777e-209">hello **where** method is followed by a **field** method followed by a method that specifies hello logical predicate.</span></span> <span data-ttu-id="4777e-210">I possibili metodi di predicato includono **eq** (uguale a), **ne** (non uguale a), **gt** (maggiore di), **ge** (maggiore o uguale a), **lt** (minore di), **le** (minore o uguale a).</span><span class="sxs-lookup"><span data-stu-id="4777e-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="4777e-211">Questi metodi consentono di confrontare numero e i valori toospecific i campi stringa.</span><span class="sxs-lookup"><span data-stu-id="4777e-211">These methods let you compare number and string fields toospecific values.</span></span>

<span data-ttu-id="4777e-212">ad esempio filtrare in base alle date.</span><span class="sxs-lookup"><span data-stu-id="4777e-212">You can filter on dates.</span></span> <span data-ttu-id="4777e-213">Hello metodi seguenti consentono di confrontare il campo di data completa hello o parti di data hello: **anno**, **mese**, **giorno**, **ora**, **minuto**, e **secondo**.</span><span class="sxs-lookup"><span data-stu-id="4777e-213">hello following methods let you compare hello entire date field or parts of hello date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="4777e-214">esempio Hello aggiunge un filtro per gli elementi il cui *data di scadenza* 2013 è uguale.</span><span class="sxs-lookup"><span data-stu-id="4777e-214">hello following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="4777e-215">Hello metodi seguenti supportano i filtri complessi nei campi stringa: **startsWith**, **endsWith**, **concat**, **sottostringa**, **indexOf**, **sostituire**, **toLower**, **toUpper**, **trim**, e  **lunghezza**.</span><span class="sxs-lookup"><span data-stu-id="4777e-215">hello following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="4777e-216">Hello seguendo i filtri di esempio per le righe della tabella in cui hello *testo* colonna inizia con "PRI0".</span><span class="sxs-lookup"><span data-stu-id="4777e-216">hello following example filters for table rows where hello *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="4777e-217">Hello metodi degli operatori seguenti è supportato nei campi numero: **aggiungere**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, e **arrotondare**.</span><span class="sxs-lookup"><span data-stu-id="4777e-217">hello following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="4777e-218">Hello seguendo i filtri di esempio per le righe della tabella in cui hello **durata** è un numero pari.</span><span class="sxs-lookup"><span data-stu-id="4777e-218">hello following example filters for table rows where hello **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="4777e-219">È possibile combinare i predicati con questi metodi logici: **and**, **or** e **not**.</span><span class="sxs-lookup"><span data-stu-id="4777e-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="4777e-220">Hello di esempio seguente unisce due precedenti esempi hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-220">hello following example combines two of hello preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="4777e-221">Raggruppare e annidare operatori logici:</span><span class="sxs-lookup"><span data-stu-id="4777e-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="4777e-222">Per ulteriori informazioni ed esempi di filtro, vedere [esplorazione ricchezza hello del modello di query client Android hello][20].</span><span class="sxs-lookup"><span data-stu-id="4777e-222">For more detailed discussion and examples of filtering, see [Exploring hello richness of hello Android client query model][20].</span></span>

### <span data-ttu-id="4777e-223"><a name="sorting"></a>Ordinare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="4777e-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="4777e-224">Hello codice seguente restituisce tutti gli elementi di una tabella **ToDoItems** disposti in ordine crescente da hello *testo* campo.</span><span class="sxs-lookup"><span data-stu-id="4777e-224">hello following code returns all items from a table of **ToDoItems** sorted ascending by hello *text* field.</span></span> <span data-ttu-id="4777e-225">*mToDoTable* hello riferimento toohello back-end tabella creata in precedenza è:</span><span class="sxs-lookup"><span data-stu-id="4777e-225">*mToDoTable* is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="4777e-226">primo parametro di hello Hello **orderBy** metodo è un nome di toohello uguale di stringa del campo hello nella quale toosort.</span><span class="sxs-lookup"><span data-stu-id="4777e-226">hello first parameter of hello **orderBy** method is a string equal toohello name of hello field on which toosort.</span></span> <span data-ttu-id="4777e-227">secondo parametro Hello utilizza hello **QueryOrder** enumerazione toospecify se toosort crescente o decrescente.</span><span class="sxs-lookup"><span data-stu-id="4777e-227">hello second parameter uses hello **QueryOrder** enumeration toospecify whether toosort ascending or descending.</span></span>  <span data-ttu-id="4777e-228">Se si applica un filtro utilizzando hello ***in*** (metodo), hello ***in*** metodo deve essere chiamato prima di hello ***orderBy*** metodo.</span><span class="sxs-lookup"><span data-stu-id="4777e-228">If you are filtering using hello ***where*** method, hello ***where*** method must be invoked before hello ***orderBy*** method.</span></span>

### <span data-ttu-id="4777e-229"><a name="selection"></a>Selezionare colonne specifiche</span><span class="sxs-lookup"><span data-stu-id="4777e-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="4777e-230">Hello codice seguente viene illustrato come tooreturn tutti gli elementi di una tabella **ToDoItems**, ma visualizza solo hello **completo** e **testo** campi.</span><span class="sxs-lookup"><span data-stu-id="4777e-230">hello following code illustrates how tooreturn all items from a table of **ToDoItems**, but only displays hello **complete** and **text** fields.</span></span> <span data-ttu-id="4777e-231">**mToDoTable** hello riferimento toohello back-end tabella creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4777e-231">**mToDoTable** is hello reference toohello backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="4777e-232">funzione di selezione di Hello parametri toohello sono nomi di stringa hello hello colonna di tabella che si desidera tooreturn.</span><span class="sxs-lookup"><span data-stu-id="4777e-232">hello parameters toohello select function are hello string names of hello table's columns that you want tooreturn.</span></span>  <span data-ttu-id="4777e-233">Hello **selezionare** metodo richiede metodi toofollow come **in** e **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="4777e-233">hello **select** method needs toofollow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="4777e-234">Può essere seguito da metodi di paging come **skip** e **top**.</span><span class="sxs-lookup"><span data-stu-id="4777e-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="4777e-235"><a name="paging"></a>Restituire i dati in pagine</span><span class="sxs-lookup"><span data-stu-id="4777e-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="4777e-236">I dati vengono **SEMPRE** restituiti in pagine.</span><span class="sxs-lookup"><span data-stu-id="4777e-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="4777e-237">numero massimo di Hello di record restituito viene impostato dal server hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-237">hello maximum number of records returned is set by hello server.</span></span>  <span data-ttu-id="4777e-238">Se il client di hello richiede più record, quindi server hello restituisce hello numero massimo di record.</span><span class="sxs-lookup"><span data-stu-id="4777e-238">If hello client requests more records, then hello server returns hello maximum number of records.</span></span>  <span data-ttu-id="4777e-239">Per impostazione predefinita, la dimensione massima della pagina hello sul server di hello è 50 record.</span><span class="sxs-lookup"><span data-stu-id="4777e-239">By default, hello maximum page size on hello server is 50 records.</span></span>

<span data-ttu-id="4777e-240">Hello primo esempio viene illustrato come tooselect hello primi cinque elementi da una tabella.</span><span class="sxs-lookup"><span data-stu-id="4777e-240">hello first example shows how tooselect hello top five items from a table.</span></span> <span data-ttu-id="4777e-241">query Hello restituisce gli elementi di hello da una tabella di **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="4777e-241">hello query returns hello items from a table of **ToDoItems**.</span></span> <span data-ttu-id="4777e-242">**mToDoTable** hello riferimento toohello back-end tabella creata in precedenza è:</span><span class="sxs-lookup"><span data-stu-id="4777e-242">**mToDoTable** is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="4777e-243">Ecco una query che ignora hello primi cinque elementi e quindi restituisce hello cinque Avanti:</span><span class="sxs-lookup"><span data-stu-id="4777e-243">Here's a query that skips hello first five items, and then returns hello next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="4777e-244">Se si desiderano tooget tutti i record in una tabella, è possibile implementare codice tooiterate su tutte le pagine:</span><span class="sxs-lookup"><span data-stu-id="4777e-244">If you wish tooget all records in a table, implement code tooiterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="4777e-245">Una richiesta per tutti i record con questo metodo crea un minimo di back-end di due richieste toohello App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4777e-245">A request for all records using this method creates a minimum of two requests toohello Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="4777e-246">Dimensioni di pagina destra scegliendo hello sono un equilibrio tra l'utilizzo della memoria richiesta hello in corso, l'utilizzo della larghezza di banda e ritardi nella ricezione di dati hello completamente.</span><span class="sxs-lookup"><span data-stu-id="4777e-246">Choosing hello right page size is a balance between memory usage while hello request is happening, bandwidth usage and delay in receiving hello data completely.</span></span>  <span data-ttu-id="4777e-247">valore predefinito di Hello (50 record) è adatto per tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4777e-247">hello default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="4777e-248">Se si opera esclusivamente nei dispositivi più grandi di memoria, aumentare le too500.</span><span class="sxs-lookup"><span data-stu-id="4777e-248">If you exclusively operate on larger memory devices, increase up too500.</span></span>  <span data-ttu-id="4777e-249">Sono stati rilevati tali dimensioni di pagina hello crescente oltre 500 registra i risultati in ritardo accettabile e problemi di memoria di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="4777e-249">We have found that increasing hello page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="4777e-250"><a name="chaining"></a>Procedura: Concatenare metodi di query</span><span class="sxs-lookup"><span data-stu-id="4777e-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="4777e-251">metodi di Hello utilizzati in una query sulle tabelle di back-end possono essere concatenati.</span><span class="sxs-lookup"><span data-stu-id="4777e-251">hello methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="4777e-252">Concatenamento di query metodi consente tooselect colonne specifiche di righe filtrate e del pool di paging.</span><span class="sxs-lookup"><span data-stu-id="4777e-252">Chaining query methods allows you tooselect specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="4777e-253">È possibile creare filtri logici complessi.</span><span class="sxs-lookup"><span data-stu-id="4777e-253">You can create complex logical filters.</span></span>  <span data-ttu-id="4777e-254">Ogni metodo di query restituisce un oggetto Query.</span><span class="sxs-lookup"><span data-stu-id="4777e-254">Each query method returns a Query object.</span></span> <span data-ttu-id="4777e-255">serie di hello tooend di metodi e query effettivamente esecuzione hello, chiamata hello **eseguire** metodo.</span><span class="sxs-lookup"><span data-stu-id="4777e-255">tooend hello series of methods and actually run hello query, call hello **execute** method.</span></span> <span data-ttu-id="4777e-256">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4777e-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="4777e-257">Hello concatenate query metodi devono essere ordinati come segue:</span><span class="sxs-lookup"><span data-stu-id="4777e-257">hello chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="4777e-258">Metodi di filtraggio (**where**).</span><span class="sxs-lookup"><span data-stu-id="4777e-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="4777e-259">Metodi di ordinamento (**orderBy**).</span><span class="sxs-lookup"><span data-stu-id="4777e-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="4777e-260">Metodi di selezione (**select**).</span><span class="sxs-lookup"><span data-stu-id="4777e-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="4777e-261">Metodi di paging (**skip** e **top**).</span><span class="sxs-lookup"><span data-stu-id="4777e-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="4777e-262"><a name="binding"></a>Associare l'interfaccia utente toohello di dati</span><span class="sxs-lookup"><span data-stu-id="4777e-262"><a name="binding"></a>Bind data toohello user interface</span></span>

<span data-ttu-id="4777e-263">L'associazione dati riguarda tre componenti:</span><span class="sxs-lookup"><span data-stu-id="4777e-263">Data binding involves three components:</span></span>

* <span data-ttu-id="4777e-264">origine dati Hello</span><span class="sxs-lookup"><span data-stu-id="4777e-264">hello data source</span></span>
* <span data-ttu-id="4777e-265">layout della schermata Hello</span><span class="sxs-lookup"><span data-stu-id="4777e-265">hello screen layout</span></span>
* <span data-ttu-id="4777e-266">scheda Hello che ties hello due insieme.</span><span class="sxs-lookup"><span data-stu-id="4777e-266">hello adapter that ties hello two together.</span></span>

<span data-ttu-id="4777e-267">Nel codice di esempio, si restituiscono dati hello dalla tabella di SQL Azure di App mobili hello **ToDoItem** in una matrice.</span><span class="sxs-lookup"><span data-stu-id="4777e-267">In our sample code, we return hello data from hello Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="4777e-268">Si tratta di una delle attività più comuni per le applicazioni dati.</span><span class="sxs-lookup"><span data-stu-id="4777e-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="4777e-269">Le query di database spesso restituiscono una raccolta di righe che hello client ottiene un elenco o matrice.</span><span class="sxs-lookup"><span data-stu-id="4777e-269">Database queries often return a collection of rows that hello client gets in a list or array.</span></span> <span data-ttu-id="4777e-270">In questo esempio, matrice hello è l'origine dati hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-270">In this sample, hello array is hello data source.</span></span>  <span data-ttu-id="4777e-271">codice Hello specifica un layout della schermata che definisce hello visualizzazione dati hello che viene visualizzato nel dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-271">hello code specifies a screen layout that defines hello view of hello data that appears on hello device.</span></span>  <span data-ttu-id="4777e-272">Hello due sono associati insieme a un adapter, che in questo codice è un'estensione di hello **ArrayAdapter&lt;ToDoItem&gt;**  classe.</span><span class="sxs-lookup"><span data-stu-id="4777e-272">hello two are bound together with an adapter, which in this code is an extension of hello **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="4777e-273"><a name="layout"></a>Definire hello Layout</span><span class="sxs-lookup"><span data-stu-id="4777e-273"><a name="layout"></a>Define hello Layout</span></span>

<span data-ttu-id="4777e-274">layout di Hello è definito da diversi frammenti di codice XML.</span><span class="sxs-lookup"><span data-stu-id="4777e-274">hello layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="4777e-275">Dato un layout esistente, hello seguente di codice rappresenta hello **ListView** desideriamo toopopulate con i dati del server.</span><span class="sxs-lookup"><span data-stu-id="4777e-275">Given an existing layout, hello following code represents hello **ListView** we want toopopulate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="4777e-276">Nel codice precedente di hello, hello *listitem* attributo specifica l'id di hello del layout di hello per una singola riga nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-276">In hello preceding code, hello *listitem* attribute specifies hello id of hello layout for an individual row in hello list.</span></span> <span data-ttu-id="4777e-277">Questo codice consente di specificare una casella di controllo e il testo associato e viene creata un'istanza di una volta per ogni elemento nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-277">This code specifies a check box and its associated text and gets instantiated once for each item in hello list.</span></span> <span data-ttu-id="4777e-278">Questo layout non viene visualizzato hello **id** campo e un layout più complesso specificare campi aggiuntivi nella visualizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-278">This layout does not display hello **id** field, and a more complex layout would specify additional fields in hello display.</span></span> <span data-ttu-id="4777e-279">Questo codice è in hello **row_list_to_do.xml** file.</span><span class="sxs-lookup"><span data-stu-id="4777e-279">This code is in hello **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="4777e-280"><a name="adapter"></a>Definire hello adattatore</span><span class="sxs-lookup"><span data-stu-id="4777e-280"><a name="adapter"></a>Define hello adapter</span></span>
<span data-ttu-id="4777e-281">Poiché la vista origine dati hello è una matrice di **ToDoItem**, abbiamo sottoclasse l'adapter da un **ArrayAdapter&lt;ToDoItem&gt;**  classe.</span><span class="sxs-lookup"><span data-stu-id="4777e-281">Since hello data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="4777e-282">Questo tipo di sottoclasse produce una visualizzazione per ogni **ToDoItem** utilizzando hello **row_list_to_do** layout.</span><span class="sxs-lookup"><span data-stu-id="4777e-282">This subclass produces a View for every **ToDoItem** using hello **row_list_to_do** layout.</span></span>  <span data-ttu-id="4777e-283">Nel codice, è possibile definire hello seguente classe che è un'estensione di hello **ArrayAdapter&lt;E&gt;**  classe:</span><span class="sxs-lookup"><span data-stu-id="4777e-283">In our code, we define hello following class that is an extension of hello **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="4777e-284">Eseguire l'override di schede di hello **getView** metodo.</span><span class="sxs-lookup"><span data-stu-id="4777e-284">Override hello adapters **getView** method.</span></span> <span data-ttu-id="4777e-285">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4777e-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="4777e-286">Creare un'istanza della classe nell'attività nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="4777e-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="4777e-287">costruttore ToDoItemAdapter toohello Hello secondo parametro è un layout di toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="4777e-287">hello second parameter toohello ToDoItemAdapter constructor is a reference toohello layout.</span></span> <span data-ttu-id="4777e-288">È ora possibile creare un'istanza hello **ListView** e assegnare hello adapter toohello **ListView**.</span><span class="sxs-lookup"><span data-stu-id="4777e-288">We can now instantiate hello **ListView** and assign hello adapter toohello **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="4777e-289"><a name="use-adapter"></a>Utilizzare hello Adapter tooBind toohello dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="4777e-289"><a name="use-adapter"></a>Use hello Adapter tooBind toohello UI</span></span>

<span data-ttu-id="4777e-290">Si è ora pronto toouse l'associazione dati.</span><span class="sxs-lookup"><span data-stu-id="4777e-290">You are now ready toouse data binding.</span></span> <span data-ttu-id="4777e-291">Hello codice seguente viene illustrato come gli elementi tooget tabella hello e riempimenti hello scheda locale con hello restituita.</span><span class="sxs-lookup"><span data-stu-id="4777e-291">hello following code shows how tooget items in hello table and fills hello local adapter with hello returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="4777e-292">Chiamare adapter hello ogni volta che si modifica hello **ToDoItem** tabella.</span><span class="sxs-lookup"><span data-stu-id="4777e-292">Call hello adapter any time you modify hello **ToDoItem** table.</span></span> <span data-ttu-id="4777e-293">Dal momento che le modifiche vengono fatte record per record, si gestisce una singola riga anziché una raccolta.</span><span class="sxs-lookup"><span data-stu-id="4777e-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="4777e-294">Quando si inserisce un elemento, chiamare hello **aggiungere** metodo hello adapter; in caso di eliminazione, chiamare hello **rimuovere** metodo.</span><span class="sxs-lookup"><span data-stu-id="4777e-294">When you insert an item, call hello **add** method on hello adapter; when deleting, call hello **remove** method.</span></span>

<span data-ttu-id="4777e-295">È possibile trovare un esempio completo in hello [progetto di avvio rapido Android][21].</span><span class="sxs-lookup"><span data-stu-id="4777e-295">You can find a complete example in hello [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="4777e-296"><a name="inserting"></a>Inserire dati back-end hello</span><span class="sxs-lookup"><span data-stu-id="4777e-296"><a name="inserting"></a>Insert data into hello backend</span></span>

<span data-ttu-id="4777e-297">Creare un'istanza di hello *ToDoItem* classe e impostarne le proprietà.</span><span class="sxs-lookup"><span data-stu-id="4777e-297">Instantiate an instance of hello *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="4777e-298">Utilizzare quindi **Insert ()** tooinsert oggetto:</span><span class="sxs-lookup"><span data-stu-id="4777e-298">Then use **insert()** tooinsert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="4777e-299">Hello dati hello inseriti nella tabella di back-end hello, ID di hello incluso e tutti gli altri valori di corrispondenze di entità restituiti (ad esempio hello `createdAt`, `updatedAt`, e `version` campi) impostato sul back-end hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-299">hello returned entity matches hello data inserted into hello backend table, included hello ID and any other values (such as hello `createdAt`, `updatedAt`, and `version` fields) set on hello backend.</span></span>

<span data-ttu-id="4777e-300">Le tabelle di App per dispositivi mobili richiedono una colonna chiave primaria denominata **id**. Questa colonna deve essere una stringa.</span><span class="sxs-lookup"><span data-stu-id="4777e-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="4777e-301">il valore predefinito Hello della colonna ID hello è un GUID.</span><span class="sxs-lookup"><span data-stu-id="4777e-301">hello default value of hello ID column is a GUID.</span></span>  <span data-ttu-id="4777e-302">È possibile specificare altri valori univoci, come gli indirizzi di posta elettronica o i nomi utente.</span><span class="sxs-lookup"><span data-stu-id="4777e-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="4777e-303">Quando un valore di ID di stringa non viene fornito un record inserito, back-end hello genera un nuovo GUID.</span><span class="sxs-lookup"><span data-stu-id="4777e-303">When a string ID value is not provided for an inserted record, hello backend generates a new GUID.</span></span>

<span data-ttu-id="4777e-304">I valori di ID di stringa forniscono hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4777e-304">String ID values provide hello following advantages:</span></span>

* <span data-ttu-id="4777e-305">ID può essere generato senza un database toohello di andata e ritorno.</span><span class="sxs-lookup"><span data-stu-id="4777e-305">IDs can be generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="4777e-306">I record sono toomerge più semplice da diverse tabelle o database.</span><span class="sxs-lookup"><span data-stu-id="4777e-306">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="4777e-307">I valori ID si integrano in modo più efficace con la logica di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4777e-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="4777e-308">I valori ID di stringa sono **OBBLIGATORI** per il supporto di sincronizzazione offline.</span><span class="sxs-lookup"><span data-stu-id="4777e-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="4777e-309">È possibile modificare un Id di una volta che viene archiviato nel database back-end hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-309">You cannot change an Id once it is stored in hello backend database.</span></span>

## <span data-ttu-id="4777e-310"><a name="updating"></a>Aggiornare dati in un'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="4777e-310"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="4777e-311">tooupdate dati in una tabella, passare hello nuovo oggetto toohello **Update ()** metodo.</span><span class="sxs-lookup"><span data-stu-id="4777e-311">tooupdate data in a table, pass hello new object toohello **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="4777e-312">In questo esempio, *elemento* è una riferimento tooa riga hello *ToDoItem* tabella in cui è stato tooit alcune modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="4777e-312">In this example, *item* is a reference tooa row in hello *ToDoItem* table, which has had some changes made tooit.</span></span>  <span data-ttu-id="4777e-313">riga Hello con hello stesso **id** viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="4777e-313">hello row with hello same **id** is updated.</span></span>

## <span data-ttu-id="4777e-314"><a name="deleting"></a>Eliminare dati in un'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="4777e-314"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="4777e-315">Hello seguente codice mostra come toodelete dati da una tabella specificando hello oggetto dati.</span><span class="sxs-lookup"><span data-stu-id="4777e-315">hello following code shows how toodelete data from a table by specifying hello data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="4777e-316">È anche possibile eliminare un elemento specificando hello **id** campo toodelete riga hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-316">You can also delete an item by specifying hello **id** field of hello row toodelete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="4777e-317"><a name="lookup"></a>Cercare un elemento specifico per ID</span><span class="sxs-lookup"><span data-stu-id="4777e-317"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="4777e-318">Cercare un elemento con una versione specifica **id** campo hello **Lookup** metodo:</span><span class="sxs-lookup"><span data-stu-id="4777e-318">Look up an item with a specific **id** field with hello **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="4777e-319"><a name="untyped"></a>Procedura: Usare dati non tipizzati</span><span class="sxs-lookup"><span data-stu-id="4777e-319"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="4777e-320">modello di programmazione non tipizzato Hello offre il controllo completo della serializzazione JSON.</span><span class="sxs-lookup"><span data-stu-id="4777e-320">hello untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="4777e-321">Esistono alcuni scenari comuni in cui è preferibile toouse un modello di programmazione non tipizzato.</span><span class="sxs-lookup"><span data-stu-id="4777e-321">There are some common scenarios where you may wish toouse an untyped programming model.</span></span> <span data-ttu-id="4777e-322">Ad esempio, se la tabella di back-end contiene molte colonne ed è necessario solo un subset di colonne hello tooreference.</span><span class="sxs-lookup"><span data-stu-id="4777e-322">For example, if your backend table contains many columns and you only need tooreference a subset of hello columns.</span></span>  <span data-ttu-id="4777e-323">modello tipizzato Hello richiede toodefine tutte le colonne di hello definite nel back-end App per dispositivi mobili hello nella classe di dati.</span><span class="sxs-lookup"><span data-stu-id="4777e-323">hello typed model requires you toodefine all hello columns defined in hello Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="4777e-324">La maggior parte delle chiamate API per l'accesso ai dati hello sono simile toohello tipizzati chiamate di programmazione.</span><span class="sxs-lookup"><span data-stu-id="4777e-324">Most of hello API calls for accessing data are similar toohello typed programming calls.</span></span> <span data-ttu-id="4777e-325">Hello differenza principale è che nel modello non tipizzato hello per richiamare metodi su hello **MobileServiceJsonTable** oggetto, anziché hello **MobileServiceTable** oggetto.</span><span class="sxs-lookup"><span data-stu-id="4777e-325">hello main difference is that in hello untyped model you invoke methods on hello **MobileServiceJsonTable** object, instead of hello **MobileServiceTable** object.</span></span>

### <span data-ttu-id="4777e-326"><a name="json_instance"></a>Creare un'istanza di una tabella non tipizzata</span><span class="sxs-lookup"><span data-stu-id="4777e-326"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="4777e-327">Toohello simile tipizzati modello, iniziare recuperando un riferimento alla tabella, ma in questo caso è un **MobileServicesJsonTable** oggetto.</span><span class="sxs-lookup"><span data-stu-id="4777e-327">Similar toohello typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="4777e-328">Ottenere riferimento hello hello chiamante **getTable** metodo in un'istanza del client hello:</span><span class="sxs-lookup"><span data-stu-id="4777e-328">Obtain hello reference by calling hello **getTable** method on an instance of hello client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="4777e-329">Dopo aver creato un'istanza di hello **MobileServiceJsonTable**, è praticamente hello stessa API disponibile come modello di programmazione tipizzato hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-329">Once you have created an instance of hello **MobileServiceJsonTable**, it has virtually hello same API available as with hello typed programming model.</span></span> <span data-ttu-id="4777e-330">In alcuni casi, i metodi di hello accettano un parametro non tipizzato invece di un parametro tipizzato.</span><span class="sxs-lookup"><span data-stu-id="4777e-330">In some cases, hello methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="4777e-331"><a name="json_insert"></a>Eseguire un inserimento in una tabella non tipizzata</span><span class="sxs-lookup"><span data-stu-id="4777e-331"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="4777e-332">Hello seguente codice mostra come toodo un'istruzione insert.</span><span class="sxs-lookup"><span data-stu-id="4777e-332">hello following code shows how toodo an insert.</span></span> <span data-ttu-id="4777e-333">primo passaggio Hello è toocreate un [JsonObject][1], che fa parte di hello [gson] [ 3] libreria.</span><span class="sxs-lookup"><span data-stu-id="4777e-333">hello first step is toocreate a [JsonObject][1], which is part of hello [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="4777e-334">Utilizzare quindi **Insert ()** tooinsert oggetto non tipizzata di hello in tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-334">Then, Use **insert()** tooinsert hello untyped object into hello table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="4777e-335">Se è necessario tooget hello ID dell'oggetto inserito hello, utilizzare hello **getAsJsonPrimitive()** metodo.</span><span class="sxs-lookup"><span data-stu-id="4777e-335">If you need tooget hello ID of hello inserted object, use hello **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="4777e-336"><a name="json_delete"></a>Eliminare un'istanza da una tabella non tipizzata</span><span class="sxs-lookup"><span data-stu-id="4777e-336"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="4777e-337">Hello codice seguente viene illustrato come toodelete un'istanza, in questo caso, hello stessa istanza di un **JsonObject** creato nella prima hello *inserire* esempio.</span><span class="sxs-lookup"><span data-stu-id="4777e-337">hello following code shows how toodelete an instance, in this case, hello same instance of a **JsonObject** that was created in hello prior *insert* example.</span></span> <span data-ttu-id="4777e-338">codice Hello è hello stesso di hello tipizzata case, ma il metodo hello ha una firma diversa, perché fa riferimento a un **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="4777e-338">hello code is hello same as with hello typed case, but hello method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="4777e-339">È inoltre possibile eliminare un'istanza direttamente utilizzando il relativo ID:</span><span class="sxs-lookup"><span data-stu-id="4777e-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="4777e-340"><a name="json_get"></a>Restituire tutte le righe di una tabella non tipizzata</span><span class="sxs-lookup"><span data-stu-id="4777e-340"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="4777e-341">Hello seguente codice mostra come tooretrieve un'intera tabella.</span><span class="sxs-lookup"><span data-stu-id="4777e-341">hello following code shows how tooretrieve an entire table.</span></span> <span data-ttu-id="4777e-342">Poiché si utilizza una tabella JSON, è possibile recuperare in modo selettivo solo alcune colonne della tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-342">Since you are using a JSON Table, you can selectively retrieve only some of hello table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="4777e-343">Hello stesso set di filtri, filtro e paging metodi disponibili per il modello tipizzato hello sono disponibili per il modello non tipizzato hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-343">hello same set of filtering, filtering and paging methods that are available for hello typed model are available for hello untyped model.</span></span>

## <span data-ttu-id="4777e-344"><a name="offline-sync"></a>Implementare la sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="4777e-344"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="4777e-345">Hello Azure Mobile App Client SDK implementa inoltre la sincronizzazione non in linea dei dati utilizzando un toostore database SQLite una copia dei dati hello del server locale.</span><span class="sxs-lookup"><span data-stu-id="4777e-345">hello Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database toostore a copy of hello server data locally.</span></span>  <span data-ttu-id="4777e-346">Operazioni eseguite su una tabella non in linea non richiedono la connettività mobile toowork.</span><span class="sxs-lookup"><span data-stu-id="4777e-346">Operations performed on an offline table do not require mobile connectivity toowork.</span></span>  <span data-ttu-id="4777e-347">Sincronizzazione non in linea degli strumenti per la resilienza e delle spese di hello di una logica più complessa per la risoluzione dei conflitti.</span><span class="sxs-lookup"><span data-stu-id="4777e-347">Offline sync aids in resilience and performance at hello expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="4777e-348">Hello Azure Mobile App Client SDK implementa hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="4777e-348">hello Azure Mobile Apps Client SDK implements hello following features:</span></span>

* <span data-ttu-id="4777e-349">Sincronizzazione incrementale: vengono scaricati solo i record aggiornati e nuovi, risparmiando larghezza di banda e utilizzo della memoria.</span><span class="sxs-lookup"><span data-stu-id="4777e-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="4777e-350">Concorrenza ottimistica: Le operazioni vengono considerate toosucceed.</span><span class="sxs-lookup"><span data-stu-id="4777e-350">Optimistic Concurrency: Operations are assumed toosucceed.</span></span>  <span data-ttu-id="4777e-351">Risoluzione dei conflitti viene posticipata fino a quando gli aggiornamenti vengono eseguiti nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-351">Conflict Resolution is deferred until updates are performed on hello server.</span></span>
* <span data-ttu-id="4777e-352">Risoluzione dei conflitti: hello che SDK rileva se una modifica in conflitto è stata eseguita nel server di hello e fornisce hook utente hello tooalert.</span><span class="sxs-lookup"><span data-stu-id="4777e-352">Conflict Resolution: hello SDK detects when a conflicting change has been made at hello server and provides hooks tooalert hello user.</span></span>
* <span data-ttu-id="4777e-353">L'eliminazione temporanea: Record eliminato è contrassegnata come eliminato, consentendo tooupdate altri dispositivi la cache offline.</span><span class="sxs-lookup"><span data-stu-id="4777e-353">Soft Delete: Deleted records are marked deleted, allowing other devices tooupdate their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="4777e-354">Inizializzare la sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="4777e-354">Initialize Offline Sync</span></span>

<span data-ttu-id="4777e-355">Ogni tabella non in linea deve essere definito nella cache offline di hello prima dell'uso.</span><span class="sxs-lookup"><span data-stu-id="4777e-355">Each offline table must be defined in hello offline cache before use.</span></span>  <span data-ttu-id="4777e-356">Definizione della tabella in genere, viene eseguita subito dopo la creazione di hello del client hello:</span><span class="sxs-lookup"><span data-stu-id="4777e-356">Normally, table definition is done immediately after hello creation of hello client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a><span data-ttu-id="4777e-357">Ottenere un toohello di riferimento non in linea la tabella della Cache</span><span class="sxs-lookup"><span data-stu-id="4777e-357">Obtain a reference toohello Offline Cache Table</span></span>

<span data-ttu-id="4777e-358">Per una tabella online, si usa `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="4777e-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="4777e-359">Per una tabella offline, usare `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="4777e-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="4777e-360">Tutti hello metodi disponibili per le tabelle in linea (incluso il filtro, ordinamento, paging, inserimento di dati, l'aggiornamento dei dati e l'eliminazione dei dati) funzionano altrettanto bene in tabelle online e offline.</span><span class="sxs-lookup"><span data-stu-id="4777e-360">All hello methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-hello-local-offline-cache"></a><span data-ttu-id="4777e-361">Sincronizzare hello Cache Offline locale</span><span class="sxs-lookup"><span data-stu-id="4777e-361">Synchronize hello Local Offline Cache</span></span>

<span data-ttu-id="4777e-362">La sincronizzazione è all'interno di controllo di hello dell'app.</span><span class="sxs-lookup"><span data-stu-id="4777e-362">Synchronization is within hello control of your app.</span></span>  <span data-ttu-id="4777e-363">Ecco un esempio di metodo di sincronizzazione:</span><span class="sxs-lookup"><span data-stu-id="4777e-363">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="4777e-364">Se non viene fornito un nome di query toohello `.pull(query, queryname)` (metodo), la sincronizzazione incrementale è tooreturn utilizzati solo i record che sono stati creati o modificati dopo pull hello completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="4777e-364">If a query name is provided toohello `.pull(query, queryname)` method, then incremental sync is used tooreturn only records that have been created or changed since hello last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="4777e-365">Gestire i conflitti durante la sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="4777e-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="4777e-366">Se si verifica un conflitto durante un'operazione `.push()`, viene generata un'eccezione `MobileServiceConflictException`.</span><span class="sxs-lookup"><span data-stu-id="4777e-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="4777e-367">elemento rilasciato server Hello è incorporato nell'eccezione hello e possono essere recuperato tramite `.getItem()` eccezione hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-367">hello server-issued item is embedded in hello exception and can be retrieved by `.getItem()` on hello exception.</span></span>  <span data-ttu-id="4777e-368">Regolare il push di hello da parte del chiamante hello seguenti di elementi nell'oggetto MobileServiceSyncContext hello:</span><span class="sxs-lookup"><span data-stu-id="4777e-368">Adjust hello push by calling hello following items on hello MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="4777e-369">Dopo che tutti i conflitti sono contrassegnati come si desidera, chiamare `.push()` tooresolve nuovamente tutti i conflitti di hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-369">Once all conflicts are marked as you wish, call `.push()` again tooresolve all hello conflicts.</span></span>

## <span data-ttu-id="4777e-370"><a name="custom-api"></a>Chiamare un'API personalizzata</span><span class="sxs-lookup"><span data-stu-id="4777e-370"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="4777e-371">Un'API personalizzata consente toodefine endpoint personalizzati che espongono la funzionalità server che non eseguire il mapping delle insert tooan, aggiornare, eliminare o operazione di lettura.</span><span class="sxs-lookup"><span data-stu-id="4777e-371">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="4777e-372">L'utilizzo di un'API personalizzata offre maggiore controllo sulla messaggistica, incluse la lettura e l'impostazione delle intestazioni del messaggio HTTP e la definizione di un formato del corpo del messaggio diverso da JSON.</span><span class="sxs-lookup"><span data-stu-id="4777e-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="4777e-373">Da un client Android, si chiama hello **invokeApi** endpoint API personalizzata di metodo toocall hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-373">From an Android client, you call hello **invokeApi** method toocall hello custom API endpoint.</span></span> <span data-ttu-id="4777e-374">Hello esempio seguente viene illustrato come toocall un endpoint API denominati **completeAll**, che restituisce una classe collection denominata **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="4777e-374">hello following example shows how toocall an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="4777e-375">Hello **invokeApi** metodo viene chiamato nel client hello, che invia una richiesta di un POST toohello nuova API personalizzata.</span><span class="sxs-lookup"><span data-stu-id="4777e-375">hello **invokeApi** method is called on hello client, which sends a POST request toohello new custom API.</span></span> <span data-ttu-id="4777e-376">risultato Hello restituito dall'API personalizzata hello viene visualizzata nella finestra di messaggio, come errori.</span><span class="sxs-lookup"><span data-stu-id="4777e-376">hello result returned by hello custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="4777e-377">Altre versioni di **invokeApi** consentono l'invio di un oggetto nel corpo della richiesta hello facoltativamente, specificare il metodo HTTP hello e Invia parametri di query con richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-377">Other versions of **invokeApi** let you optionally send an object in hello request body, specify hello HTTP method, and send query parameters with hello request.</span></span> <span data-ttu-id="4777e-378">Vengono fornite anche versioni non tipizzate di **invokeApi** .</span><span class="sxs-lookup"><span data-stu-id="4777e-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="4777e-379"><a name="authentication"></a>Aggiungere app tooyour authentication</span><span class="sxs-lookup"><span data-stu-id="4777e-379"><a name="authentication"></a>Add authentication tooyour app</span></span>

<span data-ttu-id="4777e-380">Esercitazioni già descrivono in dettaglio come tooadd queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4777e-380">Tutorials already describe in detail how tooadd these features.</span></span>

<span data-ttu-id="4777e-381">Il servizio app supporta l'[autenticazione degli utenti di app](app-service-mobile-android-get-started-users.md) con diversi provider di identità esterni: Facebook, Google, account Microsoft, Twitter e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4777e-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="4777e-382">È possibile impostare le autorizzazioni di accesso toorestrict tabelle per operazioni specifiche tooonly autenticata users.</span><span class="sxs-lookup"><span data-stu-id="4777e-382">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="4777e-383">È inoltre possibile utilizzare identità hello gli utenti autenticati tooimplement delle regole di autorizzazione nel back-end.</span><span class="sxs-lookup"><span data-stu-id="4777e-383">You can also use hello identity of authenticated users tooimplement authorization rules in your backend.</span></span>

<span data-ttu-id="4777e-384">Sono supportati due flussi di autenticazione, ovvero un flusso **server** e un flusso **client**.</span><span class="sxs-lookup"><span data-stu-id="4777e-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="4777e-385">flusso di Hello server fornisce l'esperienza di autenticazione più semplice hello, come si basa sull'interfaccia web provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-385">hello server flow provides hello simplest authentication experience, as it relies on hello identity providers web interface.</span></span>  <span data-ttu-id="4777e-386">Nessun SDK aggiuntivo è l'autenticazione del server flusso di tooimplement obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="4777e-386">No additional SDKs are required tooimplement server flow authentication.</span></span> <span data-ttu-id="4777e-387">L'autenticazione del server del flusso non fornisce un'integrazione completa in dispositivi mobili hello ed è consigliata solo per la prova di scenari.</span><span class="sxs-lookup"><span data-stu-id="4777e-387">Server flow authentication does not provide a deep integration into hello mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="4777e-388">flusso di Hello client consente una maggiore integrazione con funzionalità specifiche del dispositivo, ad esempio accesso single sign-on di si basa sul SDK, fornito dal provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-388">hello client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by hello identity provider.</span></span>  <span data-ttu-id="4777e-389">Ad esempio, è possibile integrare hello Facebook SDK nell'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4777e-389">For example, you can integrate hello Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="4777e-390">client mobili Hello Scambia in app Facebook hello e conferma il sign-on prima di effettuare lo swapping tooyour indietro app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4777e-390">hello mobile client swaps into hello Facebook app and confirms your sign-on before swapping back tooyour mobile app.</span></span>

<span data-ttu-id="4777e-391">Quattro passaggi sono necessari tooenable autenticazione nell'app:</span><span class="sxs-lookup"><span data-stu-id="4777e-391">Four steps are required tooenable authentication in your app:</span></span>

* <span data-ttu-id="4777e-392">Registrare l'app per l'autenticazione con un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="4777e-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="4777e-393">Configurare il back-end del servizio app.</span><span class="sxs-lookup"><span data-stu-id="4777e-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="4777e-394">Limitare gli utenti tooauthenticated le autorizzazioni di tabella solo in hello back-end del servizio App.</span><span class="sxs-lookup"><span data-stu-id="4777e-394">Restrict table permissions tooauthenticated users only on hello App Service backend.</span></span>
* <span data-ttu-id="4777e-395">Aggiungere app tooyour codice di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4777e-395">Add authentication code tooyour app.</span></span>

<span data-ttu-id="4777e-396">È possibile impostare le autorizzazioni di accesso toorestrict tabelle per operazioni specifiche tooonly autenticata users.</span><span class="sxs-lookup"><span data-stu-id="4777e-396">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="4777e-397">È inoltre possibile utilizzare hello SID di un utente autenticato di toomodify richieste.</span><span class="sxs-lookup"><span data-stu-id="4777e-397">You can also use hello SID of an authenticated user toomodify requests.</span></span>  <span data-ttu-id="4777e-398">Per altre informazioni, vedere [Introduzione all'autenticazione] e documentazione Server SDK HOWTO hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-398">For more information, review [Get started with authentication] and hello Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="4777e-399"><a name="caching"></a>Autenticazione: flusso server</span><span class="sxs-lookup"><span data-stu-id="4777e-399"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="4777e-400">Hello codice seguente avvia un processo di accesso server flusso usando il provider di Google hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-400">hello following code starts a server flow login process using hello Google provider.</span></span>  <span data-ttu-id="4777e-401">Configurazione aggiuntiva è necessario a causa dei requisiti di sicurezza hello per provider di Google hello:</span><span class="sxs-lookup"><span data-stu-id="4777e-401">Additional configuration is required because of hello security requirements for hello Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="4777e-402">Inoltre, aggiungere hello seguente classe di attività metodo toohello principale:</span><span class="sxs-lookup"><span data-stu-id="4777e-402">In addition, add hello following method toohello main Activity class:</span></span>

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="4777e-403">Hello `GOOGLE_LOGIN_REQUEST_CODE` definito in principale attività viene utilizzata per hello `login()` (metodo) e all'interno di hello `onActivityResult()` metodo.</span><span class="sxs-lookup"><span data-stu-id="4777e-403">hello `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for hello `login()` method and within hello `onActivityResult()` method.</span></span>  <span data-ttu-id="4777e-404">È possibile scegliere qualsiasi numero univoco, purché hello stesso numero viene utilizzato all'interno di hello `login()` metodo e hello `onActivityResult()` metodo.</span><span class="sxs-lookup"><span data-stu-id="4777e-404">You can choose any unique number, as long as hello same number is used within hello `login()` method and hello `onActivityResult()` method.</span></span>  <span data-ttu-id="4777e-405">Se il codice client hello astratta in una scheda di servizio (come illustrato in precedenza), è necessario chiamare i metodi appropriati hello nella scheda servizio hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-405">If you abstract hello client code into a service adapter (as shown earlier), you should call hello appropriate methods on hello service adapter.</span></span>

<span data-ttu-id="4777e-406">È inoltre necessario progetto hello tooconfigure per customtabs.</span><span class="sxs-lookup"><span data-stu-id="4777e-406">You also need tooconfigure hello project for customtabs.</span></span>  <span data-ttu-id="4777e-407">Specificare prima di tutto un URL di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="4777e-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="4777e-408">Aggiungere hello seguente frammento di codice troppo`AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="4777e-408">Add hello following snippet too`AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="4777e-409">Aggiungere hello **redirectUriScheme** toohello `build.gradle` file dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="4777e-409">Add hello **redirectUriScheme** toohello `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="4777e-410">Infine, aggiungere `com.android.support:customtabs:23.0.1` toohello elenco di dipendenze in hello `build.gradle` file:</span><span class="sxs-lookup"><span data-stu-id="4777e-410">Finally, add `com.android.support:customtabs:23.0.1` toohello dependencies list in hello `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="4777e-411">Ottenere ID hello di hello utente connesso da un **MobileServiceUser** utilizzando hello **Recuperaidutente** metodo.</span><span class="sxs-lookup"><span data-stu-id="4777e-411">Obtain hello ID of hello logged-in user from a **MobileServiceUser** using hello **getUserId** method.</span></span> <span data-ttu-id="4777e-412">Per un esempio di come toouse ritardo toocall hello asincrona accesso API, vedere [Introduzione all'autenticazione].</span><span class="sxs-lookup"><span data-stu-id="4777e-412">For an example of how toouse Futures toocall hello asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="4777e-413">lo schema dell'URL indicato Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="4777e-413">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="4777e-414">Assicurarsi che tutte le occorrenze di `{url_scheme_of_you_app}` rispettino questa distinzione.</span><span class="sxs-lookup"><span data-stu-id="4777e-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="4777e-415"><a name="caching"></a>Memorizzare nella cache i token di autenticazione</span><span class="sxs-lookup"><span data-stu-id="4777e-415"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="4777e-416">La memorizzazione nella cache i token di autenticazione richiede toostore hello ID utente e token di autenticazione in locale nel dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-416">Caching authentication tokens requires you toostore hello User ID and authentication token locally on hello device.</span></span> <span data-ttu-id="4777e-417">Hello prossimo avvio dell'applicazione hello, controllo della cache di hello e, se questi valori sono presenti, è possibile ignorare log hello nella procedura e riattivare i client hello con questi dati.</span><span class="sxs-lookup"><span data-stu-id="4777e-417">hello next time hello app starts, you check hello cache, and if these values are present, you can skip hello log in procedure and rehydrate hello client with this data.</span></span> <span data-ttu-id="4777e-418">Tuttavia questi dati sono riservati e devono essere archiviato crittografati per garantire la protezione in caso di furto di un telefono hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-418">However this data is sensitive, and it should be stored encrypted for safety in case hello phone gets stolen.</span></span>  <span data-ttu-id="4777e-419">È possibile visualizzare un esempio completo di come token di autenticazione toocache in [Cache sezione token di autenticazione][7].</span><span class="sxs-lookup"><span data-stu-id="4777e-419">You can see a complete example of how toocache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="4777e-420">Quando si tenta di toouse un token scaduto, viene visualizzato un *401 non autorizzato* risposta.</span><span class="sxs-lookup"><span data-stu-id="4777e-420">When you try toouse an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="4777e-421">È possibile gestire gli errori di autenticazione tramite i filtri.</span><span class="sxs-lookup"><span data-stu-id="4777e-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="4777e-422">I filtri intercettano richieste toohello back-end del servizio App.</span><span class="sxs-lookup"><span data-stu-id="4777e-422">Filters intercept requests toohello App Service backend.</span></span> <span data-ttu-id="4777e-423">il codice del filtro Hello verifica risposta hello per 401, trigger di processo di accesso hello e quindi riprende richiesta hello che ha generato hello 401.</span><span class="sxs-lookup"><span data-stu-id="4777e-423">hello filter code tests hello response for a 401, triggers hello sign-in process, and then resumes hello request that generated hello 401.</span></span>

### <span data-ttu-id="4777e-424"><a name="refresh"></a>Usare i token di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="4777e-424"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="4777e-425">token di Hello restituito da Azure App Service autenticazione e autorizzazione ha una durata definita di un'ora.</span><span class="sxs-lookup"><span data-stu-id="4777e-425">hello token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="4777e-426">Dopo questo periodo, è necessario ripetere l'autenticazione utente hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-426">After this period, you must reauthenticate hello user.</span></span>  <span data-ttu-id="4777e-427">Se si utilizzando un token di lunga durato che si è ricevuto tramite l'autenticazione client per il flusso, quindi è possibile ripetere l'autenticazione con l'autenticazione del servizio App di Azure e le autorizzazioni mediante hello stesso token.</span><span class="sxs-lookup"><span data-stu-id="4777e-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using hello same token.</span></span>  <span data-ttu-id="4777e-428">Viene generato un altro token del servizio app di Azure con una nuova durata.</span><span class="sxs-lookup"><span data-stu-id="4777e-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="4777e-429">È anche possibile registrare hello provider toouse i token di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4777e-429">You can also register hello provider toouse Refresh Tokens.</span></span>  <span data-ttu-id="4777e-430">Un token di aggiornamento non è sempre disponibile.</span><span class="sxs-lookup"><span data-stu-id="4777e-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="4777e-431">È necessaria una configurazione aggiuntiva:</span><span class="sxs-lookup"><span data-stu-id="4777e-431">Additional configuration is required:</span></span>

* <span data-ttu-id="4777e-432">Per **Azure Active Directory**, configurare un segreto client per hello App di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4777e-432">For **Azure Active Directory**, configure a client secret for hello Azure Active Directory App.</span></span>  <span data-ttu-id="4777e-433">Specificare la chiave privata client hello in hello Azure App Service quando si configura l'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4777e-433">Specify hello client secret in hello Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="4777e-434">Quando si chiama `.login()`, passare `response_type=code id_token` come parametro:</span><span class="sxs-lookup"><span data-stu-id="4777e-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="4777e-435">Per **Google**, passare hello `access_type=offline` come parametro:</span><span class="sxs-lookup"><span data-stu-id="4777e-435">For **Google**, pass hello `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="4777e-436">Per **Account Microsoft**selezionare hello `wl.offline_access` ambito.</span><span class="sxs-lookup"><span data-stu-id="4777e-436">For **Microsoft Account**, select hello `wl.offline_access` scope.</span></span>

<span data-ttu-id="4777e-437">toorefresh un token, chiamare `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="4777e-437">toorefresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="4777e-438">Come procedura consigliata, creare un filtro che rileva una risposta dal server hello 401 e tenta di token dell'utente toorefresh hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-438">As a best practice, create a filter that detects a 401 response from hello server and tries toorefresh hello user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="4777e-439">Accedere con l'autenticazione basata sul flusso client</span><span class="sxs-lookup"><span data-stu-id="4777e-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="4777e-440">processo generale di Hello per l'accesso con autenticazione di client per il flusso è come segue:</span><span class="sxs-lookup"><span data-stu-id="4777e-440">hello general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="4777e-441">Configurare l'autenticazione e l'autorizzazione del servizio app di Azure come si configura l'autenticazione basata sul flusso server.</span><span class="sxs-lookup"><span data-stu-id="4777e-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="4777e-442">Integrare il provider di autenticazione hello SDK per l'autenticazione tooproduce un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="4777e-442">Integrate hello authentication provider SDK for authentication tooproduce an access token.</span></span>
* <span data-ttu-id="4777e-443">Chiamare hello `.login()` metodo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4777e-443">Call hello `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="4777e-444">Sostituire hello `onSuccess()` (metodo) con qualsiasi tipo di codice si desidera toouse un account di accesso ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="4777e-444">Replace hello `onSuccess()` method with whatever code you wish toouse on a successful login.</span></span>  <span data-ttu-id="4777e-445">Hello `{provider}` stringa è un provider valido: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, o **twitter**.</span><span class="sxs-lookup"><span data-stu-id="4777e-445">hello `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="4777e-446">Se è stato implementato l'autenticazione personalizzata, è possibile utilizzare tag di provider di autenticazione personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-446">If you have implemented custom authentication, then you can also use hello custom authentication provider tag.</span></span>

### <span data-ttu-id="4777e-447"><a name="adal"></a>Autenticare gli utenti con hello Active Directory Authentication Library (ADAL)</span><span class="sxs-lookup"><span data-stu-id="4777e-447"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="4777e-448">È possibile utilizzare gli utenti toosign di Active Directory Authentication Library (ADAL) hello in un'applicazione tramite Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4777e-448">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="4777e-449">Utilizzando un account di accesso client del flusso è spesso preferibile toousing hello `loginAsync()` metodi che fornisce un'idea dell'esperienza utente più nativa e consente un'ulteriore personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="4777e-449">Using a client flow login is often preferable toousing hello `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="4777e-450">Configurare il back-end dell'app mobile per l'accesso AAD hello seguente [come tooconfigure App del servizio per l'account di accesso Active Directory] [ 22] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4777e-450">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="4777e-451">Verificare che passaggio facoltativo in hello toocomplete di registrazione di un'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="4777e-451">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="4777e-452">Installare ADAL modificando il hello tooinclude del file gradle seguenti definizioni:</span><span class="sxs-lookup"><span data-stu-id="4777e-452">Install ADAL by modifying your build.gradle file tooinclude hello following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="4777e-453">Aggiungere hello seguito codice tooyour applicazione, rendendo hello seguenti sostituzioni:</span><span class="sxs-lookup"><span data-stu-id="4777e-453">Add hello following code tooyour application, making hello following replacements:</span></span>

* <span data-ttu-id="4777e-454">Sostituire **INSERT-autorità-qui** con nome hello del tenant di hello in cui è stato eseguito il provisioning dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4777e-454">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="4777e-455">formato di Hello deve essere https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="4777e-455">hello format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="4777e-456">Sostituire **INSERT-RESOURCE-ID-qui** con hello client ID per il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4777e-456">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="4777e-457">È possibile ottenere l'ID client hello da hello **avanzate** scheda **impostazioni di Azure Active Directory** nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-457">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
* <span data-ttu-id="4777e-458">Sostituire **INSERT-CLIENT-ID-qui** con ID client hello copiato dall'applicazione client nativa hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-458">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
* <span data-ttu-id="4777e-459">Sostituire **INSERT-REDIRECT-URI-qui** con il sito */.auth/login/done* endpoint, utilizzando lo schema HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="4777e-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="4777e-460">Questo valore dovrebbe essere simile troppo*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="4777e-460">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="4777e-461"><a name="filters"></a>Regolare hello comunicazione tra Client e Server</span><span class="sxs-lookup"><span data-stu-id="4777e-461"><a name="filters"></a>Adjust hello Client-Server Communication</span></span>

<span data-ttu-id="4777e-462">Hello connessione Client è in genere una connessione HTTP di base utilizzando hello sottostante libreria HTTP fornita con hello Android SDK.</span><span class="sxs-lookup"><span data-stu-id="4777e-462">hello Client connection is normally a basic HTTP connection using hello underlying HTTP library supplied with hello Android SDK.</span></span>  <span data-ttu-id="4777e-463">Esistono diversi motivi per cui si toochange che:</span><span class="sxs-lookup"><span data-stu-id="4777e-463">There are several reasons why you would want toochange that:</span></span>

* <span data-ttu-id="4777e-464">Si desidera toouse un timeout di tooadjust libreria HTTP alternativo.</span><span class="sxs-lookup"><span data-stu-id="4777e-464">You wish toouse an alternate HTTP library tooadjust timeouts.</span></span>
* <span data-ttu-id="4777e-465">Si desidera tooprovide un indicatore di stato.</span><span class="sxs-lookup"><span data-stu-id="4777e-465">You wish tooprovide a progress bar.</span></span>
* <span data-ttu-id="4777e-466">Si desidera tooadd una funzionalità di gestione API toosupport intestazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="4777e-466">You wish tooadd a custom header toosupport API management functionality.</span></span>
* <span data-ttu-id="4777e-467">Si desidera toointercept una risposta non riuscita in modo che è possibile implementare la riautenticazione.</span><span class="sxs-lookup"><span data-stu-id="4777e-467">You wish toointercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="4777e-468">Si desidera che il servizio analitica tooan di toolog back-end le richieste.</span><span class="sxs-lookup"><span data-stu-id="4777e-468">You wish toolog backend requests tooan analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="4777e-469">Uso di una libreria HTTP alternativa</span><span class="sxs-lookup"><span data-stu-id="4777e-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="4777e-470">Chiamare hello `.setAndroidHttpClientFactory()` metodo subito dopo la creazione del riferimento del client.</span><span class="sxs-lookup"><span data-stu-id="4777e-470">Call hello `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="4777e-471">Ad esempio, tooset hello connection timeout too60 secondi (anziché hello impostazione predefinita 10 secondi):</span><span class="sxs-lookup"><span data-stu-id="4777e-471">For example, tooset hello connection timeout too60 seconds (instead of hello default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="4777e-472">Implementare un filtro per l'avanzamento</span><span class="sxs-lookup"><span data-stu-id="4777e-472">Implement a Progress Filter</span></span>

<span data-ttu-id="4777e-473">È possibile implementare un intercettazione di ogni richiesta implementando `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="4777e-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="4777e-474">Ad esempio, l'esempio hello aggiorna un indicatore di stato creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="4777e-474">For example, hello following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="4777e-475">È possibile collegare questo client toohello filtro come segue:</span><span class="sxs-lookup"><span data-stu-id="4777e-475">You can attach this filter toohello client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="4777e-476">Personalizzare le intestazioni delle richieste</span><span class="sxs-lookup"><span data-stu-id="4777e-476">Customize Request Headers</span></span>

<span data-ttu-id="4777e-477">Utilizzare la seguente hello `ServiceFilter` e allegare il filtro hello in hello esattamente come hello `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="4777e-477">Use hello following `ServiceFilter` and attach hello filter in hello same way as hello `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="4777e-478"><a name="conversions"></a>Configurare la serializzazione automatica</span><span class="sxs-lookup"><span data-stu-id="4777e-478"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="4777e-479">È possibile specificare una strategia di conversione che si applica a colonna tooevery utilizzando hello [gson] [ 3] API.</span><span class="sxs-lookup"><span data-stu-id="4777e-479">You can specify a conversion strategy that applies tooevery column by using hello [gson][3] API.</span></span> <span data-ttu-id="4777e-480">libreria client per Android Hello Usa [gson] [ 3] background hello tooserialize Java gli oggetti dati tooJSON prima dell'invio dei dati hello tooAzure servizio App.</span><span class="sxs-lookup"><span data-stu-id="4777e-480">hello Android client library uses [gson][3] behind hello scenes tooserialize Java objects tooJSON data before hello data is sent tooAzure App Service.</span></span>  <span data-ttu-id="4777e-481">il codice seguente Hello Usa hello **setFieldNamingStrategy()** strategia hello tooset di metodo.</span><span class="sxs-lookup"><span data-stu-id="4777e-481">hello following code uses hello **setFieldNamingStrategy()** method tooset hello strategy.</span></span> <span data-ttu-id="4777e-482">In questo esempio verrà eliminato il carattere iniziale di hello (una "m") e successivo carattere minuscoli hello, per ogni nome di campo.</span><span class="sxs-lookup"><span data-stu-id="4777e-482">This example will delete hello initial character (an "m"), and then lower-case hello next character, for every field name.</span></span> <span data-ttu-id="4777e-483">ad esempio, trasforma "mId" in "id".</span><span class="sxs-lookup"><span data-stu-id="4777e-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="4777e-484">Implementare un hello tooreduce strategia di conversione necessaria per `SerializedName()` annotazioni nella maggior parte dei campi.</span><span class="sxs-lookup"><span data-stu-id="4777e-484">Implement a conversion strategy tooreduce hello need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="4777e-485">Questo codice deve essere eseguito prima di creare un riferimento di client per dispositivi mobili usando hello **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="4777e-485">This code must be executed before creating a mobile client reference using hello **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[Introduzione all'autenticazione]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
