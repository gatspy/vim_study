# K-Vim及自定义快捷键 #
------------

- 插入模式下C - N自动补全下，C - P 自动补全上
- 正常模式下C - N关闭相对行号
- C - M 可以多行选择
- C - V - Tab 输入真正空格键
- gk<=>k可以分行上移 gj<=>j可以分行下移
- F2行号快关
- F3 显示可打印字符开关
- F4 换行开关
- F5 粘贴模式paste_mode开关,用于有格式的代码粘贴
- F6 语法开关，关闭语法可以加快大文件的展示
- 分屏窗口移动
	<pre>
	map < C-j > < C-W >j
	map < C-k > < C-W >k
	map < C-h > < C-W >h
	map < C-l > < C-W >l
	</pre>
- H <=> ^ 回行首 L <=> $ 到行尾
- ; <=> : 快速转到命令行
- 命令行增强模式
	<pre>
	" 命令行模式增强，ctrl - a到行首， -e 到行尾
	< C-j > < t_kd >
	< C-k > < t_ku >
	< C-a > < Home >
	< C-e > < End >
	</pre>
- 空格space <=> /,搜索自动进入正则模式
	<pre>
	去掉搜索高亮 ,/
	n搜索下一个，N搜索上一个
	n <=>  nzz
	N <=>  Nzz
	* <=>  *zz
	# <=>  #zz
	g* g*zz
	</pre>
- 正常模式下 * <=> #
- Buffer操作
	<pre>
	:b1 :b2   :bf :bl
	[b :bprevious<cr>
	b :bnext<cr>
    ← :bp<CR>
    → :bn<CR>
	</pre>
- Tab操作
	<pre>
	,th :tabfirst<cr>
	,tl :tablast<cr>
	,tj :tabnext<cr>
	,tk :tabprev<cr>
	,tn :tabnext<cr>
	,tp :tabprev<cr>
	,te :tabedit<cr>
	,td :tabclose<cr>
	,tm :tabm<cr>
	,1~9 切换到具体tab ,0 切换到最后一个
	,tt 循环切换tab
	< C - t >可以常规和插入模式下新建tab
	</pre>
- 可是模式调整缩进后自动选中
	<pre>
	< < gv
	> > gv
	</pre>
- Y <=> y$ 复制到行尾	
- ,sa <=> ggVG
- 可视模式 ,v <=> V`
- w!!  sudo & write a file
- kj <=> ESC 插入模式下
- <C-e> 2<C-e> 下滚2行，光标改变
- <C-y> 2<C-y> 上滚2行，不过光标没变
- ，q <=> q 快速关闭当前窗口
- ` and ' jump to markers 
- U <=> <C-r>
- ,ev <=> :e $MYVIMRC    edit
- ,sv <=> :so $MYVIMRC<CR> reload
- F10 run python

插件部分
--------
- YCM
	<pre>
	重启 :YcmRestartServer
	默认tab  s-tab 和自动补全冲突
	"let g:ycm_key_list_select_completion=['< c-n >']
	let g:ycm_key_list_select_completion = ['< Down >']
	"let g:ycm_key_list_previous_completion=['< c-p >']
	let g:ycm_key_list_previous_completion = ['< Up >']
	,jd GoToDefinitionElseDeclaration
	,gd GoToDeclaration
	</pre>
- 代码片段
	<pre>
	let g:UltiSnipsExpandTrigger       = "< tab >"
	let g:UltiSnipsJumpForwardTrigger  = "< tab >"
	let g:UltiSnipsJumpBackwardTrigger = "< s-tab >"
	，us :UltiSnipsEdit
	</pre>
- Raimondi/delimitMate  自动补全单引号，双引号等
- docunext/closetag.vim 自动补全html/xml标签
- scrooloose/nerdcommenter 快速注释 
- tpope/vim-surround 快速加入修改环绕字符
- vim-trailing-whitespace 快速去行尾空格 [, + <Space>]
- vim-easy-align 快速赋值语句对齐 ,a 可视和正常模式
- vim-easymotion 更高效的移动 [,, + w/fx] ,,h/j/k/l
- vim-signature 显示marks
	<pre>
	" m[a-zA-Z] add mark
	" '[a-zA-Z] go to mark
	" m<Space>  del all marks
	</pre>
- vim-textobj 文本对象
	<pre>
	" 增加行文本对象: l   dal yal cil
	" 增加文件文本对象: e   dae yae cie
	" 增加缩进文本对象: i   dai yai cii - 相同缩进属于同一块
	</pre>
- im-expand-region 快速选中
	<pre>
	map + <Plug>(expand_region_expand)
	map _ <Plug>(expand_region_shrink)
	</pre>
- vim-multiple-cursors 多光标选中编辑
	<pre>
	let g:multi_cursor_next_key='< C-m >'
	let g:multi_cursor_prev_key='< C-p >'
	let g:multi_cursor_skip_key='< C-x >'
	let g:multi_cursor_quit_key='< Esc >'
	</pre>
- CtrlP 文件搜索
	<pre>
	let g:ctrlp_map = '<leader>p'
	let g:ctrlp_cmd = 'CtrlP'
	map <leader>f :CtrlPMRU<CR>
	</pre>
- ctrlp-funky ctrlp插件-不用ctag进行函数快速跳转
	<pre>
	nnoremap <Leader>fu :CtrlPFunky<Cr>
	nnoremap <Leader>fU :execute 'CtrlPFunky ' . expand('< cword >')<Cr>
	</pre>
- git 操作直接在terminal里吧
- NERDTreeToggle 快速导航
	<pre>
	map <leader>n :NERDTreeToggle<CR>
	s/v 分屏打开文件
	</pre>
- vim-ctrlspace  Vim Workspace Controller
- TagbarToggle tag导航 F9
	
- 待续