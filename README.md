# Udon-Batting-Gimmick

バッティングマシンのUdonギミックです。

[![サンプル動画](http://img.youtube.com/vi/ZKBDG-i4U7k/0.jpg)](https://www.youtube.com/watch?v=ZKBDG-i4U7k)  
https://youtu.be/ZKBDG-i4U7k



<img height=400 src=res/images/29.png>


複数人でもプレイ可能です。スコアボードに各プレイヤーの飛距離が表示されます。  
<img height=300 src=res/images/25.png> <img height=300 src=res/images/26.png>  
<img height=180 src=res/images/28.png>

変化球と球の速さの調整も行えます。  
<img height=180 src=res/images/27.png>


## 導入方法

サンプルシーンから開く方法とギミックプレハブを設置する2つの方法があります。

### サンプルシーンを開く
*Assets/BattingCenterGimmick/BattingCenterGimmick.unity*

<img src=res/images/1.png>

こちらはワールドにギミックを設定したサンプルシーンとなります。

Unityのプレイボタンやローカルワールド起動からそのまま遊ぶことができます。

改変をする際にこのシーンから始めることもできます。

### ギミックプレハブを設置する
*Assets/BattingCenterGimmick/Prefabs/BattingCenterGimmick.prefab*

<img src=res/images/2.png>

こちらをワールドに設置するとギミックが動作します。

#### ホームベース、ピッチャー位置の合わせ方

1. 最初に `BattingCenterGimmick` オブジェクトを回転させて ホームベース - ピッチャー位置 を結ぶ方向を合わせます。
2. `BattingCenterGimmick` オブジェクトを移動してポームベースの位置を合わせます。  
3. `@BattingMachine` プレハブの `#LauncherPositionAnchors` オブジェクトの `z` 座標を動かしてピッチャー位置と合わせます。


<img height=200 src=res/images/22.png><img src=res/images/23.png>  
<img src=res/images/24.png>  


※ 全体のスケールは変更しないでください。  
ボールの方向は`BattingCenterGimmick`オブジェクトの回転で調整してください。  
後述の「※ 差し替えの注意点」もご確認ください。


## 音設定

`Assets/BattingCenterGimmick/Sounds` 内のファイルを差し替えることで効果音を変更できます。  
`bound`: ボールがバウンドした時の音  
`hit_1`: ボールを打った時の音  
`hit_2`: 使用されていません  
`launch`: ボールが投げられた時の音 

効果音ラボの音源を使用する場合は以下がおすすめです。  
https://soundeffect-lab.info/

`bound`: サッカーボールが跳ねる1 (生活 [3])  
`hit_1`: 木製バットで打つ1 (生活 [3])  
~~`hit_2`: 木製バットで打つ2 (生活 [3])~~  
`launch`: キャンセル4 (ボタン・システム音)  

生活 [3]  
https://soundeffect-lab.info/sound/various/various3.html

ボタン・システム音  
https://soundeffect-lab.info/sound/button/





## モデル、テクスチャの差し替え方法

最初に差し替えにおける注意事項を2点説明します。

### ※ 差し替えの注意点1: 命名規則

オブジェクトやプレハブは「`@`」や「`#`」など特定の記号で始まるものがあります。  
これらはプログラム中で識別のために使用されているため、記号に続く名称も含めて変更しないで下さい。  
<img src=res/images/12.png>



### ※ 差し替えの注意点2: プレハブの編集

ギミックはプレハブになっているため編集方法によっては変更が意図通りに反映されない場合があります。

<hr>

例えば、以下の画像のように `BattingCenterGimmick` の子に `@BattingMachine` が人数分設置されています。  
1つの `@BattingMachine` を直接シーン上で編集しただけではその1つにしか反映されません。  
<img src=res/images/3.png>

これを全てのプレハブに反映するには以下の2つの編集方法があります。

#### 方法1: プレハブ上での編集


`Assets/BattingCenterGimmick/Prefabs` にプレハブが入っているためそちらを編集します。  
<img src=res/images/4.png>

プレハブをダブルクリックすると以下のようにプレハブを編集できます。  
プレハブの中にさらにプレハブがある場合はそちらもプレハブから編集します。  
<img src=res/images/5.png>

プレハブを保存してシーン編集画面に戻るとシーン上のすべてのプレハブに変更が反映されます。  
画像中の黄色で囲った「＜」マークを押すとプレハブを保存して閉じることができます。



#### 方法2: シーン上での直接編集

<img src=res/images/6.png>

上の画像ではボールの見た目サイズを変更するために `#Body` オブジェクトの `Scale` 値を変更しました。

画像のように、プレハブ内の値を変更すると変更した箇所に青色の印が付きます。  
(`Scale` と表示されている左)

ここを右クリックすると以下の画像のようにメニューが出てきて、変更した値をプレハブに反映するか(プレハブのデフォルト値とするか)、破棄するか、を選択できます。

`Apply to Prefab ...` を行えば元のプレハブのデフォルト値に設定でき、シーン上のほかのプレハブにも反映されます。  
`Revert` を行うとその変更を破棄することができます。プレハブのデフォルト値に戻ります。

<img src=res/images/7.png>



### バット
モデルを置き換える場合は `@BattingMachine` プレハブの `#Bat/#Body` 以下にある `Bat` を置き換えます。  
<img src=res/images/8.png>

当たり判定のサイズを変更する場合は `#Bat/#Colliders/#Collider` に付与されている `Capsule Collider` のY座標、`Radius`、`Height` を変更します。  
<img src=res/images/9.png><img src=res/images/11.png>

当たり判定の見た目はSceneビュー上で確認できます。  
<img height=250 src=res/images/10.png>

### ボール

モデルを置き換える場合は `@BattingMachine` プレハブの `#Balls/@Ball_1/#Body` 以下にある `Ball` を置き換えます。  
<img src=res/images/13.png>

当たり判定のサイズを変更する場合は `#Balls/@Ball_1/#Scale/#ScaleReference` の `Scale` 値を変更します。  
こちらもバットと同じく当たり判定の見た目はSceneビュー上で確認できます。  
(ボールは `#Collider` を変更しないでください)  
<img src=res/images/14.png>

エフェクトを調整する場合は `#Effects/#Trail`、`#Effects/#BallTrailParticle` を変更します。

打球時の砂煙エフェクトとバウンド時のエフェクトは `Particles/Hitting`、`Particles/Bounding` を変更します。  
この2つは `@BattingMachine` オブジェクトのインスペクタ上で参照されているためもし参照が外れた場合は再設定が必要です。


### グラウンド
グラウンドのモデルは `BattingCenterGimmick` シーンの `References/FieldModels` に設置しています。  
プレハブは `Assets/BattingCenterGimmick/Prefabs/Parts/FieldModels.prefab` になります。

### 同梱モデルファイル
バットやホームベースのモデルなどは `Assets/BattingCenterGimmick/Models` に入っています。  
<img src=res/images/15.png>


### ターゲット

ボールが当たるとエフェクトが出るターゲットの変更方法です。

モデルの変更は `BattingCenterGimmick` プレハブの `#Targets/@Target_1/body/Target` を差し替えます。  
ボールが当たった時のエフェクトは `#Effects/#Particle` に設定されている `ParticleSystem` に対して `play`の処理が走るようになっています。  
当たり判定の調整は `#TargetCollider` で行います。  
無効化するには `#Targets` 自体を非アクティブにしてください。  
<img src=res/images/16.png>



### 設定UI


`Assets/BattingCenterGimmick/Prefabs/Parts/UI` にあるプレハブを編集してください。  
<img src=res/images/17.png>


UIの見た目変更のために画像を追加した場合は `Assets/BattingCenterGimmick/Textures/setting_img/Atlas` に保存されている画像の設定値が参考になるかもしれません。  
これらの画像と一緒にAtlas化する場合は同じフォルダ内に画像を保存して `Assets/BattingCenterGimmick/Textures/setting_img/SpriteAtlas.spriteatlas`を選択して `Pack Preview` を行います。  
<img src=res/images/21.png>




ボール速度表示UIとスコア表示UIはバットを持った状態でホームベースを中心に左に立つか右に立つかでUIの位置が左右入れ替わるようになっています。
この入れ替わる場所は `#UIs/#BallSpeedUILeftSidePosAnchor`、`#UIs/#ScoreBoardUILeftSidePosAnchor` オブジェクトの位置と向きが参照されています。




## 設定変更

初期人数や初期のボールの設定値などの変更方法に関してです。

### 初期設定


`BattingCenterGimmick` オブジェクトをクリックすると `Inspector` に設定が表示されるのでそちらを変更します。

*変化球* : 最初に選択される変化球レベル  
*球の速さ* : 最初に選択される球速  
*プレイ人数* : 最初に選択されるプレイ人数  
*ボール速さ倍率* : ボールの速さに倍率をかけます。例えば `2` にすると2倍になります。  
*打球の上への飛びやすさ倍率* : 大きくするほど打った時にボールが上方へ飛びやすくなります。  
*打球飛びやすさ倍率* : 打球時のボールの速さに倍率をかけます。例えば `2` にするとボールを打ち返した時の速度が2倍になります。  
<img src=res/images/18.png>

### ストライクゾーンサイズ、位置設定

位置とサイズの変更は `@BattingMachine` プレハブの `#HomeBasePositionAnchor/#StrikeZoneAnchor` の `Position`、`Scale` 値を設定します。

ストライクゾーンのデフォルト高さは `#StrikeZoneAnchor` の高さになります。  
ゲーム内のストライクゾーン高さ調整UIスライダーで変更できる範囲は `#StrikeZoneHeightMin` の高さ ～ `#StrikeZoneHeightMax` の高さとなります。  
(ストライクゾーンの下端上端ではなく `#StrikeZoneAnchor` の `Position` の範囲となります)  


<img height=400 src=res/images/20.png><img src=res/images/19.png>


## エラーに関して
プレハブを編集する際に以下のエラーが大量にコンソールに出力されますが無視して問題ありません。

*"ArgumentNullException: Value cannot be null."*
