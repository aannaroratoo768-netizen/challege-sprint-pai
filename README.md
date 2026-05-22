# challenge-sprint-pai
Challenge Sprint - Prompt & Artificial Intelligence - equipe 03
integrantes da equipe 03: Wendel Pedro Rezende - RM: 573126 / Victor Hugo Lavaqui - RM: 573838 / Daniel Pupo Martinez - RM: 573075 / Arthur Araujo Massarioli - RM: 573308 / Beatriz da Silva Araújo - RM: 570619  / Anna Karla Rorato Albino - RM: 569604


## Projeto Chatbot GoodWe/FIAP

## O Problema:
Com o aumento de veículos elétricos (EVs), os condomínios enfrentam sérios desafios na gestão de eletropostos compartilhados. Sem uma inteligência centralizada, surgem três problemas críticos:
1. *sobrecarga da rede:* Risco de ultrapassar a demanda contratada do condomínio se múltiplos carros carregarem simultaneamente.
2. *injustiça na cobrança:* Dificuldade em registrar ciclos exatos de recarga por morador para um faturamento individualizado justo.
3. *atrito na reserva:* Falta de orquestração no uso compartilhado das vagas com carregadores.

## Proposta: desenvolver um chatbot inteligente GoodWe
Arquitetura tecnológica: *Framework de Orquestração: LangChain (Python):* Utilizado para gerenciar o histórico de conversas (memória), estruturar os prompts e facilitar a futura integração com APIs reais da GoodWe (via LangChain Tools/Agents).


## Justificativa Técnica:
Por que o LangChain, exatamente? Pois ele serve para facilitar a conexão entre Modelos de Linguagem de Grande Escala (LLMs), como GPT, Claude e Llama, com fontes de dados externas e ferramentas de software.
As principais funções do LangChain incluem:
1. Conexão com Dados Locais (RAG): Permite que a IA acerte respostas consultando seus próprios documentos, PDFs ou bancos de dados, evitando que ela invente informações.
2. Memória Conversacional: Adiciona histórico às conversas com a IA, permitindo que ela lembre o que foi dito anteriormente.
3. Cadeias (Chains): Cria fluxos onde a saída de uma etapa serve de entrada para a próxima (ex: ler um texto, resumir, traduzir e enviar por e-mail).
4. Agentes: Dá autonomia para o modelo de linguagem interagir com ferramentas externas, como APIs da web, calculadoras e sistemas internos.


## Pequeno contexto:
GoodWe:
a GoodWe é uma empresa global de tecnologia, líder mundial na fabricação de inversores fotovoltaicos (solares) e soluções de armazenamento de energia. A marca desenvolve equipamentos para projetos residenciais, comerciais, industriais e agronegócio, convertendo a luz do sol em eletricidade e gerenciando baterias.
O portfólio da marca inclui principalmente:
1. Inversores On-Grid: Convertem a energia dos painéis solares para uso imediato e injetam o excedente na rede elétrica.
2. Inversores Híbridos: Gerenciam tanto os painéis solares quanto baterias, garantindo energia ininterrupta mesmo em quedas de rede (sistema backup).
3. Baterias Inteligentes: Soluções próprias para armazenamento e autonomia energética.A marca destaca-se pela alta eficiência e possui forte presença no mercado brasileiro, sendo amplamente recomendada por especialistas e distribuída por empresas como Solfácil, Aldo Solar e Fotus.

O que a GoodWe faz?
a GoodWe é uma empresa fabricante líder mundial de inversores fotovoltaicos ("cérebro" do sistema de energia solar).
Incluem:
1. Inversores Solares (On-Grid e Off-Grid): São o "cérebro" do sistema. Eles transformam a corrente contínua gerada pelo sol em corrente alternada (pronta para uso nos eletrodomésticos). A GoodWe possui linhas de microinversores, inversores on-grid e off-grid para locais remotos.
2. Armazenamento Híbrido: A marca é pioneira em inversores híbridos, que gerenciam tanto a energia dos painéis quanto a carga e descarga de baterias.
3. Função Backup (UPS): Na falta de energia da rede pública, o sistema comuta instantaneamente para as baterias, mantendo os equipamentos ligados sem interrupções.
4. Gestão Inteligente (Load Shifting): Permite armazenar energia solar durante o dia para usá-la à noite ou nos horários de pico da rede, reduzindo custos na conta de luz.

