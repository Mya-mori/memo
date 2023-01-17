# [A Beginner’s Guide to Data Engineering — Part I](https://medium.com/@rchang/a-beginners-guide-to-data-engineering-part-i-4227c5c457d7)を読む

## Motivation
- The more experienced I become as a data scientist, the more convinced I am that data engineering is one of the most critical and foundational skills in any data scientist’s toolkit.

## Organization of This Beginner’s Guide
- 取り扱うコンテンツ
  - Airflow
  - batch data processing
  - SQL
- part1
  - what data engineering is
  - why it is challenging
  - how it helps your organization to slale
- part2
  - Airflow
    - programmatically author
    - schedule
    - monitor workflows
  - How to use Airflow
    - Hive batch job
    - design table schemas(star schema)
    - best practice about ETL
- part3
  - advanced data engineering patterns

## My First Industry Job out of Graduate School
- I was thrown into the wild west of raw data, far away from the comfortable land of pre-processed, tidy .csv files, and I felt unprepared and uncomfortable working in an environment where this is the norm.
  - つらい...

## The Hierarchy of Analytics
![](https://miro.medium.com/max/1100/1*2XybEH3eav63pBIu-tlRlw.webp)
- Before a company can optimize the business more efficiently or build data products more intelligently, layers of foundational work need to be built first.
  - 基礎となるレイヤーを固めないとその上のレイヤーがボロボロになる
- The Hiring Out-of-Order Problem
  - One of the recipes for disaster is for startups to hire its first data contributor as someone who only specialized in modeling but have little or no experience in building the foundational layers that is the pre-requisite of everything else
  - 上のレイヤーのみを意識しすぎると悲惨な目に合う
- todat's student
  - done
    - access raw data through public APIs
  - undone
    - design table schemas
    - build data pipelines

## Building Data Foundations & Warehouses
- Data engineering field could be thought of as a superset of `business intelligence` and `data warehousing`
- “big data” distributed systems, along with concepts around the extended `Hadoop ecosystem`, `stream processing`, and in computation at scale.
- a data warehouse is a place where raw data is transformed and stored in query-able forms.
  - データウェアハウス：SQLでアクセスできるように生データを加工する場所

![](https://miro.medium.com/max/1100/1*tcDY4JKmvgfR0x_x0gpS_Q.webp)

- データウェアハウスはデータ分析を行う上でエンジン・燃料となる存在
- データウェアハウス導入事例
  - [Building Analytics at 500px](https://medium.com/@samson_hu/building-analytics-at-500px-92e9a7005c83)
  - [Scaling Airbnb’s Experimentation Platform](https://medium.com/airbnb-engineering/https-medium-com-jonathan-parks-scaling-erf-23fd17c91166)
  - [Using ML to Predict the Value of Homes on Airbnb](https://medium.com/airbnb-engineering/using-machine-learning-to-predict-value-of-homes-on-airbnb-9272d3d4739d)

## ETL: Extract, Transform, and Load
![](https://miro.medium.com/max/1100/1*Uo56hrm9r5L_5fmPsY7I9A.webp)
- Extract
  - we transport the data from their source locations to further transformations
- Transform
  - translate raw data into analysis-ready datasets
  - ETLの核心部分
- Load
  - ransport them to a final destination

## Choosing ETL Frameworks
- フレームワークの比較表(ソースが2016年のため要確認)

![](https://miro.medium.com/max/1100/1*WszG7tFQbuQrYAHnNzxnlg.webp)

## Two Paradigms: SQL- v.s. JVM-Centric ETL
- SQLは学習コストが低く転用しやすい