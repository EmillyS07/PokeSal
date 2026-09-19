# Requisitos Autorais

### 1. Sistema de Pontos de Poder e Golpes

- Cada Pokésal possui uma barra de Pontos de Poder (PP), com máximo de 100 PP, mínimo de 0 PP e iniciando a batalha com 40 PP;
- A quantidade de PP nunca poderá ser inferior a 0 ou superior a 100;
- Cada Pokésal possui 3 golpes: básico, médio e crítico;
- O golpe básico possui um custo de 0 PP;
- O golpe médio possui um custo de 50 PP;
- O golpe crítico possui um custo de 100 PP;
- Um golpe só pode ser utilizado quando o Pokésal possuir PP igual ou superior ao seu custo;
- Ao final de cada turno, o Pokésal recupera 10 PP;
- Ao utilizar um golpe básico, o Pokésal recebe 15 PP;
- Ao utilizar um golpe médio ou um golpe crítico, o Pokésal recebe 5 PP;
- A obtenção dos PP ocorre automaticamente sempre que uma das ações ou situações previstas gerar recuperação de pontos.

### 2. Sistema de Defesa e Cálculo de Dano

- O dano de um golpe deve ser calculado considerando o Dano Base do Golpe, o ATK atual do Pokésal atacante e a DEF atual do Pokésal defensor;
- O cálculo inicial do dano deve seguir a fórmula: **Dano Inicial = Dano Base do Golpe + ATK do Atacante − DEF do Defensor**;
- O cálculo deve utilizar os valores atuais de ATK e DEF no momento da execução do golpe, considerando possíveis alterações causadas por efeitos de status;
- Caso o Dano Inicial seja menor que 1, ele deve ser considerado igual a 1 HP antes da aplicação dos modificadores;
- Após o cálculo do Dano Inicial, deve ser aplicada a Vantagem de Velocidade, quando aplicável;
- Em seguida, deve ser aplicado o modificador de Vantagem ou Desvantagem Elemental, quando aplicável;
- Os modificadores devem ser aplicados sobre o dano resultante da etapa anterior;
- O dano final aplicado ao defensor deve ser um valor inteiro;
- Caso o cálculo resulte em valor decimal, o sistema deve utilizar uma regra de arredondamento consistente;
- O dano aplicado nunca poderá ser menor que 1 HP, desde que o golpe tenha acertado;
- O dano aplicado nunca poderá reduzir o HP do Pokésal para um valor inferior a 0;
- Caso o dano seja maior que o HP atual, o HP deve ser reduzido exatamente para 0;
- Quando o HP de um Pokésal chegar a 0, ele será considerado derrotado e não poderá realizar novas ações.

**Exemplo:**

CharSal possui ATK 75 e utiliza o Golpe Médio, com Dano Base 40, contra SquirtSal, que possui DEF 75.

**Dano Inicial:**

**40 + 75 − 75 = 40**

Como CharSal possui SPD 70 e SquirtSal possui SPD 40, a diferença de velocidade é de 30 pontos. Portanto, CharSal recebe o bônus de Vantagem de Velocidade de 10%.

**40 × 1,10 = 44**

Como CharSal é do tipo Fogo e SquirtSal é do tipo Água, aplica-se o modificador de desvantagem elemental de 0,5.

**44 × 0,5 = 22**

Portanto, o dano final aplicado é **22 HP**.

### 3. Sistema de Vantagem de Velocidade

- A diferença de velocidade entre os Pokésal deve ser calculada pela diferença absoluta entre seus valores de SPD;
- Quando a diferença de SPD entre os Pokésal for igual ou superior a 20 pontos, o Pokésal mais rápido receberá 10% de bônus de dano em seus golpes;
- Quando a diferença de SPD for inferior a 20 pontos, nenhum bônus de dano será aplicado;
- O bônus de velocidade deve ser aplicado somente ao Pokésal que possuir o maior valor de SPD;
- Caso os Pokésal possuam o mesmo SPD, nenhum deles receberá o bônus;
- O bônus de velocidade será aplicado somente após o cálculo do dano baseado em ATK e DEF;
- O bônus de velocidade será aplicado antes dos modificadores de vantagem ou desvantagem elemental;
- O valor de SPD utilizado deve ser o valor atual do Pokésal no momento do ataque;
- Caso algum efeito de status reduza o SPD de um Pokésal, a diferença de velocidade deverá ser recalculada;
- O bônus de velocidade será limitado a 10%.

**Exemplo:**

CyndaSal possui SPD 80.

BulbaSal possui SPD 45.

**Diferença de SPD:**

**80 − 45 = 35**

Como a diferença é superior a 20 pontos, CyndaSal recebe **10% de bônus de dano** em seus golpes.
