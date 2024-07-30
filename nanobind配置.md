# 安装nanobind
使用该python命令即可安装：python -m pip install nanobind

# 配置CmakeLists
下文是主要内容，注意最后两行是关键，其决定哪些cpp文件的代码被打包成模块。  
![image](https://github.com/user-attachments/assets/dd2f1b76-1f9a-4f9f-b93b-8de499cfd518)

# cpp代码
cpp文件内部的写法如下。  
**注意**，NB_MODULE宏标记了要生成什么模块，所以第一个参数必须和CmakeLists最后几行的模块名字对应，否则找不到。  
![image](https://github.com/user-attachments/assets/212ffcbf-7a7e-41f8-a14b-5dd8d7e9deaf)

****
### 注册类成员函数
类的成员函数在注册时需要额外使用域符标记该函数。  
![image](https://github.com/user-attachments/assets/7d58b4ff-bfef-47fa-8152-fc6c081c8c39)
****

### cpp源文件位置
和cmake的CmakeLists.txt以及build文件夹在一个层级下即可。  
![image](https://github.com/user-attachments/assets/70cb2738-3a5a-4c7c-aa20-67ab11e03779)
****
或是将cpp放在文件夹中，并在CmakeLists中注明（但是该文件夹仍然需要和CmakeLists在同一目录下）。  
![image](https://github.com/user-attachments/assets/8df7cb93-5fee-42ba-90f7-1f474a322038)
![image](https://github.com/user-attachments/assets/0aeabf5e-4bde-4997-a448-be93adf48878)


# 编译配置
在cmd中进入CmakeLists.txt所在文件夹，并调用cmake -S . -B build指令。  
再调用cmake --build build指令，即可在build文件夹中打包好模块。

# 调用cpp代码
### 一般调用
**注意**，一定要进入build/Debug文件夹才能import到自己绑定的模块，否则会提示找不到。  
进入build/Debug文件夹后，import自己指定的模块，再经由模块调用即可。  
![image](https://github.com/user-attachments/assets/4ae772fa-3368-4563-81bb-b9b1df09869a)
****
### 调用类成员函数
