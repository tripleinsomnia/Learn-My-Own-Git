# Git Note
Git專案分成三個主要區域：Git目錄、工作目錄(working directory)以及暫存區域(staging area)。
![](https://i.imgur.com/Yp6QGMm.png)



## 創建Repository
在資料夾中輸入`git init`，將folder變成repository，該資料夾底下會多出檔名為`.git`的資料夾，接著就能使用一系列的git指令。  


## 將檔案加到Staging Area
利用`git add 檔案名稱`來將檔案加到Staging Area中，再透過`git status`指令來查看Staging Area目前狀態。  
![](https://i.imgur.com/1FzcjBP.png)
由上圖可以看到原本紅色的提示變成綠色，顯示目前加到Staging Area中的檔案有哪些。  

若要一次將所有檔案加到Staging Area中，可以使用:

```shell
git add .
```

如下圖可以看到staging area中的檔案。
![](https://i.imgur.com/zqzbmK7.png)

但是若將實際的檔案刪除之後，在使用`git status`來查看Staging Area中的檔案，會發現目前的Staging Area還是原本的檔案，但是底下會出現紅字提示，告知目前刪除的檔案有那些，而這些狀態沒有新增到Staging Area內。  
![](https://i.imgur.com/zdRgUhm.png)

接著再透過`git add .`和`git status`來查看更新後的狀態，會看到實際被刪除的檔案的狀態，已經在Staging Area中更新了。  
![](https://i.imgur.com/cTxoUiZ.png)


## 查看Staging Area中的狀態
使用`git status`來查看目前Staging Area中有那些檔案  
![git statue](https://i.imgur.com/htxJ3JI.png)  


## 將不想追蹤的檔案排除在外

```shell
git rm --cache 檔案名稱
```

將不想追蹤的檔案排除在外，接著透過`git status`查看目前Staging Area狀態，可以看到檔案已經被排除在外了。  
![](https://i.imgur.com/uSEZxGg.png)  

## Create a .gitignore
不想每次都要下指令檔案給排除追蹤，這時`.gitignore`就很好用，該檔案能記錄哪些檔案是不需要被追蹤，如:log檔案之類。
首先需要先創建`.gitignore`檔案

```shell
touch .gitignore
```

![](https://i.imgur.com/4PDnONU.png)

接著將不想追蹤的檔案名稱寫進`.gitignore`檔案內

```shell
vim .gitignore
```
這邊將log.txt檔案加入。
![](https://i.imgur.com/KXTSeTi.png)

接著再commit一次將`.gitignore`提交到Repository。
![](https://i.imgur.com/miEtFLM.png)

現在來實際測試一下`.gitignore`是否有設定成功。
先對log.txt進行編輯，再使用`git status`進行查看。
![](https://i.imgur.com/Dmo9nYB.png)
這邊會看到git依舊會提示log.txt尚未家到Staging Area中。  
這是因為目前的cache記住了在`.gitignore`檔案新增之前的追蹤狀態，必須要將cache給刪除，才有效果。

```shell
git rm -r --cache .
```

這並不會刪除實際的檔案，只會將cache清除。
![](https://i.imgur.com/p209BHl.png)

接著再重新commit一次。
![](https://i.imgur.com/Dtgb6MQ.png)

對log.txt進行內容新增或修改後，在使用`git status`檢查，可以看到該檔案不再被追蹤。
![](https://i.imgur.com/ibK5kRD.png)


## Commit
在使用`commit`指令之前，需要先設定使用者名稱和信箱。

```shell
git --global user.name "USER_NAME"
git --global user.email "USER_EMAIL"
```

在設定完user name和user email後，就可以執行commit

```shell
git commit -m "COMMENT"
```

`commit`指令用來將Staging Area中的檔案提交到respository，`-m`能替該次的commit加上註解，需使用雙引號括起來。
![](https://i.imgur.com/a5AoRXR.png)

若想查看commit的資訊，則可以透過`git log`指令，該指令會顯示所有commit的作者、時間及註解，每個commit都會有一個ID。
![](https://i.imgur.com/6H6oCdb.png)

當log太多時，可能無法一次顯示完所有的commit紀錄，這時可以使用oneline模式來顯示。

```shell
git log --oneline
```

可以看到在oneline模式下，只會顯示commit的ID前七碼，以及註解。
![](https://i.imgur.com/QCgZGL1.png)



## Checkout
`checkout`功能可以讓你移動到各個brunch的commit，檢查某個commit時間點下的檔案狀態，這個指令並不會刪除某個時間點的commit。

```shell
git checkout ID
```

![](https://i.imgur.com/mDzUYB9.png)

可以再使用`git log`來確認目前所在的commit位置，可以看到目前指標`HEAD`已經不再指向master了。
![](https://i.imgur.com/QTQvcoH.png)

當想要再跳到某個commit時間點的話必須先回到master才能在chechout其他時間點。

```shell
git checkout master
```

可以看到目前]branch為master。
![](https://i.imgur.com/tMEDLbC.png)


## revert
revert指令可以倒退一個commit的狀態，執行該指令後，可以輸入comment，並會在log裡面留下commit時間點。

```shell
git revert ID
```
執行`git revert`後使用`git log`來查看。
![](https://i.imgur.com/UEJkSFY.png)

可以看到原本刪除的檔案，在`revert`之後出現了。
![](https://i.imgur.com/NgTAetK.png)

若在`revert`想要反悔上一個動作的話，可以再一次使用`revert`來還原上一個`revert`，之後再使用`git log`查看狀態。
![](https://i.imgur.com/i78J4Zi.png)

## reset
git reset主要有三種模式:

- soft
- mixed
- hard

### hard Mode
此種模式完全不保留原始commit節點的任何資訊，會連同資料夾中實體檔案內容都進行重置，也就是直接將Work Dictionary、Staging Area及git目錄都重置成目標Reset節點的資料內容。

```shell
git reset --hard ID
```

首先選擇要`reset`的節點，這邊選擇`97fbf17`這個節點。
![](https://i.imgur.com/R253WDj.png)

接著對節點進行`reset`

```shell
git reset --hard 97fbf17
```
可以看到在該節點後面的`commit`都消失了。
![](https://i.imgur.com/1tTmad0.png)



## Branch
`branch`指令能對一個專案新建一個分支，例如可以有一個分支代表release version，而另一個分支能用來debug，`branch`可以被delete、add和merged。

創建`branch`指令為

```shell
git branch bugs
```

該指令會創造一個叫bugs的`branch`。
這邊使用`checkout`指令來達到創建`branch`，並會切換到該`branch`。

```shell
git checkout -b BRANCH_NAME
```

該指令會產生並切換到名字為dev的`branch`
若要想要切回`master`分支，可以使用

```shell
git checkout master
```

查看所有`branch`可以使用

```shell
git branch -a
```
星號代表現在所在的`branch`
![](https://i.imgur.com/pnWK9U9.png)

要刪除一個`branch`，可以使用
```shell
git branch -d BRANCH_NAME
```

## merge
`merge`可以將`branch`合併。使兩個`branch`間的資料一致。

```
git merge dev
```

合併`branch`之後，透過`git log`來查看，可以看到HEAD指標指向了兩個`branch`，表示這兩個branch已經合併再一起了。
![](https://i.imgur.com/KEHVyIb.png)

