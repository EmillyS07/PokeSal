# Análise Estática de Requisitos (Teste Estático)
Relatório de Inspeção/Revisão dos requisitos, identificando ambiguidades, omissões ou contradições antes da codificação.

## 1. Seleção do Inicial

| **ID** | **Requisito** | **Problema identificado** | **Classificação** | **Impacto / Necessidade de esclarecimento** | **Esclarecimento** |
|---|---|---|---|---|---|
| SI-01 | O treinador deve escolher apenas 1 Pokésal inicial entre as opções permitidas. | Não está definido o que acontece caso o treinador tente escolher mais de um Pokésal. | Omissão | É necessário determinar se o sistema deve impedir a seleção adicional ou apresentar uma mensagem de erro. | O treinador poderá selecionar apenas 1 Pokésal. Após a seleção, o sistema deve impedir a escolha de outro Pokésal. |
| SI-02 | As opções permitidas são BulbaSal, CharSal, SquirtSal, ChikoSal, CyndaSal e TotoSal. | Não está especificado se todos os Pokésais possuem disponibilidade obrigatória para seleção em qualquer batalha. | Ambiguidade | É necessário esclarecer se todas as seis opções estarão sempre disponíveis ou se alguma condição pode limitar as escolhas. | Os seis Pokésais estarão disponíveis para seleção no início de todas as batalhas. |
| SI-03 | Cada Pokésal possui os atributos base HP, ATK, DEF e SPD. | Não foram definidos os valores dos atributos de cada Pokésal. | Omissão | É necessário especificar os valores de HP, ATK, DEF e SPD para que os atributos possam ser utilizados nos cálculos e testes da batalha. | Os valores base são: BulbaSal: HP 200, ATK 55, DEF 65, SPD 45; CharSal: HP 200, ATK 75, DEF 45, SPD 70; SquirtSal: HP 200, ATK 50, DEF 75, SPD 40; ChikoSal: HP 200, ATK 60, DEF 60, SPD 65; CyndaSal: HP 200, ATK 65, DEF 40, SPD 80; TotoSal: HP 200, ATK 60, DEF 55, SPD 55. |
| SI-04 | Cada Pokésal possui seu TipoElemental. | Não está especificado qual TipoElemental pertence a cada Pokésal. | Omissão | É necessário associar cada Pokésal a um dos tipos elementais disponíveis para que as regras de vantagem e desvantagem possam ser aplicadas. | BulbaSal e ChikoSal são do tipo Planta; CharSal e CyndaSal são do tipo Fogo; SquirtSal e TotoSal são do tipo Água. |

---

## 2. Matriz de Vantagens e Desvantagens Elementais

| **ID** | **Requisito** | **Problema identificado** | **Classificação** | **Impacto / Necessidade de esclarecimento** | **Esclarecimento** |
|---|---|---|---|---|---|
| ME-01 | Apenas os tipos Fogo, Água e Planta estão presentes. | Não está definido o comportamento quando um golpe é utilizado contra um Pokésal do mesmo tipo. | Omissão | É necessário determinar qual multiplicador de dano deve ser aplicado quando atacante e defensor possuem o mesmo tipo. | Quando o golpe for utilizado contra um Pokésal do mesmo tipo, será aplicado o multiplicador neutro de 1,0x. |
| ME-02 | Fogo é super efetivo contra Planta (dano x2.0) e pouco efetivo contra Água (dano x0.5). | Não está definido se os multiplicadores são aplicados diretamente sobre o dano base ou em alguma outra etapa do cálculo. | Ambiguidade | É necessário especificar a fórmula e a ordem de aplicação dos multiplicadores para evitar resultados diferentes na implementação. | O multiplicador elemental será aplicado após o cálculo baseado em Dano Base, ATK e DEF, após o bônus de Vantagem de Velocidade e após o efeito de Terreno, quando aplicáveis. |
| ME-03 | Água é super efetiva contra Fogo (dano x2.0) e pouco efetiva contra Planta (dano x0.5). | Não está definido o comportamento do dano de Água contra um Pokésal do tipo Água. | Omissão | É necessário definir o multiplicador aplicado em confrontos entre Pokésais do mesmo tipo. | Golpes de Água contra Pokésais do tipo Água possuem multiplicador neutro de 1,0x. |
| ME-04 | Planta é super efetiva contra Água (dano x2.0) e pouco efetiva contra Fogo (dano x0.5). | Não está definido o comportamento do dano de Planta contra um Pokésal do tipo Planta. | Omissão | É necessário definir o multiplicador aplicado em confrontos entre Pokésais do mesmo tipo. | Golpes de Planta contra Pokésais do tipo Planta possuem multiplicador neutro de 1,0x. |
| ME-05 | É necessário definir o multiplicador aplicado em confrontos entre Pokésais do mesmo tipo. | Não está explicitamente definido se todos os golpes possuem o mesmo TipoElemental do Pokésal que os utiliza ou se um Pokésal pode utilizar golpes de tipos diferentes. | Ambiguidade | É necessário esclarecer a relação entre o tipo do Pokésal e o tipo do golpe para determinar corretamente o multiplicador de dano. | Os três golpes de cada Pokésal possuem o mesmo TipoElemental do Pokésal que os utiliza. |
| ME-06 | Fogo, Água e Planta possuem multiplicadores de vantagem e desvantagem. | Não está definido se existe algum outro multiplicador ou regra quando não há vantagem ou desvantagem elemental. | Omissão | É necessário definir o multiplicador aplicado em situações neutras para que todos os possíveis confrontos tenham um resultado determinado. | Em situações sem vantagem ou desvantagem elemental, será aplicado o multiplicador neutro de 1,0x. |

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

