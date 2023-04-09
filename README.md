# Software Design 2023年6月号 ansible-playbook

このレポジトリは`Software Design 2023年6月号`の`Ansible現場を支えるPlaybook`で紹介されているPlaybookのサンプルが配置されています。

## 概要

ISO KickstartによるVM自動インストール Ansible Playbook

## ディレクトリの説明

```bash
.
├── collections
│   └── requirements.yml  # Playbookで利用するAnsible Collection一覧
├── requirements.txt  # Playbookで利用するPythonモジュール一覧
├── inventory
│   ├── group_vars
│   │   └── vcenter.yml  # vCenterへの接続情報
│   ├── host_vars
│   │   └── localhost.yml  # 明示的なlocalhost情報
│   └── hosts.yml  # インベントリファイル
├── prepare_ks.yml  # 1. Kickstart用ISOファイルの作成・配置 Playbook
├── create_vm.yml  # 2. OS自動インストール Playbook
├── templates
│   └── ks.cfg.j2  # Kickstartファイルのテンプレート
└── vars
    └── parameters.yml  # VM構築時のパラメータ一覧
```

## Playbook実行前準備

1. vCenterの接続情報を`inventory/group_vars/vcenter.yml`に記載する

2. Pythonモジュールインストール

    ```bash
    pip install -r requirements.txt
    ```

3. Ansible Collection インストール

    ```bash
    ansible-galaxy collection install -r collections/requirements.yml
    ```

4. VM構築で利用するパラメータを`vars/parameters.yml`に記載

## Playbook実行

下記コマンドを実行

```bash
ansible-playbook -i inventory prepare_ks.yml
ansible-playbook -i inventory create_vm.yml
```
