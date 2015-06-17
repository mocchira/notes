# LeoFS 
## LeoFS fundamentals
* [What kind of storage is LeoFS?](contents/what-kind-of-storage-is-leofs.md)
* [What is benefit for LeoFS users?](contents/what-is-benefit-for-leofs-users.md)
* [What are typical uses for LeoFS?](contents/what-are-typical-uses-for-leofs.md)
* [What is architecture of LeoFS?](contents/what-is-architecture-of-leofs.md)
* [Is there the roadmap of LeoFS?](contents/is-there-the-roadmap-of-leofs.md)
* [What language is LeoFS written in?](contents/what-language-is-leofs-written-in.md)
* [What languages can I use to work with LeoFS?](contents/what-languages-can-I-use-to-work-with-leofs.md)
* [How does LeoFS handle caching?](contents/how-does-leofs-handle-caching.md)


## LeoFS limits

* [LeoFS limits](contents/limitation-of-leofs.md)

## LeoFS for administrators
## Install LeoFS
* What is required machine spec?
* How do I operate LeoFS installation with the RPM package?
* How do I operate LeoFS installation with the DEB package?


### Configuration
#### Commons
* 設定ファイルにはIPアドレスとホスト名のどちらを記載すべきか
* オブジェクト名で使用可能な特殊文字
* バケット名のルールはあるか
* Does LeoFS support NFS?

#### Gateway
* ``[Cache]`` How do I configure cache?

#### Manager
* ``[consistency]`` How do I configure consistency level?
* ``[mdc-replication]`` How do I configure multi datacenter replication?

#### Storage
* ``[storage]`` Are there block size configuration? 
* ``[storage]`` How do I confiure disk structure?


### LeoFS operation
#### Commons
* 起動ユーザについて
* 停止時の注意点
* バージョンアップ方法
* アップデート方法は？
* バケットの制限はあるか
* 起動中のLeoFSに新しい設定ファイルを反映させる方法はあるか

#### Manager
* ``[consistency]`` How do I change consisntecy level during running LeoFS?
* ``[rebalance]`` How do I stop ``rebalance processing``?
* ``[rebalance]`` How do I configure message-quueing of object recover?

#### Storage
* ``[compaction]`` Should I need to stop a storage node when executing the ``compaction`` command?
* ``[compaction]`` コンパクションは自動で行われるか?
* ``[compaction]`` コンパクション時に一時的にファイル数、ディスク使用量が増えるのは何故か?
* ノード追加したときのデータは、どこに配置されるのか?
* ノード停止を検知した時、どのような振る舞いをするのか?


#### Gateway
* ``[cache]`` How do I operate cache expire?


### Trouble shooting
* ``[storage]`` How do I operate LeoFS after capacity of a storage node is full?
* ``[compaction]`` コンパクション時にhttp_errorが頻発する
* インストールは問題ないのに Storage ノードが起動しない

## LeoFS for application developers
* How can I access to LeoFS?
* When others update an object, how can I get the newest file?
* If I remove a object, does LeoFS remove it from disk?
* How do I do a compaction?

## Inside LeoFS
* How does LeoFS work on Multi-DC replication?
* How does implement cache mechanism?



