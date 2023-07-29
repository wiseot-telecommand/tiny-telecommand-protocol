# Tiny Telecommand Protocol

* GitHub: https://github.com/organizations/wiseot-telecommand
* Documnet cowork space: https://hackmd.io/O3lCv-mjRCqyXWIiKUmNUw?view

---
## 1. 概觀

"(Tiny) Telecommand"，是 Wise OT 團隊的寫作業、OJT 專案。起因為因應 IoT end-device 的監測、遙測需求，和為了整合、開發 IoT 開源平台的技術基本功做準備，因此建立的寫作業，職前 / 在職訓練用專案。因此為了 "體驗開發" IoT 通訊，亦建立了本專案，與作業用的 Tiny Telecommand Protocol。

---
## 2. Protocol 設計

### 目標

讓遙測、與被遙測端系統，可以用文件 (config) 來定義 command 的實作，實現執行階段調整 command 功能，與 machine to machine 通訊的能力。例如遙測端可在執行階段，動態從被遙測端，取得 "如何下指令" 的資訊。

### Telecommand 定義文件

* v0.0.2 *(2023/07/30)*
* Content type: text/JSON

#### Schema

```
{
    "device": "{identity name}",
    "version": "{display name}",
    "revision": "{machine read name}",
    "description": null|{text},
    "commands":
    {
        "{command name}":
        {
            "executor":
            {
                "type":"ignore|method|subprocess|expression",
                "content": null|"{text}",
            },
            "attributes":
            {
                "{name}":
                {
                    "immutable": true|false,
                    "content": <any>,
                    "description": null|{text}
                }
            },
            "parameters":
            {
                "{name}":
                {
                    "required": true|false,
                    "type": "{JSON data type}",
                    "default": null|{content},
                    "description": null|{text}
                }
            }
        }
    }
}
```
#### Executor object

定義被遙測端，在收到指令後，要如何實作、執行指令。

* ``type``:``string``
    * ``ignore``: 尚未實作、忽略指令
    * ``method``: 執行內部函式
    * ``subprocess``: 執行系統指令、外部程式
    * ``expression``: 執行運算式計算，或是 script
* ``content``:``string`` -- 對應至 executor type 的內容

#### Attributes and object

定義 command 的屬性。

* ``immutable``:``boolean`` -- 是否為唯讀屬性
* ``content``:``string`` -- 屬性內容
* ``description``:``null``|``string`` -- 文字描述

#### Parameters and object

定義 command 的參數，資料型態等。
    
* ``required``:``true``|``false`` -- 是否為必要參數
* ``type``:``string`` -- 參數的資料型態
* ``default``:``Any`` -- 參數的預設值
* ``description``:``string`` -- 文字描述

### 指令與回應格式定義

#### 送出指令

此部分留給 office hour / 作業討論。

#### 同步回應

此部分留給 office hour / 作業討論。

#### 非同步回應 schema

此部分留給 office hour / 作業討論。

#### 推播 (notification) 回應 schema

此部分留給 office hour / 作業討論。


---
## 3. API 設計

此部分留給 office hour / 作業討論。

---
## 4. 設計與實作討論

### Command

#### Attributes

##### ``timed_out``

* ``immutable``:``boolean``
* ``content``:``true``|``false``
* ``description``:``string`` -- "time-limited for command executing (seconds)"

#### Parameters

##### ``timed_out``

* ``required``:``true``|``false``
* ``type``:``boolean``
* ``default``:``true``|``false``
* ``description``:``string`` -- "time-limited for command executing (seconds)"


### API

#### 技術選型

此部分留給 office hour / 作業討論。

#### Clean Architecture 與 Command 元件的 reuse

此部分留給 office hour / 作業討論。
