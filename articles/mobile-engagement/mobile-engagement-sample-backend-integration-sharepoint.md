---
title: aaaAzure Engagement Mobile - integrazione back-end
description: La connessione di Azure Mobile Engagement con un back-end di SharePoint toocreate le campagne da SharePoint
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 06297b43-579f-46e6-8a58-961a68f9aa09
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 89e1ef57db607d63c326a760b20260ad439f08b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="da73d-103">Azure Mobile Engagement - Integrazione di API</span><span class="sxs-lookup"><span data-stu-id="da73d-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="da73d-104">In un sistema automatizzato di marketing, creazione e l'attivazione di hello anche le campagne di marketing si verificano automaticamente.</span><span class="sxs-lookup"><span data-stu-id="da73d-104">In an automated marketing system, creating and activating hello marketing campaigns also occur automatically.</span></span> <span data-ttu-id="da73d-105">A questo scopo, Azure Mobile Engagement permette la creazione di tali campagne marketing automatizzate anche mediante le API.</span><span class="sxs-lookup"><span data-stu-id="da73d-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="da73d-106">I clienti utilizzano in genere hello Mobile Engagement front-end interfaccia toocreate annunci o sondaggi e così via come parte le campagne di marketing.</span><span class="sxs-lookup"><span data-stu-id="da73d-106">Typically customers use hello Mobile Engagement front end interface toocreate announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="da73d-107">Tuttavia, come hello diventare mature campagne di marketing, è necessario tooleverage hello il blocco dei dati nei sistemi back-end hello (ad esempio, un sistema CRM o CMS come SharePoint) in modo che sia possibile creare una pipeline completamente automatizzata che consente di creare campagne in dispositivi mobili Engagement in modo dinamico in base ai dati di hello trasmessi dai sistemi back-end hello.</span><span class="sxs-lookup"><span data-stu-id="da73d-107">However as hello marketing campaigns become mature, there is a need tooleverage hello data locked in hello backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on hello data flowing in from hello backend systems.</span></span> 

![][5]

<span data-ttu-id="da73d-108">Questa esercitazione sarà inviato tramite una situazione in cui un utente di business di SharePoint consente di popolare un elenco di SharePoint con dati di marketing e un processo automatizzato preleva gli elementi elenco hello e si connette con hello Mobile Engagement sistema con hello disponibili API REST toocreate una campagna di marketing dai dati di SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="da73d-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from hello list and connects with hello Mobile Engagement system using hello available REST APIs toocreate a marketing campaign from hello SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="da73d-109">In generale, è possibile utilizzare questo esempio come punto di partenza per comprendere come toocall qualsiasi API REST di Engagement Mobile come dettagli hello due gli aspetti chiave della chiamata hello API - autenticazione e passando i parametri.</span><span class="sxs-lookup"><span data-stu-id="da73d-109">In general, you can use this sample as a starting point for understanding how toocall any Mobile Engagement REST API as it details hello two key aspects of calling hello APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="da73d-110">Integrazione con SharePoint</span><span class="sxs-lookup"><span data-stu-id="da73d-110">SharePoint integration</span></span>
1. <span data-ttu-id="da73d-111">Ecco quali esempio hello è simile a elenco SharePoint.</span><span class="sxs-lookup"><span data-stu-id="da73d-111">Here is what hello sample SharePoint list looks like.</span></span> <span data-ttu-id="da73d-112">**Titolo**, **categoria**, **NotificationTitle**, **messaggio** e **URL** vengono utilizzati per creare l'annuncio hello.</span><span class="sxs-lookup"><span data-stu-id="da73d-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating hello announcement.</span></span> <span data-ttu-id="da73d-113">È una colonna denominata **IsProcessed** che viene utilizzato dal processo di automazione di esempio hello sotto forma di hello di un programma di console.</span><span class="sxs-lookup"><span data-stu-id="da73d-113">There is a column called **IsProcessed** which is used by hello sample automation process in hello form of a console program.</span></span> <span data-ttu-id="da73d-114">È possibile eseguire il programma di console come un processo Web di Azure in modo che è possibile eseguire la pianificazione o è possibile utilizzare direttamente la creazione di hello SharePoint del flusso di lavoro tooprogram e l'attivazione annuncio hello quando un elemento viene inserito nell'elenco di SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="da73d-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use hello SharePoint workflow tooprogram creating and activating hello announcement when an item is inserted into hello SharePoint list.</span></span> <span data-ttu-id="da73d-115">In questo esempio viene utilizzato programma console hello che passa tra gli elementi di hello hello SharePoint elencare e creare l'annuncio in Azure Mobile Engagement per ognuno di essi e quindi contrassegna infine hello **IsProcessed** true toobe flag creazione di un annuncio ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="da73d-115">In this sample we use hello console program which goes through hello items in hello SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks hello **IsProcessed** flag toobe true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="da73d-116">Si sta usando codice hello tratto dall'esempio hello *autenticazione remota in SharePoint Online usando hello modello a oggetti Client* [qui](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate con elenco di SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="da73d-116">We are using hello code from hello sample *Remote Authentication in SharePoint Online Using hello Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate with hello SharePoint list.</span></span>
3. <span data-ttu-id="da73d-117">Una volta autenticato, il ciclo tramite hello elenco elementi toofind gli eventuali elementi appena creati (che avrà **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="da73d-117">Once authenticated, we loop through hello list items toofind out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
         static async void CreateCampaignFromSharepoint()
        {
            using (ClientContext clientContext = ClaimClientContext.GetAuthenticatedContext(targetSharepointSite))
            {
                // Using https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c for authentication     
                Web site = clientContext.Web;
                List list = site.Lists.GetByTitle("VideoContent");
                CamlQuery query = new CamlQuery();
                query.ViewXml = "<View/>";
                ListItemCollection items = list.GetItems(query);
   
                // Load hello SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through hello list toogo through all hello items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request toocreate AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this tootrue
                            item["IsProcessed"] = "Yes";
   
                            // Now try tooactivate hello campaign also
                            await ActivateAzMECampaign(campaignId);
                        }
                        else
                        {
                            item["IsProcessed"] = "Error";
                        }
                        item.Update();
                    }
                clientContext.ExecuteQuery();
            }
        }

