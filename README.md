# ansible

A collection of roles I use to manage project configuration and deployment

## Setup

```sh
uv run --python 3.12 --with-requirements requirements.txt ansible-galaxy collection install -r requirements.yml -p collections
```

## Run

```sh
uv run --python 3.12 --with-requirements requirements.txt ansible-playbook playbooks/personal_website.yml -u root
```
