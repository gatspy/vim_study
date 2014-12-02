# Vim学习 #
## 个人学习vim笔记 ##
### 一、常用命令 ###
**编辑模式(Insert)和命令模式和Normal模式**
********************************
#### 编辑模式 ####
- **i** → 插入字符，进入编辑状态
- **esc**→退出*Insert*模式，返回到*Normal*模式
#### Normal模式 ####
##### 光标移动 #####
- **h**→上一列
- **l**→下一列
- **j**→下一行
- **k**→上一行
- **0**→到本行行头，数字零
- **$**→到本行行尾
- **^**→到本行第一个不是blank字符的位置（所谓blank字符就是空格，tab，换行，回车等）
- **g_**→到本行最后一个不是blank字符的位置
- **NG**→到N行，10G跳到第10行
- **gg**→到第一行
- **G**→大写G跳转到最后一行
- **w**→从当前光标位置到下一个单词的开头，不包括第一个字符
- **e**→从当前光标位置到单词的结尾，包括最后一个字符<pre>
**注意**：如果认为单词是有blank字符分隔符，那么需要用大写**E**和**W**</pre>
![事例](http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/word_moves.jpg)
- **b**→到上一个单词的开头
- **ge**→到上一个单词的结尾
- **/pattern** →顺序搜索patter字符串，如果搜索多个匹配，按n键到下一个,N上一个
- **?/pattern**→逆序搜索patter字符串，如果搜索多个匹配，按n键到下一个,N上一个,C-o跳转较旧位置，C-i跳转较新位置
- **%**→匹配括号移动，包括(,{,[
- **\*和#**→匹配光标当前所在的单词，*下一个，#上一个
- **C-f** →下一页(PgUp)
- **C-b**→上一页(PgDn)
- **C-d**→1/2页
- **H or M or L**→跳转到当前窗口顶部、中间、底部<pre>可以加数字
3H 表示跳转到距窗口顶部第3行的位置
5L 表示跳转到距窗口底部第5行的位置
</pre>
- **zt/zz/zb**→移动光标所在行到顶部、中部、底部
- **f字符**→光标移动到下一个匹配字符处<pre>
fa 表示移动到下一个为a的字符处
fs 表示移动到下一个为s的字符处
3fa 表示移动到当前行第三个a的字符处
</pre>
- **t字符**→光标移动到匹配字符前的第一个字符<pre>
t,  表示移动到逗号前的第1个字符处
t)  表示移动到括号前的第1个字符处
**dt" 表示删除所有内容，直到遇到双引号**
</pre>
- **F/T字符**→同f/t 只不过是逆序查找
- **'' or ``**→两个单引号或者两个反引号返回到最近跳转的位置 
- <pre>**''** 跳转以后光标放在第一个非空字符上
**``** 跳转以后精确到列
</pre>
- **C-O or C-I**→跳转较旧位置或者跳转较新位置<pre>
这个命令前面可以跟数字表倍数
</pre>
##### 插入字符 #####
- **i**→在光标前插入
- **I**→在光标所在行的行首前插入
- **a**→在光标后插入
- **A**→在光标所在行的行末后插入
- **o**→当前行后插入一个新行
- **O**→当前行前插入一个新行,大写O

##### 编辑操作 #####
- **r**→替换当前光标所在字符为输入的字符
- **R**→*连续*替换当前光标所在字符为输入的字符
- **s**→替换一个字符，同cl
- **S**→替换整行，并保持行前缩进，同cc
- **x**→删除当前光标所在的一个字符,同dl
- **X**→删除当前光标所在字符的前一个字符,同dh
- **C**→替换当前光标处到当前行末尾,同d$
- **D**→删除当前光标处到当前行末尾,同d$
- **cw**→替换当前光标后到一个单词结尾的字符
- **dw**→删除当前光标处到一个单字/单词的末尾
- **dd**→删除当前行，并把删除的行存到剪贴板里
- **p**→粘帖剪贴板
- **yy or Y**→拷贝当前行，相当于ddp
- **u**→撤销undo
- **U**→撤销在一行中所做的改动
- **<C-r>**→恢复redo
- **.**→重复上一次的命令(***小数点***)
- **N<command>**→重复某个命令N次
-<pre>
3dd → 删除3行
3p → 粘帖文本3次
100idesc [ESC] → 会写下“desc”100次
. → 重复上一次的命令----100"desc"
desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu
3. → 重复3次"desc"
desu desu desu
</pre>
- **：[%]s/old/new[/g][c]**→替换操作
-<pre>
:s/old/new      <回车> 在当前行替换第一个匹配的old为new
:s/old/new/g    <回车> 替换整行中匹配的old为new
:%s/old/new/g   <回车> 替换整个文件中的old为new
:%s/old/new/gc  <回车> 替换整个文件中的old,并提示是否替换
:#,#s/old/new/g <回车> 替换两行之间出现的每个old.#，#表示起始行到结束行的行号
</pre>
- **命令和对象模式 operator [number] motion**
- <pre>operator:操作符，代表要做的事情。比如d(删除)、r(替换)、c(改变)
number:可以附加的数字，代表动作重复的次数
motion:动作，代表在操作的文本上的移动，比如w(单词的词首，不包括第一个字符)，可以参考移动操作
d2w:从当前位置开始删除到2个单词的位置，2dw同
d2e:从当前位置开始删除两个单词,2de同
</pre>
#### 命令模式 ####
- **:**→进入命令输入
- **:w or write**→存盘
- **:q**→退出 
- **:q!**→强制退出,不保存文件
- **:qa!**→强制退出所有正在编辑的文件就算有修改,不保存文件
- **:wq**→存盘并退出 **:X,ZZ也是同样的功能，ZZ不需要输入:**
- **:e or edit** <path/to/file>→打开一个文件编辑
- **:saveas** <path/to/file>→另存为 <path/to/file>
- **：bn and :bp** →切换多个文件中的上一个下一个
- **:n**→跳到n行的第一个字符位置
- **:help <cli\>** →显示命名帮助
- **:！<cli\>** →执行外部命令
-<pre>:! ls
:! dir
</pre>
- **v motion :w filename**→将当前选中内容保存到文件
-<pre>v打开可视化操作，然后移动光标可以看到选择的内容
按:，可以在屏幕底部出现:'<,'>
然后输入w filename，会把选择的内容保存到filename文件中
</pre>
- **:r file/cli**→提取文件或者命令内容插入到当前光行的下一行
-<pre>:r test.txt
:r !ls
</pre>
- **: cli <TAB\>**→自动补全，也可以用C-d
- **:jumps**→查看跳转表

----------
#### 进阶操作 ####
- **<C-a> or <C-x>**→+1 和 -1操作
- **q/ or q?**→在vim窗口下打开一个新的窗口，列出查找的历史记录，可以在使用编辑命令对此窗口的内容进行编辑，然后按回车，就会对光标所在行的内容进行查找。
- **文本对象Text object 区域选择**<pre>**<action\>a<object\>** or **<action\>i<object\>**
**文本对象，简单来说就是以一定标准分隔符来标识一段文本，比如一个单词，一句话，一段话。**
action可以是任何命令：d(删除)，y(复制)，v(可视模式)
i:inner(内部); a:around(围绕)
object可能是：w一个单词，W一个以空格分割的单词，s一个句子，p一个段落，也可以是特殊字符",',),\},]
**假设你有一个字符串 (map (+) ("foo")).而光标键在第一个 o 的位置**
vi" → 会选择 foo
va" → 会选择 "foo"
vi) → 会选择 "foo"
va) → 会选择 ("foo")
v2i)→ 会选择 map (+) ("foo")
v2a)→ 会选择 (map (+) ("foo"))
</pre>

