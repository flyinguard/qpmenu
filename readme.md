# qpmenu
指定フォルダ配下をサブフォルダ含めてポップアップメニュー表示して一発アクセス。

![qpmenu](https://user-images.githubusercontent.com/23325839/40714460-a7fbb08e-643d-11e8-801b-00f9f8f673ed.jpg)

## Requirement
- [AutoHotkey](https://autohotkey.com/) v1.1.27+

## Installation
- `config.ahk.sample` を `config.ahk` にリネーム後、正しい設定を埋める

あとは `qpmenu.ahk` を実行するだけです。

## Usage
普通に実行すると「qpmenu.ahk のあるフォルダ」を辿り、メニューを「マウスカーソル位置」に表示します。

```
$ qpmenu.ahk
```

**辿るフォルダを指定する** 場合は、そのフォルダパスを与えてください。

```
$ qpmenu.ahk "d:\work\text"
```

**メニュー表示位置をピクセルで指定する** こともできます(以下は画面左上 `(0, 0)` に表示する例)。

```
$ qpmenu.ahk -x 0 -y 0
```

## Usage - オープンモード
メニュー項目選択時、修飾キー(Shift, Ctrlキーなど)の押下状況で動作が変わります。

### 何も押さずに選択する
該当するファイルを **そのまま開きます**。

### Shift キーを押したまま選択する
該当するファイルを **テキストエディタで** 開きます。

使用するエディタは `config.ahk` 内で設定してください。

### Ctrl キーを押したまま選択する
該当するファイルのある **ディレクトリ** を開きます。

## Build
実行ファイルを作ることができます。

- `build.ahk.sample` を `build.ahk` にコピーする
- `build.ahk` を開き `builder` 変数の値を正しいものに修正する
  - 例: `builder = C:\Program Files\AutoHotkey\Compiler\Ahk2Exe.exe`
- `build.ahk` を実行する

## 付録

### 付録1. 秀丸エディタから呼び出す
秀丸エディタから qpmenu を呼び出すマクロ qpmenu_from_hidemaru.mac を同梱しています。

使い方:

- (1) `qpmenu_from_hidemaru.mac.sample` を `qpmenu_from_hidemaru.mac` にリネーム後、必要な設定を埋める
  - `$ahk_bin_path` 変数と `$qpmenu_path` 変数
- (2) `qpmenu_from_hidemaru.mac` を秀丸エディタにマクロ登録する
- (3) 2 で設定したマクロにショートカットキーを割り当てる

ショートカットキーを押すと「カーソル（キャレット）位置」に、「今秀丸エディタで開いているファイルのあるフォルダ」を基点として、qpmenu が表示されるはずです。

## FAQ

### Q1. メニュー項目末尾の ` | 1` この数字は何ですか？
Ans: 仕様です。消せません。

以下 AutoHotkey プログラミングの話になりますが事情を書いておきます。

AutoHotkey でポップアップメニューを作成するには `Menu` 命令を使います。この `Menu` 命令では「この選択が選択されたらこのラベルにジャンプする」という処理をサポートしており、また「選択されたメニュー項目名を取得する」命令も用意されています。

言うなればこの二つのパーツで「指定されたメニュー項目に対応するファイルパス」を特定しなければならないのですが、結論を言うとこの二つだけでは特定できません。特定するためには各項目ごとに固有の識別子が必要です。それを qpmenu では、メニュー項目名末尾に ` | (識別子)` を付けることで対応しています。

### Q2. メニューの表示に時間がかかるのですが……
Ans: 仕様です。

極端な例を挙げると、C:\ ドライブ配下を辿らせたら応答が返ってきません。そうでなくとも作者環境では 10000 ファイルを含むフォルダを辿らせて30-60秒くらいの時間を要しています。ファイル数の多いフォルダや、深い階層を持つフォルダは辿らせない方が良いでしょう。

もし表示に時間がかかりすぎて待ってられない場合は、タスクトレイアイコンから終了させることもできます。

## License
[MIT License](LICENSE)

## Author
[stakiran](https://github.com/stakiran)
