長庚大學 大數據分析方法 作業三
================

網站資料爬取
------------

``` r
#這是R Code Chunk
#install.packages("rvest")
library(rvest) ##第一次使用要先安裝 install.packages("rvest")
```

    ## Warning: package 'rvest' was built under R version 3.3.3

    ## Loading required package: xml2

    ## Warning: package 'xml2' was built under R version 3.3.3

``` r
PTT <- read_html("https://www.ptt.cc/bbs/NBA/index.html")
btnURL <- PTT %>% html_nodes("a[class='btn wide']") %>% html_attr("href")
indexNum <- as.numeric(gsub("/bbs/NBA/index|.html","",btnURL[2]))

totalPage<-NULL
for (i in (indexNum-4):(indexNum+1)){
PTT = paste("https://www.ptt.cc/bbs/NBA/index",i,".html",sep="")
Title <- read_html(PTT) %>% html_nodes(".title") %>% html_text()
PushNum <- read_html(PTT) %>% html_nodes(".nrec") %>% html_text()
Author <- read_html(PTT) %>% html_nodes(".author") %>% html_text()
tempPage <- data.frame(Title, PushNum, Author)
totalPage <- rbind(totalPage, tempPage)
}
View(totalPage)



##read_html
##html_nodes
##html_text
```

爬蟲結果呈現
------------

``` r
#這是R Code Chunk
knitr::kable(totalPage) ##請將iris取代為上個步驟中產生的爬蟲資料資料框
```

