---
title: aaaNotification hub ultime notizie esercitazione - Android
description: Informazioni su come toouse hub di notifica di Azure Service Bus toosend dispositivi tooAndroid le notifiche di notizie di rilievo.
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
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="ed309-103">Utilizzare gli hub di notifica toosend le ultime notizie</span><span class="sxs-lookup"><span data-stu-id="ed309-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="ed309-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ed309-104">Overview</span></span>
<span data-ttu-id="ed309-105">In questo argomento illustra come toouse gli hub di notifica di Azure toobroadcast ultime notizie notifiche tooan app Android.</span><span class="sxs-lookup"><span data-stu-id="ed309-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan Android app.</span></span> <span data-ttu-id="ed309-106">Al termine, verrà essere in grado di tooregister per l'interruzione delle categorie di notizie, che si è interessati e ricevere notifiche di push solo per quelle categorie.</span><span class="sxs-lookup"><span data-stu-id="ed309-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="ed309-107">Questo scenario è un modello comune per molte applicazioni in cui le notifiche hanno inviato toobe toogroups di utenti che hanno dichiarato in precedenza interesse in essi, ad esempio lettore RSS, le App per ventole musica e così via.</span><span class="sxs-lookup"><span data-stu-id="ed309-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="ed309-108">Scenari di trasmissione sono abilitati per includere uno o più *tag* durante la creazione di una registrazione nell'hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="ed309-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="ed309-109">Quando le notifiche vengono inviate tooa tag, tutti i dispositivi che sono registrati per il tag di hello riceverà la notifica hello.</span><span class="sxs-lookup"><span data-stu-id="ed309-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="ed309-110">Poiché i tag sono semplicemente stringhe, essi non è toobe in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ed309-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="ed309-111">Per ulteriori informazioni sui tag, vedere troppo[Routing hub di notifica ed espressioni Tag](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="ed309-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed309-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ed309-112">Prerequisites</span></span>
<span data-ttu-id="ed309-113">In questo argomento è basato sull'app hello è stato creato in [iniziare con gli hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="ed309-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="ed309-114">Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [Introduzione ad Hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="ed309-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="ed309-115">Aggiungi categoria selezione toohello app</span><span class="sxs-lookup"><span data-stu-id="ed309-115">Add category selection toohello app</span></span>
<span data-ttu-id="ed309-116">primo passaggio Hello è hello tooadd attività dell'interfaccia utente elementi tooyour esistente principale che consentono di hello utente tooselect categorie tooregister.</span><span class="sxs-lookup"><span data-stu-id="ed309-116">hello first step is tooadd hello UI elements tooyour existing main activity that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="ed309-117">categorie di Hello selezionate da un utente vengono archiviate nel dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ed309-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="ed309-118">Quando viene avviata l'applicazione hello, viene creata una registrazione del dispositivo nell'hub di notifica con categorie hello selezionata sotto forma di tag.</span><span class="sxs-lookup"><span data-stu-id="ed309-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="ed309-119">Aprire il file res/layout/activity_main.xml e sostituire il contenuto di hello con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="ed309-119">Open your res/layout/activity_main.xml file, and substitute hello content with hello following:</span></span>
   
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
2. <span data-ttu-id="ed309-120">Aprire il file res/values/strings.xml e aggiungere hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="ed309-120">Open your res/values/strings.xml file and add hello following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="ed309-121">A questo punto il layout grafico del file main_activity.xml dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ed309-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="ed309-122">Creare ora una classe **notifiche** nel hello stesso pacchetto come il **MainActivity** classe.</span><span class="sxs-lookup"><span data-stu-id="ed309-122">Now create a class **Notifications** in hello same package as your **MainActivity** class.</span></span>
   
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
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
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
   
    <span data-ttu-id="ed309-123">Questa classe utilizza hello archiviazione locale toostore hello le categorie di notizie, che in questo dispositivo è tooreceive.</span><span class="sxs-lookup"><span data-stu-id="ed309-123">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="ed309-124">Contiene anche metodi tooregister per queste categorie.</span><span class="sxs-lookup"><span data-stu-id="ed309-124">It also contains methods tooregister for these categories.</span></span>
