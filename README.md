# semantic-kernel-playground
練習用

# 環境構築

## フォーマット
version管理はpoetryで．
1. poetryをインストール
    ```
    brew install poetry
    ```
1. 仮想環境作成
    ```
    poetry init
    ```
1. フォーマットツールを追加
    ```
    poetry add --group lint black isort flake8 mypy
    ```

## push時にもフォーマット
自動整形を事前に設定したい場合（pre-commit）
```
poetry add --group dev pre-commit
```
.pre-commit-config.yaml を作成：
```
repos:
  - repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
      - id: black
  - repo: https://github.com/PyCQA/isort
    rev: 5.12.0
    hooks:
      - id: isort
  - repo: https://github.com/pycqa/flake8
    rev: 6.0.0
    hooks:
      - id: flake8
```

初期化：
```
poetry run pre-commit install
```

> [!tip]
> poetry & precommitで二重で整形する．
> poetryだけ：コミット時のコード品質が荒くなる
> pre-commitだけ：依存漏れ，環境差異がでやすい

## semantic-kernelの設定
### 必要なパッケージのインストール
```
poetry add semantic-kernel openai python-dotenv
```

> [!WARNING]
> poetryで依存関係のエラーが起きている場合
> pythonバージョンを指定する
> poetryのバージョン確認
> `poetry env info --path`
> 
> 解決策
> pyenvを入れる
> `brew instsall pyenv`
> pyenvにpythonをインストール
> `pyenv install 3.12.3`
> poetryに設定（globalはターミナル全体のデフォルトを変更）
> ```
> pyenv global 3.12.3
> poetry env use $(pyenv which python)
> ```

> [!tip]
> バージョン違いのpythonを入れてしまった場合
> ```
> # Python 3.12をインストール（済みならスキップ）
> pyenv install 3.12.3
> 
> # Poetryに明示して仮想環境を切り替える
> poetry env use $(pyenv prefix 3.12.3)/bin/python
>
> # バージョン確認
> poetry run python --version  
> ```

> [!WARNING]
> py3.13/bin/python: No module named pre_commit
> ✅ 解決策：hook を削除して再登録する
> 次のコマンドを順に実行してください：
> ```
> # ① 古い hook を削除
> rm .git/hooks/pre-commit
> 
> # ② Poetry 仮想環境に pre-commit を再インストール（必要なら）
> poetry install
> 
> # ③ 新しい仮想環境に合わせて pre-commit フックを再インストール
> poetry run pre-commit install
> ```

### 


