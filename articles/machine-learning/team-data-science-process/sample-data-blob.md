---
title: Azure BLOB ストレージのデータをサンプリングする | Microsoft Docs
description: Azure BLOB ストレージのデータをサンプリングする
services: machine-learning,storage
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: 48cc74a8fdef0103f79033ac2484f658303f405c
ms.sourcegitcommit: ca05dd10784c0651da12c4d58fb9ad40fdcd9b10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="heading"></a>Azure BLOB ストレージのデータをサンプリングする
このドキュメントでは、Azure Blob Storage に格納されたデータのサンプリングについて説明します。プログラムからデータをダウンロードし、Python で記述されたプロシージャを使ってそのデータをサンプリングします。

次の**メニュー**は、さまざまなストレージ環境のデータをサンプリングする方法を説明するトピックにリンクしています。 

[!INCLUDE [cap-sample-data-selector](../../../includes/cap-sample-data-selector.md)]

**データをサンプリングする理由**
分析しようとしているデータセットが大規模な場合、データをダウンサンプリングして、小規模であっても典型的であり、管理しやすいサイズに減らすことが通常は推奨されます。 これにより、データの理解、探索、および特徴エンジニアリングが容易になります。 Cortana Analytics Process におけるダウンサンプリングの役割は、データ処理機能と機械学習モデルのプロトタイプをより迅速に作成できるようにすることです。

このサンプリング タスクは、 [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)の 1 ステップです。

## <a name="download-and-down-sample-data"></a>データのダウンロードとダウン サンプリング
1. 次の Python のサンプル コードから、BLOB サービスを使用して Azure BLOB ストレージからデータをダウンロードします。 
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))

2. 上記でダウンロードしたファイルから、Pandas データ フレームにデータを読み取ります。
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. 次のように、`numpy` の `random.choice` を使用してデータをダウンサンプリングします。
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

これで、上記の 1 パーセントのサンプルのデータ フレームを操作して、さらなる探索および特徴の生成を行えるようになりました。

## <a name="heading"></a>データをアップロードし、Azure Machine Learning で読み取る
次のサンプル コードを使用すると、次のようにデータをダウンサンプリングして、 Azure Machine Learning で直接使用できます。

1. データ フレームをローカル ファイルに書き込む
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. 次のサンプル コードを使用してローカル ファイルを Azure BLOB にアップロードする
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading to the blob:"+ BLOBNAME)

3. 次のスクリーン ショットに示すように、Azure Machine Learning の[データのインポート](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/)を使用して Azure BLOB からデータを読み取ります。

![リーダー BLOB](./media/sample-data-blob/reader_blob.png)

