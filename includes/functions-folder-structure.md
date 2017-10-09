
<span data-ttu-id="17bb7-101">codice Hello per tutte le funzioni hello in un'app di funzione specificata si trova in una cartella radice che contiene un file di configurazione di host e le sottocartelle di uno o più, ognuna delle quali contengono codice hello per una funzione separata, come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="17bb7-101">hello code for all of hello functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain hello code for a separate function, as in hello following example:</span></span>

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

<span data-ttu-id="17bb7-102">Hello *host.json* file contiene una configurazione di runtime specifiche e si trova nella cartella radice hello di hello funzione app.</span><span class="sxs-lookup"><span data-stu-id="17bb7-102">hello *host.json* file contains some runtime-specific configuration and sits in hello root folder of hello function app.</span></span> <span data-ttu-id="17bb7-103">Per informazioni sulle impostazioni disponibili, vedere [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) nel wiki di hello WebJobs.Script repository.</span><span class="sxs-lookup"><span data-stu-id="17bb7-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in hello WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="17bb7-104">Ogni funzione presenta una cartella che contiene uno o più file di codice, configurazione function.json hello e altre dipendenze.</span><span class="sxs-lookup"><span data-stu-id="17bb7-104">Each function has a folder that contains one or more code files, hello function.json configuration and other dependencies.</span></span>

