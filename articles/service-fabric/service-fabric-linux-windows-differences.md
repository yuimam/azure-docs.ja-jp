---
title: "Linux と Windows での Azure Service Fabric の違い | Microsoft Docs"
description: "Linux での Azure Service Fabric と Windows での Azure Service Fabric の違いについて説明します。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/23/2018
ms.author: subramar
ms.openlocfilehash: 0a8dd9936268a4e4cb8b744a87111c3bbf3f062d
ms.sourcegitcommit: 782d5955e1bec50a17d9366a8e2bf583559dca9e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2018
---
# <a name="differences-between-service-fabric-on-linux-and-windows"></a>Linux での Service Fabric と Windows での Service Fabric の違い

Windows ではサポートされていても、Linux ではサポートされていない機能が一部存在します。 リリースごとに、この機能差は縮小され、最終的な機能は同一になります。 リリースされている最新バージョン (Windows ではバージョン 6.0、Linux ではバージョン 6.0) では、次の違いがあります。 

* すべてのプログラミング モデル (Java/C# Reliable Actors、Reliable Stateless Services および Reliable Stateful Services) はプレビュー段階にあります。
* Envoy (ReverseProxy) は、Linux 上のプレビュー段階にあります。
* Linux 用スタンドアロンのインストーラーは、まだ提供されていません。
* コンソールのリダイレクト (Linux または Windows の運用環境クラスターではサポートされていません)
* Linux 上の Fault Analysis Service (FAS)
* Service Fabric サービス (DNS サービスは Linux 上のコンテナーではサポートされています) 用の DNS サービス
* 特定の Powershell コマンドに相当する CLI コマンド (以下の一覧参照。大部分がスタンドアロン クラスターにのみ適用)

開発ツールも Windows と Linux で異なります。 Windows では Visual Studio、PowerShell、VSTS、ETW が使用され、Linux では Yeoman、Eclipse、Jenkins、LTTng が使用されます。

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a>Linux Service Fabric クラスターに対して実行できない PowerShell コマンドレット

* Invoke-ServiceFabricChaosTestScenario
* Invoke-ServiceFabricFailoverTestScenario
* Invoke-ServiceFabricPartitionDataLoss
* Invoke-ServiceFabricPartitionQuorumLoss
* Restart-ServiceFabricPartition
* Start-ServiceFabricNode
* Stop-ServiceFabricNode
* Get-ServiceFabricImageStoreContent
* Get-ServiceFabricChaosReport
* Get-ServiceFabricNodeTransitionProgress
* Get-ServiceFabricPartitionDataLossProgress
* Get-ServiceFabricPartitionQuorumLossProgress
* Get-ServiceFabricPartitionRestartProgress
* Get-ServiceFabricTestCommandStatusList
* Remove-ServiceFabricTestState
* Start-ServiceFabricChaos
* Start-ServiceFabricNodeTransition
* Start-ServiceFabricPartitionDataLoss
* Start-ServiceFabricPartitionQuorumLoss
* Start-ServiceFabricPartitionRestart
* Stop-ServiceFabricChaos
* Stop-ServiceFabricTestCommand
* Get-ServiceFabricNodeConfiguration
* Get-ServiceFabricClusterConfiguration
* Get-ServiceFabricClusterConfigurationUpgradeStatus
* Get-ServiceFabricPackageDebugParameters
* New-ServiceFabricPackageDebugParameter
* New-ServiceFabricPackageSharingPolicy
* Add-ServiceFabricNode
* Copy-ServiceFabricClusterPackage
* Get-ServiceFabricRuntimeSupportedVersion
* Get-ServiceFabricRuntimeUpgradeVersion
* New-ServiceFabricCluster
* New-ServiceFabricNodeConfiguration
* Remove-ServiceFabricCluster
* Remove-ServiceFabricClusterPackage
* Remove-ServiceFabricNodeConfiguration
* Test-ServiceFabricClusterManifest
* Test-ServiceFabricConfiguration
* Update-ServiceFabricNodeConfiguration
* Approve-ServiceFabricRepairTask
* Complete-ServiceFabricRepairTask
* Get-ServiceFabricRepairTask
* Invoke-ServiceFabricDecryptText
* Invoke-ServiceFabricEncryptSecret
* Invoke-ServiceFabricEncryptText
* Invoke-ServiceFabricInfrastructureCommand
* Invoke-ServiceFabricInfrastructureQuery
* Remove-ServiceFabricRepairTask
* Start-ServiceFabricRepairTask
* Stop-ServiceFabricRepairTask
* Update-ServiceFabricRepairTaskHealthPolicy



## <a name="next-steps"></a>次の手順
* [Linux で開発環境を準備する](service-fabric-get-started-linux.md)
* [OSX で開発環境を準備する](service-fabric-get-started-mac.md)
* [Yeoman を使用して Linux で最初の Service Fabric Java アプリケーションを作成してデプロイする](service-fabric-create-your-first-linux-application-with-java.md)
* [Eclipse 用の Service Fabric プラグインを使用して Linux で最初の Service Fabric Java アプリケーションを作成してデプロイする](service-fabric-get-started-eclipse.md)
* [Linux で最初の CSharp アプリケーションを作成する](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Service Fabric CLI を使用してアプリケーションを管理する](service-fabric-application-lifecycle-sfctl.md)
