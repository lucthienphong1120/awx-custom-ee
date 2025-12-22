# AWX Custom EE
Ansible AWX custom Execution Environment (EE)

More information: https://hub.docker.com/repository/docker/ltp1120/awx-custom-ee

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
