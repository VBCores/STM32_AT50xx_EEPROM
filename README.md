# Библиотека для работы с EEPROM VBCores
В некоторых модулях VBCores есть встроенный EEPROM AT24С64CN, для работы с которым предназначена данная библиотека
В соответствии со схемой подключения EEPROM имеет I2C-адрес `0b1010zyx`, где значения x, y и z определяются тем, как подтянуты пины A0, A1 и A2. Если пин подтянут к земле, соответствующий бит адреса равен нулю, если к "плюсу", то соответствующий бит адреса равен 1, в нашем случае все пины подтянуты к земле, и адрес устройства `0b1010000`.

## Установка
Скачайте файлы `at24_eeprom.c` в `/src`, а файл `at24_eeprom.h` в `/inc`, вашего проекта, сконфигурируйте I2C следующим образом:

*сконфигурируйте I2C следующим образом: ![alt text](https://github.com/VBCores/G4_EEPROM/tree/main/img/i2C.jpg?raw=true)

включите прерывания для I2C

## Использование
В библиотеке реализованы 4 функции
1. `at24_isConnected()` - проверяет, есть ли связь с EEPROM, и если есть возвращает `True`, если нет `False`
2. `at24_write(uint16_t address, uint8_t *data, size_t len, uint32_t timeout)`
    `address` - адрес в EEPROM. Адресация в данной библиотеке идет побайтово. Для записи в 0x0001-й байт  `address = 0х0001`
    `data` - буфер данных, которые будут записаны в EEPROM
    `len` - количество байт для записи из буфера
    `timeout` - в милисекундах
3. `at24_read(uint16_t address, uint8_t *data, size_t len, uint32_t timeout)`
    `address` - адрес в EEPROM. Адресация в данной библиотеке идет побайтово. Для чтения из 0x0003-й байта  `address = 0х0003`
    `data` - буфер в который будет записаны прочитанные из EEPROM данные
    `len` - количество байт для записи в буфера
    `timeout` - в милисекундах
4. `at24_eraseChip()` - стирает все данные из EEPROM, и если удачно возвращает `True`, если нет `False`

## Пример
Создайте новый проект на базе примера и запустите его. Раскомментируйте строчки перед while(1) для записи в EEPROM.
Данные запишуться в EEPROM, и затем будут читаться из него и передаваться в UART, для чтения используйте монитор порта. 

