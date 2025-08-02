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
s

