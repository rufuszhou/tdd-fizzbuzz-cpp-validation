## Kata介绍
1. 通过文本文件向应用程序提供输入数据 testData.txt (`resource/testData.txt`)。
2. 在 `main.cpp` 中**集成**你自己所写的代码，并将结果打印至标准输出(`stdout`)。
    * 你写的程序将把输入数据文件作为参数, 加载此文件并读取文件内的测试数据，并对每行测试数据计算结果。
    * 将所有计费结果拼接并使用 `\n` 分行，然后输出至标准输出。
3. 请把你的代码逻辑写在 `src` 目录中，单元测试代码写在 `unit_test` 目录下，充分做好单元测试。
4. 你可以添加若干个文件至`src`目录中，头文件后缀名请使用`.h`, c++文件后缀名请使用`.cpp`。
5. 你可以添加相应的单元测试文件至`unit_test`目录中，文件后缀名的要求与上相同。添加单元测试后可以删除`dummy_test.cpp`。单元测试使用[googletest](https://github.com/google/googletest)框架。
6. 请不要修改源文件之外的文件，包括`CMakeLists.txt`，`cmake`目录下文件及`.devcontainer`目录下等文件。
7. 支持使用`C++98`, `C++11`, `C++14`或`C++17`。

### FizzBuzz需求：

这是一个简单的猜数字游戏。

想象你是个小学5年级的学生，现在还有5分钟就要下课，数学老师带全班同学玩一个小游戏。他会用手指挨个指向每个学生，被指着的学生就要依次报数:第一个被指着的学生说“1”，第二个被指着的学生说“2”，以此类推。

呃......并不完全“以此类推”......如果一个学生被指着的时候，应该报的数是3的倍数，那么他就不能说这个数，而是要说“Fizz”。同样的道理，5的倍数也不能被说出来，而是要说“Buzz”。

于是游戏开始了，老师的手指向一个同学，他们开心地喊 着:“1!”，“2!”，“Fizz!”，“4!”，“Buzz!”......终于，老师指向了你，时间仿佛静止，你的嘴发干，你的掌心在出汗，你仔细计算，然后终于喊出“Fizz!”。运气不错，你躲过了一劫，游戏继续进行。

为了避免在自己这儿失败，我们想了一个作弊的法子: 最好能提前把整个列表打印出来，这样就知道到我这儿的时候该说什么了。

任务: 写一个程序，输入一个大于0的整数，如果是3的倍数替换成“Fizz”，5的倍数替换成“Buzz”，既能被3整除、又能被5整除的数则替换成“FizzBuzz”，否则输出该数字本身。

### 测试数据：

`\n`为文件中的不可见的换行字符

```text
1\n
2\n
3\n
4\n
5\n
6\n
7\n
8\n
9\n
10\n
11\n
12\n
13\n
14\n
15\n
16
```
### 期望输出：

`\n`为console输出中的不可见的换行字符

```text
1\n
2\n
Fizz\n
4\n
Buzz\n
Fizz\n
7\n
8\n
Fizz\n
Buzz\n
11\n
Fizz\n
13\n
14\n
FizzBuzz\n
16\n
```
### 开始考试

#### Windows下基于MinGW64搭建开发环境

1. 安装
下载[MSYS2](https://www.msys2.org/)，建议选择64位的版本。安装路径选择默认选项`C:\msys64\`  
*如果选择32位的版本，下面的命令中也都需要相应选择32位的版本*

2. 安装所需工具
- 等待安装完成后，进入`C:\msys64`，点击`mingw64.exe`启动命令行
- 执行`pacman -Syu`
看到提示:: Proceed with installation? [Y/n]后回车，等待命令执行完后，看到如下提示后关闭命令行窗口
```
warning: terminate MSYS2 without returning to shell and check for updates again
warning: for example close your terminal window instead of calling exit
```
- 点击`mingw64.exe`重新打开
- `pacman -Su`，看到提示`:: Proceed with installation? [Y/n]` 回车，等待命令执行完毕。
- `pacman -S mingw-w64-x86_64-gtest mingw-w64-x86_64-toolchain  mingw-w64-x86_64-cmake mingw-w64-x86_64-cotire mingw-w64-x86_64-extra-cmake-modules git  mingw-w64-x86_64-python-pip mingw-w64-x86_64-python mingw-w64-x86_64-gcc mingw-w64-x86_64-libxml2 mingw-w64-x86_64-lcov mingw-w64-x86_64-python-lxml`
看到提示:: Proceed with installation? [Y/n] 回车
- `pip install cpplint gcovr`

#### 编译命令
**编译**： 
```
mkdir build
cd build
cmake ..
mingw32-make
```
注意： **编译过程中已经集成了cpplint对代码风格的检测，如果代码风格不符合要求，编译将中止。**

**运行单元测试**：
```
cd  build
mingw32-make test
```

**运行单元测试并得到代码覆盖率**：
```
cd build
mingw32-make unit_test_coverage
```

1. 点击`开始考试`。
2. 下载考题模板并解压，重命名为`tdd-fizbuzz-cpp`。
3. `cd tdd-fizzbuzz-cpp`。
4. `git init`。
5. `git remote add origin <github自有仓库>`。
6. `git add .`。
7. `git commit -m "Initial commit"`。
8. `git push -u origin master`。
9. 接着答题。
10. 本地验证无误后，push到远程仓库，并将git地址提交到科举。
11. 提交之后等待科举出考试结果。

### 考试通过的标准

1. 在规定考试时间内完成答题，并完成所有需求。
2. 测试覆盖率100%，没有严重的Sonar问题。
3. 采用TDD开发模式。

