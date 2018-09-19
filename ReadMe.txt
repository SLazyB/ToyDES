ReadMe for HW1 Cryptography and Network Security I - HW1

User Input (Terminal):
The program asks for the user to enter a 10-bit key. This was decided over randomly generated key simply because the user is more likely to remember the key properly than a random. Also it allows for two people to agree upon a key in advance rather than after the encryption. The program then asks for a file for the program to encrypt. It will output the encrypted file into a new one called encrypt.txt.
For decryption, the user can decrypt immediately after encryption using the same key by entering the file to be decrypted. They can also change keys for decryption/encryption.

Key Construction:
The program takes in the 10-bit key entered by the user. The key is then permuted using the P10 function. All the permutations function similarly in that they construct new strings with the original input using the given reordering. After the permutation, the 10-bit segment is then split into two 5-bit sets. Both sets are then left shifted such that the leftmost bit is move to the right side. The two resulting sets are combined and permuted using the P8 function, which ignores the first two bits and outputs and 8-bit set. This 8-bit set is the first sub key. The second sub left shifts the two left shifted 5-bit sets once more and then runs them through P8. The result of this is the second sub key.

Encryption:
In the file input part, the file is encrypted line by line. Each line is encrypted letter by letter in the encryption function. The function reads in the 8-bit text and then runs it through the initial permutation function. The 8-bit output is then split in two 4-bit sets. The right half of the original set is then entering into the F function with the first sub key. The output is then xor'd with the left half of the original set. The result of this operation is entered into the F function again with the second sub key and xor'd with the right half of the original set.The result is then concatenated with the result of the first xor operation and entered into the inverse initial permutation function. The result of that is returned as the new 8-bit cipher text.

Decryptio
The same as the encryption function except the second sub key is used in place of the first sub key and the first in place of the second.

F Function:
The function takes in two values: an 4-bit set and the 8-bit sub key. The 4-bit set is expanded and permuted into an 8-bit set. This 8-bit set is then xor'd 8-bit sub key. The result is then split into two 4-bit sets. The left 4-bit set is substituted using the S0 substitution matrix. This takes the 1st and 4th bits and converts them from a binary value to the decimal value to be used as the row index of the matrix. The 2nd and 3rd bit is used as the column index. In my case the matrix contains 2-bit binary strings corresponding to the decimal values given by the professor. This process is repeated with the right half. The two outputs are then concatenated and entered into the P4 function before being outputted.