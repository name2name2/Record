
PCMan程式專案建置和執行：逐步解說
---
1. 安裝 Visual Studio 2017 (Community 即可)
   * 請至官方網站下載: https://www.visualstudio.com/    
   * 目前最新版本是Visual Studio 2019 自己沒安裝過但應該也可以
   * 安裝過程詢問要安裝那些模組時，將C++有關的套件選項都勾起來安裝
   
1. git clone pcman-windows (https://github.com/pcman-bbs/pcman-windows.git) 到本機
   * 可以用git的clone指令
   * 可以用git的一些GUI軟體的clone功能

1. 用 Visual Studio 開啟本機 pcman-windows\PCMan.sln，並且在Lite專案 > 右鍵 > 建置，此時編譯應該會發生錯誤，後面步驟會陸續解決

1. git clone vcpkg (https://github.com/Microsoft/vcpkg) 到本機
   * clone完成後，依照官方頁面教學，點兩下執行vcpkg\bootstrap-vcpkg.bat
   * 執行完成後會出現 vcpkg\vcpkg.exe
   * 將整個 vcpkg 資料夾複製到C:\   
   
   

1. 
   * 
   * 

1. 
   * 
   * 


[註1] :  

這份文件說明開發和釋出的需求

- [開發] 

請至官方網站下載: https://www.visualstudio.com/

- [開發] cpprestsdk

這兩個推薦使用 vcpkg 安裝, 安裝說明請至以下網站:


安裝指令: vcpkg install cpprestsdk

- [釋出] Microsoft Visual C++ Redistributable for Visual Studio 2017 (或相對應的版本)

可至 https://www.visualstudio.com/downloads/ 的
Other Tools and Frameworks 區域下載.