| **ID** | **Requisito** | **Problema identificado** | **Classificação** | **Impacto / Necessidade de esclarecimento** | **Esclarecimento** | 
|---|---|---|---|---|---|
| REQ-01 | A ordem de ataque do turno é determinada estritamente pelo atributo SPD. | Não está definido o que acontecerá quando os Pokésais possuírem o mesmo valor de SPD. | Omissão | É necessário definir um critério de desempate para determinar quem irá atacar primeiro. | A ordem de ataque será definida pelos seguintes critérios, nesta sequência: SPD, ATK e DEF. |
| REQ-02 | Paralisado: reduz SPD. | Não está definido quanto da SPD deve ser reduzido. | Omissão | É necessário definir o valor ou percentual da redução. | A Paralisia reduz a SPD em 10%. |
| REQ-03 | Queimado: reduz HP e ATK. | Não estão definidos os valores ou percentuais das reduções de HP e ATK. | Omissão | É necessário definir o valor ou percentual da redução. | A Queimadura reduz o HP atual e o ATK em 10%. |
| REQ-04 | Envenenado: causa dano progressivo. | Não está definido quanto dano é causado nem como o dano progride. | Omissão | É necessário definir o valor do dano e como será a progressão. | O dano é calculado sobre o ATK do Pokésal de Planta que aplicou o status: 2% no primeiro turno, 4% no segundo e 6% no terceiro. |
| REQ-05 | Aplicação de efeitos de status no final do turno. | Não está especificado por quantos turnos cada efeito permanecerá ativo. | Omissão | É necessário estabelecer a duração dos efeitos. | Os efeitos de status permanecem ativos por 3 turnos. |
| REQ-06 | Aplicação dos efeitos de status no final do turno. | Não está definida a ordem de aplicação entre os efeitos de status e os efeitos de terreno que ocorrem no final do turno. | Ambiguidade       | É necessário definir a ordem, pois isso pode resultar em diferentes comportamentos durante a batalha. | Primeiro são aplicados os efeitos do terreno e, depois, os efeitos de status. |
| REQ-07 | Efeitos de Status. | Não está definido se um Pokésal pode possuir mais de um efeito de status simultaneamente. | Omissão | É necessário determinar se os efeitos podem ser acumulados ou se um novo status substitui o anterior. | Caso receba um novo efeito, este substituirá o status anterior. |
| REQ-08 | Efeitos de Status. | Não está definido como os efeitos de status são aplicados aos Pokésais. | Omissão | É necessário definir quais golpes podem aplicar cada efeito de status e em quais condições. | Pokésal de Fogo aplica Queimadura; Pokésal de Água aplica Paralisia; Pokésal de Planta aplica Envenenamento. |

---

### 5. Gerenciamento de Mochila (Itens de Batalha)

| **ID** | **Requisito** | **Problema identificado** | **Classificação** | **Impacto / Necessidade de esclarecimento** | **Esclarecimento** |
|---|---|---|---|---|---|
| REQ-01 | Cada treinador pode usar no máximo 2 itens por batalha. | Não está definido se os dois usos permitidos podem ser do mesmo tipo de item ou se devem ser de tipos diferentes. | Ambiguidade | É necessário definir se um treinador pode utilizar o mesmo item duas vezes na batalha ou se deve utilizar dois itens diferentes. | Podem ser do mesmo tipo, desde que o treinador não ultrapasse o limite de dois usos por batalha. |
| REQ-02 | Cada treinador pode usar no máximo 2 itens por batalha. | Não está definido como e quando os itens serão disponibilizados ao jogador. | Omissão | É necessário definir se os itens serão escolhidos pelo treinador antes do início da batalha, disponibilizados aleatoriamente antes ou durante a batalha, ou escolhidos durante a batalha. | Os 2 itens de cada treinador são sorteados antes do início da batalha. |
| REQ-03 | Exemplos: Potion, Super Potion e Antidote. | Os efeitos dos itens não foram definidos. | Omissão | É necessário especificar o efeito de cada item. | A Potion recupera 20 HP, a Super Potion recupera 40 HP e o Antidote remove o efeito de Envenenamento. |
| REQ-04 | Usar um item consome o turno do treinador. | Não está definido se o item é aplicado antes ou depois da ação do oponente no fluxo do turno. | Ambiguidade | É necessário determinar o momento exato do uso do item. | O efeito do item é aplicado instantaneamente no momento em que o treinador o utiliza. |


