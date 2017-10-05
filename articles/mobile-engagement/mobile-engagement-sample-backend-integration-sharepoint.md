---
title: Azure Mobile Engagement - Integrazione del back-end
description: Informazioni su come connettere Azure Mobile Engagement a un back-end di SharePoint per creare campagne da SharePoint.
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
ms.openlocfilehash: d49f1094f4c3f170f3618f3e19e42266f9ae8858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="8fe0c-103">Azure Mobile Engagement - Integrazione di API</span><span class="sxs-lookup"><span data-stu-id="8fe0c-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="8fe0c-104">In un sistema marketing automatizzato, vengono eseguite automaticamente anche la creazione e l'attivazione delle campagne di marketing.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-104">In an automated marketing system, creating and activating the marketing campaigns also occur automatically.</span></span> <span data-ttu-id="8fe0c-105">A questo scopo, Azure Mobile Engagement permette la creazione di tali campagne marketing automatizzate anche mediante le API.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="8fe0c-106">In genere i clienti usano l'interfaccia del front-end di Mobile Engagement per creare annunci/sondaggi e così via come parte delle campagne di marketing.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-106">Typically customers use the Mobile Engagement front end interface to create announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="8fe0c-107">Nel corso della maturazione delle campagne di marketing, tuttavia, diventa necessario sfruttare i dati bloccati nei sistemi back-end (ad esempio qualsiasi sistema CRM o un sistema CMS come SharePoint), in modo che sia possibile creare una pipeline automatizzata completa, che crea a sua volta in modo dinamico campagne in Mobile Engagement in base ai dati provenienti dai sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-107">However as the marketing campaigns become mature, there is a need to leverage the data locked in the backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on the data flowing in from the backend systems.</span></span> 

![][5]

<span data-ttu-id="8fe0c-108">Questa esercitazione illustra uno scenario di questo tipo, in cui un utente aziendale di SharePoint popola un elenco di SharePoint con dati di marketing e un processo automatizzato sceglie elementi dall'elenco e li connette al sistema Mobile Engagement usando le API REST disponibili per creare una campagna di marketing dai dati di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from the list and connects with the Mobile Engagement system using the available REST APIs to create a marketing campaign from the SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8fe0c-109">In generale, è possibile usare questo esempio come punto di partenza per capire come chiamare qualsiasi API REST di Mobile Engagement, poiché illustra nel dettaglio i due aspetti chiave della chiamata delle API, ovvero l'autenticazione e il passaggio di parametri.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-109">In general, you can use this sample as a starting point for understanding how to call any Mobile Engagement REST API as it details the two key aspects of calling the APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="8fe0c-110">Integrazione con SharePoint</span><span class="sxs-lookup"><span data-stu-id="8fe0c-110">SharePoint integration</span></span>
1. <span data-ttu-id="8fe0c-111">L'elenco di SharePoint di esempio ha un aspetto analogo al seguente.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-111">Here is what the sample SharePoint list looks like.</span></span> <span data-ttu-id="8fe0c-112">I valori di **Title**, **Category**, **NotificationTitle**, **Message** e **URL** vengono usati per la creazione dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating the announcement.</span></span> <span data-ttu-id="8fe0c-113">La colonna **IsProcessed** viene usata dal processo di automazione di esempio sotto forma di programma console.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-113">There is a column called **IsProcessed** which is used by the sample automation process in the form of a console program.</span></span> <span data-ttu-id="8fe0c-114">È possibile eseguire questo programma console come processo Web di Azure, in modo che sia possibile pianificarlo, oppure si può usare direttamente il flusso di lavoro di SharePoint per programmare la creazione e l'attivazione dell'annuncio quando un elemento viene inserito nell'elenco di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use the SharePoint workflow to program creating and activating the announcement when an item is inserted into the SharePoint list.</span></span> <span data-ttu-id="8fe0c-115">In questo esempio viene usato il programma console, che esamina gli elementi dell'elenco di SharePoint, crea annunci in Azure Mobile Engagement per ogni elemento e infine contrassegna il flag **IsProcessed** come true in caso di creazione riuscita dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-115">In this sample we use the console program which goes through the items in the SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks the **IsProcessed** flag to be true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="8fe0c-116">Per l'autenticazione nell'elenco di SharePoint viene usato il codice dell'esempio di *Autenticazione remota in SharePoint Online mediante il modello a oggetti client* [qui](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) .</span><span class="sxs-lookup"><span data-stu-id="8fe0c-116">We are using the code from the sample *Remote Authentication in SharePoint Online Using the Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) to authenticate with the SharePoint list.</span></span>
3. <span data-ttu-id="8fe0c-117">Dopo l'autenticazione, gli elementi dell'elenco verranno esaminati in ciclo per individuare eventuali elementi appena creati, il cui valore **IsProcessed** sarà false.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-117">Once authenticated, we loop through the list items to find out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
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
   
                // Load the SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through the list to go through all the items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request to create AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this to true
                            item["IsProcessed"] = "Yes";
   
                            // Now try to activate the campaign also
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

