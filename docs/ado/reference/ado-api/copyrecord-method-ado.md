---
title: CopyRecord, méthode (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d70dcba3d373b195950f90b6ef82c3d670844bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704947"
---
# <a name="copyrecord-method-ado"></a>CopyRecord, méthode (ADO)
Copie une entité représentée par un [enregistrement](../../../ado/reference/ado-api/record-object-ado.md) vers un autre emplacement.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Paramètres  
 *Source*  
 Facultatif. Un **chaîne** valeur qui contient une URL en spécifiant l’entité à copier (par exemple, un fichier ou répertoire). Si *Source* est omis ou spécifie une chaîne vide, le fichier ou le répertoire représenté par les [enregistrement](../../../ado/reference/ado-api/record-object-ado.md) sera copié.  
  
 *Destination*  
 Facultatif. Un **chaîne** valeur qui contient une URL en spécifiant l’emplacement où *Source* sera copié.  
  
 *UserName*  
 Facultatif. Un **chaîne** valeur qui contient l’ID utilisateur, si nécessaire, autorise l’accès *Destination*.  
  
 *Mot de passe*  
 Facultatif. Un **chaîne** valeur qui contient le mot de passe, si nécessaire, vérifie *nom d’utilisateur*.  
  
 *Options*  
 Facultatif. Un [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md) valeur qui a comme valeur par défaut de **adCopyUnspecified**. Spécifie le comportement de cette méthode.  
  
 *Async*  
 Facultatif. Un **booléenne** valeur qui, lorsque **True**, indique que cette opération doit être asynchrone.  
  
## <a name="return-value"></a>Valeur de retour  
 Un **chaîne** valeur qui retourne généralement la valeur de *Destination*. Toutefois, la valeur exacte retournée dépend du fournisseur.  
  
## <a name="remarks"></a>Notes  
 Les valeurs de *Source* et *Destination* ne doit pas être identiques ; sinon, une erreur d’exécution se produit. Au moins un des noms de serveur, chemin d’accès ou ressource doit être différent.  
  
 Tous les enfants (par exemple, les sous-répertoires) de *Source* sont copiés de manière récursive, à moins que **valeur adCopyNonRecursive** est spécifié. Dans une opération récursive, *Destination* ne doit pas être un sous-répertoire de *Source*; sinon, l’opération n’est pas terminée.  
  
 Cette méthode échoue si *Destination* identifie une entité existante (par exemple, un fichier ou répertoire), sauf si **adCopyOverWrite** est spécifié.  
  
> [!IMPORTANT]
>  Utilisez le **adCopyOverWrite** option judicieusement. Par exemple, la spécification de cette option lors de la copie d’un fichier dans un répertoire sera *supprimer* le répertoire et remplacez-le par le fichier.  
  
> [!NOTE]
>  URL à l’aide du modèle http appellent automatiquement le [fournisseur Microsoft OLE DB pour la publication Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Pour plus d’informations, consultez [URL absolues et relatives](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>S'applique à  
 [Record, objet (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
