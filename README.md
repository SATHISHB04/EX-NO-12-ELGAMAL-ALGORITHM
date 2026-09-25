# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```#include <stdio.h>
#include <string.h>

int power(int a, int b, int p)
{
    int r = 1;

    while (b > 0)
    {
        r = (r * a) % p;
        b--;
    }

    return r;
}

int main()
{
    int p = 257, g = 3;
    int a, k, y, c1, c2, d;
    char msg[100];
    int i;

    printf("Enter Alice private key: ");
    scanf("%d", &a);

    printf("Enter message: ");
    scanf("%s", msg);

    printf("Enter random k: ");
    scanf("%d", &k);

    y = power(g, a, p);
    c1 = power(g, k, p);

    printf("Alice public key: %d\n", y);
    printf("Encrypted message: ");

    for (i = 0; i < strlen(msg); i++)
    {
        c2 = (msg[i] * power(y, k, p)) % p;
        printf("%d ", c2);
    }

    printf("\nDecrypted message: ");

    for (i = 0; i < strlen(msg); i++)
    {
        c2 = (msg[i] * power(y, k, p)) % p;
        d = (c2 * power(c1, p - 1 - a, p)) % p;
        printf("%c", d);
    }

    return 0;
}
```

## Output:

<img width="654" height="333" alt="Screenshot 2026-03-09 101453" src="https://github.com/user-attachments/assets/70d69f35-34ef-48d7-a465-631ce7b31651" />

## Result:
The program is executed successfully.
