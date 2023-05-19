# Login

## Page

![image-20230515165744938](media/image-20230515165744938.png)

### BtnLogIn

```js
{{login.run(() => navigateTo('User Management', {}), () => {})}}
```

### BtnLogUp

![image-20230515172313795](media/image-20230515172313795.png)

### Button2

![image-20230515172641295](media/image-20230515172641295.png)

## APIs

### login

```
POST {{main.env.nodeUrl}}/login
```

body

```json
{
	"email":"{{email_field.text}}",
	"password":"{{pass_field.text}}"
}
```

[Потік Node-RED](node_login.md)

### signout

```
POST {{main.env.nodeUrl}}/signout
```

- [ ] Run API on Page load

[Потік Node-RED](node_signout.md)