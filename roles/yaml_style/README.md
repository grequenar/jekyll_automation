## Author

Gloria Requena

## Repo URL 
 
 [ans_ibe_linux_r_yaml_style][ans_ibe_linux_r_yaml_style] 
 
[ans_ibe_linux_r_yaml_style]: https://github.com/grequenar/jekyll_automation/tree/master/roles/yaml_style
 
## Description 
 
Ansible role that validates yaml rules against the .yml, .yaml files contained in a specific directory. 

The rules are:
 
## Requirements

None

## Role Variables

| Variable | Required | Default | Comments |
| -------- | -------- | ------- | -------- |
| `dir_style_check` | Yes | ` ` | Set as extra var during runtime the path of the directory where the search of yaml files will be performed |

Other variables whose value is set during the execution:
- `files_list_yml`: array with the paths of the yaml files found in the directory. 
- `resultado`: array that concatenates the result of the specified yamllint and ansible-lint executions. This variables is obtained by looping over the elements of `files_list_yml`

## Date 
 
2021-01-04

## Tags

RHEL8

## Examples 

```yaml
- hosts: localhost
  connection: local

  tasks:
  - find:
      paths: "{{ dir_style_check }}"
      recurse: true
      patterns: '*.yml,*.yaml'
    register: files_list_yml

  - include_role:
      name: roles/yaml_style

  - assert:
      that: not resultado
      success_msg: "The result of the style validation is correct. No errors found."
     fail_msg: "The result of the style validation is incorrect. The following errors were found:\n {{ resultado }}"
```

