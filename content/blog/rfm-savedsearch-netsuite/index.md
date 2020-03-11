---
title: Saved Search တွင် RFM Analysis ပြုလုပ်ခြင်း 
date: "2020-03-10T22:12:03.284Z"
description: "Saved Search တွင် RFM Analysis ပြုလုပ်ခြင်း"
---

# RFM Analysis ဆိုတာဘာလဲ <br>

**RFM ဆိုတာကကော?** 👀 <br>

![credit RAA](https://www.retailreco.com/blog/wp-content/uploads/2018/11/RFM-Analytics.jpg)

RFM (မကြာမီ၊ အကြိမ်ရေ၊ ငွေကြေး) ခွဲခြမ်းစိတ်ဖြာခြင်းသည်စျေးကွက်ရှာဖွေရေးနည်းစနစ်ဖြစ်ပြီးသုံးစွဲသူများသည်မည်သည့်လတ်တလောဝယ်ယူသူမည်မျှဝယ်ယူသည် (recency)၊ မည်မျှဝယ်သည် (ကြိမ်နှုန်း) နှင့်သုံးစွဲသူမည်မျှသုံးစွဲသည်ကိုဆန်းစစ်ခြင်းအားဖြင့်မည်သည့်စားသုံးသူများမည်မျှအကောင်းဆုံးဖြစ်သည်ကိုဆုံးဖြတ်ရန်အသုံးပြုသည်။ RFM ခွဲခြမ်းစိတ်ဖြာခြင်းသည်သင်၏စီးပွားရေးလုပ်ငန်း၏ ၈၀% သည်သင့်ဖောက်သည်များ၏ ၂၀% မှလာသည်ဟူသောစျေးကွက်ရှာဖွေရေးအပေါ်အခြေခံသည်။

##### NetSuite Saved Search တွင် ဘယ်လို ပြုလုပ်မှာလဲ?

![alt text](https://i.imgur.com/p6mmpcg.png)

Reports > Saved Searches > All Saved Searches > New ကိုနိုပ်ပါ

<u>**Search Title = RFM Analysis**</u> ဟုပေးပါ

<u>**Criteria**</u> : Type = Invoice , Tax Line = false , Main Line = false

![alt text](https://i.imgur.com/FdMtYEc.png)

<u>**In Results:**</u> <br><br> Tab တွင်
Sort by = Amount <br><br>
![alt text](https://i.imgur.com/Nv1JuCC.png)
<br><br>

Field : Name , Summary Type = Group By , Label = Customer Name <br>

Field : Formula(Percent) , Summary Type = Sum , 
``PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC)``
, Label = %Recency
<br><br>
Field : Formula(Percent) , Summary Type = Sum , 
``PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC)``
, Label = %Frequency
<br><br>
Field : Formula(Percent) , Summary Type = Sum , 
`PERCENT_RANK() OVER(ORDER BY SUM({amount}) ASC)`
, Label = %Monetary
<br><br>
Field : Formula(Text) , Summary Type = Maximum , 
`CASE WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC)  BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END || CASE WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END || CASE WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END`
, Label = RFM
<br><br>
Field : Formula(Numeric) , Summary Type = Sum , 
`CASE WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC)  BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END`
, Label = R
<br><br>
Field : Formula(Numeric) , Summary Type = Sum , 
`CASE WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END`
, Label = F
<br><br>
Field : Formula(Numeric) , Summary Type = Sum , 
`CASE WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END`
, Label = M
<br><br>
Field : Formula(Numeric) , Summary Type = Sum , 
`ROUND({today}-MAX({trandate}))`
, Label = Days from Last Purchased
<br><br>
Field : Document Number , Summary Type = Count , Label = Orders
<br><br>
Field : Amount , Summary Type = Sum , Label = Amount
<br><br>
### မှတ်ချက်

> ပုံမှန်အားဖြင့် RFM တန်ဖိုးကို 111 ဟုသတ်မှတ်ထားရာတွင် ဒီဖော်မြူလာတွင် 555 ဟုသတ်မှတ်ထားပါသည်။ 

Have Fun! 🦄
