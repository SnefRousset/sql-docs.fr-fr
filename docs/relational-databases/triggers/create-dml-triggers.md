---
title: "Cr&#233;er des d&#233;clencheurs DML | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-dml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "chiffrement [SQL Server], déclencheurs DML"
  - "résolution de nom différée, déclencheurs DML"
  - "WITH ENCRYPTION (clause)"
  - "IF UPDATE"
  - "instruction SET, déclencheurs DML"
  - "déclencheurs DML, programmation"
  - "test des changements de colonnes"
  - "résultats [SQL Server], déclencheurs DML"
ms.assetid: b2b52258-642b-462e-8e0f-18c09d2eccf4
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Cr&#233;er des d&#233;clencheurs DML
  Cette rubrique explique comment créer un déclencheur DML [!INCLUDE[tsql](../../includes/tsql-md.md)] à l’aide de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] et de l’instruction [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TRIGGER.  
  
##  <a name="Top"></a> Avant de commencer  
  
### Limitations et restrictions  
 Pour obtenir la liste des limitations et des restrictions liées à la création de déclencheurs DML, consultez [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
###  <a name="Permissions"></a> Autorisations  
 Nécessite l'autorisation ALTER sur la table ou la vue sur laquelle le déclencheur est créé.  
  
##  <a name="Procedures"></a> Comment créer un déclencheur DML  
 Vous pouvez utiliser l'un des éléments suivants :  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Utilisation de SQL Server Management Studio  
  
1.  Dans l' **Explorateur d'objets**, connectez-vous à une instance du [!INCLUDE[ssDE](../../includes/ssde-md.md)] et développez-la.  
  
2.  Développez successivement **Bases de données**, la base de données [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], **Tables**, puis la table **Purchasing.PurchaseOrderHeader**.  
  
3.  Cliquez avec le bouton droit sur **Déclencheurs**, puis sélectionnez **Nouveau déclencheur**.  
  
4.  Dans le menu **Requête** , cliquez sur **Spécifier les valeurs des paramètres du modèle**. Vous pouvez aussi appuyer sur Ctrl-Maj-M pour ouvrir la boîte de dialogue **Spécifier les valeurs des paramètres du modèle**.  
  
5.  Dans la boîte de dialogue **Spécifier les valeurs des paramètres du modèle** , entrez les valeurs suivantes pour les paramètres affichés.  
  
    |Paramètre|Valeur|  
    |---------------|-----------|  
    |Auteur|*Votre nom*|  
    |Date de création|*Date du jour*|  
    |Description|Vérifie le degré de solvabilité du fournisseur avant d'autoriser l'insertion d'une nouvelle commande fournisseur.|  
    |Schema_name|Purchasing|  
    |Trigger_Name|NewPODetail2|  
    |Table_Name|PurchaseOrderDetail|  
    |Data_Modification_Statement|Supprimez UPDATE et DELETE de la liste.|  
  
6.  Cliquez sur **OK**.  
  
7.  Dans l’**Éditeur de requête**, remplacez le commentaire `-- Insert statements for trigger here` par l’instruction suivante :  
  
    ```tsql  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
8.  Pour vérifier la validité de la syntaxe, dans le menu **Requête**, cliquez sur **Analyser**. Si un message d'erreur est retourné, comparez l'instruction avec les informations ci-dessus, apportez les corrections nécessaires et répétez cette étape.  
  
9. Pour créer le déclencheur DML, dans le menu **Requête**, cliquez sur **Exécuter**. Le déclencheur DML est créé en tant qu'objet dans la base de données.  
  
10. Pour afficher le déclencheur DML dans l’Explorateur d’objets, cliquez avec le bouton droit sur **Déclencheurs**, puis sélectionnez **Actualiser**.  
  
 [Avant de commencer](#Top)  
  
###  <a name="TsqlProcedure"></a> Utilisation de Transact-SQL  
  
1.  Dans l' **Explorateur d'objets**, connectez-vous à une instance du [!INCLUDE[ssDE](../../includes/ssde-md.md)] et développez-la.  
  
2.  Dans le menu **Fichier** , cliquez sur **Nouvelle requête**.  
  
3.  Copiez et collez l'exemple suivant dans la fenêtre de requête, puis cliquez sur **Exécuter**. Cet exemple crée le même déclencheur DML stocké que dans la procédure ci-dessus.  
  
    ```  
    -- Trigger valid for multirow and single row inserts  
    -- and optimal for single row inserts.  
    USE AdventureWorks2012;  
    GO  
    CREATE TRIGGER NewPODetail3  
    ON Purchasing.PurchaseOrderDetail  
    FOR INSERT AS  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
##  <a name="PowerShellProcedure"></a> [Avant de commencer](#Top)  
  
  