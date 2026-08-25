# ansible

Configuration and deployment for the personal website and other small services.

## Operate

### Setup

```sh
uv run --python 3.12 --with-requirements requirements.txt ansible-galaxy collection install -r requirements.yml -p collections
```

### Validate

Run this before opening a pull request or making a production change:

```sh
for playbook in playbooks/*.yml; do uv run --python 3.12 --with-requirements requirements.txt ansible-playbook "$playbook" --syntax-check; done
```

### Provision the website server

`playbooks/personal_website.yml` configures the operating system, node exporter,
Caddy, and website package. Use it for a new website server or a deliberate
configuration change, not for routine website releases.

```sh
uv run --python 3.12 --with-requirements requirements.txt ansible-playbook playbooks/personal_website.yml -u root
```

### Deploy a website release

Release the website from its repository first, then install the published tag
without rerunning server provisioning:

```sh
uv run --python 3.12 --with-requirements requirements.txt ansible-playbook playbooks/deploy_personal_website.yml -u root -e version=v3.0.6
```

To roll back, rerun the same command with the preceding published version.

### Verify production

```sh
curl -fsS https://jackmitchellfordyce.com/health
```

The `personal_website` inventory group identifies the active website server.
Update it only after the replacement host has been provisioned and verified.

### Notes

- Use the pinned Ansible Core and collection versions above; they support the
  current managed hosts.
- Keep Vault material, private keys, and local collection installs out of Git.
- The normal website path is: merge website changes, tag a release, deploy that
  tag with `deploy_personal_website.yml`, then check `/health`.
