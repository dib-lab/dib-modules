# GED modules

  Ansible playbook containing some useful modules for MSU HPCC

## Why?

  As awesome as the HPCC staff is, not all software in the world is readily
  available.

## How?

  The initial installation was done from a remote computer, not inside HPCC.
  This is needed to install anaconda and ansible. Once they are installed the
  remaining roles can be executed on one of the dev-* machines, so we don't
  overload the gateway. Also there are libraries headers missing in the gateway,
  like ncurses, and so htop and tig can't be compiled, for example.

## Ansible concepts: role, inventory, playbook

  An **inventory** is a file describing the machines where we are going
  to execute our tasks. You can use it to group machines or to set specific
  configurations.

  A **role** is a self-contained collection of tasks, templates and
  other related configurations. Here each module is implemented as a role.

  A **playbook** is a file describing which roles should be executed on
  each machine of the inventory. It also contains top-level configurations.
  This is the entry point for Ansible, where it starts finding which tasks
  to execute.

## Quick start

  Edit hosts file (our inventory) and add configuration for HPCC:

  ``` ini
  [hpcc]
  hpcc.msu.edu
  ```

  Edit site.yml (our playbook) to run anaconda and ansible roles
  (comment the others).

  Run the playbook (and wait):

  ``` bash
  $ ansible-playbook -i hosts site.yml
  ```

  Go to a dev-* machine. We need the modules we just installed, so load it:

  ``` bash
  $ module use /mnt/scratch/tg/software/modulefiles
  $ module load anaconda
  $ module load ansible
  ```

  Edit hosts file to run locally this time:

  ``` ini
  [hpcc]
  localhost ansible_connection=localhost
  ```

  Uncomment the remaining roles in the playbook. Run the playbook (and wait):

  ``` bash
  $ ansible-playbook -i hosts site.yml
  ```
