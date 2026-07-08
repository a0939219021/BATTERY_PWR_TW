# BATTERY_PWR_TW — 藍牙車用電源控制器 Web BLE App

透過 Web Bluetooth 控制 BMF 板（CC2340R5 + BTS50007 高邊開關）的電源輸出。

## 使用方式

- **iPhone / iPad**：用 [Bluefy](https://apps.apple.com/app/bluefy-web-ble-browser/id1492822055) App 開啟
  `https://a0939219021.github.io/BATTERY_PWR_TW/`
- **Android / PC**：用 Chrome 開啟同一網址（需 HTTPS，本頁由 GitHub Pages 提供）

按「連線」→ 選擇 **BMF_POWER** 裝置 → 按中央電源鈕切換 ON/OFF。

## BLE 協議

| 項目 | 值 |
|---|---|
| 廣播名稱 | `BMF_POWER` |
| Service | `0xFFB0` |
| Characteristic | `0xFFB1`（Read / Write / Notify，1 byte） |
| 指令 | `0x01` = 電源 ON，`0x00` = 電源 OFF |

韌體端（BMF_EXT / CC2340R5）收到 ON 時會對 BTS50007 EN（DIO13）做 150ms 重觸發脈衝後保持高電位；OFF 則拉低。

## 對應硬體

- 板子：BMF（VBAT 12V 車電輸入 → LMR36506 buck → 3.3V；BTS50007 高邊開關輸出）
- 韌體專案：CCS 工作區 `BMF_EXT`（TI SimpleLink F3 SDK, FreeRTOS + BLE）
