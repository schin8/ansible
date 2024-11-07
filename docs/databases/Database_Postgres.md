# Postgres

## setup_postgres.yml

### Directory

```text
.
└─── playbooks
│	  └─ db
│	  	 └─ setup_postgres.yml
├── inventory
│   └─ lower.yml
├── vault
│		└─ encrypt.enc
└─── ansible.cfg  	 
	  	 
```


```mermaid
graph LR
    A[setup_postgres.yml] -->|check| B[ansible.cfg]
    B -->|Points to| C[inventory/]
    C -->|contains| C1[lower.yml]
    A -->|decrypts\nvars using| D[vault/]
    D  -->|contains| D1[encrypt.enc]

```

#### Example

```
ansible-playbook playbooks/db/setup_postgres.yml -e @vault/db_lower.enc --ask-vault-pass
```

follow up by running `create_pg_dbs.yml` to create the databases and users.