4. <span data-ttu-id="ed309-125">Nella classe **MainActivity** rimuovere i campi privati per **NotificationHub** e **GoogleCloudMessaging** e aggiungere un campo per **Notifications**:</span><span class="sxs-lookup"><span data-stu-id="ed309-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="ed309-126">Quindi, nel hello **onCreate** (metodo), rimuovere l'inizializzazione di hello di hello **hub** campo e hello **registerWithNotificationHubs** metodo.</span><span class="sxs-lookup"><span data-stu-id="ed309-126">Then, in hello **onCreate** method, remove hello initialization of hello **hub** field and hello **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="ed309-127">Aggiungere quindi hello seguendo le linee che inizializza un'istanza di hello **notifiche** classe.</span><span class="sxs-lookup"><span data-stu-id="ed309-127">Then add hello following lines which initialize an instance of hello **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="ed309-128">`HubName`e `HubListenConnectionString` dovrebbero già essere impostate con hello `<hub name>` e `<connection string with listen access>` segnaposto con la notifica hub hello nome e la stringa di connessione per *DefaultListenSharedAccessSignature* ottenuto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ed309-128">`HubName` and `HubListenConnectionString` should already be set with hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="ed309-129">Poiché le credenziali che vengono distribuite con un'applicazione client non sono in genere sicure, deve essere distribuito solo chiave hello per l'accesso in ascolto con l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="ed309-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="ed309-130">Abilita accesso che tooregister l'app per le notifiche, ma le registrazioni esistenti non può essere modificato in attesa e non possono essere inviate le notifiche.</span><span class="sxs-lookup"><span data-stu-id="ed309-130">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="ed309-131">chiave di accesso completo Hello viene utilizzata in un servizio back-end protetto per l'invio di notifiche e la modifica delle registrazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="ed309-131">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="ed309-132">Aggiungere quindi hello seguente importa e `subscribe` hello toohandle metodo sottoscrizione pulsante click (evento):</span><span class="sxs-lookup"><span data-stu-id="ed309-132">Then, add hello following imports and `subscribe` method toohandle hello subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="ed309-133">Questo metodo crea un elenco di categorie e utilizza hello **notifiche** classe elenco hello toostore nella memoria locale hello e registrare i corrispondenti tag di hello con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="ed309-133">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="ed309-134">Quando vengono modificate le categorie, registrazione hello viene ricreata con le nuove categorie hello.</span><span class="sxs-lookup"><span data-stu-id="ed309-134">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="ed309-135">L'app è in grado di toostore un set di categorie in archiviazione locale nel dispositivo hello e registrare con hub di notifica hello ogni volta che le modifiche dell'utente hello hello selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="ed309-135">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="ed309-136">Registrazione per le notifiche</span><span class="sxs-lookup"><span data-stu-id="ed309-136">Register for notifications</span></span>
<span data-ttu-id="ed309-137">Questi passaggi registrare con l'hub di notifica hello all'avvio mediante le categorie di hello che sono state archiviate nel servizio di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="ed309-137">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="ed309-138">Poiché registrationId hello assegnato da Google Cloud Messaging (GCM) è possibile modificare in qualsiasi momento, è consigliabile registrare per le notifiche di frequente errori di notifica tooavoid.</span><span class="sxs-lookup"><span data-stu-id="ed309-138">Because hello registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="ed309-139">Questo esempio viene registrato per notifica ogni volta che viene avviata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ed309-139">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="ed309-140">Per le app che vengono eseguite frequentemente, più di una volta al giorno, è possibile probabilmente ignorare la larghezza di banda di registrazione toopreserve se meno di un giorno è trascorso registrazione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="ed309-140">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="ed309-141">Aggiungere hello seguente codice alla fine hello hello **onCreate** metodo hello **MainActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="ed309-141">Add hello following code at hello end of hello **onCreate** method in hello **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="ed309-142">Ciò assicura che ogni volta che viene avviata l'applicazione hello Recupera categorie hello dall'archiviazione locale e richiede una registrazione per queste categorie.</span><span class="sxs-lookup"><span data-stu-id="ed309-142">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="ed309-143">Aggiornare quindi hello `onStart()` metodo hello `MainActivity` classe come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ed309-143">Then update hello `onStart()` method of hello `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="ed309-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="ed309-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="ed309-145">}</span><span class="sxs-lookup"><span data-stu-id="ed309-145">}</span></span>
   
    <span data-ttu-id="ed309-146">Aggiorna attività principale di hello in base allo stato di hello delle categorie salvate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ed309-146">This updates hello main activity based on hello status of previously saved categories.</span></span>

<span data-ttu-id="ed309-147">app Hello è completo ed è possibile archiviare un set di categorie in hello dispositivo archiviazione locale utilizzato tooregister con hub di notifica hello ogni volta che le modifiche dell'utente hello hello selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="ed309-147">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="ed309-148">Successivamente, verrà definito un back-end che può inviare categoria notifiche toothis app.</span><span class="sxs-lookup"><span data-stu-id="ed309-148">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="ed309-149">Invio di notifiche con tag</span><span class="sxs-lookup"><span data-stu-id="ed309-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="ed309-150">Eseguire app hello e generare le notifiche</span><span class="sxs-lookup"><span data-stu-id="ed309-150">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="ed309-151">In Android Studio compilare l'applicazione hello e avviarla in un dispositivo o l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="ed309-151">In Android Studio, build hello app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="ed309-152">Si noti che app hello di che dell'interfaccia utente fornisce un set attiva o disattiva che consente di scegliere toosubscribe categorie hello per.</span><span class="sxs-lookup"><span data-stu-id="ed309-152">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="ed309-153">Abilitare uno o più interruttori di categorie e quindi fare clic su **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="ed309-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="ed309-154">applicazione Hello converte le categorie selezionata hello in tag e richiede una nuova registrazione di dispositivi per i tag hello selezionato dall'hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="ed309-154">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="ed309-155">Hello categorie registrate vengono restituite e visualizzate in una notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="ed309-155">hello registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="ed309-156">Inviare una nuova notifica tramite l'esecuzione dell'applicazione Console .NET hello.</span><span class="sxs-lookup"><span data-stu-id="ed309-156">Send a new notification by running hello .NET Console app.</span></span>  <span data-ttu-id="ed309-157">In alternativa, è possibile inviare notifiche di modello con tag utilizzo scheda debug hello di hub di notifica in hello [portale di Azure classico].</span><span class="sxs-lookup"><span data-stu-id="ed309-157">Alternatively, you can send tagged template notifications using hello debug tab of your notification hub in hello [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="ed309-158">Le notifiche per le categorie di hello selezionato vengono visualizzati come le notifiche di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="ed309-158">Notifications for hello selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed309-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed309-159">Next steps</span></span>
<span data-ttu-id="ed309-160">In questa esercitazione è stato appreso come toobroadcast le ultime notizie per categoria.</span><span class="sxs-lookup"><span data-stu-id="ed309-160">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="ed309-161">Provare a eseguire una delle seguenti esercitazioni che evidenziano altri scenari avanzati di hub di notifica hello:</span><span class="sxs-lookup"><span data-stu-id="ed309-161">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="ed309-162">[Utilizzare gli hub di notifica toobroadcast localizzata ultime notizie]</span><span class="sxs-lookup"><span data-stu-id="ed309-162">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="ed309-163">Informazioni su come hello tooexpand interrompere l'invio di notizie app tooenable localizzata notifiche.</span><span class="sxs-lookup"><span data-stu-id="ed309-163">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[Utilizzare gli hub di notifica toobroadcast localizzata ultime notizie]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[portale di Azure classico]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
