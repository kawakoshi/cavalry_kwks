# Cavalry CLI -コマンドライン入力-

> コマンドラインインターフェース

https://docs.cavalry.scenegroup.co/applications/cavalry-cli

## 全般(General)

Cavalry CLI（コマンドラインインターフェース）は、Cavalry自体を起動しなくてもレンダリングを含む様々なタスクを可能にします。

実行するには（デフォルトの場所にCavalryをインストールしたと仮定して）

### **macOS**

- **Terminal**(ターミナル)を開きます。 (Applications/Utilities/Terminal).
- 以下のように入力し、エンターキーを押します。

```
$ cd /Applications/Cavalry.app/Contents/Applications/CavalryCLI.app/Contents/MacOS/
$ ./cavalry-cli [your command here]
```

### **Windows**

- **Command Prompt**(コマンドプロンプト)を開きます。
- 以下のように入力し、エンターキーを押します。

```
> cd C:\Program Files\Cavalry
> .\cavalry-cli [your command here]
```

`./cavalry-cli -h` (macOS) または `.\cavalry-cli -h`

を入力してEnterを押すと、以下のようなヘルプ情報が出力されます。

```
Command Line Interface
Usage: Cavalry CLI [OPTIONS] [SUBCOMMAND]


  -h,--help                   Print this help message and exit


Subcommands:
  render                      Render a scene
  version                     Version information
  auth                        Authenticate (Password may be piped or entered when prompted)
  proxy                       Set proxy settings
  list                        List additional information
```

## 

## Render

>  CLI経由でのレンダリングはProfessionalプランでのみ利用可能です。

`./cavalry-cli render -h` (macOS) または `.\cavalry-cli render -h` (Windows) 

を入力してEnterを押すと、以下のようなヘルプ情報が出力されます。

```
Render a scene
Usage: Cavalry CLI render [OPTIONS] scene


  scene TEXT REQUIRED         The full path to the Scene file.


  -h,--help                   Print this help message and exit
  -p,--padding INT            Frame number padding.
  -f,--frame INT              A single frame to render. If set, startFrame and endFrame will be ignored.
  -s,--startFrame INT         The first frame of a range to render.
  -e,--endFrame INT           The last frame of a range to render.
  -n,--name TEXT              The filename prefix.
  -d,--directory TEXT         The output directory.
  --backend TEXT              The rendering backend. Options: opengl (default), raster.
  --scale FLOAT               The Resolution Scale (unit: percent).
  --composition TEXT          The ID of the composition to render. See the 'list' command for more info.
  --render-item TEXT          The ID of the render item to render. See the 'list' command for more info. Note: All other options will be ignored.
  --dynamicCount INT          The number of Dynamic Renders to perform.
  --dynamicRange INT x 2      Set an inclusive range of Dynamic Renders to perform [start end].
[format]
  Rendering format
    --format TEXT               Sets the output format. Options: png (default), jpeg, svg, gif, apng, prores
  [PNG]
      --compression INT           Compression (0 to 9)
      --filter INT                Filter (1, 2 or 3)
  [JPEG]
      --quality INT               Quality (0 to 100)
  [ProRes]
      --codec TEXT                422HQ, 422, 422LT, 422Proxy, 4444, 4444XQ
```

これらのフラグを使ってコマンドを作成することができます。

以下の例では、「 sceneName.cv」のcvファイルの 0-50 フレームを、「outputFileName」という名前のアニメーション png としてデスクトップにレンダリングします。

**macOS**

```
./cavalry-cli render ~/Desktop/sceneName.cv -n outputFilename -d ~/Desktop/ -s 0 -e 50 --format apng
```

**Windows**

```
.\cavalry-cli render C:\Users\Username\Desktop\sceneName.cv -n outputfilename -d C:\Users\Username\Desktop\ -s 0 -e 50 --format apng
```

>  ファイルがプロジェクト設定で保存されている場合、-d (ディレクトリ) を設定しなければ、すべての出力はプロジェクト設定で定義された Renders ディレクトリに保存されます。

## Version

現在インストールされているCavalryのバージョンを確認するには、バージョンコマンドを実行します。

`./cavalry-cli version -h` (macOS) または `.\cavalry-cli version -h` (Windows)

