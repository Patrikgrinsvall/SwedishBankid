# Swedish BankId

Insomnia collection and other information on how to use Swedish Test BankId.

# How to use

1. Import collection into insomnia
![image](https://user-images.githubusercontent.com/2749942/146060952-3feda0fc-3d69-477a-be69-1cc60986527b.png)

2. Make requests
There are three requests prepared. Fill out personal number with your test bankid personal number and make sure you have your public ip adress filled out. Start with the auth request and save the orderRef. After authentication is completed on phone, use the orderref in the collect request. If you need to cancel, use the orderref in the cancel request.
![image](https://user-images.githubusercontent.com/2749942/146068432-cb322c25-36fb-4828-a149-b31778b03ff5.png)


