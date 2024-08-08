# CTF9

## Vulnerability Analysis
A função gen gera uma key de 16 bytes, onde apenas 3 desses bytes são random e os restantes são iniciados a \x00. Tal reduz a segurança da key, pois torna-a bastante mais fácil de adivinhar.

Devido à existência de poucas keys possíveis, podemos fazer uso de bruteforce para a adivinhar!

Podemos automatizar este processo de modo a que quando a "flag{" seja encontrada, saiba que encontrou a key correta.

## Exploit

```
def brute_force_attack(ciphertext, nonce):
    # We know that the key is 16 bytes long, and the first 13 bytes are '\x00'
    key_prefix = b'\x00' * 13

    # We'll try all possible combinations for the last 3 bytes
    counter = 0
    for i in itertools.product(range(256), repeat=3):
        # Increment the counter
        counter += 1

        # Print the counter every 1,000,000 keys
        if counter % 1000000 == 0:
            print(f"Tried {counter} keys so far")

        # Construct the key
        key = key_prefix + bytes(i)

        # Try to decrypt the ciphertext
        plaintext = dec(key, ciphertext, nonce)

        # If the plaintext starts with "flag{", we've found the key
        if plaintext.startswith(b"flag{"):
            return key, plaintext

    # If we get here, the brute force attack failed
    raise Exception("Brute force attack failed")
 ```
