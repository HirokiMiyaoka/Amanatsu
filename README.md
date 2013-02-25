Amanatsu
========
## Android
Version 2.2 or higher(Enable multi touch).

## How to use
Iy you only want to use Amanatsu, Download "Amanatsu.jar".
And copy "Amanatsu.jar" to "libs/" dir in your project.

## Compile
Use Eclipse.
Do not export "AndroidManifest.xml" and "project.properties".

## Sample code

<pre><code>
package XXXXX;

import android.os.Bundle;
import android.app.Activity;
import net.azulite.Amanatsu.*;

public class XXXXX extends Activity
{
  Amanatsu ama;

  @Override
  public void onCreate( Bundle savedInstanceState ) {
    super.onCreate( savedInstanceState );

    // Create Amanatsu object.
    ama = new Amanatsu( this, new Game() );

    // Set View.
    this.setContentView( ama.getGLSurfaceView() );

    // Start game.
    ama.start();
  }

}

class Game extends GameView
{
  @Override
  public void UserInit() {
    // Prepare game.
  }

  @Override
  public boolean MainLoop() {
    // Game main routine.
    return true; // false is Game end.
  }

  @Override
  public void CleanUp() {
    // Cleanup game.
  }

}
<code></pre>

## Android
バージョン2.2以上。

## 利用方法
使いたいプロジェクト内にlibsフォルダを作り、その中にAmanatsu.jarをコピーします。
ソースとか興味なくてただ単に使いたい場合は、ルートディレクトリにある"Amanatsu.jar"をダウンロード(ファイル名をクリック->Raw or View Rawをクリック)して、プロジェクト内に用意した libs/ ディレクトリに入れてください。

で、後は上のような感じで適当にゲーム処理を記述するためのGameクラス(GameViewを継承)を作り、Amanatsuオブジェクト生成時に渡したり、View登録時にAmanatsuのViewを登録してください。

また、GameViewクラスを継承すると、system、draw、sound、inputというクラス変数が利用可能で、それを使うことでゲームに必要な各種処理を行うことができます。

GameViewクラスは次のようになっています。

#### UserInit
実行開始の初めの一度だけ実行されるメソッド。

#### MainLoop
毎フレーム呼ばれるメソッド。

#### CleanUp
終了時に呼ばれるメソッド。

### Javadoc
Javadocはこちら(日本語)。

* [http://hiroki.azulite.net/wiki/Amanatsu/doc/](http://hiroki.azulite.net/wiki/Amanatsu/doc/)

## コンパイル方法
EclipseにAmanatsuのプロジェクトを追加し、プロジェクトをエクスポートしてJARファイルとして出力します。
ただし、"AndroidManifest.xml"と"project.properties"はエクスポートしないようにチェックボックスを外すこと。

## その他

### リソース

##### 画像
画像の場合、res以下のディレクトリに入れると画像がリサイズされる場合があります。
assetsに入れることを推奨(その場合createTextureではテクスチャ番号とファイルパスを与える形になる)。

##### 音声
res/rawもしくはassets内に置いてください。
前者はリソース番号、後者は音番号とファイルパスで読み込みや再生が可能。

### 入力

##### タッチ

Amanatsuでの入力は座標以外にもいくつか特徴があります。

* タッチフレームの取得(getTouchFrame, getFingerTouchFrame)
  * タッチされたフレーム数を返す
  * 0は未タッチ、-1は離れた。
  * 指番号を指定する場合-1を観測できない場合がある。
     * 指IDを使う Finger 系の命令を使うと良い。
     * getFingerIdなどで予めIDを取得すること。

##### キー入力

キー番号を指定して、その番号に割り当てられたキーが押されているかどうかや押しているフレーム数を調べることが出来ます。
フレーム数に関してはタッチ同様の仕様。

キー番号はWindowsなどの仮想キーではなく、Androidが独自に？設定した比較的順番等に規則性があるものになっています。
また、Amanatsu.K_キー名 である程度のキー番号を得ることが出来ます。
キー名は戻るボタンのBACKやキーボードのZなどの英数字、UPやSPACEなどのような名前が割り当てられています。

### リファレンス

 * [Amanatsu Javadoc](http://hiroki.azulite.net/wiki/Amanatsu/doc/)

### Amanatsuについて

#### 元ネタ
AmanatsuはWindowsのVC++用ゲームライブラリであるMikanライブラリのAndroid版だったり。

#### OpenGLの勉強をしようと思っている人へ
AmanatsuはOpenGL的に見ると、あんまりよろしくない方法を用いて高速化を行なっていると思われます。

Amanatsu全体で整合性を取るようにしているので、一部をコピーしただけではまともに動きません。

早い話、OpenGL周りは全く参考にならないということです。書籍や他の解説サイトを利用しましょう。

#### チューニングについて
極力GCを避けたいので、大きくなりそうなデータや頂点用の配列などはクラス内で使いまわしています。
そのため、並列化？　なにそれ美味しいの？　と言わんばかりの処理が勢揃いすることに。
並列化したい場合、ゲーム処理と描画処理を分けるなどの工夫をする必要があります。

#### ロゴについて
今のは適当なので、依頼予定。
