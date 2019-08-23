# Block Storage Management API
## BlockDataManager
BlockDataManager是spark storage manager的抽象接口，BlockDataManager使用blockid作为唯一识别block块数据，ManagerdBuffer来存储data，接口提供了以下方法：


| method                                                       | describe                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| getBlockData(blockId: BlockId)                               | 根据给定的blockId获取指定的BlockUsed when:NettyBlockRpcServer is requested to handle a OpenBlocks messageShuffleBlockFetcherIterator is requested to fetchLocalBlocks|
| putBlockData(    blockId: BlockId,    data: ManagedBuffer,    level: StorageLevel,    classTag: ClassTag[_]) | 使用给的的StorageLevel存储Block如果Block保存成功，返回true如果Block保存失败或者该Block已经存在，返回falseUsed exclusively when NettyBlockRpcServer is requested to handle an UploadBlock message|
| putBlockDataAsStream(    blockId: BlockId,    level: StorageLevel,    classTag: ClassTag[_]) | 存储一个作为流接收端BlockUsed exclusively when NettyBlockRpcServer is requested to receiveStream |
| releaseLock(blockId: BlockId, taskAttemptId: Option[Long])   | 释放锁：used when：TorrentBroadcast is requested to releaseLock BlockManager is requested to handleLocalReadFailure, getLocalValues, getOrElseUpdate, doPut, and releaseLockAndDispose|

## BlockId