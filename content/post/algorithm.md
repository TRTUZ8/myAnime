+++
date = '2026-04-24T13:15:00+08:00'
draft = false
title = '一些code筆記'
categories = ['心得']
tags = ['刷題筆記']
cover = './images/4.webp'
+++
## 前言
hi, 我是kaguya的狗, 我最喜歡kaguya了  
  
這邊主要會存放我在每日leetcode學習到的STL語法，可能會再加上一點演算法、資料結構, 如果有順便幫助到你就太好啦~ 

[每日挑戰leetcode的直播紀錄](https://www.youtube.com/playlist?list=PLZQoNSFaP4xyRC8JU61I62KtraqENp5NK)
## 服用注意事項

我的筆記可能沒有寫到該演算法的精隨、或是有寫錯誤的地方。  
畢竟我在寫這個算法的筆記目前都是從leetcode題目上學習的  
也就是說這個演算法可能有非常多的妙用，但這個題目只需要懂這個觀念，我就只會寫這個部分。(待價而沽的現實)  
嘛，不過當看的題目越來越多，筆記也會越來越詳細、涵蓋越來越多的觀念就是。

範例程式皆使用 C++ 示範


## 宣告技巧
### 陣列初始化 iota
初始化陣列可以直接使用iota，讓他為從 0 開始的連續整數  
省得用for再去初始化
```cpp
vector<int> v(5, 0) //初始化為[0, 0, 0, 0, 0]
std::iota(v.begin(), v.end(), 0) // 會變成[0,1,2,3,4]

```

## 並查集Disjoint Set (Union-Find) 2026-04-26更新
主要是在處理 set 合併上非常的高效  

一開始沒用disjoint Set，我怎麼合併兩個Set?
```cpp
// (錯誤示範)
set<int> A, B; //兩個set A 與 B
for (auto& i : B) { //將 set B 中每個值都丟給 A
    A.insert(i);
}
B.clear(); //清空 B 的元素
```
但這樣做非常的慢，所以我們才需要 Disjoint Set Union這個資料結構幫助我們
```cpp
vector<int> parent{0, 1, 2, 3, 4, 5} //初始化，可以用iota去初始化大小為n的
//parent[0] = 0 代表 0 的 parent 為 0 也就是他自己 (這代表 0 是一個 set 的 root)
//之後看parent[1] = 1, parent[2] = 2....也都是自己 (畢竟這是初始化，每個元素自己就是一個 set)
//當我們需要將兩個集合合併，譬如要合併[0, 1]
//我們要做的是找出 0 與 1 的parent是誰，然後讓其中一個 root 指向另一個 root 
//所以要合併之前，我們必須要找到 0 與 1 的 parent 是誰，
int find(int x) {//這邊假設 parent 是全域變數
  if (parent[x] != x) parent[x] = find(parent[x]); //這邊其實同時有做路徑壓縮 (請自行研究)
  return parent[x]; //最後我們就獲得了 index 為 x 的 parent 所在地(parent的index)
}
//怎麼讓 0 的 parent 接到 1 的 parent呢?
//透過find(x) 我們是拿到 x parent 的 index
//也就是說 parent[find(x)] = find(x) (root特性)
//接下來我們就只要執行 parent[find(0)] = find(1)就好，這樣就接上拉
void merge(int a, int b) {
  parent[find(a)] = find(b);
}
//你可能有的小疑惑: 為什麼只有find(a)要再套上一層parent
//因為我們修改的是parent[rootA]的值，而find(b)已經回傳了rootB的值
//原本: parent[rootA] = rootA; 更改後: parent[rootA] = rootB; 合併完成
```
當然以上只是最基本的DSU操作  
更多技術細節請自行研究 

[leetcode練習]  
[1722. Minimize Hamming Distance After Swap Operations](https://leetcode.com/problems/minimize-hamming-distance-after-swap-operations/description/)

[參考網站]   
https://hackmd.io/@ShanC/dsu  
https://web.ntnu.edu.tw/~algo/Set.html

## 老婆圖
kaguya我婆，最喜歡kaguya了。
![image](../../images/4.webp)