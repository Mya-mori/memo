[参考文献](https://www.oracle.com/jp/a/tech/docs/technical-resources/0420-1330-oracle-architecture.pdf)を読む

# Oracle Databaseの概要

## 内部構造
### 処理の仕組み
- クライアントはSQLでデータベースにアクセス処理を要求
- データベース時は要求に従い処理を実行
- 物理的データはストレージに格納

### コンポーネント
- インスタンス
  - サーバ上にあるメモリ＋プロセス(書き込みなどを行う)
- データベース
  - ストレージにあるデータ