## <a name="mobile-engagement-integration"></a><span data-ttu-id="da73d-118">Integrazione con Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="da73d-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="da73d-119">Una volta che si trova un elemento che richiede l'elaborazione, si estrarre informazioni hello necessarie toocreate un annuncio hello voce di elenco e chiamare `CreateAzMECampaign` toocreate e successivamente `ActivateAzMECampaign` tooactivate è.</span><span class="sxs-lookup"><span data-stu-id="da73d-119">Once we find an item which requires processing - we extract hello information required toocreate an announcement from hello list item and call `CreateAzMECampaign` toocreate it and subsequently `ActivateAzMECampaign` tooactivate it.</span></span> <span data-ttu-id="da73d-120">Si tratta essenzialmente chiamate all'API REST chiamata back-end Mobile Engagement toohello.</span><span class="sxs-lookup"><span data-stu-id="da73d-120">These are essentially REST API calls calling toohello Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="da73d-121">Hello Mobile Engagement REST API richiedono un **intestazione autorizzazione HTTP lo schema di autenticazione di base** che comprende hello `ApplicationId` hello e `ApiKey` è utilizzare hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="da73d-121">hello Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of hello `ApplicationId` and hello `ApiKey` which you get from hello Azure portal.</span></span> <span data-ttu-id="da73d-122">Assicurarsi che si sta utilizzando il messaggio hello chiave from hello **chiavi api** sezione e *non* da hello **chiavi sdk** sezione.</span><span class="sxs-lookup"><span data-stu-id="da73d-122">Make sure that you are using hello Key from hello **api keys** section and *not* from hello **sdk keys** section.</span></span> 
   
   ![][2]
   
       static string CreateAuthZHeader()
       {
           string BasicAuthzHeaderString = "Basic " + EncodeTo64(ApplicationId + ":" + ApiKey);
           return BasicAuthzHeaderString;
       }
   
       static public string EncodeTo64(string toEncode)
       {
           byte[] toEncodeAsBytes = System.Text.ASCIIEncoding.ASCII.GetBytes(toEncode);
           string returnValue = System.Convert.ToBase64String(toEncodeAsBytes);
           return returnValue;
       }  
