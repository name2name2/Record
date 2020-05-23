
PCMan程式專案建置和執行：逐步解說
---
1. 安裝 Visual Studio 2017 (Community 即可)
   * 請至官方網站下載: https://www.visualstudio.com/    
   * 目前最新版本是Visual Studio 2019 應該也可以
   * 安裝過程詢問到要安裝那些模組時，將C++有關的套件選項都勾起來安裝，依照安裝程式導引安裝完成
   
1. 建立一個本機資料夾可以放git repository，以下將資料夾路徑代稱為 `本機Git資料夾`

1. git clone pcman-windows (https://github.com/pcman-bbs/pcman-windows.git) 到 `本機Git資料夾\pcman-windows`
   * 可以用git的clone指令，或者git的相關GUI軟體的clone功能

1. git clone vcpkg (https://github.com/Microsoft/vcpkg) 到 `本機git資料夾\vcpkg`
   * clone完成後，依照官方頁面教學，點兩下執行 vcpkg\bootstrap-vcpkg.bat
   * 執行完成後會出現 vcpkg\vcpkg.exe
   * 開啟cmd，執行`cd /d 本機Git資料夾\vcpkg`，再執行`vcpkg integrate install`
      * 正確會印出訊息 `Applied user-wide integration for this vcpkg root.` 
      * 如果出現 `Warning: integration was not applied`，則將整個vcpkg資料夾複製到C:\ ，再執行`vcpkg integrate install`。後面步驟的vcpkg路徑都要改成 C:\vcpkg  [*註1](#reamrk)

1. 使用vcpkg安裝套件
   * 將cmd的路徑保持在`本機Git資料夾\vcpkg`，以下開始用cmd安裝x86版本的pacakage
   * 執行`vcpkg install cpprestsdk:x86-windows`
   * 執行`vcpkg install boost:x86-windows`，裝的套件比較多，耐心等候大約半小時安裝完成
   * 執行`vcpkg install websocketpp:x86-windows`

1. git clone cpprestsdk (https://github.com/microsoft/cpprestsdk) 到 `本機git資料夾\cpprestsdk`
 
1. 安裝CMake
   * 前往 https://cmake.org/download/ ， 下載Latest Version中適用於Windows x64的msi檔
   * 執行msi檔，跟隨安裝程式導引完成CMake安裝

1. 取得cpprestsdk相關的dll lib檔 
   * cmd 執行 `cd /d 本機Git資料夾\cpprestsdk`
   * 執行 `mkdir build.x32v141` [註2]
   * 執行 `cd build.x32v141`
   * 執行 `"C:\Program Files\CMake\bin\cmake.exe" ../Release -A Win32 -DCMAKE_TOOLCHAIN_FILE=本機Git資料夾/vcpkg/scripts/buildsystems/vcpkg.cmake`
      * 正確完成會印出訊息 `Build files have been written to: 本機Git資料夾/cpprestsdk/build.x32v141`
   * 用 visual studio 開啟 `\build.x32v141\cpprestsdk.sln`
   * 等待 visual studio 載入專案，左下角如有` Parsing Include ... Scanning Include ...` 訊息，耐心等候直到左下角訊息停止變動，出現`就緒 Ready`訊息
   * 在 cpprest 專案 > 右鍵 > Build(建置) ，等待建置成功
   * 建置成功後，會有一些`.dll .lib`等等檔案輸出到`\build.x32v141\Binaries\Debug`，全部的檔案有`cpprest141_2_10d.dll libcrypto-1_1.dll libssl-1_1.dll zlibd1.dll cpprest141_2_10d.exp cpprest141_2_10d.ilk cpprest141_2_10d.lib cpprest141_2_10d.pdb`
   * 將這些檔案複製到 `本機Git資料夾\pcman-windows\Lite` 和 `本機Git資料夾\pcman-windows\Combo` 
   
1. 設定/建置PCMan專案
   * 用 visual studio 開啟 `本機Git資料夾\pcman-windows\PCMan.sln`
   * 開啟後等待 visual studio 載入，等到左下角訊息不再變動
   * 在 Combo 專案 > 右鍵 > Properties(屬性) > Linker > All Options > 設定頁面往上滾動 > Additional Dependencies > 在現有參數後方加上 `本機Git資料夾\pcman-windows\Combo\cpprest141_2_10d.lib;` ， 小心不要覆蓋掉全部的值(發現蓋掉全部的值可按Esc還原)，是加在現有值的後方
   * 在 Combo 專案 > 右鍵 > Build(建置) ，等待建置成功
   * 在 Lite 專案 > 右鍵 > Properties(屬性) > Linker > All Options > 設定頁面往上滾動 > Additional Dependencies > 在現有參數後方加上 `;本機Git資料夾\pcman-windows\Lite\cpprest141_2_10d.lib` ， 小心不要覆蓋掉全部的值(發現蓋掉全部的值可按Esc還原)，是加在現有值的後方
   * 在 Lite 專案 > 右鍵 > Build(建置) ，等待建置成功
   * 將 Lite 或 Combo 專案 > 右鍵 > Set as StartUp Project(建置) > 按下F5 ， 即可執行程式，出現PCMan的程式畫面

1. 執行 PCMan
   * 在 Lite 或 Combo 專案 > 右鍵 > Set as StartUp Project(設定為起始專案) > 按下 F5 ， 即可執行出現PCMan的程式畫面

.

### Remark

[註1] : 我原本先把vcpkg裝在E:\ ，然後跑`integrate install`會出現`Warning: integration was not applied`訊息，雖然看到Warning先繼續安裝相關的套件完成，安裝完成後發現在visual studio裡面的cpp檔相關的`#include`還是會出現紅線錯誤。後來搜尋 https://github.com/Microsoft/vcpkg/issues/5956 提到
`I have reinstalled vcpkg directly to the c-drive and now it is working, even if I don't know why. Thank you for the support.`，我改放到C:\底下，重新執行`integrate install`就得到`Applied user-wide integration for this vcpkg root.`訊息，cpp檔裡面的`#include`也正常了。但是刪掉vcpkg再重裝在E:\，又沒問題了。

[註2] : 從 https://github.com/microsoft/cpprestsdk/wiki/How-to-build-for-Windows 學到，裡面是x64，另外搜尋一些文章得知參數改成Win32就可以輸出為32位元的版本