| Title                                                   | PushNum | Author       |
|:--------------------------------------------------------|:--------|:-------------|
| \[BOX \] Jazz 95:108 Clippers 數據                      | 21      | Rambo        |
| \[Live\] 巫師 @ 騎士                                    | 爆      | Rambo        |
| \[新聞\] 違反禁藥規定　他被聯盟禁賽20場                 | X6      | HANASUCIA    |
| \[Live\] 暴龍 @ 小牛                                    | 7       | Rambo        |
| \[Live\] 尼克 @ 馬刺                                    | 爆      | Rambo        |
| Re: \[花邊\] O'Neal談Kobe：沒有他我完成不了這些成就     | X2      | backere0720  |
| \[Live\] 灰狼 @ 拓荒者                                  | 5       | Rambo        |
| \[新聞\] MVP好難選 鵜鶘教練建議選兩個                   | 23      | DantesChen   |
| \[討論\] 拿到單季MVP大滿貫有多難                        | 7       | kyoiori100   |
| \[BOX \] Wizards 127:115 Cavaliers 數據                 | 爆      | Rambo        |
| \[討論\] 大三元與MVP                                    | 爆      | feyako       |
| \[閒聊 \] Kobe發推特祝賀Booker 70分                     | 54      | dragon803    |
| \[花邊\] 最長連續罰球金氏世界紀錄保持者逝世             | 93      | bigDwinsch   |
| \[討論\] 長相是否影響人氣很多？                         | 99      | yokann       |
| \[BOX \] Knicks 98:106 Spurs 數據                       | 44      | Rambo        |
| \[新聞\] 詹皇帶傷當眼鏡俠硬拚 騎士仍遭巫師擊敗          | 12      | kingtseng    |
| \[BOX \] Raptors 94:86 Mavericks 數據                   | 10      | Rambo        |
| \[討論\] KP是不是過譽了?                                | 25      | randy225     |
| \[情報\] POPO開玩笑：不會在季後賽開始前簽下秘密         | 38      | Wall62       |
| \[花邊\] Kobe：湖人聯繫我就一個電話的事                 | 55      | lovea        |
| \[討論\] Kobe的雕像要做成什麼姿勢？                     | 93      | tpc302       |
| \[情報\] 盧：有些防守戰術將留到季後賽用                 | 92      | CCULaoDa     |
| \[討論\] 騎士的最大心魔                                 | 6       | ppeerrrryy   |
| Re: \[討論\] 長相是否影響人氣很多？                     | 33      | rukawa28     |
| Fw: \[新聞\] 鮑爾父親：一場比賽並不能決定整個賽季       | 55      | olively      |
| \[BOX \] Timberwolves 100:112 Blazers 數據              | 36      | Rambo        |
| \[情報\] TODAY+2001TODAY                                | 9       | Ivers        |
| \[新聞\] 成就不只如此？歐尼爾：奈許2座MVP是我的         | X5      | vm04vm04     |
| \[花邊\] 庫班對BG被JJ推倒感到抱歉                       | 爆      | firstsg      |
| \[花邊\] 歐肥爆粗口　幹譙當年沒投他MVP的記者            |         | adam7148     |
| \[討論\] 關於一些籃球的英文                             | 54      | js2a117573   |
| \[新聞\] 爵士近5戰輸4場 戈貝爾：球隊有人只想刷          | 爆      | whj0530      |
| \[新聞\] 護目鏡隨手扔 詹皇差點丟到巫師二哥（影          |         | dameontree   |
| \[討論\]大家覺得 ALT如何？                              | XX      | ccps970915   |
| Re: \[花邊\] 最長連續罰球金氏世界紀錄保持者逝世         | 4       | sscck5       |
| \[討論\] 一個教練優劣的觀察期要多長？                   | 17      | h1212123tw   |
| (本文已被刪除) \[MrSatan\]                              | 4       | -            |
| \[情報\] James重申:這是我生涯中最有挑戰性的賽季         | 70      | knic52976    |
| \[討論\] MVP：西河還是鬍子？                            | 88      | ddd123       |
| \[新聞\] 成最年輕得分王 布克期許自己謙虛                | 5       | adam7148     |
| Re: \[討論\] 關於一些籃球的英文                         | 40      | ej04cj86     |
| \[新聞\] 柯爾：杜蘭特復出還需要幾周時間                 | 26      | iso2288      |
| \[討論\] 開季前~整季勝場預測 vs 現在                    | 15      | checktime    |
| \[情報\] 小河流:單挑能打爆我爹，即使他巔峰              | 40      | bigDwinsch   |
| \[新聞\] 克勞佛爆發 快艇連6季駛進季後賽                 | 22      | gt097231     |
| Re: \[心得\] 看了單場得分50+統計，原來老大這麼強!       | 10      | huntai       |
| Re: \[討論\] 長相是否影響人氣很多？                     | 96      | lariat       |
| \[情報\] TNT: LBJ 像 好 酒                              | 20      | Turtle100    |
| \[討論\] Brett Brown算是有料的教練嗎                    | 11      | whattheduck  |
| (本文已被刪除) \[waiting0212\]                          |         | -            |
| \[新聞\] NBA／伊巴卡歸隊轟下18分 助暴龍連4季闖          | 6       | iam168888888 |
| \[新聞\] Kobe退休後最大的困擾 居然是看不到NBA           | 75      | zzzz8931     |
| \[情報\] ★今日排名(2017.03.26)★                         | 6       | Rambo        |
| \[討論\] 布拉與大歐                                     | 27      | fliesa       |
| \[心得\] 突然想紀念看過的現場                           | 42      | walkerold    |
| \[情報\] 各隊場均kWPA &gt;0.2者(綜合勝率提升指數)       | 23      | checktime    |
| Re: \[討論\] 布拉與大歐                                 | 9       | Tina741214   |
| \[新聞\] 單打他準沒錯！NBA各位置防守最糟糕的現          | 爆      | brandon0415  |
| \[新聞\] 本季最絕望球隊 籃網得第一                      | 39      | jailkobe5566 |
| \[新聞\] 客場一日遊累趴 湖人主帥砲轟賽程安排            | 10      | sampsonlu919 |
| \[Live\] 籃網 @ 老鷹                                    | 爆      | Rambo        |
| (本文已被刪除) \[dragon803\]                            |         | -            |
| \[Live\] 國王 @ 快艇                                    |         | Rambo        |
| \[Live\] 雷霆 @ 火箭                                    | 爆      | Rambo        |
| \[BOX \] Suns 106:120 Hornets 數據                      | 18      | Rambo        |
| \[BOX \] Nets 107:92 Hawks 數據                         | 爆      | Rambo        |
| \[Live\] 七六人 @ 溜馬                                  | 1       | Rambo        |
| \[Live\] 熱火 @ 超賽                                    | 3       | Rambo        |
| Re: \[新聞\] 本季最絕望球隊 籃網得第一                  | 5       | sasolala     |
| \[BOX \] Bulls 109:94 Bucks 數據                        | 31      | Rambo        |
| \[BOX \] Thunder 125:137 Rockets 數據                   | 爆      | Rambo        |
| \[BOX \] Kings 98:97 Clippers 數據                      | 46      | Rambo        |
| \[新聞\] Kobe的第1座銅像　竟然在中國廣州                | 25      | JAL96        |
| \[新聞\] 林書豪勇奪19分　籃網3月第7勝到手比騎士還厲害   | 75      | jay0601zzz   |
| \[Live\] 灰熊 @ 勇士                                    | 爆      | Rambo        |
| \[Live\] 鵜鶘 @ 金塊                                    | 12      | Rambo        |
| \[BOX \] Sixers 94:107 Pacers 數據                      | 12      | Rambo        |
| \[BOX \] Heat 108:112 Celtics 數據                      | 28      | Rambo        |
| \[討論\] 小蟲V.S.嘴綠                                   | 5       | lovero61108  |
| \[Live\] 拓荒者 @ 湖人                                  | 8       | Rambo        |
| \[專欄\] 騎士漏洞愈來愈多 衛冕軍狂拉警報LYS             |         | pneumo       |
| \[新聞\] 哈登魏少難割愛 Kobe支持「雙MVP」               | 爆      | pneumo       |
| \[BOX \] Pelicans 115:90 Nuggets 數據                   | 62      | Rambo        |
| \[討論\] 這幾場籃網的板凳有什麼改變                     | 30      | mimi8598     |
| \[花邊\] 老鷹主場球迷用屁股走路                         | 35      | jay0601zzz   |
| \[BOX \] Grizzlies 94:106 Warriors 數據                 | 爆      | Rambo        |
| \[情報\] 爵士鎖定季後賽位置                             | 19      | sthho        |
| Re: \[討論\] 這幾場籃網的板凳有什麼改變                 | 28      | lopopo001    |
| (本文已被刪除) \[sthho\]                                |         | -            |
| \[新聞\] 騎士內憂外患 東區龍頭快不保                    | 39      | jailkobe5566 |
| \[討論\] Booker將來能拿幾冠?                            | 2       | yenyu73      |
| \[情報\] Lue談防守：不能過早暴露我們的實力              | 39      | knic52976    |
| \[情報\] Ryan Anderson 腳踝扭傷將休養兩週               | 18      | thnlkj0665   |
| \[討論\] 書豪是不是其實真的蠻強的啊                     | 爆      | kiske011     |
| (本文已被刪除) \[sincerity37\]                          | 53      | -            |
| Re: \[討論\] 季後全力詹這說法是光彩的嗎？               | 15      | strmof22     |
| \[BOX \] Blazers 97:81 Lakers 數據                      | 38      | Rambo        |
| Re: \[討論\] 書豪是不是其實真的蠻強的啊                 |         | belief0816   |
| Re: \[討論\] 季後全力詹這說法是光彩的嗎？               | 7       | chxx         |
| Re: \[討論\] 書豪是不是其實真的蠻強的啊                 | X2      | c1236        |
| Re: \[討論\] 季後全力詹這說法是光彩的嗎？               | 4       | amaru03      |
| Re: \[討論\] 季後全力詹這說法是光彩的嗎？               | 27      | Shufflin     |
| \[新聞\] 林書豪19分射老鷹 籃網最近4戰3勝                | 9       | sinana       |
| \[討論\] 會慶幸勇士去年沒連霸嗎？                       | 15      | star1739456  |
| Re: \[討論\] 季後全力詹這說法是光彩的嗎？               | 13      | kyle5241     |
| \[討論\] 今日是否已經選出MVP了？                        | 49      | SongLa5566   |
| \[專欄\] 林書豪在家，籃網就是不同LYS                    | XX      | kingtseng    |
| \[討論\] 各位鍵盤GM會選誰                               | 20      | ZaneTrout    |
| Re: \[討論\] 季後全力詹這說法是光彩的嗎？               | 12      | wmigrant     |
| Re: \[討論\] 書豪是不是其實真的蠻強的啊                 | X4      | a125567365   |
| \[情報\] 快艇成賽季首支最後5分鐘贏18分卻輸球的          | 51      | Yui5         |
| \[專欄\] 帶傷上陣隱瞞所有人！Harden謊稱帶腕帶?          | 爆      | encorek01231 |
| \[討論\] Shawn Marion為什麼沒進過最佳防守陣容?          | 40      | Ayanami5566  |
| Re: \[討論\] Shawn Marion為什麼沒進過最佳防守陣容?      |         | YummyKidd    |
| \[情報\] 冷笑話：Harden輕鬆就能拿到40分，但他傳給了隊友 | 58      | bigDwinsch   |
| \[花邊\] Vanessa曝Kobe虛報身高，<U+8131>鞋只有195       | 45      | bigDwinsch   |
| \[新聞\] 拓荒者爬上老八 里拉德賽後爆「秘密武器          | 20      | adam7148     |
| \[新聞\] 勇士2天內碰火箭馬刺 柯爾：主力不輪休           | 34      | zzzz8931     |
| \[情報\] Harden單季兩千分且助攻隊友得到兩千分，         | 28      | vm04vm04     |
| \[公告\] 板規6.1                                        |         | kadasaki     |
| \[公告\] 違規檢舉區                                     | 爆      | kadasaki     |
| \[情報\] 2016-2017 例行賽 (3/27 - 4/3)                  | 70      | gap6060      |
| \[公告\] 2017 板主選舉                                  | 25      | kadasaki     |

