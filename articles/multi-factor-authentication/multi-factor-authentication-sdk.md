---
title: aaaMFA software development kit per App personalizzate | Documenti Microsoft
description: "Questo articolo illustra come toodownload e utilizzare hello verifica in due passaggi tooenable di autenticazione a più fattori di Azure SDK per le app personalizzate."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>Compilazione di Multi-Factor Authentication in app personalizzate (SDK)

Consente di Azure multi-Factor Authentication Software Development Kit (SDK) di Hello in che compilare verifica in due passaggi direttamente hello Accedi o transazione processi delle applicazioni nel tenant di Azure AD.

Hello multi-Factor Authentication SDK è disponibile per c#, Visual Basic (.NET), Java, Perl, PHP e Ruby. Hello SDK fornisce un wrapper di verifica in due passaggi. Include tutto ciò che occorre toowrite del codice, inclusi i file di codice sorgente commentati, file di esempio e un file ReadMe dettagliato. Ogni SDK include anche un certificato e chiave privata per crittografare le transazioni che sono univoci tooyour Provider multi-Factor Authentication. Se si dispone di un provider, è possibile scaricare hello SDK in tutti i linguaggi e formati in base alle esigenze.

struttura Hello di hello API in hello multi-Factor Authentication SDK è semplice. Effettuare una singola funzione di chiamata API tooan con i parametri di opzione di multi-factor hello (ad esempio, la modalità di verifica) e dati utente (ad esempio toocall numero di telefono hello o hello PIN numerico toovalidate). API Hello convertono la chiamata di funzione hello in toohello le richieste di servizi web basati su cloud di servizio Azure multi-Factor Authentication. Tutte le chiamate devono includere un certificato privato di toohello di riferimento è incluso in ogni SDK.

Hello API non dispone di accesso toousers registrato in Azure Active Directory, è necessario fornire le informazioni utente in un file o database. Hello API fornisce inoltre funzionalità di gestione di registrazione o l'utente, pertanto è necessario toobuild tali processi nell'applicazione.

> [!IMPORTANT]
> toodownload hello SDK, è necessario un Provider di Azure multi-Factor Authentication toocreate anche se si dispone di licenze Azure MFA, Azure ad Premium o EMS. Se si dispone già di licenze a tale scopo, creare un Provider di Azure multi-Factor Authentication, assicurarsi che toocreate hello Provider con hello **Per utente abilitato** modello. Quindi, collegare directory che contiene le licenze di Azure MFA, Azure AD Premium o EMS hello toohello del Provider hello. Questa configurazione assicura che verrà addebitato solo se si dispone di più utenti univoci utilizzando hello SDK numero hello di licenze possedute.


## <a name="download-hello-sdk"></a>Scaricare il SDK di hello
Download hello Azure multi-Factor SDK richiede una [Provider di Azure multi-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md).  Questo richiede una sottoscrizione di Azure completa, anche se si possiedono licenze di Azure MFA, Azure AD Premium o Enterprise Mobility Suite.  hello toodownload SDK, passare toohello portale di gestione a più fattori. È possibile raggiungere il portale di hello gestendo hello direttamente i Provider di autenticazione a più fattori, oppure facendo clic su hello **"Go toohello portale"** collegamento nella pagina Impostazioni servizio di autenticazione a più fattori hello.

### <a name="download-from-hello-azure-classic-portal"></a>Scaricare dal portale di Azure classico hello
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) come amministratore.
2. A sinistra di hello, selezionare **Active Directory**.
3. Nella pagina Active Directory hello in select top hello **provider multi-Factor Authentication**
4. Nella parte inferiore di hello selezionare **Gestisci**. Viene aperta una nuova pagina.
5. Scegliere a sinistra, nella parte inferiore di hello, hello **SDK**.
   <center>![Scaricare](./media/multi-factor-authentication-sdk/download.png)</center>
6. Selezionare una lingua hello desiderata e fare clic sui collegamenti di download associati hello uno.
7. Salvare il download di hello.

### <a name="download-from-hello-service-settings"></a>Scaricare da impostazioni del servizio hello
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) come amministratore.
2. A sinistra di hello, selezionare **Active Directory**.
3. Fare doppio clic sull'istanza di Azure AD.
4. Al clic superiore hello **Configura**
5. In Multi-Factor Authentication selezionare **Gestisci impostazioni del servizio**
   ![Download](./media/multi-factor-authentication-sdk/download2.png)
