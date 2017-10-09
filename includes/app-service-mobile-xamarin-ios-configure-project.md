#### <a name="configure-hello-ios-project-in-xamarin-studio"></a><span data-ttu-id="12afe-101">Configurazione progetto iOS hello in Studio a Xamarin</span><span class="sxs-lookup"><span data-stu-id="12afe-101">Configure hello iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="12afe-102">In Xamarin.Studio, aprire **Info. plist**e aggiornamento hello **identificatore Bundle** con hello aggregare ID creato in precedenza con il nuovo ID di app.</span><span class="sxs-lookup"><span data-stu-id="12afe-102">In Xamarin.Studio, open **Info.plist**, and update hello **Bundle Identifier** with hello bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="12afe-103">Scorrere verso il basso troppo**modalità di Background**.</span><span class="sxs-lookup"><span data-stu-id="12afe-103">Scroll down too**Background Modes**.</span></span> <span data-ttu-id="12afe-104">Seleziona hello **abilitare la modalità di Background** casella e hello **notifiche Remote** casella.</span><span class="sxs-lookup"><span data-stu-id="12afe-104">Select hello **Enable Background Modes** box and hello **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="12afe-105">Fare doppio clic sul progetto in hello soluzione pannello tooopen **opzioni progetto**.</span><span class="sxs-lookup"><span data-stu-id="12afe-105">Double-click your project in hello Solution Panel tooopen **Project Options**.</span></span>
4. <span data-ttu-id="12afe-106">In **compilare**, scegliere **firma Bundle iOS**e selezionare hello identità corrispondente e profilo di provisioning è sufficiente impostare per questo progetto.</span><span class="sxs-lookup"><span data-stu-id="12afe-106">Under **Build**, choose **iOS Bundle Signing**, and select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="12afe-107">In questo modo che il progetto hello utilizza nuovo profilo hello per la firma del codice.</span><span class="sxs-lookup"><span data-stu-id="12afe-107">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="12afe-108">Per hello ufficiale Xamarin provisioning dei dispositivi documentazione, vedere [Provisioning dei dispositivi Xamarin].</span><span class="sxs-lookup"><span data-stu-id="12afe-108">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-hello-ios-project-in-visual-studio"></a><span data-ttu-id="12afe-109">Configurare il progetto di iOS hello in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="12afe-109">Configure hello iOS project in Visual Studio</span></span>
1. <span data-ttu-id="12afe-110">In Visual Studio, fare clic sul progetto hello e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="12afe-110">In Visual Studio, right-click hello project, and then click **Properties**.</span></span>
2. <span data-ttu-id="12afe-111">Nelle pagine delle proprietà hello, fare clic su hello **applicazione iOS** scheda e aggiornamento hello **identificatore** con ID hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="12afe-111">In hello properties pages, click hello **iOS Application** tab, and update hello **Identifier** with hello ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="12afe-112">In hello **firma Bundle iOS** scheda identità corrispondenti selezionare hello e provisioning profilo è solo set di backup per questo progetto.</span><span class="sxs-lookup"><span data-stu-id="12afe-112">In hello **iOS Bundle Signing** tab, select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="12afe-113">In questo modo che il progetto hello utilizza nuovo profilo hello per la firma del codice.</span><span class="sxs-lookup"><span data-stu-id="12afe-113">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="12afe-114">Per hello ufficiale Xamarin provisioning dei dispositivi documentazione, vedere [Provisioning dei dispositivi Xamarin].</span><span class="sxs-lookup"><span data-stu-id="12afe-114">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="12afe-115">Fare doppio clic sul file Info. plist tooopen e quindi abilitare **RemoteNotifications** in **modalità di Background**.</span><span class="sxs-lookup"><span data-stu-id="12afe-115">Double-click Info.plist tooopen it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

[Provisioning dei dispositivi Xamarin]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
