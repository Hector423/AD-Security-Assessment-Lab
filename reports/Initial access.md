
In this sections I document all the possible scenarios for an initial access that the lab allow me to do.

- **LLMNR/NBT-NS Poisoning**

For this access I had to force an interaction and simulate a user interacting with the domain. 

When the user tries to access a shared folder that doesn't exists, Windows uses the LLMNR and NBT-NS protocols to resolve the hostname.

This allowed me to use responder to catch the petition and see the user and hash from the request.

![](<../assets/Pasted image 20260403124842.png>)

![](<../assets/Pasted image 20260403124913.png>)

  With this method now I can try to brute force the hash and see if I can get the password from the user Administrador
![](<../assets/Pasted image 20260403125243.png>)

Also this attack reveled me new names from other computers but I will see them later.

I put the hash of the Administrador account in a .txt file and then use the tool John The Ripper to crack the hash

![](<../assets/Pasted image 20260403132537.png>)

With this technique I got the password of the user.


- 