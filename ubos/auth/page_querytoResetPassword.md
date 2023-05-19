# Qery To Reset password

## Page

![image-20230519143503437](media/image-20230519143503437.png)

### TextEmailSent

Text

```js
{{sendEmailForResetPassword.data.data}}
```

### FormButton1 (Continue)

onClick

```js
{ { sendEmailForResetPassword.run(() => navigateTo('Info',{email: InputEmail.text}), () =>  {}) } }
```

### Button2 (Don't have an account? Sign up!)

onClick

```
{ { navigateTo('Registration', {}) } }
```

### Button2Copy (Back to Login)

onClick

```
{ { navigateTo('Login',  {}) } }
```



## APIs

### sendEmailForResetPassword

```
POST {{main.env.nodeUrl}}/sendEmailForResetPassword
```

body

```js
{
	"email": "{{InputEmail.text}}"
}
```

[Потік Node-RED](node_sendEmailForResetPassword.md)
