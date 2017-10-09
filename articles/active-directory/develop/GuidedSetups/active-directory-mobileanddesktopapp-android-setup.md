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
## <a name="set-up-your-project"></a>Configurare il progetto

> Se si preferisce toodownload progetto Android Studio di questo esempio invece, [Scaricare un progetto](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) e ignorare toohello [passaggio di configurazione](#create-an-application-express) tooconfigure nell'esempio di codice hello prima dell'esecuzione.


### <a name="create-a-new-project"></a>Creare un nuovo progetto 
1.  Aprire Android Studio. Passare a `File` > `New` > `New Project`
2.  Assegnare un nome all'applicazione e fare clic su `Next`
3.  Verificare che tooselect *API 21 o più recente (Android 5.0)* e fare clic su`Next`
4.  Lasciare `Empty Activity`, fare clic su `Next` e quindi su `Finish`


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Aggiungere hello libreria di autenticazione di Microsoft (MSAL) tooyour progetto
1.  In Android Studio, passare a `Gradle Scripts` > `build.gradle (Module: app)`
2.  Copia e Incolla seguenti di hello del codice in `Dependencies`:

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a>Informazioni sul pacchetto

pacchetto Hello installa hello libreria di autenticazione di Microsoft (MSAL). MSAL gestisce l'acquisizione, la memorizzazione nella cache e l'aggiornamento utente token utilizzati tooaccess API protette da endpoint di Azure Active Directory v2.
<!--end-collapse-->

## <a name="create-your-applications-ui"></a>Creare l'interfaccia utente dell'applicazione

1.  Aprire `activity_main.xml` in `res` > `layout`
2.  Modificare il layout di attività di hello da `android.support.constraint.ConstraintLayout` o altri troppo`LinearLayout`
3.  Aggiungere `android:orientation="vertical"` proprietà troppo`LinearLayout` nodo
4.  Copia e Incolla seguenti di hello del codice in hello `LinearLayout` nodo, sostituendo il contenuto corrente di hello:

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

