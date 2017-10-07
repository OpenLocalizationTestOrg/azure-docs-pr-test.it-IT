---
title: insieme di credenziali chiave di Azure da un'applicazione Web aaaUse | Documenti Microsoft
description: "Utilizzare questa esercitazione toohelp si apprenderà come toouse Azure chiave dell'insieme di credenziali da un'applicazione web."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a>Usare l'insieme di credenziali chiave di Azure da un'applicazione Web
## <a name="introduction"></a>Introduzione
Utilizzare questa esercitazione toohelp si apprenderà come toouse Azure chiave dell'insieme di credenziali da un'applicazione web in Azure. Illustra il processo di hello dell'accesso a una chiave privata da un insieme di credenziali chiave di Azure in modo che può essere utilizzato nell'applicazione web.

**Toocomplete tempo stimato:** 15 minuti

Per informazioni generali sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali chiave di Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario disporre di hello seguenti:

* Un segreto tooa URI in un insieme di credenziali chiave di Azure
* Un ID Client e un segreto Client per un'applicazione web registrati con Azure Active Directory che ha accesso tooyour insieme di credenziali chiave
* Un'applicazione Web. Abbiamo mostrato passaggi hello per un'applicazione ASP.NET MVC distribuito in Azure come App Web.

> [!NOTE]
> È essenziale di aver completato i passaggi di hello elencati in [introduzione insieme credenziali chiavi Azure](key-vault-get-started.md) per questa esercitazione in modo da avere hello hello Client ID e segreto tooa URI e il segreto Client per un'applicazione web.
> 
> 

un'applicazione web Hello che accederà a insieme di credenziali chiave hello è hello uno che viene registrato in Azure Active Directory e sia stato assegnato l'accesso tooyour insieme di credenziali chiave. In caso non hello, tornare indietro tooRegister un'applicazione nell'esercitazione Introduzione hello e ripetere i passaggi di hello elencati.

Questa esercitazione è progettata per gli sviluppatori web che supportano hello di base per creare applicazioni web in Azure. Per altre informazioni sulle app Web di Azure, vedere [Panoramica delle app Web](../app-service-web/app-service-web-overview.md).

## <a id="packages"></a>Aggiungere i pacchetti NuGet
Sono disponibili due pacchetti che l'applicazione web deve toohave installato.

* Active Directory Authentication Library: contiene i metodi per interagire con Azure Active Directory e gestire l'identità utente
* Azure Key Vault Library: contiene i metodi per interagire con l'insieme di credenziali chiave di Azure

Entrambi questi pacchetti possono essere installati utilizzando la Console di gestione pacchetti utilizzando il comando Install-Package hello hello.

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Modificare Web.Config
Sono disponibili tre impostazioni di applicazioni che richiedono file Web. config di toobe toohello aggiunto come indicato di seguito.

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


Se non si ha intenzione toohost dell'applicazione come un'App Web di Azure, è consigliabile aggiungere hello effettivo ClientId, segreto Client e segreto URI valori toohello Web. config. In caso contrario, lasciare i valori fittizi perché i valori effettivi hello verrà aggiunta in hello portale di Azure per un ulteriore livello di sicurezza.

## <a id="gettoken"></a>Aggiungere un Token di accesso di tooGet (metodo)
In hello toouse ordine API dell'insieme di credenziali chiave, è necessario un token di accesso. Chiave dell'insieme di credenziali Client Hello gestisce le chiamate API dell'insieme di credenziali chiave toohello ma è necessario toosupply con una funzione che ottiene il token di accesso di hello.  

Di seguito è tooget codice hello un token di accesso da Azure Active Directory. Questo codice può far accedere ovunque nell'applicazione. In genere tooadd un'utilità o una classe EncryptionHelper.  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> Utilizzo di un ID Client e il segreto Client è tooauthenticate modo più semplice di hello un'applicazione Azure AD. Utilizzarlo nell'applicazione Web consente una separazione dei compiti e maggiore controllo sulla gestione delle chiavi. Ma si basa sull'inserimento di hello segreto Client nelle impostazioni di configurazione che, per alcuni, possono essere rischiose come come inserimento segreto hello che si desidera tooprotect nelle impostazioni di configurazione. Per una discussione su come toouse un ID Client e il certificato anziché tooauthenticate ID Client e il segreto Client hello applicazione Azure AD, vedere di seguito.
> 
> 

## <a id="appstart"></a>Recuperare il segreto hello su avvio applicazione
È ora base hello toocall API dell'insieme di credenziali chiave di codice e recuperare il segreto hello. Hello codice riportato di seguito è possibile inserire qualsiasi fino a quando viene chiamato prima che sia necessario toouse è. È stata inserita questo codice nell'evento di avvio dell'applicazione hello in Global. asax hello in modo che viene eseguita una volta all'avvio e rende disponibili per l'applicazione hello segreto di hello.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>Aggiungere le impostazioni dell'App nel portale di Azure (facoltativo) hello
Se si dispone di un'App Web di Azure è ora possibile aggiungere i valori effettivi per hello AppSettings hello nel portale di Azure hello. In questo modo, i valori effettivi hello non saranno inclusi nel file Web. config hello ma protetto tramite hello portale in cui si dispone di funzionalità di controllo di accesso distinti. Questi valori verranno sostituiti dai valori hello immesso nel file Web. config. Verificare che hello stessi nomi hello.

