# Presenter VM

An OpenBSD VM with some tools to generate/show presentations.
Currently groff/gpresent, later on texmaker+co.

## ToDo
move manual packages to ansible
create a home/user mount (upgrades..)

## Host
````
packer build -var-file=OpenBSD-config.json OpenBSD-65.json
vagrant box add --name obsd65 packer_obsd-65-amd64_virtualbox.box
vagrant up
vagrant ssh
````

## VM
````
useradd -g 0 -m -d /home/pbuehler
pkg_add -z ghostscript--a4-no_x11
pkg_add gmake gpresent git bash
cd /home
git clone https://github.com/endriff/sam2p.git
cd sam2p
./configure --enable-gif --disable-fax --disable-zip --enable-lzw
gmake HQ='perl -x ./hq.pl' ; gmake install
cd .. ; rm -rf sam2p
su - pbuehler
git clone https://github.com/double-p/presentations
````

## Host
````
git clone https://github.com/double-p/presentations
cd BSDCan/2019
make
````
