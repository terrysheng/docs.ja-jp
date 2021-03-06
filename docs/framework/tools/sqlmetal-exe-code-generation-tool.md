---
title: "SqlMetal.exe (コード生成ツール) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "SQLMetal [LINQ to SQL]"
  - "コード生成ツール"
  - "SQLMetal.exe"
  - "LINQ to SQL, シリアル化"
  - "LINQ to SQL, DBML ファイル"
  - "LINQ to SQL, SQLMetal"
ms.assetid: 819e5a96-7646-4fdb-b14b-fe31221b0614
caps.latest.revision: 43
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 43
---
# SqlMetal.exe (コード生成ツール)
SqlMetal コマンド ライン ツールは、[!INCLUDE[vbtecdlinq](../../../includes/vbtecdlinq-md.md)] の [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] コンポーネント用のコードとマッピングを生成します。 このトピックで後述するオプションを適用することにより、次のようなアクションを SqlMetal で実行できます。  
  
-   データベースから、ソース コードとマッピング属性またはマッピング ファイルを生成する。  
  
-   データベースから、カスタマイズ用の中間的なデータベース マークアップ言語 \(.dbml\) ファイルを生成する。  
  
-   .dbml ファイルから、コードとマッピング属性またはマッピング ファイルを生成する。  
  
 このツールは、Visual Studio と共に自動的にインストールされます。 既定では、このファイルは `drive`:\\Program Files\\Microsoft SDKs\\Windows\\v`n.nn`\\bin にあります。 Visual Studio をインストールしない場合は、[Windows SDK](http://go.microsoft.com/fwlink/?LinkId=142225) をダウンロードすることによって SQLMetal ファイルを入手することもできます。  
  
> [!NOTE]
>  Visual Studio を使用している開発者は、[!INCLUDE[vs_ordesigner_long](../../../includes/vs-ordesigner-long-md.md)] を使ってエンティティ クラスを生成することもできます。 コマンド ライン方式は、大きなデータベースにも適切に対応できます。 SqlMetal はコマンド ライン ツールであるため、ビルド プロセスでこれを使用できます。  
  
 このツールを実行するには、開発者コマンド プロンプト \(または、Windows 7 の Visual Studio コマンド プロンプト\) を使用します。 詳細については、「[コマンド プロンプト](../../../docs/framework/tools/developer-command-prompt-for-vs.md)」を参照してください。コマンド プロンプトで、次のように入力します。  
  
## 構文  
  
```  
sqlmetal [options] [<input file>]  
```  
  
## オプション  
 最新のオプションの一覧を確認するには、コマンド プロンプトでインストール場所に移動し、「`sqlmetal /?`」と入力します。  
  
 **接続オプション**  
  
|オプション|説明|  
|-----------|--------|  
|**\/server:** *\<名前\>*|データベース サーバーの名前を指定します。|  
|**\/database:** *\<名前\>*|サーバー上のデータベース カタログを指定します。|  
|**\/user:** *\<名前\>*|ログオン ユーザー ID を指定します。 既定値は、Windows 認証を使用します。|  
|**\/password:** *\<パスワード\>*|ログオン パスワードを指定します。 既定値は、Windows 認証を使用します。|  
|**\/conn:** *\<connection string\>*|データベース接続文字列を指定します。**\/server**、**\/database**、**\/user**、または **\/password** オプションと共に使用することはできません。<br /><br /> 接続文字列にファイル名は含めないでください。 代わりに、コマンド ラインにファイル名を入力ファイルとして追加します。 たとえば、**sqlmetal \/code:"c:\\northwind.cs" \/language:csharp "c:\\northwnd.mdf"** というコマンド ラインは、入力ファイルとして "c:\\northwnd.mdf" を指定します。|  
|**\/timeout:** *\<秒\>*|SqlMetal がデータベースにアクセスする際のタイムアウト値を指定します。 既定値は 0 \(時間制限なし\) です。|  
  
 **抽出オプション**  
  
|オプション|説明|  
|-----------|--------|  
|**\/views**|データベース ビューを抽出します。|  
|**\/functions**|データベース関数を抽出します。|  
|**\/sprocs**|ストアド プロシージャを抽出します。|  
  
 **出力オプション**  
  
|オプション|説明|  
|-----------|--------|  
|**\/dbml** *\[:file\]*|出力を .dbml として送ります。**\/map** オプションと共に使用することはできません。|  
|**\/code** *\[:file\]*|出力をソース コードとして送ります。**\/dbml** オプションと共に使用することはできません。|  
|**\/map** *\[:file\]*|属性ではなく XML マッピング ファイルを生成します。**\/dbml** オプションと共に使用することはできません。|  
  
 **その他**  
  
|オプション|説明|  
|-----------|--------|  
|**\/language:** *\<language\>*|ソース コードの言語を指定します。<br /><br /> 有効な *\<language\>* は、vb と csharp です。<br /><br /> 既定値は、コード ファイル名の拡張子から派生します。|  
|**\/namespace:** *\<名前\>*|生成されるコードの名前空間を指定します。 既定値は、名前空間なしです。|  
|**\/context:** *\<type\>*|データ コンテキスト クラスの名前を指定します。 既定値は、データベース名から派生します。|  
|**\/entitybase:** *\<type\>*|生成されるコード内のエンティティ クラスの基本クラスを指定します。 既定値は、エンティティの基本クラスなしです。|  
|**\/pluralize**|クラスとメンバーの名前を自動的に複数化または単数化します。<br /><br /> このオプションは、米国英語バージョンでのみ使用できます。|  
|**\/serialization:** *\<option\>*|シリアル化可能なクラスを生成します。<br /><br /> 有効な *\<option\>* は、None と Unidirectional です。 既定値は None です。<br /><br /> 詳細については、「[Serialization](../../../docs/framework/data/adonet/sql/linq/serialization.md)」を参照してください。|  
  
 **入力ファイル**  
  
|オプション|説明|  
|-----------|--------|  
|**\<入力ファイル\>**|SQL Server Express .mdf ファイル、[!INCLUDE[ssEW](../../../includes/ssew-md.md)] .sdf ファイル、または .dbml 中間ファイルを指定します。|  
  
## 解説  
 SqlMetal の実際の機能には、次の 2 つの段階が含まれています。  
  
-   データベースのメタデータを .dbml ファイルに抽出する。  
  
-   コード出力ファイルを生成する。  
  
     適切なコマンド ライン オプションを使用することで、[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] または C\# ソース コードを生成するか、XML マッピング ファイルを生成できます。  
  
 メタデータを .mdf ファイルから抽出するには、他のすべてのオプションの後に .mdf ファイルの名前を指定する必要があります。  
  
 **\/server** を指定しない場合、**localhost\/sqlexpress** と見なされます。  
  
 次の条件が少なくとも 1 つ満たされる場合、[!INCLUDE[sqprsqext](../../../includes/sqprsqext-md.md)] は例外をスローします。  
  
-   自身を呼び出すストアド プロシージャを SqlMetal が抽出しようとした。  
  
-   ストアド プロシージャ、関数、またはビューの入れ子レベルが 32 を超える。  
  
     SqlMetal はこの例外をキャッチして、それを警告として報告します。  
  
 入力ファイル名を指定するには、その名前をコマンド ラインに入力ファイルとして追加します。 \(**\/conn** オプションを使用して\) 接続文字列にファイル名を含める操作は、サポートされていません。  
  
## 例  
 抽出された SQL メタデータを格納する .dbml ファイルを生成します。  
  
 **sqlmetal \/server:myserver \/database:northwind \/dbml:mymeta.dbml**  
  
 SQL Server Express を使用して .mdf ファイルから抽出された SQL メタデータを格納する .dbml ファイルを生成します。  
  
 **sqlmetal \/dbml:mymeta.dbml mydbfile.mdf**  
  
 SQL Server Express から抽出された SQL メタデータを格納する .dbml ファイルを生成します。  
  
 **sqlmetal \/server:.\\sqlexpress \/dbml:mymeta.dbml \/database:northwind**  
  
 .dbml メタデータ ファイルからソース コードを生成します。  
  
 **sqlmetal \/namespace:nwind \/code:nwind.cs \/language:csharp mymetal.dbml**  
  
 SQL メタデータからソース コードを直接生成します。  
  
 **sqlmetal \/server:myserver \/database:northwind \/namespace:nwind \/code:nwind.cs \/language:csharp**  
  
> [!NOTE]
>  サンプル データベース Northwind で **\/pluralize** オプションを使用する場合には、注意を必要とする動作があります。 SqlMetal がテーブルのために行型の名前を生成するとき、テーブル名は単数形です。 テーブルに関する <xref:System.Data.Linq.DataContext> プロパティを生成するときには、テーブル名は複数形です。 偶然にも、サンプル データベース Northwind 内のテーブルには既に複数形が使われています。 このため、この部分はうまく機能しません。 データベース テーブルの名前は単数形にするのが一般的ですが、.NET では、コレクションの名前を複数形にすることも一般的です。  
  
## 参照  
 [How to: Generate the Object Model in Visual Basic or C\#](../../../docs/framework/data/adonet/sql/linq/how-to-generate-the-object-model-in-visual-basic-or-csharp.md)   
 [Code Generation in LINQ to SQL](../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)   
 [External Mapping](../../../docs/framework/data/adonet/sql/linq/external-mapping.md)