# Designfast — Smart Web Experience

## 1. O Problema
A Designfast, uma pequena empresa de serviços digitais, precisava modernizar sua presença online. Os clientes dependiam de contato manual para obter informações sobre serviços (Landing Pages, Equipe Dedicada) e preços. O objetivo foi criar uma solução web rápida, de baixo custo e escalável, automatizando o primeiro atendimento de forma inteligente sem perder a abordagem consultiva.

## 2. A Solução Desenvolvida e Ferramentas (No-Code/Low-Code)
A aplicação desenvolvida é um site institucional responsivo integrado a um assistente virtual.

* **Framer:** Utilizado como plataforma no-code principal para a construção da interface web responsiva e hospedagem do site.
* **Make:** Responsável pela orquestração do fluxo de dados e pelo processamento da Inteligência Artificial (Agente Maia).
* **Cloudflare Workers:** Utilizado como middleware seguro para receber as requisições do Framer e encaminhá-las via webhook para o Make, tratando as políticas de CORS.

<img width="1898" height="900" alt="Captura de tela 2026-10-24 154338" src="https://github.com/user-attachments/assets/52ecd71e-90b8-4f1f-9c0e-5dd5582f50cc" />
*Figura 1: Interface institucional do site da Designfast desenvolvido no Framer.*

## 3. Personalizações Realizadas (HTML, CSS e JavaScript)
Para ir além das limitações visuais do template no Framer, aplicou-se personalização com **CSS**.

Foram criados seletores específicos para a seção de preços (`#pricing`), focando nos elementos `PricingHeader` e `PricingSubtitle`. Essa intervenção em CSS garantiu que o subtítulo respeitasse a largura definida, quebrasse as linhas corretamente e mantivesse o alinhamento centralizado em todos os dispositivos, assegurando a legibilidade e a responsividade.

Além disso, foi injetado código customizado (**JavaScript**) no Framer para capturar as mensagens do usuário e enviá-las via método POST para o endpoint do Cloudflare.

<img width="1611" height="830" alt="Captura de tela 2026-10-13 141538" src="https://github.com/user-attachments/assets/d8622aaa-3223-4c13-af2f-1f3012035a34" /> <img width="1893" height="901" alt="Captura de tela 2026-10-13 144742" src="https://github.com/user-attachments/assets/a15ce8e1-ca07-4f09-bfdf-5cbf17cece4e" /> <img width="937" height="816" alt="Captura de tela 2026-10-24 154755" src="https://github.com/user-attachments/assets/8b6b8a30-69c3-40c6-9e17-e15653c40238" />

*Figura 2: Seção de Preços com ajuste de largura e alinhamento via CSS customizado.*

## 4. Recurso de IA e Automação Integrado
Implementou-se a **Maia**, uma consultora comercial virtual baseada em Inteligência Artificial acoplada a um fluxo de automação no **Make**.

### Arquitetura do Cenário no Make:
1. **Webhook (Custom Webhook):** Recebe a requisição POST enviada pelo site através do Cloudflare Worker, contendo a mensagem do visitante (`message`) e o identificador (`sessionId`).
2. **Atendimento IA (Make AI Agent / Maia):** Módulo de IA Generativa configurado com engenharia de prompt avançada. Aplica regras estritas de preços (Landing Page a R$ 350, Equipe Dedicada a R$ 1.200/mês), postura consultiva, suporte a transferências para o botão de especialistas do site e restrições da **LGPD** (bloqueio de coleta de dados sensíveis).
3. **JSON (Create JSON):** Estrutura o texto gerado pela IA e o ID de sessão nos campos `reply` e `sessionId`.
4. **Resposta JSON (Webhook Response - 200):** Envia a resposta formatada de volta para a aplicação web em tempo real.
5. **Erro JSON 500 (Webhook Response - Error Handler):** Rota de contingência para tratamento de falhas, impedindo que o chatbot fique travado sem resposta.

<img width="1020" height="689" alt="Captura de tela 2026-10-22 172912" src="https://github.com/user-attachments/assets/feb9170f-d163-4ffe-a3b3-661c9dba36c6" />
*Figura 3: Fluxo completo de automação e integração de IA construído no Make.*

<img width="1187" height="639" alt="Captura de tela 2026-10-24 155024" src="https://github.com/user-attachments/assets/09b3bac7-48c1-43b2-9faa-f1fe970b2609" />
*Figura 4: Execução do fluxo no Make confirmando o processamento sem erros.*

 <img width="462" height="564" alt="Captura de tela 2026-10-24 155133" src="https://github.com/user-attachments/assets/2f07e94c-6cae-4ce0-87f5-6fb3b7a221bd" />
*Figura 5: Assistente virtual Maia respondendo às dúvidas de valores e serviços no site.*

## 5. Limitações e Aprendizados

* **Limitações:**
  * O agente de IA atual não registra automaticamente os dados do lead em um CRM externo, orientando o visitante a realizar o pedido de proposta através do canal de contato oficial do site.

* **Aprendizados Pessoais e Técnicos:**
  * **Customização de Código (CSS e JS):** Por não ter afinidade prévia com programação, o maior desafio prático foi aplicar as estilizações CSS no Framer para alinhar a seção de preços e acertar as quebras de linha responsivas. A inteligência artificial foi utilizada como parceira de apoio para gerar os trechos de código necessários, permitindo testar e ajustar o layout iterativamente até atingir o resultado visual desejado.
  * **Ajuste Fino de Engenharia de Prompt:** Alinhar o comportamento da "Maia" exigiu várias rodadas de teste. No início, a IA tendia a fornecer respostas muito longas ou com informações desnecessárias. Foi preciso refinar as instruções no Make para garantir que ela mantivesse o tom consultivo, fizesse apenas uma pergunta por mensagem e respeitasse estritamente as regras de negócio e de LGPD.
  * **Uso da IA como Copiloto de Desenvolvimento:** O projeto demonstrou na prática como ferramentas No-Code/Low-Code somadas à IA generativa permitem que pessoas sem background técnico em programação desenvolvam soluções funcionais, estéticas e integradas.

## 6. Como Acessar e Testar a Solução
Para avaliar o funcionamento da aplicação web e a integração do chatbot com a inteligência artificial, siga os passos abaixo:

1. **Acesse o site publicado:**
   Link oficial: https://real-method-609760.framer.app/

2. **Inicie o atendimento:**
   No canto inferior direito da tela, clique no ícone de chat (balão azul) para abrir a janela da assistente virtual "Maia".

3. **Testes recomendados:**
   Você pode testar o comportamento comercial e as regras de negócio da IA enviando as seguintes mensagens:
   * `"Quais serviços vocês oferecem?"` (Ela apresenta as opções disponíveis).
   * `"Quanto custa uma landing page?"` (Ela informa R$ 350 e faz uma pergunta de alinhamento).
   * `"Quero contratar um serviço de vocês."` (Ela assume postura consultiva para entender o objetivo).
   * `"Quero falar com um atendente"` (Ela indica o uso do botão de especialista presente no site).<img width="1898" height="900" alt="Captura de tela 2026-10-24 154338" src="https://github.com/user-attachments/assets/a134d82a-2ea5-43b2-84d7-fce227b9549a" />
