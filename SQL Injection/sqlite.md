
# 註解  
### 單行註解  
二個連字號 --  
### 多行註解  
類似c++ /*...*/  
### 不建議使用  
井字號  

# 系統預設內建表單:  
### sqlite_master  
### sqlite_schema  

# UNION語法  
### UNION SELECT sql,2,3,4,5,6,7,8,9 FROM sqlite_master  
sqlite的特異功能是，可以直接用常數（literal）填充，比如數字直接代替欄位名稱，數字在 SELECT 裡是常數。  
