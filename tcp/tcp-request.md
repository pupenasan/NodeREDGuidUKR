[<- На головну](../)  [Розділ](README.md)

## TCP Request

![](media/tcp-request.png)Простий вузол для відправки клієнтського запиту TCP та очікування відповіді.

 Запит відправляється через  `msg.payload` на порт TCP-сервера, після чого очікується відповідь.

![](media/tcprequest_cfg.png)

Connects, sends the "request", and reads the "response". It can either count a number of returned characters into a fixed buffer, match a specified character before returning, wait a fixed timeout from first reply and then return, sit and wait for data, or send then close the connection immediately, without waiting for a reply.

Підключається, надсилає "запит" і читає "відповідь". `Return` налаштовується на різні режими очікування відповіді для видачі отриманих даних:

- він може або підрахувати кількість символів у фіксованому буфері (`fixed number of charts`), 
- очікувати вказаний символ перед тим як повернути результат(`when character received`)
- чекати фіксований час очікування від першої відповіді, а потім повернути результат(`after a fixed timeout`),
- сидіти і чекати даних (`never`) і ніколи не закривати зєднання  
- відправляти запит, а потім негайно закривати з'єднання, не чекаючи відповідь.

Відповідь буде виводитися у  `msg.payload` як буфер, тому ви, можливо, захочете перетворити його у рядок з використанням методу `.toString ()`.

Якщо ви залишаєте хост або порт tcp порожнім, їх потрібно встановити, використовуючи властивості `msg.host` та ` msg.port` у кожному повідомленні, надісланому до вузла.

