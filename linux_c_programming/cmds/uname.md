# uname

```bash
uname [OPTION]..
```

打印某些系统信息， 如果没有选项，则与`-s`相同。

| 选项                          | 释义                            | 例子                                             |
| --------------------------- | ----------------------------- | ---------------------------------------------- |
| `-a`, `--all`               | 按以下顺序打印所有信息，忽略`-p`和`-i`（如果未知） | 略                                              |
| `-s`, `--kernel-name`       | 打印内核名称                        | Linux                                          |
| `-n`, `--nodename`          | 打印网络节点主机名                     | 主机名                                            |
| `-r`, `--kernel-release`    | 打印内核版本                        | 3.10.0-1127.19.1.el7.x86_64<br>4.19.0-13-amd64 |
| `-m`, `--machine`           | 打印机器硬件名称                      | x86_64                                         |
| `-p`, `--processor`         | 打印处理器类型（非便携式）                 | x86_64<br>unknown                              |
| `-i`, `--hardware-platform` | 打印硬件平台（不可移植）                  | x86_64<br>unknown                              |
| `-o`, `--operating-system`  | 打印操作系统                        | GNU/Linux                                      |
