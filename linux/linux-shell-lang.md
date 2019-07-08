-b filename : 当filename 存在并且是块文件时返回真(返回0)
-c filename : 当filename 存在并且是字符文件时返回真
-d pathname : 当pathname 存在并且是一个目录时返回真
-e pathname : 当由pathname 指定的文件或目录存在时返回真
-f filename : 当filename 存在并且是正规文件时返回真
-g pathname : 当由pathname 指定的文件或目录存在并且设置了SGID 位时返回真
-h filename : 当filename 存在并且是符号链接文件时返回真 (或 -L filename)
-k pathname : 当由pathname 指定的文件或目录存在并且设置了”粘滞”位时返回真
-p filename : 当filename 存在并且是命名管道时返回真
-r pathname : 当由pathname 指定的文件或目录存在并且可读时返回真
-s filename : 当filename 存在并且文件大小大于0 时返回真
-S filename : 当filename 存在并且是socket 时返回真
-t fd : 当fd 是与终端设备相关联的文件描述符时返回真
-u pathname : 当由pathname 指定的文件或目录存在并且设置了SUID 位时返回真
-w pathname : 当由pathname 指定的文件或目录存在并且可写时返回真
-x pathname : 当由pathname 指定的文件或目录存在并且可执行时返回真
-O pathname : 当由pathname 存在并且被当前进程的有效用户id 的用户拥有时返回真(字母O 大写)
-G pathname : 当由pathname 存在并且属于当前进程的有效用户id 的用户的用户组时返回真
file1 -nt file2 : file1 比file2 新时返回真
file1 -ot file2 : file1 比file2 旧时返回真
