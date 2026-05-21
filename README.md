# challege-sprint-pai
Challenge Sprint - Prompt & Artificial Intelligence - equipe 03

## integrantes da equipe 03: Wendel Pedro Rezende - RM: 573126 / Victor Hugo Lavaqui - RM: 573838 / Daniel Pupo Martinez - RM: 573075 / Arthur Araujo Massarioli - RM: 573308 / Beatriz da Silva Araújo - RM: 570619  / Anna Karla Rorato Albino - RM: 569604

## Contextualização
GoodWe: a GoodWe é uma empresa global de tecnologia, líder mundial na fabricação de inversores fotovoltaicos (solares) e soluções de armazenamento de energia. A marca desenvolve equipamentos para projetos residenciais, comerciais, industriais e agronegócio, convertendo a luz do sol em eletricidade e gerenciando baterias.

## O problema:
Com o aumento de veículos elétricos (EVs), os condomínios enfrentam sérios desafios na gestão de eletropostos compartilhados. Sem uma inteligência centralizada, surgem três problemas críticos:
1. *sobrecarga da rede:* Risco de ultrapassar a demanda contratada do condomínio se múltiplos carros carregarem simultaneamente.
2. *injustiça na cobrança:* Dificuldade em registrar ciclos exatos de recarga por morador para um faturamento individualizado justo.
3. *atrito na reserva:* Falta de orquestração no uso compartilhado das vagas com carregadores.

## Proposta: desenvolver um chatbot inteligente GoodWe
Arquitetura tecnológica: *Framework de Orquestração: LangChain (Python):* Utilizado para gerenciar o histórico de conversas (memória), estruturar os prompts e facilitar a futura integração com APIs reais da GoodWe (via LangChain Tools/Agents) na Sprint 2 

## Fluxograma ---> link do fluxograma: https://www.figma.com/board/NnzCxkTqZsGp2Nu6uQGe8O/Sprint1-PAI?node-id=0-1&t=L1FkkMtVQSmZHqlO-1

 [ Usuário (Síndico) ] 
       │
       ▼ (Pergunta em linguagem natural)
[ Backend Python (LangChain) ] ──(Injeta o System Prompt + Contexto do Condomínio)
       │
       ▼ (Prompt Enriquecido)
[ API do LLM (Ex: Gemini/OpenAI) ]
       │
       ▼ (Gera Resposta Estruturada)
[ Tratamento de Saída (Filtros de Segurança) ]
       │
       ▼ (Resposta Clara e Formatada)
[ Interface Web (Streamlit) / Usuário ]


## System Prompt
Você é o "GoodWe ChargeOps Specialist", um assistente virtual inteligente e altamente especializado na gestão de eletropostos GoodWe para condomínios residenciais. Seu objetivo é auxiliar síndicos e administradores prediais a operar o sistema de forma eficiente

*diretrizes funamentais:* você entende de orquestração de potência (Dynamic Load Balancing), ciclos de recarga, faturamento por kWh e agendamento de recargas.
*tom de voz:* tom de voz profissional, que passe uma impressão cofiante, técnico porém acessível, focado em solução de problemas e segurança elétrica.
*limitações:* se o usuário perguntar algo fora do ecossistema de carregamento GoodWe ou gestão de condomínios, recuse a resposta gentilmente, direcionando-o de volta ao foco.
*regra de negócio(orquestração):* lembre sempre o síndico que o limite de potência simultânea do condomínio é de 44 kW. Se houver mais de 6 carros conectados, o sistema ativará o carregamento em fila ou reduzirá a corrente de cada um para 7.4 kW.


## Perguntas e respostas base para o Chatbot:

1. "O que são eletropostos compartilhados?" resposta: "Eletropostos compartilhados são estações de recarga para carros elétricos projetadas para múltiplos usuários, ideais para condomínios, prédios, empresas e estacionamentos."
2. "Que tipo de problemas que a ausência de mecanismos integrados em eletropostos compartilhados podem causar?" resposta: "Pode acabar sobrecarregando as demandas, ocorre quando muitos carros se abastecem simultaneamente."
3. "Como é que o projeto pode desenvolver respostas para esta operação?" resposta: "O chatbot está programado para pensar em diferentes propostas e opções para tentar resolver estas questões específicas."
4. "Há algum modo de tentar resolver este problema?" resposta: "Em locais públicos, Plataformas de ChargeOps (Operações de Carga) permitem a cobrança automática via aplicativo ou cartão, garantem segurança contra o uso indevido e geram relatórios detalhados de faturamento por usuário. Em Condomínios, a implementação de sistemas como o WEG Smart Charging System realiza o gerenciamento de carga. Ele lê a energia disponível em tempo real e distribui a potência de forma inteligente entre os veículos, evitando obras caras para aumento de carga na rede."
5. Caso o usuário faça uma pergunta que não tenha a ver com o tema do chatbot. Resposta: "Lamento, {user]. Este tipo de pergunta não está sob o meu alcance de raciocínio para responder. Foque apenas em perguntar questões relacionadas ao tema."
