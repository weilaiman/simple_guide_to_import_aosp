# simple_guide_to_import_aosp

1，使用国内的镜像源下载源码
1-1，这里推荐看这个网站 ， 清华的镜像 https://mirrors.tuna.tsinghua.edu.cn/help/AOSP/ 
1-2，运行
curl https://mirrors.tuna.tsinghua.edu.cn/git/git-repo -o repo
chmod +x repo
1-3，vim repo，修改一下里面的
REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo/'
备注：不修改的话会被墙
1-4，将repo加入环境变量Path,如果不加也可以，就是后面的命令用到repo的地方全部写为./repo即可

2，同步源码
2-1，运行
repo init -u https://aosp.tuna.tsinghua.edu.cn/platform/manifest -b android-4.0.1_r1
-b后面的参数是某个版本，也就是branch，比如这里要拉取的4.0.1的r1版本代码
2-2，运行
repo sync
备注：这里是拉取这个版本全部的源码，Android的一个版本的源码实在是保罗万象，啥都有，如果不是要编译ROM，只是来看framework层的内容的话（大部分是来解bug），那么运行
repo sync platform/frameworks/base 
同步framework层的代码就OK了，其实repo sync后面跟的参数是 project name，如果想知道还有那些project可以同步的，可以在.repo/manifest.xml中查看

3，使用idegen来处理project
3-1，在framework同级目录下建立 /out/host/linux-x86/framework目录
3-2，网络上下载idegen.jar，复制到/out/host/linux-86/framework下

3-3，在framework同级目录运行
repo sync platform/development
在同步代码后运行
./development/tools/idegen/idegen.sh

4, 源码导入Android Studio
4-1，上述步骤完成后framework同级目录会生成android.ipr和android.iml两个文件，使用Android Studio 在菜单中 Open -> File打开android.ipr就能自动导入整个工程了，以后看Android源码再也不求人。。