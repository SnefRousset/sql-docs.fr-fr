---
title: WillExecute, événement (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 234a0eeba57958063a6f2eedb8510486df8a53a0
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255502"
---
# <a name="willexecute-event-ado"></a>WillExecute, événement (ADO)
Le **WillExecute** événement est appelé juste avant l’exécution d’une commande en attente sur une connexion.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Paramètres  
 *Source*  
 Un **chaîne** qui contient une commande SQL ou un nom de procédure stockée.  
  
 *CursorType*  
 Un [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) qui contient le type de curseur pour le **Recordset** qui s’ouvre. Avec ce paramètre, vous pouvez modifier le curseur à n’importe quel type pendant un **Recordset**[méthode Open (objet Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) opération. *CursorType* seront ignorés pour d’autres opérations.  
  
 *LockType*  
 Un [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) qui contient le type de verrou pour la **Recordset** qui s’ouvre. Avec ce paramètre, vous pouvez modifier le verrou à n’importe quel type pendant un **RecordsetOpen** opération. *LockType* seront ignorés pour d’autres opérations.  
  
 *Options*  
 Un **Long** valeur qui indique les options qui peuvent être utilisées pour exécuter la commande ou ouvrir le **Recordset**.  
  
 *adStatus*  
 Un [il ne](../../../ado/reference/ado-api/eventstatusenum.md) valeur d’état qui peut-être être **adStatusCantDeny** ou **adStatusOK** lorsque cet événement est appelé. S’il s’agit **adStatusCantDeny**, cet événement ne peut pas demander l’annulation de l’opération en attente.  
  
 *pCommand*  
 Le [commande objet (ADO)](../../../ado/reference/ado-api/command-object-ado.md) de l’objet pour lequel cette notification d’événement s’applique.  
  
 *pRecordset*  
 Le [objet Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) de l’objet pour lequel cette notification d’événement s’applique.  
  
 *pConnection*  
 Le [objet Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) de l’objet pour lequel cette notification d’événement s’applique.  
  
## <a name="remarks"></a>Notes  
 Un **WillExecute** événement peut survenir en raison d’une connexion.  [Execute, méthode (objet Connection ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [Execute, méthode (commande ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md), ou [méthode Open (objet Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) méthode le *pConnection* doit de paramètre toujours contenir une référence valide à un **connexion** objet. Si l’événement est dû à **Connection.Execute**, le *Connection* et *pCommand* paramètres sont définis sur **rien**. Si l’événement est dû à **Recordset.Open**, le *Connection* paramètre référencera le **Recordset** objet et le *pCommand* paramètre est défini sur **rien**. Si l’événement est dû à **Command.Execute**, le *pCommand* paramètre référencera le **commande** objet et le *Connection* paramètre est défini sur **rien**.  
  
 **WillExecute** vous permet d’examiner et modifier les paramètres d’exécution en attente. Cet événement peut retourner une demande d’annulation de la commande en attente.  
  
> [!NOTE]
>  Si la source de l’original pour un **commande** est un flux de données spécifié par le [CommandStream propriété (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) propriété, en affectant une nouvelle chaîne à la **WillExecute** _Source_ paramètre modifie la source de la **commande**. Le **CommandStream** propriété est effacée et [CommandText propriété (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) propriété sera actualisée avec la nouvelle source. Le flux d’origine spécifié par **CommandStream** seront publiés et ne sont pas accessibles.  
  
 Si le dialecte de la nouvelle chaîne source diffère de la configuration d’origine de la [Dialect, propriété](../../../ado/reference/ado-api/dialect-property.md) propriété (qui correspondait à la **CommandStream**), le dialecte correct doit être spécifié en définissant le **dialecte** propriété de l’objet de commande référencé par *pCommand*.  
  
## <a name="see-also"></a>Voir aussi  
 [Exemple de modèle d’événements ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Résumé du Gestionnaire d’événements ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Connection, objet (ADO MD)](../../../ado/reference/ado-api/connection-object-ado.md)
