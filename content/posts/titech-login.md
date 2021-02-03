---
title: "大学ポータルに自動ログインしてみました(~Ruby編~)"
date: 2021-01-24T17:43:43+09:00
draft: false
images: ["/images/ruby-titech.png"]
tags: ["ruby"]
categories: ["program"]
---

こんにちは、ぬまです。
今回は僕の通う大学のポータルサイトのログインがとてつもなくめんどくさかったので、自動ログインスクリプトを作って自作コマンドにしちゃいました!!  
「大学　自動ログイン」などでぐぐるとそんなに記事がなく、Pythonが多い印象でした。Rubyで書いた記事があまり見当たらなかったので、せっかくならRubyで作ろうと言った動機です。  
### 問題点  
とてつもなくめんどくさいというのはどういうことか説明しましょう。  
以下がログインフォームです。以下のログインフォームはありふれたログインフォームなのでGoogelChromeなどに記憶させればログインは容易にできます。  
僕の大学はログインしたあとにマトリクス認証というのがあり、学生証の裏のマトリクスを見比べて該当する箇所を入力しなければなりません。これがめちゃくちゃめんどくさい！！毎回入力する番号変わるし学生証と見比べなければならないのは厄介です、、、セキュリティ面ではかなり強いと思いますが、、   
{{< figure src="/images/login1.png" class="center" width="400" >}}    
{{< figure src="/images/login2.png" class="center" width="400" >}}   

