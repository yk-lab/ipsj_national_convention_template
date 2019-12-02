# 情報処理学会全国大会用テンプレート
`maketitle` コマンドの再定義部分については [jsclasses(Haruhiko Okumura, Japanese TeX Development Community)](https://github.com/texjporg/jsclasses) の `maketitle` コマンドを改変しています。

## 動作確認環境
* MacTeX (2019.0410)
* upLaTeX (e-upTeX 3.14159265-p3.8.2-u1.25-190131-2.6 (utf8.uptex) (TeX Live 2019))
* dvipdfmx (20190503)

## 実行方法
開発時に実際に実行していた方法を紹介します。

以下の内容で `.latexmkrc` というファイルをプロジェクトルートに作成します。
なお，Skim のインストールが必要な内容になっているので，`$pdf_previewer` の内容は必要に応じて変更してください。

```perl:.latexmkrc
#!/usr/bin/env perl
$latex            = 'uplatex -synctex=1 -halt-on-error -shell-escape';
$latex_silent     = 'uplatex -synctex=1 -halt-on-error -interaction=batchmode';
$bibtex           = 'upbibtex';
$dvipdf           = 'dvipdfmx %O -o %D %S';
$makeindex        = 'mendex %O -o %D %S';
$max_repeat       = 5;
$pdf_mode	  = 3; # generates pdf via dvipdfmx

# Prevent latexmk from removing PDF after typeset.
# This enables Skim to chase the update in PDF automatically.
$pvc_view_file_via_temporary = 0;

# Use Skim as a previewer
#$pdf_previewer    = "xdg-open";
$pdf_previewer = 'open -a /Applications/Skim.app'; # Skimの場所を指定する
```

その後，プロジェクトルートに移動し， `latexmk` コマンドを用いて PDF の作成などを行います。

```console
$ cd <Project_root>
$ latexmk -pvc sample.tex
```
