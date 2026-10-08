---
title: "2 智慧刀把簡介"
chapter: 2
document: "智慧刀把操作說明書"
format: "MkDocs / AI-agent knowledge base"
---

# 2 智慧刀把簡介

> 本章簡介智慧刀把(Smart Tool Holder,
> STH)之應用架構、通用規格、認證規範、與充電模組規格等。智慧刀把應用架構，如圖4所示，單機CNC內的智慧刀把感測訊號，可透過2.4G
> Wi-Fi經由無線路由器(Router)連接至機邊(Raspberry RPI/OT) ;
> 機邊經由有線網路，經由路由器連接至Edge PC 圖形化操作軟體。Edge PC
> 圖形化操作軟體除了透過控制器的通訊介面(如OPC/UA)與CNC控制器同步，截取CNC當下的狀態、座標、NC與設定等，並藉由MQTT通訊協定，對各機台上的機邊進行統一的控制與管理。MQTT負責智慧刀把與虛擬刀房(Virtual
> Tool Room,
> VTR)之間的數據通訊；機邊負責對接智慧刀把，並對其感測訊號進行解析、轉換、儲存、處理與比較，解析後的特徵資料會被自動儲存，以作為後續數據分析與異常檢測的基礎。

在應用上，機邊可透過MQTT將感測摘要發佈給Edge PC 。此外，藉由Edge PC
提供的虛擬刀房(VTR)，除可設定加工計畫，顯示當下的智慧刀把狀態與加工訊號，更可設定管制界線，並進行離線分析等。

<img src="media/image7.png"
style="width:6.63279in;height:4.24894in" />

**圖 4、智慧刀把應用架構**

## 2.1 通用規格

**表 2、智慧刀把通用規格**

| ** **        | **項目**            | **Smart Tool Holder- Turing-E** |
|--------------|---------------------|---------------------------------|
| **訊號特性** | **訊號取樣率 (Hz)** | up to 3.6kHz/per channel        |
|              | **偵測項目**        | Fx, Fy, Mz                      |
|              | **精密度**          | ±3%                             |
| **通訊架構** | **通訊方式**        | Wi-Fi                           |
|              | **通訊頻帶**        | 2.45 GHz 802.11 b/g/n           |
| **電力供給** | **持續操作 (hr)**   | \>6                             |
|              | **待機時間 (day)**  | \>10                            |
| **機械特性** | **防水防塵等級**    | IP67                            |
|              | **充電方式**        | 接觸充電                        |
|              | **最大轉速 (rpm)**  | G1/15,000                       |
| **軟體特性** | **受力監控**        | 線上監控                        |
|              | **刀具磨耗推估**    | Option                          |
|              | **系統整合功能**    | Option                          |

**  
**

## 2.2 測試規範(符合性測試)

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 83%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>分類</strong></td>
<td><strong>測試規範/條件</strong></td>
</tr>
<tr class="even">
<td><strong>RF</strong></td>
<td>EN300328, 台灣LP0002, FCC 15C</td>
</tr>
<tr class="odd">
<td><strong>EMC</strong></td>
<td><p>FCC 15B, EN301489-1, EN301489-17</p>
<p>重工業設備: IEC/EN61000-6-2 (EMS, Immunity), IEC/EN61000-6-4 (EMI,
Emission)</p>
<p>IEC61000-4-2 (ESD Test)</p></td>
</tr>
<tr class="even">
<td rowspan="2"><strong>Safety</strong></td>
<td><p>EN62311(EMF)</p>
<p>充電器: EN 62368</p>
<p>電池的Cell &amp; Pack: IEC/EN 62133-2:2017、UN 38.3</p></td>
</tr>
<tr class="odd">
<td><p>Machinery Directive 2006/42/EC</p>
<p>EN ISO 12100</p></td>
</tr>
<tr class="even">
<td><strong>Function</strong></td>
<td>IEC 60529-IP67 (防水防塵)</td>
</tr>
<tr class="odd">
<td><strong>Environment</strong></td>
<td>RoHS</td>
</tr>
</tbody>
</table>

## 2.3 充電模組

> 燈號如表 3、智慧刀把充電座燈號，充電時注意變壓器確實插入如圖
> 5、充電器Adapter位置所示，夾持方向如圖 6、充電座夾持方式。

**表 3、智慧刀把充電座燈號**

| **狀態**   | **燈號** |     |
|------------|----------|-----|
|            | Green    | Red |
| **未充電** | \-       | \-  |
| **充電中** | \-       | On  |
| **充飽電** | On       | \-  |

<img src="media/image8.png"
style="width:2.11458in;height:2.3125in" />
<img src="media/image6.png"
style="width:1.82074in;height:1.03657in" />

**圖 5、充電器Adapter位置，圖左V**1**，圖右V**2

<img src="media/image9.png"
style="width:3.41509in;height:2.36181in" />

**圖 6、充電座夾持方式**

**  
**

| **Item**                          | **Specifications**                 |
|-----------------------------------|------------------------------------|
| **Operating Temperature**         | 0’C~50’C                           |
| **Storage Temperature**           | -10’C~60’C                         |
| **Input Voltage**                 | DC 12V                             |
| **Max. Input Current**            | 2A                                 |
| **Max. Charging Current**         | 2A                                 |
| **Charging CC mode**              | 2A                                 |
| **Charging CV mode**              | MAX 8.5V                           |
| **Adapter Input Specifications**  | Vac 100V~240V- 50/60Hz-0.5A        |
| **Adapter Output Specifications** | DC 12V-2A                          |
| **Max. Charging Time**            | 2hr                                |
| **Battery life - Activity**       | ≧ 6hr                              |
| **Battery life - Standby**        | ≧ 10 days                          |
| **Charging state-LED**            | 未充不亮/充電中紅燈亮/充飽電綠燈亮 |