3. <span data-ttu-id="da73d-123">Per creare il tipo di annuncio hello della campagna, fare riferimento toohello [documentazione](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="da73d-123">For creating hello announcement type campaign - refer toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="da73d-124">È necessario assicurarsi di avere specificato la campagna hello toomake `kind` come *annuncio* hello e [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) e passarlo come FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="da73d-124">You need toomake sure that you are specifying hello campaign `kind` as *announcement* and hello [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create hello payload toosend hello content
                // Reference -> https://msdn.microsoft.com/library/dn913749.aspx
                string data =
                    @"{""name"":""" + campaignName + @"""," + 
                    @"""type"":""only_notif""," + 
                    @"""deliveryTime"":""any"","" + 
                    @""notificationTitle"":""" + notificationTitle + 
                    @""",""notificationMessage"":""" + notificationMessage + 
                    @""",""actionUrl"":""" + actionURL + @"""}";
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("data", data),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is hello campaign id
                    campaignId = Convert.ToInt32(responseString);
                    Console.WriteLine("Campaign successfully created with id {0}", campaignId);
                }
                else
                {
                    Console.WriteLine("Campaign creation failed with error - '{0}'", responseString);
                }
                return campaignId;
            }
        }
4. <span data-ttu-id="da73d-125">Dopo aver creato annuncio hello creato, verrà visualizzato un risultato simile hello seguenti nel portale Mobile Engagement hello (si noti che lo stato di hello = bozza e attivato = n/d)</span><span class="sxs-lookup"><span data-stu-id="da73d-125">Once you have hello announcement created, you will see something like hello following on hello Mobile Engagement portal (note that hello State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="da73d-126">`CreateAzMECampaign`Crea una campagna di annuncio e restituisce il relativo chiamante toohello Id.</span><span class="sxs-lookup"><span data-stu-id="da73d-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id toohello caller.</span></span> <span data-ttu-id="da73d-127">`ActivateAzMECampaign`richiede l'Id come campagna di hello tooactivate parametro hello.</span><span class="sxs-lookup"><span data-stu-id="da73d-127">`ActivateAzMECampaign` requires this Id as hello parameter tooactivate hello campaign.</span></span> 
   
        static async Task<bool> ActivateAzMECampaign(int campaignId)
        {
            string activateUriFragment = "/reach/1/activate";
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("id", campaignId.ToString()),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + activateUriFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                if (response.StatusCode.ToString() == "OK")
                {
                    Console.WriteLine("Campaign successfully activated");
                    return true;
                }
                else
                {
                    Console.WriteLine("Campaign activation failed with error - '{0}'", responseString);
                    return false;
                }
            }
        }
6. <span data-ttu-id="da73d-128">Dopo aver creato annuncio hello attivata, si noterà simile alla seguente hello nel portale Mobile Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="da73d-128">Once you have hello announcement activated, you will see something like hello following on hello Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="da73d-129">Non appena viene attivata la campagna hello, tutti i dispositivi che soddisfano il criterio di hello nella campagna hello inizierà a visualizzare le notifiche.</span><span class="sxs-lookup"><span data-stu-id="da73d-129">As soon as hello campaign gets activated, any devices which satisfy hello criterion on hello campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="da73d-130">Si noterà anche che l'elemento di elenco hello contrassegnato con IsProcessed = false è stata impostata tooTrue dopo la creazione della campagna di annuncio hello.</span><span class="sxs-lookup"><span data-stu-id="da73d-130">You will also notice that hello list item marked with IsProcessed = false has been set tooTrue once hello announcement campaign is created.</span></span>  

<span data-ttu-id="da73d-131">In questo esempio creata una campagna di annuncio semplice impostazione delle proprietà di hello necessario per lo più.</span><span class="sxs-lookup"><span data-stu-id="da73d-131">This sample created a simple announcement campaign specifying mostly hello required properties.</span></span> <span data-ttu-id="da73d-132">È possibile personalizzare questa come è possibile dal portale hello usando informazioni hello [qui](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="da73d-132">You can customize this as much as you can from hello portal by using hello information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



