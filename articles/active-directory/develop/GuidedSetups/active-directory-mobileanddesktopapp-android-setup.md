---
title: aaaAzure AD v2 Android Getting Started - il programma di installazione | Documenti Microsoft
description: "Informazioni sul modo in cui un'app di Android può ottenere un token di accesso e chiamare l'API o le API Graph Microsoft che richiedono token di acceso dall'endpoint di Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="e6996-103">Configurare il progetto</span><span class="sxs-lookup"><span data-stu-id="e6996-103">Set up your project</span></span>

> <span data-ttu-id="e6996-104">Se si preferisce toodownload progetto Android Studio di questo esempio invece,</span><span class="sxs-lookup"><span data-stu-id="e6996-104">Prefer toodownload this sample's Android Studio project instead?</span></span> <span data-ttu-id="e6996-105">[Scaricare un progetto](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) e ignorare toohello [passaggio di configurazione](#create-an-application-express) tooconfigure nell'esempio di codice hello prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e6996-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="e6996-106">Creare un nuovo progetto</span><span class="sxs-lookup"><span data-stu-id="e6996-106">Create a new project</span></span> 
1.  <span data-ttu-id="e6996-107">Aprire Android Studio. Passare a `File` > `New` > `New Project`</span><span class="sxs-lookup"><span data-stu-id="e6996-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="e6996-108">Assegnare un nome all'applicazione e fare clic su `Next`</span><span class="sxs-lookup"><span data-stu-id="e6996-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="e6996-109">Verificare che tooselect *API 21 o più recente (Android 5.0)* e fare clic su`Next`</span><span class="sxs-lookup"><span data-stu-id="e6996-109">Make sure tooselect *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="e6996-110">Lasciare `Empty Activity`, fare clic su `Next` e quindi su `Finish`</span><span class="sxs-lookup"><span data-stu-id="e6996-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="e6996-111">Aggiungere hello libreria di autenticazione di Microsoft (MSAL) tooyour progetto</span><span class="sxs-lookup"><span data-stu-id="e6996-111">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1.  <span data-ttu-id="e6996-112">In Android Studio, passare a `Gradle Scripts` > `build.gradle (Module: app)`</span><span class="sxs-lookup"><span data-stu-id="e6996-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="e6996-113">Copia e Incolla seguenti di hello del codice in `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="e6996-113">Copy and paste hello following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="e6996-114">Informazioni sul pacchetto</span><span class="sxs-lookup"><span data-stu-id="e6996-114">About this package</span></span>

<span data-ttu-id="e6996-115">pacchetto Hello installa hello libreria di autenticazione di Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="e6996-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="e6996-116">MSAL gestisce l'acquisizione, la memorizzazione nella cache e l'aggiornamento utente token utilizzati tooaccess API protette da endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="e6996-116">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="e6996-117">Creare l'interfaccia utente dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e6996-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="e6996-118">Aprire `activity_main.xml` in `res` > `layout`</span><span class="sxs-lookup"><span data-stu-id="e6996-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="e6996-119">Modificare il layout di attività di hello da `android.support.constraint.ConstraintLayout` o altri troppo`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="e6996-119">Change hello activity layout from `android.support.constraint.ConstraintLayout` or other too`LinearLayout`</span></span>
3.  <span data-ttu-id="e6996-120">Aggiungere `android:orientation="vertical"` proprietà troppo`LinearLayout` nodo</span><span class="sxs-lookup"><span data-stu-id="e6996-120">Add `android:orientation="vertical"` property too`LinearLayout` node</span></span>
4.  <span data-ttu-id="e6996-121">Copia e Incolla seguenti di hello del codice in hello `LinearLayout` nodo, sostituendo il contenuto corrente di hello:</span><span class="sxs-lookup"><span data-stu-id="e6996-121">Copy and paste hello following code into hello `LinearLayout` node, replacing hello current content:</span></span>

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

