# [Functional Data Engineering — a modern paradigm for batch data processing](https://maximebeauchemin.medium.com/functional-data-engineering-a-modern-paradigm-for-batch-data-processing-2327ec32c42a)を読む

## Introduction
- functional programming
  - 関数型コードでは、関数の出力値は関数に渡された引数にのみ依存
```python
def test(x):
    y = x + 1
    return y
```
  - 入力に依存しない状態変化を除外できることで、プログラムの理解が容易になる
  - データパイプラインが複雑になろうとも関数型コードは明快さを維持する

## Reproducibility
- transparent and reproducible
  - 結果を得るためのプロセスを明確にする
- if we want to change a business rule and perform a backfill all of the downstream computation, we need the guarantee that the change of logic is the only moving part

## Pure tasks
- individual tasks should target a single output, the same way that a pure-function shouldn’t return a set of heterogenous objects
- 関数型コードと同様の考え方
- どうしてもPure task作成時に副作用が出るならば、タスクを小分けして管理する

## Table partitions as immutable objects

## A persistent and immutable staging area
- staging area すべてのデータを保持しておく場所

## Changing logic over time
- ビジネスロジックは時間とともに変化する
  - 下流のロジック・データは汚いものになるため再計算が必要
  - 例)
    - ある年度で集計方法が変化したとき、変化後のロジックで変化前を計算しなおした際にずれが生じる

## But what about dimensions?
- demension is slowly changing like upsert(updata + insert)
- The dimension table becomes a collection of dimension snapshots where each partition contains the full dimension as-of a point in time
- type 2 SDC
  - 管理が面倒
    - サロゲートキーの管理
    - FACTへの結合時のサロゲートキーの検索
    - プロセスエラーが多く、再現性がない
- ディメンションが大きいとき
  - スナップショットアプローチとSCDタイプの併用 <- 確認

## Unit of work
- 作業単位：一つの出力と同じ
  - パーティションのマッピングが容易
  - 作業単位を明確にできる
- Airflow ならそれができる

## A DAG of partitions
- we move away from individual rows or cells being the “atomic state” that can be mutated to a place where partitions are the smallest unit that can be changed by tasks
- パーテーションのデータリネージはより容易に概念化できる

## Past dependencies
![](https://miro.medium.com/max/1100/1*flGEwSAfWsOBkk7PIa-QbQ.webp)

- 流れのわかるフローを持つべき
- 特殊な計算ロジック・集計は別のモデルで作成するべき

## Late arriving facts
- データが遅れて到着する
  - 最初のイベント時間とイベント受信・処理時間を切り離す
  - 2つの異なる時間軸を作成する

## A standard deviation
- ルールを破る
  - 例：SLAと完全性のトレードオフ