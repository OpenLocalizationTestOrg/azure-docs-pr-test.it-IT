---
title: aaaHow tooSet dei Computer per lo sviluppo di servizi multimediali con .NET
description: Informazioni sui prerequisiti di hello per servizi multimediali usando hello Media Services SDK per .NET. Viene inoltre illustrato come toocreate un'app di Visual Studio.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a>Sviluppo di applicazioni di Servizi multimediali con .NET
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Questo argomento viene illustrata la modalità di servizi multimediali di sviluppo di toostart applicazioni con .NET.

Hello **Azure Media Services .NET SDK** libreria consente tooprogram in servizi multimediali usando .NET. anche più facile toodevelop con .NET, hello toomake **Azure Media Services .NET SDK Extensions** viene fornita una libreria. contenente un set di funzioni di supporto e metodi di estensione che semplificano il codice .NET. Entrambe le librerie sono disponibili tramite **NuGet** e **GitHub**.

## <a name="prerequisites"></a>Prerequisiti
* Un account di Servizi multimediali ottenuto con una sottoscrizione di Azure nuova o esistente. Vedere l'argomento hello [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).
* Sistemi operativi: Windows 10, Windows 7, Windows 2008 R2 o Windows 8.
* .NET Framework 4.5
* Visual Studio.

## <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio
In questa sezione illustra come toocreate un progetto in Visual Studio e configurarlo per lo sviluppo di servizi multimediali.  In questo caso, il progetto di hello è un'applicazione console c# Windows, ma hello stessi passaggi di configurazione illustrati di seguito si applicano tooother tipi di progetti, che è possibile creare per le applicazioni di servizi multimediali (ad esempio, un'applicazione Windows Form o un'applicazione Web ASP.NET).

Questa sezione viene illustrato come toouse **NuGet** tooadd Media Services .NET SDK extensions e altre librerie dipendenti.

In alternativa, è possibile ottenere i bit di Media Services .NET SDK più recente di hello da GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) o [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), compilare la soluzione hello e aggiungere hello riferimenti toohello client progetto. Tutte le dipendenze necessarie di hello scaricate ed estratte automaticamente.

1. Creare una nuova applicazione console C# in Visual Studio. Immettere hello **nome**, **percorso**, e **Nome soluzione**, quindi fare clic su OK.
2. Compilare la soluzione hello.
3. Utilizzare **NuGet** tooinstall e aggiungere **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**). Insieme al pacchetto viene installato anche **Media Services .NET SDK** e vengono aggiunte tutte le altre dipendenze necessarie.
   
    Assicurarsi di aver hello la versione più recente di NuGet. Per altre informazioni e per istruzioni di installazione, vedere [NuGet](http://nuget.codeplex.com/).
4. In Esplora soluzioni fare doppio clic su nome hello del progetto di hello e scegliere Gestione pacchetti NuGet.
   
    verrà visualizzata la finestra di dialogo Gestisci pacchetti NuGet di Hello.
5. Nella raccolta Online hello, cercare le estensioni di Microsoft Azure, scegliere Azure Media Services .NET SDK Extensions e quindi fare clic su pulsante Installa hello.
   
    progetto Hello viene modificato e fa riferimento a toohello Media Services .NET SDK Extensions Media Services .NET SDK e altri assembly dipendenti vengono aggiunti.
6. toopromote un ambiente di sviluppo di pulizia, è consigliabile abilitare il ripristino del pacchetto NuGet. Per altre informazioni vedere l'articolo relativo al [ripristino del pacchetto NuGet](http://docs.nuget.org/consume/package-restore).
7. Aggiungere un riferimento troppo**Configuration** assembly. Questo assembly contiene hello System. Configuration. **ConfigurationManager** classe che rappresenta il file di configurazione tooaccess utilizzato (ad esempio, App. config).
   
    riferimenti tooadd mediante finestra di dialogo Gestione riferimenti hello, fare clic sul nome del progetto in Esplora soluzioni hello hello. Selezionare quindi Aggiungi e Riferimenti.
   
    viene visualizzata la finestra Gestione riferimenti Hello.
8. Negli assembly di .NET framework, trovare e selezionare l'assembly System. Configuration hello e fare clic su OK.
9. Aprire il file app. config hello e aggiungere un *appSettings* file toohello di sezione.     
   
    Impostare i valori hello che sono necessari tooconnect toohello API di servizi multimediali. Per ulteriori informazioni, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

    Se si utilizza [l'autenticazione utente](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) il file di configurazione verrà probabilmente dispongono di valori per il dominio tenant di Azure AD e hello endpoint API REST AMS.
    
    >[!Important]
    >La maggior parte degli esempi di codice nella documentazione di servizi multimediali di Azure hello impostato, utilizzare un tipo di utente (interattivo) di autenticazione tooconnect toohello AMS API. Questo metodo di autenticazione funzionerà in modo efficace per le app native di gestione o monitoraggio: app per dispositivi mobili, app di Windows e app console. Questo metodo di autenticazione non è adatto per il tipo applicazioni come API delle applicazioni, servizi Web e server.  Per ulteriori informazioni, vedere [hello accesso API AMS con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Sovrascrivi hello esistente **utilizzando** istruzioni all'inizio di hello del file Program.cs hello con hello seguente codice.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

A questo punto, si è pronti toostart lo sviluppo di un'applicazione di servizi multimediali.    

## <a name="example"></a>Esempio

Di seguito è riportato un esempio di piccole dimensioni che si connette toohello AMS API e vengono elencati tutti i processori di contenuti multimediali disponibili.
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a>Passaggi successivi

Ora [è possibile connettersi toohello API AMS](media-services-use-aad-auth-to-access-ams-api.md) e avviare [sviluppo](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

