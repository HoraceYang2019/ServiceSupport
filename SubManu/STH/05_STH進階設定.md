---
title: "5 智慧刀把- 進階設定說明"
chapter: 5
document: "智慧刀把操作說明書"
format: "MkDocs / AI-agent knowledge base"
---

# 5 智慧刀把- 進階設定說明

> 智慧刀把(smart tool holder, STH)內藏無線感測板(wireless sensing board,
> WSB)，使用時，STH透過Router採TCP/IP與機邊(Edge)
> 連線。機邊(Edge)可透過TCP/IP送出命令，STH將依據命令執行，並回傳訊息給機邊。
>
> 其中，智慧刀把有五種主要運作模式，分別為閒置、傳輸、設定、休眠與休眠喚醒模式，模式移轉如圖
> 64、智慧刀把模式切換所示。

<img src="media/image62.png"
style="width:6.201in;height:3.91989in"
alt="二代刀把-溝通協定 20230113_WSB狀態機 20230308.png" />

**圖 64、智慧刀把模式切換**

- 當電源供給且Reset後，STH進入閒置模式，此為未連線前的模式，用以檢測內部元件、電壓、與其他STH內部是否存在異常，燈號顯示如**表
  4**所示。

- 當在閒置與設定模式，且超過預定地設定時間、或收到休眠命令時，STH即進入休眠模式，。

- 當在設定模式且收到Edge連線，或在設定模式且收到傳輸命令，則進入傳輸模式，燈號顯示如**表
  4**所示。

- 當在休眠模式且感測到超過G值門檻之晃動，可從**休眠模式**離開，此時先進入**閒置模式**，待與Edge端連線完成後即可切回**傳輸模式**。G
  Sensor的靈敏度使用完整設定值(範圍1~63, default:4)。

- 在設定模式時，智慧刀把可設定的參數包含Router
  SSID、Password、IP、port、RF Power
  Level、G值門檻、polling間隔與休眠時間。

- **休眠喚醒模式:**設定polling間隔後，可讓WSB定時從**休眠模式**離開，並進入短暫的喚醒狀態。在此模式下會回報一次Header(封包序列號:99999)給Edge，Edge收到後可視需要回覆以下二種命令給WSB:

1\. 回覆**進入休眠模式**命令:讓WSB回到休眠模式。

2\. 回覆**進入閒置模式**命令:讓WSB進入閒置模式，即恢復正常啟動。

**表 4、智慧刀把模式燈號**

| **模式** | **狀態**             | **燈號 (RGB)**    |                 |                 |
|----------|----------------------|-------------------|-----------------|-----------------|
|          |                      | **Green**         | **Blue**        | **Red**         |
| **初始** | 初始化裝置           | \-                | \-              | \-              |
| **閒置** | 初始化完成           | 長亮5 (s)         | \-              | \-              |
|          | 正常，震動啟動未連線 | 50 (ms) / 1 (s)   |                 |                 |
|          | 裝置上電時偵測到異常 | \-                | \-              | 長亮            |
|          | 低電位               | \-                | \-              | 50 (ms) / 3 (s) |
| **休眠** | 裝置睡眠(休眠模式)   | \-                | \-              | \-              |
| **喚醒** | RTC啟動未連線        | 50 (ms) / 2.5 (s) |                 | \-              |
| **傳輸** | TCP 封包通道啟用     | \-                | 50 (ms) / 1 (s) | \-              |
| **設定** | TCP 封包通道啟用     | \-                | 長亮            | \-              |

## 5.1 連線設定

> 刀把網路設定S0與S1，S0為出貨預設，預設SSID:
> ST_route，Port:6500。S1設定為使用者設定，可利用設定模式設定。

1.  進入**傳輸模式**後，前預設30 (s)，STH使用S1設定。

2.  當等待預設30
    (s)內，STH一直未能以S1設定連線時，則自動改以S0設定連線，最大預設時間為等待30
    (s)。

3.  若在**傳輸模式**內，超過 60 (s)未連線，則進入**休眠模式。**

**表 5、智慧刀把連線設定**

|                     | **S0設定** | **S1設定**                    |
|---------------------|------------|-------------------------------|
| **Router SSID**     | ST_route   | ST_route\[1, 2.., n\]         |
| **Router Password** | 123456abc  | User defined                  |
| **連線埠 (Port)**   | 6500       | \[6501, 6502, …, 6510\]       |
| **Edge IP**         | 10.0.0.103 | \[10.0.0.104, …, 10.0.0.123\] |

## 5.2 模式切換

> **啟動模式:** 刀把在上電啟動與運作過程中，會動態檢測內部Sensor
> IC，當MCU檢測到與內部任一個Sensor
> IC出現連線問題時，智慧刀把會顯示紅燈。此時如果繼續使用，刀把在運作上可能會出現異常。當使用者發現異常燈號出現時，首先應確認刀把電源是否正常，並試著斷電重啟刀把，重啟之後如果依舊會出現異常燈號，應送回原廠進行確認維修。
>
> **休眠模式:**
>
> 啟動後進入休眠之狀態條件(進入休眠時間可設定，可調範圍20~255秒,
> default:30)

