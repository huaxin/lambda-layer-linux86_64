# lambda-layer-linux86_64

Install python 3.11 docker image:
docker pull dockerproxy.com/library/python:3.11

Run the docker image, install the libraries you expected and pack in a package
docker run -it dockerproxy.com/library/python:3.11 /bin/bash
root@aca036f0134b:/layer# python --version
Python 3.11.0
root@aca036f0134b:/layer# pip --version
pip 23.0.1 from /usr/local/lib/python3.11/site-packages/pip (python 3.11)
root@aca036f0134b:/# mkdir layer/python
root@aca036f0134b:/# cd layer
root@aca036f0134b:/layer# pip install --platform manylinux2014_x86_64 --implementation cp --python-version 3.11 --only-binary=:all: --upgrade --target python psycopg2_binary cryptography paramiko six
root@aca036f0134b:/layer# cd python
root@aca036f0134b:/layer/python# rm -r *dist-info __pycache__
root@aca036f0134b:/layer/python# ls -lta
total 1116
drwxr-xr-x 10 root root    4096 Oct 13 03:08 .
drwxr-xr-x  3 root root    4096 Oct 13 03:06 paramiko
drwxr-xr-x  5 root root    4096 Oct 13 03:06 cryptography
drwxr-xr-x  5 root root    4096 Oct 13 03:06 nacl
drwxr-xr-x  3 root root    4096 Oct 13 03:06 cffi
-rwxr-xr-x  1 root root 1064368 Oct 13 03:06 _cffi_backend.cpython-311-x86_64-linux-gnu.so
drwxr-xr-x  3 root root    4096 Oct 13 03:06 bcrypt
drwxr-xr-x  3 root root    4096 Oct 13 03:06 psycopg2
drwxr-xr-x  2 root root    4096 Oct 13 03:06 psycopg2_binary.libs
drwxr-xr-x  4 root root    4096 Oct 13 03:06 pycparser
-rw-r--r--  1 root root   34549 Oct 13 03:06 six.py
drwxr-xr-x  4 root root    4096 Oct 13 03:00 ..
root@aca036f0134b:/layer/python# tar -zcvf ../python.tar.gz .

Open a new command
docker ps -a
CONTAINER ID   IMAGE                                   COMMAND                   CREATED          STATUS                        PORTS     NAMES
aca036f0134b   dockerproxy.com/library/python          "/bin/bash"               27 minutes ago   Up 27 minutes                           amazing_ishizaka

docker cp aca036f0134b:/layer/python.tar.gz C:/Users/<userid>/
