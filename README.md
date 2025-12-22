# AWX Custom EE
Ansible AWX custom Execution Environment (EE)

More information: https://hub.docker.com/repository/docker/ltp1120/awx-custom-ee

## Prepare

```sh
pip3 install ansible-builder
git clone https://github.com/lucthienphong1120/awx-custom-ee
cd awx-custom-ee
```

## Usage

Build image:
```sh
ansible-builder build -t ansible/ee:2.15-custom -v 3
```

List image:
```sh
docker images
```

Test image:
```sh
docker run --rm -it ansible/ee:2.15-custom bash
```
