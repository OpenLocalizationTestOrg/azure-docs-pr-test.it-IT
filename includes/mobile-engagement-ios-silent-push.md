> [!IMPORTANT]
> <span data-ttu-id="048d6-101">le notifiche Push da Mobile Engagement tooreceive, è necessario tooenable `Silent Remote Notifications` nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="048d6-101">tooreceive Push Notifications from Mobile Engagement, you need tooenable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="048d6-102">È necessario la matrice UIBackgroundModes tooadd hello remoto notifica valore toohello nel file Info. plist.</span><span class="sxs-lookup"><span data-stu-id="048d6-102">You need tooadd hello remote-notification value toohello UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="048d6-103">Aprire `info.plist` file nel progetto hello</span><span class="sxs-lookup"><span data-stu-id="048d6-103">Open `info.plist` file in hello project</span></span>
2. <span data-ttu-id="048d6-104">Fare clic con il pulsante destro su hello prima voce elenco hello (`Information Property List`) e aggiungere una nuova riga</span><span class="sxs-lookup"><span data-stu-id="048d6-104">Right click on hello top item in hello list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="048d6-105">Nella nuova riga hello immettere`Required background modes`</span><span class="sxs-lookup"><span data-stu-id="048d6-105">In hello new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="048d6-106">Fare clic sulla riga hello tooexpand di hello freccia sinistra</span><span class="sxs-lookup"><span data-stu-id="048d6-106">Click on hello left arrow tooexpand hello row</span></span>
5. <span data-ttu-id="048d6-107">Aggiungere hello seguente elemento toohello valore 0`App downloads content in response toopush notifications`</span><span class="sxs-lookup"><span data-stu-id="048d6-107">Add hello following value toohello item 0 `App downloads content in response toopush notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="048d6-108">Dopo aver modificato hello, Info. plist hello XML deve contenere hello seguente chiave e valore:</span><span class="sxs-lookup"><span data-stu-id="048d6-108">Once you make hello change, hello info.plist XML should contain hello following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="048d6-109">Se si usano **Xcode 7+** e **iOS 9+**:</span><span class="sxs-lookup"><span data-stu-id="048d6-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="048d6-110">Abilitare **Notifiche push** in Destinazioni > Nome destinazione > Funzionalità.</span><span class="sxs-lookup"><span data-stu-id="048d6-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

