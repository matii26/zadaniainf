# zadaniainf


dane_6_1

def encrypt(word, key):
    encrypted_word = ""
    for char in word:
        encrypted_char = chr(ord(char) + key)
        encrypted_word += encrypted_char
    return encrypted_word

def main():
    input_filename = "dane_6_1.txt"
    output_filename = "wyniki_6_1.txt"
    key = 107

    try:
        with open(input_filename, 'r') as input_file, open(output_filename, 'w') as output_file:
            words = input_file.read().split()
            for word in words:
                encrypted_word = encrypt(word, key)
                output_file.write(encrypted_word + '\n')
        print(f"Słowa zostały zaszyfrowane i zapisane do pliku {output_filename}")
    except FileNotFoundError:
        print(f"Plik {input_filename} nie został znaleziony.")
    except Exception as e:
        print(f"Wystąpił błąd: {str(e)}")

if __name__ == "__main__":
    main()


dane_6_2


def odszyfruj(szyfrogram, klucz):
    odszyfrowane_slowo = ""
    for znak in szyfrogram:
        odszyfrowany_znak = chr(ord(znak) - int(klucz))
        odszyfrowane_slowo += odszyfrowany_znak
    return odszyfrowane_slowo

# Otwórz plik z danymi
with open('dane_6_2.txt', 'r') as dane_file:
    lines = dane_file.readlines()

# Otwórz plik wynikowy
with open('wyniki_6_2.txt', 'w') as wyniki_file:
    # Iteruj przez każdą linię w pliku z danymi
    for line in lines:
        # Podziel linię na szyfrogram i klucz
        szyfrogram, klucz = line.split()
        
        # Odszyfruj słowo i zapisz wynik w pliku wynikowym
        odszyfrowane_slowo = odszyfruj(szyfrogram, klucz)
        wyniki_file.write(odszyfrowane_slowo + '\n')

print("Odszyfrowane słowa zapisane w pliku wyniki_6_2.txt.")



dane_6_3


def decrypt(word, key):
    decrypted_word = ""
    for char in word:
        decrypted_word += chr((ord(char) - ord('A') - key) % 26 + ord('A'))
    return decrypted_word

def find_errors(input_file, output_file):
    with open(input_file, 'r') as file:
        lines = file.readlines()

    decrypted_words = []
    for line in lines:
        words = line.split()
        original_word = words[0]
        encrypted_word = words[1]
        key = 0

        while decrypt(encrypted_word, key) != original_word:
            key += 1

        decrypted_words.append(decrypt(encrypted_word, key))

    with open(output_file, 'w') as file:
        for word in decrypted_words:
            file.write(word + '\n')

if __name__ == "__main__":
    input_file = "dane_6_3.txt"
    output_file = "wyniki_6_3.txt"
    find_errors(input_file, output_file)
