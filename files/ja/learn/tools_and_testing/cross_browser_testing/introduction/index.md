---
title: はじめてのブラウザー横断テスト
slug: Learn/Tools_and_testing/Cross_browser_testing/Introduction
l10n:
  sourceCommit: bb026bcb88b7f45374d602301b7b0db5a49ff303
---

{{LearnSidebar}}{{NextMenu("Learn/Tools_and_testing/Cross_browser_testing/Testing_strategies", "Learn/Tools_and_testing/Cross_browser_testing")}}

この記事では、ブラウザー横断テストの概要について、ブラウザー横断テストとは何か、よくある問題、デバッグ/トラブルシューティングのための手法などを説明します。

<table>
  <tbody>
    <tr>
      <th scope="row">前提知識:</th>
      <td>
        <a href="/ja/docs/Learn/HTML">HTML</a>,
        <a href="/ja/docs/Learn/CSS">CSS</a>,
        <a href="/ja/docs/Learn/JavaScript">JavaScript</a> 言語の基本を理解していること。
      </td>
    </tr>
    <tr>
      <th scope="row">目的:</th>
      <td>
        ブラウザー横断テストに関わるハイレベルな概念を理解すること。
      </td>
    </tr>
  </tbody>
</table>

## ブラウザー横断テストとは？

ブラウザー横断テストとは、ウェブサイトがさまざまなブラウザーや端末で確実に動作することを確実にするためのテストです。ウェブ開発者は、次のようなことを考慮する必要があります。

- 最新の JS/CSS 機能をすべては対応していない、少し古いブラウザーも含めた、さまざまなブラウザー。
- デスクトップやノートパソコン、タブレットやスマートフォン、スマートテレビなど、さまざまなハードウェア能力を持つ端末。
- スクリーンリーダーなどの支援技術に頼っていたり、キーボードしか使用していないような障碍を持っている人。

サイトが MacBook Pro やハイエンドの Galaxy Nexus で動作したからといって、すべてのユーザーにとってうまく動作するとは限らないのです。

