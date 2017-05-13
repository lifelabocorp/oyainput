# このソフトについて

Linuxで親指シフト入力を可能にするためのソフトウェアです。 
MozcやAnthy、libkccなど、主要な変換エンジンで利用可能です。 
fcitxでの利用を想定していますが、ibusやuimでも利用可能です。 
新しめのLinuxならだいたい動くと思います。 
Ubuntu16.04LTSで動作確認しています。


# インストール方法

ターミナルから以下のコマンドを入力します。

  $ make clean; make; sudo make install

インストールには管理者(root)権限が必要です。 
またGCC、makeが必要ですので、もしエラーになる場合はapt-get
などで事前に導入しておいてください。


# 起動方法

  $ oyainput [username]

usernameは利用するユーザー名を指定します。
省略した場合は、現在のログインユーザー名になります。
もしsuコマンドなどで管理者(root)モードでターミナルにログイン
している場合はrootユーザのホームディレクトリを見に行くことに
なりますので、[username]は省略しないことをおすすめします。


# 設定ファイルについて
設定ファイルは、初回起動時にホームディレクトリ下に以下の
名前で作成されます。

  (HOMEDIR)/.oyainputconf

## 項目の説明 

1行ごとに、 
設定項目=設定値 
という書式で記述します。 
各設定項目の説明を以下に記述します。
 
LOYAKEY=キー名 
左親指シフトキー
 
ROYAKEY=キー名 
右親指シフトキー
 
ONKEY=キー名 
一時停止状態から再開します
 
OFFKEY=キー名 
一時停止状態にします
 
NICOLATIME=数字 
親指キー単独打鍵の判定時間(ミリ秒)を設定します
 
DEVFILENO=数字 
キーボードのデバイスイベントファイルの番号の数字を指定します。
本ソフトはキーボードを自動判別しますが、複数のキーボードが
接続されている場合に、うまく動作しない可能性があります。
その場合はこの設定で接続デバイス番号を指定します。
下記のコマンドでデバイス情報一覧が表示されますので接続されている
キーボードのデバイスイベント番号を調べることができます。

  $ cat /proc/bus/input/devices


IM=連携対象のインプットメソッドフレームワーク名 
日本語モードのONとOFFに合わせて、親指シフトモードのONとOFFを
自動で切り替えます。 
現在設定可能なのはfcitxのみです。 
IM=fcitx 
この設定を利用する場合は、fcitxの設定も確認してください。
下記のようになっていることを確認してください。
「入力メソッドの設定」で 
・１番最初に直接入力（キーボードまたはキーボードレイアウト名） 
・２番目に変換エンジン（Mozc、Anthyなど） 
となるように設定します。 
これで、たとえばfcitxの全体設定の入力メソッドのオンオフした
さいに、連動して親指シフトもオンとオフが自動で切り替わります。
 

KEYADD=(キー名):(出力ローマ字) 
通常打鍵時のキーを追加、または置換します
 
LKEYADD=(キー名):(出力ローマ字) 
左親指キー同時打鍵時のキーを追加（置換）します
 
RKEYADD=(キー名):(出力ローマ字) 
右親指キー同時打鍵時のキーを追加（置換）します
 

### 設定で指定可能なキー
キー名は以下が指定可能です。 
SPACE,A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z,
1,2,3,4,5,6,7,8,9,0,F1,F2,F3,F4,F5,F6,F7,F8,F9,F10,F11,F12,F13,
MINUS,SEMICOLON,APOSTROPHE,GRAVE,BACKSLASH,COMMA,DOT,SLASH,
ZENKAKUHANKAKU,KATAKANA,HIRAGANA,HENKAN,KATAKANAHIRAGANA,MUHENKAN,
ESC,EQUAL,BACKSPACE,TAB,LEFTBRACE,RIGHTBRACE,ENTER,
LEFTCTRL,RIGHTCTRL,LEFTSHIFT,RIGHTSHIFT,LEFTALT,RIGHTALT,
HOME,SCREENLOCK,CAPSLOCK,NUMLOCK,SCROLLLOCK,
SCROLLUP,SCROLLDOWN,UP,DOWN,LEFT,RIGHT,PAGEUP,PAGEDOWN,
KP0,KP1,KP2,KP3,KP4,KP5,KP6,KP7,KP8,KP9,KPMINUS,KPPLUS,KPDOT,
KPJPCOMMA,KPENTER,KPSLASH,KPLEFTPAREN,KPRIGHTPAREN,KPASTERISK,
102ND,RO,SYSRQ,END,INSERT,DELETE,YEN,LEFTMETA,RIGHTMETA,
 
出力ローマ字は以下が指定可能です。 
A,I,U,E,O,KA,KI,KU,KE,KO,SA,SI,SU,SE,SO,TA,TI,TU,TE,TO,
NA,NI,NU,NE,NO,HA,HI,HU,HE,HO,MA,MI,MU,ME,MO,YA,YI,YU,YE,YO,
RA,RI,RU,RE,RO,GA,GI,GU,GE,GO,ZA,ZI,ZU,ZE,ZO,DA,DI,DU,DE,DO,
BA,BI,BU,BE,BO,PA,PI,PU,PE,PO,WA,WI,WU,WE,WO,XA,XI,XU,XE,XO,
XYA,XYI,XYU,XYE,XYO,XTU,NN,VU,DEL,BS,QUESTION,
SLASH,TILDE,LKAGI,RKAGI,LBRACKET,RBRACKET,LPAREN,RPAREN,
0,1,2,3,4,5,6,7,8,9,MINUS,PERIOD,COMMA,KUTEN,KUTOUTEN,
NAKAGURO,DAKUTEN,HANDAKUTEN
