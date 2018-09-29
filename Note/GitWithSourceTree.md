# SourceTree
SourceTree是一個git的圖形化工具，讓你可以透過圖形化介面執行git的指令。

## Create a local repository
在下載並安裝好之後，我們使用SourceTree開始建立一個local repository。
打開SourceTree切換到Local頁面，並點選create按鈕來創建local repository。
![](https://i.imgur.com/1rD3PPe.png)
選擇完資料夾後就案Create來創建。
接著會跳出提示，說明你創建的資料夾已經存在，這邊選則Yes即可。
![](https://i.imgur.com/dv91dHM.png)
接著就可以開始使用SourceTree的各種功能了。

## Commit
首先，先試著在respository內新增一些檔案，在首頁的部分可以看到剛才新建的respository，接著點兩下進到該respository內。
![](https://i.imgur.com/Qh8oudv.png)

接著點選`Open in Explorer`來開啟目錄，並建立測試用的檔案及資料夾，這邊在scr資料夾底下建立了index.txt和script.txt檔案。
![](https://i.imgur.com/9Va1NlI.png)

回到SourceTree，可以看到畫面上會顯示剛才新增的檔案，代表還沒加到Staging Area中。
![](https://i.imgur.com/g4oLvnI.png)

可以透過`Stage All`來將所有檔案將到Staging Area中。
![](https://i.imgur.com/F0944CP.png)

加到Staging Area中的檔案會顯示在上面，並且可以點選檔案來查看內容。
![](https://i.imgur.com/GOJwTcn.png)

接著可以在下面的textarea輸入comment並commit檔案。
![](https://i.imgur.com/MxqLoxx.png)

commit之後會看到畫面中沒有任何檔案，這是因為剛剛做了commit的動作，著點選左邊的`master`。
![](https://i.imgur.com/F1d1y3C.png)

可以看到剛剛的commit。
![](https://i.imgur.com/tLxglQk.png)

接著試著將檔案做修改，這邊將index.txt刪除和修改script.txt檔案內容。
接著回到`Working Copy`畫面中，可以看到SourceTree會顯示script.txt檔案被修改，index.txt檔案遺失。
![](https://i.imgur.com/hDH91R3.png)

將檔案加到Staging Area中，右邊一樣可以看到修改的內容。
![](https://i.imgur.com/Mw58EnY.png)

輸入comment並commit，再到`master`查看，可以看到剛才的commit已經顯示在master上。
![](https://i.imgur.com/E008GrC.png)


## gitignore
若要將檔案排除追蹤的話，可以新建`.gitignore`檔案，來將檔案untrack，而檔案就不會被加到Staging Area中了。
這邊先在資料夾中創建AutoGen/log.txt檔案。
![](https://i.imgur.com/Fkr3ZoI.png)

接著點選檔案名稱將檔案反白，在點選右鍵選擇Ignore，這邊選則第三項，該資料夾底下的檔案皆不會被加到Staging Area中。
![](https://i.imgur.com/buBNE8f.png)

接著可以看到產生了`.gitignore`檔案。
![](https://i.imgur.com/pzuXnMc.png)

接著再commit，可以看到`.gitignore`檔案被commit，而AutoGen資料夾底下的檔案都被忽略了，達到了我們要的目的。
![](https://i.imgur.com/4XZ0j70.png)

## Branch
### Create Branch
要創建branch可以點選上方的工具列，就會跳出創建視窗，接著只要輸入branch名稱，就能創建。
![](https://i.imgur.com/hTly3MD.png)

創建完之後可以在畫面上看到剛才創建的`branch`。
![](https://i.imgur.com/RNxLXNM.png)

接著試著修正`branch`上的錯誤，並commit。
![](https://i.imgur.com/t0FxMR0.png)

### Delete Branch
刪除branch之前，需先checkout到其他branch上，在左側master上點選滑鼠右鍵，選擇checkout master切換到master。
![](https://i.imgur.com/CJOAE65.png)

切換成功後，會看到master前面有一個圓圈，代表現在所在的branch。
![](https://i.imgur.com/t7x3CaT.png)

接著點選上方branch按鈕來進行刪除的動作，選擇Delete Branches分頁，勾選要刪除的branch。
![](https://i.imgur.com/DJ0vZYQ.png)

按下Delete Branches後會再跳出確認的視窗，選擇OK。
![](https://i.imgur.com/5OsIseg.png)

回到畫面之後就能看到刪除的branch已經不存在了。
![](https://i.imgur.com/WPC0A8r.png)


## Merge
若要將兩個branch合併，可以使用上方工具列的Merge功能，首先先確認已經切換到master分支。
![](https://i.imgur.com/SQLGDz7.png)


接著點選上方Merge按鈕，接著在要merge的分支上點選將他反白，可以看到修改的內容差別，按下OK後就能進行合併。
![](https://i.imgur.com/vOUV5mR.png)

回到畫面後就能看到兩個branch已經合併。
![](https://i.imgur.com/KanYQ9T.png)

接著就能將不再需要的branch給刪除，這邊在不要的branch上面使用滑鼠右鍵，選擇刪除。
![](https://i.imgur.com/QfhZAjw.png)

這邊會在跳出確認視窗，選擇確定。
![](https://i.imgur.com/yWMcXMT.png)

回到畫面之後，可以看到只剩下一個branch。
![](https://i.imgur.com/kQNgEo6.png)


## GitHub
這部分會介紹如何使用SourceTree和GitHub互動。
首先在GitHub上建立一個新的repository。
![](https://i.imgur.com/ZRJj2jO.png)

接著回到SourceTree並透過terminal的方式來和remote repository建立關聯。

```shell
git remote add origin URL
```

可以透過`git remote -v`來查看是否成功。
![](https://i.imgur.com/IzViM0J.png)
可以看到origin已經新增成功，接著就能把terminal給關掉。

### Push
使用上方的Push按鈕，可以選取要推送的branch，按下Push後會需要登入GitHub的帳號，登入完成後，可能會需要幾分鐘來將local repository推送到remote repository，這取決於你的repository大小。
![](https://i.imgur.com/2SoPVfK.png)

完成後就能在畫面上看到成功推送到remote repository。
![](https://i.imgur.com/IikPZ2q.png)


### Pull
在Pull動作之前，先從GitHub上新增README.md和LICENSE.md方便測試。

透過上方的Pull按鈕，可以將remote repository同步到local repository

![](https://i.imgur.com/2zEz4re.png)
在Pull按鈕上可以看到remote repository的檔案是否和local repository一樣。

按下OK後就能在畫面上看到剛剛新增的檔案，已經被同步到local repository了。
![](https://i.imgur.com/wPkPaFb.png)
