# How to create Private Debian Repository?
If you are searching for the steps to create a Private Debian Repository which can be hosted on remote server or local server using apache then you are at right place..!!

Here you go…!!

Go to archives folder in your Ubuntu machine using command

`cd /var/cache/apt/archives`

Create backup folder to take backup of current archived Debians

`mkdir backup_debian`

Move current archived Debian packages to backup folder

`mv *.deb backup_debian`

Check **/etc/apt/sources.list** should be pointing to internet debian repository

Do `apt-get update`

Check if the Debian package which you want to include in private repo is already installed in your system? If yes then first remove that package using command

`apt-get autoremove <package-name>`

Now install that package again using below command so that we can get all required debians in archives directory

`apt-get install <package-name>`

Now list current packages in archives folder using **ls -lrt**, you will be able to see all the dependent .deb files will be listed there

Now we need **reprepro** package to push this downloaded debians to private repo, so run

`apt-get install reprepro`

Now we’ll create one private debian repo folder which later will be hosted on remote server or local server

`mkdir /root/repository`

Next, create a directory called conf and a file in that directory called distributions:

`mkdir /root/repository/conf
touch /root/repository/conf/distributions`

Open the distributions file with your favorite editor. You’ll need the following configuration:

`Origin: repo.example.com 
Label: repo.example.com 

Codename: common 
Architectures: i386 amd64 
source Components: main 
Description: example repo 
SignWith: D69C3E54`

Move all the installed debians to private repo using

`reprepro -b /root/repository includedeb common *.deb`

Check **/root/repository/dists/common/main/binary-amd64/Packages** file and grep your installed package name to verify it is included in our Private Debian Repository successfully..!!

Now you can host this folder on your local server which can be further used as local Private Debian Repository by changing repo details of **/etc/apt/sources.list** file

Congratulations..!! We are done..!! Now you are ready to download your package from your Private Debian Repository hosted locally without using internet

Please comment if you need more details on /etc/apt/sources.list content and how to host apache server locally.

Thanks a lot for your time..!!

`Happy Coding…!!`
