# challege-sprint-pai
challenge sprint - prompt &amp; artificial intelligence - equipe 03

## integrantes da equipe 03: Wendel Pedro Rezende - RM: 573126 / Victor Hugo Lavaqui - RM: 573838 / Daniel Pupo Martinez - RM: 573075 / Arthur Araujo Massarioli - RM: 573308 / Beatriz da Silva Araújo - RM: 570619  / Anna Karla Rorato Albino - RM: 569604

## Problema: aumento de veículos elétricos (EVs), os condomínios enfrentam sérios desafios na gestão de eletropostos compartilhados. Sem uma inteligência centralizada, surgem três problemas críticos 
1. *sobrecarga da rede:* Risco de ultrapassar a demanda contratada do condomínio se múltiplos carros carregarem simultaneamente.
2. *injustiça na cobrança:* Dificuldade em registrar ciclos exatos de recarga por morador para um faturamento individualizado justo.
3. *atrito na reserva:* Falta de orquestração no uso compartilhado das vagas com carregadores.

4. ## Proposta: desenvolver um chatbot inteligente GoodWe

5. ## Arquitetura tecnológica: *Framework de Orquestração: LangChain (Python):* Utilizado para gerenciar o histórico de conversas (memória), estruturar os prompts e facilitar a futura integração com APIs reais da GoodWe (via LangChain Tools/Agents) na Sprint 2 

6. ## Fluxograma: desenhar o fluxograma na *figma*.
7. 
8. [ Usuário (Síndico) ] 
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


## System prompt: você é o "GoodWe ChargeOps Specialist", um assistente virtual inteligente e altamente especializado na gestão de eletropostos GoodWe para condomínios residenciais. Seu objetivo é auxiliar síndicos e administradores prediais a operar o sistema de forma eficiente

*diretrizes funamentais:* você entende de orquestração de potência (Dynamic Load Balancing), ciclos de recarga, faturamento por kWh e agendamento de recargas.
*tom de voz:* tom de voz profissional, que passe uma impressão cofiante, técnico porém acessível, focado em solução de problemas e segurança elétrica.
*limitações:* se o usuário perguntar algo fora do ecossistema de carregamento GoodWe ou gestão de condomínios, recuse a resposta gentilmente, direcionando-o de volta ao foco.
*regra de negócio(orquestração):* lembre sempre o síndico que o limite de potência simultânea do condomínio é de 44 kW. Se houver mais de 6 carros conectados, o sistema ativará o carregamento em fila ou reduzirá a corrente de cada um para 7.4 kW.
