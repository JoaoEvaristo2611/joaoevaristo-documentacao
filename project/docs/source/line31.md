# Line 31
**Autor**: João Evaristo

### Indice
- [Introdução](#introducao)
- [Trabalho Realizado](#trabalho-realizado)
    - [Estação 10](#estacao-10)
        - [Tags](#tags-10)	
        - [Grafcet(Automático)](#grafcets-estacao-10-automatico)
    - [Estação 20](#estacao-20)   
        - [Tags](#tags-20)
        - [Grafcet (Automático)](#grafcets-estacao-20-automatico)   
    - [Estação 30](#estacao-30)
        - [Tags](#tags-30)
        - [Grafcet(Automático)](#grafcets-estacao-30-automatico)    
    - [Estação 40](#estacao-40)
        - [Tags](#tags-40)
        - [Grafcet (Automático)](#grafcets-estacao-40-automatico)  
    - [Estação 50](#estaçao-50)
        - [Tags](#tags-50)
        - [Grafcet sem rejeição(Automático)](#grafcets-estacao-50-sem-rejeicao-automatico)
        -[Grafcet com rejeição(Automático)](#grafcets-estacao-50-com-rejeicoes-automatico)
        - [Fluxogramas](#fluxogramas)
            - [Fluxograma Estação 50 sem rejeições (Inteiro)](#fluxograma-estacao-50-com-rejeicoes-inteiro)
            - [Fluxograma Estação 50 com rejeições(Partes)](#fluxograma-estacao-50-com-rejeicoes-partes)
        - [Texto estreturado](#programacao-de-texto-estruturado)

    

### Introdução
A linha 31 faz parte dos grupo 30. Essa linha e dividida por 5 estações que são **"Transporte"**, **"colocação de corpo"**,**"Prensa"**, **"Colocação de miolo"** e **"Tapete de verificação de peças"**. 
Este trabalho foi programado em LEADER e texto estreturado 

### Trabalho Realizado:
<br /><br />

#### Estação 10
<br /><br />
Esta estação esta equipa com 2 fins de curso, um servo motor, 5 sensores e 3 cilindros.
Esta estação começa a funcionar assim que receber informação que a 20 ja fez o seu trabalho. Quando ele receber essa informação o carrinho da estação 10 ira estar na posição 0.000mm que e onde a estação 20 esta, depois do carrinho estiver nessa posição a garra vai a frente e vai fechar, logo a seguir de fechar o carrinho vai levantar e vai recuar. Quando recuar o carrinho vai para a posição da estação 30 que é em 287.2048mm, ao chegar o carro vai avançar e vai deixar a peça e enquanto as estação 30 estiver a trabalhar a 10 fica a espera e assim que acabar o carro vai buscar lhe e depois vai para a estação 40 que fica em 776.1536 mm e ira fazer o mesmo que tem feito nas outras. Logo a seguir vai entregar na 50 que e em 1051.882mm e logo a seguir vai voltar para a posição Home.    
Como fazer o carinho andar 
<br /><br />

##### Como fazer o carinho andar 
Para este processo 5 blocos de funções que são: MC_Home, MC_Reset, MC_Halt, Mc_Home e MC_MoveAbsolute


MC_Power – é uma função que deve ser chamada e ligada antes de qualquer instrução de movimento, sem ela não será possível comando o servo.
![Estação10](./lines/line31/2020_2021/Software/Imagens/PLC10.jpg)
<br /><br />

##### Tags 10
<br />

###### Entradas
<br /><br />

| Tags                      | Inputs        | comments                      | 
| --------------------------|---------------| ------------------------------|
| Axis_1_Homing_switch      | %I0.0         | Fim de curso tras             |
| Axis_1_HighHw_LimitSwitch | %I0.1         | Fim de Curso(Frente)          |
| Axis_1_LowHw_LimitSwitch  | %I0.2         | Sensor de Frente              |
| 3121010B10                | %I0.3         | Sensor de Movimento(Baixo)    |
| 311010B11                 | %I0.4         | Sensor de Movimento(Cima)     |
| 311020B20                 | %I0.5         | Sensor de Rotacao(Esquerda)   |
| 311020B21                 | %I0.6         | Sensor de Posicao(Direita)    |
| 311030B10                 | %I0.7         | Sensor de Pos.Av              |
| 311030B11                 | %I1.0         | Sensor de Pos.Rec             |
| 3110G10                   | %I1.1         | Sensor de Garra               |
| 311920SB2                 | %I8.4         | STOP                          |
| 311920SB1                 | %I8.5         | START                         |
| 311920QS                  | %I8.6         | Botao de emergencia           |
| 311920SA                  | %I8.7         | Seletor                       |
<br /><br />

###### Saidas

| Tags             | Outputs  | comments                      |
| -----------------|----------| ------------------------------|
| Axis_1_Pulse     |%Q0.0     |                               |
| Axis_1_Direction |%Q0.1     |                               |
| 3110Y10          |%Q0.3     | Cilindro Vertical             |
| 3110Y20A         |%Q0.4     | Cilindro Rotacional(Esquerda) |
| 3110Y20B         |%Q0.5     | Cilindro Rotacional(Direita)  |
| 3110Y30          |%Q0.6     | Cilindro Horizontal           |
| 3110GA           |%Q0.7     | Fechar Garra                  |
| 3110GB           |%Q1.0     | Abrir Garra                   |
| 31192011         |%Q8.5     | Luz Laranja                   |
| 31192012         |%Q8.6     | Luz Verde                     |
| 31192013         |%Q8.7     | Luz Encarnada                 |
<br /><br />

##### Grafcets Estação 10 (Automatico)
<br /><br />

![](./lines/line31/2020_2021/Software/Grafecet/PLC19.svg)

<br /><br />

#### Estação 20
<br /><br />
Esta estação e composta por 8 sensores e 2 cilindros.
Esta estação começa a funcionar assim que o sensor baixo do copo ativar, assim que este ativar o cilindro de cima ira para a frente e logo a seguir o de baixo também vai a frente e logo a seguir vai recuar e o de cima também ira fazer o mesmo. Esta estação so voltara a funcionar quando o sensor da base deixar de detetar.  

![Estação 20](./lines/line31/2020_2021/Software/Imagens/PLC20.jpg)
<br /><br />

##### Tags 20
<br /><br />

###### Entradas
<br /><br />

| Tags      | Inputs | comments                    | 
| -----     |--------| ----------------------------|
| 3130B21   | %I0.0  | Sensor de frente            |
| 3120B22   | %I0.1  | Sensor de Trás              |
| 3120B11   | %I0.2  | Sensor de Frente            |
| 3120B12   | %I0.3  | Sensor de Trás              |
| 3120B40   | %I0.4  | Sensor Base                 |
| 3120B31   | %I0.5  | Sensor de Cima(Tubo)        |
| 3120B32   | %I0.6  | Sensor de Baixo(Tubo)       |
| 3120B33   | %I0.7  | Sensor Metálico(Tubo)       |
| 3129SB2   | %I1.2  | Stop                        |
| 3129QS    | %I1.3  | Start                       |
| 311920SA  | %I1.4  | Switch de Emergência        |
| 3120SA    | %I1.5  |   Seletor                   |
<br /><br />

###### Saidas

| Tags             | Outputs  | comments                      |
| -----------------|----------| ------------------------------|
| 3120Y20          |%Q0.0     | Cilindro Superior             |
| 3120Y10          |%Q0.1     | Cilindro Inferior             |
| 292011           |%Q0.7     | Luz Laranja                   |
| 292012           |%Q1.0     | Luz Verde                     |
| 292013           |%Q1.1     | Luz Encarnada                 |
<br /><br />

##### Grafcets Estação 20 (Automatico)
<br /><br />

![](./lines/line31/2020_2021/Software/Grafecet/PLC29.svg)
<br /><br />

#### Estação 30
<br /><br />

Esta estação  tem cerca de 6 sensores e 3 cilindros. Esta estação so ira começar a trabalhar quando a 10 for la meter a peça quando este a meter a copo ira fechar e a ira para trás quando este tiver la a prensa ira descer e ira voltar par cima. Logo a seguir o cpo ira voltar a frente e a estação 20 ira ficar a esperar que a 10 vai buscar a peça e volte a por outra. 

<br /><br />

![Estação 30](./lines/line31/2020_2021/Software/Imagens/PLC30.jpg)

<br /><br />

##### Tags 30
<br /><br />

###### Entradas
<br /><br />

| Tags      | Input  | comments                    | 
| -----     |--------| ----------------------------|
| 3130B21   | %I0.0  | Sensor Garra                |
| 3130B22   | %I0.1  | Sensor Garra Fechada        |
| 3130B11   | %I0.2  | Sensor de Trás (Base)       |
| 3130B12   | %I0.3  | Sensor de Frente(Base)      |
| 3130B31   | %I0.4  | Sensor de Pos.Rec(Prensa)   |
| 3130B32   | %I0.5  | Sensor de Pos.Av(Prensa)    |
| 3139SB2   | %I1.2  | Stop                        |
| 3139SB1   | %I1.3  | Start                       |
| 3139QS    | %I1.4  | Switch de Emergência        |
| 3139SA    | %I1.5  | Switch ON/OFF               |
<br /><br />

###### Saidas

| Tags      | Outputs  | comments           |
| -----     |----------| -------------------|
| 3130Y20   |%Q0.0     | Garra              |
| 3130Y10   |%Q0.2     | Base               |
| 3130Y30   |%Q0.3     | Prensa             |
| 392011    |%Q0.7     | Luz Laranja        |
| 392012    |%Q1.0     | Luz Verde Garra    |
| 392013    |%Q1.1     | Luz Encarnada Garra|


##### Grafcets Estação 30 (Automatico)
<br /><br />

![](./lines/line31/2020_2021/Software/Grafecet/PLC39.svg)
<br /><br />

#### Estação 40
<br /><br />
Esta estação e composta por 16 sensores e 6 cilindros.Esta estação esta estação esta dividida em 2 processos a primeira que é onde esta o armazenamento dos miolo ira começar o seu processo quando o sensor baixo do copo detetar um miolo. Quando isto acontecer o cilindro de cima ira avançar e o de baixo ira recuar permitindo assim o processamento do miolo.Quando fizer o processamento ira parar a um prato que ira rodar e esperar que a garra o va buscar e assim poderá fazer tudo de novo. Ja o segundo processo so ira começar a processar quando o prato rodar e o sensor ativar e quando a estação 10 for meter la o corpo.
Quando isto tiver tudo feito a garra ira descer pegar no miolo e voltar acima, e a seguir vai a frente descer e meter o miolo no copo assim fazendo o produto final.
Q
<br /><br />

![Estação 40](./lines/line31/2020_2021/Software/Imagens/PLC40.jpg)
<br /><br />

##### Tags 40
<br /><br />

###### Entradas

<br /><br />

| Tags      | Input  | comments                    |
| -----     |--------| ----------------------------|
| 314020B11 | %I0.0  | Sensor Tubo em cima         |
| 314020B10 | %I0.1  | Sensor Tubo em baixo        |
| 314010B31 | %I0.2  | Sensor Prato lado Esq.      |
| 314010B30 | %I0.3  | Sensor Prato lado Dir.      |
| 314010B10 | %I0.4  | Sensor Tubo                 |
| 314020B21 | %I0.5  | Sensor á Frente             |
| 314020B20 | %I0.6  |Sensor a trás                |
| 314020B30 | %I0.7  | Sensor á Frente             |
| 314020B31 | %I1.0  | Sensor a trás               |
| 314010B20 | %I1.1  | Sensor posição inicial      |
| 314030B21 | %I1.2  | Sensor Mov.(Prato)          |
| 314030B10 | %I1.3  | Sensor Garra                |
| 314930B41 | %I1.4  | Sensor de Garra em baixo    |
| 314030B40 | %I1.5  | Sensor de garra em cima     | 
| 314030B51 | %I8.0  | Sensor de Trás              |
| 314030B50 | %I8.1  | Sensor de Frente            |
| 3149SB2   | %I8.2  | Stop                        |
| 3149SB1   | %I8.3  | Start                       |
| 3149QS    | %I8.4  | Switch de Emerg.            |
| 3149SA    | %I8.5  | Switch ON/OFF               |
<br /><br />

###### Saidas

| Tags             | Outputs  | comments                     |
| -----------------|----------| -----------------------------|
| 314020Y10        |%Q0.0     | Cilindro Baixo do Tubo       |
| 314020Y20        |%Q0.1     | Cilindro Cima do Tubo        |
| 314010R10        |%Q0.2     | Prato                        |
| 314030G10        |%Q0.3     | Garra                        |
| 314030Y20        |%Q0.4     | Cilindro Vertical            |
| 314030Y10        |%Q0.5     | Cilindro Horizontal          |
| 314040HL10       |%Q0.6     | Semáforo Encarnado           |
| 314040HL20       |%Q0.7     | Semáforo Laranja             |
| 314040HL30       |%Q1.0     | Semáforo Verde               |
| 4920HL1          |%Q8.5     | Luz Laranja                  |
| 4920HL2          |%Q8.6     | Luz verde                    |
| 4920HL3          |%Q8.7     | Luz Encarnada                |

##### Grafcets Estação 40 (Automatico)
<br /><br />

![](./lines/line31/2020_2021/Software/Grafecet/PLC49.svg)

<br /><br />

#### Estação 50
<br /><br />
Esta estação tem 9 sensores e 3 cilindros. Quando o carrinho 10 deixar a peça no tapete um dos sensores ira detetar essa peça o que ira fazer com que o tapete começe a andar. Quando este começar a andar a peça ira passar por 2 sensores um que deteta peças de metal e outro que deteta peças brancas e se o sensor de metal e o branco detetar quer dizer que a peça é  toda de metal o que ira fazer com que o primeiro cilindro ira para a frente assim metendo a peça no armazenamento correto. Quando so o sensor branco detetar quer dizer que a peça e branca por isso  será o segundo cilindro a ir a frente e quando nenhum desses nao detetar quer dizer que a peça e preta e assim  ira ser o terceiro cilindro a avançar. Mas quando as peças tiverem erradas nenhum dos cilindros ira a frente o que vai fazer com que a peça ira cair numa caixa de rejeições.
Para saber quando os sensores deviam atuar e os cilindros tivemos que fazer varias medições e para fazer essas tivemos que na programação fazer quando um dos sensores detetar ira aparecer no computador os valores. Ja para sabermos a distancia dos cilindros ja tivemos que fazer a mão .

<br /><br />

![Estação50](./lines/line31/2020_2021/Software/Imagens/PLC50.jpg)
<br /><br />

##### Tags 50
<br /><br />

###### Entradas
<br /><br />

| Tags      | Input  | comments         |
| -----     |--------| -----------------|
|           |I0.0	 |Encoder(Fase A)   |
|           |I0.1	 |Encoder(Fase B)   |
|           |I0.2    |Encoder(Fase C)   |
|3150B11	|I0.3	 |Sensor de Material|
|3150B12	|I0.4    |Sensor de Metálico|
|3150B13	|I0.5    |Sensor de Ótico   |
|3150B21	|I0.7    |Sensor(Cilindro 1)|
|3150B31	|I1.0    |Sensor(Cilindro 2)|
|3150B41	|I1.1    |Sensor(Cilindro 3)|				
|3159SB2	|I1.2    |Stop              |				
|3159SB1	|I1.3    |Start             |				
|3159QS	    |I1.4    |Switch de Emerg.  |				
|3159SA	    |I1.5    |Switch ON/OFF     |				
<br /><br />

###### Saidas

| Tags             | Outputs  | comments                      |
| -----------------|----------| ------------------------------|
| TP               |%Q0.0     | Motor (Rotação Av)            |
| TP(1)            |%Q0.1     | Motor (Rotação Rec)           |
| 3150Y20          |%Q0.4     | Cilindro 1                    |
| 3150Y30          |%Q0.5     | Cilindro 2                    |
| 3150Y40          |%Q0.6     | Cilindro 3                    |
| 592011           |%Q0.7     | Luz Amarela                   |
| 592012           |%Q1.0     | Luz Verde                     |
| 592013           |%Q1.1     | Luz Vermelha                  |

###### Grafcets Estação 50 sem rejeição(Automatico)
<br /><br />

![](./lines/line31/2020_2021/Software/Grafecet/PLC59_sem_rejeicoes.svg)
<br /><br />

###### Grafcets Estação 50 com rejeições(Automatico)
<br /><br />

![](./lines/line31/2020_2021/Software/Grafecet/plc59_com_rejeicoes.svg)  
<br /><br />

#### Fluxogramas
<br /><br /> 

##### Fluxograma Estação 50 com rejeições(Inteiro)
<br /><br />

![](./lines/line31/2020_2021/Software/Fluxograma/Fluxograma_PLC59_com_rejeicao_Inteiro.svg) 
<br /><br />

##### Fluxograma Estação 50 com rejeições(Partes)
<br /><br />

![](./lines/line31/2020_2021/Software/Fluxograma/Fluxograma_PLC59_com_rejeicao_partes.svg)
<br /><br />

##### Programação de texto Estruturado 
![](./lines/line31/2020_2021/Software/Texto_estruturado/1.png)

![](./lines/line31/2020_2021/Software/Texto_estruturado/2.png) 

![](./lines/line31/2020_2021/Software/Texto_estruturado/3.png)

![](./lines/line31/2020_2021/Software/Texto_estruturado/4.png)