fonte: https://de.goodwe.com/images/download/GW_EM_Manual%20Do%20Usuario-PT.pdf


## Fluxograma ---> link do fluxograma: [https://www.figma.com/board/NnzCxkTqZsGp2Nu6uQGe8O/Sprint1-PAI?node-id=0-1&t=L1FkkMtVQSmZHqlO-1](https://www.figma.com/board/NnzCxkTqZsGp2Nu6uQGe8O/Sprint1-PAI?node-id=0-1&t=K2qih9anm7fHgomL-1)

estrutura base pensada:

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
Você é o "GoodWe ChargeOps Specialist", um assistente virtual inteligente e altamente especializado na gestão de eletropostos GoodWe para condomínios residenciais. Seu objetivo é auxiliar síndicos e administradores prediais a operar o sistema de forma eficiente.

1. *Diretrizes fundamentais:* você entende de orquestração de potência (Dynamic Load Balancing), ciclos de recarga, faturamento por kWh e agendamento de recargas.
2. *Tom de voz e persona:* tom de voz profissional, que passe uma impressão cofiante, técnico porém acessível, focado em solução de problemas e segurança elétrica.
Por quê essa persona? Este tipo de personagem ajuda o chatbot a passar uma sensação mais confiante e profissional, visto que o mesmo foi criado com um objetivo de pensar e criar respostas para questões reais, ajudando nas dúvidas que o usuário tiver (desde que não saia do conhecimento do chatbot, caso contrário, o chat recusará a resposta e voltará para o foco inicial).
3. *Limitações:* se o usuário perguntar algo fora do ecossistema de carregamento GoodWe ou gestão de condomínios, recuse a resposta gentilmente, direcionando-o de volta ao foco.
4. *Regra de negócio(orquestração):* lembre sempre o síndico que o limite de potência simultânea do condomínio é de 44 kW. Se houver mais de 6 carros conectados, o sistema ativará o carregamento em fila ou reduzirá a corrente de cada um para 7.4 kW.


## Perguntas e respostas base para o Chatbot:

1. "O que são eletropostos compartilhados?" resposta: "Eletropostos compartilhados são estações de recarga para carros elétricos projetadas para múltiplos usuários, ideais para condomínios, prédios, empresas e estacionamentos."
2. "Que tipo de problemas que a ausência de mecanismos integrados em eletropostos compartilhados podem causar?" resposta: "Pode acabar sobrecarregando as demandas, ocorre quando muitos carros se abastecem simultaneamente."
3. "Como é que o projeto pode desenvolver respostas para esta operação?" resposta: "O chatbot está programado para pensar em diferentes propostas e opções para tentar resolver estas questões específicas."
4. "Há algum modo de tentar resolver este problema?" resposta: "Em locais públicos, Plataformas de ChargeOps (Operações de Carga) permitem a cobrança automática via aplicativo ou cartão, garantem segurança contra o uso indevido e geram relatórios detalhados de faturamento por usuário. Em Condomínios, a implementação de sistemas como o WEG Smart Charging System realiza o gerenciamento de carga. Ele lê a energia disponível em tempo real e distribui a potência de forma inteligente entre os veículos, evitando obras caras para aumento de carga na rede."
5. Caso o usuário faça uma pergunta que não tenha a ver com o tema do chatbot. Resposta: "Lamento, {user}. Este tipo de pergunta não está sob o meu alcance de raciocínio para responder. Foque apenas em perguntar questões relacionadas ao tema."

# Lembrete: Criar um documento .txt no Word para ser enviado para o professor.