- **块操作<C-v>**<pre>**0 <C-v\> <C-d\> I-- [ESC]**
0 → 到行头
C-v → 开始块操作
C-d → 向下移动
I-- [ESC] → 在行首插入--,然后退出编辑模式
注意:window下GVIM进入可视块用[c-q]
v一般可视
V可视一行
</pre>

- **宏录制qa**<pre>**操作序列:qa,q,@a,@@**
qa:把操作记录记录在寄存器a
q :停止录制
@a:replay被录制的宏a
@@:replay最新录制的宏
实例: 只有1的文本中操作 qaYp<C-a>q
</pre>

- **:reg查看寄存器**<pre>**拷贝外部剪贴板内容到vim中**
"*p 表示从外部文件(系统剪切版)粘帖到vim，"+p相同的功能
"+y 表示从vim复制到系统剪切版(v ^ "+y 复制一行到系统剪切板)	
"+d 表示剪切
</pre>
- **mark标记 m[a-zA-Z]**<pre>**跳转使用'[a-zA-Z] or `[a-zA-Z]**
[a-z]小写字母标记缓冲区，每个缓冲区都可以定义小写字母标记，互不干扰
[A-Z]大写字母标记全局
delm[a-zA-Z] 删除指定的标记
:marks 列出所有的标记
</pre>
- **surround**

