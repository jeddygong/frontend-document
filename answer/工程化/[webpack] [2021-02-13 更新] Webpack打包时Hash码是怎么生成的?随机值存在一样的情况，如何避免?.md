#### 1、Hash

	##### webpack生态中存在多种计算hash 的方式:

	* hash
	* chunkhash
	* contenthash



**Hash** 代表每次webpack编译中生成的hash值，所有使用这种方式的文件hash都相同。每次构建都会使webpack计算新的hash。



**chunkhash** 基于入口文件(entry) 及其关联的chunk生成，某个文件的改动只会影响与它有关联的chunk的hash值，不会影响其他文件。



**conenthash** 根据文件内容创建。当文件内容发生变化时,contenthash发生变化。



#### 2、避免相同随机值

webpack在计算hash后分割chunk。产生相同随机值可能是因为这些文件属于同一个chunk，可以将某一个文件提 到独立的chunk (如放入entry)

