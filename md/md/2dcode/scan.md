





## 一 、流程图

```flow
st=>start: 开始
op=>operation: 获取图片
con=>condition: 图片是否可用
op1=>operation: 获取码图类别
con1=>condition: 解析码图
op2=>subroutine: 反色处理
op3=>subroutine: 增加对比度处理
con2=>condition: 处理后码图解析
io=>inputoutput: 输出码图信息
e=>end: 结束

st->op->con(yes)->op1->con1(yes)->io->e
con(no)->op
con1(no)->op2(right)->op3(right)->con2(yes)->io
con2(no)->op



```

```mermaid
graph LR;
    A-->B;
    A-->C;
    B-->D
```





``` mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D
```





## 二、 饼图





``` mermaid
pie    title Key elements in Product X    
"Calcium" : 42.96    
"Potassium" : 50.05   
"Magnesium" : 10.01   
"Iron" :  5

```







## 三、 甘特图

```mermaid
%% 语法示例
        gantt
        dateFormat  YYYY-MM-DD
        title 软件开发甘特图
        section 设计
        需求                      :done,    des1, 2014-01-06,2014-01-08
        原型                      :active,  des2, 2014-01-09, 3d
        UI设计                     :         des3, after des2, 5d
    未来任务                     :         des4, after des3, 5d
        section 开发
        学习准备理解需求                      :crit, done, 2014-01-06,24h
        设计框架                             :crit, done, after des2, 2d
        开发                                 :crit, active, 3d
        未来任务                              :crit, 5d
        耍                                   :2d
        section 测试
        功能测试                              :active, a1, after des3, 3d
        压力测试                               :after a1  , 20h
        测试报告                               : 48h
```



## 四、uml图

```mermaid
%% 时序图例子,-> 直线，-->虚线，->>实线箭头
  sequenceDiagram
    participant 张三
    participant 李四
    张三->王五: 王五你好吗？
    loop 健康检查
        王五->王五: 与疾病战斗
    end
    Note right of 王五: 合理 食物 <br/>看医生...
    李四-->>张三: 很好!
    王五->李四: 你怎么样?
    李四-->王五: 很好!
```



## 五、类图







```mermaid
classDiagram
      Animal <|-- Duck
      Animal <|-- Fish
      Animal <|-- Zebra
      Animal : +int age
      Animal : +String gender
      Animal: +isMammal()
      Animal: +mate()
      class Duck{
          +String beakColor
          +swim()
          +quack()
      }
      class Fish{
          -int sizeInFeet
          -canEat()
      }
      class Zebra{
          +bool is_wild
          +run()
      }
```

