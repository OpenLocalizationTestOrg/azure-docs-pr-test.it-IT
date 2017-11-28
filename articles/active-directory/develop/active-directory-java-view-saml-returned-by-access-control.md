---
title: aaaView SAML restituito da hello servizio Access Control (linguaggio)
description: Informazioni su come tooview SAML restituito dal servizio di controllo di accesso di hello nelle applicazioni Java ospitato in Azure.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a><span data-ttu-id="2d830-103">Modalità di restituzione da hello Azure Access Control Service tooview SAML</span><span class="sxs-lookup"><span data-stu-id="2d830-103">How tooview SAML returned by hello Azure Access Control Service</span></span>
<span data-ttu-id="2d830-104">Questa guida illustra le modalità di restituzione tooyour applicazione dal servizio Azure Access Control (ACS) di hello hello tooview sottostante Security Assertion Markup Language (SAML).</span><span class="sxs-lookup"><span data-stu-id="2d830-104">This guide will show you how tooview hello underlying Security Assertion Markup Language (SAML) returned tooyour application by hello Azure Access Control Service (ACS).</span></span> <span data-ttu-id="2d830-105">Hello Guida si basa sui hello [come utenti Web con accesso controllo servizio Azure usando Eclipse tooAuthenticate](active-directory-java-authenticate-users-access-control-eclipse.md) argomento, il codice che visualizza le informazioni di hello SAML.</span><span class="sxs-lookup"><span data-stu-id="2d830-105">hello guide builds on hello [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays hello SAML information.</span></span> <span data-ttu-id="2d830-106">un'applicazione Hello completata avrà un aspetto simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="2d830-106">hello completed application will look similar toohello following.</span></span>

![Esempio di output SAML][saml_output]

<span data-ttu-id="2d830-108">Per ulteriori informazioni su ACS, vedere hello [passaggi successivi](#next_steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="2d830-108">For more information on ACS, see hello [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="2d830-109">Hello filtro di controllo di Azure Access Services è una versione community technology preview.</span><span class="sxs-lookup"><span data-stu-id="2d830-109">hello Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="2d830-110">Come versione preliminare, non è formalmente supportata da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2d830-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2d830-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2d830-111">Prerequisites</span></span>
<span data-ttu-id="2d830-112">attività hello toocomplete in questa guida completa hello campione [come utenti Web con accesso controllo servizio Azure usando Eclipse tooAuthenticate](active-directory-java-authenticate-users-access-control-eclipse.md) e utilizzarlo come punto iniziale per questa esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="2d830-112">toocomplete hello tasks in this guide, complete hello sample at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as hello starting point for this tutorial.</span></span>

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a><span data-ttu-id="2d830-113">Aggiungere hello JspWriter tooyour compilazione distribuzione e percorso assembly della libreria</span><span class="sxs-lookup"><span data-stu-id="2d830-113">Add hello JspWriter library tooyour build path and deployment assembly</span></span>
<span data-ttu-id="2d830-114">Aggiungere libreria hello contenente hello **javax.servlet.jsp.JspWriter** tooyour classe compilare assembly percorso e la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2d830-114">Add hello library that contains hello **javax.servlet.jsp.JspWriter** class tooyour build path and deployment assembly.</span></span> <span data-ttu-id="2d830-115">Se si utilizza Tomcat, libreria di hello è **jsp api.jar**, che si trova nella hello Apache **lib** cartella.</span><span class="sxs-lookup"><span data-stu-id="2d830-115">If you are using Tomcat, hello library is **jsp-api.jar**, which is located in hello Apache **lib** folder.</span></span>

1. <span data-ttu-id="2d830-116">In Project Explorer di Eclipse, fare clic sul **MyACSHelloWorld**, fare clic su **Build Path**, fare clic su **configurare Build Path**, fare clic su hello **librerie** scheda e quindi fare clic su **aggiungere file JAR esterna**.</span><span class="sxs-lookup"><span data-stu-id="2d830-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click hello **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="2d830-117">In hello **JAR selezione** finestra di dialogo, passare toohello necessarie JAR, selezionarlo e quindi fare clic su **aprire**.</span><span class="sxs-lookup"><span data-stu-id="2d830-117">In hello **JAR Selection** dialog, navigate toohello necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="2d830-118">Con hello **le proprietà per MyACSHelloWorld** finestra di dialogo ancora aperto, fare clic su **distribuzione Assembly**.</span><span class="sxs-lookup"><span data-stu-id="2d830-118">With hello **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="2d830-119">In hello **Assembly di distribuzione Web** finestra di dialogo, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2d830-119">In hello **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="2d830-120">In hello **nuova direttiva Assembly** finestra di dialogo, fare clic su **dei percorsi di compilazione Java** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2d830-120">In hello **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="2d830-121">Selezionare la libreria appropriata hello e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="2d830-121">Select hello appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="2d830-122">Fare clic su **OK** tooclose hello **le proprietà per MyACSHelloWorld** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2d830-122">Click **OK** tooclose hello **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-hello-jsp-file-toodisplay-saml"></a><span data-ttu-id="2d830-123">Modificare hello JSP file toodisplay SAML</span><span class="sxs-lookup"><span data-stu-id="2d830-123">Modify hello JSP file toodisplay SAML</span></span>
<span data-ttu-id="2d830-124">Modificare **index.jsp** toouse hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="2d830-124">Modify **index.jsp** toouse hello following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate hello child nodes of hello doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-hello-application"></a><span data-ttu-id="2d830-125">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="2d830-125">Run hello application</span></span>
1. <span data-ttu-id="2d830-126">Eseguire l'applicazione nell'emulatore di calcolo di hello o distribuire tooAzure, attenendosi alla procedura hello documentata in [come utenti Web con accesso controllo servizio Azure usando Eclipse tooAuthenticate](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="2d830-126">Run your application in hello computer emulator or deploy tooAzure, using hello steps documented at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="2d830-127">Avviare il browser e aprire l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="2d830-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="2d830-128">Dopo l'accesso dell'applicazione tooyour, si noterà informazioni SAML, inclusi l'asserzione di sicurezza hello fornita dal provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="2d830-128">After you log on tooyour application, you'll see SAML information, including hello security assertion provided by hello identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d830-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d830-129">Next steps</span></span>
<span data-ttu-id="2d830-130">toofurther esplorare funzionalità ACS e tooexperiment con scenari più sofisticati, vedere [Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="2d830-130">toofurther explore ACS's functionality and tooexperiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
