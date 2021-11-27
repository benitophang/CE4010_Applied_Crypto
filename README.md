# CE4010 Applied Crypto Project

#### Motivations

This project is a demonstration of attacks on "weak" RSA. The two attacks demonstrated are wiener's attack and partial key exposure attack (Coppersmith Theorem) which are both mathematical attacks on RSA. Wiener's attack exploits small d while Coppersmith's attack exploits small e along with known n/4 LSB. They are chosen to show why we cannot compromise on small d or small e for faster encryption/decryption.

Reasons for choosing wiener's attack is due to its simplicity. It can be easily checked against, especially with code. Due to this simplicity compared to Coppersmith's attack, we know that it is better to pick a large d such that Wiener's condition is not met and use methods such as Chinese Remainder Theorem for faster decryption.

This basic Coppersmith attack was chosen due to Coppersmith theorem being the basis for many other types of attack on RSA vulnerability such as ROCA vulnerability. It can also be used for other attack methods for example Boneh and Durfee attack or targeting the MSB instead. I believe Professor Sourav wrote about this in his paper with Santanu Sarkar and Subhamoy Maitra on Partial Key Exposure Attacks Improvements. Hopefully, this can provide a simple understanding of Coppersmith Theorem such that we can learn from this and implement other techniques that also uses Coppersmith Theorem.


#### Research

Some mathematical knowledge is required to understand both attacks. Required mathematical knowledge are:
1. Continued Fractions + Convergents
2. Coppersmith Theorem (Don't have to know in depth YET but have to understand what the theorem does. I.E given f(x,y)=polynomial with two variables over integers Z. x and y can be found in polynomial time under certain conditions.)


#### Design & Development

The notebook only features the backend logic and functions as well as demonstration of work + proof of concept. (N, public exponent e etc have to be manually fed into the relevant functions). Future development could include frontend UI for users to input N,e. As we implement more attacks, different attack could be automatically chosen for different type of input if we want a more consumer-based product. Wiener's attack implementation is referenced from lecture slides. Coppersmith Attack is referenced from numerous online articles. Further improvement could include better implementation of sage methods such as .small_roots() by creating polynomial rings for faster computation of factors. Current implementation is naive. More experience with sage required.


#### Use of code

Wiener's attack can be used if we know that d < 1/3* N^1/4. Else, if e is unusually large, we can also try wiener's attack on the suspicion that d will be short due to large e. Main drawback of Wiener's attack is that Wiener's condition can't be checked, hence we could run the attack and get no results in return, most likely due to failure to meet Wiener's condition.

Coppersmith's attack can be used as long as we know the last n/4 bits of key d. Time complexity is O(en^a) for some value of a where n refers to number of bits hence, e is required to be small as it is linear in e. This linearity can be explained as the first part of the algorithm loops through all values of e while the factoring steps at the end takes n^a for some value of a. 

An example use case of coppersmith's attack would be to employ side channel attacks along with coppersmith attack. Side channel attacks such as power tracing or timing attacks can allow us to find info about the private key. We would then target the LSB and once we obtain n/4 LSB, we can use the coppersmith attack implementation to find out the rest of the key.
