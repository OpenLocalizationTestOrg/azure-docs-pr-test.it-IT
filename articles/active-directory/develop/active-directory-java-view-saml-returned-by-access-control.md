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
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a>Modalità di restituzione da hello Azure Access Control Service tooview SAML
Questa guida illustra le modalità di restituzione tooyour applicazione dal servizio Azure Access Control (ACS) di hello hello tooview sottostante Security Assertion Markup Language (SAML). Hello Guida si basa sui hello [come utenti Web con accesso controllo servizio Azure usando Eclipse tooAuthenticate](active-directory-java-authenticate-users-access-control-eclipse.md) argomento, il codice che visualizza le informazioni di hello SAML. un'applicazione Hello completata avrà un aspetto simile toohello seguente.

![Esempio di output SAML][saml_output]

Per ulteriori informazioni su ACS, vedere hello [passaggi successivi](#next_steps) sezione.

> [!NOTE]
> Hello filtro di controllo di Azure Access Services è una versione community technology preview. Come versione preliminare, non è formalmente supportata da Microsoft.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
attività hello toocomplete in questa guida completa hello campione [come utenti Web con accesso controllo servizio Azure usando Eclipse tooAuthenticate](active-directory-java-authenticate-users-access-control-eclipse.md) e utilizzarlo come punto iniziale per questa esercitazione hello.

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a>Aggiungere hello JspWriter tooyour compilazione distribuzione e percorso assembly della libreria
Aggiungere libreria hello contenente hello **javax.servlet.jsp.JspWriter** tooyour classe compilare assembly percorso e la distribuzione. Se si utilizza Tomcat, libreria di hello è **jsp api.jar**, che si trova nella hello Apache **lib** cartella.

1. In Project Explorer di Eclipse, fare clic sul **MyACSHelloWorld**, fare clic su **Build Path**, fare clic su **configurare Build Path**, fare clic su hello **librerie** scheda e quindi fare clic su **aggiungere file JAR esterna**.
2. In hello **JAR selezione** finestra di dialogo, passare toohello necessarie JAR, selezionarlo e quindi fare clic su **aprire**.
3. Con hello **le proprietà per MyACSHelloWorld** finestra di dialogo ancora aperto, fare clic su **distribuzione Assembly**.
4. In hello **Assembly di distribuzione Web** finestra di dialogo, fare clic su **Aggiungi**.
5. In hello **nuova direttiva Assembly** finestra di dialogo, fare clic su **dei percorsi di compilazione Java** e quindi fare clic su **Avanti**.
6. Selezionare la libreria appropriata hello e fare clic su **fine**.
7. Fare clic su **OK** tooclose hello **le proprietà per MyACSHelloWorld** finestra di dialogo.

## <a name="modify-hello-jsp-file-toodisplay-saml"></a>Modificare hello JSP file toodisplay SAML
Modificare **index.jsp** toouse hello seguente codice.

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

## <a name="run-hello-application"></a>Eseguire un'applicazione hello
1. Eseguire l'applicazione nell'emulatore di calcolo di hello o distribuire tooAzure, attenendosi alla procedura hello documentata in [come utenti Web con accesso controllo servizio Azure usando Eclipse tooAuthenticate](active-directory-java-authenticate-users-access-control-eclipse.md).
2. Avviare il browser e aprire l'applicazione Web. Dopo l'accesso dell'applicazione tooyour, si noterà informazioni SAML, inclusi l'asserzione di sicurezza hello fornita dal provider di identità hello.

## <a name="next-steps"></a>Passaggi successivi
toofurther esplorare funzionalità ACS e tooexperiment con scenari più sofisticati, vedere [Access Control Service 2.0][Access Control Service 2.0].

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
