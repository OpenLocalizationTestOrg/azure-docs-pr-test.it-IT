<span data-ttu-id="d574c-101">Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="d574c-101">Every blob in Azure storage must reside in a container.</span></span> <span data-ttu-id="d574c-102">Hello contenitore fa parte del nome blob hello.</span><span class="sxs-lookup"><span data-stu-id="d574c-102">hello container forms part of hello blob name.</span></span> <span data-ttu-id="d574c-103">Ad esempio, `mycontainer` hello nome del contenitore di hello in questi blob URI di esempio:</span><span class="sxs-lookup"><span data-stu-id="d574c-103">For example, `mycontainer` is hello name of hello container in these sample blob URIs:</span></span>

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

<span data-ttu-id="d574c-104">Un nome di contenitore deve essere un nome DNS valido, toohello conforme alle regole di denominazione:</span><span class="sxs-lookup"><span data-stu-id="d574c-104">A container name must be a valid DNS name, conforming toohello following naming rules:</span></span>

1. <span data-ttu-id="d574c-105">Il nome del contenitore devono iniziare con una lettera o un numero e possono contenere solo lettere, numeri e hello trattino (-).</span><span class="sxs-lookup"><span data-stu-id="d574c-105">Container names must start with a letter or number, and can contain only letters, numbers, and hello dash (-) character.</span></span>
2. <span data-ttu-id="d574c-106">Ciascun carattere trattino (-) deve essere immediatamente preceduto e seguito da una lettera o un numero: nei nomi dei contenitori non sono consentiti trattini consecutivi.</span><span class="sxs-lookup"><span data-stu-id="d574c-106">Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.</span></span>
3. <span data-ttu-id="d574c-107">Tutte le lettere in un nome di contenitore deve essere composto solo da minuscole.</span><span class="sxs-lookup"><span data-stu-id="d574c-107">All letters in a container name must be lowercase.</span></span>
4. <span data-ttu-id="d574c-108">La lunghezza dei nomi dei contenitori deve essere compresa tra 3 e 63 caratteri.</span><span class="sxs-lookup"><span data-stu-id="d574c-108">Container names must be from 3 through 63 characters long.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d574c-109">Si noti che hello nome di un contenitore deve essere sempre in minuscolo.</span><span class="sxs-lookup"><span data-stu-id="d574c-109">Note that hello name of a container must always be lowercase.</span></span> <span data-ttu-id="d574c-110">Se si include una lettera maiuscola in un nome di contenitore o in caso contrario violano le regole di denominazione di hello contenitore, si potrebbe ricevere un errore 400 (richiesta non valida).</span><span class="sxs-lookup"><span data-stu-id="d574c-110">If you include an upper-case letter in a container name, or otherwise violate hello container naming rules, you may receive a 400 error (Bad Request).</span></span> 
> 
> 

