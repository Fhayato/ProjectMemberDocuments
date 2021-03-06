# アクセス修飾子とカプセル化

## はじめに

課題については資料の説明部分は大幅な変更がかからないため講習時間より先に見て学習していただいて構いません。</br>
ただし、課題については直前に変更がかかる場合があるため、自己責任でお願いします。</br>
変数・関数・クラスなどで、指定のないものに関しては、各自適当な名前付けを行ってください。</br>
　(ExerciseX_X のような、書式が決まっているものは除く)</br>


## アクセス範囲/アクセス修飾子

全てのクラス、フィールド、メソッドにはアクセス範囲が定められており、各クラス、フィールド、メソッドの宣言の前に以下のようなキーワード(アクセス修飾子と呼ぶ)を記述することでアクセス範囲を指定することが出来る。

|修飾子                  |公開範囲                                  |
|:----------------------|:--------------------------------------:|
|public                 |全てのクラスから参照可能  　　　　　　　　　　　 |
|protected              |同一クラス/同一パッケージ/サブクラスのみ参照可能 |
|(なし/package private)  |同一クラス/同一パッケージのみ参照可能          |
|private                |同一クラスのみ参照可能                       |

理解し辛い学生は、とりあえず全てのフィールド/メソッドをprivateとして定義し、必要に応じてprotectedやpublicにすると良い。

```java
public class Television {
		private boolean power;	// Televisionクラスの中でのみアクセス可能
		private double volume;

		public Television(){		// 全てのクラスからアクセス可能
			this.power = false;	this.volume = 0.0;
    }	
		public void turnPower(){
			this.power = !this.power;
		}
}
```


## アクセサ(セッター, ゲッター)

どのクラスにおいても、全てのフィールドは基本的にprivateもしくはprotected修飾子が付加されているため、外部からアクセスすることが出来ない。</br>
そこで、外部からアクセスする必要があるフィールドにのみ、setter(セッター)、getter(ゲッター)というメソッドをpublicで定義する。</br>
セッターとゲッターをまとめてアクセサと呼ぶ。</br>
アクセサはメソッド名の命名に規則があり、それぞれ

```java
// int型のnumberはフィールドとして既に定義されているものとする
public void setNumber(int number){  this.number = number;  }
public int getNumber(){  return number;  }
```

と記述する。


## カプセル化

アクセス修飾子により外部からのアクセス範囲を制限し、アクセサにより利用してもらいたいフィールド/メソッドへのアクセスを提供することをカプセル化と呼ぶ。</br>
カプセル化はオブジェクト指向プログラミングにおける大きな要素の一つである。</br>
大きなプロジェクトにおいては、カプセル化により、利用してもらいたくないクラス/フィールド/メソッドへのアクセスを禁止することで人為的なバグを減らすことが出来る。</br>

現実的な例:
	テレビのチャンネルは直接ではなく、テレビに付属するチャンネル変更ボタンやリモコンのチャンネル変更ボタンにより変更してほしい。</br>

```java
television.channel = 2019;		// カプセル化されていないとこんなことも出来てしまう

// アクセサによりフィールドの値の取りうる範囲を制限
public void setChannel(int channel){
	this.channel = channel;
	if(channel < 0 || channel > 12) this.channel = 0;
}
```


## クラス図について

/*image*/

## 演習課題

### 課題1

* lecture02で作成したCarクラスのfuelをカプセル化し、外部クラスからの直接のアクセスを制限しなさい。(lecture03にコピーしてから変更を加えること)
* Carのインスタンスに給油ができるようにGasStationクラスとCarクラスを変更しなさい。(アクセサを用いること)
* ExerciseのmainでGasStationのrefuel()を2度呼び出しなさい。また、refuel()を呼び出す毎にfuelを表示しなさい。
* Carインスタンスのrun()を呼び、燃料が1消費されていることを確認しなさい。</br>
lecture02の課題2-1では、mainメソッド内に`car.fuel += 20;`と入力できたが、今回の課題で用いたCarインスタンスではコンパイルエラーとなるのは何故か。</br>
また、Carクラスのrun()でfuelに直接アクセスしてもエラーが起きないのは何故か。

