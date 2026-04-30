## Flow in HL formst

```json

LOGIN = string45

HOST = chat-be

FE = chat

WA_LOGIN = testtest

WA_TOKEN = 4a57e4c3-9877-487b-9a2f-29bae392556e

PHONE  = 79240154372

SOURCE = whatsapp


POST HOST.touch-api.com/auth/register
{
    "login": "LOGIN",
    "password": "LOGIN",
    "passwordUnsafe": true,
    "generateStaticToken": true
}

TOKEN = RESULT->tokens->accessToken

SATKN = RESULT->staticToken


POST HOST.touch-api.com/account
header: Authorization: Bearer TOKEN
{
    "source": "SOURCE",
    "token": "WA_TOKEN",
    "login": "WA_LOGIN"
}

ACC1_UUID = RESULT->uuid


POST HOST.touch-api.com/account
header: Authorization: Bearer TOKEN
{
    "source": "SOURCE",
    "token": "WA_TOKEN",
    "login": "WA_LOGIN2"
}

ACC2_UUID = RESULT->uuid


POST HOST.touch-api.com/task-manager/creating-sync-chats-task
header: Authorization: Bearer TOKEN
{
  "accountUuid": "ACC1_UUID",
  "limit": 100,
  "skip": 0,
  "repeatEnabled": true
}


POST HOST.touch-api.com/task-manager/creating-sync-chats-task
header: Authorization: Bearer TOKEN
{
  "accountUuid": "ACC2_UUID",
  "limit": 100,
  "skip": 0,
  "repeatEnabled": true
}


POST cloud.controller.touch-api.com/api/addWebhook
{
"webhookUrl":"https://chat-be.touch-api.com/hook/ACC1_UUID",
"source": "SOURCE",
"token":"WA_TOKEN",
"login":"WA_LOGIN"
}


POST cloud.controller.touch-api.com/api/getInfo
{
"source": "SOURCE",
"token":"WA_TOKEN",
"login":"WA_LOGIN"
}


URL = https://FE.touch-api.com?satkn=SATKN

```