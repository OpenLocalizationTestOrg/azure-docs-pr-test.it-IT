### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="bebb9-101">Risolvere i problemi relativi a Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="bebb9-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="bebb9-102">Se si riceve hello seguente messaggio di errore, non è registrato alcun provider di risorse Insights hello:</span><span class="sxs-lookup"><span data-stu-id="bebb9-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="bebb9-103">provider di risorse tooregister hello, eseguire hello in hello portale di Azure come segue:</span><span class="sxs-lookup"><span data-stu-id="bebb9-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="bebb9-104">Nel riquadro di spostamento hello hello sinistra, fare clic su *sottoscrizioni*</span><span class="sxs-lookup"><span data-stu-id="bebb9-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="bebb9-105">Selezionare la sottoscrizione di hello identificata nel messaggio di errore hello</span><span class="sxs-lookup"><span data-stu-id="bebb9-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="bebb9-106">Fare clic su *Provider di risorse*.</span><span class="sxs-lookup"><span data-stu-id="bebb9-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="bebb9-107">Trovare hello *Insights* provider</span><span class="sxs-lookup"><span data-stu-id="bebb9-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="bebb9-108">Fare clic su hello *registrare* collegamento</span><span class="sxs-lookup"><span data-stu-id="bebb9-108">Click hello *Register* link</span></span>

![Registrare il provider di risorse Microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="bebb9-110">Una volta hello *Insights* provider di risorse è registrato, nuovo tentativo di configurazione della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="bebb9-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="bebb9-111">In PowerShell, se si riceve hello seguente messaggio di errore, occorre tooupdate la versione di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bebb9-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="bebb9-112">Aggiornare la versione di PowerShell toohello novembre 2016 (v2.3.0) o versione successiva, rilasciare seguendo le istruzioni di hello nella hello [Introduzione ai cmdlet di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) articolo.</span><span class="sxs-lookup"><span data-stu-id="bebb9-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
