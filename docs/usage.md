## User() 초기화
로그인 및 회원가입에 대한 API를 호출하는 곳에서 데이터 베이스를 연결해주는 `User()` 초기화 함수 파리미터를 설정해서 객체를 생성해주세요.

```py
from dong_api.users import User


user = User(db_name, db_table_name)
```
- `db_name` : SQLite DB 이름
<br/ >
- `db_table_name` : DB table 이름

라미터에 작성된 데이터베이스에 대해 아래와 같은 메서드를 제공합니다.

## signinUser()
에플리케이션으로부터 전달 받은 사용자의 로그인 정보를 데이터베이스에서 조회 한 후, 결과를 반환하는 메서드입니다.

``` py
 response = user.signinUser(data)
```
- `user.signinUser(data)` : 파라미터로 사용자의 email과 password를 넣어줍니다.

<br/ >
데이터베이스 안에 사용자의 정보가 없거나 혹은 비밀번호가 틀렸을 경우 `False`와 실패 메시지를 반환합니다. 반대로 사용자의 정보를 찾고 입력받은 정보와 일치하는 경우 `True`와 성공 메시지, `username`, `access_token`을 생성하여 반환 합니다.

**Fail**
```json
// 이메일을 잘못 입력한 경우
{
    "result": false,
    "message": "이메일을 다시 확인해주세요.",
}

// 사용자가 없는 경우
{
    "result": false,
    "message": "존재하지 않는 이메일입니다.",
}

// 비밀번호가 틀린 경우
{
    "result": false,
    "message": "비밀번호를 다시 확인해주세요.",
}
```

**Success**
```json
{
    "result": true,
    "message": "로그인이 완료되었습니다.",
    "username": "도라에몽",
    "access_token": "..."
}
```

<br/ >


## signupUser()
에플리케이션으로부터 전달 받은 사용자의 회원가입 정보를 데이터베이스에서 조회 및 추가한 후, 결과를 반환하는 메서드입니다.
```py
response = user.signupUser(data)
```
- `user.signupUser(data)` : 파라미터로 사용자의 email과 password, username을 넣어줍니다.

<br/ >
먼저 전달받은 사용자의 email과 username이 데이터베이스이 존재하는지 확인합니다. email 또는 username이 이미 존재하는 경우, False와 실패 메시지를 반환합니다. 반대로 존재하지 않는 경우에는 데이터베이스에 추가한 후에 True와 성공 메시지를 반환합니다. 

**Fail**
```json
// 이메일이 존재하는 경우
{
    "result": false,
    "message": "이미 가입된 이메일입니다.",
}

// 유저 이름이 존재하는 경우
{
    "result": false,
    "message": "이미 존재하는 유저 이름입니다.",
}
```

**Success**
```json
{
    "result": true,
    "message": "회원가입이 완료되었습니다.",
}
```

<br/ >
<br/ >
<br/ >
