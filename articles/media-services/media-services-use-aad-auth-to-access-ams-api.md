---
title: aaaAccess API di servizi multimediali di Azure con l'autenticazione di Azure Active Directory | Documenti Microsoft
description: Informazioni sui concetti e le procedure tootake toouse Azure Active Directory (Azure AD) tooauthenticate accesso toohello API di servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a>Hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD
 
Hello API di servizi multimediali di Azure è un'API RESTful. È possibile utilizzare è tooperform operazioni sulle risorse di supporto utilizzando un'API REST o tramite SDK client disponibili. Servizi multimediali di Azure offre un SDK client di Servizi multimediali per Microsoft .NET. toobe autorizzato alle risorse di servizi multimediali tooaccess e hello API di servizi multimediali, deve prima essere autenticato. 

Servizi multimediali supporta l'[autenticazione basata su Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md). servizio REST di Azure Media Hello suppone hello utente o applicazione che effettua le richieste API REST di hello entrambi hello **collaboratore** o **proprietario** tooaccess ruolo hello risorse. Per ulteriori informazioni, vedere [Introduzione a controllo di accesso basato sui ruoli nel portale di Azure hello](../active-directory/role-based-access-control-what-is.md).  

> [!IMPORTANT]
> Attualmente servizi multimediali supporta modello di autenticazione hello Azure Access Control service. L'autorizzazione di Controllo di accesso, tuttavia, verrà dichiarata deprecata il 1° giugno 2018. Si consiglia di migrare il modello di autenticazione di Azure AD toohello appena possibile.

Questo documento offre una panoramica di come tooaccess hello API di servizi multimediali tramite l'API REST o .NET.

## <a name="access-control"></a>Controllo di accesso

Per hello Azure Media REST richiesta toosucceed, utente chiamante hello deve avere un ruolo di proprietario o collaboratore per hello tooaccess sta tentando di account di servizi multimediali.  
Solo un utente con ruolo di proprietario hello può concedere a media risorsa (account) accesso toonew utenti o applicazioni. ruolo di collaboratore Hello può accedere solo risorse di supporto di hello.
Le richieste non autorizzate hanno esito negativo e restituiscono il codice di stato 401. Se questo codice di errore, verificare se l'utente ha hello collaboratore o il ruolo di proprietario assegnato per l'account di servizi multimediali dell'utente hello. È possibile archiviare hello portale di Azure. Ricerca per l'account di supporto e quindi fare clic su hello **il controllo degli accessi** scheda. 