## <a name="mobile-engagement-integration"></a><span data-ttu-id="8fe0c-118">Integrazione con Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8fe0c-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="8fe0c-119">Quando viene rilevato un elemento che richiede l'elaborazione, vengono estratte le informazioni necessarie per creare un annuncio dall'elemento dell'elenco, viene chiamato `CreateAzMECampaign` per creare l'annuncio e infine `ActivateAzMECampaign` per attivarlo.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-119">Once we find an item which requires processing - we extract the information required to create an announcement from the list item and call `CreateAzMECampaign` to create it and subsequently `ActivateAzMECampaign` to activate it.</span></span> <span data-ttu-id="8fe0c-120">Si tratta essenzialmente di chiamate all'API REST per il back-end di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-120">These are essentially REST API calls calling to the Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="8fe0c-121">Le API REST di Mobile Engagement necessitano di un'**intestazione HTTP dell'autorizzazione dello schema di autorizzazione di base**, costituita da `ApplicationId` e `ApiKey`, disponibili nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-121">The Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of the `ApplicationId` and the `ApiKey` which you get from the Azure portal.</span></span> <span data-ttu-id="8fe0c-122">Assicurarsi di usare la chiave della sezione **Chiavi API** e *non* della sezione **Chiavi SDK**.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-122">Make sure that you are using the Key from the **api keys** section and *not* from the **sdk keys** section.</span></span> 
   
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
3. <span data-ttu-id="8fe0c-123">Per la creazione di una campagna di tipo annuncio, fare riferimento alla [documentazione](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fe0c-123">For creating the announcement type campaign - refer to the [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="8fe0c-124">È necessario assicurarsi di specificare l'elemento `kind` della campagna come *announcement* e il [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) e infine di passarlo come FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-124">You need to make sure that you are specifying the campaign `kind` as *announcement* and the [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create the payload to send the content
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
   
                // Send the POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is the campaign id
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
4. <span data-ttu-id="8fe0c-125">Al termine della creazione dell'annuncio, il portale di Mobile Engagement avrà un aspetto analogo al seguente. Si noti che Stato=Bozza e Attivato = N/D.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-125">Once you have the announcement created, you will see something like the following on the Mobile Engagement portal (note that the State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="8fe0c-126">`CreateAzMECampaign` crea una campagna di tipo annuncio e restituisce il rispettivo ID al chiamante.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id to the caller.</span></span> <span data-ttu-id="8fe0c-127">`ActivateAzMECampaign` richiede questo ID come parametro per l'attivazione della campagna.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-127">`ActivateAzMECampaign` requires this Id as the parameter to activate the campaign.</span></span> 
   
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
   
                // Send the POST request
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
6. <span data-ttu-id="8fe0c-128">Dopo l'attivazione dell'annuncio, il portale di Mobile Engagement avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="8fe0c-128">Once you have the announcement activated, you will see something like the following on the Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="8fe0c-129">Non appena viene attivata la campagna, tutti i dispositivi che soddisfano i criteri della campagna inizieranno a visualizzare notifiche.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-129">As soon as the campaign gets activated, any devices which satisfy the criterion on the campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="8fe0c-130">Si potrà anche notare che l'elemento dell'elenco contrassegnato come IsProcessed = false è stato impostato su True dopo la creazione della campagna.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-130">You will also notice that the list item marked with IsProcessed = false has been set to True once the announcement campaign is created.</span></span>  

<span data-ttu-id="8fe0c-131">Questo esempio ha creato una semplice campagna di tipo annuncio, specificando principalmente le proprietà necessarie.</span><span class="sxs-lookup"><span data-stu-id="8fe0c-131">This sample created a simple announcement campaign specifying mostly the required properties.</span></span> <span data-ttu-id="8fe0c-132">È possibile personalizzare come si desidera l'esempio nel portale, usando le informazioni disponibili [qui](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fe0c-132">You can customize this as much as you can from the portal by using the information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



