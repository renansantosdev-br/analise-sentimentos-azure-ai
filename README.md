# Análise de Sentimentos com Azure AI: Speech e Language Studio

## Resumo

Este repositório serve como um guia prático e um registro de aprendizado sobre a utilização dos serviços de Inteligência Artificial do Azure, especificamente o **Speech Studio** e o **Language Studio**. O foco principal é a criação de uma solução completa que transforma áudio de fala em insights acionáveis através da análise de sentimentos, documentando cada passo do processo e os insights adquiridos.

## 🎯 Objetivos de Aprendizagem

* **Aplicar os conceitos aprendidos em um ambiente prático:** Ir além da teoria, implementando uma solução de ponta a ponta com as ferramentas do Azure.
* **Documentar processos técnicos de forma clara e estruturada:** Criar um material de referência que seja útil tanto para revisão pessoal quanto para a comunidade.
* **Utilizar o GitHub como ferramenta para compartilhamento de documentação técnica:** Organizar e apresentar o conhecimento adquirido de forma profissional e acessível.

## 🛠️ Tecnologias Utilizadas

* **Microsoft Azure AI:** Plataforma de nuvem para serviços de Inteligência Artificial.
* **Azure Speech Studio:** Ferramenta para conversão de fala em texto (Speech-to-Text) de alta precisão.
* **Azure Language Studio:** Suíte de ferramentas para processamento e análise de linguagem natural, com foco em Análise de Sentimentos.
* **GitHub:** Plataforma para hospedagem do código e da documentação.

---

## 📖 Uso Prático e Aprofundado das Ferramentas

A verdadeira força desta solução está na combinação sinérgica do Speech Studio e do Language Studio. O processo consiste em um pipeline onde a qualidade da saída de uma etapa determina o sucesso da etapa seguinte.

### **1. Azure Speech Studio: A Ponte da Voz para o Texto**

O Speech Studio é a porta de entrada da nossa análise. Sua função é transcrever o áudio com a maior fidelidade possível.

#### **Funcionalidades Chave Exploradas:**

* **Transcrição em Lote (Batch Transcription):** Ideal para processar um grande volume de arquivos de áudio já gravados, como chamadas de um call center, entrevistas ou reuniões. A precisão aqui é crucial.
* **Modelos de Fala Personalizados (Custom Speech):** Para cenários de nicho com vocabulário específico (termos técnicos, nomes de produtos, jargões), o treinamento de um modelo personalizado pode aumentar drasticamente a acurácia da transcrição, evitando que a análise de sentimentos subsequente seja feita sobre um texto incorreto.

#### **Insights e Anotações Práticas:**

* **Qualidade do Áudio é Fundamental:** A máxima "garbage in, garbage out" se aplica perfeitamente aqui. Áudios com baixo ruído, sem sobreposição de vozes e com clareza na dicção geram transcrições significativamente melhores.
* **Configuração de Idioma e Localidade:** Especificar corretamente o idioma e a região (ex: `pt-BR` para Português do Brasil) melhora o reconhecimento de sotaques e expressões locais.
* **Pontuação e Formatação:** O Speech Studio pode adicionar pontuação automaticamente, o que é vital para o Language Studio interpretar corretamente as pausas e a estrutura das frases, impactando a análise de sentimentos.

*Exemplo de transcrição pode ser encontrado em: [`/artefatos/transcricoes/`](./artefatos/transcricoes/)*

### **2. Azure Language Studio: Decifrando a Intenção no Texto**

Com o texto em mãos, o Language Studio entra em ação para extrair o significado e o sentimento por trás das palavras.

#### **Funcionalidades Chave Exploradas:**

* **Análise de Sentimentos (Sentiment Analysis):** Classifica um texto (ou cada sentença individualmente) como `positivo`, `negativo` ou `neutro`. O recurso mais valioso aqui são os **scores de confiança**, que indicam a probabilidade de cada classificação estar correta. Um score de `0.95` para `negativo` é um indicador muito mais forte do que um score de `0.55`.

* **Mineração de Opinião (Aspect-Based Sentiment Analysis):** Este é o recurso que aprofunda a análise. Em vez de apenas um sentimento geral, ele identifica o sentimento associado a **aspectos** ou **tópicos específicos** dentro do texto.

    * **Exemplo:** Na frase "A bateria do celular é ótima, mas a câmera é muito lenta", a análise de sentimento tradicional poderia resultar em "misto" ou "neutro". Com a Mineração de Opinião, obtemos:
        * `Bateria`: **Positivo**
        * `Câmera`: **Negativo**

#### **Insights e Anotações Práticas:**

* **Sentimento Misto é Comum e Valioso:** Muitas opiniões reais não são 100% positivas ou negativas. Identificar esses sentimentos mistos é crucial para um feedback completo.
* **Contexto é Rei:** A análise é poderosa, mas não infalível. Uma frase como "Que atendimento rápido, inacreditável!" pode ser genuinamente positiva ou sarcástica. O modelo padrão captura o sentimento literal; a análise de sarcasmo ainda é um desafio complexo em IA.
* **Granularidade da Análise:** Analisar o sentimento por sentença oferece uma visão muito mais detalhada do que analisar o sentimento do documento inteiro. Uma chamada de suporte pode começar negativa, se tornar neutra durante a resolução e terminar positiva.

*Exemplo de resultado da análise pode ser encontrado em: [`/artefatos/resultados_analise/`](./artefatos/resultados_analise/)*

---

## 💡 Fluxo de Trabalho da Solução: De Ponta a Ponta

1.  **Entrada de Áudio:** Um arquivo de áudio (ex: `.wav`, `.mp3`) é carregado.
2.  **Processamento no Speech Studio:** O áudio é submetido ao serviço de Speech-to-Text, que o transcreve para um arquivo de texto.
3.  **Entrada de Texto no Language Studio:** O texto transcrito é usado como entrada para o serviço de Análise de Sentimentos.
4.  **Análise e Geração de Insights:** O Language Studio retorna uma estrutura de dados (geralmente JSON) com o sentimento geral, o sentimento por sentença e a mineração de opinião sobre aspectos específicos.
5.  **Tomada de Decisão:** Os insights gerados podem ser usados para avaliar a satisfação do cliente, identificar pontos de melhoria em produtos/serviços e treinar equipes de atendimento.

![Fluxo de Trabalho](docs/imagens/workflow_diagram.png) ## Conclusão

Esta prática demonstrou como os serviços do Azure AI podem ser orquestrados para criar soluções sofisticadas de análise de linguagem. A documentação neste repositório reflete as etapas, os desafios e os aprendizados do processo, servindo como uma base sólida para futuras implementações e estudos na área de IA de Voz e Linguagem.
