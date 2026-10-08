---
title: "7 異常排除"
chapter: 7
document: "智慧刀把操作說明書"
format: "MkDocs / AI-agent knowledge base"
---

# 7 異常排除

異常排除包含電力異常、連線異常、與資料異常等現象、原因與排除方法，分述如下。

## 7.1 電力異常問題

<table>
<colgroup>
<col style="width: 7%" />
<col style="width: 92%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>1</strong></th>
<th><strong>搖晃刀把後沒有燈號顯示</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td
colspan="2"><p>休眠模式(無燈號)下，搖晃刀把即可進入閒置模式(綠燈閃爍)，如果搖晃刀把後沒有顯示燈號，則刀把處於休眠喚醒模式，這時請接上充電座。</p>
<p><img src="media/image79.png"
style="width:1.26562in;height:1.68633in" /></p></td>
</tr>
<tr class="even">
<td
colspan="2"><p>A.將刀把連接上充電座，充電正常時，充電座會長亮紅燈</p>
<p>B.待刀把充電完成後，充電座會長亮綠燈，便可取下刀把</p>
<p>C.搖晃刀把後進入閒置模式(綠燈閃爍)，這時可以正常使用</p>
<p>D.一段時間無動作，則刀把會進入休眠模式(無燈號)</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 7%" />
<col style="width: 92%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>2</strong></th>
<th><strong>刀把接上充電座後，充電座沒有燈號顯示</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td
colspan="2"><p>正常情況下刀把接上充電座後，充電座會顯示紅燈代表充電中，如果沒有顯示燈號，可能是充電接點未貼合或變壓器不符合規格以及充電座故障。</p>
<p><img src="media/image80.png"
style="width:2.28571in;height:1.67457in" /></p></td>
</tr>
<tr class="even">
<td
colspan="2"><p>A.檢查充電座的充電接點是否正確貼合智慧刀把的充電接點</p>
<p>B.檢查充電座的變壓器是否符合要求，變壓器輸出電壓應為DC12V，輸出電流應為2A</p>
<p>C.更換為要求之變壓器後，如果還是無法充電，則可能是充電座本身故障，請聯絡採購單位進行維修服務</p></td>
</tr>
</tbody>
</table>

## 7.2 連線異常問題

智慧刀把無法連線時，請先依異常情境參考對應問題：「3 執行 LOAD
STHSCAN（掃描功能）後，沒有顯示可用刀把」或「4 Available STHs
有顯示可用刀把，但 LOAD ALL 無法連接」。

<table>
<colgroup>
<col style="width: 7%" />
<col style="width: 92%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>3</strong></th>
<th><strong>執行LOAD
STHSCAN(掃描功能)後，後沒有顯示可用刀把</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td colspan="2"><p><a href="#LOADSTHSCAN"><strong>LOAD
STHSCAN(載入STH掃描程序)</strong></a>執行後，正常情況下會顯示刀把的MAC和Port號，如果沒有顯示可用刀把，請參考以下情況排除錯誤。</p>
<p><img src="media/image81.png"
style="width:6.89028in;height:0.67014in" /></p></td>
</tr>
<tr class="even">
<td
colspan="2"><p>A.先確認刀把狀態，搖晃刀把後進入閒置模式(綠燈閃爍)</p>
<p>B.檢查<strong>連線檢查</strong>中的設定是否正確，<strong>Networking(TCP/IP設定)</strong>及<strong>MessageBroking(MQTT設定)</strong>中的各項設定如下圖所示</p>
<p><img src="media/image37.png"
style="width:6.89028in;height:1.18958in" /></p>
<p>C.檢查<strong>設定IP與Router位置</strong>，IP位址為10.0.0.103，子網路遮罩為255.255.255.0</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 8%" />
<col style="width: 91%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>4</strong></th>
<th>Available STHs 有顯示可用刀把，但 LOAD ALL 無法連接</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td colspan="2"><p><a href="#AvailableSTHs"><strong>Available
STHs(目前可用智慧刀把)</strong></a>正常顯示可用刀把，但是<a
href="#LOADALL"><strong>LOAD
ALL(載入所有)</strong></a>無法連接上刀把。正常情況會像<a
href="#日誌顯示"><strong>日誌顯示(Logs)</strong></a>，持續顯示Target
MAC、Port號等訊息，錯誤時則如下圖情形。</p>
<p><img src="media/image82.png"
style="width:5.1012in;height:1.20409in" /></p></td>
</tr>
<tr class="even">
<td
colspan="2"><p>A.檢查<strong>設定計畫需要綁定的智慧刀把與刀具</strong>的MAC與刀具編號，如下圖所示STH1、STH2等刀把的MAC與刀具編號</p>
<p><img src="media/image83.png"
style="width:6.89028in;height:1.36319in" /></p>
<p>B<strong>.</strong>確認<strong>智慧刀把與刀具綁定</strong>有完成，使用此按鈕來綁定智慧刀把的MAC與刀具編號</p>
<p><img src="media/image84.png"
style="width:5.71676in;height:2.68091in" /></p></td>
</tr>
<tr class="odd">
<td colspan="2"><p>C. 確認<strong>儲存設定</strong>的<a
href="#APPLYUPDATES"><strong>APPLY
UPDATES(應用更新)</strong></a>按鈕是否有點擊</p>
<p>D.應用更新後確定<strong>啟用的智慧刀把(Active
STH)</strong>有MAC號，如下圖</p>
<p><img src="media/image40.png"
style="width:5.15972in;height:0.48403in" /></p></td>
</tr>
</tbody>
</table>

## 7.3 資料異常問題

<table>
<colgroup>
<col style="width: 9%" />
<col style="width: 90%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>5</strong></th>
<th><strong>刀具過度磨損或損壞</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td
colspan="2"><p>當刀具過度磨損或是刀具有損壞時，模擬分析會觀察到Torque(Nm)資料顯示異常，會超過上與下管制界線(UCL/LCL)，請更換其他刀具進行加工。</p>
<p><img src="media/image85.png"
style="width:6.89028in;height:3.45069in" /></p></td>
</tr>
<tr class="even">
<td colspan="2"><p>A.跳到即時監控頁面</p>
<p>B.執行<a href="#TOOLCHANGE"><strong>TOOL
CHANGE(換刀)</strong></a>，進行換刀的動作</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 9%" />
<col style="width: 90%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>6</strong></th>
<th><strong>Node Red服務暫停、網站無回應</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td colspan="2"><p>當發現Node
Red網站無回應，可以前往工作管理員的服務，檢查Node-Red狀態，如是已暫停，且啟動沒有動作，到命令提示字元(CMD)下，啟動Node-Red，如果有問題會顯示如圖畫面。</p>
<p><img src="media/image86.png"
style="width:6.89028in;height:2.69444in" /></p>
<p>看到Failed to stary
server，下方紅框有指出有問題的.json檔案，複製該行位置將檔案刪除或剪下到別的位置，後重新使用命令提示字元(CMD)啟動Node-Red
服務並重新啟動電腦就能正常運行了。</p></td>
</tr>
</tbody>
</table>