**工作路径<pwd\>**
----------------------------------------------
- **工作路径的操作**
	<pre>
	查看当前工作的路径 → :pwd
	修改工作路径 → :cd ..
	修改当前窗口工作路径 → :lcd ..
	相关配置：set autochdir: 自动设当前编辑的文件所在目录为当前工作路径
	查看当前窗口buffer文件,参考下面的窗口节--当前窗口文件：
	</pre>
**缓冲区<buffer\>**
----------------------------------------------
- buffer是啥→每个bufffer都对应着一个相应的文件，打开一个文件就有一个Buffer， 也存在不对应文件的buffer
- buffer识别→每个buffer有自己的编号和名字，名字==文件的名字
- buffer创建→创建一个buffer,可以vim a.txt或者:e b.txt
- buffer列表→命令模式输入:ls 或 :buffers 或 :files
- buffer加入→用badd命令，此命令会读取文件，并加入bufferlist
- buffer删除→命令模式:bdelete 编号或名字。bdelete a.txt
- buffer移除→bunload此命令会移除当前的buffer，并从内存删除，但是不会从bufferlist中移除
- buffer读取→当前窗口读取buffer 和 新窗口读取buffer
	<pre>当前窗口 → ctrl-^，如果当前buffer修改没有保存，就打不开你需要的buffer
	新建窗口 → sbuffer c.txt,会新建一个窗口读取需要的buffer
	</pre>
