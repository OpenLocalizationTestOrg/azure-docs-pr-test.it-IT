> [!IMPORTANT]
> <span data-ttu-id="a45a1-101">Per ricevere le notifiche push da Mobile Engagement, è necessario abilitare `Silent Remote Notifications` nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a45a1-101">To receive Push Notifications from Mobile Engagement, you need to enable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="a45a1-102">È necessario aggiungere il valore di notifica remota alla matrice UIBackgroundModes nel file Info.plist.</span><span class="sxs-lookup"><span data-stu-id="a45a1-102">You need to add the remote-notification value to the UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="a45a1-103">Aprire il file `info.plist` del progetto.</span><span class="sxs-lookup"><span data-stu-id="a45a1-103">Open `info.plist` file in the project</span></span>
2. <span data-ttu-id="a45a1-104">Fare clic con il pulsante destro del mouse sul primo elemento dell'elenco (`Information Property List`) e aggiungere una nuova riga.</span><span class="sxs-lookup"><span data-stu-id="a45a1-104">Right click on the top item in the list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="a45a1-105">Nella nuova riga immettere `Required background modes`</span><span class="sxs-lookup"><span data-stu-id="a45a1-105">In the new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="a45a1-106">Fare clic sulla freccia sinistra per espandere la riga.</span><span class="sxs-lookup"><span data-stu-id="a45a1-106">Click on the left arrow to expand the row</span></span>
5. <span data-ttu-id="a45a1-107">Aggiungere il seguente valore all'elemento 0 `App downloads content in response to push notifications`</span><span class="sxs-lookup"><span data-stu-id="a45a1-107">Add the following value to the item 0 `App downloads content in response to push notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="a45a1-108">Dopo avere apportato la modifica, info.plist XML deve contenere la chiave e il valore seguenti:</span><span class="sxs-lookup"><span data-stu-id="a45a1-108">Once you make the change, the info.plist XML should contain the following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="a45a1-109">Se si usano **Xcode 7+** e **iOS 9+**:</span><span class="sxs-lookup"><span data-stu-id="a45a1-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="a45a1-110">Abilitare **Notifiche push** in Destinazioni > Nome destinazione > Funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a45a1-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

