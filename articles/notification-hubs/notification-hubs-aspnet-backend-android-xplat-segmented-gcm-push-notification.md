---
title: Esercitazione sull'invio di ultime notizie mediante Hub di notifica - Android
description: Informazioni su come usare Hub di notifica di Bus di servizio di Azure per inviare notifiche relative alle ultime notizie a dispositivi Android.
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76ec01c874fceedab7d76b2ef58e4b45b5489f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="19765-103">Uso di Hub di notifica per inviare le ultime notizie</span><span class="sxs-lookup"><span data-stu-id="19765-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="19765-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="19765-104">Overview</span></span>
<span data-ttu-id="19765-105">Questo argomento illustra come usare Hub di notifica di Azure per trasmettere le notifiche relative alle ultime notizie a un'app per Android.</span><span class="sxs-lookup"><span data-stu-id="19765-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span></span> <span data-ttu-id="19765-106">Al termine dell'esercitazione, si sarà appreso a effettuare la registrazione alle categorie di ultime notizie desiderate e ricevere le notifiche push solo da tali categorie.</span><span class="sxs-lookup"><span data-stu-id="19765-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="19765-107">Questo scenario è un modello comune per molte app nelle quali le notifiche devono essere inviate a gruppi di utenti che hanno dichiarato un interesse, ad esempio lettori di feed RSS, app per fan di musica e così via.</span><span class="sxs-lookup"><span data-stu-id="19765-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="19765-108">È possibile abilitare gli scenari di trasmissione includendo uno o più *tag* durante la creazione di una registrazione nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="19765-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="19765-109">Quando le notifiche vengono inviate a un tag, tutti i dispositivi che hanno effettuato la registrazione al tag riceveranno la notifica.</span><span class="sxs-lookup"><span data-stu-id="19765-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="19765-110">Poiché i tag sono costituiti da stringhe, non è necessario eseguire il provisioning anticipatamente.</span><span class="sxs-lookup"><span data-stu-id="19765-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="19765-111">Per ulteriori informazioni sui tag, vedere [Espressioni di routing e tag  per hub di notifica](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="19765-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19765-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="19765-112">Prerequisites</span></span>
<span data-ttu-id="19765-113">Questo argomento si basa sull'app creata nell'esercitazione [Introduzione ad Hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="19765-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="19765-114">Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [Introduzione ad Hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="19765-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="19765-115">Aggiungere la selezione delle categorie all'app</span><span class="sxs-lookup"><span data-stu-id="19765-115">Add category selection to the app</span></span>
<span data-ttu-id="19765-116">Il primo passaggio prevede l'aggiunta degli elementi dell'interfaccia utente all'attività principale esistente per consentire all'utente di selezionare le categorie per le quali registrarsi.</span><span class="sxs-lookup"><span data-stu-id="19765-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span></span> <span data-ttu-id="19765-117">Le categorie selezionate da un utente sono archiviate nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="19765-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="19765-118">All'avvio dell'app, viene creata una registrazione nell'hub di notifica con le categorie selezionate come tag.</span><span class="sxs-lookup"><span data-stu-id="19765-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="19765-119">Aprire il file res/layout/activity_main.xml e sostituire il contenuto con il seguente:</span><span class="sxs-lookup"><span data-stu-id="19765-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span></span>
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. <span data-ttu-id="19765-120">Aprire il file res/values/strings.xml e aggiungere le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="19765-120">Open your res/values/strings.xml file and add the following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="19765-121">A questo punto il layout grafico del file main_activity.xml dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="19765-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="19765-122">Creare una classe **Notifications** nello stesso pacchetto della classe **MainActivity**.</span><span class="sxs-lookup"><span data-stu-id="19765-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span></span>
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed to register - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    <span data-ttu-id="19765-123">Questa classe utilizza l'archiviazione locale per archiviare le categorie di notizie che il dispositivo deve ricevere.</span><span class="sxs-lookup"><span data-stu-id="19765-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="19765-124">Contiene inoltre i metodi per effettuare la registrazione per queste categorie.</span><span class="sxs-lookup"><span data-stu-id="19765-124">It also contains methods to register for these categories.</span></span>
4. <span data-ttu-id="19765-125">Nella classe **MainActivity** rimuovere i campi privati per **NotificationHub** e **GoogleCloudMessaging** e aggiungere un campo per **Notifications**:</span><span class="sxs-lookup"><span data-stu-id="19765-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="19765-126">A questo punto, nel metodo **onCreate** rimuovere l'inizializzazione del campo **hub** e il metodo **registerWithNotificationHubs**.</span><span class="sxs-lookup"><span data-stu-id="19765-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="19765-127">Aggiungere quindi le righe seguenti, che inizializzano un'istanza della classe **Notifications** .</span><span class="sxs-lookup"><span data-stu-id="19765-127">Then add the following lines which initialize an instance of the **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="19765-128">`HubName` e `HubListenConnectionString` dovrebbero già essere impostati con i segnaposto `<hub name>` e `<connection string with listen access>` con il nome dell’hub di notifica e la stringa di connessione per *DefaultListenSharedAccessSignature* impostata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="19765-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="19765-129">Poiché le credenziali che sono distribuite con un'app client in genere non sono sicure, distribuire solo la chiave per l'accesso Listen con l'app client.</span><span class="sxs-lookup"><span data-stu-id="19765-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="19765-130">L'accesso Listen consente all'app di registrarsi per le notifiche ma le registrazioni esistenti non possono essere modificate e le notifiche non possono essere inviate.</span><span class="sxs-lookup"><span data-stu-id="19765-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="19765-131">La chiave di accesso completa viene utilizzata in un servizio back-end sicuro per l'invio delle notifiche e la modifica delle registrazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="19765-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="19765-132">Quindi, aggiungere le seguenti importazioni e metodo `subscribe` per gestire l’evento clic del pulsante sottoscrivi:</span><span class="sxs-lookup"><span data-stu-id="19765-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span></span>
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    <span data-ttu-id="19765-133">Questo metodo crea un elenco di categorie e utilizza la classe **Notifications** per archiviare l'elenco nell'archiviazione locale e registrare i tag corrispondenti nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="19765-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="19765-134">Se le categorie vengono modificate, la registrazione viene ricreata con le nuove categorie.</span><span class="sxs-lookup"><span data-stu-id="19765-134">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="19765-135">L'app può quindi archiviare un set di categorie nell'archiviazione locale del dispositivo ed effettuare la registrazione con l'hub di notifica ogni volta che l'utente modifica la selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="19765-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="19765-136">Registrazione per le notifiche</span><span class="sxs-lookup"><span data-stu-id="19765-136">Register for notifications</span></span>
<span data-ttu-id="19765-137">Questa procedura consente di effettuare la registrazione con l'hub di notifica all'avvio usando le categorie archiviate nella risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="19765-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="19765-138">Poiché il valore di registrationId assegnato da Google Cloud Messaging (GCM) può cambiare in qualsiasi momento, è necessario ripetere la registrazione per le notifiche di frequente per evitare errori di notifica.</span><span class="sxs-lookup"><span data-stu-id="19765-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="19765-139">In questo esempio viene effettuata la registrazione per le notifiche a ogni avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="19765-139">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="19765-140">Per le app che vengono eseguite di frequente, oltre una volta al giorno, è possibile ignorare la registrazione per conservare la larghezza di banda qualora sia trascorso meno di un giorno dalla registrazione precedente.</span><span class="sxs-lookup"><span data-stu-id="19765-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="19765-141">Aggiungere questo codice alla fine del metodo **onCreate** nella classe **MainActivity**:</span><span class="sxs-lookup"><span data-stu-id="19765-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="19765-142">In questo modo, ogni volta che l'app viene avviata vengono recuperate le categorie dall'archiviazione locale e viene richiesta una registrazione per queste categorie.</span><span class="sxs-lookup"><span data-stu-id="19765-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="19765-143">Aggiornare quindi il metodo `onStart()` della classe `MainActivity` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="19765-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="19765-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="19765-144">@Override  protected void onStart() {</span></span>
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    <span data-ttu-id="19765-145">}</span><span class="sxs-lookup"><span data-stu-id="19765-145">}</span></span>
   
    <span data-ttu-id="19765-146">L'attività principale viene aggiornata in base allo stato delle categorie salvate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="19765-146">This updates the main activity based on the status of previously saved categories.</span></span>

