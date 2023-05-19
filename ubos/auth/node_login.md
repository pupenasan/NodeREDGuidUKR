# Потік `POST /login`

Обробляє логін користувача зі сторінки UI [Login](page_login.md). 

У якості параметрів передається JSON з Appsmith:

```json
{
	"email":"{{email_field.text}}",
	"password":"{{pass_field.text}}"
}
```

Потік обробляється в послідовності

1) `check` - Перевірка на коректність пошти та паролю, тобто що задовольняє умовам формату, якщо ні - відмова
2) `mongo Find` - Пошук в БД серед активних користувачів
3) `check auth` - перевірка знайденого:
   - якщо користувача не знайдено - відмова
   - якщо паролі не співпадають - відмова
   - якщо користувач не активний - відмова 



![image-20230517131030174](media/image-20230517131030174.png)

## check

```js
const regexEmail = /^(([^<>()[\]\.,;:\s@\"]+(\.[^<>()[\]\.,;:\s@\"]+)*)|(\".+\"))@(([^<>()[\]\.,;:\s@\"]+\.)+[^<>()[\]\.,;:\s@\"]{2,})$/i;
const regexPassword = /^(?!.*\s).{8,}/;
const email = msg.payload.email.toLowerCase();

//якщо email некоректний
if (!regexEmail.test(email)) {
    msg.statusCode = 401;
    msg.payload = {
        data: "Email is invalid",
        code: 401
    }
    return [null, msg];
//якщо password некоректний
} else if (!regexPassword.test(msg.payload.password)) {
    msg.statusCode = 401;
    msg.payload = {
        data: "The password is invalid. The value must be at least 8 characters and without whitespaces",
        code: 401
    }
    return [null, msg];
//якщо password і email коректний    
} else {
    msg.collection = "admins"
    msg.fromApp = msg.payload
    node.warn(msg.fromApp) //вивести на консоль для дебага
    msg.payload = {
        email: email,
        deleted: false,
        active: true
    }
    return [msg, null];
}
```

## mongo Find

Operation = Find

Шукає в `collection = msg.collection` документи які задовольняють умові 

```js
    msg.payload = {
        email: email,
        deleted: false,
        active: true //тільки активних користувачів
    }
```

Повертає список користувачів

## check auth

```js
//якщо не знайдено користувача в колекції admins
if(msg.payload.length === 0){
    msg.statusCode = 401;
    msg.payload = {
        data: "Incorrect email or password",
        code:401
    }
    node.warn("Email not found");
    return [null,msg]

//якщо знайдено користувача
} else {
    // порівняти збережені та введені паролі
    let check = await bcrypt.compare(msg.fromApp.password, msg.payload[0].password);
    // якщо пароль не співпадає
    if (!check) {
        msg.statusCode = 401;
        msg.payload = {
            data: "Incorrect email or password",
            code: 401
        }
        node.warn("Password incorrect");
        return [null, msg]
    }
    
    // якщо користувач не активний (ніколи не спрацює???)
    if (msg.payload[0].active === false) {
        msg.statusCode = 401;
        msg.payload = {
            data: "Email not activated",
            code: 401
        }
        return [null, msg]
    }
}

//якщо програма дійшла до цього місця - потік продвожується по першому виходу
return[msg,null]
```



## jwt token

```js
msg.payload = msg.payload[0]
// створюємо шифрований jwt токен
const token = jwt.sign(
    { 
        user_id: msg.payload._id, 
        email:msg.payload.email },
    "test", // слово для шифрування 
    {
        expiresIn: "1400m", //час життя токена
    }
);

//віправити токен в куках
msg.cookies = {};
msg.cookies["user_token"] = token;

return msg;
```

