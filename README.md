# Jim_TASA_Monopulse
## step1. 符號定義
- \[ P_o \] 為我們收到的訊號

\( P_o = \frac{1}{2} \left( P_{\Sigma} + P_{\Delta} + 2 \sqrt{P_{\Sigma} \cdot P_{\Delta}} \cos(\phi) \right) \)

- $$ P_{\Sigma} $$ 代表 Sum port power
- $ P_{\Delta} $ 代表 Difference port power
- $ \phi $ 是兩路間相位差

$ \phi = \phi_o + \phi_t + \phi_i $

- $ \phi_o $ : $ \Sigma 和 \Delta $ 線路相位差
- $ \phi_t $ : 目標物極座標投影的角度
- $ \phi_i $ :  相位偏移器設定相位角度

## step2. 校正後找出 $ \phi_o $
1. 將天線對準衛星後，往自定義的0度方向做移動（表示 $ \phi_t =0 $）
2. 切換 phase shifter 觀察 AM 或 RSSI 訊號
3. 找出 phase shifter 在幾度時會有最大值 $ \phi $ = 0&deg;
4. 同上 找出 phase shifter 在幾度時會有最小值 $ \phi $ = 180&deg;

## Step3. 設定 $ \phi_i $
1. $ \phi_i $ 為自定義
2. 自定義 0&deg; 90&deg; 180&deg; 270&deg;
3. 用 i = 1, 2, 3, 4 取代 看起來更簡潔
4. $ \phi_i = \phi_o + (i-1) \times 90^\circ , \quad i = 1, 2, 3, 4 $
5. 經由以上算式，我們的$ \phi $ 簡化成以下
6. $ \phi = \phi_t + (i-1) \times 90^\circ , \quad i = 1, 2, 3, 4 $
7. 經過以上簡化後，我們的 $ \phi $ 只剩下 ($\phi_t$ , i) 兩個變數

## Step4. 計算收到的訊號功率P

$ P_i = \frac{1}{2} \left( P_{\Sigma} + P_{\Delta} + 2 \sqrt{P_{\Sigma} \cdot P_{\Delta}} \cos(\phi_i) \right) ,\quad  \Phi_i = \Phi_t + (i-1) \frac{\pi}{2} , \quad i = 1, 2, 3, 4 $

帶入 \( i = 1, 2, 3, 4 \) 的結果如下：

### 方程式:
$ 
P_1 = \frac{1}{2} \left( P_{\Sigma} + P_{\Delta} + 2 \sqrt{P_{\Sigma} \cdot P_{\Delta}} \cos(\phi_t) \right)
$

$ 
P_2 = \frac{1}{2} \left( P_{\Sigma} + P_{\Delta} - 2 \sqrt{P_{\Sigma} \cdot P_{\Delta}} \sin(\phi_t) \right)
$

$ 
P_3 = \frac{1}{2} \left( P_{\Sigma} + P_{\Delta} - 2 \sqrt{P_{\Sigma} \cdot P_{\Delta}} \cos(\phi_t) \right)
$

$ 
P_4 = \frac{1}{2} \left( P_{\Sigma} + P_{\Delta} + 2 \sqrt{P_{\Sigma} \cdot P_{\Delta}} \sin(\phi_t) \right)
$

經整理可得合併後的方程式：

1. $ P_{\Sigma} + P_{\Delta} = P_1 + P_3 = P_2 + P_4 $

2. $ P_{\Sigma} \cdot P_{\Delta} = \frac{1}{16} \left[ (P_1 - P_3)^2 + (P_4 - P_2)^2 \right] $

3. $ \frac{P_4 - P_2}{P_1 - P_3} = \tan(\phi_t) $

因此可解出 $ P_{\Sigma} ,\quad P_{\Delta} ,\quad \phi_t $

# 結論

## A. 目標誤差角度 $ \theta_t $ 計算方式

## $ \theta_t = k_t \cdot \left( \frac{P_{\Delta}}{P_{\Sigma}} \right) $
PS. 其中 $ k_t $ 可由模擬或實測得到

## B. 方位 $ \phi_t $ 計算方式

$ \phi_t = \tan^{-1} \left( \frac{P_4 - P_2}{P_1 - P_3} \right) $

