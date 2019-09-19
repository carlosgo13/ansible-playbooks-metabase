# nephelaiio.playbooks-metabase

[![Build Status](https://travis-ci.org/nephelaiio/ansible-playbooks-metabase.svg?branch=master)](https://travis-ci.org/nephelaiio/ansible-playbooks-metabase)

Ansible playbook to install [Metabase](https://metabase.com)

## Playbook descriptions

The following lists the group targets and descriptions for every playbook

| playbook     | description         | target       |
| ---          | ---                 | ---          |
| metabase.yml | deploy metabase app | metabase_app |
| postgres.yml | deploy metabase db  | metbase_db   |

## Playbook variables

The following parameters are available/required for playbook invocation

### [metabase.yml](metabase.yml):
| required | variable                       | description                            | default                              |
| ---      | ---                            | ---                                    | ---                                  |
| no       | metabase_app_tag               | metabase container tag                 | v0.33.2                              |
| no       | metabase_app_container         | metabase container name                | metabase                             |
| *yes*    | metabase_db_pass               | metabase db access password            | no                                   |
| no       | metabase_db_user               | metabase db access username            | metabase                             |
| no       | metabase_db_name               | metabase db name                       | metabase                             |
| no       | metabase_db_host               | metabase db access host                | "{{ ansible_default_ipv4.address }}" |
| no       | metabase_db_port               | metabase db access port                | 5432                                 |
| no       | metabase_maxmem_mb             | maximum memory for metabase container  | "{{ ansible_memtotal_mb - 1024 }}M"  |
| no       | metabase_encryption_secret_key | metabase credential encryption key (*) | n/a                                  |

(*) See [credential encryption](https://metabase.com/docs/v0.33.0/operations-guide/encrypting-database-details-at-rest.html) documentation for more details

### [postgresql.yml](postgresql.yml):
| required | variable         | description                 | default                              |
| ---      | ---              | ---                         | ---                                  |
| *yes*    | metabase_db_pass | metabase db access password | no                                   |
| no       | metabase_db_user | metabase db access username | metabase                             |
| no       | metabase_db_name | metabase db name            | metabase                             |
| no       | metabase_db_host | metabase db access host     | "{{ ansible_default_ipv4.address }}" |
| no       | metabase_db_port | metabase db access port     | 5432                                 |

## Dependencies

This playbook has the following git submodule dependencies:

* [plugins/mitogen](https://github.com/dw/mitogen)

## Example Invocation

```
git checkout https://galaxy.ansible.com/nephelaiio/ansible-playbooks-metabase metabase
ansible-playbook -i inventory/ metabase/upgrade.yml
```

## License

This project is licensed under the terms of the [MIT License](/LICENSE)