### 解決策  
そこで！！自動ログインしてしまおうということです。  
使うライブラリは「selenium-webdriver」というもので、ブラウザを直接操作するためのライブラリです。今回はChromeを操作するため、ChromeDriverを自分のChromeのバージョンと合わせてダウンロードしておく必要があります。  
[ここからダウンロードできます](https://chromedriver.chromium.org/downloads)  
ダウンロードできたらChromeDriverを使えるようにするため/usr/local/binに移動します。
```bash
mv ['解凍した場所'] /usr/local/bin
```  
次に、selenium-webdriver(ruby上で使う)をインストールします。
```bash
gem install selenium-driver
```  
プログラムを説明します。  
以下でchromeを開いてURL先へ移動
```ruby
driver = Selenium::WebDriver.for :chrome, options: options
driver.get LOGIN_URL
```
移動先でページの要素を取得して入力したりクリックしたりすることができるので、実際のコードをもとに説明します。
```ruby
driver.find_element(:xpath, '//*[@id="portal-form"]/form[2]/input').click  # pathから要素を取得し、クリックする

input_pass1 = driver.find_element(:name, 'message3') # nameから要素取得
input_pass1.send_keys login_info.matrix[el_pass1[1]][0][el_pass1[3].to_i] # 取得した要素にデータを入力
```  
これらの内容はChromeの開発者ツールから要素を取得することができます。  
xpathの取得の際に特定の要素の取得に困ったので、デペロッパーツールを使うとこんな感じで綺麗にxpathをコピーできます。
{{< figure src="/images/developer-xpath.png" class="center" width="700" >}}   

### パスワード情報について  
loginInfoクラスにパスワード情報は持たせるようにしています。
```ruby
class LoginInfo
  attr_accessor :username, :password, :matrix
  
  def initialize
    @username = ''
    @password = ''
    @matrix = {
      'A' =>
        [1 => "", 2 => "", 3 => "", 4 => "", 5 => "", 6 => "", 7 => ""],
      'B' =>
        [1 => "", 2 => "", 3 => "", 4 => "", 5 => "", 6 => "", 7 => ""],
      'C' =>
        [1 => "", 2 => "", 3 => "", 4 => "", 5 => "", 6 => "", 7 => ""],
      'D' =>
        [1 => "", 2 => "", 3 => "", 4 => "", 5 => "", 6 => "", 7 => ""],
      'E' =>
        [1 => "", 2 => "", 3 => "", 4 => "", 5 => "", 6 => "", 7 => ""],
      'F' =>
        [1 => "", 2 => "", 3 => "", 4 => "", 5 => "", 6 => "", 7 => ""],
      'G' =>
        [1 => "", 2 => "", 3 => "", 4 => "", 5 => "", 6 => "", 7 => ""],
      'H' =>
        [1 => "", 2 => "", 3 => "", 4 => "", 5 => "", 6 => "", 7 => ""],
      'I' =>
        [1 => "", 2 => "", 3 => "", 4 => "", 5 => "", 6 => "", 7 => ""],
      'J' =>
        [1 => "", 2 => "", 3 => "", 4 => "", 5 => "", 6 => "", 7 => ""],
    }
  end
end

```

### プログラム  
以下がメインのプログラムになります。  
```ruby
require 'selenium-webdriver'
require File.dirname(__FILE__) + '/loginInfo'

class TitechWeb
  LOGIN_URL = "https://portal.titech.ac.jp/"
  
  def login
    begin
      args = ['disable-infobars']
      options = Selenium::WebDriver::Chrome::Options.new(args: args)
      driver = Selenium::WebDriver.for :chrome, options: options
      driver.get LOGIN_URL
      login_info = LoginInfo.new()

      driver.find_element(:xpath, '//*[@id="portal-form"]/form[2]/input').click
      sleep 1

      driver.find_element(:name, 'usr_name').send_keys login_info.username
      driver.find_element(:name, 'usr_password').send_keys login_info.password
      driver.find_element(:name, 'OK').click

      sleep 2

      el_pass1 = driver.find_element(:xpath, '//*[@id="authentication"]/tbody/tr[4]/th[1]').text
      el_pass2 = driver.find_element(:xpath, '//*[@id="authentication"]/tbody/tr[5]/th[1]').text
      el_pass3 = driver.find_element(:xpath, '//*[@id="authentication"]/tbody/tr[6]/th[1]').text

      input_pass1 = driver.find_element(:name, 'message3')
      input_pass1.send_keys login_info.matrix[el_pass1[1]][0][el_pass1[3].to_i]

      input_pass2 = driver.find_element(:name, 'message4')
      input_pass2.send_keys login_info.matrix[el_pass2[1]][0][el_pass2[3].to_i]

      input_pass3 = driver.find_element(:name, 'message5')
      input_pass3.send_keys login_info.matrix[el_pass3[1]][0][el_pass3[3].to_i]

      sleep 2

      driver.find_element(:name, 'OK').click

    ensure
      gets 
      driver.quit()
    end
  end
end

if __FILE__ == $0
  titech = TitechWeb.new()
  titech.login()
end

```  
これで少なくともプログラムを実行すれば自動ログインは可能になりました。
### 自作コマンド化
ただし、いちいち実行するのはめんどくさいので、自作コマンドとしてコマンドを叩けばログインできるようにしたいと思います。やることは絶対パスでファイルを実行するシェルスクリプトを作り、そのスクリプトを実行できるようにパスを通すということです。  
コマンド名のスクリプトファイルを生成して中にプログラム実行するコマンドを入力します。以下のように。  
```bash
#!/bin/sh
ruby "['フォルダがが存在する絶対パス']/src/titechWeb.rb"
```
あとはこのスクリプトをどこでも実行できるようにします。
今回はsetup.shにまとめているので、中身を説明します。
```bash
#!/bin/sh
SCRIPT_DIR=$(cd $(dirname $0); pwd)
ln -si $SCRIPT_DIR"/titech" /usr/local/bin
chmod 777 $SCRIPT_DIR"/titech"
```  
ここでは、先ほど作ったスクリプトを/usr/local/binにシンボリックリンクを作成します。あとは/usr/local/binにあるスクリプトを実行可能にしました。  
これで自作コマンドtitechの完成です。  

では、今回はこの辺で！

ソースは[こちら](https://github.com/tomoyuki-hiranuma/titech-login)になります。
