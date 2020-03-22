[<- На головну](../)  [Розділ](README.md)

## Modbus-tcp Write (запис об’єктів)

![img](media/mbtcp_write.png) Підключається до TCP server для запису **msg.payload** в coil або register (рис.6.3). 

Підтримуються функції:

- FC 5: Write Single Coil
- FC 6: Write Single Holding     Register
- FC 15: Write Multiple Coils
- FC 16: Write Multiple Holding     Registers

У налаштуванні вибирається функція (FC), стартова адреса coil/register (0:65535). 


![img](media/6_3.png)

рис.6.3. Налаштування вузла Modbus-tcp Write

Для FC 5 у **msg.payload** вказується число або строкове значення 0 або 1. Для FC 6 у **msg.payload** повинна бути число або рядок між 0:65535. Для FC15, **msg.payload** повинен бути масивом чисел або рядків 0 або 1. Для FC 16, **msg.payload** повинен бути масивом чисел або рядків зі значеннями між 0:65535.