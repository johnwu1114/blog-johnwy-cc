---
title: 'ASP.NET Core 3 系列 - 從頭開始'
author: John Wu
tags:
  - ASP.NET Core
  - ASP.NET Core 3
  - VS Code
categories:
  - ASP.NET Core
date: 2019-10-23 23:12
featured_image: /images/b/45.png
---

自九月推出 .NET Core 3.0 正式版後，最近終於開始把產品從 .NET Core 2 開始升級到 .NET Core 3.0。  
之前寫的 [ASP.NET Core 2 系列文章](/tags/it-邦幫忙-2018-鐵人賽/) 有部分內容已過時，所以將重新整理成 ASP.NET Core 3 的內容，並補充一些說明。  
本篇主要介紹基本的 ASP.NET Core 3 環境準備及如何用 Visual Studio Code (VS Code) 開發 ASP.NET Core。  

<!-- more -->

## 前言

開發 .NET Core 必需要安裝 .NET Core SDK，所以先到官網下載 .NET Core SDK 的安裝檔，官網下載位置[點此](https://dotnet.microsoft.com/download)。  

.NET Core 是跨作業系統的框架，不再像 .NET Framework 要依附在 Windows 的作業系統才能執行，所以可以依照各平台版本進行下載及安裝。  
文中範例用的截圖大部分是 Windows 作業系統，但本系列教學都會是以指令為主，並不受限於 Windows 平台。  
*(安裝軟體步驟太簡單，除了按**下一步**以外，幾乎沒什麼好解說的，所以不介紹怎麼安裝軟體。)*  

安裝完成後，可以透過 .NET Core CLI (Command-Line Interface) 確認 .NET Core SDK 安裝的版本，指令如下：  

```sh
dotnet --version
```

## 建立網站專案

先建立一個專案資料夾 `MyWebsite`，然後在該資料夾執行 .NET Core CLI 建置網站的指令：  

```sh
# 建立專案資料夾
mkdir MyWebsite

# 進入專案資料夾
cd MyWebsite

# 建立 ASP.NET Core 專案
dotnet new web
```

![ASP.NET Core 3 系列 - 從頭開始 - 建立專案](/images/b/45.png)

.NET Core CLI 會在該資料夾，建立一個空的 ASP.NET Core 專案，內容如下：  

![ASP.NET Core 3 系列 - 從頭開始 - 專案目錄](/images/b/46.png)

```sh
obj/                            # 專案暫存目錄
Properties/                     # 開發用的環境設定
MyWebsite.csproj                # 專案檔
appsettings.Development.json    # 執行程式組態設定(開發階段)
appsettings.json                # 執行程式組態設定(預設)
Program.cs                      # 程式進入檔
Startup.cs                      # 啟動網站設定
```

> .NET Core 3.0 之後，`*.csproj` 專案檔變得很乾淨俐落，如上圖。  
> 當宣告 `<Project Sdk="Microsoft.NET.Sdk.Web">` 就會預設參考 `Microsoft.AspNetCore.App` 套件。  

## 啟動網站

建立完成後，就可以用 .NET Core CLI 啟動網站了。啟動網站指令：  

```sh
dotnet run
```

.NET Core CLI 預設會起一個`http://localhost:5000/`的站台，用瀏覽器打開此連結就可以看到 ASP.NET Core 網站了。如下：  

![ASP.NET Core 3 系列 - 從頭開始 - 啟動網站](/images/b/47.png)  

## Visual Studio Code  

.NET Core 都已經跨作業系統了，開發工具當然也就不再限制於 Visual Studio IDE (Visual Studio 2019/2017 等)。基本上純文字編輯器搭配 .NET Core CLI 就可以開發 ASP.NET Core 了，但沒有中斷點除錯或 Autocomplete 開發有些辛苦。  

* Windows 作業系統，最推薦的當然還是 [Visual Studio IDE](https://visualstudio.microsoft.com/)  
* 跨平台的話強烈推薦 JetBrains 公司出的 [Rider](https://www.jetbrains.com/rider/)  
* 最輕量化跨平台推薦 [Visual Studio Code](https://code.visualstudio.com/) (簡稱 VS Code)。  

VS Code 是一套可安裝擴充套件的文字編輯器，有支援 Windows、Mac 及 Linux 版本，極輕量又免費。  
只要安裝擴充套件就變成了 IDE，並且支援多種不同的程式語言。下載位置[點此](https://code.visualstudio.com/Download)。  

> 範例選擇用 VS Code 最主要的原因是免費且跨平台。  

### 安裝擴充套件

打開 VS Code 可以在左邊看到五個 Icon，點選最下面的那個 Extensions 圖示，並在 Extensions 搜尋列輸入 **C#** ，便可以找到 `C#` 的擴充套件安裝。如下圖：

![ASP.NET Core 3 系列 - 從頭開始 - VS Code C# 擴充套件](/images/ironman/i01-4.png)

### 開啟專案

VS Code 跟一般文字編輯器有些不同，它是以資料夾為工作區域，開啟一個目錄，就等通於是開啟一個專案。從上方工具列 **File** -> **Open Folder** 選擇 ASP.NET Core 專案目錄，大概隔幾秒後，VS Code 會提示是否要幫此專案加入 Build/Debug 的設定。如下圖：  

![ASP.NET Core 3 系列 - 從頭開始 - VS Code 開啟專案](/images/ironman/i01-5.png)

### Build/Debug 設定

如果沒有自動提示加入 Build/Debug 設定，可以在左邊 Icon，點選倒數第二個 Debug 圖示，手動加入 Build/Debug 設定。如下步驟：  

![ASP.NET Core 3 系列 - 從頭開始 - VS Code Build/Debug 設定](/images/ironman/i01-6.png)
![ASP.NET Core 3 系列 - 從頭開始 - VS Code Build/Debug 設定](/images/ironman/i01-7.png)

設定完成後，VS Code 會自動建立 *.vscode* 目錄及設定檔 *launch.json*、*tasks.json*。  
目錄結構如下：  

```sh
.vscode/                        # VS Code 設定檔目錄
  launch.json                   # 用 VS Code 啟動程式的設定檔
  tasks.json                    # 定義 launch.json 會用道的指令設定檔
obj/                            # 專案暫存目錄
Properties/                     # 開發用的環境設定
MyWebsite.csproj                # 專案檔
appsettings.Development.json    # 執行程式組態設定(開發階段)
appsettings.json                # 執行程式組態設定(預設)
Program.cs                      # 程式進入檔
Startup.cs                      # 啟動網站設定
```

如果 VS Code 自動建立失敗，那就手動新增 *launch.json* 及 *tasks.json* 吧...  
內容如下：  

*launch.json*:  

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": ".NET Core Launch",
      "type": "coreclr",
      "request": "launch",
      "preLaunchTask": "build",
      "program": "${workspaceFolder}/bin/Debug/netcoreapp3.0/MyWebsite.dll",
      "args": [],
      "cwd": "${workspaceFolder}",
      "console": "internalConsole",
      "stopAtEntry": false
    }
  ]
}
```

*tasks.json*:  

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "build",
      "command": "dotnet",
      "type": "process",
      "args": [
        "build"
      ],
      "problemMatcher": "$msCompile"
    }
  ]
}
```

### 中斷點除錯

在程式碼行號左邊點擊滑鼠就可以下中斷點了，跟一般 IDE 差不多。然後在 Debug 側欄啟動偵錯：  

![ASP.NET Core 3 系列 - 從頭開始 - VS Code 中斷點除錯](/images/ironman/i01-8.png)

當執行到該中斷點後，就會停下來，並在 Debug 側欄顯示當前變數狀態等，也可以用滑鼠移到變數上面檢視該變數的內容。如下：

![ASP.NET Core 3 系列 - 從頭開始 - VS Code 中斷點除錯](/images/ironman/i01-9.png)

偵錯方式跟大部分的 IDE 都差不多，可以 Step over、Step in/out 等。  
如此一來就可以用 VS Code 輕鬆開發 ASP.NET Core。  
