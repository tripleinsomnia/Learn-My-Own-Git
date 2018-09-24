# GitHub Note
這篇文章記錄了如何快速上手GitHub的基本功能。  
GitHub是一個可以上傳repositories的server，透過GitHub你可以和其他人協同合作開發project。

## Creating Remote Respository
在創建完帳號登入之後，選擇New repository。
![](https://i.imgur.com/oWsLYbC.png)

在創建時，只輸入名字和描述。
![](https://i.imgur.com/ugBoVxF.png)

接著按下`create repository`之後，會看到該頁面:
![](https://i.imgur.com/hezGj3N.png)
這邊可以看到有兩種方式連接到remote repository，這邊使用https方式。


## Connect to Remote Repository
開啟terminal，創建一個資料夾，這個資料夾名稱不必和GitHub上的repository相同，接著切換到新創建的資料夾內，並使用`git init`創建一個git repository。
![](https://i.imgur.com/J7AM3PH.png)

使用remote指令將local連到server的repository

```shell
git remote add origin URL
```

這邊的URL就是剛才從GitHub上看到的URL。
![](https://i.imgur.com/GbN5m03.png)

可以使用以下指令來檢查是否有連到github上面的repository。

```shell
git remote -v
```
可以看到會有兩個URL:
- fetch:
和pull差不多，將檔案從remote repository拉到local repository拉到local。
- push
將檔案從local repository拉到local repository拉到local。

![](https://i.imgur.com/ivrjJvb.png)


## Push
Push指令用來將local repository的檔案，推送到remote repository。
在這之前，我們先在local repository創建README.md檔案。

### Create README
`README.md`檔案為Markdown語言寫的檔案，在進入repository時候，會預設顯示的檔案，通常用來介紹repository內容或是使用方式等。

```shell
echo "# EasyGitHub" >> README.md
echo "this repository is for github learning." >> README.md
```

在創建好之後進行`commit`，將檔案推送到local repository。

```shell
git add .
git commit -m "create README"
```
![](https://i.imgur.com/OkwmRXh.png)

### Push to remote repository

```shell
git push -u origin master
```

這邊在下了push指令之後，會要求輸入GitHub的帳號和密碼，之後就會看到成功push之後的訊息。
![](https://i.imgur.com/yDOXaG7.png)

接著回到GitHub畫面，確認README.md是否有成功push到remote repository。
![](https://i.imgur.com/rAs3yi6.png)



## Pull
pull指令可以將remote repository拉到local repository，在開始之前，我們先在GitHub上創建`LICENSE.md`和`.gitignore`檔案。

### Create LICENSE
這邊透過GitHub的license template來建立`LICENSE.md`，該檔案可以告知其他使用者這個repository的使用權限，這邊選擇創建`MIT License`，代表其他人可以任意使用這個repository的內容。

點選`create new file`
![](https://i.imgur.com/1JmtoEH.png)

檔名輸入`LICENSE.md`，接著GitHub會偵測你的檔名，右邊會跳出license template的按鈕。
![](https://i.imgur.com/PANBIvQ.png)

接著點選`choose a license template`，在左側選擇`MIT License`，並在右側輸入years和full name，完成後按下綠色按鈕`Review and submit`。
![](https://i.imgur.com/HqGtHpM.png)

可以看到LICENSE.md檔案內容已經自動填上。
![](https://i.imgur.com/sMwZNma.png)

接著將畫面往下拉，輸入comment後，點選率色按鈕`Commit new file`完成創建。
![](https://i.imgur.com/Neq2BW8.png)

畫面會自動跳回repository頁面，可以看到LICENSE檔案已經成功創建。
![](https://i.imgur.com/WrL7Oc2.png)

### Create gitignore
`.gitignore`是用來記錄，那些檔案不想同步，GitHub上面也提供了許多template，但是這邊不使用。
按下`create new file`創建`.gitignore`檔案，接著再輸入的地方輸入想要掠過同步的檔案或資料夾名稱，這邊輸入的是`AutoGenerate/`，代表AutoGenerate資料夾底下的檔案，皆忽略。
![](https://i.imgur.com/TvBu5CR.png)

再將視窗拉到底下，進行commit動作。
![](https://i.imgur.com/otvdQfy.png)

點選`Commit new file`後會跳回repository頁面，在這邊可以確認`.gitignore`檔案已經成功創建。
![](https://i.imgur.com/CFuIu0z.png)

## Pull to loacl repository
接下來將remote repository，pull到local repository。
```shell
git pull origin master
```
這邊會將master從remote repository拉到local repository。
![](https://i.imgur.com/zsZFW4q.png)

使用`git log`指令來確認，剛剛再GitHub上面的commit都同步到local repository了。
![](https://i.imgur.com/WJ6WfhY.png)



## master和origin/master
可以看到在上面的動作完成後，HEAD指標同時指向了master及origin/master。
- master 
代表了local repository的branch
- origin/master
代表repository的branch。

這邊我們在local repository新增一個檔案，並做commit的動作。
![](https://i.imgur.com/1rI07T6.png)

接著使用`git log`
![](https://i.imgur.com/p28Z9P1.png)
可以看到HEAD指標指向了最新一次的commit，而這個commit是在local repository執行的，所以HEAD指向了master這個branch，代表local repository比remote repository多了一次的commit狀態。


## branch
這邊介紹如何將remote repository的branch刪除，在某些情況下可能需要這麼做，舉例來說，有一個branch是用來修正錯誤，當你將錯誤修正之後，會將branch和master做合併，合併之後，就不再需要該branch，這時就能把該branch從remote repository中刪除。

首先，先在GitHub上面創建一個測試用的檔案，檔案內容隨意，這邊示範的是`myFunc.js`。

使用pull將remote repository給同步到local repository。
![](https://i.imgur.com/nZcD4wr.png)

接著使用`git checkout -b error01`創建一個名為error01的branch。
![](https://i.imgur.com/DwlMQRo.png)

對myFunc.js進行內容修正，並commit。
![](https://i.imgur.com/iNiUzyW.png)

切換到master，並merge。
```shell
git checkout master
git merge error01
```

![](https://i.imgur.com/qEa5RAR.png)

接著將local repository推送到remote repository

```shell
git push
```

這邊只需要`git push`指令，而不用在指定branch名稱，因為上一次已經有指定過名稱了，git會記住上次push的branch，下次就不需要輸入branch的名稱。
![](https://i.imgur.com/zkdZetn.png)

到GitHub可以看到只有一個branch。
![](https://i.imgur.com/f9sR6pi.png)

將local repository推送到remote repository的branch上面。
![](https://i.imgur.com/1WHQUA3.png)

到GitHub上可以看到branch變成兩個了，使用branch的按鈕可以顯示目前所有的branch。
![](https://i.imgur.com/PhJ5qdi.png)

刪除remote repository可以使用:

```shell
git push --delete origin error01
```

![](https://i.imgur.com/TL7o6Xx.png)

remote repository的branch error01就會被刪除，可以到GitHub確認。

![](https://i.imgur.com/2CDCqGp.png)

