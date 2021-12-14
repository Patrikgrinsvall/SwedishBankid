# Swedish BankId Insomnia / Postman collection and instructions

Insomnia collection and other information on how to use Swedish Test BankId.

## How to use

1. Import collection into insomnia
![image](https://user-images.githubusercontent.com/2749942/146060952-3feda0fc-3d69-477a-be69-1cc60986527b.png)

2. Setup the client certificate
Bankid uses two way mutual ssl connection where a client certificate is needed to communicate with bankid api endpoints. In production this certificate is replaced with a "Relying party certificate". 
![image](https://user-images.githubusercontent.com/2749942/146069167-7fd81d8e-bf4c-41f7-956c-3aee9ee75f7b.png)

3. Disable certificate validation
*Note* Its possible to add this to the OS certificate store as well, but a bit unnessisary in test environment. In production environment however, you will need to either install in OS certificate store, disable verification in CURL or the http client library your application uses or pass the certificate to CURL. (i will add instructions on how to do it next time i build a bankid application)
![image](https://user-images.githubusercontent.com/2749942/146069702-6218b126-c104-4f44-a59f-34ff635e5d26.png)


4. Authenticate and collect response
There are three requests prepared. Fill out personal number with your test bankid personal number and make sure you have your public ip adress filled out. Start with the auth request and save the orderRef. After authentication is completed on phone, use the orderref in the collect request. If you need to cancel, use the orderref in the cancel request.
![image](https://user-images.githubusercontent.com/2749942/146068432-cb322c25-36fb-4828-a149-b31778b03ff5.png)

5. Building the app.
 - In an app, call your API and the API will call bankid. Dont bundle your RP certificate into a frontend app.
 - First call authenticate
 - Second, save the orderref in a session or temporary variable untill the authentication is either complete or canceled/failed.
 - Poll /collect endpoint from frontend app to your API which calls bankid with the orderref parameter. Once every 2 seconds is a pretty good interval.  
 - Eventually you will get a "complete" status or an error. Then the orderref can be saved as a reference but most likley it can be thrown away.
 - Text messages are provided in bankid rp info document or i have them in this repo:
   - Swedish: https://github.com/Patrikgrinsvall/laravel-bankid/blob/master/resources/lang/vendor/bankid/sv/messages.php
   - English: https://github.com/Patrikgrinsvall/laravel-bankid/blob/master/resources/lang/vendor/bankid/en/messages.php
