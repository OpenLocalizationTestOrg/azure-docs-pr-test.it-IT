1. <span data-ttu-id="cdd07-101">Hello Open Android SDK Manager facendo clic sull'icona di hello sulla barra degli strumenti hello di Android Studio o facendo clic **strumenti** -> **Android** -> **SDK Manager**menu hello.</span><span class="sxs-lookup"><span data-stu-id="cdd07-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="cdd07-102">Individuare la versione di destinazione hello di hello Android SDK utilizzato nel progetto, aprirla facendo **Mostra i dettagli del pacchetto**e scegliere **Google APIs**, se non è già installato.</span><span class="sxs-lookup"><span data-stu-id="cdd07-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="cdd07-103">Fare clic su hello **strumenti SDK** scheda. Se Google Play Service non è già installato, fare clic su **Google Play Services** come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="cdd07-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="cdd07-104">Quindi fare clic su **applica** tooinstall.</span><span class="sxs-lookup"><span data-stu-id="cdd07-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="cdd07-105">Si noti percorso SDK hello, per l'utilizzo in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="cdd07-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="cdd07-106">Aprire hello **gradle** file nella directory dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="cdd07-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="cdd07-107">In *dependencies*aggiungere questa riga:</span><span class="sxs-lookup"><span data-stu-id="cdd07-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="cdd07-108">Fare clic su hello **di progetto di sincronizzazione con i file Gradle** icona nella barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="cdd07-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="cdd07-109">Aprire **AndroidManifest.xml** e aggiungere questo toohello tag *applicazione* tag.</span><span class="sxs-lookup"><span data-stu-id="cdd07-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

