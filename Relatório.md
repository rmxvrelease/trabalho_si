<center>

### Universidade de Brasília
#### Instituto de Ciências Exatas
#### Departamento de Ciência da Computação
#### Sistemas de Informação - 2025.2

![UnB](images/unb.png)

# Trabalho Final

### Dupla 14:
#### Júlia Paulo Amorim - 241039270
#### Rafael Monteiro Ximenes de Vasconcelos - 241002402 

</center>

- Link para o repositório do trabalho: [trabalho_si](https://github.com/rmxvrelease/trabalho_si)

# 1. Introdução

> Missão B: Entregar mercadorias/equipamentos
>
> Quando necessário, um robô deve coletar os recursos requisitados no estoque e entregá-los ao agente
solicitante em um local especificado. Na fase de coleta, o robô deve ir aos locais de armazenamento onde
os recursos podem ser encontrados. A ordem a ser seguida é definida pela estimativa do tempo de espera
somado ao caminho que o robô deve percorrer. Assim que o robô chega a um local de armazenamento e
é o momento de solicitar o recurso, o robô envia uma mensagem para o estoque com a especificação
precisa dos recursos solicitados e aguarda até que os recursos sejam coletados. Uma vez coletados,
começa a fase de entrega. Nessa fase, o robô fará o número necessário de viagens para levar todos os
recursos ao local especificado. Se a bateria do robô designado estiver baixa (10%) na fase de coleta, o
robô retornará à estação de recarga e atribuirá a missão a outro robô. Se a bateria do robô designado
estiver baixa (30%) na fase de entrega, o robô deverá retornar o recurso a um ponto de controle e atribuir
a tarefa restante a outro robô, que saberá onde o recurso está posicionado. Em caso de falha ao retornar
o recurso para o ponto de controle, um alerta deve ser acionado e o relatório enviado ao gerente do setor.
Quando múltiplos itens forem necessários de diferentes estoques, múltiplos robôs podem ser designados
para tarefas paralelas de coleta e entrega, a fim de reduzir o tempo para concluir a missão. Exemplos de
mercadorias/equipamentos incluem: (i) equipamentos médicos estéreis, que devem ser transportados
de instalações estéreis para os destinos de uso, e (ii) roupas de cama limpas, que devem ser movidas
periodicamente da lavanderia para os quartos de armazenamento próximos ao local de uso.

### 1.1 - Contexto do Problema
Um grande problema contemporâneo é a logística de transporte materiais, especialmente de items críticos para hospitais como equipamentos médicos estéreis e roupas de cama limpas. A necessidade de eficiência operacional, combinada com requisitos de esterilidade e periodicidade, exige soluções que minimizem interferência humana em processos de entrega.

Neste Contexto, a Missão B surge como um problema de automação logística de um sistema de entregas para um solicitante, onde robôs autônomos devem realizar coleta e entrega de recursos de forma segura, eficiente e confiável. O sistema operaa em um ambiente com múltiplos atores, restrições físicas e condições variáveis.

### 1.2 - Descrição do Problema
O problema consiste em um sistema robótico autônomo para entrega de materiais e equipamentos, caracterizado por:

- Pedido: Um solicitante faz um pedido para um controlador da missão, que inicia o processo alocando robôs
- Coleta: Deslocamento do robô até os locais de armazenamento e destino com rotas baseadas em tempo de espera + distância
- Comunicação: Interação padronizada com mensagens para saber a disponibilidade de estoque e alocação
- Entrega: Transporte até o local de destino com múltiplas viagens quando necessário
- Paralelismo: Coordenação de múltiplos robôs para execução paralela de uma entrega
- Tratamento de erros: Possui mecanismos de falha para pouca bateria dos robôs e recuperação de equipamentos

### 1.3 - Objetivo Principal
O objetivo principal do sistema e da missão é a entrega de mercadorias e equipamentos de forma autônoma, maximizando a eficiência e confiabilidade do transporte, assim melhorando a utilização dos recursos pelo solicitante



# 2. Fundamentação Teórica

### 2.1 Fase 1: Initiation - Compreensão do Contexto e Stakeholders
#### 2.1.1 Context Diagram

Teoria: O diagrama de contexto define os limites do sistema e suas interfaces com entidades externas, estabelecendo claramente o escopo do sistema. Identificando as atividades do mundo real que a máquina precisa melhorar e apoiar.

No Projeto:

    - Sistema Central: Sistema de Entrega com Robôs Autônomos

    - Entidades Externas: Requerentes, Equipe do Armazém, Gerente do Setor

    - Fluxos de Dados: Solicitações, confirmações, notificações e mensagems

#### 2.1.2 Stakeholder Onion Diagram

Teoria: O modelo "cebola" de stakeholders classifica stakeholders por níveis de influência e envolvimento com o projeto. A fim de que seja possível identificar todas as partes interessadas e compreender relacões de influência

No Projeto:

    - Núcleo: Controlador da Missão (influência direta)

    - Anel Interno: Operadores Diretos (envolvimento diário)

    - Anel Médio: Suporte Técnico (suporte operacional)

    - Anel Externo: Impactados e Reguladores (influência indireta)

### 2.2 Fase 2: Investigation - Exploração do Domínio e Objetivos
#### 2.2.1 Domain Scenarios

Teoria: Os domain scenarios fornecem narrativas contextuais de situações operacionais. A fim de que seja possível contextualizar requisitos em situações reais e antecipar casos de exceção

No Projeto:

    - 2 cenários narrativos cobrindo casos normais e de exceção

    - Estrutura padronizada: Atores, Objetos do Mundo, Ações e Passos

    - Foco em situações reais: Caso ideal e bateria baixa

#### 2.2.2 Goal Model

Teoria: Framework KAOS abordagem orientada a objetivos para engenharia de requisitos. Permite que os objetivos de um projeto sejam organizados e estruturados de forma hierárquica, identificando requisitos como refinamentos de goals

Componentes aplicados:

    - Goals: Estados desejados do sistema (Achieve, Maintain, Avoid)

    - Agents: Entidades responsáveis por atingir goals

    - Refinements: Relações AND/OR entre goals

    - Responsibility assignments: Atribuição de goals a agents

### 2.3 Fase 3: Decision - Priorização e Impacto
#### 2.3.1 Impact Maps

Teoria: Metodologia de Impact Mapping para alinhamento estratégico, traduzindo goals em ações concretas e priorizando o desenvolvimento baseado em impacto. Com o objetivo de garantir o alinhamento entre o desenvolvimento e os objetivos

Estrutura:

Why? (Goal) → Who? (Actor) → How? (Impact) → What? (Deliverable)

No Projeto:

    - 2 Impact Maps goals selecionados

    - Foco em deliverables implementáveis

    - Conexão explícita entre features e objetivos de negócio

### 2.4 Fase 4: Formulation - Especificação Detalhada
### 2.4.1 Specification by Example com Example Maps

Teoria: Os BDDs e os Example Maps usam estruturas Given-When-Then para especificar comportamentos, além do Example Mapping ser uma técnica que explora as regras de negócio. A fim de eliminar ambiguidades através de exemplos concretos e facilitar o entendimento do sistema

No Projeto:

    - User stories para features

    - Tabelas de exemplos para regras

    - BDDs para comportamentos específicos

# 3. Modelagens
## Fase 1: Initiation
- ### Context Diagram

A imagem consiste em um "Context Diagram" no qual se descreve o trabalho (Work) que o sistema de entregas robótico deve realizar. Vale notar que o diagrama não especifica de que forma o trabalho deve ser executado nem o funcionamento
interno do serviço, ele apenas descreve as manifestações externas e os efeitos provenientes da sua realização sobre os atores diretamente afetados por ele.

Assim, o diagrama em questão poderia representar o serviço de entregas tanto antes da sua automação por meio de robôs 
(The World-as-is) quanto depois dela (The World-to-be). Essa é uma característica típica do que se convencionou denominar "project-level context diagram" ou "diagrama de contexto a nível de projeto", em tradução livre.

![context diagram](context_diagram/context_diagram.jpg)

- ### Stakeholder Onion Diagram
O Stakeholder Onion Diagram foi elaborado para visualizar claramente os diferentes níveis de envolvimento, influência e impacto das diversas partes no sistema, permitindo identificar os principais atores do sistema, garantir que todas perspectivas sejam consideradas e compreender as necessidades e expectativas

- Camadas:
    1. Núcleo:
        - Controlador da Missão
    2. Anel Interno: Operadores diretos
        - Equipe Operacional
        - Solicitantes (Equipe Médica)
        - Equipe do Armazém
    3. Anel Médio: Suporte e Infraestrutura
        - Fornecedores técnicos
        - Desenvolvedores
        - Gerente do setor
    4. Anel Externo: Impactados e Reguladores
        - Pacientes
        - Visitantes do Hospital
        - Funcionários do Hospital
        - Comunidade

![stakeholder onion](stakeholder_onion/stakeholder_onion.png)

## Fase 2: Investigation
- ### Domain Scenarios
Cenário 1: Entrega Normal de Item Médico

- Actors:
    - Solicitante
    - Sistema de Controle de Missões
    - Robô
    - Equipe do Armazém

- World Objects:
    - Item médico
    - Estoque
    - Armazém
    - Destino

- Actions and Steps:
    1. Solicitante solicita o equipamento através do sistema
    2. Sistema de Controle recebe a solicitação e verifica disponibilidade no estoque do Armazém
    3. Sistema designa Robô para a missão
    4. Robô navega até o Armazém usando o caminho mais rápido
    5. Ao chegar, Robô envia mensagem para Equipe do Armazém
    6. Equipe do Armazém confirma e carrega o item no robô
    7. Robô inicia fase deslocamento para o destino
    8. Robô entrega o item no local

![domain scenario 1](domain_scenarios/domain_scenario_1.png)

Cenário 2: Bateria Baixa na Fase de Coleta

- Actors:
    - Solicitante
    - Sistema de Controle de Missões
    - Robô A
    - Robô B

- World Objects:
    - Item
    - Estoque
    - Destino
    - Estação de recarga

- Actions and Steps:
    1. Solicitante solicita item médico
    2. Sistema controlador verifica disponibilidade no Armazém
    2. Sistema designa Robô A (bateria fraca)
    3. Durante navegação para Armazém, bateria cai para menos de 10%
    4. Robô navega até Armazém e o sistema detecta bateria menor que 10%
    5. Robô A interrompe missão e retorna à estação de recarga mais próxima
    6. Sistema automaticamente atribui missão a Robô B (bateria boa)
    7. Robô B navega para Armazém
    8. Robô B envia mensagem para Equipe do Armazém que coleta o Item
    9. Desloca até o Destino
    10. Completa entrega no Destino

![domain scenario 2](domain_scenarios/domain_scenario_2.png)

- ### Goal Model (v1)
A primeira versão do Goal Model é a disponibilizada para o workshop da matéria, sendo parte da base da maior parte das modelagens realizadas no projeto. Os goals são divididos desde o momento da solicitação, da coleta e da entrega

![goal model v1](images/goal_model_v1.svg)

## Fase 3: Decision
- ### Impact Map
O Impact Mapping é uma técnica de planejamento estratégico que visa conectar objetivos de negócio com iniciativas de desenvolvimento através de uma estrutura visual. No contexto do sistema de entregas, os Impact Maps foram utilizados para desdobrar goals de alto nível em entregas concretas, identificar atores relevantes e seus comportamentos desejados, mapear impactos que cada funcionalidade deve gerar e definir deliverables específicos

Cada Impact Map segue uma estrutura hierárquica de quatro níveis:
 * Nível 1: GOAL (Por quê?)
 * Nível 2: ACTOR (Quem?)
 * Nível 3: IMPACT (Como?)
 * Nível 4: DELIVERABLE (O quê?)

- Impact Map 1: Goal - Estar com bateria acima de 10%
![impact map 1](impact_maps/impact_map_1.png)

- Impact Map 2: Goal - Recurso é entregue ao robô
![impact map 2](impact_maps/impact_map_2.png)

- ### Goal Model (v2)
![goal model v2](images/goal_model_v2.svg)

## Fase 4: Formulation
- ### Specification by Example

Analisando o sistema de entregas foi possível coletar 5 user stories, desde o requerente dos materiais, até o gerente e o funcionário do armazém. Cada história possui regras específicas e seus exemplos dando certo e errado

- Feature 1:
![story1](images/story1.png)

- Feature 2:
![story2](images/story2.png)

- Feature 3:
![story3](images/story3.png)

- Feature 4:
![story4](images/story4.png)

- Feature 5:
![story5](images/story5.png)

- ### Goal Model (vFinal)
![goal model vfinal](goal_model/goal_model_definitivo.svg)

# 4. Conclusões
A fundamentação teórica junto aos modelos apresentados valida que a abordagem de engenharia de requisitos é tecnicamente acertiva e prática. Assegurando que o sistema de entregas será desenvolvido com base em requisitos bem compreendidos, alinhados com necessidades reais e especificados com precisão suficiente para guiar desenvolvimento, teste e implementação.

Em resumo, a metodologia aplicada garante que o sistema resultante será desde o começo do projeto até o fim permeada por requisitos bem coletados e mapeados.

# 5. Referências
 - ROBERTSON, Suzanne; ROBERTSON, James. Mastering the Requirements Process: Getting Requirements Right, 2012

 - VAN LAMSWEERDE, Axel. Requirements Engineering: From System Goals to UML Models to Software Specifications, 2009

 - HOFER, Stefan; SCHWENTNER, Henning. Domain Storytelling: A Collaborative, Visual, and Agile Way to Build Domain-Driven Software, 2021

 - ALEXANDER, Ian; MALDEN, Neil. Scenarios, Stories, Use Cases: Through the Systems Development Life-Cycle, 2004

 - ADZIC, Gojko. Making a big impact with software products and projects, 2012

 - PATTON, Jeff; ECONOMY, Peter. User Story Mapping: Discover the Whole Story, Build the Right Product, 2014

 - ROSE, Seb; NAGY, Gáspár. Formulation: Express examples using Given/When/Then, 2012