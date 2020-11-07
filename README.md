# sagemath-jupyter-setup
Notes and files to setup Debian Unstable (sid) LXD or VM with Jupyter Notebook
server for maths and data analysis

## Setup

### LXD

On laptop or desktop with limited memory, LXD is faster and more memory
efficient than VM.

For Ubuntu:

Basics for LXD documentation here:

https://ubuntu.com/server/docs/containers-lxd

`lxc launch images:debian/sid/default sagemath-jupyter`

Set password:

`lxc exec sagemath-jupyter -- passwd root`

Probably should change the mirror it /etc/apt/sources.list to a a closer
and faster repo. List of repos:

https://www.debian.org/mirror/list

### FreeBSD bhyve VM

sagemath isn't ported to work on FreeBSD yet
https://trac.sagemath.org/ticket/26249 so a VM with Debian
Sid is needed.

vm management `pkg install vm-bhyve`

https://github.com/churchers/vm-bhyve

### Installing key packages

Packages of what I use are in this debian-pkg.list

    EXPORT LC_ALL=C
    sudo xargs -a debian-pkg.list apt install

EXPORT LC_ALL is to fix issue with initial installation of texlive-base.

### Accessing Jupyter Notebook on server or LXC

Easiest way is to simply do ssh tunnel:

`ssh -L 8888:localhost:8888 <ipaddress of server> 'jupyter notebook`

If on LXD you can find the IP by doing `lxc list`

Copy and paste the url to access the notebook on your desktop browser and
you're good to go.

I usually prefer having ssh shell, using tools such as tmux and starting
`jupyter notebook` so I can use other tools on the server.

You can set it up listening to proper IP, but that are more steps
to go through.

Online documentation for this setup here:
https://jupyter-notebook.readthedocs.io/en/stable/public_server.html
