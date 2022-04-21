# Vigenère cipher

## Introduction
The Vigenère cipher  is a method of encrypting alphabetic text by using a series of interwoven Caesar ciphers, based on the letters of a keyword. It employs a form of polyalphabetic substitution.

First described by Giovan Battista Bellaso in 1553, the cipher is easy to understand and implement, but it resisted all attempts to break it until 1863, three centuries later. This earned it the description le chiffrage indéchiffrable (French for 'the indecipherable cipher'). Many people have tried to implement encryption schemes that are essentially Vigenère ciphers. In 1863, Friedrich Kasiski was the first to publish a general method of deciphering Vigenère ciphers.

In the 19th century the scheme was misattributed to Blaise de Vigenère (1523–1596), and so acquired its present name.

## Description

In a [Caesar cipher](https://en.wikipedia.org/wiki/Caesar_cipher "Caesar cipher"), each letter of the alphabet is shifted along some number of places. For example, in a Caesar cipher of shift 3, `a` would become `D`, `b` would become `E`, `y` would become `B` and so on. The Vigenère cipher has several Caesar ciphers in sequence with different shift values.

To encrypt, a table of alphabets can be used, termed a _[tabula recta](https://en.wikipedia.org/wiki/Tabula_recta "Tabula recta")_, _Vigenère square_ or _Vigenère table_. It has the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows. The alphabet used at each point depends on a repeating keyword.

For example, suppose that the to be encrypted is

`attackatdawn`.

The person sending the message chooses a keyword and repeats it until it matches the length of the plaintext, for example, the keyword "LEMON":

`LEMONLEMONLE`

Each row starts with a key letter. The rest of the row holds the letters A to Z (in shifted order). Although there are 26 key rows shown, a code will use only as many keys (different alphabets) as there are unique letters in the key string, here just 5 keys: {L, E, M, O, N}. For successive letters of the message, successive letters of the key string will be taken and each message letter enciphered by using its corresponding key row. The next letter of the key is chosen, and that row is gone along to find the column heading that matches the message character. The letter at the intersection of `key-row, msg-col` is the enciphered letter.

For example, the first letter of the plaintext, `a`, is paired with `L`, the first letter of the key. Therefore, row `A` and column `L` of the Vigenère square are used, namely `L`. Similarly, for the second letter of the plaintext, the second letter of the key is used. The letter at row `T` and column `E` is `X`. The rest of the plaintext is enciphered in a similar fashion:

Plaintext:

`attackatdawn`

Key:

`LEMONLEMONLE`

Ciphertext:

`LXFOPVEFRNHR`

Decryption is performed by going to the row in the table corresponding to the key, finding the position of the ciphertext letter in that row and then using the column's label as the plaintext. For example, in row `L` (from `_L_EMON`), the ciphertext `L` appears in column `A`, so `a` is the first plaintext letter. Next, in row `E` (from `L_E_MON`), the ciphertext `X` is located in column `T`. Thus `t` is the second plaintext letter.

## Algebraic 
https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher#Algebraic_description


## Cryptanalysis
https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher#Cryptanalysis


## Code

```python
# Function

# - Encrypt
# - Decrypt
# - Brute force


import string




################################## GLOBAL ###########################################################


ALPHABET = string.ascii_lowercase

#https://en.wikipedia.org/wiki/Letter_frequency

ALPHABET_ENGLISH_FREQ = {"a": 0.082, "b":0.015, "c":0.028, "d":0.043, "e":0.13, "f":0.022, "g":0.02, "h":0.061, "i":0.07, "j":0.0015, "k":0.007, "l": 0.04, "m":0.024, "n":0.067, "o":0.075, "p":0.019, "q": 0.00095, "r":0.06, "s": 0.063, "t":0.091, "u":0.028, "v":0.0098,"w":0.024, "x":0.0015, "y": 0.02, "z":0.00074}


############################# Function principal ###################################################

# Encrypt
def encrypt(_message, _key):

	cipher_message = ""

	for block in _message:
		for index in range(len(block)):

			if block[index] not in ALPHABET:
				cipher_message += block[index]
				continue

			cypher_letter_number = (ALPHABET.index(block[index]) + ALPHABET.index(_key[index])) % 26
			cipher_message += ALPHABET[cypher_letter_number]

	return cipher_message


# Decrypt
def decrypt(_cipher_text, _key):
	plaint_text = ""
	for block in _cipher_text:
		for index in range(len(block)):
			if block[index] in ALPHABET:
				plain_letter_number = (ALPHABET.index(block[index]) - ALPHABET.index(_key[index])) % 26
				plaint_text += ALPHABET[plain_letter_number]
			else:
				plaint_text += block[index]
	return  plaint_text


# Brute force

def crack_the_key(_message, _key_length=0):
	
	if(_key_length == 0):
		key_length = get_length_key(_message)
	else:
		key_length = _key_length



	key = find_key(_message, key_length)

	test = chunking_message_key_length(_message, len(key))

	plaint_text = decrypt(test, key)

	plaint_text = format_message_read(_message, plaint_text)


	return plaint_text


################################# Crack the key function ####################################################


def get_length_key(_message):

	#change 20 for more sample
	result_Ic_avg = []
	for i in range(2, 10):
		cipher_chunked = chunking_message_key_length(_message, i)

		array_sample = get_each_letter(cipher_chunked, i)
		
		Ic_avg = 0

		for block in array_sample:
			frequence = frequence_of_letter(block)
			Ic_avg += IC(frequence, len(block))

		Ic_avg /= i

		result_Ic_avg.append(Ic_avg)

		#debug
		#print(f"key length: {i} : Ic_avg: {Ic_avg}")

		#HELP
		#English	0.0667		French	0.0778
		#German		0.0762		Spanish	0.0770
		#Italian	0.0738		Russian	0.0529	

	list_of_key_length = []

	print("----List of key length----")
	print("")
	#debug
	#print(result_Ic_avg)

	for ic_avg in result_Ic_avg:
		if(ic_avg <= 0.0667 and ic_avg >= 0.06):
			print(f"Keys length: {result_Ic_avg.index(ic_avg) + 2}")
			list_of_key_length.append(result_Ic_avg.index(ic_avg) + 2)



	# Not sure of this
	for length in list_of_key_length:
		test = 0
		for length_tmp in list_of_key_length:
			if((length_tmp % length) == 0):
				test += 1
			if(test == len(list_of_key_length)):
				length_key = length
				print()
				print(f"---Length keys most accurate--")
				print()
				print(f"Length: {length_key}")
				return length_key 

		return 0



	

	return

def find_key(_message, _key_length):
	cipher_chunked = chunking_message_key_length(_message, _key_length)
	array_sample = get_each_letter(cipher_chunked, _key_length)

	key = ""

	# Each letter in sample is encrypt with the same key letter
	for sample in array_sample:
		#Ceasar brute A-Z
		tmp_list_chi = []
		for letter in ALPHABET:

			sample_decrypt = decrypt(sample, letter)
			frequence = frequence_of_letter(sample_decrypt)

			chi_squared_sum = chi_squared_stat(frequence, len(sample))

			tmp_list_chi.append(chi_squared_sum)
			# Debug 
			#print(f"letter: {letter}  chi_squared: {chi_squared_sum}")
		#Debug	
		#print("next key letter")
		min_chi_square = min(tmp_list_chi)
		key += ALPHABET[tmp_list_chi.index(min_chi_square)]

	print()
	print("----Key-----")
	print()
	print(f"Key: {key}")
	print()
	print("------Plaint text----------")
	print()

	return key


###################### HELP #######################################################################"""

def get_each_letter(_cipher_chunked, _position):
	array_of_nth_letter = []# array with n(key length) array of every position letter

	for j in range(_position): # 4(test key length) - 1 = 3
		tmp_array = [] 
		for chunk in _cipher_chunked:
			if(j < len(chunk)):
				tmp_array.append(chunk[j]) # every i letter of chunk

		array_of_nth_letter.append(tmp_array)

	return array_of_nth_letter



def frequence_of_letter(_sample):

	frequence = {}

	for letter in ALPHABET:
		frequence[letter] = 0


	for letter in _sample:
		frequence[letter] += 1

	return frequence


def IC(_frequence, _length_sample):

	Ic = 0
	for letter, val in _frequence.items():
		Ic += (val*(val-1)) / (_length_sample*(_length_sample - 1)) # (Fi * (Fi - 1)) / (N*(N-1)) with Fi = frequence of letter N = length of text


	return Ic

def chi_squared_stat(_frequence, _length_sample):
	chi_squared_sum = 0
	for letter, val in _frequence.items():
		chi_squared = ((val - (_length_sample *ALPHABET_ENGLISH_FREQ[letter])) ** 2) / (_length_sample * ALPHABET_ENGLISH_FREQ[letter])
		chi_squared_sum += chi_squared

	return chi_squared_sum


################################## FORMAT FUNCTION ##########################################################


# Formate message for calcule
def chunking_message_key_length(_message, _length):


	_message = _message.lower()

	#replace all non ascii charactere 
	for char in _message:
		if char not in ALPHABET:
			_message = _message.replace(char, "")



	list_block_message = [_message[i : i + _length] for i in range(0, len(_message), _length)] # range(start, stop, step) && _message[i : i + _length] => exclu i + _length
	return list_block_message



#Format message for reading
def format_message_read(_original_message, _result_message):

	result_message_format = list(_result_message)

	for index in range(len(_original_message)):
		if(_original_message[index].isupper()):
			result_message_format[index] = result_message_format[index].upper()
			continue
		if(_original_message[index] not in ALPHABET):
			result_message_format.insert(index, _original_message[index])
		

	return ''.join(result_message_format)



################################ MAIN FUNCTION ###############################################################

def main():

	key = "gfla"
	message = open("message.txt", "r").read()
	print()

	#message = "bj labw exlwszx mk ybrv B pmf maefdl"

	#message_chunked = chunking_message_key_length(message, len(key))

	#cipher_text = encrypt(message_chunked, key)
	#plaint_text = decrypt(message_chunked, key)

	#get_length_key(message)
	#test="Neiynytkwpsznygnthitmtsztcyvjzprjzfzjyrkhpibjnrkittltctnnygyyseeitdttecxjltk"
	#IC(frequence_of_letter(test.lower()), len(test))

	#find_key(message, 4)

	print(crack_the_key(message))

	#print(format_message_read(message, plaint_text))



	return

if __name__ == "__main__":
	main()

# Test


```