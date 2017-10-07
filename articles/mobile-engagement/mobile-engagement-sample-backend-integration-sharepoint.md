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
# <a name="azure-mobile-engagement---api-integration"></a>Azure Mobile Engagement - Integrazione di API
In un sistema automatizzato di marketing, creazione e l'attivazione di hello anche le campagne di marketing si verificano automaticamente. A questo scopo, Azure Mobile Engagement permette la creazione di tali campagne marketing automatizzate anche mediante le API. 

I clienti utilizzano in genere hello Mobile Engagement front-end interfaccia toocreate annunci o sondaggi e così via come parte le campagne di marketing. Tuttavia, come hello diventare mature campagne di marketing, è necessario tooleverage hello il blocco dei dati nei sistemi back-end hello (ad esempio, un sistema CRM o CMS come SharePoint) in modo che sia possibile creare una pipeline completamente automatizzata che consente di creare campagne in dispositivi mobili Engagement in modo dinamico in base ai dati di hello trasmessi dai sistemi back-end hello. 

![][5]

Questa esercitazione sarà inviato tramite una situazione in cui un utente di business di SharePoint consente di popolare un elenco di SharePoint con dati di marketing e un processo automatizzato preleva gli elementi elenco hello e si connette con hello Mobile Engagement sistema con hello disponibili API REST toocreate una campagna di marketing dai dati di SharePoint hello. 

> [!IMPORTANT]
> In generale, è possibile utilizzare questo esempio come punto di partenza per comprendere come toocall qualsiasi API REST di Engagement Mobile come dettagli hello due gli aspetti chiave della chiamata hello API - autenticazione e passando i parametri. 
> 
> 

## <a name="sharepoint-integration"></a>Integrazione con SharePoint
1. Ecco quali esempio hello è simile a elenco SharePoint. **Titolo**, **categoria**, **NotificationTitle**, **messaggio** e **URL** vengono utilizzati per creare l'annuncio hello. È una colonna denominata **IsProcessed** che viene utilizzato dal processo di automazione di esempio hello sotto forma di hello di un programma di console. È possibile eseguire il programma di console come un processo Web di Azure in modo che è possibile eseguire la pianificazione o è possibile utilizzare direttamente la creazione di hello SharePoint del flusso di lavoro tooprogram e l'attivazione annuncio hello quando un elemento viene inserito nell'elenco di SharePoint hello. In questo esempio viene utilizzato programma console hello che passa tra gli elementi di hello hello SharePoint elencare e creare l'annuncio in Azure Mobile Engagement per ognuno di essi e quindi contrassegna infine hello **IsProcessed** true toobe flag creazione di un annuncio ha esito positivo.
   
    ![][1]
2. Si sta usando codice hello tratto dall'esempio hello *autenticazione remota in SharePoint Online usando hello modello a oggetti Client* [qui](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate con elenco di SharePoint hello.
3. Una volta autenticato, il ciclo tramite hello elenco elementi toofind gli eventuali elementi appena creati (che avrà **IsProcessed** = false). 
   
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

## <a name="mobile-engagement-integration"></a>Integrazione con Mobile Engagement
1. Una volta che si trova un elemento che richiede l'elaborazione, si estrarre informazioni hello necessarie toocreate un annuncio hello voce di elenco e chiamare `CreateAzMECampaign` toocreate e successivamente `ActivateAzMECampaign` tooactivate è. Si tratta essenzialmente chiamate all'API REST chiamata back-end Mobile Engagement toohello. 
2. Hello Mobile Engagement REST API richiedono un **intestazione autorizzazione HTTP lo schema di autenticazione di base** che comprende hello `ApplicationId` hello e `ApiKey` è utilizzare hello portale di Azure. Assicurarsi che si sta utilizzando il messaggio hello chiave from hello **chiavi api** sezione e *non* da hello **chiavi sdk** sezione. 
   
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
3. Per creare il tipo di annuncio hello della campagna, fare riferimento toohello [documentazione](https://msdn.microsoft.com/library/azure/mt683750.aspx). È necessario assicurarsi di avere specificato la campagna hello toomake `kind` come *annuncio* hello e [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) e passarlo come FormUrlEncodedContent. 
   
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
4. Dopo aver creato annuncio hello creato, verrà visualizzato un risultato simile hello seguenti nel portale Mobile Engagement hello (si noti che lo stato di hello = bozza e attivato = n/d)
   
    ![][3]
5. `CreateAzMECampaign`Crea una campagna di annuncio e restituisce il relativo chiamante toohello Id. `ActivateAzMECampaign`richiede l'Id come campagna di hello tooactivate parametro hello. 
   
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
6. Dopo aver creato annuncio hello attivata, si noterà simile alla seguente hello nel portale Mobile Engagement hello:
   
    ![][4]
7. Non appena viene attivata la campagna hello, tutti i dispositivi che soddisfano il criterio di hello nella campagna hello inizierà a visualizzare le notifiche. 
8. Si noterà anche che l'elemento di elenco hello contrassegnato con IsProcessed = false è stata impostata tooTrue dopo la creazione della campagna di annuncio hello.  

In questo esempio creata una campagna di annuncio semplice impostazione delle proprietà di hello necessario per lo più. È possibile personalizzare questa come è possibile dal portale hello usando informazioni hello [qui](https://msdn.microsoft.com/library/azure/mt683751.aspx). 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



