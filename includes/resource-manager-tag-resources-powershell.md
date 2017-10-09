La versione 3.0 del modulo AzureRm.Resources hello incluso modifiche significative in come usano i tag. Prima di continuare, controllare la versione:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Se i risultati mostrano versione 3.0 o versione successiva, con l'ambiente esempi hello in questo argomento. Se non è disponibile la versione 3.0 o successiva, [aggiornare la versione](/powershell/azureps-cmdlets-docs/) usando PowerShell Gallery o l'Installazione guidata piattaforma Web prima di continuare con questo argomento.

```powershell
Version
-------
3.5.0
```

toosee hello tag esistenti per un *gruppo di risorse*, utilizzare:

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

Lo script restituisce hello seguente formato:

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

toosee hello tag esistenti per un *risorsa con un ID di risorsa specificato*, utilizzare:

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

In alternativa, toosee hello tag esistenti per un *risorse che dispone di un gruppo di risorse e al nome specificato*, utilizzare:

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget *gruppi di risorse che dispongono di un tag specifico*, utilizzare:

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget *le risorse che dispongono di un tag specifico*, utilizzare:

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

Ogni volta che si applica tag tooa risorsa o un gruppo di risorse, sovrascrivere i tag esistenti hello su tale risorsa o un gruppo di risorse. Pertanto, è necessario utilizzare un approccio diverso in base a se hello risorsa o il gruppo dispone di tag esistenti. 

tooadd tag tooa *gruppo di risorse senza i tag esistenti*, utilizzare:

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

tooadd tag tooa *gruppo di risorse con i tag esistenti*, recuperare i tag esistenti hello, aggiungere di nuovo tag hello e riapplicare tag hello:

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

tooadd tag tooa *risorsa senza i tag esistenti*, utilizzare:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooadd tag tooa *risorse con i tag esistenti*, utilizzare:

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooapply tutti i tag da un gruppo tooits di risorse, e *non mantenere i tag esistenti risorse hello*, utilizzare hello lo script seguente:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

tooapply tutti i tag da un gruppo tooits di risorse, e *preservare i tag esistenti su risorse che non siano duplicati*, utilizzare hello lo script seguente:

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

tooremove tutti i tag, passare a una tabella di hash vuoto:

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



