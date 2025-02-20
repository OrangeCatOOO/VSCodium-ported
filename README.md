## Feature 特点  
* 解压即用,无需配置环境变量
* 集成 C/C++
* 集成 Python

## Install 安装方法
1. 下载压缩包，其中后缀中含有py的为安装了python环境的VSCodium，含有C的为安装了C环境的VScodium。
通过网盘分享的文件：VSCodium绿色版
链接: https://pan.baidu.com/s/194i8lXtTzlXBmviuAlre8Q
提取码: vva4
3. 解压缩(非中文目录)  
4. 中文版直接运行启动.bat 英文版运行Start.bat（中英文的差距主要在VSCodium中是否安装了简体中文插件）  
5. 关于中英文语言的切换：如果下载的是中文版，则已经安装好了简体中文插件，否则需要在VSCodium左侧的插件商店中下载简体中文插件。
（插件商店为VScodium左侧的小图标的第五个）
6. 在VSCodium中使用（Ctrl+Shift+P）快捷键 打开命令面板。
7. 在命令面板中，输入Configure Display Language，选择Configure Display Language命令，显示已安装的语言包列表。
8. 在已安装的语言包列表中选择需要切换的语言包。


## Hello World 测试
1. 打开VSCode,点击左侧文件标志,打开文件夹,(!注意,VSCode只支持文件夹下构建程序,从VC6.0过渡过来的需要适应一下!)  
2. 新建 `test.c` 文件,键入 `hello world` 代码  
(!注意,VSCodium跟某些IDE不同,生成的exe不会出现"Press any key to continue",需要手动加 `getchar()` 或 `system("pause")`!不然会导致输出的命令框一闪而逝)
3. 按F5调试,目的是生成 `launch.json` 文件  

然后将生成的 `launch.json` 文件代码删除,换成下面的并保存  
```json
{
"version": "0.2.0",
"configurations": [
    {
        "name": "C++ Launch",
        "preLaunchTask": "build",
        "type": "cppdbg",
        "request": "launch",
        "program": "${fileDirname}/${fileBasenameNoExtension}.exe",
        "args": [],
        "stopAtEntry": false,
        "cwd": "${fileDirname}",
        "environment": [],
        "externalConsole": true,
        "MIMode": "gdb",
        "miDebuggerPath": ".\\.portable\\mingw64\\bin\\gdb.exe",
        "setupCommands": [
            {
                "description": "Enable pretty-printing for gdb",
                "text": "-enable-pretty-printing",
                "ignoreFailures": true
            }
        ]
    }]
}
```  
4. 按F5调试,此时肯定会报错,打开新生成的 `tasks.json` 文件  
将生成的 `tasks.json` 文件代码删除,换成下面的并保存  
```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build",
            "type": "shell",
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "presentation": {
                "echo": true,
                "reveal": "always",
                "focus": false,
                "panel": "shared"
            },
            "windows": {
                "command": "g++",
                "args": [
                    "-ggdb",
                    "\"${file}\"",
                    "--std=c++11",
                    "-o",
                    "\"${fileDirname}\\${fileBasenameNoExtension}.exe\""
                ]
            }
        }
    ]
}
```  
5. 此时再按下F5,即可看到程序成功运行  


## Reference 参考文献
Github_ID:DIOLeo https://github.com/DIOLeo/VSCode-Portable?tab=readme-ov-file
