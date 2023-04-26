# Secrets
You’re a senior cyber security engineer and during your shift, we have intercepted/noticed a high privilege actions from unknown source that could be identified as malicious. We have got you the ticket that made these actions.
You are the one who created the secret for these tickets. Please fix this and submit the low privilege ticket so we can make sure that you deserve this position.
Here is the ticket:

``` eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmbGFnIjoiQlRMe180X0V5ZXN9IiwiaWF0Ijo5MDAwMDAwMCwibmFtZSI6IkdyZWF0RXhwIiwiYWRtaW4iOnRydWV9.jbkZHll_W17BOALT95JQ17glHBj9nY-oWhT1uiahtv8 ```


## 1) Can you identify the name of the token? (Format: String)

``` https://www.base64decode.org/ ```
``` {"typ":"JWT","alg":"HS256"}{"flag":"BTL{_4_Eyes}","iat":90000000,"name":"GreatExp","admin":true}Y[^8P׸%Z& ```

** Answer: ** JWT

## 2) What is the structure of this token? (Format: Section.Section.Section) 

``` https://jwt.io/ ```

** Answer: ** HEADER.PAYLOAD. SIGNATURE

## 3) What is the hint you found from this token? (Format: String) 

** Answer: ** _4_Eyes

## 4) What is the Secret? (Format: String)

1. save the Token in a text file
2. save as jwt.txt

``` hashcat jwt.txt -a 3 7a7a7a7a ```

** Answer: ** bT!0

## 5) Can you generate a new verified signature ticket with a low privilege? (Format: String.String.String) 

** Answer: **