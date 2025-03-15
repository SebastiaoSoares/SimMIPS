# SimMIPS  

SimMIPS é um microprocessador programável desenvolvido no **Logisim**, baseado em uma arquitetura inspirada no **MIPS**. O projeto tem como objetivo explorar conceitos de arquitetura de computadores, instruções RISC e implementação de processadores no ambiente de simulação do Logisim.

## Sumário
- [Equipe](#equipe);
- [Instruções já implementadas](#instruções-já-implementadas);
- [Como usar](#como-usar);
- [O circuito](#o-circuito);
- [Em desenvolvimento](#em-desenvolvimento);

## Equipe
A equipe do trabalho elaborado na disciplina de Arquitetura e Organização de Computadores, do curso de Ciência da Computação da Universidade Federal do Cariri (UFCA), é composta pelos seguintes membros:

**Estudantes:**
- Sebastião Sousa Soares
- Bruno da Silva Macedo

**Professor:**
- Ramon Nepomuceno

## Instruções já implementadas  
Até o momento, o SimMIPS suporta as seguintes instruções:  

### Tipo R  (OPCODE: 000000)
- `add`     (FUNCT: 000000)
- `sub`     (FUNCT: 000001)
- `mul`     (FUNCT: 000010)
- `div`     (FUNCT: 000011)
- `and`     (FUNCT: 000100)
- `or`      (FUNCT: 000101)
- `slt`     (FUNCT: 000110)

### Tipo I
- `addi`    (OPCODE: 000001)
- `subi`    (OPCODE: 000010)
- `muli`    (OPCODE: 000011)
- `divi`    (OPCODE: 000100)
- `beq`     (OPCODE: 000101)
- `lw`      (OPCODE: 000111)
- `sw`      (OPCODE: 001000)
- `bne`     (OPCODE: 001001)
- `slti`    (OPCODE: 001010)

### Tipo J
- `jump`    (OPCODE: 000110)

### Formato das instruções
* **Tipo R**: OPCODE (6 bits) | RS (5 bits) | RT (5 bits) | RD (5 bits) | SHAMT (5 bits) | FUNCT (6 bits)
* **Tipo I**: OPCODE (6 bits) | RS (5 bits) | RT (5 bits) | IMEDIATO (16 bits)
* **Tipo J**: OPCODE (6 bits) | LABEL (26 bits)

### Exemplo de instrução
Instrução ASM:
```asm
addi $t1, $t0, 5
```
Significado e código de máquina:
```
$t0 = $t1 + 5   # 000001 00001 00000 0000000000000101 (bin) | 04200005 (hex)
```

## Como usar  
1. Abra o arquivo `.circ` no **Logisim**  
2. Carregue um programa na memória RAM (como a instrução de exemplo "instruction.txt")  
3. Execute o processador e observe os resultados nos registradores e na memória  

## O circuito

### Instruções do Tipo R
*add, sub, mul, div, and, or, slt*

Essas instruções são efetuadas, de modo geral, dentro da ULA (Unidade Lógica Aritmética). A UC (Unidade de Controle) envia a informação de que está sendo efetuada uma instrução do tipo R (opcode "000000"), que, por sua vez, espera um RS e um RT, para efetuar a operação desejada (indicada pelo funct específico), um RD para armazenar o resultado e o funct. Do funct é extraída a menor quantidade de bits necessária para indicar a um MUX qual função deve ser escolhida para ser registrada em RD.

As instruções add, sub, mul e div, utilizam suas operações específicas. And e or utilizam as portas lógicas correspondentes. Por fim, slt faz uso do comparador de magnitude. Todos dentro da ULA.

## Em desenvolvimento  
- Expandindo o conjunto de instruções
