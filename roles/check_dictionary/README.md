## Author

Gloria Requena

## Repo URL 
 
 [ans_ibe_linux_r_check_dictionary][ans_ibe_linux_r_check_dictionary] 
 
[ans_ibe_linux_r_check_dictionary]: https://github.com/grequenar/jekyll_automation/tree/master/roles/check_dictionary
 
## Description 
 
Ansible role that validates the format of the values assigned to the keys of each item of a yaml dictionary. 

| Key | Description | Accepted format |
| -------- | -------- | ------- |
| `Name`  | Name of the ansible artifact according to the accepted name convention | `ans_country_group_type_name ` |
| `Title` | Title of the post that will be created on the site | [10,50] characters |
| `Author`| Identification of the person that has developed the artifact | First and last name OR email address|
| `Repository` | URL of the repository that contains the files of the ansible artifact that is being documented | starts with `https://` |
| `Short_description` | Brief explanation of the purpose of the ansible artifact | [25,500] characters |
| `Tags` | Key words that summarize important aspects of the artifact | separated by `,` |
| `Date` | Date of when the dictionary entry was created | `YYYY-MM-DD` |
 
## Requirements

None

## Role Variables

| Variable | Required | Default | Comments |
| -------- | -------- | ------- | -------- |
| `dict_file` | Yes | `ans_doc_dictionary_correct.yml ` | dictionary file that will be validated. This variables is only necessary for POC purposes, to show the different outcome with a correct/incorrect dictionary. It will be passed at runtime |

Other variables whose value is set during the execution:
- `resultado`: array that concatenates the result of the format errors found in the dictionary entries

## Date 
 
2021-01-07

## Tags

RHEL8

## Examples 

```yaml
- hosts: localhost
  connection: local
 
  tasks:
  - include_vars:
      file: "{{ dict_path }}/{{ dict_file }}"

  - include_role:
      name: roles/check_dictionary

  - assert:
      that: not resultado
      success_msg: "The result of the format validation is correct."
      fail_msg: "The result of the format validation is incorrect. The following errors were found:\n {{ resultado }}"

```

