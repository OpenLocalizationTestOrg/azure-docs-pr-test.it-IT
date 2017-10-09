---
title: aaaHow tooConfigure l'autenticazione reciproca TLS per l'App Web
description: Informazioni su come tooconfigure client web app toouse certificato di autenticazione in TLS.
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: 8aeb9b35058fac50b8b38f6428207ad4a82d8637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a><span data-ttu-id="84215-103">Come tooConfigure l'autenticazione reciproca TLS per l'App Web</span><span class="sxs-lookup"><span data-stu-id="84215-103">How tooConfigure TLS Mutual Authentication for Web App</span></span>
## <a name="overview"></a><span data-ttu-id="84215-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="84215-104">Overview</span></span>
<span data-ttu-id="84215-105">È possibile limitare l'accesso tooyour Azure web app, consentendo di diversi tipi di autenticazione per tale.</span><span class="sxs-lookup"><span data-stu-id="84215-105">You can restrict access tooyour Azure web app by enabling different types of authentication for it.</span></span> <span data-ttu-id="84215-106">Un modo toodo è così tooauthenticate usando un certificato client quando è richiesta hello tramite TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="84215-106">One way toodo so is tooauthenticate using a client certificate when hello request is over TLS/SSL.</span></span> <span data-ttu-id="84215-107">Questo meccanismo è denominato l'autenticazione reciproca TLS o l'autenticazione del certificato client e questo articolo descrive come toosetup l'autenticazione del certificato client toouse app web.</span><span class="sxs-lookup"><span data-stu-id="84215-107">This mechanism is called TLS mutual authentication or client certificate authentication and this article will detail how toosetup your web app toouse client certificate authentication.</span></span>

> <span data-ttu-id="84215-108">**Nota:** se si accede al sito tramite HTTP e non HTTPS, non si riceveranno i certificati client.</span><span class="sxs-lookup"><span data-stu-id="84215-108">**Note:** If you access your site over HTTP and not HTTPS, you will not receive any client certificate.</span></span> <span data-ttu-id="84215-109">Pertanto, se l'applicazione richiede i certificati client non è consigliabile consentire le richieste applicazione tooyour tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="84215-109">So if your application requires client certificates you should not allow requests tooyour application over HTTP.</span></span>
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a><span data-ttu-id="84215-110">Configurare l'app Web per l'autenticazione del certificato client</span><span class="sxs-lookup"><span data-stu-id="84215-110">Configure Web App for Client Certificate Authentication</span></span>
<span data-ttu-id="84215-111">toosetup i certificati di client toorequire di app web che è necessario tooadd hello clientCertEnabled sito impostazione per l'app web e impostarlo tootrue.</span><span class="sxs-lookup"><span data-stu-id="84215-111">toosetup your web app toorequire client certificates you need tooadd hello clientCertEnabled site setting for your web app and set it tootrue.</span></span> <span data-ttu-id="84215-112">Questa impostazione non è attualmente disponibile tramite l'esperienza di gestione di hello in hello portale e API REST hello sarà necessaria tooaccomplish toobe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="84215-112">This setting is not currently available through hello management experience in hello Portal, and hello REST API will need toobe used tooaccomplish this.</span></span>

