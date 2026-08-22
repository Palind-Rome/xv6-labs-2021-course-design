# xv6 Labs 2021：操作系统课程设计

这是同济大学操作系统课程设计项目。

本仓库完成 MIT 6.S081 / Fall 2021 的全部十个 xv6 实验。项目以 MIT `xv6-labs-2021` 各实验原始分支为基线，每个实验保留在同名分支中，方便独立编译、测试和答辩演示。

## 实验索引

| 顺序 | 实验 | 分支 | 主要内容 |
| --- | --- | --- | --- |
| 1 | Xv6 and Unix utilities | `util` | `sleep`、`pingpong`、素数筛、`find`、`xargs` |
| 2 | System calls | `syscall` | 系统调用跟踪、系统信息统计 |
| 3 | Page tables | `pgtbl` | USYSCALL、页表打印、访问位检测 |
| 4 | Traps | `traps` | RISC-V、栈回溯、周期性用户态 alarm |
| 5 | Copy-on-write | `cow` | COW fork、页引用计数、写时复制 |
| 6 | Multithreading | `thread` | 用户线程切换、哈希表锁、线程屏障 |
| 7 | Network driver | `net` | E1000 TX/RX 描述符环与中断并发 |
| 8 | Locks | `lock` | 每 CPU 空闲链表、低竞争块缓存 |
| 9 | File system | `fs` | 二级间接块、符号链接 |
| 10 | mmap | `mmap` | VMA、懒加载、共享回写、fork 继承 |

完整实验报告见
[docs/操作系统课程设计实验报告.md](docs/操作系统课程设计实验报告.md)。

## 环境

- Windows 11 + WSL2
- Ubuntu 24.04 LTS
- QEMU RISC-V system emulator
- `riscv64-linux-gnu-gcc`、GNU Make、Python 3

安装依赖：

```bash
sudo apt-get update
sudo apt-get install -y git build-essential gdb-multiarch qemu-system-misc \
  gcc-riscv64-linux-gnu binutils-riscv64-linux-gnu
```

## 编译、运行与测试

```bash
git clone https://github.com/Palind-Rome/xv6-labs-2021-course-design.git
cd xv6-labs-2021-course-design
git switch util                 # 替换为需要演示的实验分支
make clean
make qemu                       # Ctrl-a x 退出 QEMU
make grade                      # 运行该分支的官方评分测试
```

每个分支均可单独运行。网络实验还需在另一个终端执行 `make server`；线程实验的 `ph` 和 `barrier` 是 Linux 宿主程序，评分脚本会自动编译运行。

## 实测结果

在 Ubuntu 24.04、QEMU 8.2.2、RISC-V GCC 13.3 环境运行官方 `make grade`：

| 分支 | 结果 |
| --- | ---: |
| `util` | 100/100 |
| `syscall` | 35/35 |
| `pgtbl` | 46/46 |
| `traps` | 85/85 |
| `cow` | 110/110 |
| `thread` | 60/60 |
| `net` | 100/100 |
| `lock` | 70/70 |
| `fs` | 100/100 |
| `mmap` | 140/140 |

## 项目结构

```text
kernel/       xv6 内核、驱动和文件系统源码
user/         xv6 用户态程序与实验测试
notxv6/       宿主 Linux 上运行的线程实验
docs/         课程设计实验报告（main 分支）
grade-lab-*   MIT 官方实验评分脚本
```

## 许可

xv6 原始代码遵循仓库中的 MIT License。课程设计新增代码在同一许可下发布。
