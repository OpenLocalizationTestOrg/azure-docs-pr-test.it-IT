## <a name="clean-up-deployment"></a><span data-ttu-id="d61e3-101">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="d61e3-101">Clean up deployment</span></span> 

<span data-ttu-id="d61e3-102">Dopo l'esecuzione di script di esempio hello, comando seguire hello può essere utilizzato tooremove gruppo di risorse hello, istanza di Cache Redis di Azure e le risorse correlate nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="d61e3-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```