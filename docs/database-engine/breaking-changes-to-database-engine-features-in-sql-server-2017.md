---
title: Changements importants dans les fonctionnalités du moteur de base de données de SQL Server 2017 | Microsoft Docs
description: Changements importants dans les fonctionnalités du moteur de base de données de SQL Server 2017
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.custom: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- breaking changes 2017 [SQL Server]
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 9b38a4358eb5ac7c0ab05ac7e2175c22011cea66
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52528953"
---
# <a name="breaking-changes-to-database-engine-features-in-includesssqlv14-mdincludessssqlv14-mdmd"></a>Changements importants dans les fonctionnalités du moteur de base de données de [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


  Cette rubrique décrit les changements importants apportés à [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]. Ces modifications peuvent interrompre les applications, scripts ou fonctionnalités fondés sur les versions antérieures de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Il se peut que vous rencontriez ces problèmes lors d'une mise à niveau.  
  
## <a name="breaking-changes-in-includesssqlv14-mdincludessssqlv14-mdmd-includessdeincludesssde-mdmd"></a>Modifications avec rupture dans [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-  CLR utilise la sécurité d’accès du code (CAS) dans le .NET Framework, qui n’est plus pris en charge comme limite de sécurité. À compter de [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)], une option de `sp_configure` appelée `clr strict security` est introduite pour améliorer la sécurité des assemblys CLR. clr strict security est activée par défaut, et traite les assemblys CLR `SAFE` et `EXTERNAL_ACCESS` comme s’ils étaient marqués `UNSAFE`. L’option `clr strict security` peut être désactivée pour assurer une compatibilité descendante, mais ceci n’est pas recommandé. Quand `clr strict security` est désactivée, un assembly CLR créé avec `PERMISSION_SET = SAFE` peut être en mesure d’accéder à des ressources système externes, d’appeler du code non managé et d’acquérir des privilèges **sysadmin**. Une fois la sécurité stricte activée, le chargement des assemblys qui ne sont pas signés échoue. En outre, si une base de données a des assemblys `SAFE` ou `EXTERNAL_ACCESS`, les instructions `RESTORE` ou `ATTACH DATABASE` peuvent être exécutées, mais le chargement des assemblys peut échouer.   
  Pour charger les assemblys, vous devez modifier, ou bien supprimer et recréer, chaque assembly, de façon à ce qu’il soit signé avec un certificat ou une clé asymétrique qui a une connexion correspondante avec l’autorisation `UNSAFE ASSEMBLY` sur le serveur. Pour plus d’informations, consultez [CLR strict security](../database-engine/configure-windows/clr-strict-security.md). 

## <a name="previous-versions"></a> Versions précédentes  

- [Changements essentiels dans les fonctionnalités du moteur de base de données de SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)

- [Changements essentiels dans les fonctionnalités du moteur de base de données de SQL Server 2014](https://docs.microsoft.com/sql/database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016?view=sql-server-2014#SQL14)

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>Documentation archivée pour les très anciennes versions de SQL Server

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a> Voir aussi  
 [Fonctionnalités du moteur de base de données dépréciées dans SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Fonctionnalités du moteur de base de données supprimées dans SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilité descendante du moteur de base de données SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Niveau de compatibilité ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
