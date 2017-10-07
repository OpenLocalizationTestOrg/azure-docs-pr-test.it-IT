---
title: aaaUsing tooaccess .NET SDK servizio API di Azure Mobile Engagement
description: Viene descritto come toouse hello tooaccess Mobile Engagement .NET SDK servizio API di Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: c07728aa-43f2-4238-8b4a-c9eddf9d838b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 812be6f507b29f7b2de6454e06face8082c2d161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a>Con .NET SDK tooaccess servizio API di Azure Mobile Engagement
Azure Mobile Engagement espone un set di API per l'utente toomanage dispositivi, Reach/Push campagne di marketing e così via toointeract con queste API, è possibile utilizzare un [file Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) che è possibile utilizzare con strumenti SDK toogenerate per il preferito lingua. È consigliabile utilizzare hello [AutoRest](https://github.com/Azure/AutoRest) strumento toogenerate del SDK da questo file Swagger.

> [!NOTE]
> servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti. Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

È stato creato un SDK di .NET in modo simile, che consente di toointeract con queste API tramite un wrapper di c# e non è necessario toodo hello negoziazione del token di autenticazione e aggiornare manualmente.  

In questo esempio viene eseguita insieme hello di passaggi toofollow toouse hello .NET SDK:

1. Prima di tutto, è necessario l'autenticazione di toosetup hello per le API tramite hello Azure Active Directory come descritto [qui](mobile-engagement-api-authentication.md#authentication). Alla fine di hello di questi passaggi, è necessario un valore valido **SubscriptionId**, **TenantId**, **ApplicationId** e **Secret**. 
2. Si utilizzerà un semplice toodemonstrate di applicazione Console di Windows utilizzano hello .NET SDK con scenario hello di creazione di una campagna di annuncio. Aprire Visual Studio e creare un' **applicazione console**.   
3. È quindi necessario hello toodownload .NET SDK è disponibile come **libreria di gestione di Microsoft Azure Engagement** nella raccolta Nuget hello [qui](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).
   Se si sta installando hello Nuget da Visual Studio, è necessario di disporre di controllo contrassegnato hello tooensure **versione provvisoria di inclusione** opzione durante la ricerca per il pacchetto di hello:
   
    ![][1]
4. In hello `Program.cs` file, aggiungere i seguenti spazi dei nomi hello:
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. Successivamente sarà necessario toodefine hello seguendo le costanti che verrà utilizzato per l'autenticazione e l'interazione con l'App di Engagement Mobile hello in cui si sta creando una campagna di annuncio hello:
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is hello Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using hello one as specified in hello Azure portal (NOT hello App Name)
        const string APP_RESOURCE_NAME = "";
6. Definire hello `EngagementManagementClient` variabile che verrà utilizzato metodi di Mobile Engagement SDK toocall hello:
   
        static EngagementManagementClient engagementClient; 
7. Aggiungere hello seguente tooyour `Main` metodo:
   
        try
            {
                // Initialize hello Engagement SDK toocall out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. Definire hello al metodo che si occupa dell'inizializzazione hello `EngagementManagementClient` prima autenticazione e quindi associando stesso con l'App di Engagement Mobile hello in cui si prevede di campagna di annuncio hello toocreate:
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is hello Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create hello campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > Si noti che è necessario hello toouse **nome risorsa App** come definito nel portale di gestione di Azure hello per il parametro AppName hello. 
   > 
   > 
9. Infine, definire hello CreateCampaign che si occuperà di toocreate EngagementClient hello inizializzata in precedenza un semplice utilizzando **in qualsiasi momento** & **sola notifica** campagna con un titolo e un messaggio: 
   
        private async static Task CreateCampaign()
        {
            //  Refer toohello Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all hello non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing hello app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer toohello Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. Hello esecuzione dell'applicazione console e verrà visualizzato seguito hello in seguito alla creazione di una campagna hello:
    
    **Campaign Id '159' was created successfully and it is in 'draft' state**

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
