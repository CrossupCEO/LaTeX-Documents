# Visual Studio CodeでLaTeXを利用する
Visual Studio Code（以下，VS Code）はMicrosoftが開発しているGUIエディタであり，多くのプログラマに愛用されています．VS Codeでは様々な拡張機能が配布されており，ここではLaTeXをVS Codeで利用するための手順とLaTeXを使うのに必要な拡張機能を紹介します．

※ TeX Liveを導入済の前提で説明します．

# VS Codeのインストール
VS Codeを[こちら](https://code.visualstudio.com)のサイトからダウンロードしてください．英語で記述されていますが，後でVS Codeの日本語化を行うので心配しないでください．
![vscode-web](https://github.com/CrossupCEO/LaTeX-Documents/blob/main/vscode/img/vscode-web.png)

# 拡張機能のインストール
## 拡張機能のインストール方法
1. 左端のバーから**Extintions**タブを選択します
2. 検索欄に拡張機能名（以下で紹介）を入力します．
3. インストールしたい拡張機能を選択し，**Install**をクリックします．

## 必須な拡張機能
上記のインストール方法に従って，以下の拡張機能をインストールしてください．

### Japanese Language Pack for Visual Studio Code
VS Codeを日本語化してくれる拡張機能です．Japanese Language Packで調べると出てきます．

### LaTeX Workshop
VS CodeでLaTeXを使う上で最も重要な拡張機能です．これを導入することでLaTeX文書のコンパイルが行えるようになります．

# LaTeX Workshopの設定
LaTeX WorkshopをインストールするだけではVS CodeでLaTeX文書をコンパイルすることができません．LaTeXのコンパイルで使うツールを設定しなければなりません．以下ではdvipdfmxとpLaTeX2eを使ったコンパイル設定を紹介します．

GUIの設定画面がありますが，ここでは簡潔に説明するためにコードを記述することで設定します．大丈夫です．難しくありません．
1. ファンクションキーF1または，Ctrl-Shift-P（macOSでは⇧⌘P）でコマンドパレットを表示します．
2. settingsまたは設定と検索します
3. 「基本設定: 設定 (JSON) を開く」を選択します
4. settings.jsonというファイルが開かれるはずです
5. settings.jsonに以下のコードを記述し保存してください．こちらのコードは[こちら](https://github.com/CrossupCEO/LaTeX-Documents/blob/main/settings.json)からダウンロードできます．
```
{
    "latex-workshop.latex.tools": [
        {
            "name": "ptex2pdf",
            "command": "ptex2pdf",
            "args": [
                "-l",
                "-ot",
                "-kanji=utf8",
                "-interaction=nonstopmode",
                "-synctex=1 -file-line-error",
                "%DOCFILE%.tex"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "pLaTeX2e",
            "tools": [
                "ptex2pdf"
            ]
        }
    ],
    "latex-workshop.view.pdf.viewer": "tab",
    "editor.renderControlCharacters": true,
    "editor.accessibilitySupport": "off"
}
```
以上で設定完了です．

【補足】こちらのコードを説明します
- `latex-workshop.latex.tools` では，数あるコンパイルコマンドから使いたいコマンド`command`を引数`args`と共に好きな名前`name`をつけてtoolとして登録します．今回は`ptex2pdf`というコマンドしか登録していません．
- `latex-workshop.latex.recipies` では，`latex-workshop.latex.tools`で登録したtoolからどれを選んでコンパイルするかrecipieとして記述します．例えば，コンパイルボタンを押すと，`ptex2pdf`というtoolを3回繰り返すrecipieを作成できます．今回は一般的な1回だけのrecipieを作りましま．

# 実際の利用方法
VS CodeでLaTeXファイル（拡張子`.tex`）を開いてください．LaTeX Workshopが導入済の場合，上部に2つのボタンが追加されているはずです．
- Build LaTeX Project：LaTeXファイルのコンパイルを行うボタン
- View LaTeX PDF File：ページを2分割し，右側にコンパイル結果のPDFを表示する．

LaTeXファイルをコンパイルする際は，Build LaTeX Projectボタンをクリックするだけでコンパイルが完了します．また，エラーが発生した場合はエラー内容が下部に表示されるはずです．

![latexworkshop](https://github.com/CrossupCEO/LaTeX-Documents/blob/main/vscode/img/latexworkshop.png)
