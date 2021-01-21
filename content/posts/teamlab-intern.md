---
title: "チームラボインターンに参加してきました"
date: 2021-01-06T00:07:41+09:00
draft: false
images: ["/images/teamlab.png"]
---

こんにちは、ぬまです。  
今回は11月と12月にわたってチームラボ株式会社でインターン生として業務に参加しました。  
もともと業務での経験がゼロだったためだいぶ貴重な経験をさせていただいたので、参加記録を残したいと思います。極秘事項が多いため、詳しいことは残せないが残念です。  
{{< figure src="/images/teamlab.png" class="center" width="300" >}}  
## インターン概要
日程：11月26日~12月23日  
配属：ECサイトの案件  
技術：Ruby on Rails, MySQL, Redis, Docker, AWS(ECS, ECR, CodePipeline)  
## 応募背景
サマーインターンを通してある程度ハッカソンの開発経験を積んできましたが、業務経験がないので就業型に参加したい！つよつよエンジニアからレビューをもらいたい！！という思いがありました。あと、Rails書きたい！！ある日、Paiza経由でのスカウトをいただき、カジュアル面談という名の面接を申し込みました。(面接官がのちのメンバーでした)  
応募理由や技術的な質問などをざっくばらんに話をして楽しく終わり、受かっても落ちてもチームラボ良さそうだなという印象を持った記憶があります。後日、プログラミング試験を受け、採用をいただきました。  
## そもそもチームラボ株式会社とは？
HPから引用させていただくと  
>**TECHNOLOGY×CREATIVE**  
>テクノロジーとクリエイティブの境界はすでに曖昧になりつつあり、今後のこの傾向はさらに加速していくでしょう。そんな情報社会において、サイエンス・テクノロジー・デザイン・アートなどの境界を曖昧にしながら、『実験と革新』をテーマにものを創ることによって、もしくは、創るプロセスを通して、ものごとのソリューションを提供します。  

詳しくは[HP](https://www.team-lab.com/)見てみてください。かわいいです。  
職種はテクノロジー、クリエイティブ、カタリストに分かれており、ざっくりいうと左からエンジニア、デザイナー、マネージャーという認識です。  
僕は、テクノロジーの中のパッケージチーム、いわゆるWebエンジニアのチームの中のECチームに配属されました。  
## やったこと
参画した最初はi18nというgemの導入によりエラー文が英語表記になっていたためymlファイルをいじって日本語に直すような比較的簡単なタスクをこなす中で、アプリ全体をなんとなく理解していきました。その後はECサイトなため、さまざまなバリデーションやエラーハンドリングを実装しました。
## 初めての経験
・核となるアプリを拡張することで大きなECサイトを構築するという経験は今までしたことがなく、個人で実現できるわけでもなくかなり貴重な経験でした。その中で、モデル、コントローラ、ビューをそれぞれオーバーライドすることでアプリが完成していくのはなかなかに面白かったです。  
・state_machineをつかった状態の管理。state_machineというgemを使うことでECサイトの各状態の遷移をみてバリデーションをかけたり、ある状態に移り変わる時になにかしたり、ある状態から移り変わる時になにかしたりと、融通が効くのでかなり面白かったです。  
・ファイルインポート時のエラーメッセージをエラーの数だけ表示させる。エラーが起きた時にraiseすると処理が終わってしまうので、うまくエラー処理するのが難しかった印象があります。  
・隣にメンターさんがいてくれたため、困った時に空いていればすぐに聞ける環境は初めてでかなりありがたく理解が数倍捗りました。  
・そもそも業務に参画すること自体初めてでした。  
・自分が書いたコードを実際のエンジニアの方にレビューを受け、それが実際のサービスの一部になる感覚。楽しすぎました。  
・詰まった時に業務時間内に勉強できることは、飲食店や塾講師のアルバイトにはできない機会だと感じます。  
## ご飯（ここ重要←）
インターン期間中に連れてっていただいたご飯で特においしかったお店を紹介します。  
・ポンチ軒:さくさくで口の中でお肉がとろけました。基本的に行列でたまたま一度だけいけました。
{{< figure src="/images/ponchi.png" class="center" width="350" >}}  

・つじ田:痺れの中のからさがあり、坦々麺うまい  
{{< figure src="/images/tsujita.png" class="center" width="350" >}}  

・一頭:お肉がうまうまで２回もいってしまいました。(ポンチ軒に行こうとしたら行列だったので。。)メンターさん曰く、トングの先が細い焼肉店はおいしいらしい(？)  
{{< figure src="/images/itto.png" class="center" width="350" >}}  


## 感想
実務での開発がどういう物なのか正直想像もついていない状態で参加させていただいて、実際の一人での開発と大きく違うこととして、自分以外のエンジニアが僕のコードを読むことだったり、仕様を理解することであったり、メンバー同士で話し合う環境があったり、人と関わる点で大きく違うなと実感しました。  
また、**チーム**ラボでは**チーム**の仲が良く、Slackで業務と全然関係ない話で盛り上がったりミーティングでも楽しくお話しする時間があったり、開発する上での**チーム**力がものすごく高かった印象です。  
コロナ禍にもかかわらず、オンラインオフライン兼用でインターンシップに参加させていただきありがとうございました。コロナ禍で不安はあったものの、毎朝全フロアを消毒を徹底しており、扉の前にマスクが常備してあるので、外出て戻ったらマスクを変える制度ができており、社員さんのみでなくインターン生に対する受け入れ体制も充実していた印象です。このような状況下でも受け入れてくださりありがとうございました。  
{{< figure src="/images/teamlab2.png" class="center" width="400" >}}  
↑これはオフィス6階の共用スペースで外部の人とのミーティングなどはここで行われています。めちゃくちゃかわいいです。ぜひ一度足を運んでみてください。  
では〜  