1.  加工/刀庫狀態TCP SOCKET通道斷線超過30秒(default)

2.  G sensor喚醒刀把/運送狀態無連router，超過60秒(default)

3.  在**設定模式下，**TCP SOCKET通道斷線超過30秒(default)

> **喚醒模式:**

1.  刀把在運送前，G
    Sensor設定值可設為角度喚醒(設定值64)，此模式下較不易藉由震動喚醒裝置，但只要刀把角度發生改變時(大於80°)則可以簡單地喚醒裝置。

2.  休眠模式喚醒，到連線router進入傳輸模式正常10秒內可以完成。

3.  透過晃動(超過G值門檻)即可喚醒智慧刀把。

> **設定模式:**

1.  可設定刀把的RF Power，提供不同Power Level可調(Level範圍 1~5,
    default: 2 ) (1: 5dBm , 2: 8.5dBm , 3: 13dBm , 4: 16.5dBm ,5:
    19.5dBm)

2.  polling間隔(可設定時間15 s
    ~1天，預設disable)，可在休眠模式下定時喚醒，此時狀態為休眠喚醒模式。在休眠喚醒模式下會固定連結設定1
    router，並定時回報電量等資訊，如果超過時間(休眠時間)未找到設定1
    router，則回去休眠模式。

### 5.2.1 傳輸模式

> **傳輸模式:** 傳輸模式可回饋天線強度(RSSI dBm)

**表 6、傳輸模式**

|     | **Function**     | **Edge Command**             | **WSB Response**           |
|-----|------------------|------------------------------|----------------------------|
| 1   | **進入設定模式** | cmd\n                        | Enter Configuration Mode\n |
|     |                  | **離開傳輸模式進入設定模式** |                            |

### 5.2.2 設定模式- 寫入

**表 7、設定模式- 寫入**

<table>
<colgroup>
<col style="width: 5%" />
<col style="width: 23%" />
<col style="width: 25%" />
<col style="width: 45%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th><strong>Function</strong></th>
<th><strong>Edge Command</strong></th>
<th><strong>WSB Response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td rowspan="2">1</td>
<td rowspan="2"><strong>回至傳輸模式</strong></td>
<td>exit\n</td>
<td>Exit Configuration Mode\n</td>
</tr>
<tr class="even">
<td colspan="2">設定離開設定模式回到傳輸模式</td>
</tr>
<tr class="odd">
<td rowspan="2">2</td>
<td rowspan="2"><strong>設定Router SSID</strong></td>
<td>ssid: ST_route \n</td>
<td>SSID setting “ST_route” OK\n</td>
</tr>
<tr class="even">
<td colspan="2">設定Router SSID為ST_route</td>
</tr>
<tr class="odd">
<td rowspan="2">3</td>
<td rowspan="2"><strong>設定Password</strong></td>
<td>pass:123456abc\n</td>
<td>Password setting “123456abc” OK\n</td>
</tr>
<tr class="even">
<td colspan="2">設定Router Password為123456abc</td>
</tr>
<tr class="odd">
<td rowspan="2">4</td>
<td rowspan="2"><strong>設定IP</strong></td>
<td>ip:1.1.1.102\n</td>
<td>IP setting “1.1.1.102” OK\n</td>
</tr>
<tr class="even">
<td colspan="2">設定IP為1.1.1.102</td>
</tr>
<tr class="odd">
<td rowspan="2">5</td>
<td rowspan="2"><strong>設定port</strong></td>
<td>port:6500\n</td>
<td>Port setting “6500” OK\n</td>
</tr>
<tr class="even">
<td colspan="2">設定port為6500</td>
</tr>
<tr class="odd">
<td rowspan="2">6</td>
<td rowspan="2"><strong>設定RF Power Level</strong></td>
<td>power:3\n</td>
<td>RF TX Power setting “3” OK\n</td>
</tr>
<tr class="even">
<td colspan="2">1~5, default: 2; (5, 8.5, 13, 16.5, 19.5) dBm</td>
</tr>
<tr class="odd">
<td rowspan="2">7</td>
<td rowspan="2"><strong>設定喚醒</strong><strong>G值門檻</strong></td>
<td>gsensor:10\n</td>
<td>G-Sensor setting “10” OK\n</td>
</tr>
<tr class="even">
<td colspan="2"><p>設定G-Sensor靈敏度為10 (範圍1~64,default:4)</p>
<ul>
<li><p>設定值1~63:震動模式靈敏度</p></li>
<li><p>設定值64:角度喚醒(80°)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td rowspan="2">8</td>
<td rowspan="2"><strong>設定休眠時間</strong></td>
<td>ctime:60\n</td>
<td>ctime setting “60” OK\n</td>
</tr>
<tr class="even">
<td colspan="2">設定休眠時間為60s(範圍20~255s ,default:30s)</td>
</tr>
<tr class="odd">
<td rowspan="2">9</td>
<td rowspan="2"><strong>設定polling間隔</strong></td>
<td>ptime:8\n</td>
<td>ptime setting “8” OK\n</td>
</tr>
<tr class="even">
<td
colspan="2"><p>設定休眠時ptime設定為8(設定值範圍0~5760,default:0)</p>
<ul>
<li><p>設定值0:休眠時不進行定時polling</p></li>
<li><p>設定值1~5760:休眠間隔(基本單位15s)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td rowspan="2">10</td>
<td rowspan="2"><strong>進入休眠模式</strong></td>
<td>sleep\n</td>
<td>Enter Sleep Mode\n</td>
</tr>
<tr class="even">
<td colspan="2">設定離開設定模式進入休眠模式</td>
</tr>
</tbody>
</table>

