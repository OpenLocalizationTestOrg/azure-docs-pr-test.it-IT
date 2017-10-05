---
title: Come usare Azure Mobile Apps SDK per Android | Microsoft Docs
description: Come usare Azure Mobile Apps SDK per Android
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
ms.openlocfilehash: 4b15d024ca6d5bbafe83d321a64021aecd78c4a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="996fc-103">Come usare Azure Mobile Apps SDK per Android</span><span class="sxs-lookup"><span data-stu-id="996fc-103">How to use the Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="996fc-104">Questa guida illustra come usare Android SDK del client per le App per dispositivi mobili di Azure per implementare scenari comuni, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="996fc-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span></span>

* <span data-ttu-id="996fc-105">L'esecuzione di query sui dati, come inserimento, aggiornamento ed eliminazione.</span><span class="sxs-lookup"><span data-stu-id="996fc-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="996fc-106">L'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="996fc-106">Authentication.</span></span>
* <span data-ttu-id="996fc-107">La gestione degli errori.</span><span class="sxs-lookup"><span data-stu-id="996fc-107">Handling errors.</span></span>
* <span data-ttu-id="996fc-108">La personalizzazione del client.</span><span class="sxs-lookup"><span data-stu-id="996fc-108">Customizing the client.</span></span>

<span data-ttu-id="996fc-109">Questa guida descrive Android SDK lato client.</span><span class="sxs-lookup"><span data-stu-id="996fc-109">This guide focuses on the client-side Android SDK.</span></span>  <span data-ttu-id="996fc-110">Per altre informazioni sugli SDK lato server per le app per dispositivi mobili, vedere [Usare l'SDK del server back-end .NET][10] o [Come usare Node.js SDK back-end][11].</span><span class="sxs-lookup"><span data-stu-id="996fc-110">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="996fc-111">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="996fc-111">Reference Documentation</span></span>

<span data-ttu-id="996fc-112">È possibile trovare il [riferimento API Javadocs][12] per la libreria client Android in GitHub.</span><span class="sxs-lookup"><span data-stu-id="996fc-112">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="996fc-113">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="996fc-113">Supported Platforms</span></span>

<span data-ttu-id="996fc-114">Azure Mobile Apps SDK per Android supporta API di livello da 19 a 24 (da KitKat a Nougat) per i fattori di forma di telefoni e tablet.</span><span class="sxs-lookup"><span data-stu-id="996fc-114">The Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="996fc-115">L'autenticazione in particolare utilizza un approccio comune ai framework Web per raccogliere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="996fc-115">Authentication, in particular, utilizes a common web framework approach to gather credentials.</span></span>  <span data-ttu-id="996fc-116">L'autenticazione basata sul flusso server non funziona con dispositivi con fattore di forma piccolo, ad esempio gli orologi.</span><span class="sxs-lookup"><span data-stu-id="996fc-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="996fc-117">Installazione e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="996fc-117">Setup and Prerequisites</span></span>

<span data-ttu-id="996fc-118">Completare l' [esercitazione introduttiva sulle App per dispositivi mobili di Azure](app-service-mobile-android-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="996fc-118">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="996fc-119">Questa attività garantisce che vengano soddisfatti tutti i prerequisiti per lo sviluppo di App per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="996fc-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="996fc-120">L'esercitazione introduttiva è utile per configurare il proprio account e creare il primo back-end per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="996fc-120">The Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="996fc-121">Se si decide di non completare l'esercitazione introduttiva, completare le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="996fc-121">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span></span>

* <span data-ttu-id="996fc-122">[creare un back-end dell'app per dispositivi mobili][13] da usare con l'app Android.</span><span class="sxs-lookup"><span data-stu-id="996fc-122">[create a Mobile App backend][13] to use with your Android app.</span></span>
* <span data-ttu-id="996fc-123">In Android Studio [aggiornare i file di compilazione Gradle](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="996fc-123">In Android Studio, [update the Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="996fc-124">[Abilitare l'autorizzazione per Internet](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="996fc-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="996fc-125"><a name="gradle-build"></a>Aggiornare il file di compilazione Gradle</span><span class="sxs-lookup"><span data-stu-id="996fc-125"><a name="gradle-build"></a>Update the Gradle build file</span></span>

<span data-ttu-id="996fc-126">Modificare entrambi i file **build.gradle** :</span><span class="sxs-lookup"><span data-stu-id="996fc-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="996fc-127">Aggiungere il codice seguente al livello *Project* del file **build.gradle** all'interno del tag *buildscript*:</span><span class="sxs-lookup"><span data-stu-id="996fc-127">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="996fc-128">Aggiungere il codice seguente al livello *Module app* del file **build.gradle** all'interno del tag *dependencies*:</span><span class="sxs-lookup"><span data-stu-id="996fc-128">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="996fc-129">La versione più recente è la 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="996fc-129">Currently the latest version is 3.3.0.</span></span> <span data-ttu-id="996fc-130">Le versioni supportate sono elencate [su bintray][14].</span><span class="sxs-lookup"><span data-stu-id="996fc-130">The supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="996fc-131"><a name="enable-internet"></a>Abilitare l'autorizzazione per Internet</span><span class="sxs-lookup"><span data-stu-id="996fc-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="996fc-132">Per accedere ad Azure, è necessario abilitare l'autorizzazione INTERNET per l'app.</span><span class="sxs-lookup"><span data-stu-id="996fc-132">To access Azure, your app must have the INTERNET permission enabled.</span></span> <span data-ttu-id="996fc-133">Se non è già abilitata, aggiungere la riga di codice seguente al file **AndroidManifest.xml** :</span><span class="sxs-lookup"><span data-stu-id="996fc-133">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="996fc-134">Creare una connessione client</span><span class="sxs-lookup"><span data-stu-id="996fc-134">Create a Client Connection</span></span>

<span data-ttu-id="996fc-135">App per dispositivi mobili di Azure fornisce quattro funzioni all'applicazione per dispositivi mobili:</span><span class="sxs-lookup"><span data-stu-id="996fc-135">Azure Mobile Apps provides four functions to your mobile application:</span></span>

* <span data-ttu-id="996fc-136">Accesso ai dati e sincronizzazione offline con un servizio di App per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="996fc-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="996fc-137">Chiamata ad API personalizzate scritte con Azure Mobile Apps Server SDK.</span><span class="sxs-lookup"><span data-stu-id="996fc-137">Call Custom APIs written with the Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="996fc-138">Autenticazione con autenticazione e autorizzazione nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="996fc-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="996fc-139">Registrazione di notifiche push con Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="996fc-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="996fc-140">Per ogni funzione prima di tutto è necessario creare un oggetto `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="996fc-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="996fc-141">È consigliabile creare un solo oggetto `MobileServiceClient` nel client per dispositivi mobili, ovvero il modello deve essere singleton.</span><span class="sxs-lookup"><span data-stu-id="996fc-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="996fc-142">Per creare un oggetto `MobileServiceClient`:</span><span class="sxs-lookup"><span data-stu-id="996fc-142">To create a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with the Site URL
    this);                  // Your application Context
```

<span data-ttu-id="996fc-143">`<MobileAppUrl>` è una stringa o un oggetto URL che punta al back-end per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="996fc-143">The `<MobileAppUrl>` is either a string or a URL object that points to your mobile backend.</span></span>  <span data-ttu-id="996fc-144">Se si usa il servizio app di Azure per ospitare il back-end per dispositivi mobili, verificare di usare la versione `https://` sicura dell'URL.</span><span class="sxs-lookup"><span data-stu-id="996fc-144">If you are using Azure App Service to host your mobile backend, then ensure you use the secure `https://` version of the URL.</span></span>

<span data-ttu-id="996fc-145">Per il client è anche necessario l'accesso all'attività o al contesto (il parametro `this` nell'esempio).</span><span class="sxs-lookup"><span data-stu-id="996fc-145">The client also requires access to the Activity or Context - the `this` parameter in the example.</span></span>  <span data-ttu-id="996fc-146">La costruzione MobileServiceClient deve avvenire nel metodo `onCreate()` dell'attività a cui si fa riferimento nel file `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="996fc-146">The MobileServiceClient construction should happen within the `onCreate()` method of the Activity referenced in the `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="996fc-147">Come procedura consigliata, è opportuno astrarre le comunicazioni del server nella relativa classe (modello singleton).</span><span class="sxs-lookup"><span data-stu-id="996fc-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="996fc-148">In questo caso, è consigliabile passare l'attività nel costruttore per configurare il servizio in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="996fc-148">In this case, you should pass the Activity within the constructor to appropriately configure the service.</span></span>  <span data-ttu-id="996fc-149">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="996fc-149">For example:</span></span>

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

<span data-ttu-id="996fc-150">È ora possibile chiamare `AzureServiceAdapter.Initialize(this);` nel metodo `onCreate()` dell'attività principale.</span><span class="sxs-lookup"><span data-stu-id="996fc-150">You can now call `AzureServiceAdapter.Initialize(this);` in the `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="996fc-151">Tutti gli altri metodi che hanno necessità di accedere al client usano `AzureServiceAdapter.getInstance();` per ottenere un riferimento all'adattatore del servizio.</span><span class="sxs-lookup"><span data-stu-id="996fc-151">Any other methods needing access to the client use `AzureServiceAdapter.getInstance();` to obtain a reference to the service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="996fc-152">Operazioni dati</span><span class="sxs-lookup"><span data-stu-id="996fc-152">Data Operations</span></span>

<span data-ttu-id="996fc-153">Azure Mobile Apps SDK fondamentalmente fornisce accesso ai dati archiviati in SQL Azure nel back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="996fc-153">The core of the Azure Mobile Apps SDK is to provide access to data stored within SQL Azure on the Mobile App backend.</span></span>  <span data-ttu-id="996fc-154">È possibile accedere a questi dati usando classi fortemente tipizzate (preferibile) o query non tipizzate (non consigliato).</span><span class="sxs-lookup"><span data-stu-id="996fc-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="996fc-155">La maggior parte di questa sezione illustra l'uso di classi fortemente tipizzate.</span><span class="sxs-lookup"><span data-stu-id="996fc-155">The bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="996fc-156">Definire le classi di dati client</span><span class="sxs-lookup"><span data-stu-id="996fc-156">Define client data classes</span></span>

<span data-ttu-id="996fc-157">Per accedere ai dati dalle tabelle di SQL Azure, definire le classi di dati client che corrispondono alle tabelle nel back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="996fc-157">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span></span> <span data-ttu-id="996fc-158">Negli esempi di questo argomento si presuppone l'uso di una tabella denominata **MyDataTable** con le colonne seguenti:</span><span class="sxs-lookup"><span data-stu-id="996fc-158">Examples in this topic assume a table named **MyDataTable**, which has the following columns:</span></span>

* <span data-ttu-id="996fc-159">id</span><span class="sxs-lookup"><span data-stu-id="996fc-159">id</span></span>
* <span data-ttu-id="996fc-160">text</span><span class="sxs-lookup"><span data-stu-id="996fc-160">text</span></span>
* <span data-ttu-id="996fc-161">complete</span><span class="sxs-lookup"><span data-stu-id="996fc-161">complete</span></span>

<span data-ttu-id="996fc-162">L'oggetto lato client tipizzato corrispondente si trova in un file denominato **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="996fc-162">The corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="996fc-163">Aggiungere i metodi getter e setter per ogni campo aggiunto.</span><span class="sxs-lookup"><span data-stu-id="996fc-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="996fc-164">Se la propria tabella di SQL Azure include più colonne, aggiungere i campi corrispondenti a questa classe.</span><span class="sxs-lookup"><span data-stu-id="996fc-164">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span></span>  <span data-ttu-id="996fc-165">Se ad esempio l'oggetto di trasferimento dati (DTO) include una colonna Priority di tipo Integer, è consigliabile aggiungere questo campo insieme ai relativi metodi getter e setter:</span><span class="sxs-lookup"><span data-stu-id="996fc-165">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns the item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets the item priority
*
* @param priority
*            priority to set
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="996fc-166">Per informazioni su come creare altre tabelle nel back-end delle app per dispositivi mobili, vedere [Procedura: Definire un controller tabelle][15] (back-end .NET) o [Procedura: Definire le tabelle con uno schema dinamico][16] (back-end Node.js).</span><span class="sxs-lookup"><span data-stu-id="996fc-166">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="996fc-167">Una tabella del back-end di App per dispositivi mobili di Azure definisce cinque campi speciali, quattro dei quali disponibili per i client:</span><span class="sxs-lookup"><span data-stu-id="996fc-167">An Azure Mobile Apps backend table defines five special fields, four of which are available to clients:</span></span>

* <span data-ttu-id="996fc-168">`String id`: ID univoco globale per il record.</span><span class="sxs-lookup"><span data-stu-id="996fc-168">`String id`: The globally unique ID for the record.</span></span>  <span data-ttu-id="996fc-169">Come procedura consigliata, impostare l'ID come rappresentazione di stringa di un oggetto [UUID][17].</span><span class="sxs-lookup"><span data-stu-id="996fc-169">As a best practice, make the id the String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="996fc-170">`DateTimeOffset updatedAt`: data/ora dell'ultimo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="996fc-170">`DateTimeOffset updatedAt`: The date/time of the last update.</span></span>  <span data-ttu-id="996fc-171">Il campo updatedAt viene impostato dal server e non deve mai essere impostato dal codice client.</span><span class="sxs-lookup"><span data-stu-id="996fc-171">The updatedAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="996fc-172">`DateTimeOffset createdAt`: data/ora di creazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="996fc-172">`DateTimeOffset createdAt`: The date/time that the object was created.</span></span>  <span data-ttu-id="996fc-173">Il campo createdAt viene impostato dal server e non deve mai essere impostato dal codice client.</span><span class="sxs-lookup"><span data-stu-id="996fc-173">The createdAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="996fc-174">`byte[] version`: rappresentata in genere come stringa, anche la versione viene impostata dal server.</span><span class="sxs-lookup"><span data-stu-id="996fc-174">`byte[] version`: Normally represented as a string, the version is also set by the server.</span></span>
* <span data-ttu-id="996fc-175">`boolean deleted`: indica che il record è stato eliminato, ma non ancora definitivamente.</span><span class="sxs-lookup"><span data-stu-id="996fc-175">`boolean deleted`: Indicates that the record has been deleted but not purged yet.</span></span>  <span data-ttu-id="996fc-176">Non usare `deleted` come proprietà nella classe.</span><span class="sxs-lookup"><span data-stu-id="996fc-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="996fc-177">Il campo `id` è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="996fc-177">The `id` field is required.</span></span>  <span data-ttu-id="996fc-178">I campi `updatedAt` e `version` vengono usati per la sincronizzazione offline, rispettivamente per la sincronizzazione incrementale e per la risoluzione dei conflitti.</span><span class="sxs-lookup"><span data-stu-id="996fc-178">The `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="996fc-179">Il campo `createdAt` è un campo di riferimento e non viene usato dal client.</span><span class="sxs-lookup"><span data-stu-id="996fc-179">The `createdAt` field is a reference field and is not used by the client.</span></span>  <span data-ttu-id="996fc-180">I nomi sono nomi delle proprietà usati per la trasmissione in rete e non sono modificabili.</span><span class="sxs-lookup"><span data-stu-id="996fc-180">The names are "across-the-wire" names of the properties and are not adjustable.</span></span>  <span data-ttu-id="996fc-181">È tuttavia possibile creare un mapping tra l'oggetto e tali nomi usando la libreria [gson][3].</span><span class="sxs-lookup"><span data-stu-id="996fc-181">However, you can create a mapping between your object and the "across-the-wire" names using the [gson][3] library.</span></span>  <span data-ttu-id="996fc-182">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="996fc-182">For example:</span></span>

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

### <a name="create-a-table-reference"></a><span data-ttu-id="996fc-183">Creare un riferimento alla tabella</span><span class="sxs-lookup"><span data-stu-id="996fc-183">Create a Table Reference</span></span>

<span data-ttu-id="996fc-184">Per accedere a una tabella, creare prima di tutto un oggetto [MobileServiceTable][8] chiamando il metodo **getTable** su [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="996fc-184">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span></span>  <span data-ttu-id="996fc-185">Questo metodo presenta due overload:</span><span class="sxs-lookup"><span data-stu-id="996fc-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="996fc-186">Nel codice seguente **mClient** è un riferimento all'oggetto MobileServiceClient.</span><span class="sxs-lookup"><span data-stu-id="996fc-186">In the following code, **mClient** is a reference to your MobileServiceClient object.</span></span>  <span data-ttu-id="996fc-187">Il primo overload viene usato quando il nome della classe e il nome della tabella sono identici ed è quello usato nella guida introduttiva:</span><span class="sxs-lookup"><span data-stu-id="996fc-187">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="996fc-188">Il secondo overload viene usato quando il nome della tabella è diverso da quello della classe: il primo parametro è il nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="996fc-188">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="996fc-189"><a name="query"></a>Eseguire una query su una tabella del back-end</span><span class="sxs-lookup"><span data-stu-id="996fc-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="996fc-190">Ottenere prima di tutto un riferimento alla tabella.</span><span class="sxs-lookup"><span data-stu-id="996fc-190">First, obtain a table reference.</span></span>  <span data-ttu-id="996fc-191">Eseguire quindi una query sul riferimento alla tabella.</span><span class="sxs-lookup"><span data-stu-id="996fc-191">Then execute a query on the table reference.</span></span>  <span data-ttu-id="996fc-192">Una query è qualsiasi combinazione di:</span><span class="sxs-lookup"><span data-stu-id="996fc-192">A query is any combination of:</span></span>

* <span data-ttu-id="996fc-193">Una [clausola di filtro](#filtering) `.where()`.</span><span class="sxs-lookup"><span data-stu-id="996fc-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="996fc-194">Una [clausola di ordinamento](#sorting) `.orderBy()`.</span><span class="sxs-lookup"><span data-stu-id="996fc-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="996fc-195">Una [clausola di selezione campo](#selection) `.select()`.</span><span class="sxs-lookup"><span data-stu-id="996fc-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="996fc-196">`.skip()` e `.top()` per i [risultati di paging](#paging).</span><span class="sxs-lookup"><span data-stu-id="996fc-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="996fc-197">Le clausole devono essere presentate nell'ordine precedente.</span><span class="sxs-lookup"><span data-stu-id="996fc-197">The clauses must be presented in the preceding order.</span></span>

### <span data-ttu-id="996fc-198"><a name="filter"></a> Applicazione di filtri ai risultati</span><span class="sxs-lookup"><span data-stu-id="996fc-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="996fc-199">Il formato generale di una query è:</span><span class="sxs-lookup"><span data-stu-id="996fc-199">The general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts the async into a sync result
```

<span data-ttu-id="996fc-200">L'esempio precedente restituisce tutti i risultati, fino alle dimensioni di pagina massime impostate dal server.</span><span class="sxs-lookup"><span data-stu-id="996fc-200">The preceding example returns all results (up to the maximum page size set by the server).</span></span>  <span data-ttu-id="996fc-201">Il metodo `.execute()` esegue la query sul back-end.</span><span class="sxs-lookup"><span data-stu-id="996fc-201">The `.execute()` method executes the query on the backend.</span></span>  <span data-ttu-id="996fc-202">La query viene convertita in una query [OData v3][19] prima della trasmissione al back-end di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="996fc-202">The query is converted to an [OData v3][19] query before transmission to the Mobile Apps backend.</span></span>  <span data-ttu-id="996fc-203">Alla ricezione, il back-end di App per dispositivi mobili converte la query in un'istruzione SQL prima di eseguirla nell'istanza di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="996fc-203">On receipt, the Mobile Apps backend converts the query into an SQL statement before executing it on the SQL Azure instance.</span></span>  <span data-ttu-id="996fc-204">Poiché l'attività di rete richiede tempo, il metodo `.execute()` restituisce [`ListenableFuture<E>`][18].</span><span class="sxs-lookup"><span data-stu-id="996fc-204">Since network activity takes some time, The `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="996fc-205"><a name="filtering"></a>Filtrare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="996fc-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="996fc-206">L'esecuzione della query seguente restituisce tutti gli elementi della tabella **ToDoItem** in cui **complete** è uguale a **false**.</span><span class="sxs-lookup"><span data-stu-id="996fc-206">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="996fc-207">**mToDoTable** è il riferimento alla tabella di Servizi mobili creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="996fc-207">**mToDoTable** is the reference to the mobile service table that we created previously.</span></span>

<span data-ttu-id="996fc-208">Definire un filtro con la chiamata al metodo **where** sul riferimento alla tabella.</span><span class="sxs-lookup"><span data-stu-id="996fc-208">Define a filter using the **where** method call on the table reference.</span></span> <span data-ttu-id="996fc-209">Il metodo **where** è seguito da un metodo **field**, seguito a sua volta da un metodo che specifica il predicato logico.</span><span class="sxs-lookup"><span data-stu-id="996fc-209">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span></span> <span data-ttu-id="996fc-210">I possibili metodi di predicato includono **eq** (uguale a), **ne** (non uguale a), **gt** (maggiore di), **ge** (maggiore o uguale a), **lt** (minore di), **le** (minore o uguale a).</span><span class="sxs-lookup"><span data-stu-id="996fc-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="996fc-211">Questi metodi consentono di confrontare campi numerici e campi stringa con valori specifici,</span><span class="sxs-lookup"><span data-stu-id="996fc-211">These methods let you compare number and string fields to specific values.</span></span>

<span data-ttu-id="996fc-212">ad esempio filtrare in base alle date.</span><span class="sxs-lookup"><span data-stu-id="996fc-212">You can filter on dates.</span></span> <span data-ttu-id="996fc-213">I metodi seguenti consentono di confrontare l'intero campo data o parti della data: **year**, **month**, **day**, **hour**, **minute** e **second**.</span><span class="sxs-lookup"><span data-stu-id="996fc-213">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="996fc-214">L'esempio seguente aggiunge un filtro per gli elementi la cui *data di scadenza* (due) è uguale a 2013.</span><span class="sxs-lookup"><span data-stu-id="996fc-214">The following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="996fc-215">I metodi seguenti supportano filtri complessi sui campi di tipo stringa: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim** e **length**.</span><span class="sxs-lookup"><span data-stu-id="996fc-215">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="996fc-216">L'esempio seguente filtra le righe della tabella in cui la colonna *text* inizia con "PRI0".</span><span class="sxs-lookup"><span data-stu-id="996fc-216">The following example filters for table rows where the *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="996fc-217">I metodi operatore seguenti sono supportati sui campi numerici: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling** e **round**.</span><span class="sxs-lookup"><span data-stu-id="996fc-217">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="996fc-218">L'esempio seguente filtra le righe della tabella in cui il valore di **duration** è un numero pari.</span><span class="sxs-lookup"><span data-stu-id="996fc-218">The following example filters for table rows where the **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="996fc-219">È possibile combinare i predicati con questi metodi logici: **and**, **or** e **not**.</span><span class="sxs-lookup"><span data-stu-id="996fc-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="996fc-220">L'esempio seguente combina due degli esempi precedenti.</span><span class="sxs-lookup"><span data-stu-id="996fc-220">The following example combines two of the preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="996fc-221">Raggruppare e annidare operatori logici:</span><span class="sxs-lookup"><span data-stu-id="996fc-221">Group and nest logical operators:</span></span>

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

<span data-ttu-id="996fc-222">Per una descrizione più dettagliata ed esempi di filtro, vedere [Exploring the richness of the Android client query model][20] (Analisi delle funzionalità complesse disponibili nel modello di query client per Android).</span><span class="sxs-lookup"><span data-stu-id="996fc-222">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model][20].</span></span>

### <span data-ttu-id="996fc-223"><a name="sorting"></a>Ordinare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="996fc-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="996fc-224">Il codice di esempio seguente restituisce tutti gli elementi di una tabella di oggetti **ToDoItems** elencati in ordine crescente in base al campo *text* .</span><span class="sxs-lookup"><span data-stu-id="996fc-224">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span></span> <span data-ttu-id="996fc-225">*mToDoTable* è il riferimento alla tabella del back-end creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="996fc-225">*mToDoTable* is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="996fc-226">Il primo parametro del metodo **orderBy** è una stringa uguale al nome del campo in base al quale eseguire l'ordinamento.</span><span class="sxs-lookup"><span data-stu-id="996fc-226">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span></span> <span data-ttu-id="996fc-227">Il secondo parametro usa l'enumerazione **QueryOrder** per specificare l'ordinamento crescente o decrescente.</span><span class="sxs-lookup"><span data-stu-id="996fc-227">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span></span>  <span data-ttu-id="996fc-228">Se per il filtro si usa il metodo ***where***, è necessario chiamare il metodo ***where*** prima del metodo ***orderBy***.</span><span class="sxs-lookup"><span data-stu-id="996fc-228">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span></span>

### <span data-ttu-id="996fc-229"><a name="selection"></a>Selezionare colonne specifiche</span><span class="sxs-lookup"><span data-stu-id="996fc-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="996fc-230">Il codice seguente illustra come restituire tutti gli elementi di una tabella di oggetti **ToDoItems**, visualizzando però solo i campi **complete** e **text**.</span><span class="sxs-lookup"><span data-stu-id="996fc-230">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span></span> <span data-ttu-id="996fc-231">**mToDoTable** è il riferimento alla tabella del back-end creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="996fc-231">**mToDoTable** is the reference to the backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="996fc-232">I parametri della funzione select sono i nomi in formato stringa delle colonne della tabella che si vuole restituire.</span><span class="sxs-lookup"><span data-stu-id="996fc-232">The parameters to the select function are the string names of the table's columns that you want to return.</span></span>  <span data-ttu-id="996fc-233">Il metodo **select** deve seguire metodi come **where** e **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="996fc-233">The **select** method needs to follow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="996fc-234">Può essere seguito da metodi di paging come **skip** e **top**.</span><span class="sxs-lookup"><span data-stu-id="996fc-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="996fc-235"><a name="paging"></a>Restituire i dati in pagine</span><span class="sxs-lookup"><span data-stu-id="996fc-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="996fc-236">I dati vengono **SEMPRE** restituiti in pagine.</span><span class="sxs-lookup"><span data-stu-id="996fc-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="996fc-237">Il numero massimo di record restituiti viene impostato dal server.</span><span class="sxs-lookup"><span data-stu-id="996fc-237">The maximum number of records returned is set by the server.</span></span>  <span data-ttu-id="996fc-238">Se il client richiede più record, il server restituisce il numero massimo di record.</span><span class="sxs-lookup"><span data-stu-id="996fc-238">If the client requests more records, then the server returns the maximum number of records.</span></span>  <span data-ttu-id="996fc-239">Per impostazione predefinita, le dimensioni di pagina massime nel server sono pari a 50 record.</span><span class="sxs-lookup"><span data-stu-id="996fc-239">By default, the maximum page size on the server is 50 records.</span></span>

<span data-ttu-id="996fc-240">Il primo esempio illustra come selezionare i primi cinque elementi di una tabella.</span><span class="sxs-lookup"><span data-stu-id="996fc-240">The first example shows how to select the top five items from a table.</span></span> <span data-ttu-id="996fc-241">La query restituisce gli elementi di una tabella di oggetti **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="996fc-241">The query returns the items from a table of **ToDoItems**.</span></span> <span data-ttu-id="996fc-242">**mToDoTable** è il riferimento alla tabella del back-end creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="996fc-242">**mToDoTable** is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="996fc-243">Ecco una query che ignora i primi cinque elementi e quindi restituisce i cinque successivi:</span><span class="sxs-lookup"><span data-stu-id="996fc-243">Here's a query that skips the first five items, and then returns the next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="996fc-244">Per ottenere tutti i record in una tabella, implementare il codice per scorrere tutte le pagine:</span><span class="sxs-lookup"><span data-stu-id="996fc-244">If you wish to get all records in a table, implement code to iterate over all pages:</span></span>

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

<span data-ttu-id="996fc-245">Una richiesta per tutti i record con questo metodo crea un minimo di due richieste al back-end di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="996fc-245">A request for all records using this method creates a minimum of two requests to the Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="996fc-246">La scelta delle dimensioni di pagina appropriate è un equilibrio tra utilizzo della memoria mentre la richiesta è in corso, utilizzo della larghezza di banda e ritardo nella ricezione completa dei dati.</span><span class="sxs-lookup"><span data-stu-id="996fc-246">Choosing the right page size is a balance between memory usage while the request is happening, bandwidth usage and delay in receiving the data completely.</span></span>  <span data-ttu-id="996fc-247">Il valore predefinito (50 record) è adatto a tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="996fc-247">The default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="996fc-248">Se si opera esclusivamente su dispositivi con maggiore memoria, aumentare fino a 500.</span><span class="sxs-lookup"><span data-stu-id="996fc-248">If you exclusively operate on larger memory devices, increase up to 500.</span></span>  <span data-ttu-id="996fc-249">È stato osservato che l'aumento delle dimensioni di pagina oltre i 500 record comporta ritardi inaccettabili e problemi di memoria di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="996fc-249">We have found that increasing the page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="996fc-250"><a name="chaining"></a>Procedura: Concatenare metodi di query</span><span class="sxs-lookup"><span data-stu-id="996fc-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="996fc-251">I metodi usati per eseguire query su tabelle di back-end possono essere concatenati.</span><span class="sxs-lookup"><span data-stu-id="996fc-251">The methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="996fc-252">Il concatenamento dei metodi di query consente di selezionare colonne specifiche di righe filtrate ordinate e sottoposte a paging.</span><span class="sxs-lookup"><span data-stu-id="996fc-252">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="996fc-253">È possibile creare filtri logici complessi.</span><span class="sxs-lookup"><span data-stu-id="996fc-253">You can create complex logical filters.</span></span>  <span data-ttu-id="996fc-254">Ogni metodo di query restituisce un oggetto Query.</span><span class="sxs-lookup"><span data-stu-id="996fc-254">Each query method returns a Query object.</span></span> <span data-ttu-id="996fc-255">Per terminare la serie di metodi ed eseguire effettivamente la query, chiamare il metodo **execute** .</span><span class="sxs-lookup"><span data-stu-id="996fc-255">To end the series of methods and actually run the query, call the **execute** method.</span></span> <span data-ttu-id="996fc-256">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="996fc-256">For example:</span></span>

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

<span data-ttu-id="996fc-257">I metodi con query concatenate devono essere ordinati nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="996fc-257">The chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="996fc-258">Metodi di filtraggio (**where**).</span><span class="sxs-lookup"><span data-stu-id="996fc-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="996fc-259">Metodi di ordinamento (**orderBy**).</span><span class="sxs-lookup"><span data-stu-id="996fc-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="996fc-260">Metodi di selezione (**select**).</span><span class="sxs-lookup"><span data-stu-id="996fc-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="996fc-261">Metodi di paging (**skip** e **top**).</span><span class="sxs-lookup"><span data-stu-id="996fc-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="996fc-262"><a name="binding"></a>Associare dati all'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="996fc-262"><a name="binding"></a>Bind data to the user interface</span></span>

<span data-ttu-id="996fc-263">L'associazione dati riguarda tre componenti:</span><span class="sxs-lookup"><span data-stu-id="996fc-263">Data binding involves three components:</span></span>

* <span data-ttu-id="996fc-264">Origine dati</span><span class="sxs-lookup"><span data-stu-id="996fc-264">The data source</span></span>
* <span data-ttu-id="996fc-265">Layout della schermata</span><span class="sxs-lookup"><span data-stu-id="996fc-265">The screen layout</span></span>
* <span data-ttu-id="996fc-266">Adattatore che collega i due componenti.</span><span class="sxs-lookup"><span data-stu-id="996fc-266">The adapter that ties the two together.</span></span>

<span data-ttu-id="996fc-267">Nel codice di esempio i dati vengono restituiti dalla tabella di app per dispositivi mobili di SQL Azure **ToDoItem** in una matrice.</span><span class="sxs-lookup"><span data-stu-id="996fc-267">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="996fc-268">Si tratta di una delle attività più comuni per le applicazioni dati.</span><span class="sxs-lookup"><span data-stu-id="996fc-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="996fc-269">Le query su database restituiscono spesso una raccolta di righe che il client ottiene in un elenco o una matrice.</span><span class="sxs-lookup"><span data-stu-id="996fc-269">Database queries often return a collection of rows that the client gets in a list or array.</span></span> <span data-ttu-id="996fc-270">In questo esempio la matrice è l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="996fc-270">In this sample, the array is the data source.</span></span>  <span data-ttu-id="996fc-271">Nel codice viene specificato un layout di schermata che definisce la visualizzazione dei dati che appaiono sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="996fc-271">The code specifies a screen layout that defines the view of the data that appears on the device.</span></span>  <span data-ttu-id="996fc-272">I due elementi vengono associati tra loro tramite un adattatore, che in questo codice è un'estensione della classe **ArrayAdapter&lt;ToDoItem&gt;**.</span><span class="sxs-lookup"><span data-stu-id="996fc-272">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="996fc-273"><a name="layout"></a>Definire il layout</span><span class="sxs-lookup"><span data-stu-id="996fc-273"><a name="layout"></a>Define the Layout</span></span>

<span data-ttu-id="996fc-274">Il layout è definito da diversi frammenti di codice XML.</span><span class="sxs-lookup"><span data-stu-id="996fc-274">The layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="996fc-275">Dato un layout esistente, il codice seguente rappresenta l'oggetto **ListView** che si vuole popolare con i dati del server.</span><span class="sxs-lookup"><span data-stu-id="996fc-275">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="996fc-276">Nel codice precedente l'attributo *listitem* consente di specificare l'ID del layout per una singola riga dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="996fc-276">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span></span> <span data-ttu-id="996fc-277">Questo codice specifica una casella di controllo e il testo ad essa associato e viene creata una sola istanza per ogni elemento nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="996fc-277">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span></span> <span data-ttu-id="996fc-278">Questo layout non visualizza il campo **id** , ma se il layout è più complesso nella visualizzazione vengono specificati campi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="996fc-278">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span></span> <span data-ttu-id="996fc-279">Il codice è incluso nel file **row_list_to_do.xml**.</span><span class="sxs-lookup"><span data-stu-id="996fc-279">This code is in the **row_list_to_do.xml** file.</span></span>

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

#### <span data-ttu-id="996fc-280"><a name="adapter"></a>Definire l'adattatore</span><span class="sxs-lookup"><span data-stu-id="996fc-280"><a name="adapter"></a>Define the adapter</span></span>
<span data-ttu-id="996fc-281">Poiché l'origine dati della visualizzazione è una matrice di oggetti **ToDoItem**, viene creata una sottoclasse per l'adattatore da una classe **ArrayAdapter&lt;ToDoItem&gt;**.</span><span class="sxs-lookup"><span data-stu-id="996fc-281">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="996fc-282">Questa sottoclasse consente di ottenere una visualizzazione per ogni oggetto **ToDoItem** che usa il layout **row_list_to_do**.</span><span class="sxs-lookup"><span data-stu-id="996fc-282">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span></span>  <span data-ttu-id="996fc-283">Nel codice viene definita la classe seguente che costituisce un'estensione della classe **ArrayAdapter&lt;E&gt;**:</span><span class="sxs-lookup"><span data-stu-id="996fc-283">In our code, we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="996fc-284">Eseguire l'override del metodo **getView** dell'adattatore.</span><span class="sxs-lookup"><span data-stu-id="996fc-284">Override the adapters **getView** method.</span></span> <span data-ttu-id="996fc-285">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="996fc-285">For example:</span></span>

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

<span data-ttu-id="996fc-286">Creare un'istanza della classe nell'attività nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="996fc-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="996fc-287">Il secondo parametro del costruttore ToDoItemAdapter è un riferimento al layout.</span><span class="sxs-lookup"><span data-stu-id="996fc-287">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span></span> <span data-ttu-id="996fc-288">È ora possibile creare un'istanza di **ListView** e assegnare l'adattatore a **ListView**.</span><span class="sxs-lookup"><span data-stu-id="996fc-288">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="996fc-289"><a name="use-adapter"></a>Usare l'adattatore per l'associazione all'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="996fc-289"><a name="use-adapter"></a>Use the Adapter to Bind to the UI</span></span>

<span data-ttu-id="996fc-290">È ora possibile utilizzare l'associazione dati.</span><span class="sxs-lookup"><span data-stu-id="996fc-290">You are now ready to use data binding.</span></span> <span data-ttu-id="996fc-291">Il codice seguente illustra come recuperare gli elementi nella tabella e inserisce gli elementi restituiti per l'adattatore locale.</span><span class="sxs-lookup"><span data-stu-id="996fc-291">The following code shows how to get items in the table and fills the local adapter with the returned items.</span></span>

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

<span data-ttu-id="996fc-292">Chiamare l'adattatore ogni volta che si modifica la tabella **ToDoItem** .</span><span class="sxs-lookup"><span data-stu-id="996fc-292">Call the adapter any time you modify the **ToDoItem** table.</span></span> <span data-ttu-id="996fc-293">Dal momento che le modifiche vengono fatte record per record, si gestisce una singola riga anziché una raccolta.</span><span class="sxs-lookup"><span data-stu-id="996fc-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="996fc-294">Quando si inserisce un elemento, chiamare il metodo **add** sull'adattatore, mentre quando lo si elimina, chiamare il metodo **remove**.</span><span class="sxs-lookup"><span data-stu-id="996fc-294">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span></span>

<span data-ttu-id="996fc-295">Un esempio completo è disponibile nel [progetto di avvio rapido per Android][21].</span><span class="sxs-lookup"><span data-stu-id="996fc-295">You can find a complete example in the [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="996fc-296"><a name="inserting"></a>Inserire dati nel back-end</span><span class="sxs-lookup"><span data-stu-id="996fc-296"><a name="inserting"></a>Insert data into the backend</span></span>

<span data-ttu-id="996fc-297">Viene creata un'istanza della classe *ToDoItem* e vengono impostate le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="996fc-297">Instantiate an instance of the *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="996fc-298">Usare quindi **insert()** per inserire un oggetto:</span><span class="sxs-lookup"><span data-stu-id="996fc-298">Then use **insert()** to insert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="996fc-299">L'entità restituita corrisponde ai dati inseriti nella tabella del back-end, inclusi l'ID e gli eventuali altri valori, ad esempio i campi `createdAt`, `updatedAt` e `version`, impostati sul back-end.</span><span class="sxs-lookup"><span data-stu-id="996fc-299">The returned entity matches the data inserted into the backend table, included the ID and any other values (such as the `createdAt`, `updatedAt`, and `version` fields) set on the backend.</span></span>

<span data-ttu-id="996fc-300">Le tabelle di App per dispositivi mobili richiedono una colonna chiave primaria denominata **id**.</span><span class="sxs-lookup"><span data-stu-id="996fc-300">Mobile Apps tables require a primary key column named **id**.</span></span> <span data-ttu-id="996fc-301">Questa colonna deve essere una stringa.</span><span class="sxs-lookup"><span data-stu-id="996fc-301">This column must be a string.</span></span> <span data-ttu-id="996fc-302">Il valore predefinito della colonna ID è un GUID.</span><span class="sxs-lookup"><span data-stu-id="996fc-302">The default value of the ID column is a GUID.</span></span>  <span data-ttu-id="996fc-303">È possibile specificare altri valori univoci, come gli indirizzi di posta elettronica o i nomi utente.</span><span class="sxs-lookup"><span data-stu-id="996fc-303">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="996fc-304">Se non si fornisce un valore ID di stringa per un record inserito, il back-end genera un nuovo GUID.</span><span class="sxs-lookup"><span data-stu-id="996fc-304">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span></span>

<span data-ttu-id="996fc-305">I valori ID di stringa offrono i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="996fc-305">String ID values provide the following advantages:</span></span>

* <span data-ttu-id="996fc-306">Gli ID possono essere generati senza creare un round trip al database.</span><span class="sxs-lookup"><span data-stu-id="996fc-306">IDs can be generated without making a round trip to the database.</span></span>
* <span data-ttu-id="996fc-307">L'unione di record da tabelle o database diversi risulta semplificata.</span><span class="sxs-lookup"><span data-stu-id="996fc-307">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="996fc-308">I valori ID si integrano in modo più efficace con la logica di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="996fc-308">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="996fc-309">I valori ID di stringa sono **OBBLIGATORI** per il supporto di sincronizzazione offline.</span><span class="sxs-lookup"><span data-stu-id="996fc-309">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="996fc-310">Non è possibile modificare un ID dopo che è stato archiviato nel database back-end.</span><span class="sxs-lookup"><span data-stu-id="996fc-310">You cannot change an Id once it is stored in the backend database.</span></span>

## <span data-ttu-id="996fc-311"><a name="updating"></a>Aggiornare dati in un'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="996fc-311"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="996fc-312">Per aggiornare i dati in una tabella, passare il nuovo oggetto al metodo **update()** .</span><span class="sxs-lookup"><span data-stu-id="996fc-312">To update data in a table, pass the new object to the **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="996fc-313">In questo esempio *item* è un riferimento a una riga nella tabella *ToDoItem* alla quale sono state apportate alcune modifiche.</span><span class="sxs-lookup"><span data-stu-id="996fc-313">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span></span>  <span data-ttu-id="996fc-314">Viene aggiornata la riga con lo stesso **id** .</span><span class="sxs-lookup"><span data-stu-id="996fc-314">The row with the same **id** is updated.</span></span>

## <span data-ttu-id="996fc-315"><a name="deleting"></a>Eliminare dati in un'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="996fc-315"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="996fc-316">Il codice seguente illustra come eliminare dati da una tabella specificando l'oggetto dati.</span><span class="sxs-lookup"><span data-stu-id="996fc-316">The following code shows how to delete data from a table by specifying the data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="996fc-317">È anche possibile eliminare un elemento specificando il campo **id** della riga da eliminare.</span><span class="sxs-lookup"><span data-stu-id="996fc-317">You can also delete an item by specifying the **id** field of the row to delete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="996fc-318"><a name="lookup"></a>Cercare un elemento specifico per ID</span><span class="sxs-lookup"><span data-stu-id="996fc-318"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="996fc-319">Cercare un elemento con un campo **id** specifico con il metodo **lookUp()**:</span><span class="sxs-lookup"><span data-stu-id="996fc-319">Look up an item with a specific **id** field with the **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="996fc-320"><a name="untyped"></a>Procedura: Usare dati non tipizzati</span><span class="sxs-lookup"><span data-stu-id="996fc-320"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="996fc-321">Il modello di programmazione non tipizzato offre un controllo accurato della serializzazione JSON.</span><span class="sxs-lookup"><span data-stu-id="996fc-321">The untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="996fc-322">È consigliabile usarlo in alcuni scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="996fc-322">There are some common scenarios where you may wish to use an untyped programming model.</span></span> <span data-ttu-id="996fc-323">Un esempio di utilizzo è una tabella di back-end che contiene un numero elevato di colonne ed è necessario fare riferimento solo ad alcune di esse.</span><span class="sxs-lookup"><span data-stu-id="996fc-323">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span></span>  <span data-ttu-id="996fc-324">Il modello tipizzato richiede la definizione di tutte le colonne definite nel back-end di App per dispositivi mobili nella classe dati.</span><span class="sxs-lookup"><span data-stu-id="996fc-324">The typed model requires you to define all the columns defined in the Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="996fc-325">La maggior parte delle chiamate API per l'accesso ai dati è simile alle chiamate della programmazione tipizzata.</span><span class="sxs-lookup"><span data-stu-id="996fc-325">Most of the API calls for accessing data are similar to the typed programming calls.</span></span> <span data-ttu-id="996fc-326">La principale differenza consiste nel fatto che nel modello non tipizzato i metodi vengono chiamati sull'oggetto **MobileServiceJsonTable**, anziché su **MobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="996fc-326">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span></span>

### <span data-ttu-id="996fc-327"><a name="json_instance"></a>Creare un'istanza di una tabella non tipizzata</span><span class="sxs-lookup"><span data-stu-id="996fc-327"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="996fc-328">Analogamente al modello tipizzato, si inizia recuperando un riferimento alla tabella, ma in questo caso si tratta di un oggetto **MobileServicesJsonTable** .</span><span class="sxs-lookup"><span data-stu-id="996fc-328">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="996fc-329">Ottenere il riferimento chiamando il metodo **getTable** su un'istanza del client:</span><span class="sxs-lookup"><span data-stu-id="996fc-329">Obtain the reference by calling the **getTable** method on an instance of the client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="996fc-330">Dopo avere creato un'istanza di **MobileServiceJsonTable**, l'istanza contiene praticamente la stessa API disponibile con il modello di programmazione tipizzato.</span><span class="sxs-lookup"><span data-stu-id="996fc-330">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span></span> <span data-ttu-id="996fc-331">In alcuni casi, i metodi accettano un parametro non tipizzato anziché un parametro tipizzato.</span><span class="sxs-lookup"><span data-stu-id="996fc-331">In some cases, the methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="996fc-332"><a name="json_insert"></a>Eseguire un inserimento in una tabella non tipizzata</span><span class="sxs-lookup"><span data-stu-id="996fc-332"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="996fc-333">Nel codice seguente viene illustrato come eseguire un'operazione di insert.</span><span class="sxs-lookup"><span data-stu-id="996fc-333">The following code shows how to do an insert.</span></span> <span data-ttu-id="996fc-334">Il primo passaggio consiste nel creare un oggetto [JsonObject][1], incluso nella libreria [gson][3].</span><span class="sxs-lookup"><span data-stu-id="996fc-334">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="996fc-335">Usare quindi il metodo **insert()** per inserire l'oggetto non tipizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="996fc-335">Then, Use **insert()** to insert the untyped object into the table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="996fc-336">Se è necessario ottenere l'ID dell'oggetto inserito, usare il metodo **getAsJsonPrimitive()** .</span><span class="sxs-lookup"><span data-stu-id="996fc-336">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="996fc-337"><a name="json_delete"></a>Eliminare un'istanza da una tabella non tipizzata</span><span class="sxs-lookup"><span data-stu-id="996fc-337"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="996fc-338">Nel codice seguente viene illustrato come eliminare un'istanza, in questo caso la stessa istanza di un oggetto **JsonObject** creato nell'esempio *insert* precedente.</span><span class="sxs-lookup"><span data-stu-id="996fc-338">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span></span> <span data-ttu-id="996fc-339">Il codice è analogo a quello del caso tipizzato, ma il metodo ha una firma diversa poiché fa riferimento a un oggetto **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="996fc-339">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="996fc-340">È inoltre possibile eliminare un'istanza direttamente utilizzando il relativo ID:</span><span class="sxs-lookup"><span data-stu-id="996fc-340">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="996fc-341"><a name="json_get"></a>Restituire tutte le righe di una tabella non tipizzata</span><span class="sxs-lookup"><span data-stu-id="996fc-341"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="996fc-342">Il seguente codice illustra come recuperare un'intera tabella.</span><span class="sxs-lookup"><span data-stu-id="996fc-342">The following code shows how to retrieve an entire table.</span></span> <span data-ttu-id="996fc-343">Poiché si sta usando una tabella JSONO, è possibile recuperare in modo selettivo solo alcune colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="996fc-343">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span></span>

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

<span data-ttu-id="996fc-344">Lo stesso insieme di metodi di filtro e paging disponibili per il modello tipizzato è disponibile per il modello non tipizzato.</span><span class="sxs-lookup"><span data-stu-id="996fc-344">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model.</span></span>

## <span data-ttu-id="996fc-345"><a name="offline-sync"></a>Implementare la sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="996fc-345"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="996fc-346">Azure Mobile Apps Client SDK implementa anche la sincronizzazione offline dei dati usando un database SQLite per archiviare una copia locale dei dati del server.</span><span class="sxs-lookup"><span data-stu-id="996fc-346">The Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database to store a copy of the server data locally.</span></span>  <span data-ttu-id="996fc-347">Le operazioni eseguite su una tabella offline non richiedono la connettività per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="996fc-347">Operations performed on an offline table do not require mobile connectivity to work.</span></span>  <span data-ttu-id="996fc-348">La sincronizzazione offline agevola la resilienza e le prestazioni a scapito di una logica più complessa per la risoluzione dei conflitti.</span><span class="sxs-lookup"><span data-stu-id="996fc-348">Offline sync aids in resilience and performance at the expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="996fc-349">Azure Mobile Apps Client SDK implementa le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="996fc-349">The Azure Mobile Apps Client SDK implements the following features:</span></span>

* <span data-ttu-id="996fc-350">Sincronizzazione incrementale: vengono scaricati solo i record aggiornati e nuovi, risparmiando larghezza di banda e utilizzo della memoria.</span><span class="sxs-lookup"><span data-stu-id="996fc-350">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="996fc-351">Concorrenza ottimistica: si presuppone che le operazioni abbiano esito positivo.</span><span class="sxs-lookup"><span data-stu-id="996fc-351">Optimistic Concurrency: Operations are assumed to succeed.</span></span>  <span data-ttu-id="996fc-352">La risoluzione dei conflitti viene posticipata finché gli aggiornamenti non vengono eseguiti nel server.</span><span class="sxs-lookup"><span data-stu-id="996fc-352">Conflict Resolution is deferred until updates are performed on the server.</span></span>
* <span data-ttu-id="996fc-353">Risoluzione dei conflitti: l'SDK rileva quando è stata apportata una modifica in conflitto nel server e fornisce hook per avvisare l'utente.</span><span class="sxs-lookup"><span data-stu-id="996fc-353">Conflict Resolution: The SDK detects when a conflicting change has been made at the server and provides hooks to alert the user.</span></span>
* <span data-ttu-id="996fc-354">Eliminazione temporanea: i record eliminati vengono contrassegnati come tali, consentendo agli altri dispositivi di aggiornare la cache offline.</span><span class="sxs-lookup"><span data-stu-id="996fc-354">Soft Delete: Deleted records are marked deleted, allowing other devices to update their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="996fc-355">Inizializzare la sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="996fc-355">Initialize Offline Sync</span></span>

<span data-ttu-id="996fc-356">Ogni tabella offline deve essere definito nella cache offline prima dell'uso.</span><span class="sxs-lookup"><span data-stu-id="996fc-356">Each offline table must be defined in the offline cache before use.</span></span>  <span data-ttu-id="996fc-357">La definizione della tabella in genere viene eseguita immediatamente dopo la creazione del client:</span><span class="sxs-lookup"><span data-stu-id="996fc-357">Normally, table definition is done immediately after the creation of the client:</span></span>

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

                // Create a table definition.  As a best practice, store this with the model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define the table in the local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize the local store
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

### <a name="obtain-a-reference-to-the-offline-cache-table"></a><span data-ttu-id="996fc-358">Ottenere un riferimento alla tabella della cache offline</span><span class="sxs-lookup"><span data-stu-id="996fc-358">Obtain a reference to the Offline Cache Table</span></span>

<span data-ttu-id="996fc-359">Per una tabella online, si usa `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="996fc-359">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="996fc-360">Per una tabella offline, usare `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="996fc-360">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="996fc-361">Tutti i metodi disponibili per le tabelle online (inclusi filtri, ordinamento, paging, inserimento di dati, aggiornamento di dati ed eliminazione di dati) funzionano correttamente sia nelle tabelle online che in quelle offline.</span><span class="sxs-lookup"><span data-stu-id="996fc-361">All the methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-the-local-offline-cache"></a><span data-ttu-id="996fc-362">Sincronizzare la cache locale offline</span><span class="sxs-lookup"><span data-stu-id="996fc-362">Synchronize the Local Offline Cache</span></span>

<span data-ttu-id="996fc-363">La sincronizzazione è sotto il controllo dell'app.</span><span class="sxs-lookup"><span data-stu-id="996fc-363">Synchronization is within the control of your app.</span></span>  <span data-ttu-id="996fc-364">Ecco un esempio di metodo di sincronizzazione:</span><span class="sxs-lookup"><span data-stu-id="996fc-364">Here is an example synchronization method:</span></span>

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

<span data-ttu-id="996fc-365">Se viene fornito un nome di query al metodo `.pull(query, queryname)`, viene usata la sincronizzazione incrementale per restituire solo i record creati o modificati dopo il corretto completamento dell'ultimo pull.</span><span class="sxs-lookup"><span data-stu-id="996fc-365">If a query name is provided to the `.pull(query, queryname)` method, then incremental sync is used to return only records that have been created or changed since the last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="996fc-366">Gestire i conflitti durante la sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="996fc-366">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="996fc-367">Se si verifica un conflitto durante un'operazione `.push()`, viene generata un'eccezione `MobileServiceConflictException`.</span><span class="sxs-lookup"><span data-stu-id="996fc-367">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="996fc-368">L'elemento rilasciato dal server viene incorporato nell'eccezione e può essere recuperato da `.getItem()` nell'eccezione.</span><span class="sxs-lookup"><span data-stu-id="996fc-368">The server-issued item is embedded in the exception and can be retrieved by `.getItem()` on the exception.</span></span>  <span data-ttu-id="996fc-369">Modificare il push chiamando gli elementi seguenti sull'oggetto MobileServiceSyncContext:</span><span class="sxs-lookup"><span data-stu-id="996fc-369">Adjust the push by calling the following items on the MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="996fc-370">Dopo che tutti i conflitti sono stati contrassegnati nel modo desiderato, chiamare di nuovo `.push()` per risolvere tutti i conflitti.</span><span class="sxs-lookup"><span data-stu-id="996fc-370">Once all conflicts are marked as you wish, call `.push()` again to resolve all the conflicts.</span></span>

## <span data-ttu-id="996fc-371"><a name="custom-api"></a>Chiamare un'API personalizzata</span><span class="sxs-lookup"><span data-stu-id="996fc-371"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="996fc-372">Un'API personalizzata consente di definire endpoint personalizzati che espongono la funzionalità del server di cui non è possibile eseguire il mapping a un'operazione di inserimento, aggiornamento, eliminazione o lettura.</span><span class="sxs-lookup"><span data-stu-id="996fc-372">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="996fc-373">L'utilizzo di un'API personalizzata offre maggiore controllo sulla messaggistica, incluse la lettura e l'impostazione delle intestazioni del messaggio HTTP e la definizione di un formato del corpo del messaggio diverso da JSON.</span><span class="sxs-lookup"><span data-stu-id="996fc-373">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="996fc-374">Per chiamare l'endpoint dell'API personalizzata da un client Android, chiamare il metodo **invokeApi** .</span><span class="sxs-lookup"><span data-stu-id="996fc-374">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span></span> <span data-ttu-id="996fc-375">L'esempio seguente illustra come chiamare un endpoint API denominato **completeAll**, che restituisce una classe della raccolta denominata **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="996fc-375">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

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

<span data-ttu-id="996fc-376">Nel client viene chiamato il metodo **invokeApi** , che invia una richiesta POST alla nuova API personalizzata.</span><span class="sxs-lookup"><span data-stu-id="996fc-376">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span></span> <span data-ttu-id="996fc-377">Il risultato restituito dall'API personalizzata viene visualizzato in una finestra di dialogo con messaggio, insieme a eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="996fc-377">The result returned by the custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="996fc-378">Altre versioni di **invokeApi** consentono di inviare facoltativamente un oggetto nel corpo della richiesta, specificare il metodo HTTP e inviare parametri di query con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="996fc-378">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span></span> <span data-ttu-id="996fc-379">Vengono fornite anche versioni non tipizzate di **invokeApi** .</span><span class="sxs-lookup"><span data-stu-id="996fc-379">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="996fc-380"><a name="authentication"></a>Aggiungere l'autenticazione all'app</span><span class="sxs-lookup"><span data-stu-id="996fc-380"><a name="authentication"></a>Add authentication to your app</span></span>

<span data-ttu-id="996fc-381">Le esercitazioni descrivono già in dettaglio come aggiungere queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="996fc-381">Tutorials already describe in detail how to add these features.</span></span>

<span data-ttu-id="996fc-382">Il servizio app supporta l'[autenticazione degli utenti di app](app-service-mobile-android-get-started-users.md) con diversi provider di identità esterni: Facebook, Google, account Microsoft, Twitter e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="996fc-382">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="996fc-383">È possibile impostare le autorizzazioni per le tabelle per limitare l'accesso per operazioni specifiche solo agli utenti autenticati.</span><span class="sxs-lookup"><span data-stu-id="996fc-383">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="996fc-384">È inoltre possibile utilizzare l'identità degli utenti autenticati per implementare regole di autorizzazione nel backend.</span><span class="sxs-lookup"><span data-stu-id="996fc-384">You can also use the identity of authenticated users to implement authorization rules in your backend.</span></span>

<span data-ttu-id="996fc-385">Sono supportati due flussi di autenticazione, ovvero un flusso **server** e un flusso **client**.</span><span class="sxs-lookup"><span data-stu-id="996fc-385">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="996fc-386">Il flusso server è il processo di autenticazione più semplice, poiché si basa sull'interfaccia Web del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="996fc-386">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span></span>  <span data-ttu-id="996fc-387">Non sono necessari SDK aggiuntivi per implementare l'autenticazione del flusso server.</span><span class="sxs-lookup"><span data-stu-id="996fc-387">No additional SDKs are required to implement server flow authentication.</span></span> <span data-ttu-id="996fc-388">L'autenticazione del flusso server non fornisce un'integrazione completa con il dispositivo mobile ed è consigliata solo per dimostrare scenari concettuali.</span><span class="sxs-lookup"><span data-stu-id="996fc-388">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="996fc-389">Il flusso client assicura maggiore integrazione con funzionalità specifiche del dispositivo, ad esempio Single-Sign-On, poiché si basa su SDK forniti dal provider di identità.</span><span class="sxs-lookup"><span data-stu-id="996fc-389">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span></span>  <span data-ttu-id="996fc-390">Ad esempio, è possibile integrare l'SDK di Facebook nell'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="996fc-390">For example, you can integrate the Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="996fc-391">Il client per dispositivi mobili passa all'app Facebook e conferma l'accesso prima di passare di nuovo all'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="996fc-391">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span></span>

<span data-ttu-id="996fc-392">Per abilitare l'autenticazione nell'app, è necessario eseguire quattro passaggi:</span><span class="sxs-lookup"><span data-stu-id="996fc-392">Four steps are required to enable authentication in your app:</span></span>

* <span data-ttu-id="996fc-393">Registrare l'app per l'autenticazione con un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="996fc-393">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="996fc-394">Configurare il back-end del servizio app.</span><span class="sxs-lookup"><span data-stu-id="996fc-394">Configure your App Service backend.</span></span>
* <span data-ttu-id="996fc-395">Limitare le autorizzazioni per la tabella solo agli utenti autenticati nel back-end del servizio app.</span><span class="sxs-lookup"><span data-stu-id="996fc-395">Restrict table permissions to authenticated users only on the App Service backend.</span></span>
* <span data-ttu-id="996fc-396">Aggiungere codice di autenticazione all'app.</span><span class="sxs-lookup"><span data-stu-id="996fc-396">Add authentication code to your app.</span></span>

<span data-ttu-id="996fc-397">È possibile impostare le autorizzazioni per le tabelle per limitare l'accesso per operazioni specifiche solo agli utenti autenticati.</span><span class="sxs-lookup"><span data-stu-id="996fc-397">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="996fc-398">Per modificare le richieste, è anche possibile usare il SID di un utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="996fc-398">You can also use the SID of an authenticated user to modify requests.</span></span>  <span data-ttu-id="996fc-399">Per altre informazioni, vedere [Aggiungere l'autenticazione all'app Android] e la documentazione sulle procedure dell'SDK del server.</span><span class="sxs-lookup"><span data-stu-id="996fc-399">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="996fc-400"><a name="caching"></a>Autenticazione: flusso server</span><span class="sxs-lookup"><span data-stu-id="996fc-400"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="996fc-401">Il codice seguente avvia la procedura di accesso del flusso server con il provider Google.</span><span class="sxs-lookup"><span data-stu-id="996fc-401">The following code starts a server flow login process using the Google provider.</span></span>  <span data-ttu-id="996fc-402">È necessaria una configurazione aggiuntiva a causa dei requisiti di sicurezza per il provider Google:</span><span class="sxs-lookup"><span data-stu-id="996fc-402">Additional configuration is required because of the security requirements for the Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="996fc-403">Aggiungere anche il metodo seguente alla classe Activity principale:</span><span class="sxs-lookup"><span data-stu-id="996fc-403">In addition, add the following method to the main Activity class:</span></span>

```java
// You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check the request code matches the one we send in the login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check the error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="996fc-404">L'elemento `GOOGLE_LOGIN_REQUEST_CODE` definito nell'attività principale viene usato per il metodo `login()` e nel metodo `onActivityResult()`.</span><span class="sxs-lookup"><span data-stu-id="996fc-404">The `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for the `login()` method and within the `onActivityResult()` method.</span></span>  <span data-ttu-id="996fc-405">È possibile scegliere qualsiasi numero univoco, purché lo stesso numero venga usato nei metodi `login()` e `onActivityResult()`.</span><span class="sxs-lookup"><span data-stu-id="996fc-405">You can choose any unique number, as long as the same number is used within the `login()` method and the `onActivityResult()` method.</span></span>  <span data-ttu-id="996fc-406">Se si astrae il codice client in un adattatore di un servizio (come illustrato prima), è consigliabile chiamare i metodi appropriati sull'adattatore del servizio.</span><span class="sxs-lookup"><span data-stu-id="996fc-406">If you abstract the client code into a service adapter (as shown earlier), you should call the appropriate methods on the service adapter.</span></span>

<span data-ttu-id="996fc-407">È anche necessario configurare il progetto per customtabs.</span><span class="sxs-lookup"><span data-stu-id="996fc-407">You also need to configure the project for customtabs.</span></span>  <span data-ttu-id="996fc-408">Specificare prima di tutto un URL di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="996fc-408">First specify a redirect-URL.</span></span>  <span data-ttu-id="996fc-409">Aggiungere il frammento di codice seguente a `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="996fc-409">Add the following snippet to `AndroidManifest.xml`:</span></span>

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

<span data-ttu-id="996fc-410">Aggiungere **redirectUriScheme** al file `build.gradle` per l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="996fc-410">Add the **redirectUriScheme** to the `build.gradle` file for your application:</span></span>

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

<span data-ttu-id="996fc-411">Aggiungere infine `com.android.support:customtabs:23.0.1` all'elenco di dipendenze nel file `build.gradle`:</span><span class="sxs-lookup"><span data-stu-id="996fc-411">Finally, add `com.android.support:customtabs:23.0.1` to the dependencies list in the `build.gradle` file:</span></span>

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

<span data-ttu-id="996fc-412">È possibile ottenere l'ID dell'utente connesso da un oggetto **MobileServiceUser** usando il metodo **getUserId**.</span><span class="sxs-lookup"><span data-stu-id="996fc-412">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span></span> <span data-ttu-id="996fc-413">Per un esempio di come usare Futures per chiamare le API di accesso asincrone, vedere [Aggiungere l'autenticazione all'app Android].</span><span class="sxs-lookup"><span data-stu-id="996fc-413">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="996fc-414">Lo schema URL indicato rispetta la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="996fc-414">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="996fc-415">Assicurarsi che tutte le occorrenze di `{url_scheme_of_you_app}` rispettino questa distinzione.</span><span class="sxs-lookup"><span data-stu-id="996fc-415">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="996fc-416"><a name="caching"></a>Memorizzare nella cache i token di autenticazione</span><span class="sxs-lookup"><span data-stu-id="996fc-416"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="996fc-417">Per memorizzare nella cache i token di autenticazione, è necessario archiviare l'ID utente e il token di autenticazione in locale nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="996fc-417">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span></span> <span data-ttu-id="996fc-418">Al successivo avvio dell'app, la cache viene verificata e, se sono presenti questi valori, è possibile ignorare la procedura di accesso e riattivare il client con questi dati.</span><span class="sxs-lookup"><span data-stu-id="996fc-418">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span></span> <span data-ttu-id="996fc-419">Questi dati sono tuttavia sensibili e devono essere crittografati per garantire la sicurezza in caso di furto del telefono.</span><span class="sxs-lookup"><span data-stu-id="996fc-419">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span></span>  <span data-ttu-id="996fc-420">È possibile vedere un esempio completo della memorizzazione nella cache dei token di autenticazione nella sezione [Memorizzare nella cache i token di autenticazione][7].</span><span class="sxs-lookup"><span data-stu-id="996fc-420">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="996fc-421">Quando si prova a usare un token scaduto, viene visualizzata una risposta di tipo *401 - Non autorizzato* .</span><span class="sxs-lookup"><span data-stu-id="996fc-421">When you try to use an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="996fc-422">È possibile gestire gli errori di autenticazione tramite i filtri.</span><span class="sxs-lookup"><span data-stu-id="996fc-422">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="996fc-423">I filtri intercettano le richieste al back-end del servizio app.</span><span class="sxs-lookup"><span data-stu-id="996fc-423">Filters intercept requests to the App Service backend.</span></span> <span data-ttu-id="996fc-424">Il codice di filtro verifica quindi la risposta per un errore di tipo 401, attiva il processo di accesso e quindi riprende la richiesta che ha generato l'errore.</span><span class="sxs-lookup"><span data-stu-id="996fc-424">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span></span>

### <span data-ttu-id="996fc-425"><a name="refresh"></a>Usare i token di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="996fc-425"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="996fc-426">La durata definita del token restituito dall'autenticazione e dall'autorizzazione nel servizio app di Azure è di un'ora.</span><span class="sxs-lookup"><span data-stu-id="996fc-426">The token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="996fc-427">Dopo questo periodo, è necessario ripetere l'autenticazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="996fc-427">After this period, you must reauthenticate the user.</span></span>  <span data-ttu-id="996fc-428">Se si usa un token di lunga durata ricevuto tramite l'autenticazione basata sul flusso client, è possibile ripetere l'autenticazione con l'autenticazione e l'autorizzazione del servizio app di Azure usando lo stesso token.</span><span class="sxs-lookup"><span data-stu-id="996fc-428">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using the same token.</span></span>  <span data-ttu-id="996fc-429">Viene generato un altro token del servizio app di Azure con una nuova durata.</span><span class="sxs-lookup"><span data-stu-id="996fc-429">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="996fc-430">È anche possibile registrare il provider per l'uso di token di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="996fc-430">You can also register the provider to use Refresh Tokens.</span></span>  <span data-ttu-id="996fc-431">Un token di aggiornamento non è sempre disponibile.</span><span class="sxs-lookup"><span data-stu-id="996fc-431">A Refresh Token is not always available.</span></span>  <span data-ttu-id="996fc-432">È necessaria una configurazione aggiuntiva:</span><span class="sxs-lookup"><span data-stu-id="996fc-432">Additional configuration is required:</span></span>

* <span data-ttu-id="996fc-433">Per **Azure Active Directory**, configurare un segreto client per l'app Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="996fc-433">For **Azure Active Directory**, configure a client secret for the Azure Active Directory App.</span></span>  <span data-ttu-id="996fc-434">Specificare il segreto client nel servizio app di Azure durante la configurazione dell'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="996fc-434">Specify the client secret in the Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="996fc-435">Quando si chiama `.login()`, passare `response_type=code id_token` come parametro:</span><span class="sxs-lookup"><span data-stu-id="996fc-435">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="996fc-436">Per **Google**, passare `access_type=offline` come parametro:</span><span class="sxs-lookup"><span data-stu-id="996fc-436">For **Google**, pass the `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="996fc-437">Per un **account Microsoft**, selezionare l'ambito `wl.offline_access`.</span><span class="sxs-lookup"><span data-stu-id="996fc-437">For **Microsoft Account**, select the `wl.offline_access` scope.</span></span>

<span data-ttu-id="996fc-438">Per aggiornare un token, chiamare `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="996fc-438">To refresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="996fc-439">Come procedura consigliata, creare un filtro che rileva una risposta 401 dal server e prova ad aggiornare il token dell'utente.</span><span class="sxs-lookup"><span data-stu-id="996fc-439">As a best practice, create a filter that detects a 401 response from the server and tries to refresh the user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="996fc-440">Accedere con l'autenticazione basata sul flusso client</span><span class="sxs-lookup"><span data-stu-id="996fc-440">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="996fc-441">Il processo generale per l'accesso con l'autenticazione basata sul flusso client è il seguente:</span><span class="sxs-lookup"><span data-stu-id="996fc-441">The general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="996fc-442">Configurare l'autenticazione e l'autorizzazione del servizio app di Azure come si configura l'autenticazione basata sul flusso server.</span><span class="sxs-lookup"><span data-stu-id="996fc-442">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="996fc-443">Integrare l'SDK del provider di autenticazione per generare un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="996fc-443">Integrate the authentication provider SDK for authentication to produce an access token.</span></span>
* <span data-ttu-id="996fc-444">Chiamare il metodo `.login()` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="996fc-444">Call the `.login()` method as follows:</span></span>

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

<span data-ttu-id="996fc-445">Sostituire il metodo `onSuccess()` con il codice che si vuole usare all'esecuzione di un accesso.</span><span class="sxs-lookup"><span data-stu-id="996fc-445">Replace the `onSuccess()` method with whatever code you wish to use on a successful login.</span></span>  <span data-ttu-id="996fc-446">La stringa `{provider}` è un provider valido: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount** o **twitter**.</span><span class="sxs-lookup"><span data-stu-id="996fc-446">The `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="996fc-447">Se è stata implementata l'autenticazione personalizzata, è anche possibile usare il tag del provider di autenticazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="996fc-447">If you have implemented custom authentication, then you can also use the custom authentication provider tag.</span></span>

### <span data-ttu-id="996fc-448"><a name="adal"></a>Autenticare gli utenti con Active Directory Authentication Library (ADAL)</span><span class="sxs-lookup"><span data-stu-id="996fc-448"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="996fc-449">È possibile usare Active Directory Authentication Library (ADAL) per far accedere gli utenti all'applicazione tramite Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="996fc-449">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="996fc-450">L'uso dell'accesso del flusso client è spesso preferibile all'uso dei metodi `loginAsync()` , perché garantisce un'esperienza utente più naturale e consente una maggiore personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="996fc-450">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="996fc-451">Configurare il back-end dell'app per dispositivi mobili per l'accesso ad Azure Active Directory seguendo l'esercitazione [Come configurare un'applicazione del servizio app per usare l'account di accesso di Azure Active Directory][22].</span><span class="sxs-lookup"><span data-stu-id="996fc-451">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="996fc-452">Assicurarsi di completare il passaggio facoltativo di registrazione di un'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="996fc-452">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="996fc-453">Installare ADAL modificando il file build.gradle per includere le definizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="996fc-453">Install ADAL by modifying your build.gradle file to include the following definitions:</span></span>

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

1. <span data-ttu-id="996fc-454">Aggiungere all'applicazione il codice seguente apportando le sostituzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="996fc-454">Add the following code to your application, making the following replacements:</span></span>

* <span data-ttu-id="996fc-455">Sostituire **INSERT-AUTHORITY-HERE** con il nome del tenant in cui è stato eseguito il provisioning dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="996fc-455">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="996fc-456">Il formato deve essere https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="996fc-456">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="996fc-457">Sostituire **INSERT-RESOURCE-ID-HERE** con l'ID client per il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="996fc-457">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="996fc-458">L'ID client è disponibile nella scheda **Avanzate** in **Impostazioni di Azure Active Directory** nel portale.</span><span class="sxs-lookup"><span data-stu-id="996fc-458">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
* <span data-ttu-id="996fc-459">Sostituire **INSERT-CLIENT-ID-HERE** con l'ID client copiato dall'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="996fc-459">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
* <span data-ttu-id="996fc-460">Sostituire **INSERT-REDIRECT-URI-HERE** con l'endpoint */.auth/login/done* del sito, usando lo schema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="996fc-460">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="996fc-461">Questo valore deve essere simile a *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="996fc-461">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

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

## <span data-ttu-id="996fc-462"><a name="filters"></a>Modificare la comunicazione client-server</span><span class="sxs-lookup"><span data-stu-id="996fc-462"><a name="filters"></a>Adjust the Client-Server Communication</span></span>

<span data-ttu-id="996fc-463">La connessione client è in genere una connessione HTTP di base che usa la libreria HTTP sottostante fornita con Android SDK.</span><span class="sxs-lookup"><span data-stu-id="996fc-463">The Client connection is normally a basic HTTP connection using the underlying HTTP library supplied with the Android SDK.</span></span>  <span data-ttu-id="996fc-464">I motivi per cui potrebbe essere necessario modificarla sono diversi:</span><span class="sxs-lookup"><span data-stu-id="996fc-464">There are several reasons why you would want to change that:</span></span>

* <span data-ttu-id="996fc-465">Si vuole usare una libreria HTTP alternativa per modificare i timeout.</span><span class="sxs-lookup"><span data-stu-id="996fc-465">You wish to use an alternate HTTP library to adjust timeouts.</span></span>
* <span data-ttu-id="996fc-466">Si vuole fornire un indicatore di stato.</span><span class="sxs-lookup"><span data-stu-id="996fc-466">You wish to provide a progress bar.</span></span>
* <span data-ttu-id="996fc-467">Si vuole aggiungere un'intestazione personalizzata per supportare la funzionalità di gestione API.</span><span class="sxs-lookup"><span data-stu-id="996fc-467">You wish to add a custom header to support API management functionality.</span></span>
* <span data-ttu-id="996fc-468">Si vuole intercettare una risposta non riuscita per poter implementare la riautenticazione.</span><span class="sxs-lookup"><span data-stu-id="996fc-468">You wish to intercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="996fc-469">Si vogliono registrare le richieste del back-end in un servizio di analisi.</span><span class="sxs-lookup"><span data-stu-id="996fc-469">You wish to log backend requests to an analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="996fc-470">Uso di una libreria HTTP alternativa</span><span class="sxs-lookup"><span data-stu-id="996fc-470">Using an alternate HTTP Library</span></span>

<span data-ttu-id="996fc-471">Chiamare il metodo `.setAndroidHttpClientFactory()` immediatamente dopo avere creato il riferimento al client.</span><span class="sxs-lookup"><span data-stu-id="996fc-471">Call the `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="996fc-472">Ad esempio, per impostare il timeout di connessione su 60 secondi, invece dei 10 secondi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="996fc-472">For example, to set the connection timeout to 60 seconds (instead of the default 10 seconds):</span></span>

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

### <a name="implement-a-progress-filter"></a><span data-ttu-id="996fc-473">Implementare un filtro per l'avanzamento</span><span class="sxs-lookup"><span data-stu-id="996fc-473">Implement a Progress Filter</span></span>

<span data-ttu-id="996fc-474">È possibile implementare un intercettazione di ogni richiesta implementando `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="996fc-474">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="996fc-475">Il codice seguente ad esempio aggiorna un indicatore stato già creato:</span><span class="sxs-lookup"><span data-stu-id="996fc-475">For example, the following updates a pre-created progress bar:</span></span>

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

<span data-ttu-id="996fc-476">È possibile collegare questo filtro al client come segue:</span><span class="sxs-lookup"><span data-stu-id="996fc-476">You can attach this filter to the client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="996fc-477">Personalizzare le intestazioni delle richieste</span><span class="sxs-lookup"><span data-stu-id="996fc-477">Customize Request Headers</span></span>

<span data-ttu-id="996fc-478">Usare l'elemento `ServiceFilter` seguente e collegare il filtro come per `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="996fc-478">Use the following `ServiceFilter` and attach the filter in the same way as the `ProgressFilter`:</span></span>

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

### <span data-ttu-id="996fc-479"><a name="conversions"></a>Configurare la serializzazione automatica</span><span class="sxs-lookup"><span data-stu-id="996fc-479"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="996fc-480">È possibile specificare una strategia di conversione che si applica a tutte le colonne tramite l'API [gson][3].</span><span class="sxs-lookup"><span data-stu-id="996fc-480">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span></span> <span data-ttu-id="996fc-481">La libreria client Android usa [gson][3] in modo invisibile per serializzare oggetti Java in dati JSON, prima che i dati vengano inviati al Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="996fc-481">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span></span>  <span data-ttu-id="996fc-482">Il codice seguente usa **setFieldNamingStrategy()** per impostare la strategia.</span><span class="sxs-lookup"><span data-stu-id="996fc-482">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span></span> <span data-ttu-id="996fc-483">Questo esempio elimina il carattere iniziale (una "m") e quindi applica il minuscolo al carattere successivo per ogni nome di campo,</span><span class="sxs-lookup"><span data-stu-id="996fc-483">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span></span> <span data-ttu-id="996fc-484">ad esempio, trasforma "mId" in "id".</span><span class="sxs-lookup"><span data-stu-id="996fc-484">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="996fc-485">Implementare una strategia di conversione per ridurre la necessità di annotazioni `SerializedName()` nella maggior parte dei campi.</span><span class="sxs-lookup"><span data-stu-id="996fc-485">Implement a conversion strategy to reduce the need for `SerializedName()` annotations on most fields.</span></span>

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

<span data-ttu-id="996fc-486">Questo codice deve essere eseguito prima di creare un riferimento al client per dispositivi mobili usando **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="996fc-486">This code must be executed before creating a mobile client reference using the **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
<span data-ttu-id="996fc-487">[Aggiungere l'autenticazione all'app Android]: app-service-mobile-android-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="996fc-487">[Get started with authentication]: app-service-mobile-android-get-started-users.md</span></span>
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
