数据结构对齐是代码编译后在内存的布局与使用方式。包括三方面内容：数据对齐、数据结构填充（padding）与包入（packing）。
现代计算机一般是32比特或64比特地址对齐，如果要访问的变量没有对齐，可能会触发总线错误。
当数据小于计算机的字（word）尺寸，可能把几个数据元素放在一个字中，称为包入（packing）。