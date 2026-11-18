\#Psychology Questionnaire Analyzer



\##1.项目简介

本项目是一个基于Python的心理学问卷数据分析程序，主要用于对问卷收集的数据进行初步整理和描述性统计分析。



在心理学研究中，问卷调查是一种常见的数据收集方式。面对问卷数据，需要对原始数据进行检查、整理，并计算各题目的基本统计指标。本项目尝试使用Python实现这一过程，提高问卷数据处理的效率。



程序以CSV文件为输入，对问卷数据进行有效性检查，并计算各题目的平均数，标准差，最大值，最小值以及不同选项的频数和百分比，最后将分析结果导出为CSV文件。



\##2.文件说明

‘questionnaire\_analyzer.ipynb' :Python主程序，负责读取问卷数据，数据清理、描述性统计和频数分析

&#x20;  'sample\_questionnaire.csv' : 示例问卷数据，包含参与者编号及Q1-Q5五个题目的回答



\##3.代码说明

\###3.1导入所需模块

import os

import csv  （读取和处理CSV文件）

import statistics  （计算平均数和标准差）

from collections import Counter    （统计不同选项出现的次数）



\###3.2读取问卷数据

with open(file\_path,"r",encoding="utf-8-sig")as file:

&#x20;   reader=csv.DictReader(file)

&#x20;   data=list(reader)

（使用'csv.DictReader()'读取CSV文件，将每一行数据转换为字典，方便根据题目名称提取对应的回答）



\###3.3数据检查与清理

missing\_count=0

invalid\_count=0



clean\_data=\[]



for participant in data:

&#x20;   clean\_participant={}



&#x20;   for question in questions:

&#x20;       answer=participant\[question].strip()



&#x20;       if answer=="":

&#x20;           missing\_count +=1

&#x20;           clean\_participant\[question]=None



&#x20;       elif answer.isdigit() and 1 <= int(answer) <=5:

&#x20;                clean\_participant\[question]=int(answer)



&#x20;       else:

&#x20;           invalid\_count+=1

&#x20;           clean\_participant\[question]=None

&#x20;

clean\_data.append(clean\_participant)



（通过循环检查每位参与者的每道题目回答，将空白答案识别为缺失值，将非数字或超出1-5范围的回答识别为无效数据，并将有效回答转换为整数，完成数据清理。）



\###3.4 描述性统计分析

&#x20;n=len(scores)



&#x20;   if n>0:

&#x20;       mean\_score=statistics.mean(scores)

&#x20;       min\_score=min(scores)

&#x20;       max\_score=max(scores)



&#x20;       #只有两个及以上有效答案时才能计算样本标准差

&#x20;       if n>=2:

&#x20;           sd\_score=statistics.stdev(scores)

&#x20;       else:

&#x20;           sd\_score=None

（针对每道题目提取有效回答，计算有效样本数，均值，最小值和最大值。当有效样本数不少于2时，进一步计算样本标准差，用于描述问卷回答的基本情况。）



\###3.5频数与百分比分析

&#x20;score\_counts=Counter(scores)



&#x20;   #计算总有效答案数量

&#x20;   total=len(scores)



&#x20;   #统计1-5分的频数和百分比

&#x20;   for score in range(1,6):



&#x20;       frequency=score\_counts.get(score,0)



&#x20;       if total>0:

&#x20;           percentage=frequency/total\*100

&#x20;       else:

&#x20;           percentage=0

（使用counter（）统计各分数出现的次数，并计算1-5分各选项的频数和百分比，了解不同回答的分布情况。）



\###3.6导出分析结果

os.makedirs("output",exist\_ok=True)

&#x20;   writer=csv.DictWriter(file,fieldnames=fieldnames)

&#x20;   writer.writeheader()

&#x20;   writer.writerows(descriptive\_results)

使用os.makedirs()创建结果保存文件夹，并通过csv.DictWriter()将统计结果写入CSV文件，便于后续查看，整理和使用。





\##4.学习心得与规划

这一次算是正式第一次叩响GitHub这个久仰大名的技术社区的大门，我时刻充满了一股相见恨晚的感觉，这就是部分工科生的聚集地与天堂啊，我暂时不知道自己基于Python的兴趣点在哪，于是我搜索”深圳大学“和”陈天行“...让我仿佛进入新世界。再结合自己在作业推动下摸爬滚打地完成一个小小的心理学数据分析项目，我被技术的魅力所折服，同样，遇到代码块的无限次报错，我会下意识觉得自己连这么简单的代码都完成不了，我也认识到学习的路是任重道远。一方面我崇拜技术的魅力，一方面我也深知每一步都需要脚踏实地，稳扎稳打。我想，如果我全力以赴，是不是也能在2027年9月秋招的时候，在简历上分享自己的GitHub链接呢。但是我需要切记不能好高骛远，一定要脚踏实地！首先，我一定要好好夯实基础，要强化自己的理解，先手写代码，才能明白自己的薄弱点，然后渐渐以岗位需求等方面去强化和完善自己的能力。未来我希望基于自己的职业规划和实际兴趣，做一些真正能落地的项目，但是当下最重要的是夯实代码基础，我的执行力要跟上我的想象力。