を入力してEnterを押すと、以下のようなヘルプ情報が出力されます。

```
Version information
Usage: Cavalry CLI version [OPTIONS]


  -h,--help                   Print this help message and exit
```

### **macOS**

```
./cavalry-cli version
```

### **Windows**

```
.\cavalry-cli version
```

以下のように、インストールされているCavalryのバージョンを返します。

```
[11:30:29.657 info    ] App Version: 0.15
```

## **Auth-認証-**

CLIを使用してレンダリングするには認証が必要です。
直近でProfessionalライセンスでCavalryアプリケーションを使用したことがある場合、すでに認証されていますが、認証されていない場合は、authコマンドを使用して認証することができます。

`./cavalry-cli auth -h` (macOS) or `.\cavalry-cli auth -h` (Windows)

を入力してEnterを押すと、以下のようなヘルプ情報が出力されます。

```
Authenticate (Password may be piped or entered when prompted)
Usage: Cavalry CLI auth [OPTIONS] email


  email TEXT REQUIRED         Email Address
```

以下のようにメールアドレスを入力します。(name@email.comは自身が登録したものに置き換えてください)

```
./cavalry-cli auth name@email.com
```

その後、パスワードの入力を求められます。
認証されると、Render コマンドが実行されます。

## Proxy

プロキシサーバの設定は、proxyコマンドを使用して入力/更新することができます。

`./cavalry-cli proxy -h` (macOS) または `.\cavalry-cli proxy -h` (Windows)

を入力してEnterを押すと、以下のようなヘルプ情報が出力されます。

```
Set proxy settings 
[At least 1 of the following options are required]
Usage: Cavalry CLI proxy [OPTIONS]

  -h,--help                   Print this help message and exit
  --address TEXT Excludes: --reset
                              Server Address
  --username TEXT Needs: --address Excludes: --reset
                              Username (Password may be piped or entered when prompted)
  --reset Excludes: --address --username
                              Reset proxy settings
```

## **List**

>  Professionalプランでのみご利用いただけます。

コンポジション（Composition）やレンダーキュー（Render Queue）のアイテムIDのように、シーンに関する追加情報をリストアップすることができます。
 これらは、フラグとしてレンダーコマンドに追加することができます。

`./cavalry-cli list -h` (macOS) または `.\cavalry-cli list -h` (Windows)

を入力してEnterを押すと、以下のようなヘルプ情報が出力されます。

```
List additional information
Usage: Cavalry CLI list [OPTIONS] [scene]


  scene TEXT                  The full path to the scene file.


  -h,--help                   Print this help message and exit
  --compositions Needs: scene List all compositions
  --render-items Needs: scene List all render items
```

例えば、以下のようにコマンドと、リストを表示したいファイルパスを指定することで、そのシーンに含まれる全てのコンポジションの情報を出力します。

**macOS**

```
./cavalry-cli list ~/Desktop/sceneName.cv --compositions
```

**Windows**

```
.\cavalry-cli list C:\Users\Username\Desktop\sceneName.cv --compositions
```

Enterを押すと、以下のようにシーン内のコンポジションとそのIDのリストが表示されます。

```
[11:17:43.468 info    ] Relinked asset: asset#2
[11:17:43.471 info    ] Composition ID                Composition Name              
[11:17:43.471 info    ] compNode#1                    Composition 1                 
[11:17:43.471 info    ] 
[11:17:43.471 debug   ] Saving preferences
```

コンポジション ID は、レンダリングコマンドの一部として '--composition' フラグを使用することができます。
例えば、Composition 1 をレンダリングしたい場合は、'--composition compNode#1' をレンダリングコマンドに追加します。

## **用語集(Glossary)**

**INT** - 整数とは、小数点以下を含まない数値です。
 例：`4`

**INT x 2** - 範囲を定義するための2つの整数の集合です。
例：`4 8 ` (`4[space]8`)

**FLOAT -** フロートとは、小数点以下の桁数を持つ数字のことです。
例：`23.5`

**TEXT** - 文字、数字、特殊文字、ダッシュ記号、数字記号を含むことができるテキスト文字列です。
例：`sceneName-01`