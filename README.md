# LicenseTxtGenerator

- LicenseTxtGeneratorは、ユーザの環境にインストールされたPythonパッケージを読み取り、ライセンス情報として出力するスクリプトです。
- LicenseTxtGeneratorで出力されたライセンス情報は、GitHub等で用いられる*LICENSE.txt*として公開されることを想定しています。

## 開発環境

- Windows 11
- Python 3.10.6
- venv
- pip
- VSCode
- PEP8

## 環境構築方法

- 仮想環境:

```sh
# 仮想環境構築
python -m venv .env

# 仮想環境起動
.\.env\Scripts\activate

# pip更新
python.exe -m pip install --upgrade pip

# Python依存パッケージのインストール(初回のみ)
pip install -r requirements.txt

# 仮想環境終了(仮想環境内で)
deactivate
```

- ディレクトリ構造:

```txt
./
├─📁.env
│　├─📁Scripts
│　│　├─📄activate.bat  👈仮想環境起動バッチ
│　│　└─📄deactivate.bat  👈仮想環境終了バッチ
│　└─📄*.*  👈その他仮想環境設定ファイル
├─🐍*.py  👈Pythonソースコード
├─📄.flake8.py  👈flake8設定ファイル
├─📄LICENSE.json  👈入力ファイル
├─📄LICENSE.meta.json  👈特殊入力ファイル
├─⚖LICENSE.txt  👈ライセンス情報ファイル
└─📄requirements.txt  👈依存ライブラリ
```

## 動作仕様

- LicenseTxtGeneratorは、環境にインストールされているPythonパッケージを読み取り、「入力ファイル」として出力します。
- その後、入力ファイルを改めて読み取り、Requirementファイル(一般的に*requirements.txt*と呼ばれているものです)との整合性をチェックします。
- 整合性に問題があるファイルがあった場合、それらのファイルを警告として標準出力します。
- 入力ファイルの内容に基づき、既定のフォーマットでパッケージのライセンス情報を「出力ファイル」として出力します。
- LicenseTxtGeneratorは、環境にインストールされているPythonパッケージの読み取りにサードパーティライブラリとしてpip-licensesを利用しています。しかしながら、pip-licensesは自分自信の依存パッケージを出力しません。そのため、LicenseTxtGeneratorでは自信のメンテナンス用に「特殊入力ファイル」が用意されています。特殊入力ファイルには、pip-licensesの依存パッケージのライセンス情報が定義されています。この内容は、通常の入力ファイルの内容と実行時に結合され、一連のデータとして扱われます。

## 使用方法

1. 以下を実行。

```sh
# 仮想環境内で
python main.py
```

2. *LICENSE.txt*ファイルが出力されます。
3. main.pyには、*gen-license-txt*の動作を制御する引数を渡すことが出来ます。

| 引数名 | ショートハンド | 型 | 説明 |
| -- | -- | -- | -- |
| `--python` | `-p` | 文字列 | 対象とする環境のPythonまでのパス。*python.exe*までのパス。 | 
| `--requirement` | `-r` | 文字列 | Requirementファイルまでのパス。 |
| `--license` | `-l` | 配列(文字列) | 対象のライセンス。MIT,BSDなど。スペース区切りで渡す。 |
