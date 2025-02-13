# 籃球員分隊偵測
人眼能直接看場上的球員的球衣或是動作來判斷誰是哪一隊的，但是要怎麼讓電腦也能判斷?
我們嘗試利用自己標註的資料訓練成的自訂義yolo模型來做這件事
## 目標
能夠針對不同的比賽的球員、籃球以及籃框進行偵測並對兩隊球員有判斷隊伍的功能
## 資料
為了訓練我的自定義模型，我和組員在 youtube 上擷取了含影像增強共1285張籃球比賽的圖片，

並使用 Roboflow 標記了球員、籃球以及籃框這是我用於訓練模型的所有數據。

## 流程和代碼
第一步是在我的自定義類上訓練 YOLO 物件檢測模型，分別有球員、籃球以及籃框三個類，但是訓練集太大了所以沒有放上來。

(訓練結果還不夠好，有時會把裁判也當成球員)

最初我們用resnet來取特徵，但是分群效果很不理想

因為取得的特徵可能不只是顏色，也有可能是球員的動作，還有可能是標註資料的背景影響

所以我們換成HSV提取顏色特徵

接著取中心圓點(如下圖，只取重要部分來提升準確率)

![](https://github.com/zeater2322/Team_division/blob/master/mask.png)

利用 HSV 圖像的顏色直方圖取特徵並且進行正規化處理

再利用層次聚類來根據特徵做分類(分隊)

為了防止每幀的偵測導致所有A隊球員在下一幀變成B隊，而B隊變成A隊(因為AB分隊為隨機)

儲存並計算A隊和B隊各自的特徵平均

並與下一幀的AB隊特徵平均做歐基里斯距離計算來找到前後幀最相近特徵

最後結合tkinter做介面，包括播放暫停之外還有進度條等等功能，結果如下

!!注意右邊按鈕 可以選擇要顯示或隱藏偵測框或是準確率!!

![](https://github.com/zeater2322/Team_division/blob/master/test_short.gif)
## 利用技術/語言
- 語言:

    Python

- 圖形使用者介面（GUI）:

    Tkinter

- 影像處理和顯示:

    OpenCV / 
    PIL (Python Imaging Library)

- 深度學習模型:

    PyTorch / 
    torchvision / 
    YOLO (You Only Look Once)

- 影像預處理和轉換:

    torchvision.transforms

- 聚類和一致性標籤:

    Scipy (linkage, fcluster, linear_sum_assignment) / 
    sklearn.preprocessing (normalize)

- 數據結構和計算:

    Numpy
    Collections (deque)

- 多執行緒處理:

    threading

- 可視化:

    Matplotlib
