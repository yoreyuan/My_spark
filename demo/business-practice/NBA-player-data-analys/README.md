Spark 商业案例之NBA篮球运动员大数据分析系统应用案例
---

### 15.1 NBA篮球运动员大数据分析系统架构和实现思路
基于NBA球员历史数据1970年至2016年各种表现，为全方位分析球员的技能，构建最强NBA篮球团队做数据分析支撑系统。

具体的数据中，关键的数据项如下所示：  

 术语  |   释义
 ---- | ----
3P:   |  3分命中
3PA:  |  3分出手
3P%:  |  3分命中率
2P:   |  2分命中
2PA:  |  2分出手
2P%   |  2分命中率
TRB   |  篮板球
STL   |  抢断
AST   |  助攻
BLK   |  盖帽
FT    |  罚球命中
TOV   |  失误
  
* 如何对球员进行评价？也就是如何进行科学的指标计算，  
一个比较流行的算法是`Z-score`: 其基本的计算过程基于球员的得分减去平均值后除以指标差。
例如，一个球员2016年的平均篮板数是7.1，而所有球员在2016年的平均篮板数是4.5， 标准差是1.3， 那么该球员Z-score得分为2=(7.1-4.5)/1.3。  

* 具体如何通过Spark 技术实现：
    * 第一步： 数据预处理：例如去除不必要的标题等信息
    * 第二部： 数据的缓存：为加速后面的数据处理打下基础
    * 第三部： 基础数据项计算：方差、均值、最大值、最小值、出现次数等。
    * 第四部： 计算Z-score，一般会进行广播，可以提升效率。
    * 第五步： 基于前面四部的基础，可以借助spark SQL进行多维度NBA篮球运动员数据分析，可以使用SQL语句，也可以使用DataSet。
    * 第六步： 把数据放到Redis或者DB中。
    
    
* 数据来源
**NBA** 美国职业篮球联赛，是由北美30支队伍组成的男子职业篮球联赛，汇集了世界上最顶级的球员。NBA一共有30支球队，东部分区和西部分区各有15支球队。
其中西部分区又被划分为西北赛区、太平洋赛区、西南赛区，每个赛区由5支球队组成。
东部分区包括三大赛区：大西洋赛区、东南赛区、中部赛区，每个赛区也由5支球队组成。  
每个分区，均为前八名进入季后赛，对阵依据第一对第八，第二对第七，依次类推。
每一轮系列赛均采取七局四胜的赛制，常规赛战绩占优的球队拥有主场优势。
两大赛区冠军进行冠军总决赛，同样为七局四胜。
  
[](http://www.basketball-reference.com/leagues/NBA_2017_totals.html)
UserID YoreYuan
Password yore****


### 15.2 NBA篮球运动员大数据分析系统代码实战：数据清洗和初步处理  
* 数据清洗第一步：对原始的NBA球员数据进行初步处理，并进行缓存。  例如数据中可能含有多个逗号中间没有值的(,,)，需要清洗为(,0,)

* 数据清洗第二步：对原始的NBA球员数据记性基础性处理，并进行基础数据项计算：方差、均值、最大值、最小值、出现次数等。


### 15.3 NBA篮球运动员大数据分析代码实战之核心基础数据项编写
统计出每年NBA球员比赛的各项聚合统计数据

根据数据，按照NBA球员比赛数据统计需求，统计出NBA球员数据每年标准分 Z-Score计算  































