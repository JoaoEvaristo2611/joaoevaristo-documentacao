# Line 31
**Autor**: JoãoEvaristo

### Indice
- [Introdução](#introducao)
- [Trabalho Realizado](#trabalho-realizado)
    - [Estação 10](#Estaçao_10)
        - [Tags](#Tags_10)	
        - [Grafcet(Automático)](#Grafcets_Estaçao_10(Automatico))
    - [Estação 20](#Estaçao_20)   
        - [Tags](#Tags_20)
        - [Grafcet (Automático)](#Grafcets_Estaçao_20(Automatico))   
    - [Estação 30](#Estaçao_30)
        - [Tags](#Tags_30)
        - [Grafcet(Automático)](#Grafcets_Estaçao_30(Automatico))    
    - [Estação 40](#Estaçao_40)
        - [Tags](#Tags_40)
        - [Grafcet (Automático)](#Grafcets_Estaçao_40(Automatico))  
    - [Estação 50](#Estaçao_50)
        - [Tags](#Tags_50)
        - [Grafcet (Automático)](#Grafcets_Estaçao_50(Automatico))
        - [Fluxogramas](#Fluxogramas)
            - [Fluxograma Estação 50 com rejeições (Inteiro)](#Fluxograma-Estação-50-com-rejeições-Inteiro)
            - [Fluxograma Estação 50 com rejeições(Partes)](#Fluxograma-Estação-50-com-rejeições-Partes)

    

### Introdução
A linha 31 faz parte dos grupo 30. Essa linha e dividida por 5 estações que são **"Transporte"**, **"colocação de corpo"**,**"Prensa"**, **"Colocação de miolo"** e **"Tapete de verificação de peças"**. 

### Trabalho Realizado:
<br /><br />

#### Estação 10
<br /><br />
Nesta estação a programação foi a mais longa porque tivemos que interligar lhe com as das outras estações. Esta estação tem 2 fins de curso um tapete com um servo motor 5 sensores e 1 cilindro. A  primeira parte da programação foi mandar o carro para a posição HOME que e a posição 0 que e onde a estação 20 esta, a estação 10  fica a espera que a 20 acabe o seu trabalho e quando o sensor base detetar os cilindros do carro iram para frente e a garra ira fechar e depois levantar para logo de seguida voltar a posição inicial, Logo a seguir o carro ira para a posição da estação30 que e 287.2048mm o carro ira levantar e depois os cilindros vão avançar e depois a garra vai abrir e vai esperar ate a estação 30 confirmar que acabou de fazer tudo e quando a 10 receber essa informação ira buscar a peça e ira mover se para a estação 40 na posiçao 776..1536 e vai meter a peça e esperar que esse faça esse trabalho e de seguida vai apanhar  a peça e entregar-lhe a 50 na posiçao 1051.882 e depois disso vai voltar a posição home e vai fazer tudo de novo.
<br /><br />

![Estação10](./lines/line31/2020_2021/Software/Imagens/PLC10.jpg)
<br /><br />

##### Tags 10
<br />

| Tags                      | Inputs        | comments                      | Tags            | Outputs| Comments                     |
| --------------------------|---------------| ------------------------------|-----------------|--------|------------------------------|
| Axis_1_Homing_switch      | %I0.0         | Fim de curso tras             | Axis_1_Pulse    | %Q0.0  |                              |
| Axis_1_HighHw_LimitSwitch | %I0.1         | Fim de Curso(Frente)          | Axis_1_Direction| %Q0.1  |                              |
| Axis_1_LowHw_LimitSwitch  | %I0.2         | Sensor de Frente              | 3110Y10         | %Q0.3  | Cilindro Vertical            |
| 3121010B10                | %I0.3         | Sensor de Movimento(Baixo)    | 3110Y10         | %Q0.4  | Cilindro Rotacional(Esquerda)|
| 311010B11                 | %I0.4         | Sensor de Movimento(Cima)     | 3110Y20A        | %Q0.5  | Cilindro Rotacional(Direita))|
| 311020B20                 | %I0.5         | Sensor de Rotacao(Esquerda)   | 3110Y20B        | %Q0.6  | Cilindro Horizontal          |
| 311020B21                 | %I0.6         | Sensor de Posicao(Direita)    | 3110Y30         | %Q0.7  | Fechar Garra                 |
| 311030B10                 | %I0.7         | Sensor de Pos.Av              | 3110GA          | %Q1.0  | Abrir Garra                  |
| 311030B11                 | %I1.0         | Sensor de Pos.Rec             | 3110GB          | %Q8.5  | Luz Laranja                  |
| 3110G10                   | %I1.1         | Sensor de Garra               | 31192011        | %Q8.6  | Luz Verde                    |
| 311920SB2                 | %I8.4         | STOP                          | 31192012        | %Q8.7  | Luz Encarnada                |
| 311920SB1                 | %I8.5         | START                         |                 |        |                              |
| 311920QS                  | %I8.6         | Botao de emergencia           |                 |        |                              |
| 311920SA                  | %I8.7         | Seletor                       |                 |        |                              |
<br /><br />

##### Grafcets Estação 10 (Automatico)
<br /><br />

![](./lines/line31/2020_2021/Software/Grafecet/PLC19.svg)

<br /><br />

#### Estação 20
<br /><br />
Na estação 20 a primeira tarefa a ser feita foi a identificação de sensores e cilindros. Esta estação tem cerca de 8 sensores e 2 cilindros. A tarefa seguinte foi a realização do grafcet. O objetivo do grafcet era quando um dos sensores que esta no copo detetar uma peça o cilindro de cima vai a frente para prender as peças de chegar a base enquanto o cilindro de baixo vai a frente até ao sensor da base detetar o objeto e voltava a estaca inicial enquanto a estação 10 o vai buscar a peça e o sensor deixa-se de dar sinal. Logo a seguir á realização do grafcet   foi a programação do próprio que foi em leader no TIA PORTAL (totally integrated automation portal).

![Estação 20](./lines/line31/2020_2021/Software/Imagens/PLC20.jpg)
<br /><br />

##### Tags 20
<br /><br />

| Tags      | Inputs | comments                    | Tags     | Outputs| Comments           |
| -----     |--------| ----------------------------|----------|--------|--------------------|
| 3130B21   | %I0.0  | Sensor de frente            | 3120Y20  | %Q0.0  | Cilindro Superior  |
| 3120B22   | %I0.1  | Sensor de Trás              | 3120Y10  | %Q0.1  | Cilindro Inferior  |
| 3120B11   | %I0.2  | Sensor de Frente            | 292011   | %Q0.7  | Luz Laranja        |
| 3120B12   | %I0.3  | Sensor de Trás              | 292012   | %Q1.0  | Luz Verde          |
| 3120B40   | %I0.4  | Sensor Base                 | 292013   | %Q1.1  | Luz Encarnada      |
| 3120B31   | %I0.5  | Sensor de Cima(Tubo)        |          |        |                    |
| 3120B32   | %I0.6  | Sensor de Baixo(Tubo)       |          |        |                    |
| 3120B33   | %I0.7  | Sensor Metálico(Tubo)       |          |        |                    |
| 3129SB2   | %I1.2  | Stop                        |          |        |                    |
| 3129QS    | %I1.3  | Start                       |          |        |                    |
| 311920SA  | %I1.4  | Switch de Emergência        |          |        |                    |
| 3120SA    | %I1.5  |   Seletor                   |          |        |                    |
<br /><br />

##### Grafcets Estação 20 (Automatico)
<br /><br />

![](./lines/line31/2020_2021/Software/Grafecet/PLC29.svg)
<br /><br />

#### Estação 30
<br /><br />
Na estação 30 fizemos as mesmas tarefas da anterior a identificação, a realização do grafcet e a programação do próprio.  Esta estação tem 6 sensores 1 cilindro e uma prensa. O objetivo do grafcet era quando o sensor detetava uma peça tinha que esperar até que a estação 10 coloca-se a peça onde devia, logo a seguir o copo onde foi colocada a peça ira fechar e o cilindro ira para tras. Quando o cilindro estiver atras o sensor que esta nesse cilindro ira ativar e mandar a informação que o cilindro esta na posição desejada logo a seguir a prensa ira fazer a função dela a o cilindro ira para a frente e o copo ira abrir e vai ficar a espera que a estação 10 o vá buscar
<br /><br />

![Estação 30](./Software/Imagens/PLC30.jpg)
<br /><br />

##### Tags 30
<br /><br />


| Tags      | Input  | comments                    | Tags     | Outputs| Comments              |
| -----     |--------| ----------------------------|----------|--------|-----------------------|
| 3130B21   | %I0.0  | Sensor Garra                | 3130Y20  | %Q0.0  | Garra                 |
| 3130B22   | %I0.1  | Sensor Garra Fechada        | 3130Y10  | %Q0.2  | Base                  |
| 3130B11   | %I0.2  | Sensor de Trás (Base)       | 3130Y30  | %Q0.3  | Prensa                |
| 3130B12   | %I0.3  | Sensor de Frente(Base)      | 392011   | %Q0.7  | Luz Laranja           |
| 3130B31   | %I0.4  | Sensor de Pos.Rec(Prensa)   | 392012   | %Q1.0  | Luz Verde Garra       |
| 3130B32   | %I0.5  | Sensor de Pos.Av(Prensa)    | 392013   | %Q1.1  | Luz Encarnada Garra   |
| 3139SB2   | %I1.2  | Stop                        |          |        |                       |
| 3139SB1   | %I1.3  | Start                       |          |        |                       |
| 3139QS    | %I1.4  | Switch de Emergência        |          |        |                       |
| 3139SA    | %I1.5  | Switch ON/OFF               |          |        |                       |
<br /><br />

##### Grafcets Estação 30 (Automatico)
<br /><br />

![](./lines/line31/2020_2021/Software/Grafecet/PLC39.svg)
<br /><br />

#### Estação 40
<br /><br />
Na estação 40 os objetivos eram o mesmo. Esta estação tem cerca de 16 sensores 6 cilindros. Na parte da programação já foi complexo porque tivemos que fazer 2 grafcets diferentes. O primeiro grafcet que fizemos foi para o copo ir metendo uma peça de cada vez no prato e esperar que o próprio rode, já no segundo grafcet tivemos que programar a garra para apanhar a peça que estava no prato que tinha rodado e que a leve até a peça que esta a espera na base. No primeiro grafcet o sensor do copo tem que detetar para o cilindro de cima va para a frente para impedir que mais peças descam e que o sensor de baixo volte para tras fazendo com que a peça va para o prato e quando o sensor esquerdo do prato deteta-se a peça ira rodar e quando isto aconter o cilindro de baixo vai avançar e o de cima recuar e repetindo todo o processo novamente.
Já no segundo grafcet quando recebesse a informação que o sensor da direita do prato e da base deteta-se os cilindro verticais da garra iram  descer e fechar quando chegar ao final depois disso ira voltar a cima, depois os cilindros horizontais iram avançar e logo a seguir os cilindros verticais iram voltar a repetir o processor anterior mas enves de fechar a garra ira abrir metendo assim o miolo no corpo.
<br /><br />

![Estação 40](./lines/line31/2020_2021/Software/Imagens/PLC40.jpg)
<br /><br />

##### Tags 40
<br /><br />

| Tags      | Input  | comments                    | Tags       | Outputs| Comments              |
| -----     |--------| ----------------------------|------------|--------|-----------------------|
| 314020B11 | %I0.0  | Sensor Tubo em cima         | 314020Y10  | %Q0.0  | Cilindro Baixo do Tubo|
| 314020B10 | %I0.1  | Sensor Tubo em baixo        | 314020Y20  | %Q0.1  | Cilindro Cima do Tubo |
| 314010B31 | %I0.2  | Sensor Prato lado Esq.      | 314010R10  | %Q0.2  | Prato                 |
| 314010B30 | %I0.3  | Sensor Prato lado Dir.      | 314030G10  | %Q0.3  | Garra                 |
| 314010B10 | %I0.4  | Sensor Tubo                 | 314030Y20  | %Q0.4  | Cilindro Vertical     |
| 314020B21 | %I0.5  | Sensor á Frente             | 314030Y10  | %Q0.5  | Cilindro Horinzontal  |
| 314020B20 | %I0.6  |Sensor a trás                | 314040HL10 | %Q0.6  | Semáforo Encarnado    |
| 314020B30 | %I0.7  | Sensor á Frente             | 314040HL20 | %Q0.7  | Semáforo Laranja      |
| 314020B31 | %I1.0  | Sendor a trás               | 314040HL30 | %Q1.0  | Semáforo Verde        |
| 314010B20 | %I1.1  | Sensor posição inicial      | 4920HL1    | %Q8.5  | Luz Laranja           |
| 314030B21 | %I1.2  | Sensor Mov.(Prato)          | 4920HL2    | %Q6.6  | Luz Verde             |
| 314030B10 | %I1.3  | Sensor Garra                | 4920HL3    | %Q8.7  | Luz Encarnada         |
| 314930B41 | %I1.4  | Sensor de Garra em baixo    |            |        |                       |
| 314030B40 | %I1.5  | Sensor de garra em ciima    |            |        |                       |
| 314030B51 | %I8.0  | Sensor de Trás              |            |        |                       |
| 314030B50 | %I8.1  | Sensor de Frente            |            |        |                       |
| 3149SB2   | %I8.2  | Stop                        |            |        |                       |
| 3149SB1   | %I8.3  | Start                       |            |        |                       |
| 3149QS    | %I8.4  | Switch de Emerg.            |            |        |                       |
| 3149SA    | %I8.5  | Switch ON/OFF               |            |        |                       |
<br /><br />

##### Grafcets Estação 40 (Automatico)
<br /><br />

![](./lines/line31/2020_2021/Software/Grafecet/PLC49.svg)

<br /><br />

#### Estação 50
<br /><br />

Nesta estação tivemos que fazer o que fizemos nos outros, mas não só . Tambem tivemos que fazer programação estruturada que é uma programação textual de alto nível, possibilita a solução de problemas mais complexos. A programação foi feita para quando o sensor detetar e o plc  50 receber a informação que a estação 10 o tapete vai começar a andar para a frente enquanto ele tiver a andar vai passar por 2 sensores 1 que é metálico e outro que deteta peças brancas.  Se os dois sensores detetarem significa que e uma peça de metal por isso o primeiro cilindro ira avançar quando a peça esta la. Se so um detetar quer dizer que e uma peça branca por isso o segundo cilindro ira para a frente e se nenhum detetar significa que e preta por isso so o terceiro cilindro ira para a frente. Para detetar as peças com erros teve que se fazer programação estruturada que é uma programação textual de alto nível, possibilita a solução de problemas mais complexos. Para fazer isto tivemos que tirar medidas para sabermos quantos centímetros a peça demora ate chegar o corpo aos 2 sensores e depois tivemos que medir quantos centímetros a peça anda ate o miolo detetar nos dois sensores 
<br /><br />

![Estação50](./lines/line31/2020_2021/Software/Imagens/PLC50.jpg)
<br /><br />

##### Tags 50
<br /><br />

| Tags      | Input  | comments         | Tags    | Outputs| Comments          |
| -----     |--------| -----------------|---------|--------|-------------------|
|           |I0.0	 |Encoder(Fase A)   |TP	      |Q0.0    |Motor (Rotação Av) |
|           |I0.1	 |Encoder(Fase B)   |TP(1)    |	Q0.1   |Motor (Rotação Rec)|
|           |I0.2    |Encoder(Fase C)   |3150Y20  |	Q0.4   |Cilindro 1         |
|3150B11	|I0.3	 |Sensor de Material|3150Y30  |	Q0.5   |Cilindro 2         |
|3150B12	|I0.4    |Sensor de Metálico|3150Y40  |	Q0.6   |Cilindro 3         |
|3150B13	|I0.5    |Sensor de Ótico   |592011   |	Q0.7   |Luz Amarela        |
|3150B21	|I0.7    |Sensor(Cilindro 1)|592012   |	Q1.0   |Luz Verde          |
|3150B31	|I1.0    |Sensor(Cilindro 2)|592013   |	Q1.1   |Luz Vermelha       |
|3150B41	|I1.1    |Sensor(Cilindro 3)|				
|3159SB2	|I1.2    |Stop              |				
|3159SB1	|I1.3    |Start             |				
|3159QS	    |I1.4    |Switch de Emerg.  |				
|3159SA	    |I1.5    |Switch ON/OFF     |				
<br /><br />

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