<span data-ttu-id="19765-147">Ora l'app è completa e può quindi archiviare un set di categorie nell'archiviazione locale del dispositivo ed effettuare la registrazione con l'hub di notifica ogni volta che l'utente modifica la selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="19765-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="19765-148">Verrà ora definito un back-end per l'invio delle notifiche delle categorie all'app.</span><span class="sxs-lookup"><span data-stu-id="19765-148">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="19765-149">Invio di notifiche con tag</span><span class="sxs-lookup"><span data-stu-id="19765-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="19765-150">Eseguire l'app e generare notifiche</span><span class="sxs-lookup"><span data-stu-id="19765-150">Run the app and generate notifications</span></span>
1. <span data-ttu-id="19765-151">In Android Studio, compilare l'app e avviarla in un dispositivo o emulatore.</span><span class="sxs-lookup"><span data-stu-id="19765-151">In Android Studio, build the app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="19765-152">Si noti che l'interfaccia utente dell'app fornisce un set di interruttori che consentono di scegliere le categorie per le quali effettuare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="19765-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="19765-153">Abilitare uno o più interruttori di categorie e quindi fare clic su **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="19765-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="19765-154">L'app converte le categorie selezionate in tag e richiede una nuova registrazione del dispositivo per i tag selezionati dall'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="19765-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="19765-155">Le categorie registrate vengono restituite e visualizzate in notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="19765-155">The registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="19765-156">Inviare una nuova notifica eseguendo l'app .NET Console.</span><span class="sxs-lookup"><span data-stu-id="19765-156">Send a new notification by running the .NET Console app.</span></span>  <span data-ttu-id="19765-157">In alternativa, è possibile inviare notifiche modello con tag usando la scheda debug dell'hub di notifica nel [portale di Azure classico].</span><span class="sxs-lookup"><span data-stu-id="19765-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="19765-158">Le notifiche per le categorie selezionate vengono visualizzate come notifiche di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="19765-158">Notifications for the selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19765-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="19765-159">Next steps</span></span>
<span data-ttu-id="19765-160">In questa esercitazione si è appreso a trasmettere le ultime novità per categoria.</span><span class="sxs-lookup"><span data-stu-id="19765-160">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="19765-161">Per informazioni su altri scenari avanzati di Hub di notifica, provare a completare le seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="19765-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="19765-162">[Usare Hub di notifica per la trasmissione di notizie localizzate]</span><span class="sxs-lookup"><span data-stu-id="19765-162">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="19765-163">Informazioni su come espandere l'app relativa alle ultime novità per abilitare l'invio di notifiche localizzate.</span><span class="sxs-lookup"><span data-stu-id="19765-163">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
<span data-ttu-id="19765-164">[Usare Hub di notifica per la trasmissione di notizie localizzate]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="19765-164">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="19765-165">[portale di Azure classico]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="19765-165">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