### 5.2.3 設定模式- 讀取

**表 8、設定模式- 讀取**

|     | **Function**           | **Edge Command**                                                                                        | **WSB Response**     |                                      |
|-----|------------------------|---------------------------------------------------------------------------------------------------------|----------------------|--------------------------------------|
| 1   | **讀取Router SSID**    | rssid\n                                                                                                 | rssid:設定值\n       |                                      |
|     |                        | 讀取Router SSID                                                                                         |                      |                                      |
| 2   | **讀取Password**       | rpass\n                                                                                                 | rpass:設定值\n       |                                      |
|     |                        | 讀取Router Password設定值                                                                               |                      |                                      |
| 3   | **讀取IP**             | rip\n                                                                                                   | rip:設定值\n         |                                      |
|     |                        | 讀取IP設定值                                                                                            |                      |                                      |
| 4   | **讀取port**           | rport\n                                                                                                 | rport:設定值\n       |                                      |
|     |                        | 讀取port設定值                                                                                          |                      |                                      |
| 5   | **讀取RF Power Level** | rpower\n                                                                                                | rpower:設定值\n      |                                      |
|     |                        | 1~5, default: 5; (5, 8.5, 13, 16.5, 19.5) dBm                                                           |                      |                                      |
| 6   | **讀取G值門檻**        | rgsensor\n                                                                                              | rgsensor:設定值\n    |                                      |
|     |                        | 讀取G-Sensor靈敏度                                                                                      |                      |                                      |
| 7   | **讀取休眠時間**       | rctime\n                                                                                                | rctime:設定值\n      |                                      |
|     |                        | 讀取休眠時間                                                                                            |                      |                                      |
| 8   | **讀取polling間隔**    | rptime\n                                                                                                | rptime:設定值\n      |                                      |
|     |                        | 讀取polling間隔                                                                                         |                      |                                      |
| 9   | **讀取電壓值**         | rbat\n                                                                                                  | rbat:實際電壓值\n    |                                      |
|     |                        | 讀取目前電池電壓                                                                                        |                      |                                      |
| 10  | **讀取訊號強度**       | rRSSI\n                                                                                                 | rRSSI:接收訊號強度\n |                                      |
|     |                        | 讀取目前接收訊號強度                                                                                    |                      |                                      |
| 11  | **讀取程式版本**       | rVER\n                                                                                                  |                      | rVER:\<M\>核心1版本,\<E\>核心2版本\n |
|     |                        | 讀取目前WSB兩個核心的程式版本ex: rVER:\<M\>01.11,\<E\>02.03                                             |                      |                                      |
| 12  | **繼續同步**           | syn\n                                                                                                   | syn:OK\n             |                                      |
|     |                        | 設定模式為2分鐘timeout，機邊(Edge)如不能在2分鐘傳設定資料，要傳syn給無線感測板(WSB)否則會被視為通道斷線 |                      |                                      |

### 5.2.4 休眠模式

> 以超過G值門檻之晃動，即可切回傳輸模式。
>
> 休眠喚醒模式:

**表 9、休眠設定**

|     | **Function**     | **Edge Command**             | **WSB Response**   |
|-----|------------------|------------------------------|--------------------|
| 1   | **進入休眠模式** | sleep\n                      | Enter Sleep Mode\n |
|     |                  | 離開休眠喚醒模式進入休眠模式 |                    |
| 2   | **進入閒置模式** | exit\n                       | Enter Idle Mode\n  |
|     |                  | 離開休眠喚醒模式進入閒置模式 |                    |

在傳輸模式下，機邊(Edge)接收STH後，可發現接收之資料可區分成兩群，分別為Header與Content，Header標記MAC傳輸時間等，而Content紀錄4頻道資料。
