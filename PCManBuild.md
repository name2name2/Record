
PCMan程式專案建置和執行：逐步解說
---
1. 安裝 Visual Studio 2017 (Community 即可)
   * 請至官方網站下載: https://www.visualstudio.com/    
   * 目前最新版本是Visual Studio 2019 自己沒安裝過但應該也可以
   * 安裝過程詢問要安裝那些模組時，將C++有關的套件選項都勾起來安裝
   
1. 建立一個本機資料夾可以放git repository，以下將資料夾路徑代稱為 `本機Git資料夾`

1. git clone pcman-windows (https://github.com/pcman-bbs/pcman-windows.git) 到 `本機Git資料夾\pcman-windows`
   * 可以用git的clone指令，或者git的相關GUI軟體的clone功能

1. git clone vcpkg (https://github.com/Microsoft/vcpkg) 到 `本機git資料夾\vcpkg`
   * clone完成後，依照官方頁面教學，點兩下執行 vcpkg\bootstrap-vcpkg.bat
   * 執行完成後會出現 vcpkg\vcpkg.exe
   * 開啟cmd，執行`cd /d 本機Git資料夾\vcpkg`，再執行`vcpkg integrate install`
      * 正確會印出訊息 `Applied user-wide integration for this vcpkg root.` 
      * 如果出現 `Warning: integration was not applied`，則將整個vcpkg資料夾複製到C:\ ，再重複一次這個步驟  [註1]

1. 使用vcpkg安裝套件
   * 將cmd的路徑保持在`本機Git資料夾\vcpkg`，以下開始安裝x86版本的pacakage
   * 執行`vcpkg install cpprestsdk:x86-windows`
   * 執行`vcpkg install boost:x86-windows`，裝的套件比較多，耐心等候大約半小時安裝完成
   * 執行`vcpkg install websocketpp:x86-windows`

1. git clone cpprestsdk (https://github.com/microsoft/cpprestsdk) 到 `本機git資料夾\cpprestsdk`
   

   CMake > sln
   Parsing Include Scanning Include左下角
1. 
   * 
   * 

1. 
   * 
   * 



1. 用 Visual Studio 開啟本機 pcman-windows\PCMan.sln，並且在Lite專案 > 右鍵 > 建置，此時編譯應該會發生錯誤，後面步驟會陸續解決


[註1] : 我原本先把vcpkg裝在E:\ ，然後跑`integrate install`會出現`Warning: integration was not applied`訊息，雖然看到Warning先繼續安裝相關的套件完成，安裝完成後發現在visual studio裡面的cpp檔相關的`#include`還是會出現紅線錯誤。後來搜尋 https://github.com/Microsoft/vcpkg/issues/5956 提到
`I have reinstalled vcpkg directly to the c-drive and now it is working, even if I don't know why. Thank you for the support.`，我改放到C:\底下，重新執行`integrate install`就得到`Applied user-wide integration for this vcpkg root.`訊息，cpp檔裡面的`#include`也正常了。



這份文件說明開發和釋出的需求

- [開發] 

請至官方網站下載: https://www.visualstudio.com/

- [開發] cpprestsdk

這兩個推薦使用 vcpkg 安裝, 安裝說明請至以下網站:


安裝指令: vcpkg install cpprestsdk

- [釋出] Microsoft Visual C++ Redistributable for Visual Studio 2017 (或相對應的版本)

可至 https://www.visualstudio.com/downloads/ 的
Other Tools and Frameworks 區域下載.
