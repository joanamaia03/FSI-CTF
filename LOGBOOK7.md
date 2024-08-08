# 

## Task 1 - Crashing the program

Ao passarmos a string %s não aparece a mensagem "returned properly" no terminal, o que significa que o programa não funcionou propriamente.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook7/image_1.png?ref_type=heads)
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook7/image_2.png?ref_type=heads)

## Task 2 - Printing out the server program's memory

### 2.a - Stack Data

Passamos AAAA de modo a adicionar este valor à stack, usando de seguida uma sequência de %x de modo a encontrar a posição na qual estamos a escrever o caracter A que corresponde ao valor 41 em hexadecimal.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook7/image_3.png?ref_type=heads)
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook7/image_4.png?ref_type=heads)

### 2.b - Heap Data

Ao escrevemos o endereço da mensagem secreta no início da stack, usando %x como placeholder, o %s irá ler a string no endereço que escrevemos.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook7/image_5.png?ref_type=heads)

## Task 3 - Modifying the Server Program's memory

### 3.a - Change the value to a different value

Ao escrevermos o indereço no início da stack, usando %x como placeholder, o %n vai escrever o número de caracteres que escrevemos antes do %n.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook7/image_6.png?ref_type=heads)

### 3.b - Change the value to 0x5000

O valor do target deve ser mudado para um valor concreto: 5000 corresponde a 20408 em decimal, 4 corresponde aos bytes do endereço, 63 por cada endereço representado pelo %x, o que no fim resulta em 638. X=20408-4-633=20215. Introduzimos este valor num %x para adicionarmos caracteres extra e assim escrevermos 5000 no endereço destino.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook7/image_7.png?ref_type=heads)

