# Análise Estática de Requisitos (Teste Estático)
Relatório de Inspeção/Revisão dos requisitos, identificando ambiguidades, omissões ou contradições antes da codificação.


### 3. Mecânica do Estacionamento da UCSal (Efeito de Terreno)

| **ID** | **Requisito** | **Problema identificado** | **Classificação** | **Impacto / Necessidade de esclarecimento** |
|---     |---            |---                        |---                |---                                          |
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

