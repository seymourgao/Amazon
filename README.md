# Amazon-
Python pandas jieba

# :blush: 亚马逊某商品数据分析

使用 Pandas对数据进行提取分析，主要分析电商商品的评论、商品星级等，数据源来自网络。

## 环境
* Windows/Linux
* Python 3.7
## 依赖
* pandas
* jieba

## 导入数据
 ```
temp = pd.read_csv('input/amazon/Amazon.csv')
print(temp)
 ```
![](https://github.com/seymourgao/Photo/blob/master/1.png)

## 统计品牌次数
 ```
temp1=temp['brand'].value_counts()
print(temp1[:10])
 ```
![](https://github.com/seymourgao/Photo/blob/master/2.png)

## 统计品牌次数前十名
 ```
temp1=temp.pivot_table(index="brand",values="comment_num",aggfunc=np.sum)
temp2=temp1[temp1["comment_num"]>0]
temp3=temp2.sort_values(by='comment_num',ascending=False)
tempa=temp3
print(tempa[:10])
 ```
![](https://github.com/seymourgao/Photo/blob/master/3.png)

## 统计5星级品牌前十名
 ```
temp1=temp[temp["star"]>0]
temp2=temp1.pivot_table(index="brand",values="star")
temp3=temp2.sort_values(by='star',ascending=False)
tempb=temp3
print(tempb[:10])

 ```
![](https://github.com/seymourgao/Photo/blob/master/4.png)

## 品牌数据合并
 ```
BrandStats=pd.merge(tempa,tempb,left_index=True, right_index=True)
print(BrandStats[:20])

 ```
![](https://github.com/seymourgao/Photo/blob/master/5.png)

## 进行品牌评论合并进行词频分析
 ```
tempa=pd.read_csv('E:/Tableau教程/amazon/Amazon.csv')
tempb=pd.read_csv('E:/Tableau教程/amazon/AmazonComment.csv')
tempa=tempa.loc[:,["shop_id","brand"]]
temp=pd.merge(tempb,tempa,on='shop_id',how='left')

temp1=temp[temp["brand"]=="SEPTWOLVES 七匹狼"]
temp2=temp1["comment_text"]
temp3=' '.join(temp2)

tempkey=jieba.analyse.extract_tags(temp3, topK=10,withWeight=False,allowPOS=())
print('、'.join(tempkey))
 ```
![](https://github.com/seymourgao/Photo/blob/master/7.png)

## 结果展示
 ```
def topN(brand):
    a=temp[temp["brand"]==brand]
    b=a["comment_text"]
    c=' '.join(b)
    d=jieba.analyse.extract_tags(c, topK=10,withWeight=False,allowPOS=())
    e='、'.join(d)
    return e

BrandStats["topWords"]="none"
print(BrandStats)

for i in range(2395):
    BrandStats.iloc[i,2]=topN(BrandStats.index[i])

print(BrandStats[100:150])
 ```
![](https://github.com/seymourgao/Photo/blob/master/8.png)
![](https://github.com/seymourgao/Photo/blob/master/9.png)



 
 
 
 
 
 [回到顶部](#readme)
