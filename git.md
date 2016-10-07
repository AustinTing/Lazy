Git
===
簡單流程
--- 

- 先確認這次修改的東西 
```
git status
```
- 加入所有更動檔案
```
git add .
```
- 建立一個commit (Add xxx, Update xxx...etc)
```
git commit -m "Add xxx"
```
- 將遠端的repo拉回來
```
git pull
```
- Re-Run專案 (拉回後可能會遇到一些狀況之後在分別處理)
AS會告訴你有衝突的地方，更改xml有更動的地方，java部分跟我說
- 處理完衝突最後上傳
```
git push
```
拉專案
----
- 打開你的git.cmd
- 回到D:
```
cd ..
```
- 切到20percent
```
cd 20percent
```
- 打開連結 https://github.com/AustinTing?tab=repositories

- 選取專案名稱
- 右邊綠綠的clone複製連結
- 回到git.cmd
```
git clone 貼上連結
```
- 用AS開專案，要google-service

