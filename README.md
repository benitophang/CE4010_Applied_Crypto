# CE4010_Applied_Crypto_Project

##### 1)Motivations

This project is a demonstration of attacks on "weak" RSA. The two attacks demonstrated are wiener's attack and partial key exposure attack (Coppersmith Theorem) which are both mathematical attacks on RSA. Reasons for choosing wiener's attack is due to its simplicity. It can be easily checked against, especially with code.

This basic Coppersmith attack was chosen due to it being the basis for other types of attack on RSA vulnerability such as ROCA vulnerability. It can also be used for other attack methods for example targeting the MSB instead. I believe Professor Sourav also wrote about this specifically in his paper with Santanu Sarkar and Subhamoy Maitra.


#### 2)Research

Some mathematical knowledge is required to understand both attacks. Required mathematical knowledge are:
1. Continued Fractions + Convergents
2. Coppersmith Theorem (Don't have to know in depth but have to understand what the theorem does. I.E given f(x,y)=polynomial with two variables over integers Z. x and y can be found in polynomial time under certain conditions.)


#### 3)Design & Development

The notebook only features the backend logic and functions. (N, public exponent e etc have to be manually fed into the relevant functions). Frontend UI should be implemented for better user experience. Wiener's attack implementation is referenced from lecture slides. Coppersmith Attack is referenced from numerous online articles.


#### 4)Use of code

Wiener's attack can be used if we know that d < 1/3* N^1/4. Else, if e is unusually large, we can also try wiener's attack on the suspicion that d will be short due to large e. Main drawback of Wiener's attack is that Wiener's condition can't be checked, hence we could run the attack and get no results in return, most likely due to failure to meet Wiener's condition.

Coppersmith's attack can be used as long as we know the last n/4 bits of key d. Time complexity is O(en^a) for some value of a where n refers to number of bits hence, e is required to be small as it is linear in e. This linearity can be explained as the first part of the algorithm loops through all values of e while the factoring steps at the end takes n^a for some value of a. 

An example use case of coppersmith's attack would be to employ side channel attacks along with coppersmith attack. Side channel attacks such as power tracing or timing attacks can allow us to find info about the private key. We would then target the LSB and once we obtain n/4 LSB, we can use the coppersmith attack implementation to find out the rest of the key.
