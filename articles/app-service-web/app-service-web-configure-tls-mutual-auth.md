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
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a>Come tooConfigure l'autenticazione reciproca TLS per l'App Web
## <a name="overview"></a>Panoramica
È possibile limitare l'accesso tooyour Azure web app, consentendo di diversi tipi di autenticazione per tale. Un modo toodo è così tooauthenticate usando un certificato client quando è richiesta hello tramite TLS/SSL. Questo meccanismo è denominato l'autenticazione reciproca TLS o l'autenticazione del certificato client e questo articolo descrive come toosetup l'autenticazione del certificato client toouse app web.

> **Nota:** se si accede al sito tramite HTTP e non HTTPS, non si riceveranno i certificati client. Pertanto, se l'applicazione richiede i certificati client non è consigliabile consentire le richieste applicazione tooyour tramite HTTP.
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a>Configurare l'app Web per l'autenticazione del certificato client
toosetup i certificati di client toorequire di app web che è necessario tooadd hello clientCertEnabled sito impostazione per l'app web e impostarlo tootrue. Questa impostazione non è attualmente disponibile tramite l'esperienza di gestione di hello in hello portale e API REST hello sarà necessaria tooaccomplish toobe utilizzato.

È possibile utilizzare hello [ARMClient strumento](https://github.com/projectkudu/ARMClient) toomake è facile toocraft hello chiamata all'API REST. Dopo l'accesso con lo strumento hello occorre hello tooissue comando seguente:

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

tutti gli elementi di {} sostituzione con informazioni per l'app web e creazione di un file chiamato contenuto enableclientcert.json con hello JSON seguente:

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

Assicurarsi che valore hello toochange toowherever "location" app web è presente ad esempio North Central US o via di Stati Uniti occidentali.

È inoltre possibile utilizzare hello tooflip https://resources.azure.com `clientCertEnabled` proprietà troppo`true`.

> **Nota:** se si esegue ARMClient da Powershell, è necessario hello tooescape simbolo @ per il file JSON hello con un apice inverso '.
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a>L'accesso a hello Client certificato da Your App Web
Se si utilizza ASP.NET e configura l'autenticazione del certificato client toouse app, il certificato di hello sarà disponibile tramite hello **HttpRequest.ClientCertificate** proprietà. Per altri stack di applicazione, il certificato client di hello sarà disponibile nell'app tramite un valore con codificata base64 nell'intestazione della richiesta "X-ARR-ClientCert" hello. L'applicazione può creare un certificato da questo valore e quindi usarlo a scopo di autenticazione e autorizzazione nell'applicazione.

## <a name="special-considerations-for-certificate-validation"></a>Considerazioni speciali per la convalida del certificato
certificato client Hello viene inviato toohello applicazione non passa attraverso qualsiasi convalida dalla piattaforma di App Web di Azure hello. Convalidare il certificato è responsabilità di hello dell'app web hello. Ecco un esempio di codice ASP.NET che convalida le proprietà del certificato a scopo di autenticazione.

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
