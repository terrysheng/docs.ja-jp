---
title: "デスクトップ アプリケーションでのリソースのパッケージ化と配置 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "配置 (アプリケーションを) [.NET Framework]、リソース"
  - "リソース ファイル、配置"
  - "ハブ アンド スポーク リソース配置モデル"
  - "リソース ファイル、パッケージ化"
  - "アプリケーション リソース、パッケージ化"
  - "単一リソース アセンブリ"
  - "サテライト アセンブリ"
  - "既定のカルチャ (アプリケーションの)"
  - "名前 [.NET Framework]、リソース"
  - "フォールバック プロセス (リソースの)"
  - "グループ化 (カルチャの)"
  - "アプリケーション リソース、配置"
  - "アプリケーション リソース、名前付け規則"
  - "カルチャ、パッケージ化と配置 (リソースの)"
  - "リソース ファイル、名前付け規則"
  - "パッケージ化 (アプリケーション リソースの)"
  - "アプリケーション リソース、フォールバック プロセス"
  - "リソース ファイル、フォールバック プロセス"
  - "ローカライズ (リソースを)"
  - "ニュートラル カルチャ"
ms.assetid: b224d7c0-35f8-4e82-a705-dd76795e8d16
caps.latest.revision: 26
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 26
---
# デスクトップ アプリケーションでのリソースのパッケージ化と配置
アプリケーションがローカライズされたリソースを取得するに <xref:System.Resources.ResourceManager> クラスによって表される .NET Framework リソース マネージャーに依存します。  リソース マネージャーは、リソースのパッケージ化と配置にハブ アンド スポーク モデルを使用していることを前提としています。  ハブは、ローカライズできない実行可能コードと、ニュートラルまたは既定のカルチャと呼ばれる単一のカルチャのリソースを含むメイン アセンブリです。  既定のカルチャは、アプリケーションで使用されるフォールバック カルチャです; ローカライズされたリソースが見つからない場合は、リソースを使用するのはカルチャです。  各スポークは、単一のカルチャ用のリソースを含むが、コードはまったく含まないサテライト アセンブリにつながります。  
  
 このモデルにはいくつかのメリットがあります。  
  
-   アプリケーションを配置した後で、新しいカルチャ用のリソースを徐々に追加していくことができます。  アプリケーションの開発後に、カルチャ固有のリソースを開発するために長時間を要する場合があります。このモデルを使用すると、まずメイン アプリケーションをリリースし、後日にカルチャ固有のリソースをリリースできます。  
  
-   アプリケーションのサテライト アセンブリを更新または変更するときに、アプリケーションを再コンパイルしなくても済みます。  
  
-   アプリケーションは、特定のカルチャに必要なリソースを含むサテライト アセンブリだけを読み込みます。  このため、システム リソースの使用率を大幅に下げることができます。  
  
 ただし、このモデルにはデメリットもあります。  
  
-   複数のリソース セットを管理する必要があります。  
  
-   複数の構成をテストする必要があるので、アプリケーションのテストにかかる初期費用が増大します。  しかし、長い期間で捉えると、複数の国際バージョンを平行してテストおよび保守するよりも、複数のサテライトを持つ 1 つのコア アプリケーションをテストする方が簡単で負荷もかかりません。  
  
