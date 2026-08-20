# ansible

A collection of roles I use to manage project configuration and deployment

## Setup

```sh
uv run --python 3.12 --with-requirements requirements.txt ansible-galaxy collection install -r requirements.yml -p collections
```

## Run

Provision a new server:

```sh
uv run --python 3.12 --with-requirements requirements.txt ansible-playbook playbooks/personal_website.yml -u root
```

Deploy a website release without reprovisioning the server:

```sh
uv run --python 3.12 --with-requirements requirements.txt ansible-playbook playbooks/deploy_personal_website.yml -u root -e version=v3.0.6
```
