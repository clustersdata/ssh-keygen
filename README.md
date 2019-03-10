# ssh-keygen
ssh-keygen
# ssh-keygen
ssh-keygen
使用sshkey连接github等服务器
    平常使用git时因为用了https的方式，所以经常要输入密码，其实我们是可以通过这个公钥连接github git.oschina.net等服务器，这样可以省去了我们输入用户名密码这么一个步骤了。

    1.生成公钥--- ssh-keygen
    无论是什么系统要使用git，那么都需要安装git工具，这个是去官网下载，安装完成后都会有了这么一个命令--- ssh-keygen，这个命令就是用来生成公钥的，生成公钥有什么好处在前面就已经说了。

    这个命令使用是很简单的

➜  ~  ssh-keygen
    直接运行，一路确定（按回车键）就可以了，这样就生成了了公钥，需要注意的是在执行的过程中会提示你文件保存的路径，在那一个步骤你要留意这个保存的路径。

    完成后，文件保存的路径，在linux中一般是 "/home/subying/.ssh/"，windows下一般是"c:\用户\subying\.ssh\" 这里的subying是我登录的用户名，你会在里面看到一个名为'id_rsa.pub'的文件。最正确就是前面说的在生成过程中留意那个路径，如果没有留意怎么办？呵呵，再生成一次...



    2.上传到服务器(网站github\git.oschina.net等)
    生成公钥后，就是要上传到服务器了，我们常用的git服务应该在是github git.oschina.net这样的网站，那么这些网站的设置都是类似的。

    首先是找到个人设置里面，在左侧找到ssh key(ssh 公钥)这样的菜单，点击进去进行设置，下面给出github git.oschina.net的连接

    https://github.com/settings/ssh （github）

    http://git.oschina.net/profile/sshkeys  (git.oschina.net)

    设置的时候一般是设置标题和内容，标题可以自己取一个，那么内容就是刚才生成的那个id_rsa.pub文件的内容，可以用编辑器、记事本这样的工具打开，复制。

    步骤如下截图：

    3.验证是否成功    
    验证的方式就是使用命令 'ssh -T git@网站url'，那么要判断我们上面设置的github git.oschina.net，可以分别执行 'ssh -T git@github.com'  'ssh -T git@git.oschina.net' ，效果如下

 

➜  nodejs-download-website-Image git:(master) ssh -T git@github.com
The authenticity of host 'github.com (192.30.252.130)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.252.130' (RSA) to the list of known hosts.
Hi subying! You've successfully authenticated, but GitHub does not provide shell access.
➜  nodejs-download-website-Image git:(master) ssh -T git@git.oschina.net
The authenticity of host 'git.oschina.net (124.202.141.153)' can't be established.
ECDSA key fingerprint is 27:e5:d3:f7:2a:9e:eb:6c:93:cd:1f:c1:47:a3:54:b1.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'git.oschina.net,124.202.141.153' (ECDSA) to the list of known hosts.
Welcome to Git@OSC, subying!
    成功后都会看到一些欢迎的信息，比如github的'Hi subying! You've successfully authenticated'，git.oschina.net的'Welcome to Git@OSC, subying!'  这里的subying是我的账号名。



    4.将https改成ssh
    做完上面的步骤后，并不是说就可以clone都不需要输入用户名和密码了，记住的是这个是ssh的公钥，所以clone的时候要用ssh的url而不是https的url，否则你用了https的url还是需要输入用户名和密码的。

    那么如果之前已经用了https了，现在要怎么修改呢？用命令'git remote set-url origin 项目的sshurl'，比如我的就是这样'git remote set-url origin git@git.oschina.net:subying/nodejs-download-website-Image.git'，或者是直接修改了项目里面.git文件中的config文件，把https的url改成ssh的url就可以了。

