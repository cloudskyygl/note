要想在 WSL 中使用在 Windows 定义的 PATH 中的命令，必须加 .exe 。这是因为 wsl 不会把 .exe 作为可执行文件的扩展名，而是把 .exe 作为可执行文件名称的一部分，这与 Linux 中的情况是一致的，对于 PATH 中的命令，当然要使用完整的名称。例如，使用 java.exe，而不是 java。尽管 WSL 能运行 Windows 的 .exe 可执行文件，这仍是 Linux 环境


启用Windows沙盒功能会自动打开组策略中的虚拟安全功能

因为这个是基于Hyper-V技术的，开启后会和Virtual Box或者Vmware冲突，安卓模拟器一般基于Virtual Box

所以短期内坚决禁止沙盒
