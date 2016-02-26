# SCM

Ansible role to provision SCM repositories.
It can be used to set up e.g. a local development machine with houndreds of repositories.


## Requirements

This role uses task includes with *with_* loops.
Therefor, ansible 2.0 or newer is required.


## Role Variables

### repo_list

A list of repositories.
Each item needs to have the following keys:

* **url**: Protocol address of the git/hg repository..
* **dest**: Absolute path of where the repository should be checked out to.
* **type** (*optional*): Type of the repository. Can be either *git* (default) or *hg*.


### repo_root

The root folder in which rpositories are cloned.


### user_email

The email address for the repository author when adding commits.

### user_name

The user name for the repository author when adding commits.


### git_force_update

If *no* (default), do not retrieve new revisions from the origin repository.


### hg_force_update

If *no* (default), do not retrieve new revisions from the origin repository


## Dependencies

This role has no dependencies.

## Example Playbook

This role can be used to set up repositories for local development, e.g. for different customers:

    - hosts: localhost
      connection: local
      gather_facts: false

      roles:
        - role: scm
          user_email: 'yourname@example-customer.com'
          user_name: 'Your Name'
          repo_root: '/home/user/development/customer1'
          repo_list:
            - url: 'git@bitbucket.org:customer1/repo1.git'
              dest: 'project_1/repo1'

            - url: git@github.com:customer1/repo2.git
              dest: project_2/repo2

            - url: ssh://hg@bitbucket.org/customer1/repo3
              dest: project_1/repo3
              type: hg

        - role: scm
          user_email: 'yourname@another-customer.com'
          user_name: 'Your Name'
          repo_root: '/home/user/development/customer2'
          repo_list:
            - url: 'git@bitbucket.org:customer2/project.git'
              dest: 'project'


## License

MIT