## リソースの名前付け規則  
 アプリケーションのリソースをパッケージ化するときには、共通言語ランタイムが要求するリソースの名前付け規則を使用して、各リソースに名前を付ける必要があります。  ランタイムはカルチャ名でリソースを識別します。  各カルチャは、言語と関連付けられた 2 文字の小文字のカルチャ名と、組み合わせやには一意の名前、国に関連付けられた 2 文字の大文字のサブカルチャ、の名前または空白を必要に応じて設定されます。  サブカルチャ名がある場合は、カルチャ名の後ろにダッシュ \(\-\) で区切って続けます。  例では、日本語、米国、ドイツ語の de\-AT ドイツで、オーストリアで話されるで話されるドイツ語にの de\-DE で話される英語にの en\-US で話されるに日本語の ja\-JP が含まれます。  カルチャ名の [各国語サポート \(NLS\) のリファレンス](http://go.microsoft.com/fwlink/?LinkId=200048) 一覧については、Go Global Developer Center で参照してください。  
  
> [!NOTE]
>  リソース ファイルの作成方法の詳細については、MSDN ライブラリの [リソース ファイルの作成](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md) と [サテライト アセンブリの作成](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md) を参照してください。  
  
<a name="cpconpackagingdeployingresourcesanchor1"></a>   
## リソース フォールバック プロセス  
 リソースをパッケージ化および配置するためのハブ アンド スポーク モデルは、代替プロセスを使用して適切なリソースを検索します。  アプリケーションが利用できないローカライズされたリソースを要求した場合、共通言語ランタイムによって、ユーザーの要求に一致する検索し、最終的な解決策としては例外をスローします、適切なフォールバック カルチャのリソースを階層を示します。  階層の各レベルにおいて、適切なリソースが見つかった場合、ランタイムはそのリソースを使用します。  リソースが見つからない場合、次のレベルへ移って検索が続行されます。  
  
 検索のパフォーマンスを向上させるには、<xref:System.Resources.NeutralResourcesLanguageAttribute> 属性をメイン アセンブリに適用して、メイン アセンブリで使用するニュートラル言語の名前を渡します。  
  
> [!TIP]
>  ランタイムがリソース アセンブリのプローブ リソース フォールバック プロセスとプロセスを最適化するために [\<relativeBindForResources\>](../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md) 構成要素を使用する方法があります。  詳細については、[リソース フォールバック プロセスを最適化する](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md#Optimizing) セクションを参照します。  
  
 リソース フォールバック プロセスは、次の手順があります。:  
  
1.  実行時の 1 番目のアプリケーションの要求されたカルチャと一致するアセンブリに [グローバル アセンブリ キャッシュ](../../../docs/framework/app-domains/gac.md) を確認します。  
  
     グローバル アセンブリ キャッシュには、多数のアプリケーションによって共有されるリソース アセンブリを格納できます。  このため、作成するすべてのアプリケーションのディレクトリ構造内に、特定のリソース セットを含める必要がなくなります。  アセンブリへの参照が検出されると、そのアセンブリの中に要求されたリソースがあるかどうかが検索されます。  要求されたリソースがアセンブリ内に見つかった場合、ランタイムはそのリソースを使用します。  リソースが見つからなかった場合、ランタイムは検索を続行します。  
  
2.  次に、ランタイム チェック、要求されたカルチャと一致するディレクトリの現在実行しているアセンブリのディレクトリ。  ディレクトリが見つかった場合、そのディレクトリの中に、要求されたカルチャ用の有効なサテライト アセンブリがあるかどうかが検索されます。  次に、見つかったサテライト アセンブリの中で、要求されたリソースが検索されます。  アセンブリ内でリソースが見つかった場合、ランタイムはそのリソースを使用します。  リソースが見つからなかった場合、ランタイムは検索を続行します。  
  
3.  次に、ランタイムはクエリのサテライト アセンブリがオンデマンドでインストールされるかどうかを判定する Windows インストーラー。  その場合は、インストールを処理し、アセンブリを読み込み、それ以降は、要求されたリソースを検索します。  アセンブリ内でリソースが見つかった場合、ランタイムはそのリソースを使用します。  リソースが見つからなかった場合、ランタイムは検索を続行します。  
  
4.  ランタイムは、サテライト アセンブリを見つけることができないことを示すために <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> イベントを発生させます。  イベントを処理することを選択した場合、イベント ハンドラーはリソースの参照に使用するサテライト アセンブリへの参照を返すことができます。  それ以外の場合、イベント ハンドラーは `null` を返し、検索を示します。  
  
5.  次に、ランタイムはもう一度グローバル アセンブリ キャッシュを検索します、要求されたカルチャの親アセンブリを示します。  グローバル アセンブリ キャッシュ内に親アセンブリが存在する場合、ランタイムはそのアセンブリの中で、要求されたリソースを検索します。  
  
     親カルチャは、適切なフォールバック カルチャとして定義されます。  リソースを用意することが例外をスローすることで目的のため、フォールバック候補として親を検討してください。  このプロセスを使用して、リソースを再利用することもできます。  子のカルチャが要求されたリソースをローカライズする必要がない場合は、親のレベルだけに特定のリソースが含まれている必要があります。  たとえば、en \(ニュートラル英語\)、en\-GB \(英国で話される英語\)、および en\-US \(米国で話される英語\) 用のサテライト アセンブリを作成する場合、サテライト、共通用語が含まれ、en\-GB および en\-US サテライトは、それらの用語にのみオーバーライドを提供します。  
  
6.  ランタイムは次に、現在実行されているアセンブリのディレクトリの中に、親ディレクトリが含まれるかどうかをチェックします。  親ディレクトリが存在する場合、そのディレクトリの中で、親カルチャ用の有効なサテライト アセンブリが検索されます。  アセンブリが見つかった場合、そのアセンブリの中で要求されたリソースが検索されます。  リソースが見つかった場合、ランタイムはそのリソースを使用します。  リソースが見つからなかった場合、ランタイムは検索を続行します。  
  
7.  次に、ランタイムはクエリの親サテライト アセンブリがオンデマンドでインストールされるかどうかを判定する Windows インストーラー。  その場合は、インストールを処理し、アセンブリを読み込み、それ以降は、要求されたリソースを検索します。  アセンブリ内でリソースが見つかった場合、ランタイムはそのリソースを使用します。  リソースが見つからなかった場合、ランタイムは検索を続行します。  
  
8.  ランタイムは適切なフォールバック リソースを見つけることができないことを示すために <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> イベントを発生させます。  イベントを処理することを選択した場合、イベント ハンドラーはリソースの参照に使用するサテライト アセンブリへの参照を返すことができます。  それ以外の場合、イベント ハンドラーは `null` を返し、検索を示します。  
  
9. 次に、ランタイムの検索は多くの潜在的なレベルで前の手順 3 のようにアセンブリを、表示されます。  各カルチャに <xref:System.Globalization.CultureInfo.Parent%2A?displayProperty=fullName> のプロパティによって定義されている、親が独自の親があります。1 回の親は一つだけです。  親カルチャの検索は、カルチャの <xref:System.Globalization.CultureInfo.Parent%2A> のプロパティが <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>を返すと停止します; リソース フォールバックの場合、インバリアント カルチャはリソースを使用するために、カルチャまたは親カルチャとは見なされません。  
  
10. もともと指定されたカルチャとそのすべての親を検索してもリソースが見つからない場合は、既定 \(フォールバック\) カルチャ用のリソースが使用されます。  通常、既定のカルチャのリソースは、メイン アプリケーション アセンブリに含まれています。  ただし、<xref:System.Resources.NeutralResourcesLanguageAttribute> 属性の <xref:System.Resources.NeutralResourcesLanguageAttribute.Location%2A> のプロパティには、リソースの最終フォールバック位置のサテライト アセンブリであるメイン アセンブリではなくことを示すために <xref:System.Resources.UltimateResourceFallbackLocation> の値を指定できます。  
  
    > [!NOTE]
    >  既定のリソースは、メイン アセンブリとともにコンパイルできる唯一のリソースです。  <xref:System.Resources.NeutralResourcesLanguageAttribute> 属性を使用してサテライト アセンブリを指定しない限り、最終フォールバック \(最終的な親\) です。  したがって、メイン アセンブリに既定のリソース セットを常に組み込むことをお勧めします。  これにより、例外がスローされることを防止できます。  既定のリソース ファイルを含めておくことにより、すべてのリソース用のフォールバック リソースを用意して、カルチャに固有のリソースではなくても、少なくとも 1 つは利用できるリソースが確実に存在するようにしておくことができます。  
  
11. 最後に、ランタイムは、既定 \(フォールバック\) カルチャ用のリソースが見つからなかった場合、<xref:System.Resources.MissingManifestResourceException> または <xref:System.Resources.MissingSatelliteAssemblyException> 例外がリソースが見つからないことを示すためにスローされます。  
  
 たとえば、リソースがスペイン語 \(メキシコ\) 用に es\-MX \(カルチャ\) ローカライズしたアプリケーション要求とします。  ランタイムは、es\-MX に一致しますが、捜しましたりはアセンブリを最初にグローバル アセンブリ キャッシュを。  ランタイムは、es\-MX ディレクトリを実行しているアセンブリのディレクトリの現在検索します。  それが失敗すると、ランタイムは、適切なフォールバック カルチャを \(この場合は英語反映する親アセンブリをグローバル アセンブリ キャッシュを再度検索 \(スペイン語\)   親アセンブリが見つからなかった場合、ランタイムは es\-MX カルチャに対応するリソースが見つかるまで親アセンブリにあるすべてのレベルを検索します。  リソースが見つからなかった場合、ランタイムは既定のカルチャ用のリソースが使用されます。  
  
<a name="Optimizing"></a>   
### リソース フォールバック プロセスを最適化する  
 次の状況では、ランタイムはサテライト アセンブリのリソースを検索するプロセスを最適化する  
  
-   サテライト アセンブリは、コード アセンブリと同じ場所に配置されます。  コードのアセンブリが [グローバル アセンブリ キャッシュ](../../../docs/framework/app-domains/gac.md)にインストールされている場合、サテライト アセンブリは、グローバル アセンブリ キャッシュにインストールされます。  コードのアセンブリがディレクトリにインストールされている場合、サテライト アセンブリは、ディレクトリのカルチャ固有のフォルダーにインストールされます。  
  
-   サテライト アセンブリは、オンデマンド インストールされていません。  
  
-   アプリケーション コードは <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> イベントを処理しません。  
  
 [\<relativeBindForResources\>](../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md) 要素を追加し、次の例に示すように、アプリケーションの構成ファイルで `true` へ `enabled` 属性を設定することによって、サテライト アセンブリのプローブを最適化します。  
  
```  
  
<configuration>  
   <runtime>  
      <relativeBindForResources enabled="true" />  
   </runtime>  
</configuration>  
  
```  
  
 サテライト アセンブリの最適化されたプローブが選択機能です。  つまり、ランタイムは [\<relativeBindForResources\>](../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md) 要素は、アプリケーションの構成ファイルで、`enabled` 属性が `true`に設定されている場合 [リソース フォールバック プロセス](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md#cpconpackagingdeployingresourcesanchor1) に記載されている手順に従います。  この場合、サテライト アセンブリのプローブのプロセスは、次のように変更します。:  
  
-   ランタイムでは、サテライト アセンブリのプローブに親コード アセンブリの場所が使用されます。  親アセンブリがグローバル アセンブリ キャッシュにインストールされている場合、ランタイムはキャッシュのアプリケーションのディレクトリにプローブします。  親アセンブリをアプリケーション ディレクトリにインストールされている場合、ランタイムは、アプリケーション ディレクトリに、グローバル アセンブリ キャッシュにプローブします。  
  
-   ランタイムでは、サテライト アセンブリのオンデマンド インストール用の Windows インストーラーを問い合わせません。  
  
-   特定のリソース アセンブリのプローブが失敗した場合、ランタイムは <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> イベントを発生させません。  
  
### サテライト アセンブリへの最終フォールバック  
 オプションでメイン アセンブリからリソースを削除し、ランタイムが特定のカルチャに対応するサテライト アセンブリから最終フォールバック リソースを読み込むように指定できます。  フォールバック プロセスを制御するには、<xref:System.Resources.NeutralResourcesLanguageAttribute.%23ctor%28System.String%2CSystem.Resources.UltimateResourceFallbackLocation%29?displayProperty=fullName> のコンストラクターを使用して、リソース マネージャーは、メイン アセンブリとサテライト アセンブリからフォールバック リソースを取得する必要があるかどうかを指定する <xref:System.Resources.UltimateResourceFallbackLocation> パラメーターの値を指定します。  
  
 次の例は、\(fr\) のフランス語の言語のサテライト アセンブリでアプリケーションのフォールバック リソースを格納するために <xref:System.Resources.NeutralResourcesLanguageAttribute> 属性を使用します。例に `Greeting`という名前の一つの文字列リソースを定義するには、2 とおりの、テキスト ベースのリソース ファイルがあります。  1 番目は、resources.fr.txt フランス語のリソースが含まれています。  
  
```  
Greeting=Bon jour!  
```  
  
 2 番目のリソース、ru.txt、ロシア語のリソースが含まれています。  
  
```  
Greeting=Добрый день  
```  
  
 これら二つのファイルを .resources ファイルにコマンド ラインから [リソース ファイル ジェネレーター \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) を実行することによってコンパイルされます。フランス語のリソースの場合は、次の操作:  
  
 **resgen.exe resources.fr.txt**  
  
 ロシア語リソースに対して、次の操作:  
  
 **resgen.exe resources.ru.txt**  
  
 .resources ファイル、ダイナミック リンク ライブラリにフランス語のリソースのコマンド ラインから [アセンブリ リンカー \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md) を実行すると、次のように埋め込まれます:  
  
 **al \/t:lib \/embed:resources.fr.resources \/culture:fr \/out:fr\\Example1.resources.dll**  
  
 とロシア語のリソースに対しては次のように:  
  
 **al \/t:lib \/embed:resources.ru.resources \/culture:ru \/out:ru\\Example1.resources.dll**  
  
 アプリケーションのソース・コードは Example1.cs または Example1.vb という名前のファイルにあります。  これは、既定のアプリケーション リソースを fr サブディレクトリにあることを示すために <xref:System.Resources.NeutralResourcesLanguageAttribute> 属性が含まれています。  このメソッドは、リソース マネージャーをインスタンス化し、`Greeting` リソースの値を取得し、コンソールに表示されます。  
  
 [!code-csharp[Conceptual.Resources.Packaging#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.packaging/cs/example1.cs#1)]
 [!code-vb[Conceptual.Resources.Packaging#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.packaging/vb/example1.vb#1)]  
  
 次のようにコマンド ラインから C\# ソース・コードをコンパイルする:  
  
 **csc Example1.cs**  
  
 Visual Basic コンパイラのコマンドはよく似ています:  
  
 **vbc Example1.vb**  
  
 メイン アセンブリに埋め込まれるリソースがないため `/resource` スイッチを使用してコンパイルする必要はありません。  
  
 言語がロシア語以外はであるシステムで例を実行すると、次の出力を表示する:  
  
```  
Bon jour!  
```  
  
## パッケージ化に関して提案される代替手段  
 期間または予算制約は、一連のアプリケーションがサポートするすべてのサブカルチャ用のリソースを作成しない場合もあります。  代わりに、すべての関連のサブカルチャが使用できる親カルチャ用に単一のサテライト アセンブリを作成できます。  たとえば、地域固有の英語のリソースを要求する、地域固有のドイツ語のリソースを要求するユーザーごとに一つの、サテライト アセンブリ German \(de\) をユーザーによって取得される単一の英語のサテライト アセンブリ \(en\-US\) を指定できます。  たとえば、ドイツのドイツ語 \(de\-DE\)、オーストリア \(de\-AT\)、およびスイス \(de\-CH\) で話されるドイツ語にの要求は、サテライト アセンブリ German \(de\) に戻ります。  したがって、既定のリソースは、最終フォールバックで、ほとんどのアプリケーション ユーザーから要求されるため、慎重に選択してこれらのリソースをリソース必要があります。  この方法はあまりカルチャに固有である配置しますが、アプリケーションのローカライズ費用をリソースを削減できます。  
  
## 参照  
 [デスクトップ アプリケーションのリソース](../../../docs/framework/resources/index.md)   
 [グローバル アセンブリ キャッシュ](../../../docs/framework/app-domains/gac.md)   
 [リソース ファイルの作成](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md)   
 [サテライト アセンブリの作成](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md)