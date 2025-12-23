# AWX Custom EE
Ansible AWX custom Execution Environment (EE)

## References

More information: https://hub.docker.com/r/ltp1120/awx-custom-ee

Note: AWX Offical EE image is based on Centos, so this repo build from scratch with centos minimal (Check out the [compatible version](https://quay.io/repository/ansible/awx-ee?tab=tags))
+ Base OS: centos/centos:stream9
+ Python version: python3.11
+ Ansible core version: ansible-core>=2.15.0rc2,<2.16
+ Ansible runner version: ansible-runner

P/s: I tried with ubuntu/debian image but it's not working, because the [builder is intentionally designed to work only with RHEL](https://github.com/ansible/ansible-builder/issues/636)

Ansible Core & Python Compatibility Table (Control Node):

| Ansible Core Version | Python Version | Note                                    |
| -------------------- | -------------- | --------------------------------------- |
| 2.15                 | 3.9 - 3.11	    | Python 3.12 is not officially supported |
| 2.16                 | 3.10 - 3.12	  | Good support on CentOS 9                |
| 2.17                 | 3.10 - 3.12    | Recommended for new systems             |
| 2.18                 | 3.11 - 3.13    | Minimum Python requirement is 3.11      |

## Prepare

```sh
apt update && apt install -y python3-pip
pip3 install ansible-builder ansible-runner
```

## Usage

Clone the source:
```
git clone https://github.com/lucthienphong1120/awx-custom-ee
cd awx-custom-ee
```

Change the environments:
+ Init environment: execution-environment.yml
+ System binary: bindep.txt
+ Python packages: requirements.txt
+ Galaxy collections: requirements.yml
+ Ansible config: ansible.cfg

Build the image:
```sh
ansible-builder build -t ansible/ee:2.15-custom -v 3
```

List images:
```sh
docker images
```

Test the image:
```sh
docker run --rm -it ansible/ee:2.15-custom bash
```

Run ansible runner on ee:
```sh
ansible-runner run --process-isolation --process-isolation-executable=docker --container-image ansible/ee:2.15-custom -p demo.yml .
```
