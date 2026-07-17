Lab: Username enumeration via subtly different responses

<img width="1688" height="826" alt="image" src="https://github.com/user-attachments/assets/dcdf4455-3d91-49fb-869f-e3a56e65fd47" />

when we navigated to the /my-account directory,entered the usernane "hi" and the password "pass" and sent the request, we received an "invalid username" response:

<img width="1402" height="747" alt="image" src="https://github.com/user-attachments/assets/495a6597-2a7f-4d0f-97fc-1111ee701089" />

now we get back lab page we can see candidate usernames and passwords list. now we may save passwords and username in your machine and become txt file 

<img width="1982" height="1244" alt="image" src="https://github.com/user-attachments/assets/900b47f9-1560-4e5f-9860-c1ef0c837063" />


then create file and rename as you wish
then inside that file, we open linux terminal and type nano username.txt then opend nano GNU and copy username list. likewise password list save password.txt

<img width="636" height="366" alt="image" src="https://github.com/user-attachments/assets/a9f611b6-41da-4e94-92a2-9fb3b9174e65" />

We sent the request to Burp Intruder and brute-forced the username and password. First We checked for different responses by brute-forcing the username parameter:

<img width="2674" height="1232" alt="image" src="https://github.com/user-attachments/assets/a97259fa-a1a3-4548-ba1c-bb358c5d09a3" />

We were able to see that the username pi had a different length is response :

<img width="2872" height="468" alt="image" src="https://github.com/user-attachments/assets/ed530a8c-4270-4e61-82ff-580878d1b3d2" />

We then used pi as our username and attacked the password parameter and found that the 1234567 had a different length : 

<img width="2872" height="670" alt="image" src="https://github.com/user-attachments/assets/7204778e-b039-4e2c-84d6-7d3a4206af27" />

We were able to login using the credentials pi:1234567 and solve the lab :

<img width="2872" height="1414" alt="image" src="https://github.com/user-attachments/assets/fc1996b1-5eb1-4fc9-9298-1392f0c4b093" />
















