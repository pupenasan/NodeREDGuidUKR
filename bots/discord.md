# Інтеграція з Discord

## Через Веб-хуки

1) Створити сервер
2) Наведи курсор на назву каналу → натисни ⚙️ Edit Channel. В меню зліва вибери Integrations. У розділі Webhooks натисни “Create Webhook”. Вкажи: Ім’я Webhook-а (наприклад, `PLC Alerts Bot`), Канал, куди він надсилатиме повідомлення, При бажанні — аватарку.
3) Натисни “Copy Webhook URL”. Збережи зміни (кнопка Save Changes унизу).



https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks

Далі через POST передавати повідомлення на створений URL. 

