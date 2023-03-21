# ansible.nf-pipeline-watcher

This playbook setups the Nextflow Watcher script (`link`) and installs the following dependencies for running the pipeline:

Nextflow 20.11.0-edge
Docker 5:20.10.14~3-0~ubuntu-focal
Go 1.17.8
Singularity v3.9.7

It is designed to run on a clean Ubuntu 20.04 server (i.e. a server on which nextflow etc. have not yet been installed).

This repo also contains a GitHub Actions workflow which tests the playbook.

## Install instructions

Install ansible

```
sudo apt update
sudo apt install ansible
```

Clone the repository

```
git clone repository
```

Run the playbook

```
cd ansible.nf-pipeline-watcher
ansible-playbook playbook.yml
```

## Updating software versions
The versions for the installed software are found in `ansible.nf-pipeline-watcher/roles/nf-pipeline-watcher/defaults/main.yml`. 
These can be updated. When updates are made to the playbook, a new GitHub Actions run is triggered.

To check for the latest versions of Nextflow look [here](https://github.com/nextflow-io/nextflow/releases)

Versions of Singularity can be found [here](https://github.com/sylabs/singularity/releases). 
The release notes should suggest which version of Go to use.
Note that Singularity is end of life and will be replaced with [Apptainer](https://github.com/apptainer/apptainer)

A list of the latest versions of Docker can be found [here](https://docs.docker.com/engine/release-notes/). 
To update the version in the ansible you'll have to use the following format `5:VERSION-NO-HERE~3-0~ubuntu-focal`


## GitHub Actions Run
Everytime a commit is made to master branch, this triggers a run of the GitHub Actions workflow found in 
`ansible.nf-pipeline-watcher/.github/workflows/main.yml`.

This workflow tests the ansible playbook by running it on a GitHub Actions hosted server. The OS of the server is set in `ansible.nf-pipeline-watcher/.github/workflows/main.yml` in the following line:

```
runs-on: ubuntu-20.04
```
https://github.com/annacprice/ansible.nf-pipeline-watcher/blob/23e7deb0283a5c394821cc84e568118695d7d7f7/.github/workflows/main.yml#L13

This can be changed to another Ubuntu environment e.g. `ubuntu-18.04` (note that if you do this, you'll have to update the Docker version to match the OS
and that this playbook can only run on Ubuntu servers). 

More information on GitHub environments can be found [here](https://github.com/actions/virtual-environments).

If the GitHub Actions workflow run is successful, you'll see a green tick next to the commit, failed runs show a red cross.
You can also check the badge at the top of the README for the build status.
To investigate a failed run, look under the Actions tab at the top of the page for more information, 
then click on the failed run and then click build.
The workflow can also be manually run through the Actions tab.