6. Nella pagina Impostazioni servizi hello in basso hello hello fare clic su **Go toohello portale**. Viene aperta una nuova pagina.
   ![Scaricare](./media/multi-factor-authentication-sdk/download3a.png)
7. Scegliere a sinistra, nella parte inferiore di hello, hello **SDK**.
8. Selezionare una lingua hello desiderata e fare clic sui collegamenti di download associati hello uno.
9. Salvare il download di hello.

## <a name="whats-in-hello-sdk"></a>Novità in hello SDK
Hello SDK include hello seguenti elementi:

* **README**. Viene illustrato come toouse hello API di autenticazione a più fattori in un'applicazione nuova o esistente.
* **File di origine** per Multi-Factor Authentication
* **Certificato client** utilizzare toocommunicate con hello servizio multi-Factor Authentication
* **Chiave privata** certificato hello
* **Risultati delle chiamate.** Un elenco di codici risultato chiamata. tooopen questo file, utilizzare un'applicazione con formattazione del testo, ad esempio WordPad. Hello utilizzare tootest codici risultato chiamata e risoluzione dei problemi di implementazione di hello di multi-Factor Authentication nell'applicazione. Non sono codici di stato di autenticazione.
* **Esempi.** Codice di esempio per un'implementazione di base funzionante di Multi-Factor Authentication.

> [!WARNING]
> certificato client hello è un certificato privato univoco generato per un utente. Non condividere o perdere questo file. Se per la protezione di hello tooensuring chiave delle comunicazioni con il servizio multi-Factor Authentication hello.

## <a name="code-sample"></a>Esempio di codice
In questo esempio di codice viene illustrato come toouse Ciao API hello vocale modalità standard di Azure multi-Factor Authentication SDK tooadd chiama applicazione tooyour di verifica. Modalità standard è una chiamata telefonica che hello tooby risponde utente premendo il tasto di # hello.

In questo esempio utilizza hello c# .NET 2.0 multi-Factor Authentication SDK in un'applicazione ASP.NET di base con logica sul lato server c#, ma il processo di hello è simile in altri linguaggi. Poiché hello SDK include file di origine, non eseguibili, è possibile compilare i file hello e farvi riferimento o includerli direttamente nell'applicazione.

> [!NOTE]
> Quando si implementa multi-Factor Authentication, utilizzare metodi aggiuntivi di hello (telefonata o SMS) come toosupplement secondario e terziario verifica il metodo di autenticazione principale (nome utente e password). Questi metodi non sono progettati come metodi di autenticazione principale.

### <a name="code-sample-overview"></a>Panoramica dell'esempio di codice
Questo codice di esempio per un'applicazione demo web semplice Usa una telefonata con un # risposta chiave tooverify hello autenticazione utente. Questo fattore telefonata è noto in Multi-Factor Authentication come modalità standard.

codice sul lato client Hello non include tutti gli elementi specifici di multi-Factor Authentication. Fattori di autenticazione aggiuntivi hello sono indipendenti l'autenticazione principale hello, è possibile aggiungere senza modificare l'interfaccia hello esistente sign-on. Ciao API hello multi-Factor SDK consentono di personalizzare l'esperienza utente hello, ma potrebbe non essere necessario toochange nulla affatto.

il codice lato server Hello aggiunge l'autenticazione in modalità standard nel passaggio 2. Crea un oggetto PfAuthParams con parametri hello che sono necessari per la verifica in modalità standard: nome utente, numero e la modalità di telefono e hello percorso toohello certificato client (CertFilePath), che è obbligatorio in ogni chiamata. Per una dimostrazione di tutti i parametri PfAuthParams, vedere il file di esempio hello in hello SDK.

Successivamente, il codice di hello passa hello PfAuthParams oggetto toohello pf_authenticate() una funzione. valore restituito di Hello indica hello riuscita o meno dell'autenticazione hello. Hello parametri, callStatus e errorID, contengono le informazioni sul risultato chiamata aggiuntiva. i codici risultato chiamata Hello sono documentati nel file di risultati di chiamata hello in hello SDK.

Questa implementazione minima può essere scritta in poche righe. Nel codice di produzione, tuttavia, è necessario includere la gestione degli errori più sofisticati, il codice di database aggiuntivo e un'esperienza utente avanzata.

### <a name="web-client-code"></a>Codice client web
Hello seguito è riportato il codice client web per una pagina demo.

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a>Codice lato server
Nel seguente codice lato server di hello, multi-Factor Authentication è configurato ed eseguire nel passaggio 2. Modalità standard (MODE_STANDARD) è che un utente di hello toowhich telefonata risponde premendo il tasto di # hello.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
