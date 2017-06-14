---
title: "Méthodes de traitement par lots | Documents Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- methods [Reporting Services], batches
- BatchHeader SOAP header
- Web service [Reporting Services], methods
- Report Server Web service, batching
- batches [Reporting Services]
- XML Web service [Reporting Services], methods
- locking [Reporting Services]
- multiple Web service methods
ms.assetid: 86435534-c9fe-4b49-b88c-7fb6d21976b0
caps.latest.revision: 36
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8b08c9f44efd416e3d5c9f24cb54f74569ba2882
ms.contentlocale: fr-fr
ms.lasthandoff: 06/13/2017

---
# <a name="batching-methods"></a>Méthodes de traitement par lot
  L'utilisation d'en-têtes SOAP dans [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vous permet d'inclure plusieurs méthodes Web Service dans une même opération. Les méthodes sont exécutées dans la portée d'une transaction de base de données unique, dans l'ordre de leur appel.  
  
 La restauration est un avantage offert par l'utilisation de plusieurs méthodes de traitements par lots. En cas d'erreur sur un appel de méthode au cours de l'exécution d'un lot, le serveur de rapports arrête l'exécution du lot et restaure les opérations précédentes. Cette opération est utile lorsqu'un appel de méthode dépend de l'achèvement réussi d'autres appels de méthode dans ce lot.  
  
 Le service Web ne fournit pas de sémantique de verrouillage pour les traitements par lots de plusieurs méthodes. Les lignes dans la base de données du serveur de rapports ne sont pas verrouillées pour la mise à jour tant que le message n'a pas été envoyé au serveur et la commande Execute appelée.  
  
 Il n'y a pas non plus de contrôles concurrentiels pour garantir que la base de données n'a pas changé depuis la dernière lecture des données. Si deux clients modifient le même élément, la dernière mise à jour réussit si les paramètres sont encore valides (par exemple, l'élément n'a pas été renommé).  
  
 L'exemple suivant appelle la méthode <xref:ReportService2005.ReportingService2005.CreateFolder%2A> trois fois et exécute ces appels comme un lot unique. Si un des appels à <xref:ReportService2005.ReportingService2005.CreateFolder%2A> échoue, le lot entier est annulé.  
  
```vb  
Imports System  
Imports System.Web.Services.Protocols  
Imports myNamespace.MyReferenceName  
  
Class Sample  
    Sub Main(args() As String)  
        Dim rs As New ReportingService2005()  
        rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
      ' Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/ReportService2005.asmx"  
  
        Dim bh As New BatchHeader()  
  
        bh.BatchId = service.CreateBatch()  
        rs.BatchHeaderValue = bh  
        rs.CreateFolder("New Folder1", "/", Nothing)  
        rs.CreateFolder("New Folder2", "/", Nothing)  
        rs.CreateFolder("New Folder3", "/", Nothing)  
  
        Console.WriteLine("Creating folders...")  
        rs.BatchHeaderValue = bh  
        rs.ExecuteBatch()  
        Console.WriteLine("Folders created successfully.")  
  
        rs.BatchHeaderValue = Nothing  
    End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.Web.Services.Protocols;   
using myNamespace.MyReferenceName;  
  
class Sample  
{  
    static void Main(string[] args)  
    {  
        ReportingService2005 rs = new ReportingService2005();  
        rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
      // Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/ReportService2005.asmx"  
  
        BatchHeader bh = new BatchHeader();  
  
        bh1.BatchID = service.CreateBatch();  
        rs.BatchHeaderValue = bh;  
        rs.CreateFolder("New Folder1", "/", null);  
        rs.CreateFolder("New Folder2", "/", null);  
        rs.CreateFolder("New Folder3", "/", null);  
  
        Console.WriteLine("Creating folders...");  
        rs.BatchHeaderValue = bh1;  
        rs.ExecuteBatch();  
        Console.WriteLine("Folders created successfully.");  
  
        rs.BatchHeaderValue = null;  
    }  
}  
```  
  
## <a name="see-also"></a>Voir aussi  
 <xref:ReportService2005.ReportingService2005.CancelBatch%2A>   
 <xref:ReportService2005.ReportingService2005.CreateBatch%2A>   
 [Informations techniques de référence &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)   
 [À l’aide de Reporting Services des en-têtes SOAP](../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)  
  
  