解釋爬蟲結果
------------

``` r
#這是R Code Chunk

dim(totalPage)
```

    ## [1] 123   3

``` r
nrow(totalPage)
```

    ## [1] 123

``` r
str(totalPage)
```

    ## 'data.frame':    123 obs. of  3 variables:
    ##  $ Title  : Factor w/ 115 levels "\n\t\t\t\n\t\t\t\t[BOX ] Jazz 95:108 Clippers 數據\n\t\t\t\n\t\t\t",..: 1 7 19 8 5 20 6 17 14 4 ...
    ##  $ PushNum: Factor w/ 59 levels "10","12","21",..: 3 16 15 11 16 14 8 4 11 16 ...
    ##  $ Author : Factor w/ 77 levels "backere0720",..: 10 10 6 10 10 1 10 3 8 10 ...

共爬出幾篇文章標題? Ans: 2017/03/27抓到了122個標題('data.frame': 122 obs. of 3 variables)

``` r
#這是R Code Chunk

table(totalPage$Author)
```

    ## 
    ##  backere0720   bigDwinsch   DantesChen    dragon803       feyako 
    ##            1            4            1            1            1 
    ##    HANASUCIA    kingtseng   kyoiori100        lovea        Rambo 
    ##            1            2            1            1           28 
    ##     randy225       Wall62       yokann            -     adam7148 
    ##            1            1            1            5            3 
    ##   ccps970915     CCULaoDa   dameontree       ddd123      firstsg 
    ##            1            1            1            1            1 
    ##   h1212123tw        Ivers   js2a117573    knic52976      olively 
    ##            1            1            1            2            1 
    ##   ppeerrrryy     rukawa28       sscck5       tpc302     vm04vm04 
    ##            1            1            1            1            2 
    ##      whj0530  brandon0415    checktime     ej04cj86       fliesa 
    ##            1            1            2            1            1 
    ##     gt097231       huntai iam168888888      iso2288 jailkobe5566 
    ##            1            1            1            1            2 
    ##       lariat sampsonlu919   Tina741214    Turtle100    walkerold 
    ##            1            1            1            1            1 
    ##  whattheduck     zzzz8931        JAL96   jay0601zzz  lovero61108 
    ##            1            2            1            2            1 
    ##     sasolala   belief0816        c1236         chxx     kiske011 
    ##            1            1            1            1            1 
    ##    lopopo001     mimi8598       pneumo        sthho     strmof22 
    ##            1            1            2            1            1 
    ##   thnlkj0665      yenyu73   a125567365      amaru03  Ayanami5566 
    ##            1            1            1            1            1 
    ## encorek01231      gap6060     kadasaki     kyle5241     Shufflin 
    ##            1            1            3            1            1 
    ##       sinana   SongLa5566  star1739456     wmigrant         Yui5 
    ##            1            1            1            1            1 
    ##    YummyKidd    ZaneTrout 
    ##            1            1

``` r
max(table(totalPage$Author))
```

    ## [1] 28

哪個作者文章數最多？ Ans: 2017/03/27抓到的資料是Rambo有最多文章，有28篇。

有趣的現象 Ans: 以NBA看板為例，大約平均一天會有三頁資料，相當於每天有60筆資料。 我觀察到有趣的現象是大家好像比較少在別人的文章留言，都直接另外發一篇Re:XXXXX，可能大家喜歡自己當作者。
