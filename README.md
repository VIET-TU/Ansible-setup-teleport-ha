# Cài đặt ansible:

- Server: ubuntu
```bash
# Install Ansible via pip
sudo apt install -y python3-pip
python3 --version
sudo pip3 install ansible
```

**Lưu ý**: phài cài python trển server agent, nếu python trên server agent quá cũ thì phải cài bản mới hơn ví dụ 3.10.12
- Cài python trển server agent nếu python quá cũ (Centos)

```bash
sudo yum update -y
sudo yum groupinstall -y "Development Tools"

sudo yum install -y gcc gcc-c++ make \
    zlib-devel bzip2 bzip2-devel readline-devel \
    sqlite sqlite-devel openssl-devel tk-devel \
    libffi-devel xz-devel wget

cd /usr/src
sudo wget https://www.python.org/ftp/python/3.10.12/Python-3.10.12.tgz

sudo tar xzf Python-3.10.12.tgz
cd Python-3.10.12
sudo ./configure --enable-optimizations
sudo make -j$(nproc)
sudo make altinstall

python3 --version
```

**Lưu ý**: nhớ add hosts domain: teleport.gtsc.vn trên từng server

# Lệnh chạy ansible
```bash
# setup etcd
ansible-playbook -i inventory.ini etcd-config.yml 

# setup teleport role proxy,auth,node
ansible-playbook -i inventory.ini teleport_service_auth_proxy-config.yml 

# setup teleport node
ansible-playbook -i inventory.ini teleport_agent.yml 
```