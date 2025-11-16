# EX-NO-13 — MESSAGE AUTHENTICATION CODE (MAC)

## AIM:
To implement a Message Authentication Code (MAC) to verify message integrity and authenticity using a shared secret key.

## ALGORITHM:

1. **Message Authentication Code (MAC):**  
   A cryptographic method to ensure message integrity and authenticity using a secret key.

2. **Initialization:**  
   - Choose a hash function (or simple XOR here).  
   - Choose a secret key **K**.  
   - Take message **M** as input.

3. **MAC Generation:**  
   Compute MAC using:  
   \[
   \text{MAC}(M, K) = H(K || M)
   \]  
   Here, XOR is applied to each byte of the message and key.

4. **Verification:**  
   - Receiver calculates the MAC using the same key.  
   - If computed MAC matches the sent MAC → message is authentic.

5. **Security:**  
   MAC security depends on secrecy of key **K** and strength of hash function.

## PROGRAM:
```c
#include <stdio.h>
#include <string.h>

#define KEY "secretkey"  // Shared secret key

// Function to calculate a simple MAC using XOR
unsigned int calculate_mac(const char *message, const char *key)
{
    unsigned int mac = 0;
    int i;

    for (i = 0; i < strlen(message); i++)
    {
        mac ^= message[i];
    }

    for (i = 0; i < strlen(key); i++)
    {
        mac ^= key[i];
    }

    return mac;
}

int main()
{
    char message[256];
    unsigned int mac_sent, mac_received;

    // Input message from user
    printf("Enter the message: ");
    fgets(message, sizeof(message), stdin);
    message[strcspn(message, "\n")] = '\0'; // Remove newline

    // Sender generates MAC
    mac_sent = calculate_mac(message, KEY);
    printf("Generated MAC (sent): %u\n", mac_sent);

    // Receiver calculates MAC
    mac_received = calculate_mac(message, KEY);
    printf("Calculated MAC (received): %u\n", mac_received);

    // Verify integrity
    if (mac_sent == mac_received)
    {
        printf("Message is authentic.\n");
    }
    else
    {
        printf("Message integrity check failed.\n");
    }

    return 0;
}
```

## OUTPUT:
<img width="714" height="318" alt="image" src="https://github.com/user-attachments/assets/05d21fc8-7633-4505-ba9c-54ccde4af672" />



## RESULT:
The Message Authentication Code (MAC) was successfully generated and verified, ensuring message integrity and authenticity.
