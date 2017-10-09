<span data-ttu-id="36e77-101">La versione 3.0 del modulo AzureRm.Resources hello incluso modifiche significative in come usano i tag.</span><span class="sxs-lookup"><span data-stu-id="36e77-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="36e77-102">Prima di continuare, controllare la versione:</span><span class="sxs-lookup"><span data-stu-id="36e77-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="36e77-103">Se i risultati mostrano versione 3.0 o versione successiva, con l'ambiente esempi hello in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="36e77-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="36e77-104">Se non è disponibile la versione 3.0 o successiva, [aggiornare la versione](/powershell/azureps-cmdlets-docs/) usando PowerShell Gallery o l'Installazione guidata piattaforma Web prima di continuare con questo argomento.</span><span class="sxs-lookup"><span data-stu-id="36e77-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="36e77-105">toosee hello tag esistenti per un *gruppo di risorse*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="36e77-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="36e77-106">Lo script restituisce hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="36e77-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="36e77-107">toosee hello tag esistenti per un *risorsa con un ID di risorsa specificato*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="36e77-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="36e77-108">In alternativa, toosee hello tag esistenti per un *risorse che dispone di un gruppo di risorse e al nome specificato*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="36e77-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="36e77-109">tooget *gruppi di risorse che dispongono di un tag specifico*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="36e77-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="36e77-110">tooget *le risorse che dispongono di un tag specifico*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="36e77-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="36e77-111">Ogni volta che si applica tag tooa risorsa o un gruppo di risorse, sovrascrivere i tag esistenti hello su tale risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="36e77-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="36e77-112">Pertanto, è necessario utilizzare un approccio diverso in base a se hello risorsa o il gruppo dispone di tag esistenti.</span><span class="sxs-lookup"><span data-stu-id="36e77-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="36e77-113">tooadd tag tooa *gruppo di risorse senza i tag esistenti*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="36e77-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="36e77-114">tooadd tag tooa *gruppo di risorse con i tag esistenti*, recuperare i tag esistenti hello, aggiungere di nuovo tag hello e riapplicare tag hello:</span><span class="sxs-lookup"><span data-stu-id="36e77-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="36e77-115">tooadd tag tooa *risorsa senza i tag esistenti*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="36e77-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="36e77-116">tooadd tag tooa *risorse con i tag esistenti*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="36e77-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="36e77-117">tooapply tutti i tag da un gruppo tooits di risorse, e *non mantenere i tag esistenti risorse hello*, utilizzare hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="36e77-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="36e77-118">tooapply tutti i tag da un gruppo tooits di risorse, e *preservare i tag esistenti su risorse che non siano duplicati*, utilizzare hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="36e77-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="36e77-119">tooremove tutti i tag, passare a una tabella di hash vuoto:</span><span class="sxs-lookup"><span data-stu-id="36e77-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



