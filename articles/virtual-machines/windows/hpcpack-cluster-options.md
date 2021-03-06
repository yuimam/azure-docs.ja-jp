---
title: Azure での Windows HPC Pack クラスター オプション | Microsoft Docs
description: Microsoft HPC Pack を使用して Azure クラウドで Windows ハイ パフォーマンス コンピューティング (HPC) クラスターを作成および管理するためのオプションについて学習します。
services: virtual-machines-windows,cloud-services,batch
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 10/26/2017
ms.author: danlep
ms.openlocfilehash: c5b8c16e076be3002425ceeac377043cea1a40a7
ms.sourcegitcommit: 5b2ac9e6d8539c11ab0891b686b8afa12441a8f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2018
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-cluster-for-windows-hpc-workloads-in-azure"></a>Azure で Windows HPC ワークロード用のクラスターを作成して管理するための HPC Pack のオプション
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

この記事では、Windows ワークロードの実行に使用する HPC Pack クラスターを作成するためのオプションについて説明します。 また、[Linux HPC ワークロード](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)を実行するのに使用する HPC Pack クラスターを作成するためのオプションもあります。


## <a name="hpc-pack-cluster-in-azure-vms-and-vm-scale-sets"></a>Azure VM と VM スケール セットの HPC Pack クラスター
### <a name="azure-templates"></a>Azure テンプレート
* (GitHub) [HPC Pack 2016 クラスター テンプレート](https://github.com/MsHpcPack/HPCPack2016)
* (GitHub) [HPC Pack 2012 R2 クラスター テンプレート](https://github.com/MsHpcPack/HPCPack2012R2)
* (Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (クイックスタート) [HPC クラスターを作成する](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (クイックスタート) [Create an HPC cluster with custom compute node image (カスタム コンピューティング ノード イメージを使用した HPC クラスターの作成)](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Azure VM イメージ
* [Windows Server 2016 上の HPC Pack 2016 ヘッド ノード](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [Windows Server 2016 上の HPC Pack 2016 コンピューティング ノード](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [Windows Server 2012 R2 上の HPC Pack 2016 ヘッド ノード](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [Windows Server 2012 R2 上の HPC Pack 2016 コンピューティング ノード](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [Windows Server 2012 R2 上の HPC Pack 2012 R2 ヘッド ノード](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [Windows Server 2012 R2 上の HPC Pack 2012 R2 コンピューティング ノード](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [Windows Server 2012 R2 上の HPC Pack コンピューティング ノードと Excel](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script-for-hpc-pack-2012-r2"></a>HPC Pack 2012 R2 の PowerShell デプロイメント スクリプト
* [HPC Pack IaaS デプロイ スクリプトを使用し、Windows VM でハイ パフォーマンス コンピューティング (HPC) クラスターを作成する](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>チュートリアル
* [チュートリアル: Azure に HPC Pack 2016 クラスターをデプロイする](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [チュートリアル: Azure の HPC Pack クラスターで Excel と SOA ワークロードを実行する](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-the-azure-portal"></a>Azure ポータルを使用した手動デプロイメント
* [Marketplace イメージを利用し、Azure VM で HPC Pack クラスターのヘッド ノードを作成する](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>クラスターの管理
* [Azure の HPC Pack クラスターのコンピューティング ノードの数と可用性を管理する](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [クラスターのワークロードに合わせて Azure の HPC Pack クラスター リソースを自動的に拡大縮小する](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [オンプレミス コンピューターから Azure にデプロイされた HPC Pack クラスターに HPC ジョブを送信する](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [HPC Pack でのジョブ管理](https://technet.microsoft.com/library/jj899585.aspx)
* [Azure Active Directory を使用して Azure の HPC Pack 2016 クラスターを管理する](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="burst-with-worker-role-nodes"></a>worker ロール ノードでのバースト 
* [HPC Pack を使用した Azure ワーカー インスタンスへのバースト](https://technet.microsoft.com/library/gg481749.aspx)
* [Azure で HPC Pack を使用してハイブリッド クラスターをセットアップする](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Azure での HPC Pack クラスターへのオンデマンドの "バースト" ノードの追加](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="burst-with-azure-batch"></a>Azure Batch でのバースト
* [HPC Pack を使用した Azure Batch へのバースト](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="rdma-clusters-for-mpi-workloads"></a>MPI ワークロードのための RDMA のクラスター
* [HPC Pack を使用して Windows RDMA クラスターをセットアップして MPI アプリケーションを実行する](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

