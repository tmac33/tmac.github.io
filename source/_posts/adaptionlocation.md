title: 改变 adaptive component 位置
date: 2017-07-14 06:25:24
categories: revit
tags: [revit]
comments: true
---


<center> 有一国外网友问到关于自适应族位置的放置方式，这里做一记录</center>

<!-- more -->



# 情况

如果你想改变计划点参数，比如：Measurement Type,Chord Length,Measure Form,手动流程如下：

![](http://osej1thz9.bkt.clouddn.com/static/images/adapterlocation1.png)

1.为每个参数创建每个点的用户参数
   1.测量类型1
   2.点位置1
   3.测量类型2
   4.点位置2
   5.等等
   
2.使用API​​为每个家庭实例设置这些值

3.使用动态模型更新：

   1.随时参考点参数变化，自动更新这些用户参数
   
   2.在用户参数变化的任何时候自动更新参考点参数


![](http://osej1thz9.bkt.clouddn.com/static/images/adapterlocation2.png)


# 代码执行

此代码执行上面列出的步骤2，步骤3。
您将注意到，“测量类型”内部存储为整数，我们需要将该整数转换为相应的字符串（Chord Length，Segment Length ...），以便我们可以从同名参数中获取长度值。

```cs
public void adapt()
{
    Document doc = this.ActiveUIDocument.Document;
    using (Transaction t = new Transaction(doc,"Set Adapt Comp Data"))
    {
        t.Start();
        foreach (FamilyInstance fi in new FilteredElementCollector(doc).OfClass(typeof(FamilyInstance)).Cast<FamilyInstance>())
        {
            int ctr = 1;
            foreach (ElementId pointId in AdaptiveComponentInstanceUtils.GetInstancePlacementPointElementRefIds(fi))
            {
                ReferencePoint referencePoint = doc.GetElement(pointId) as ReferencePoint;
                Parameter measurementTypeParam = referencePoint.get_Parameter("Measurement Type");
                if (measurementTypeParam == null)
                    continue;
                
                int i = measurementTypeParam.AsInteger();
                string s = "";
                double paramValue = 0;
                if (i == 1)
                    s = "Non-Normalized Curve Parameter";
                else if (i == 2)
                    s = "Normalized Curve Parameter";
                else if (i == 3)
                    s = "Segment Length";
                else if (i == 4)
                    s = "Normalized Segment Length";
                else if (i == 5)
                    s = "Chord Length";
                
                paramValue = referencePoint.get_Parameter(s).AsDouble();
                
                fi.get_Parameter("Measurement Type " + ctr).Set(s);
                fi.get_Parameter("Point " + ctr).Set(paramValue);
                
                ctr++;
            }
        }
        t.Commit();
    }
}
``` 