![Impostazioni dell'applicazione visualizzate nel portale di Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>Autenticazione con un certificato anziché un client secret
Un altro modo tooauthenticate un'applicazione Azure AD è tramite un ID Client e un certificato anziché un ID Client e il segreto Client. Seguenti sono hello passaggi toouse un certificato in un'applicazione Web di Azure:

1. Ottenere o creare un certificato
2. Associare hello certificato a un'applicazione Azure AD
3. Aggiungere hello toouse di App Web tooyour codice certificato
4. Aggiungere un tooyour certificato App Web

**Ottenere o creare un certificato** Per i nostri scopi rendiamo un certificato di prova. Ecco un paio di comandi che è possibile utilizzare in un prompt dei comandi per sviluppatori di toocreate un certificato. Cambiare directory toowhere che Hello i file di certificato creato.  Inoltre, per hello all'inizio e data di fine del certificato hello, utilizzare hello data corrente più 1 anno.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Prendere nota della data di fine hello e una password di hello per PFX hello (in questo esempio: 31/07/2016 e test123). Saranno necessarie più avanti.

Per ulteriori informazioni sulla creazione di un certificato di prova, vedere [Procedura: creare il proprio certificato di prova](https://msdn.microsoft.com/library/ff699202.aspx)

**Associare hello certificati con un'applicazione Azure AD** dopo aver creato un certificato, è necessario tooassociate con un'applicazione Azure AD. Attualmente, hello portale di Azure non supporta questo flusso di lavoro. Questo può essere completato tramite PowerShell. Eseguire hello seguente certificato hello tooassoicate di comandi con un'applicazione hello Azure AD:

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

Dopo aver eseguito questi comandi, è possibile visualizzare un'applicazione hello in Azure AD. Durante la ricerca, assicurarsi di selezionare "Applicazioni di proprietà dell'azienda" anziché "Applicazioni usate dall'azienda" nella finestra di dialogo Ricerca hello.

toolearn informazioni sugli oggetti di Azure Active Directory dell'applicazione e agli oggetti, vedere [oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md)

**Aggiungere hello toouse di App Web tooyour codice certificato** ora si aggiungerà codice tooyour App Web tooaccess hello cert e utilizzarlo per l'autenticazione.

Prima di tutto è cert hello tooaccess di codice.

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


Si noti che hello StoreLocation è CurrentUser anziché LocalMachine. E che ci stiamo fornendo toohello 'false' Find (metodo), poiché si sta usando un certificato di test.

Di seguito è riportato il codice che usa hello CertificateHelper e crea un ClientAssertionCertificate necessaria per l'autenticazione.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


Di seguito è hello nuovo codice tooget hello token di accesso. Questo strumento sostituisce hello GetToken (metodo) precedente. È stato indicato un nome diverso per comodità.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

È stato inserito tutto il codice nella classe Utils del progetto Web App per semplificarne l'utilizzo.

ultima modifica del codice Hello è hello metodo Application_Start. È prima necessario toocall hello hello tooload di metodo GetCert() ClientAssertionCertificate. E quindi si modifica metodo di callback hello che viene fornito quando si crea un nuovo KeyVaultClient. Si noti che questa impostazione sostituisce il codice hello che si è verificato in precedenza.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Aggiungere un certificato tooyour App Web, tramite il portale di Azure hello** aggiunta tooyour un certificato App Web è un processo semplice in due passaggi. In primo luogo, andare toohello portale di Azure e passare tooyour App Web. Nel pannello delle impostazioni hello per le App Web, fare clic sulla voce di hello per "i domini personalizzati e SSL". In hello pannello visualizzato è saranno hello tooupload in grado di certificato creato in precedenza, KVWebApp.pfx, che è importante ricordare la password di hello per pfx hello.

![Aggiunta di un tooa certificato App Web nel portale di Azure hello][2]

ultimo elemento che è necessario toodo Hello è tooadd un tooyour di impostazione dell'applicazione Web App con sito Web di nome hello\_carico\_certificati e il valore *. Ciò garantisce che siano caricati tutti i certificati. Se si desidera hello solo tooload i certificati che è stato caricato, quindi è possibile immettere un elenco delimitato da virgole di relative identificazioni personali.

toolearn più sull'aggiunta di un tooa certificato App Web, vedere [tramite certificati nelle applicazioni di siti Web di Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**Aggiungere un insieme di credenziali di tooKey certificato come un segreto** invece di caricare direttamente il toohello certificato del servizio Web App, è possibile archiviarla nell'insieme di credenziali chiave come chiave privata e distribuirlo da questa posizione. Si tratta di un processo in due passaggi descritto nella seguente post di blog, hello [distribuzione certificato dell'App Web Azure tramite l'insieme di credenziali chiave](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>Passaggi successivi
Per i riferimenti alla programmazione, vedere [Informazioni di riferimento sull'API client C# dell'insieme di credenziali chiave di Azure](https://msdn.microsoft.com/library/azure/dn903628.aspx).

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