<span data-ttu-id="84215-113">È possibile utilizzare hello [ARMClient strumento](https://github.com/projectkudu/ARMClient) toomake è facile toocraft hello chiamata all'API REST.</span><span class="sxs-lookup"><span data-stu-id="84215-113">You can use hello [ARMClient tool](https://github.com/projectkudu/ARMClient) toomake it easy toocraft hello REST API call.</span></span> <span data-ttu-id="84215-114">Dopo l'accesso con lo strumento hello occorre hello tooissue comando seguente:</span><span class="sxs-lookup"><span data-stu-id="84215-114">After you log in with hello tool you will need tooissue hello following command:</span></span>

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

<span data-ttu-id="84215-115">tutti gli elementi di {} sostituzione con informazioni per l'app web e creazione di un file chiamato contenuto enableclientcert.json con hello JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="84215-115">replacing everything in {} with information for your web app and creating a file called enableclientcert.json with hello following JSON content:</span></span>

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

<span data-ttu-id="84215-116">Assicurarsi che valore hello toochange toowherever "location" app web è presente ad esempio North Central US o via di Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="84215-116">Make sure toochange hello value of "location" toowherever your web app is located e.g. North Central US or West US etc.</span></span>

<span data-ttu-id="84215-117">È inoltre possibile utilizzare hello tooflip https://resources.azure.com `clientCertEnabled` proprietà troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="84215-117">You can also use https://resources.azure.com tooflip hello `clientCertEnabled` property too`true`.</span></span>

> <span data-ttu-id="84215-118">**Nota:** se si esegue ARMClient da Powershell, è necessario hello tooescape simbolo @ per il file JSON hello con un apice inverso '.</span><span class="sxs-lookup"><span data-stu-id="84215-118">**Note:** If you run ARMClient from Powershell, you will need tooescape hello @ symbol for hello JSON file with a back tick \`.</span></span>
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a><span data-ttu-id="84215-119">L'accesso a hello Client certificato da Your App Web</span><span class="sxs-lookup"><span data-stu-id="84215-119">Accessing hello Client Certificate From Your Web App</span></span>
<span data-ttu-id="84215-120">Se si utilizza ASP.NET e configura l'autenticazione del certificato client toouse app, il certificato di hello sarà disponibile tramite hello **HttpRequest.ClientCertificate** proprietà.</span><span class="sxs-lookup"><span data-stu-id="84215-120">If you are using ASP.NET and configure your app toouse client certificate authentication, hello certificate will be available through hello **HttpRequest.ClientCertificate** property.</span></span> <span data-ttu-id="84215-121">Per altri stack di applicazione, il certificato client di hello sarà disponibile nell'app tramite un valore con codificata base64 nell'intestazione della richiesta "X-ARR-ClientCert" hello.</span><span class="sxs-lookup"><span data-stu-id="84215-121">For other application stacks, hello client cert will be available in your app through a base64 encoded value in hello "X-ARR-ClientCert" request header.</span></span> <span data-ttu-id="84215-122">L'applicazione può creare un certificato da questo valore e quindi usarlo a scopo di autenticazione e autorizzazione nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="84215-122">Your application can create a certificate from this value and then use it for authentication and authorization purposes in your application.</span></span>

## <a name="special-considerations-for-certificate-validation"></a><span data-ttu-id="84215-123">Considerazioni speciali per la convalida del certificato</span><span class="sxs-lookup"><span data-stu-id="84215-123">Special Considerations for Certificate Validation</span></span>
<span data-ttu-id="84215-124">certificato client Hello viene inviato toohello applicazione non passa attraverso qualsiasi convalida dalla piattaforma di App Web di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="84215-124">hello client certificate that is sent toohello application does not go through any validation by hello Azure Web Apps platform.</span></span> <span data-ttu-id="84215-125">Convalidare il certificato è responsabilità di hello dell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="84215-125">Validating this certificate is hello responsibility of hello web app.</span></span> <span data-ttu-id="84215-126">Ecco un esempio di codice ASP.NET che convalida le proprietà del certificato a scopo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="84215-126">Here is sample ASP.NET code that validates certificate properties for authentication purposes.</span></span>

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read hello certificate from hello header into an X509Certificate2 object
            // Display properties of hello certificate on hello page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept hello certificate as a valid certificate if all hello conditions below are met:
                // 1. hello certificate is not expired and is active for hello current time on server.
                // 2. hello subject name of hello certificate has hello common name nildevecc
                // 3. hello issuer name of hello certificate has hello common name nildevecc and organization name Microsoft Corp
                // 4. hello thumbprint of hello certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained tooa Trusted Root Authority (or revoked) on hello server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want tootest if hello certificate chains tooa Trusted Root Authority you can uncomment hello code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }
