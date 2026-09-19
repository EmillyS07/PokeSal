# Análise Estática de Requisitos (Teste Estático)
Relatório de Inspeção/Revisão dos requisitos, identificando ambiguidades, omissões ou contradições antes da codificação.

## 1. Seleção do Inicial

| **ID** | **Requisito** | **Problema identificado** | **Classificação** | **Impacto / Necessidade de esclarecimento** |
|---|---|---|---|---|
| SI-01 | O treinador deve escolher apenas 1 Pokésal inicial entre as opções permitidas. | Não está definido o que acontece caso o treinador tente escolher mais de um Pokésal. | Omissão | É necessário determinar se o sistema deve impedir a seleção adicional ou apresentar uma mensagem de erro. |
| SI-02 | As opções permitidas são BulbaSal, CharSal, SquirtSal, ChikoSal, CyndaSal e TotoSal. | Não está especificado se todos os Pokésais possuem disponibilidade obrigatória para seleção em qualquer batalha. | Ambiguidade | É necessário esclarecer se todas as seis opções estarão sempre disponíveis ou se alguma condição pode limitar as escolhas. |
| SI-03 | Cada Pokésal possui os atributos base HP, ATK, DEF e SPD. | Não foram definidos os valores dos atributos de cada Pokésal. | Omissão | É necessário especificar os valores de HP, ATK, DEF e SPD para que os atributos possam ser utilizados nos cálculos e testes da batalha. |
| SI-04 | Cada Pokésal possui seu TipoElemental. | Não está especificado qual TipoElemental pertence a cada Pokésal. | Omissão | É necessário associar cada Pokésal a um dos tipos elementais disponíveis para que as regras de vantagem e desvantagem possam ser aplicadas. |

---

## 2. Matriz de Vantagens e Desvantagens Elementais

| **ID** | **Requisito** | **Problema identificado** | **Classificação** | **Impacto / Necessidade de esclarecimento** |
|---|---|---|---|---|
| ME-01 | Apenas os tipos Fogo, Água e Planta estão presentes. | Não está definido o comportamento quando um golpe é utilizado contra um Pokésal do mesmo tipo. | Omissão | É necessário determinar qual multiplicador de dano deve ser aplicado quando atacante e defensor possuem o mesmo tipo. |
| ME-02 | Fogo é super efetivo contra Planta (dano x2.0) e pouco efetivo contra Água (dano x0.5). | Não está definido se os multiplicadores são aplicados diretamente sobre o dano base ou em alguma outra etapa do cálculo. | Ambiguidade | É necessário especificar a fórmula e a ordem de aplicação dos multiplicadores para evitar resultados diferentes na implementação. |
| ME-03 | Água é super efetiva contra Fogo (dano x2.0) e pouco efetiva contra Planta (dano x0.5). | Não está definido o comportamento do dano de Água contra um Pokésal do tipo Água. | Omissão | É necessário definir o multiplicador aplicado em confrontos entre Pokésais do mesmo tipo. |
| ME-04 | Planta é super efetiva contra Água (dano x2.0) e pouco efetiva contra Fogo (dano x0.5). | Não está definido o comportamento do dano de Planta contra um Pokésal do tipo Planta. | Omissão | É necessário definir o multiplicador aplicado em confrontos entre Pokésais do mesmo tipo. |
| ME-05 | É necessário definir o multiplicador aplicado em confrontos entre Pokésais do mesmo tipo. | Não está explicitamente definido se todos os golpes possuem o mesmo TipoElemental do Pokésal que os utiliza ou se um Pokésal pode utilizar golpes de tipos diferentes. | Ambiguidade | É necessário esclarecer a relação entre o tipo do Pokésal e o tipo do golpe para determinar corretamente o multiplicador de dano. |
| ME-06 | Fogo, Água e Planta possuem multiplicadores de vantagem e desvantagem. | Não está definido se existe algum outro multiplicador ou regra quando não há vantagem ou desvantagem elemental. | Omissão | É necessário definir o multiplicador aplicado em situações neutras para que todos os possíveis confrontos tenham um resultado determinado. |

---

### 3. Mecânica do Estacionamento da UCSal (Efeito de Terreno)

| **ID** | **Requisito** | **Problema identificado** | **Classificação** | **Impacto / Necessidade de esclarecimento** | **Esclarecimento** |
|---|---|---|---|---|---|
| REQ-01 | Efeitos de terreno | Não está definido como o terreno é selecionado no início da batalha. | Omissão | É necessário definir se o terreno é escolhido pelo jogador, sorteado ou previamente determinado. | O terreno é sorteado aleatoriamente no início da batalha. |
| REQ-02 | Efeitos de terreno | Não está definido se o terreno pode mudar durante a batalha. | Omissão | É necessário determinar se existe apenas um terreno por batalha ou se o terreno pode mudar durante a batalha. | Cada batalha possui apenas um terreno. |
| REQ-03 | Efeitos de terreno | Não está definida a ordem de aplicação dos efeitos de terreno e dos multiplicadores de vantagem/desvantagem elemental. | Ambiguidade | É necessário informar, pois a ausência dessa informação pode gerar resultados diferentes para o cálculo do dano final. | Primeiro é aplicado o efeito do terreno e, depois, o multiplicador de vantagem/desvantagem elemental. |
| REQ-04 | Asfalto Quente (Dia): aumenta o dano de golpes do tipo Fogo em 15% | Não é informado como o bônus de 15% deve ser calculado. | Ambiguidade | É necessário definir em qual etapa o bônus de terreno é aplicado, se será em relação ao dano base do golpe ou após a aplicação dos multiplicadores de vantagem/desvantagem elemental. | É aplicado sobre o dano base do golpe, antes da aplicação do multiplicador elemental. |
| REQ-05 | Poça de Chuva / Piso Escorregadio: golpes de Água aplicam 10% adicionais de precisão ou dano | O requisito apresenta duas possibilidades diferentes. | Ambiguidade | É necessário definir qual atributo receberá o bônus de 10%. | Recebem 10% de bônus no dano. |
| REQ-06 | Poça de Chuva / Piso Escorregadio | Não está definido como funciona o bônus de precisão caso essa opção seja escolhida. | Omissão | É necessário definir como a precisão será calculada e aplicada. | Não se aplica. |
| REQ-07 | Canteiro Central: Pokésal do tipo Planta recupera 5% do HP máximo ao final de cada turno | Não está especificado se a recuperação pode ultrapassar o HP máximo. | Omissão | É necessário definir um limite para a recuperação de HP. | Não pode ultrapassar 200 HP, que é o HP máximo de um Pokésal. |
| REQ-08 | Canteiro Central: Pokésal do tipo Planta recupera 5% do HP máximo ao final de cada turno | Não está definido se um Pokésal do tipo Planta derrotado durante o turno pode receber a recuperação de HP do terreno. | Omissão | É necessário definir se o efeito de recuperação é aplicado somente a Pokésais com HP maior que 0 ou também a Pokésais que tenham chegado a 0 HP durante o turno. | O Pokésal que chegar a 0 HP é derrotado imediatamente e não recebe nenhum bônus. |

---

### 4. Sistema de Batalha por Turnos e Iniciativa

| **ID** | **Requisito** | **Problema identificado** | **Classificação** | **Impacto / Necessidade de esclarecimento** |
|---|---|---|---|---|
| REQ-01 | Efeitos de terreno | Não está definido como o terreno é selecionado no início da batalha. | Omissão | É necessário definir se o terreno é escolhido pelo jogador, sorteado ou previamente determinado. |
| REQ-02 | Efeitos de terreno | Não está definido se o terreno pode mudar durante a batalha. | Omissão | É necessário determinar se existe apenas um terreno por batalha ou se o terreno pode mudar durante a batalha. |
| REQ-03 | Efeitos de terreno | Não está definida a ordem de aplicação dos efeitos de terreno e dos multiplicadores de vantagem/desvantagem elemental. | Ambiguidade | É necessário informar, pois a ausência dessa informação pode gerar resultados diferentes para o cálculo do dano final. |
| REQ-04 | Asfalto Quente (Dia): aumenta o dano de golpes do tipo Fogo em 15% | Não é informado como o bônus de 15% deve ser calculado. | Ambiguidade | É necessário definir em qual etapa o bônus de terreno é aplicado, se será em relação ao dano base do golpe ou após a aplicação dos multiplicadores de vantagem/desvantagem elemental. |
| REQ-05 | Asfalto Quente (Dia) | Não está definido como o sistema determina que é “Dia”. | Omissão | É necessário definir se o período é informado pelo jogador, sorteado ou determinado por algum mecanismo de tempo durante a batalha. |
| REQ-06 | Poça de Chuva / Piso Escorregadio: golpes de Água aplicam 10% adicionais de precisão ou dano | O requisito apresenta duas possibilidades diferentes. | Ambiguidade | É necessário definir qual atributo receberá o bônus de 10%. |
| REQ-07 | Poça de Chuva / Piso Escorregadio | Não está definido como funciona o bônus de precisão caso essa opção seja escolhida. | Omissão | É necessário definir como a precisão será calculada e aplicada. |
| REQ-08 | Canteiro Central: Pokésal do tipo Planta recupera 5% do HP máximo ao final de cada turno | Não está especificado se a recuperação pode ultrapassar o HP máximo. | Omissão | É necessário definir um limite para a recuperação de HP. |
| REQ-09 | Canteiro Central: Pokésal do tipo Planta recupera 5% do HP máximo ao final de cada turno | Não está definido se um Pokésal do tipo Planta derrotado durante o turno pode receber a recuperação de HP do terreno. | Omissão | É necessário definir se o efeito de recuperação é aplicado somente a Pokésal com HP maior que 0 ou também a Pokésal que tenham chegado a 0 HP durante o turno. |

---

### 5. Gerenciamento de Mochila (Itens de Batalha)

| **ID** | **Requisito analisado** | **Problema identificado** | **Classificação** | **Impacto / Necessidade de esclarecimento** |
|---|---|---|---|---|
| REQ-01 | Cada treinador pode usar no máximo 2 itens por batalha | Não está definido se os dois usos permitidos podem ser do mesmo tipo de item ou se devem ser de tipos diferentes. | Ambiguidade | É necessário definir se um treinador pode utilizar o mesmo item duas vezes na batalha ou se deve utilizar dois itens diferentes. |
| REQ-02 | Cada treinador pode usar no máximo 2 itens por batalha | Não está definido como e quando os itens serão disponibilizados ao jogador. | Omissão | É necessário definir se os itens serão escolhidos pelo treinador antes do início da batalha, disponibilizados aleatoriamente antes ou durante a batalha, ou escolhidos durante a batalha. |
| REQ-03 | Exemplos: Potion, Super Potion e Antidote | Os efeitos dos itens não foram definidos. | Omissão | É necessário especificar o efeito de cada item. |
| REQ-04 | Usar um item consome o turno do treinador | Não está definido se o item é aplicado antes ou depois da ação do oponente no fluxo do turno. | Ambiguidade | É necessário determinar o momento exato do uso do item. |