- buffer跳转→b会在当前窗口加载buffer，sb会在新窗口加载buffer
	<pre>1.跳到第一个 → bfirst 或 sbfirst 还可以用 brewind 或 sbrewind
	2.跳到下一个 → bnext 或 sbnext
	3.跳到前一个 → bNext 或 sbNext，还可以用 bprevious 或 sbprevious
	3.跳最后一个 → blast 或 sblast
	4.跳到修改的 → bmodified或:sbmodified
	</pre>
    > [Vim Buffer](http://blog.sina.com.cn/s/blog_61dfab6b0100qvgb.html "Buffer")
- 常用插件
	<pre>BufExplorer 神奇三剑
	  \be 打开bufferexplorer的窗口，：BufferExplorer
	  \bs 水平分割打开 ，这个还要按快一点，要不会进入向前替换插入模式。。有点晕
	  \bv 垂直分割打开 ，这个还要按快一点，要不会进入可视模式。。有点晕
	minibufexpl 
	</pre>
**窗口<window\>**
----------------------------------------------
- vim是多窗口的，一个页中可以有很多窗口，每个窗口可以加载不同的buff
- 启用多窗口编辑
	<pre>1.vim -on a.txt b.txt 显示水平分割的两个窗口
	2.vim -On a.txt b.txt 显示垂直分割的两个窗口
	3.上面的n数字，表示预分配窗口
	</pre>
- 窗口分割 :[n] split(vsplit)  [++opt]  [+cmd]  [file]
	<pre>n   为vim指定在新窗口中显示的行数，且新窗口的大小刚好容纳该行数，新窗口位于画面顶端
	opt  传递vim选项信息给新的窗口会话（请注意，它的前面必须加上两个加号）
	cmd 传入欲在新窗口中执行的命令（请注意，它的前面必须加上一个加号）
	file  指定在新窗口中编辑的文件
	：sview  filename  以只读的方式水平分割打开一个新窗口
	：sfind  [++opt]  [+cmd]  [file]  和split的运作方式相似，但在path中寻找filename，如果vim未找到文件则不显示
	</pre>
- 窗口跳转 Ctrl+W + [h | j | k | l]
	<pre>Ctrl + w + h：向左移动窗口
	Ctrl + w + j： 向下移动窗口
	Ctrl + w + j： 向上移动窗口
	Ctrl + w + l： 向右移动窗口
	
	Ctrl + w + w：这个命令会在所有窗口中循环移动
	Ctrl + w + t：移动到最左上角的窗口
	Ctrl + w + b：移动到最右下角的窗口
	Ctrl + w + p：移动到前一个访问的窗口
	</pre>
	> [vim 多窗口编辑 ](http://blog.csdn.net/shuangde800/article/details/11430659)
- 关闭窗口 Ctrl+W + [q | c | o]
	<pre>Ctrl + W + q：离开窗口
	Ctrl + W + c： 关闭窗口
	Ctrl + W + o： 关闭当前窗口以为的窗口
	</pre>
- 当前窗口文件 
  	<pre>echo @%
	Ctrl + G
	f / file
	</pre>
- 小技巧
	<pre>当前窗口满屏：Ctrl + W + O,有多窗口，觉得当前窗口小。
	</pre>
**分页<tab\>**
----------------------------------------------
- 分页操作
	<pre>:tabnew [filename] 打开新分页
	</pre>
- 分页跳转
	<pre>
	tabnext 移动到下一个分页，并且可以递归
	tabmove 移动到下一个分页，不能递归
	Ctrl + PgUp:移动到上一个
	Ctrl + PgDn:移动到下一个
	gt , gT 也可以切换分页tab
	</pre>
- 分页关闭
	<pre>:tabclose
	:tabonly
	</pre>
- 常用映射
	<pre>
	map < leader > tn :tabnew<cr>
	map < leader > to :tabonly<cr>
	map < leader > tc :tabclose<cr>
	map < leader > tm :tabmove
	map < leader > t < leader > :tabnext
	</pre>

##### 关于窗口，分页，缓冲的关系说明 #####
- 缓冲就是文件的映射，一个vim的实例中缓冲是共享的
- 每个分页可以有多个窗口
- 每个窗口都可以单独从缓存读取文件编辑

**折叠<folding\>**
----------------------------------------------
  **常规模式下： zR 展开全部折叠（是大写的 R） zM 全部折叠（是大写的 M）**</br>
  **我的配置里设置了用空格键折叠**

**映射<map\>**
----------------------------------------------
- **5中操作模式：**Command(Ex)、Insert、Normal、Visual、Select
	<pre>Command命令模式 输入:进入 ，Ex模式大写Q进入，状态栏会提示gq
	  **Ex其实就是多行的Command-Line模式
	Insert插入模式：i进入，esc退出
	Normal正常模式
	Visual可视模式：v c-v
	Select选择模式 鼠标拖选区域的时候进入
	</pre>
- **3种映射：map、nmap、imap、vmap、cmap**
	<pre>1.nore组合表示不递归映射
      :map a b
      :map c a
      等同map c b就是键c等同于b，如果用了nore那键c还是键c
	2.unmap组合表示删除映射
	  :unmap c 那就是键c现在没有映射
	3.mapclean表示删除相关模式下的所有映射
	  插件快捷键冲突处理
	  :nunmap < C-N >
	  :nnoremap < C-N > :NERDTreeToggle<CR>
	4.在命令模式下输入map、imap、vmap、cmap、command可以查看所有的相应模式下的键映射
	</pre>
	> [vim的几种模式和按键映射](http://haoxiang.org/2011/09/vim-modes-and-mappin/ "dsad")
- 常用映射组合 默认map命令影响到普通模式和可视模式。
	<pre>
	:map :noremap :unmap :mapclear
	:nmap :nnoremap :nunmap :nmapclear
	:vmap :vnoremap :vunmap :vmapclear
	:imap :inoremap :iunmap :imapclear
	:cmap :cnoremap :cunmap :cmapclear
	</pre>

**常用配置<VIMRC\>**
-----------------------------------------------
- **快速编辑我的配置 .vimrc or \_vimrc**
	<pre>
	" 快速修改 vimrc 文件
	if has("win32")
    	map <silent> <leader>e :e $VIM/_vimrc<cr>
	else
    	map <silent> <leader>e :e $VIM/.vimrc<cr>
	endif
	</pre>
	**linux下面:echo $VIM,如果不在home下，需要修改$VIM为$MYVIMRC**

- **配置即时生效 .vimrc or \_vimrc**
	<pre>
	"保存.vimrc文件后会自动调用新的.vimrc
	autocmd! bufwritepost _vimrc source $VIM/_vimrc
	</pre>
	
**常用插件<Other\>** scriptname命令查看
----------------------------------------------
- **ctags | cscope**
	<pre>
	ctags:   ctags –R src 
	cscope:  cscope -Rbq
	</pre>
- **taglist** 
	<pre>
	,tl
	</pre>
- **tagbar** 
	<pre>
	,tb
	</pre>
	>[vi/vim使用进阶: 使用标签(tag)文件](http://easwy.com/blog/archives/advanced-vim-skills-use-ctags-tag-file/)
	>
	[http://easwy.com/blog/archives/advanced-vim-skills-cscope/](http://easwy.com/blog/archives/advanced-vim-skills-cscope/)
	>
	[http://easwy.com/blog/archives/vim-cscope-ctags/](http://easwy.com/blog/archives/vim-cscope-ctags/)> 
	
	>[Vim编程之：tags,cscope,taglist](http://my.oschina.net/hevakelcj/blog/138950)
- **quickfix** 	
	> [vi/vim使用进阶: 剑不离手 – quickfix](http://easwy.com/blog/archives/advanced-vim-skills-quickfix-mode/)
- **ctrlp** 
	<pre>高仿sublime Ctrl + P
	命令模式:CtrlP 可以配置成自己想要的组合
		let g:ctrlp_map = ',,'
	常规模式:Ctrl + P
	新建文件:如文件new.js没找到，按Ctrl + Y 可新建这个文件，并打开
	切换匹配：Ctrl + D 默认是文件夹匹配，Ctrl+D切换到文件匹配
	切换模式：Ctrl + F 可以在buffer mru file三种切换
	多文件选择：在列表中Ctrl+j/k上下选择文件，Ctrl+Z标记，然后Ctrl+[W]+o打开
	打开为你定位：ind:n[定位到打开文件的n行] / ind:/tag[定位到打开文件的tag位置处]
	</pre>
	> [vim中的杀手级插件：CtrlP](http://zuyunfei.com/2013/08/26/vim-plugin-ctrlp/)
	> 
	> [ControlP 中文手册](http://blog.codepiano.com/pages/ctrlp-cn.dark.html)
- **airline → 美化状态条**
	<pre>这个其实不需要，但是骚人怎么能拒绝美的诱惑
	有了这个啊，我觉得powerline就是瘪三，用它就是找虐型的，反正我是各种失败沮丧。
	airline安装简单，兼容型强
	set laststatus=2
	let g:airline_theme="luna"
	let g:airline_powerline_fonts = 1//设置使用powerline字体
	set gfn=Meslo\ LG\ S\ DZ\ for\ Powerline:13 //for gvim
	此处设置字体有坑上面是linux字体写好，win字体如下
	显示git状态，需要安装vim-fugitive
	修改vimrc文件加入
	Bundle 'vim-fugitive'
	let g:airline#extensions#branch#enabled=1
	然后在vim中BundleInstall
	set guifont=Meslo_LG_S_for_Powerline:h11
	在终端terminal下还需要设置一步
	set t_Co=256
	自定义主题放在:省略各种/vim-airline/autoload/airline/themes下即可
	</pre>
	> [powerline-fonts](https://github.com/Lokaltog/powerline-fonts)
	> 
	> [aireline安装和配置](http://blog.razrlele.com/vim/)
	> [ControlP 中文手册](http://blog.codepiano.com/pages/ctrlp-cn.dark.html)
- **YouCompleteMe → 强大的自动完成**
	<pre>
	这个安装配置看着官方文档就是头都大了,看着就感觉高大上,看着那么繁复的安装配置恨不得不用了。
	安装过程：以win7x64为例，喜欢折腾受虐的下面略过吧
		看看下面这步骤，前5步要全都自己编译安装，而且win中的各种坑...真的有想撞墙的冲动。
	    	1.python2.7+是必须要安装好的，并且在系统环境变量PATH中加入python.exe所在路径
		2.需要替换libpython27.a，这步很重要。要不后面make的时候各种坑，我被折磨了好久。
		3.MinGW-w64安装，并设置环境变量,可以复制mingw32-make.exe，然后粘帖改名为make.exe
		  下载地址看下面的链接
		4.LLVM-clang安装,安装好以后也在环境变量设置下吧。
		5.CMake安装
		6.Vim-64位安装
		7.安装YCM这个没撒说的了，用VUndle或者Pathogen,看个人喜好了。
		  git clone https://github.com/Valloric/YouCompleteMe .
		  git submodule update --init --recursive
		8.替换interlocked.hpp文件，从下面路径下载
		9.修改YouCompleteMe\third_party\ycmd\cpp\CMakeLists.txt
		  在文件最后增加下面的语句
		  set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -include cmath")
		  add_definitions(-DBOOST_PYTHON_SOURCE)
		  add_definitions(-DBOOST_THREAD_BUILD_DLL)
		  add_definitions(-DMS_WIN64)
		9.然后就是编译了。。。。
		  cmake -G "MinGW Makefiles" -DPATH_TO_LLVM_ROOT=D:\Program\DevEnv\MinGW-llvm -DPYTHON_INCLUDE_DIR=D:\Program\DevEnv\Python27\include -DPYTHON_LIBRARY=D:\Program\DevEnv\Python27\libs\python27.lib . D:\tmp\YouCompleteMe\third_party\ycmd\cpp
		  make ycm_support_libs
		  遇到了各种坑...我所遇到的问题
		  cmake的时候系统环境变量里由于有cygwin的设置,sh报错。。
		  cmake的时候系统环境变量里由于有git的设置，sh报错。。。 就这两个问题就折腾了好久。
		  由于Mingw64以前安装过是4.9.1各种失败。。。又下载了3中的包重新替换mingw64的环境
		  出现错误architecture of input file `C:\Python27\libs\libpython27.a(du ks00143.o)' is incompatible with i386:x86-64 output...，按照官方提示用了2中的包替换libpython27.a
		  又出现undefined reference to `__imp__Py_NoneStruct,我的python是2.7.7，去官方下了个2.7.8安装了，然后又操作了一次2，本机最后一次操作。还是错误。。。
		  最后试了一次删除cmake中-DPYTHON_INCLUDE_DIR和-DPYTHON_LIBRARY居然成功了。。。。
		  --虚拟机中编译成功了。我就用虚拟机中的编译的包吧
		  
	</pre>
	[Python2.7.8-w64](https://www.python.org/ftp/python/2.7.8/python-2.7.8.amd64.msi)</br>
	[libpython27.a](http://www.lfd.uci.edu/%7Egohlke/pythonlibs/#libpython)</br>
	[MinGW-w64/4.8.1/x64/POSIX/SJLJ](http://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/4.8.1/threads-posix/sjlj/)</br>
	[LLVM-clang-w64](https://bitbucket.org/Haroogan/llvm-for-windows/downloads/llvm-3.4-mingw-w64-4.8.1-x64-posix-sjlj.zip)</br>
	[VIM-w64(YCM作者推荐)](https://bitbucket.org/Haroogan/vim-for-windows/downloads/vim-7.4.417-python-2.7-python-3.4-ruby-2.0.0-lua-5.2-perl-5.18-windows-x64.zip)</br>
	[VIM-w64(我个人推荐到这里下)](http://tuxproject.de/projects/vim/complete-x64.7z)</br>
	[interlocked.hpp](https://github.com/Reikion/YouCompleteMe/blob/master/cpp/BoostParts/boost/detail/interlocked.hpp)</br>
	[官方编译指导Instructions for 64-bit using MinGW64 (clang)](https://github.com/Valloric/YouCompleteMe/wiki/Windows-Installation-Guide#instructions-for-64-bit-using-mingw64-clang)
- **py-mode** 
- **jedi** 
- **mru** 