#### 実行結果


```java
給油しました。
	残量:20
給油しました。
	残量:40
	燃料を1消費して走りました。
	残量:39
```


### 課題2

以下のクラスを作成せよ。</br>
/*image*/
* 作成したクラスをカプセル化し、必要に応じてアクセサを新たに追加せよ。
* attack()では引数で受け取ったFighterのHPを自分のstrength分減らし、与えたダメージ量と、ダメージを与えたということを表示する。
* isAlive()では自分のHPを比較し、生きているかををbooleanで返す。
* HP, strength, nameは引数付きコンストラクタにて初期化せよ。
* Fighterを2つインスタンス化し、互いに戦わせる。
* Fighterのコンストラクタに各自適当に値を見繕いインスタンス化し、main内に保持せよ。
* whileを用いて、どちらかのFighterが倒れるまで攻撃を繰り返す。
* ダメージが発生するごとに残りHPを表示する。
* ifを用いて勝敗を表示する。

#### 実行結果


```java
Fighter1はFighter2に100ダメージを与えた。
Fighter2の 残りHP: 80
Fighter2はFighter1に150ダメージを与えた。
Fighter1の 残りHP: 60
Fighter1はFighter2に100ダメージを与えた。
Fighter2の 残りHP: -20
Fighter2は倒れた。
Fighter1は勝利した。
```


### 課題3

銀行のATMシステム(みたいなもの)を作成しなさい。</br>
* クラスはAccountとExercise3_3の二つで、最低限以下どちらかのクラス図になるような機能を備える。
/*image*/
* 作成したクラスをカプセル化しなさい。
* ここまで作成したメソッドの処理を記述しなさい
* depositは入金
* withdrawは引き出し
* matchAccountNumberはnumberの一致するアカウントを探す
* main内に複数アカウントをインスタンス化し、入金と引き出しを用いbalanceの値が変更できることを確認せよ。
* 現時点では、アカウントの認証がないまま入金や引き出しが可能となっている。
* メソッドを１つ以上用意(いくつ作るかは個人の判断に任せる)し、アカウント群・口座番号・金額(それ以外に必要な引数があれば随時追加すること)を引数に渡すことでアカウント群からアカウントを探し、入金・引き出し・アカウントの詳細の表示をするようにプログラムを変更せよ。
* 先のクラス図では、システムを抽象的に示しただけであるため、ここまでプログラムを作成しても機能は足りない。各自、必要だと思しき機能を追加せよ。
* 操作ごとにログが残るようにメソッドに標準出力で操作内容を表示するようにせよ。
* 適当なアカウントの口座への操作を記述し、意図通りプログラムが動くかを確認せよ。

#### 実行結果

```java
川越さんのアカウントを作成しました
初期残高は 1000 円、口座番号は 123456 です
前川さんのアカウントを作成しました
初期残高は 200 円、口座番号は 654321 です
川越さんの口座から 100 円引き出しました
前川さんのに口座に 200 円入金しました
名前:川越 口座番号:123456 残高:900
名前:前川 口座番号:654321 残高:400
```


## 課題が終わった学生

次回はオブジェクト指向の重要な概念の2つ目である “継承” を学習して頂きます。</br>
継承はオブジェクト指向の重要な概念でありながら、最も理解し辛い要素でもあります。</br>
継承は簡単に言ってしまうと、同じような機能を持つクラスが複数ある時、それらの元(親)となるクラスを作成し、その親クラスから派生した子クラスを定義することで親クラスのフィールド/メソッドを使いまわす手法の事を言います。</br>
また、メソッドについては、オーバーライドという機能を使うことで、親クラスのメソッドの処理をサブクラスの中で書き換えることも出来ます。</br>
これはあくまでざっくりとした説明であるため、これが継承のすべてではありません。</br>
各自、オブジェクト指向プログラミングとはいったいどういったものなのか調べてみてください。</br>