> **メモ:** [Make the web work for everyone](https://hacks.mozilla.org/2016/07/make-the-web-work-for-everyone/) では、人々が使っているさまざまなブラウザーの種類やそれぞれのマーケットシェア、それに伴うブラウザー間の懸念点などが説明されています。

ウェブサイトは、さまざまなブラウザーや端末、障碍を持った人々にとって利用可能なものでなければなりません（例：スクリーンリーダーに対応）。コア機能が何らかの形で利用可能であれば、サイトはすべてのブラウザーや端末でまったく同じ使い勝手を提供する必要はありません。例えば、現行のブラウザーではアニメーションや 3D、光沢のあるものを表現することができるかもしれませんが、古いブラウザーでは同じ情報を平坦なグラフィックで表示させるだけかもしれません。

また、ウェブサイトがすべてのブラウザーや端末で動作することは不可能に近いので、ウェブ開発者は、コードが動作するブラウザーや端末の範囲についてサイトオーナーと合意する必要があります。

## ブラウザー間の問題が発生するのはなぜか

ブラウザー間の問題が発生する理由はさまざまありますが、ここではブラウザー/端末/推奨する環境設定の違いで動作が異なる場合の課題について話していることに注意してください。ブラウザー間の問題に取り組む前に、ソース中のバグを解決するべきです（必要に応じて前述の [HTML のデバッグ](/ja/docs/Learn/HTML/Introduction_to_HTML/Debugging_HTML)、[CSS のデバッグ](/ja/docs/Learn/CSS/Building_blocks/Debugging_CSS)、[何が間違っている? JavaScript のトラブルシューティング](/ja/docs/Learn/JavaScript/First_steps/What_went_wrong)の記事を見て記憶を呼び覚ましてください）。

ブラウザー間の問題が発生する原因は主に以下になります。

- ブラウザーにはバグがあったり、機能の実装が異なっていたりすることがあります。 1990 年代に IE4 と Netscape4 が覇権を争っていた頃、ブラウザー各社は競争優位に立とうと意図的にさまざまなことを実装し、開発者を地獄に陥れました。最近のブラウザーはだいぶ標準に従うようになっていますが、それでも時々、違いやバグが忍び込んできます。
- ブラウザーによっては、技術機能の対応レベルが他のブラウザーと異なることがあります。これは、ブラウザーの実装が始まったばかりの最先端の機能を扱っている場合や、新しい機能の開発が行われるずっと前に凍結された、開発が行われなくなった（つまり新しい作業が行われなくなった）非常に古いブラウザーに対応しなければならない場合に避けられないことです。例えば、あなたのサイトで最先端の JavaScript 機能を使用したい場合、古いブラウザーでは動作しないかもしれません。古いブラウザーに対応する必要がある場合、それらを使用しないか、必要に応じて何らかのクロスコンパイラーを使用して古い構文にコードを変換する必要があるかもしれません。
- 端末によっては、ウェブサイトの実行が遅くなったり、表示が崩れたりする制約が発生することがあります。例えば、デスクトップ PC できれいに見えるようにデザインされたサイトでも、モバイル端末では小さく見えたり読みにくくなったりするでしょう。また、大きなアニメーションをたくさん記載する場合、高スペックのタブレットでは問題なくても、低スペックの端末では動作が重くなったり、カクカクしたりする可能性があります。

上記の他にも理由はあります。

後述の記事では、ブラウザー間の問題についてよくある問題について掘り下げ、解決策を提示します。

## ブラウザー横断テストの作業手順

このようなブラウザー横断テストは、時間のかかる怖い作業に聞こえるかもしれませんが、その必要はありません。もし大規模なプロジェクトに取り組んでいるのであれば、定期的にテストを行い、対象とするユーザーにとって新しい機能が動作するかどうか、また、コードに新しく追加した部分が前回動作していた古い機能を壊していないかどうかを確認する必要があります。

テストをすべて自分のプロジェクトの終わりまで放置してしまうと、バグを発見して修正しながら進めるよりも、バグを修正するための費用と時間がかかってしまいます。

プロジェクトにおけるテストとバグ修正のワークフローは、おおよそ以下の 4 つのフェーズに分けることができます（これはとても大まかなもので、人によってこれとは全く異なることを行うかもしれません）。

**初期計画** > **開発** > **テスト/発見** > **修正/反復**

2-4 の段階は、実装をすべて取得するために必要な回数だけ繰り返される傾向があります。テストプロセスのさまざまな部分については、以降の記事でもっと詳しく見ていきますが、とりあえず、各段階で起こりうることをまとめておきましょう。

### 初期計画

最初の計画段階では、おそらくサイトの所有者/クライアント（あなたの上司、またはあなたがウェブサイトを構築している外部の会社の誰かかもしれません）と何度か計画会議を行い、ウェブサイトがどのようなものであるべきか、どのようなコンテンツや機能があるべきか、どのようなものであるべきかなどを正確に決定します。この点で、サイトを開発するためにどれくらいの時間があるのか、納期はどれくらいなのか、この作業に対していくら支払うつもりなのか、なども知っておきたいところです。これについてはあまり詳しく説明しませんが、ブラウザー間の問題はこのような計画に重大な効果をもたらすことがあります。

必要な機能設定と、その機能をどのような技術で構築するかというアイディアが得られたら、ターゲットオーディエンスの調査を始めるべきです。クライアントが前回行った調査、例えば自分自身で所有している他のウェブサイトや、あなたにとって今作業しているウェブサイトの以前のバージョンから、このことに関するデータを既に持っていることができるかもしれません。そうでない場合は、競合他社の利用状況や、サイトがサービスを提供する国の利用状況など、他にも見ていくことでよいアイディアが得られるでしょう。直観も役立つことがあります。

例えば、北米の顧客を対象とした e コマースサイトを構築するとします。このサイトは、ほとんどのデスクトップおよびモバイル（iOS、Android、Windows phone）ブラウザーの最後のいくつかのバージョンで完全に動作する必要があります。これには、 Chrome （および Chrome と同じレンダリングエンジンをベースにしているため Opera）、Firefox、Edge、Safari を含みます。
また、 WCAG AA に準拠したアクセシビリティが必要です。

これで対象とするテストプラットフォームがわかりましたので、必要な機能設定と使用する技術を確認しましょう。
例えば、 e コマースサイトのオーナーが、商品ページに WebGL を利用した各商品の 3D ツアーを組み込みたいと考えている場合、古いバージョンのブラウザーではそれだけでは動作しないことを受け入れる必要があります。

潜在的な問題のある部分のリストをコンパイルする必要があります。

> [!NOTE]
> 技術に関するブラウザーの対応情報は、MDN、すなわちあなたが今いるサイトでさまざまな機能を見ていくことで見つけることができます。また、 [caniuse.com](https://caniuse.com/) にも有益な情報があります。

これらの詳細について合意したら、サイトの開発を始めることができます。

### 開発

これでサイトを開発することになります。開発の様々な部分をモジュールに分割する必要があります。例えば、ホームページ、商品ページ、ショッピングカート、支払いワークフローなど、様々なサイトの領域を分割することができます。共通のヘッダーとフッターの実装、商品ページの詳細表示の実装、ショッピングカートウィジェットの維持などです。

例えば、ブラウザー横断開発には複数の一般的な戦略があります。

- 対象とするすべてのブラウザーで、すべての機能を可能な限り忠実に動作するようにします。これには、さまざまなブラウザーで異なる方法で機能を再現する異なるコードパスを書いたり、{{glossary("Polyfill", "ポリフィル")}}を使用して JavaScript や他の技術で不足している対応を模倣したり、単一のコードを書くことができ、ブラウザーの対応によってバックグラウンドで異なることを行うライブラリーを使用したりすることで改善されます。
- すべてのブラウザーで同じように動作するわけではないことを受け入れ、すべての機能に対応していないブラウザーでは、さまざまな（受け入れられる）解決策を提供しましょう。これは端末の制約上避けられないこともあります。映画館のワイドスクリーンは、あなたがサイトをどのようにプログラムしようとも、 4 インチのモバイル画面と同じ体験は得られません。
- サイトが一部の古いブラウザーでは動作しないことを受け入れ、先に進みましょう。あなたのクライアント/ユーザーベースがそれで OK であれば、これは OK です。

通常は、上記の 3 つの手法を組み合わせて開発することになるでしょう。最も重要なことは、コミットする前にそれぞれの小さな部分をテストすることです。すべてのテストを最後まで残さないでください。

### テスト/発見

それぞれの実装フェーズの後、新しい機能をテストする必要があります。手始めに、あなたのコードに、機能が動作しなくなるような一般的な課題がないことを確認する必要があります。

1. Firefox、Safari、Chrome、Edge など、システム上の安定したブラウザーでテストしてください。
2. 簡易的なアクセスビリティテストを行なってください。例えば、キーボードだけでサイトを使用してみたり、スクリーンリーダーを使用してサイトが操作可能かどうかを確認してください。
3. Android や iOS などのモバイルプラットフォームでテストしてください。

この時点で、新しいコードで見つけた問題を修正します。

次に、テスト対象ブラウザーのリストを対象オーディエンスのブラウザーリストいっぱいに広げてみて、ブラウザー間の問題を取り除くことに集中し始めるべきです（[対象ブラウザーの決定](/ja/docs/Learn/Tools_and_testing/Cross_browser_testing/Testing_strategies#テストするブラウザーと端末の選択)の詳細情報は次の記事を参照してください）。例えば次のようにします。

- できる限りすべての現行デスクトップ用ブラウザーで最新の変更をテストしてみてください。Firefox、Chrome、Opera、Edge、デスクトップ用の Safari（理想的には Mac、Windows、Linux）を含みます。
- 一般的な携帯電話やタブレットのブラウザー（iPhone/iPad の iOS Safari、iPhone/iPad/Androidの Chrome や Firefox など）でテストしてください。
- また、対象ブラウザーリストに記載されている他のブラウザーでもテストを行ってください。

最も簡易なオプションは、自分でできるテストをすべて行うことです（チームで作業する場合はチームメイトに手伝ってもらう）。可能な限り、実際の端末でテストするようにしてください。

物理的なハードウェア上ですべての異なるブラウザー、オペレーティングシステム、端末の組み合わせをテストする手段がない場合、エミュレーター（デスクトップコンピューター上のソフトウェアを使ってデバイスをエミュレートする）や仮想マシン（デスクトップコンピューター上で複数のオペレーティングシステムとソフトウェアの組み合わせをエミュレートできるソフトウェア）を使用することもできます。この方法は、特に状況によってはとても有益な選択肢です。例えば、 Windows では同じマシンに複数のバージョンの Windows を同時にインストールすることができないため、複数の仮想マシンを使用することが唯一の選択肢となる場合が多いのです。

もう1つのオプションは、ユーザーグループ、すなわちあなたのサイトをテストするために開発チーム以外の人々のグループを使用することです。これは、友人や家族のグループ、他の従業員のグループ、地元の大学のクラス、または有料でサイトをテストして結果を提供する、プロのユーザーテストのセットアップかもしれません。

最後に、監査ツールや自動化ツールを使用して、テストをよりスマートに行うことができます。これは、プロジェクトが大きくなるにつれて賢明な選択です。自分自身でテスト自動化システムを設定することができます（[Selenium](https://www.selenium.dev/) はよく使われるアプリです）。このシステムでは、例えば、さまざまなブラウザーでサイトを読み込んだりすることができます。

- ボタンをクリックすると何かが正常に動作するかどうかを確認し（例えば地図が表示されるなど）、テストが完了したら結果を表示します。
- それぞれの画面ショットを撮ることで、レイアウトがさまざまなブラウザーで一貫しているかどうかを確認できます。

テストにお金を投資したいのであれば、セットアップとテストの大部分を自動化してくれる商用ツールもあります（[Sauce Labs](https://saucelabs.com/) や [Browser Stack](https://www.browserstack.com/) など）。この種のツールは通常、継続的インテグレーションのワークフローを作成することができ、コードの変更をコードリポジトリーに送信する前に自動的にテストします。

#### リリース前のブラウザーでのテスト

プレリリース版のブラウザーでテストするのはよい考えであることが多いので、以下のリンクを参照してください。

- [Firefox Developer Edition](https://www.mozilla.org/ja/firefox/developer/)
- [Microsoft Edge Insider](https://www.microsoftedgeinsider.com/)
- [Safari Technology Preview](https://developer.apple.com/safari/technology-preview/)
- [Chrome Canary](https://www.google.com/chrome/canary/)
- [Opera Developer](https://www.opera.com/computer/beta)

これは、サイトでとても新しい技術を使用していて、最新の実装に対してテストしたい場合や、ブラウザー最新リリースバージョンでバグがあり、ブラウザー開発者が新しいバージョンでバグを修正したかどうかを確認したい場合に特に多く見られます。

### 修正/繰り返し

バグを発見したら、修正する必要があります。

最初のことは、バグが発生している箇所を可能な限り絞り込むことです。バグの報告者から、どのプラットフォーム、端末、ブラウザーのバージョンなど、できるだけ多くの情報を取得してください。似たような構成（たとえば、異なるデスクトッププラットフォーム上の同じブラウザーバージョンや、同じプラットフォーム上の同じブラウザーのいくつかの異なるバージョン）で試してみて、バグがどの程度広く維持されるかを確認してください。

それはあなたのせいではないかもしれません - ブラウザーにバグが存在する場合、ベンダーが迅速に修正することを期待します。既に修正されたかもしれません - 例えば Firefox リリース 49 にあるバグが Firefox Nightly (バージョン 52) では存在しなくなった場合、修正されたことになります。もし修正されていなければ、バグを報告することをお勧めします（下記の[バグを報告する](#バグを報告する)を参照）。

もしあなたの責任であれば、修正する必要があります。バグの原因を探すには、他のウェブ開発のバグと同じ戦略が必要です（再度、[HTML のデバッグ](/ja/docs/Learn/HTML/Introduction_to_HTML/Debugging_HTML)、[CSS のデバッグ](/ja/docs/Learn/CSS/Building_blocks/Debugging_CSS)、[何が間違っている? JavaScript のトラブルシューティング](/ja/docs/Learn/JavaScript/First_steps/What_went_wrong)を参照してください）。バグの原因がわかったら、それが問題を引き起こしている特定のブラウザーでそれを回避する方法を決める必要があります。問題のコードをそのまま変更するべきではありません、それが他のブラウザーでコードを壊してしまう可能性があるからです。一般的な手法は、何らかの方法でコードをフォークすることです。例えば、JavaScript 機能検出コードを使用して問題の機能が動作しない状況を検出し、動作する用途では別のコードを実行するようにします。

修正が完了したら、その修正が問題なく動作しているか、他の場所や 他のブラウザーでサイトが壊れる原因になっていないかを確認するために、テストプロセスを繰り返します。

## バグを報告する

ブラウザーでバグを発見した場合は、上記で述べたことを繰り返しますが、それらを報告する必要があります。

- [Firefox Bugzilla](https://bugzilla.mozilla.org/)
- [EdgeHTML issue tracker](https://developer.microsoft.com/en-us/microsoft-edge/)
- [Safari](https://bugs.webkit.org/)
- [Chrome](https://bugs.chromium.org/p/chromium/issues/list)
- [Opera](https://opera.atlassian.net/servicedesk/customer/portal/9)

## 要約

この記事では、ブラウザー横断テストに関して知っておくべき最も大事な概念について、高位の理解を与えてきました。この知識を備えたことで、ブラウザー横断テストの戦略について学び始める準備ができています。

{{NextMenu("Learn/Tools_and_testing/Cross_browser_testing/Testing_strategies", "Learn/Tools_and_testing/Cross_browser_testing")}}