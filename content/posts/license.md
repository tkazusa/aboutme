---
author: "Taketoshi Kazusa"
date: 2021-02-02
linktitle: 最近の OSS 界隈のライセンス問題について
menu:
  main:
    parent: tutorials
next: /tutorials/github-pages-blog
prev: /tutorials/automated-deployments
title: SSPL をきっかけに最近の OSS 界隈のライセンス問題について
weight: 10
---

Elastic 社の Elasticsearch 及び Kibana のライセンス変更に関連して、AWS が [Stepping up for a truly open source Elasticsearch](https://aws.amazon.com/jp/blogs/opensource/stepping-up-for-a-truly-open-source-elasticsearch/)で言及した、"What this means for the open source community" が気になったので少し調べてみた。

> The term “open source” has had a specific meaning since it was coined in 1998. Elastic’s assertions that the SSPL is “free and open” are misleading and wrong. They’re trying to claim the benefits of open source, while chipping away at the very definition of open source itself. Their choice of SSPL belies this. SSPL is a non-open source license designed to look like an open source license, blurring the lines between the two. As the Fedora community states, “consider the SSPL to be ‘Free’ or ‘Open Source’ causes shadow to be cast across all other licenses in the FOSS ecosystem.”


この引用中にある、SSPL とはどういうライセンスで、Elastic 社の主張はなんであり、何がオープンソースから逸脱してしまうのか。

### ここまでの経緯
**[2021/1/15 Doubling down on open, Part II](https://www.elastic.co/jp/blog/licensing-change)**
- Elastic 社が Elasticsearch 及び Kibana を Apache 2.0 ライセンスコードから、Server Side Public License (SSPL) と Elastic License のデュアルライセンスへ移行すると宣言
- Elastic 社の主張としては、 Elastic コミュニティや Elastic Cloud やセルフマネージド向けの Elastic ソフトウェアをご利用のお客様へは影響がないとしている

**[2020/1/20 License Change Clarification](https://www.elastic.co/jp/blog/license-change-clarification)**
- 今回の変更により、「Amazon Elasticsearch Serviceをはじめ、Elasticのプロダクトを入手し、サービスとして直接販売している事業者には影響があります。」としている
- SSLP は GPL に基づくライセンス、コピーレフトライセンスだが、OSI認可ライセンスではない
- Elastic Liccense はコピーレフトがない
  - BSL などを参考にシンプルにしていく可能性がある、BSL は Open Source Initiative が認めるオープンソースライセンスではないが、OSI創立者の Bruce Persens 氏が 2017 年に一定の評価
  - BSL を最新のソースコードに 3 年から 5 年くらいの期限付きで設定し、ALv2 へ置き換えるなどを検討

**[Amazon: NOT OK - why we had to change Elastic licensing](https://www.elastic.co/blog/why-license-change-AWS)** 
- Amazon Elasticsearch Service は商標違反ではないかと指摘
- 「Open Distro for Elasticsearch」を出した際に、商用コードを第三者がコピーして使われたと主張
  - そもそも [Open Distro for Elasticsearch を出した理由](https://aws.amazon.com/jp/blogs/opensource/keeping-open-source-open-open-distro-for-elasticsearch/)
    - Elasticservice のコードにオープンソースとプロプライエタリなコードが混在していて、うかつにビルドして使ってしまうと、ライセンス違反に抵触するかも。
    - AWSは「Open Distro for Elasticsearch」がフォークではなく、アップストリームにフィードバックし、オリジナルの最新バージョンに追随していくと表明し、オープンソースの流儀に沿っていると主張

この流れを踏まえて、AWS は冒頭の [Stepping up for a truly open source Elasticsearch](https://aws.amazon.com/jp/blogs/opensource/stepping-up-for-a-truly-open-source-elasticsearch/) を公開した。


### Server Side Public License とはなんなのか
[SSPLの問題点と主要Linuxディストリビューションから除外されるMongoDB](https://yudai.arielworks.com/memo/2019/01/31/182140)が非常に参考になった。もともと Elasticservice 及び Kibana において [ALv2](https://www.apache.org/licenses/LICENSE-2.0) で提供されていたものが、SSLP と Elastic Lisence で提供されるようになる。この SSLP は GPLv3 をベースにしているライセンスである。オープンソースプロジェクトが、そのソースコードを活用したクラウドベンダーがサービス提供をすると、開発者は報酬を得られない、コミュニティは十分貢献を得ないままである、という課題から提案されたライセンスである。[MongoDB はこれをオープンソースライセンスにあたると主張](https://www.mongodb.com/licensing/server-side-public-license/faq)するが、Open Source Definition(OSD) の9条に違反するため、オープンソースライセンスとは認証されることはなさそう、とのこと。実際に、Elasticsearvice の件がブログなどで宣言され始める 2021/1/19 に OSI から [The SSPL is Not an Open Source License](https://opensource.org/node/1099) と改めて声明が出ている。

> Fauxpen source licenses allow a user to view the source code but do not allow other highly important rights protected by the Open Source Definition, such as the right to make use of the program for any field of endeavor.

SSPL だと好きなところで使える、という権利を侵害するため、オープンソースの定義を満たさないと。余談だが、これ以降の文章でも、この変更によって、Apache ライセンスのもとで提供されていた時代に、オープンソースの流儀にしたがってプロジェクトが運営されると信じて貢献したエンジニアの時間とエネルギーが、プロプライエタリな製品に組み込まれることになっていることへの批判を割と強い口調で書かれている。

クラウドベンダーへ不満を持つオープンソースカンパニーはあるだろうし、各社がどういう意図でどのようなライセンスを選択し、それが OSS コミュニティへどう影響するかは見ていきたい。

### 参考
- [Open Source Initiative](https://opensource.org/)