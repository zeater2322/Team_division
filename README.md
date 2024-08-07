# 籃球員分隊偵測
## 目標
能夠針對不同的比賽的球員、籃球以及籃框進行偵測並對兩隊球員有判斷隊伍的功能
## 資料
為了訓練我的自定義模型，我和組員在 youtube 上擷取了含影像增強共1285張籃球比賽的圖片，並使用 Roboflow 標記了球員、籃球以及籃框這是我用於訓練模型的所有數據。
## 流程和代碼
第一步是在我的自定義類上訓練 YOLO 物件檢測模型，分別有球員、籃球以及籃框三個類，但是訓練集太大了所以沒有放上來。
訓練結果還不夠好，有時會把裁判也當成球員


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
