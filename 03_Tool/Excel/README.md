# Excel

<!-- TOC -->
- [1. 設定](#1-設定)
  - [1.1. クイックアクセスツールバー](#11-クイックアクセスツールバー)
- [2. ショートカット](#2-ショートカット)
  - [2.1. 一覧](#21-一覧)
- [3. アクセスキー一覧](#3-アクセスキー一覧)
  - [3.1. 書式(Option)](#31-書式option)
  - [3.2. 挿入(Insert)](#32-挿入insert)
- [4. マクロ](#4-マクロ)
  - [4.1. 自作マクロ](#41-自作マクロ)
    - [4.1.1. ファイル抽出](#411-ファイル抽出)
---
<br>
<!-- /TOC -->

## 1. 設定

### 1.1. クイックアクセスツールバー
1. Excelのオプションを開く。（ショートカット：alt → f → t ）
2. クイックアクセスツールバーで自分好みにカスタマイズする。<br>
[おすすめ設定](Excel%20Customizations.exportedUI)  
※端末にダウンロードして、ユーザー設定からインポートする。
<br>
<br>

## 2. ショートカット
### 2.1. 一覧
| コマンド | 意味 |
| ---- | ---- |
| ctrl + e | フラッシュフィル（法則性のあるデータの自動入力） |
<br>

## 3. アクセスキー一覧

### 3.1. 書式(Option)
| コマンド | 意味 |
| ---- | ---- |
| ALT → O → R → E | 行高の任意編集（Row hEight） |
| ALT → O → R → A | 行高の自動編集（Row Auto） |
| ALT → O → R → H | 行の非表示（Row Hide） |
| ALT → O → R → U | 行非表示の取消（Row Undo） |
| ALT → O → C → W | セル幅の任意編集（Cell Width） |
| ALT → O → C → A | セル幅の自動編集（Cell Auto）★ |
| ALT → O → C → H | 行の非表示（Cell Hide） |
| ALT → O → C → U | 行非表示の取消（Cell Undo） |

### 3.2. 挿入(Insert)
|  コマンド  |  意味  |
| ---- | ---- |
| ALT → I → B | 改ページの挿入 |

<br>

## 4. マクロ

### 4.1. 自作マクロ

#### 4.1.1. ファイル抽出

```vb
Sub OpenAllFile()
'##################################################
'# 名前：ファイルオープン
'# 機能：マクロ格納ディレクトリ配下のファイルを
'#       全て開いて閉じる
'# 備考：
'##################################################

'========================================
' 変数定義
'========================================
Dim strFilePath        As String
Dim strFileFullPath    As String
Dim strFileName        As String
Dim strExtension       As String
Dim wbMain             As Workbook
Dim wbOpen             As Workbook
Dim wsMain             As Worksheet
Dim wsOpen             As Worksheet

'========================================
' 変数設定
'========================================
'ブックの設定
Set wbMain = ThisWorkbook
'シートの設定
Set wsMain = wbMain.ActiveSheet
'拡張子の設定
strExtension = "xlsx"
'ファイルオープンフラグの初期化
flgOpen = False
'ファイル名の設定
strFilePath = wbMain.Path
strFileName = Dir(strFilePath + "\*" + strExtension)
strFileFullPath = strFilePath + "\" + strFileName

'========================================
' メイン処理
'========================================
Do While strFileName <> ""

    'ファイル名の確認
    If strFileName <> wbMain.Name Then
        'ファイルオープン
        Workbooks.Open (strFileFullPath)
        'アクティブブックの設定
        Set wbOpen = ActiveWorkbook
        'アクティブシートの設定
        Set wsOpen = wbOpen.ActiveSheet
        'デバッグ用
        Debug.Print (strFileName)
        Debug.Print (wsOpen.Cells(1, 1))
        Debug.Print (wsOpen.Range("A1"))
        'マクロシートに書き込み
        'wsMain.Range("A1") = wsOpen.Range("A1")
        'ファイルクローズ
        Workbooks(strFileName).Close SaveChanges:=False
    End If
    
    '次のファイル名を取得
    strFileName = Dir()
    strFileFullPath = strFilePath + "\" + strFileName

Loop

End Sub
```

<br>
