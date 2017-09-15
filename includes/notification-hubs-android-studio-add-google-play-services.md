1. <span data-ttu-id="6eed8-101">Aprire Android SDK Manager facendo clic sull'icona della barra degli strumenti di Android Studio o su **Strumenti** -> **Android** -> **SDK Manager** nel menu.</span><span class="sxs-lookup"><span data-stu-id="6eed8-101">Open the Android SDK Manager by clicking the icon on the toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on the menu.</span></span> <span data-ttu-id="6eed8-102">Trovare la versione di destinazione di Android SDK usata nel progetto, aprirla facendo clic su **Show Package Details** (Visualizza dettagli pacchetto) e quindi scegliere **Google APIs** (API Google), se non è già installato.</span><span class="sxs-lookup"><span data-stu-id="6eed8-102">Locate the target version of the Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="6eed8-103">Fare sulla scheda **SDK Tools** .</span><span class="sxs-lookup"><span data-stu-id="6eed8-103">Click the **SDK Tools** tab.</span></span> <span data-ttu-id="6eed8-104">Se Google Play Service non è già installato, fare clic su **Google Play Services** come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6eed8-104">If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="6eed8-105">Fare quindi clic su **Apply** per installarlo.</span><span class="sxs-lookup"><span data-stu-id="6eed8-105">Then click **Apply** to install.</span></span> 
   
    <span data-ttu-id="6eed8-106">Prendere nota del percorso dell'SDK per l'uso in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="6eed8-106">Note the SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="6eed8-107">Aprire il file **build.gradle** nella directory dell'app.</span><span class="sxs-lookup"><span data-stu-id="6eed8-107">Open the **build.gradle** file in the app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="6eed8-108">In *dependencies*aggiungere questa riga:</span><span class="sxs-lookup"><span data-stu-id="6eed8-108">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="6eed8-109">Fare clic sul pulsante **Sync Project with Gradle Files** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="6eed8-109">Click the **Sync Project with Gradle Files** icon in the tool bar.</span></span>
6. <span data-ttu-id="6eed8-110">Aprire **AndroidManifest.xml** e aggiungere il tag seguente al tag *application* .</span><span class="sxs-lookup"><span data-stu-id="6eed8-110">Open **AndroidManifest.xml** and add this tag to the *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

