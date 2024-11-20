# ESP-32-BLE-Beacon
ESP-32 BLE Beacon  This project demonstrates how to configure the ESP-32 (esp version: 3.0.7) as a Bluetooth Low Energy (BLE) beacon device. A BLE beacon broadcasts specific information that nearby BLE-enabled devices can detect. This setup is commonly used for applications like proximity marketing, indoor navigation, or asset tracking.
 

## Why this project?
This implementation resolves issue found in many BLE demo codes for the ESP-32 which is incompatibility with specific ESP32 Arduino Core versions where BLE examples fail with newer core versions, but this code is optimized for version 3.0.7.

### error!
```bash
/private/var/folders/8g/rk42hd814lq9y176l9rz12l00000gn/T/.arduinoIDE-unsaved20241020-34923-qogwcj.xnb/sketch_nov20a/sketch_nov20a.ino: In function 'void setBeacon()':
/private/var/folders/8g/rk42hd814lq9y176l9rz12l00000gn/T/.arduinoIDE-unsaved20241020-34923-qogwcj.xnb/sketch_nov20a/sketch_nov20a.ino:54:18: error: no match for 'operator+=' (operand types are 'std::string' {aka 'std::__cxx11::basic_string<char>'} and 'String')
   54 |   strServiceData += oBeacon.getData();
      |   ~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~
In file included from /Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/string:53,
                 from /Users/arkabanerjee/Library/Arduino15/packages/esp32/hardware/esp32/3.0.7/libraries/BLE/src/BLEDevice.h:18,
                 from /private/var/folders/8g/rk42hd814lq9y176l9rz12l00000gn/T/.arduinoIDE-unsaved20241020-34923-qogwcj.xnb/sketch_nov20a/sketch_nov20a.ino:3:
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1376:9: note: candidate: 'template<class _Tp> constexpr std::__cxx11::basic_string<_CharT, _Traits, _Alloc>::_If_sv<_Tp, std::__cxx11::basic_string<_CharT, _Traits, _Alloc>&> std::__cxx11::basic_string<_CharT, _Traits, _Alloc>::operator+=(const _Tp&) [with _CharT = char; _Traits = std::char_traits<char>; _Alloc = std::allocator<char>]'
 1376 |         operator+=(const _Tp& __svt)
      |         ^~~~~~~~
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1376:9: note:   template argument deduction/substitution failed:
In file included from /Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/stl_pair.h:60,
                 from /Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/stl_algobase.h:64,
                 from /Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/specfun.h:45,
                 from /Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/cmath:1935,
                 from /Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/math.h:36,
                 from /Users/arkabanerjee/Library/Arduino15/packages/esp32/hardware/esp32/3.0.7/cores/esp32/esp32-hal.h:30,
                 from /Users/arkabanerjee/Library/Arduino15/packages/esp32/hardware/esp32/3.0.7/cores/esp32/Arduino.h:36,
                 from /private/var/folders/8g/rk42hd814lq9y176l9rz12l00000gn/T/arduino/sketches/6825C93ED06659C931C50653EAE0CEFD/sketch/sketch_nov20a.ino.cpp:1:
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/type_traits: In substitution of 'template<bool _Cond, class _Tp> using enable_if_t = typename std::enable_if::type [with bool _Cond = false; _Tp = std::__cxx11::basic_string<char>&]':
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:155:8:   required by substitution of 'template<class _CharT, class _Traits, class _Alloc> template<class _Tp, class _Res> using _If_sv = std::enable_if_t<std::__and_<std::is_convertible<const _Tp&, std::basic_string_view<_CharT, _Traits> >, std::__not_<std::is_convertible<const _Tp*, const std::__cxx11::basic_string<_CharT, _Traits, _Alloc>*> >, std::__not_<std::is_convertible<const _Tp&, const _CharT*> > >::value, _Res> [with _Tp = String; _Res = std::__cxx11::basic_string<char>&; _CharT = char; _Traits = std::char_traits<char>; _Alloc = std::allocator<char>]'
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1376:2:   required by substitution of 'template<class _Tp> constexpr std::__cxx11::basic_string<char>::_If_sv<_Tp, std::__cxx11::basic_string<char>&> std::__cxx11::basic_string<char>::operator+=(const _Tp&) [with _Tp = String]'
/private/var/folders/8g/rk42hd814lq9y176l9rz12l00000gn/T/.arduinoIDE-unsaved20241020-34923-qogwcj.xnb/sketch_nov20a/sketch_nov20a.ino:54:37:   required from here
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/type_traits:2614:11: error: no type named 'type' in 'struct std::enable_if<false, std::__cxx11::basic_string<char>&>'
 2614 |     using enable_if_t = typename enable_if<_Cond, _Tp>::type;
      |           ^~~~~~~~~~~
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1329:7: note: candidate: 'constexpr std::__cxx11::basic_string<_CharT, _Traits, _Alloc>& std::__cxx11::basic_string<_CharT, _Traits, _Alloc>::operator+=(const std::__cxx11::basic_string<_CharT, _Traits, _Alloc>&) [with _CharT = char; _Traits = std::char_traits<char>; _Alloc = std::allocator<char>]'
 1329 |       operator+=(const basic_string& __str)
      |       ^~~~~~~~
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1329:38: note:   no known conversion for argument 1 from 'String' to 'const std::__cxx11::basic_string<char>&'
 1329 |       operator+=(const basic_string& __str)
      |                  ~~~~~~~~~~~~~~~~~~~~^~~~~
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1339:7: note: candidate: 'constexpr std::__cxx11::basic_string<_CharT, _Traits, _Alloc>& std::__cxx11::basic_string<_CharT, _Traits, _Alloc>::operator+=(const _CharT*) [with _CharT = char; _Traits = std::char_traits<char>; _Alloc = std::allocator<char>]'
 1339 |       operator+=(const _CharT* __s)
      |       ^~~~~~~~
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1339:32: note:   no known conversion for argument 1 from 'String' to 'const char*'
 1339 |       operator+=(const _CharT* __s)
      |                  ~~~~~~~~~~~~~~^~~
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1349:7: note: candidate: 'constexpr std::__cxx11::basic_string<_CharT, _Traits, _Alloc>& std::__cxx11::basic_string<_CharT, _Traits, _Alloc>::operator+=(_CharT) [with _CharT = char; _Traits = std::char_traits<char>; _Alloc = std::allocator<char>]'
 1349 |       operator+=(_CharT __c)
      |       ^~~~~~~~
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1349:25: note:   no known conversion for argument 1 from 'String' to 'char'
 1349 |       operator+=(_CharT __c)
      |                  ~~~~~~~^~~
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1363:7: note: candidate: 'constexpr std::__cxx11::basic_string<_CharT, _Traits, _Alloc>& std::__cxx11::basic_string<_CharT, _Traits, _Alloc>::operator+=(std::initializer_list<_Tp>) [with _CharT = char; _Traits = std::char_traits<char>; _Alloc = std::allocator<char>]'
 1363 |       operator+=(initializer_list<_CharT> __l)
      |       ^~~~~~~~
/Users/arkabanerjee/Library/Arduino15/packages/esp32/tools/esp-x32/2302/xtensa-esp32-elf/include/c++/12.2.0/bits/basic_string.h:1363:43: note:   no known conversion for argument 1 from 'String' to 'std::initializer_list<char>'
 1363 |       operator+=(initializer_list<_CharT> __l)
      |                  ~~~~~~~~~~~~~~~~~~~~~~~~~^~~
/private/var/folders/8g/rk42hd814lq9y176l9rz12l00000gn/T/.arduinoIDE-unsaved20241020-34923-qogwcj.xnb/sketch_nov20a/sketch_nov20a.ino:56:30: error: cannot convert 'std::string' {aka 'std::__cxx11::basic_string<char>'} to 'String'
   56 |   oAdvertisementData.addData(strServiceData);
      |                              ^~~~~~~~~~~~~~
      |                              |
      |                              std::string {aka std::__cxx11::basic_string<char>}
In file included from /Users/arkabanerjee/Library/Arduino15/packages/esp32/hardware/esp32/3.0.7/libraries/BLE/src/BLEServer.h:22,
                 from /Users/arkabanerjee/Library/Arduino15/packages/esp32/hardware/esp32/3.0.7/libraries/BLE/src/BLEDevice.h:21:
/Users/arkabanerjee/Library/Arduino15/packages/esp32/hardware/esp32/3.0.7/libraries/BLE/src/BLEAdvertising.h:36:23: note:   initializing argument 1 of 'void BLEAdvertisementData::addData(String)'
   36 |   void addData(String data);  // Add data to the payload.
      |                ~~~~~~~^~~~

exit status 1

Compilation error: no match for 'operator+=' (operand types are 'std::string' {aka 'std::__cxx11::basic_string<char>'} and 'String')
```
