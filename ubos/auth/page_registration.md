# Registration

## Page

![image-20230515164754501](media/image-20230515164754501.png)

### Кпока Login

 ![image-20230515165356256](media/image-20230515165356256.png)

### Кпопка Sign Up

![image-20230515165241665](media/image-20230515165241665.png) 

## APIs

### registration

```
POST {{main.env.nodeUrl}}/registration
```

body

```json
{
	"firstname":"{{firstname_field.text}}",
	"lastname":"{{lastname_field.text}}",
	"email":"{{email_field.text}}",
	"password":"{{pass_field.text}}"
}
```

[Node-RED](node_registration.md)