![Scheda Controllo di accesso](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a>Tipi di autenticazione 
 
Quando si utilizza l'autenticazione di Azure AD con Servizi multimediali di Azure, sono disponibili due opzioni di autenticazione:

- **Autenticazione utente**. Eseguire l'autenticazione di una persona che utilizza hello app toointeract con risorse di servizi multimediali. applicazione interattiva Hello deve prima richiedere le credenziali dell'utente hello utente hello. Un esempio è un'applicazione console di gestione usata dai processi di codifica toomonitor gli utenti autorizzati o streaming live. 
- **Autenticazione basata su entità servizio**. Consente di eseguire l'autenticazione di un servizio. Le applicazioni che in genere usano questo metodo di autenticazione sono app che eseguono servizi daemon, servizi di livello intermedio o processi pianificati. Esempi sono le app Web, le app per le funzioni, le app per la logica, l'interfaccia API e i microservizi.

### <a name="user-authentication"></a>Autenticazione utente 

Le applicazioni che devono utilizzare il metodo di autenticazione utente hello sono gestione o il monitoraggio di applicazioni native: App per dispositivi mobili, applicazioni di Windows e applicazioni Console. Questo tipo di soluzione è utile quando si desidera che l'interazione umana con servizio hello in uno dei seguenti scenari hello:

- Dashboard di monitoraggio per i processi di codifica.
- Dashboard di monitoraggio per lo streaming live.
- Applicazione di gestione per le risorse tooadminister agli utenti di computer desktop o portatile in un account di servizi multimediali.

> [!NOTE]
> Questo metodo di autenticazione non deve essere usato con le applicazioni per consumatori. 

Un'applicazione nativa deve innanzitutto acquisire un token di accesso da Azure AD e quindi utilizzarlo quando si effettua l'API di REST di servizi multimediali toohello di richieste HTTP. Aggiungere l'intestazione della richiesta di token toohello accesso hello. 

Hello seguente diagramma viene illustrato un flusso di autenticazione di una tipica applicazione interattiva: 

![Diagramma di app native](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

Nel precedente diagramma di hello, hello numeri rappresentano flusso hello delle richieste di hello in ordine cronologico.

> [!NOTE]
> Quando si utilizza il metodo di autenticazione utente hello, tutte le app di condivideranno hello stesso ID di client applicazione nativa (impostazione predefinita) e l'applicazione nativa URI di reindirizzamento. 

1. Richiedere le credenziali all'utente.
2. Richiedere un token di accesso di Azure AD con hello seguenti parametri:  

    * Endpoint tenant di Azure AD.

        le informazioni sul tenant Hello possono essere recuperate da hello portale di Azure. Posizionare il cursore sul nome hello dell'utente connesso di hello nell'angolo superiore destro di hello.
    * URI di risorsa per Servizi multimediali. 

        Questo URI è hello uguale per gli account servizi multimediali in hello stesso ambiente di Azure (ad esempio, https://rest.media.azure.net).

    * ID client dell'applicazione Servizi multimediali (nativa).
    * URI di reindirizzamento dell'applicazione Servizi multimediali (nativa).
    * URI di risorsa per Servizi multimediali REST.
        
        Hello URI rappresenta l'endpoint dell'API REST hello (ad esempio, https://test03.restv2.westus.media.azure.net/api/).

    tooget valori per questi parametri, vedere [utilizzare impostazioni di autenticazione tooaccess portale Azure AD Azure hello](media-services-portal-get-started-with-aad.md) utilizzando l'opzione di autenticazione utente hello.

3. token di accesso di Azure AD Hello viene inviato toohello client.
4. client Hello invia una richiesta toohello API REST di Azure Media, con il token di accesso di hello Azure AD.
5. client Hello ottiene nuovamente hello dati da servizi multimediali.

Per informazioni su come toocommunicate autenticazione toouse Azure AD con altre richieste utilizzando hello client di Media Services .NET SDK, vedere [usano Azure AD authentication tooaccess hello API dei servizi multimediali con .NET](media-services-dotnet-get-started-with-aad.md). 

Se non si utilizza client .NET di servizi multimediali hello SDK, è necessario creare manualmente una richiesta di token di accesso di Azure AD utilizzando i parametri di hello descritti nel passaggio 2. Per ulteriori informazioni, vedere [come toouse hello Azure AD Authentication Library tooget hello token di Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="service-principal-authentication"></a>Autenticazione di un'entità servizio

Le applicazioni che usano in genere questo metodo di autenticazione sono app che eseguono servizi di livello intermedio e processi pianificati: app Web, app per le funzioni, app per la logica, API e microservizi. Questo metodo di autenticazione è anche adatto per applicazioni interattive in cui è possibile toouse un account di servizio toomanage alle risorse.

Quando si usa hello Servizio autenticazione principale metodo toobuild degli scenari degli utenti, l'autenticazione è gestita in genere nel livello intermedio di hello (tramite alcune API) e non direttamente in un'applicazione desktop o mobile. 

toouse questo metodo, creare un'applicazione Azure AD ed entità nel proprio tenant del servizio. Dopo aver creato un'applicazione hello, assegnare hello app collaboratore o proprietario del ruolo accesso toohello account di servizi multimediali. È possibile farlo in hello portale di Azure mediante Azure CLI, o con uno script di PowerShell. È anche possibile usare un'applicazione Azure AD esistente. È possibile registrare e gestire le app di Azure AD e l'entità servizio [nel portale di Azure hello](media-services-portal-get-started-with-aad.md). oppure usare l'[interfaccia della riga di comando di Azure 2.0](media-services-use-aad-auth-to-access-ams-api.md) o [PowerShell](media-services-powershell-create-and-configure-aad-app.md). 

![App di livello intermedio](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

Dopo aver creato l'applicazione Azure AD, si otterranno i valori per hello seguenti impostazioni. Per l'autenticazione sono necessari i valori seguenti:

- ID Client 
- Segreto client 

Nella figura precedente di hello, hello numeri rappresentano flusso hello delle richieste di hello in ordine cronologico:
    
1. Un'applicazione di livello intermedio (API web o applicazione web) richiede un token di accesso di Azure AD con hello seguenti parametri:  

    * Endpoint tenant di Azure AD.

        le informazioni sul tenant Hello possono essere recuperate da hello portale di Azure. Posizionare il cursore sul nome hello dell'utente connesso di hello nell'angolo superiore destro di hello.
    * URI di risorsa per Servizi multimediali. 

        Questo URI è hello uguale per gli account di servizi multimediali che si trovano in hello stesso ambiente di Azure (ad esempio, https://rest.media.azure.net).

    * URI di risorsa per Servizi multimediali REST.

        Hello URI rappresenta l'endpoint dell'API REST hello (ad esempio, https://test03.restv2.westus.media.azure.net/api/).

    * I valori dell'applicazione Azure AD: hello client ID e segreto client.
    
    tooget valori per questi parametri, vedere [utilizzare impostazioni di autenticazione tooaccess portale Azure AD Azure hello](media-services-portal-get-started-with-aad.md) utilizzando l'opzione di autenticazione dell'entità servizio hello.

2. token di accesso di Azure AD Hello viene inviato toohello di livello intermedio.
4. livello intermedio Hello Invia richiesta toohello API REST di Azure Media con token di Azure AD hello.
5. livello intermedio Hello consente di ottenere dati hello da servizi multimediali.

Per ulteriori informazioni su come toocommunicate autenticazione toouse Azure AD con altre richieste utilizzando hello client di Media Services .NET SDK, vedere [tooaccess autenticazione usano Azure AD API di servizi multimediali di Azure con .NET](media-services-dotnet-get-started-with-aad.md). 

Se non si utilizza client .NET di servizi multimediali hello SDK, è necessario creare manualmente una richiesta di token di Azure AD tramite i parametri descritti nel passaggio 1. Per ulteriori informazioni, vedere [come toouse hello Azure AD Authentication Library tooget hello token di Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="troubleshooting"></a>Risoluzione dei problemi

Eccezione: "server remoto hello ha restituito un errore: non autorizzato (401)."

Soluzione: Per toosucceed richiesta REST di servizi multimediali di hello, utente chiamante hello deve essere un ruolo di collaboratore o proprietario in hello tooaccess sta tentando di account di servizi multimediali. Per ulteriori informazioni, vedere hello [il controllo degli accessi](media-services-use-aad-auth-to-access-ams-api.md#access-control) sezione.

## <a name="resources"></a>Risorse

Hello gli articoli seguenti è riportate alcune panoramiche dei concetti di autenticazione di Azure AD: 

- [Scenari di autenticazione per Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [Aggiungere, aggiornare o rimuovere un'applicazione in Azure AD](../active-directory/develop/active-directory-integrating-applications.md)
- [Gestire il controllo degli accessi in base al ruolo con Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a>Passaggi successivi

* Utilizzare il portale di Azure hello troppo[tooconsume l'autenticazione di Azure AD API di servizi multimediali di Azure di accedere](media-services-portal-get-started-with-aad.md).
* Utilizzare l'autenticazione di Azure AD troppo[accedere alle API di servizi multimediali di Azure con .NET](media-services-dotnet-get-started-with-aad.md).

