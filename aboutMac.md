# Mac相关

1. *permission denied*   
答：一般是权限不够，在命令行前加`sudo`即可解决  

2. *permission denied, mkdir '/Users/YaliixxG/gyl/reduxdemo/node_modules/jest-haste-map/node_modules/fsevents/build*  
答：这种是权限不够，并且是在`node_modules`这个文件夹下，这个说明是 npm 权限问题，用这个命令行解决 `npm config set unsafe-perm=true`，删掉`node_modules`，重新进行安装  

3. *permission denied, mkdir*  
答：一个文件有3种权限，读、写、可执行，你这个文件没有可执行权限，需要加上可执行权限。终端下先 cd到该文件的目录下，执行命令 `chmod a+x ./文件名`这样就可以打开该文件了