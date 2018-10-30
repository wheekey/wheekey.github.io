---
published: true
---
## Если нужна авторизация на сайте при запросе, то заголовки нужно добавить следующие:

```
$ch = curl_init("https://example.com");
curl_setopt($ch, CURLOPT_USERPWD, "$usernameAuthentification:$passwordAuthentification");
curl_setopt($ch, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($userData));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$token = curl_exec($ch);
var_dump($token);
```
