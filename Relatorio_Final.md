UNIVERSIDADE FEDERAL DO ABC

PROCESSAMENTO DIGITAL DE IMAGENS
MEDIVISÃO - Auxílio ao Diagnóstico de Câncer de Pele

Equipe 1:
Lorena Silva Sampaio - 11201212025
Samira Haddad - 11201812350
Larissa Rodrigues de Almeida - 11201812076
William Fernandes Dias - 11202020043

SANTO ANDRÉ
2025

SUMÁRIO
INTRODUÇÃO	3
Contexto e Cenário de Aplicação	3
Fundamentação Teórica	4
MATERIAIS E MÉTODOS	6
Modelagem Funcional do SPI (MF)	6
Descrição da implementação do Sistema de Processamento de Imagem (SPI)	8
Lista dos Arquivos	10
Análise Técnica	12
LABORATÓRIO EXPERIMENTAL	13
Roteiro do Laboratório Experimental	13
Análise dos Resultados do Teste de Campo TCS	20
CONCLUSÕES	26
REFERÊNCIAS BIBLIOGRÁFICAS	28
ANEXOS	28
ANEXO A - CÓDIGOS	28
ANEXO B - ENTREVISTAS	29

INTRODUÇÃO
Esse projeto é dedicado à detecção precoce de câncer de pele através do uso de técnicas de Processamento Digital de Imagens (PDI) para o tratamento e análise de imagens de lesões cutâneas, com o objetivo de auxiliar na identificação de padrões sugestivos de malignidade.

O objetivo é realizar um tratamento em imagens obtidas com fotografias tiradas com câmera (web-cam) através de técnicas de pré-processamento, as imagens pré-processadas devem então ser submetidas para análise por uma rede neural, construída a partir de treinamento de modelo de aprendizado de máquina.

As etapas de pré-processamento que visam otimizar a qualidade das imagens e realçar informações relevantes incluem:

Tratamento de ruídos: Redução de artefatos para melhorar a clareza das imagens.
Filtragem: Aplicação de filtros para destacar bordas e texturas importantes das lesões.
Realce e Restauração: Melhoria do contraste e da nitidez para facilitar a visualização de detalhes.
Ajuste de Histograma: Otimização da distribuição de cores para melhor análise visual.
Segmentação: Isolamento da área da lesão para análise focada.

Em adição, modelos de redes neurais foram implementadas para a classificação final das lesões.

Assim sendo, o foco inicial deste projeto é demonstrar como as técnicas de processamento digital de imagens podem ser aplicadas eficazmente em imagens de câncer de pele, preparando-as para uma análise mais aprofundada com inteligência artificial. Vale salientar que o tema foi definido após a realização de entrevistas empáticas com pessoas de diversos perfis (em anexo), através das quais detectamos uma necessidade de atuação de processamento digital de imagens na área médica e facilitação de diagnóstico precoce.

Contexto e Cenário de Aplicação

Esse trabalho se dá no contexto médico, na relação médico-paciente em atendimento ambulatorial ou a distância.

O público alvo são médicos, especialmente dermatologistas, técnicos e demais profissionais da saúde responsáveis pela análise de exames de câncer de pele. Logo, usuários sem experiência com tecnologia da informação e computação.   

O intuito é que a ferramenta não necessite de treinamento prévio, mas que seja viável consultar a documentação em caso de dúvidas. A interação com o sistema se dará por desktops, os dispositivos de entrada seriam mouse e teclado, e os dispositivos de saída a tela.

O cenário de aplicação se dá uma vez que uma imagem de pele esteja disponível, o médico (seja do laboratório ou o solicitante) fará a submissão da imagem via computador. O sistema também prevê que uma foto possa ser tirada via webcam e submetida para a análise, a análise no geral demora menos de 30 segundos para devolver um resultado, apontando um mapa de calor e probabilidade da mancha na pele ser um câncer maligno ou benigno.

Para a sua execução, o médico precisará apenas seguir uma sequência de cliques bem destacada e intuitiva, bem como confirmar as informações do paciente com a imagem a ser analisada (é importante que essas informações estejam corretas para que os dados provenientes da análise sejam devidamente anexados ao prontuário do paciente).

O sistema é acessado via interface web, onde profissionais de saúde ou pacientes podem:
- Se cadastrar;
- Tirar uma foto;
- Realizar processamento na foto obtida;
- Submeter a foto para análise;
- Receber um resultado com mapa de calor, porcentagem de probabilidade do diagnóstico ser benigno ou maligno;

Fundamentação Teórica

O avanço da inteligência artificial tem o potencial de transformar a área da saúde, especialmente em um cenário onde a disponibilidade de profissionais médicos é limitada. No Brasil, a proporção de médicos é de 2,56 por mil habitantes (AGÊNCIA BRASIL, 2023), o que pode dificultar o acesso rápido e eficiente a diagnósticos especializados, especialmente em regiões mais afastadas. Esse número é significativamente menor do que em países como Mônaco, que conta com 7,51 médicos por mil habitantes (WORLD BANK, 2023), demonstrando uma disparidade na distribuição de profissionais da saúde ao redor do mundo.

A detecção precoce de doenças como o câncer é um fator crítico para a eficácia do tratamento. No caso do câncer de cólon e reto, por exemplo, a taxa de cura pode chegar a 90% quando o diagnóstico é feito em estágios iniciais (PFIZER, 2023). No entanto, o diagnóstico precoce depende de exames de imagem e da avaliação médica, o que pode ser prejudicado por limitações de infraestrutura e acesso. Além disso, o sistema de registro de exames e diagnósticos no SUS ainda é bastante primitivo (GOVERNO FEDERAL, 2023), sem integração eficiente dos históricos clínicos e das suspeitas médicas, dificultando um acompanhamento contínuo e preciso dos pacientes.

Estudos mostram que a precisão média dos algoritmos de IA aplicados às modalidades de imagem combinadas foi de 86%, semelhante à dermatoscopia. Com o avanço da tecnologia de IA aumenta-se a eficácia do diagnóstico de imagens da pele e consequentemente há melhoria no prognóstico. (GUANDALINI et al.)

Para atingir esse objetivo, usamos a biblioteca OpenCV (Open Source Computer Vision Library), uma biblioteca de código aberto voltada para visão computacional e processamento de imagens em tempo real (Bradski, G., 2000). Utilizamos as funções abaixo:

1. **Resize (Redimensionamento)**: o redimensionamento de imagens adapta a entrada a um tamanho padrão, garantindo uniformidade.

2. **Normalização**: transforma os valores dos pixels (geralmente no intervalo [0, 255]) para uma faixa menor, como [0, 1] ou [-1, 1].

3. **Filtro Gaussiano**: utilizado para suavizar a imagem, reduzindo ruídos e detalhes finos. Ele aplica uma média ponderada, onde os pixels mais próximos têm mais influência que os distantes, seguindo uma distribuição Gaussiana.

4. **Filtro CLAHE (Contrast Limited Adaptive Histogram Equalization)**: aumenta o contraste da imagem localmente, evitando a super amplificação do ruído. Útil em imagens de baixa iluminação, onde o contraste global pode ser insuficiente.

5. **Segmentação de Otsu**: técnica de binarização automática que calcula um limiar ótimo separando fundo e objeto baseando-se na minimização da variância intraclasse.

6. **Segmentação de Watershed**: interpreta a imagem como um relevo topográfico. As regiões "alagadas" a partir de marcadores iniciais permitem a segmentação precisa de objetos adjacentes que tocam uns aos outros.

7. **Operações Morfológicas (Abertura, Fechamento, Dilatação e Erosão)**:
   - **Erosão (cv2.erode)**: Diminui áreas brancas, removendo pequenos ruídos.
   - **Dilatação (cv2.dilate)**: Expande áreas brancas, reforçando objetos.
   - **Abertura**: Erosão seguida de dilatação; remove pequenos objetos/brilhos e preserva a estrutura principal.
   - **Fechamento**: Dilatação seguida de erosão; fecha pequenos buracos dentro dos objetos.

8. **Rede Neural Convolucional (CNN)**:
   Após o pré-processamento, as imagens são alimentadas em uma CNN:
   - **Camadas Convolucionais**: capazes de extrair automaticamente padrões locais (bordas, texturas) por meio de filtros treináveis.
   - **Camada Densa (Fully Connected)**: usa os recursos extraídos para tomar decisões (classificação, regressão, etc.).

Assim sendo, este projeto utiliza técnicas de processamento digital de imagens e rede neural para desenvolver uma ferramenta que auxilie no diagnóstico precoce do câncer de pele.

MATERIAIS E MÉTODOS

Modelagem Funcional do SPI (MF)

O sistema permite que usuários tirem uma foto com webcam e enviem as imagens de lesões na pele para pré-processamento com as seguintes funções:

- Resize  
- Normalização  
- Filtro Gaussiano  
- Filtro CLAHE  
- Segmentação de Otsu  
- Segmentação de Watershed  
- Operações Morfológicas: abertura, fechamento, dilatação e erosão.

As imagens pré-processadas são então enviadas para uma rede neural convolucional (CNN), com duas camadas convolucionais e uma densa.

O dataset ISIS 2024 foi utilizado para treinar essa rede. Esse dataset foca na detecção de câncer de pele a partir de imagens de lesões cutâneas recortadas de fotografias. Ele contém milhares de imagens JPEG de lesões rotuladas com diagnósticos binários (maligno ou benigno) e é proveniente da colaboração internacional ISIC.

Adicionalmente, implementamos uma aplicação web para propiciar maior facilidade aos usuários. Apresentamos um fluxograma representando o funcionamento do backend e modelo UML (Unified Modeling Language) do banco de dados.

Back-end (notebook):

(Figura 1: Fluxograma do processamento no backend)

Banco de dados:

(Figura 2: Modelo UML do Banco de Dados)

Descrição da implementação do Sistema de Processamento de Imagem (SPI)

Este projeto concentra-se no pré-processamento de imagens de pele utilizando os fundamentos do Processamento Digital de Imagens (PDI) aprendidos na disciplina, com o objetivo de preparar as imagens para análises posteriores, como a aplicação de técnicas de aprendizado de máquina (ML) e redes neurais profundas.

O sistema desenvolvido é composto por duas partes principais:

- Um notebook Jupyter, que demonstra o pipeline completo de pré-processamento e classificação.
- Uma aplicação web, que permite a exploração interativa das funcionalidades implementadas.

Técnicas de Pré-Processamento Aplicadas

As etapas de pré-processamento realizadas incluem:

- Redução de Ruído: Suavização com filtro Gaussiano.
- Filtragem e Convolução: Realce de bordas e texturas.
- Realce de Contraste: Aplicação de CLAHE e ajustes de histograma.
- Segmentação: Separação da região de interesse utilizando métodos como Otsu e Watershed.
- Operações Morfológicas: Erosão, dilatação, abertura e fechamento para refinamento das máscaras segmentadas.

Implementação da Rede Neural Convolucional (CNN)

Após o pré-processamento das imagens, foi desenvolvido e treinado um modelo de Rede Neural Convolucional (CNN) para a tarefa de classificação binária das imagens.

O modelo apresenta a seguinte estrutura:

- **Camadas de Aumento de Dados**: Transformações aleatórias como rotações, flips, zooms e variações de brilho, para melhorar a robustez do modelo.
- **Pré-processamento**: Normalização dos pixels para a faixa [0,1] usando Rescaling.
- **Primeira Camada Convolucional**: 32 filtros (3×3), ativação ReLU, seguida de uma camada de max-pooling.
- **Segunda Camada Convolucional**: 64 filtros (3×3), ativação ReLU, seguida de max-pooling.
- **Camada de Flattening**: Transformação dos mapas de ativação em vetor.
- **Camada Densa**: 128 unidades com ativação ReLU e regularização com Dropout (0,5).
- **Camada de Saída**: 2 unidades de saída com ativação Sigmoid para classificação binária.

O modelo foi compilado utilizando o otimizador Adam e a função de perda `binary_crossentropy`, sendo avaliado com as métricas de **acurácia**, **precisão** e **recall**.

O treinamento foi realizado com:
- 10 épocas,
- Batch size de 32,
- 20% dos dados utilizados para validação.

Por fim, o modelo foi avaliado utilizando as métricas do relatório de classificação (*classification report*), demonstrando a eficácia do pipeline completo de pré-processamento e classificação.

Aplicação Web

A aplicação é acessada através do arquivo `index.html`, podendo ser aberta diretamente no navegador ou executada em um servidor local. Para autenticação, um formulário de login está disponível, utilizando as credenciais:

- Usuário: `b`
- Senha: `b`

Há ainda a opção de criação de novos usuários por meio de uma tela de cadastro. Após o login, o usuário pode navegar entre as seguintes funcionalidades:

- Página Inicial: Apresentação do projeto e menu de navegação.
- Perfil: Visualização e edição das informações pessoais.
- Captura e Upload de Imagens: Upload de imagens de pele ou captura por câmera.
- Pré-processamento: Exibição detalhada das técnicas aplicadas (segmentação, filtragem e realce).
- Análise de Imagens: Visualização dos resultados de processamento e classificação.

Lista dos Arquivos

- **Backend-notebook [GitHub]**:  
  https://github.com/samyhad/skin_cancer_detection

- **Aplicação web [GitHub]**:  
  https://github.com/lorenypsum/medivisao

- **Aplicação web [página de acesso]**:  
  https://lorenypsum.github.io/medivisao/pages/index.html

(Figura 3: Imagem da tela de pré-processamento de imagens)  
(Figura 4: Imagem da tela de análise de imagens)

Análise Técnica

**Grau de Atendimento ao Cenário Proposto**

- **Pré-processamento**: O sistema desenvolvido atendeu de forma satisfatória ao cenário proposto, que era o de pré-processar imagens dermatológicas para posterior análise baseada em redes neurais convolucionais (CNNs). As etapas de redução de ruído, segmentação de lesões, realce de contraste e filtragem morfológica foram testadas e aplicadas corretamente para fornecer imagens pré-processadas para a rede neural.

- **Resultado rede neural**: O resultado da rede neural se deu de forma parcialmente satisfatória. Embora tenha conseguido apresentar um mapa de calor na imagem e uma probabilidade de câncer maligno ou benigno, os resultados ainda não chegam perto do estado da arte. A rede neural tem apenas duas camadas de profundidade e requer mais treinamento para apresentar resultados melhores. Como melhoria futura, deveríamos utilizar uma rede já pré-treinada ou dedicar tempo e recursos para a criação, treinamento e validação de uma rede maior.

- **Aplicação web funcional**: Permitiu a interação do usuário com o sistema, desde o upload das imagens até a visualização dos resultados de análise, atendendo também a objetivos de usabilidade e integração.

**Métricas de Desempenho Obtidas**

Após o treinamento do modelo CNN com as imagens pré-processadas, foram obtidas as seguintes métricas de avaliação no conjunto de teste:

| Métrica     | Valor (%) |
|-------------|------------|
| Acurácia    | 72,03%     |
| Precisão    | 65,48%     |
| Recall      | 93,22%     |
| F1-Score    | 76,92%     |

(Tabela 1: Resultados dos testes)

Análise Qualitativa

**Pré-processamento**:  
A aplicação das técnicas de filtragem, segmentação e realce de contraste melhorou visualmente a qualidade das imagens, favorecendo a extração de padrões relevantes pelas camadas convolucionais.

**Análise**:  
O modelo CNN é simples (apenas duas camadas convolucionais) e não foi capaz de atingir métricas de desempenho completamente satisfatórias, mas mostrou um resultado prévio para um cenário de prototipação inicial.

**Interface**:  
A aplicação web ofereceu uma experiência intuitiva para upload e análise das imagens, permitindo validar o fluxo de ponta a ponta sem necessidade de configuração técnica adicional por parte do usuário.

---

### LABORATÓRIO EXPERIMENTAL

**Roteiro do Laboratório Experimental**

Para utilizar o sistema desenvolvido para o projeto, o usuário deve seguir o seguinte passo-a-passo:

De forma prática e intuitiva, o usuário segue estes passos:

1. **Captura de Imagem**:  
O sistema oferece uma funcionalidade de captura de imagem, onde o usuário pode tirar uma foto da mancha ou lesão diretamente com sua câmera (por exemplo, usando um notebook, celular ou webcam).

2. **Pré-processamento Automático**:  
Após capturada, a imagem é automaticamente tratada com diversas técnicas de PDI:
   - Remoção de ruídos, para limpar a imagem;
   - Realce de bordas e contraste, para destacar os detalhes da lesão;
   - Ajuste de iluminação e nitidez, facilitando a análise visual;
   - Segmentação da área da mancha, isolando a região de interesse.

3. **Visualização dos Resultados**:  
O sistema exibe lado a lado a imagem original e a imagem processada, mostrando claramente os realces feitos. Isso ajuda o usuário a perceber possíveis alterações visuais relevantes na lesão.

4. **Análise Baseada em Padrões Visuais**:  
Embora o sistema ainda não forneça um diagnóstico médico, ele ajuda a identificar padrões visuais que podem ser sugestivos de alteração na pele, servindo como uma ferramenta educativa e preventiva.

**Procedimento experimental**

1. **Abrir o sistema MediVisão**:  
   Acesse: https://lorenypsum.github.io/medivisao/pages/index.html

2. **Login**:  
   Ao abrir o sistema do MediVisão, será possível visualizar a tela de login (Figura 5). Utilize as credenciais:
   - Usuário: b
   - Senha: b

   Isso permite o acesso como usuário anônimo para testar a plataforma.

3. **Tela inicial**:  
   Após o login, será exibida a tela inicial da plataforma (Figura 6).

4. **Captura de imagem da pele**:
   - No menu lateral esquerdo, clique em “Pré-Processamento” (Figura 7).
   - Na tela de captura de imagem, clique em “Ativar câmera” (Figura 8).
   - Mire a câmera na mancha da pele e clique em “Capturar foto” (Figura 9).

5. **Processamento e download da imagem capturada**:
   - Após a captura da foto, clique no botão “Carregar Imagem” para prepará-la para o processamento (Figura 10).
   - A imagem será exibida na seção “Imagem original”.
   - O usuário poderá realizar o download, salvar a imagem e aplicar filtros para que o sistema consiga identificar e analisar lesões com maior precisão (Figura 11).

6. **Submissão da imagem para análise**:
   - Salve a imagem clicando em “Download”.
   - Navegue para a página de análise (Figura 12).
   - Selecione a imagem salva no seu computador e clique no botão “Analisar Imagem”.

7. **Resultados da análise**:
   - Após a conclusão da análise, clique no botão “OK”.
   - Desça até o fim da página para ver os resultados (Figura 13).

   O mapa de saliência indica a existência de manchas ou possíveis lesões na pele, e o diagnóstico representa a probabilidade da existência de câncer de pele.

   Caso deseje salvar o resultado da análise, clique no botão azul escrito “Salvar Resultado”.

Análise dos Resultados do Teste de Campo TCS

Durante os testes de campo, 8 usuários testaram o software, realizando o roteiro descrito anteriormente. Após a execução, cada candidato respondeu dois questionários: um para avaliar o experimento e outro para fornecer feedback sobre o sistema.

**Experimento**

As figuras 14 a 19 mostram as perguntas sobre o experimento e um consolidado das respostas dos usuários:

(Figura 14 - Questão 1 do questionário sobre o experimento)  
(Figura 15 - Questão 2 do questionário sobre o experimento)  
(Figura 16 - Questão 3 do questionário sobre o experimento)  
(Figura 17 - Questão 4 do questionário sobre o experimento)  
(Figura 18 - Questão 5 do questionário sobre o experimento)  
(Figura 19 - Questão 6 do questionário sobre o experimento)

Com base nas respostas, pode-se concluir que o roteiro foi bem estruturado, e não houve dificuldades em executá-lo. Além disso, é possível afirmar que o experimento foi suficiente para que os usuários compreendessem a proposta do projeto e como ele pode ser aplicado em uma situação real.

**Feedback dos usuários**

As figuras 20 a 24 mostram os resultados da pesquisa de feedback realizada com os candidatos do experimento:

(Figura 20 - Questão 1 do questionário de feedback)  
(Figura 21 - Questão 2 do questionário sobre o experimento)  
(Figura 22 - Questão 3 do questionário sobre o experimento)  
(Figura 23 - Questão 4 do questionário sobre o experimento)  
(Figura 24 - Questão 7 do questionário sobre o experimento)

Além das perguntas de múltipla escolha, o questionário incluiu questões sobre usabilidade, qualidade e aplicabilidade do MediVisão. No geral, a interface do sistema e a facilidade de uso se destacaram como principais pontos fortes, e a maioria dos usuários confirmou que ele seria útil para diagnósticos de câncer de pele.

Portanto, a análise dos resultados do experimento mostra que o sistema cumpre o objetivo de oferecer um diagnóstico rápido e automatizado de malignidade cutânea de forma prática e eficiente.

CONCLUSÕES

O projeto proposto teve como objetivo principal aplicar técnicas de Processamento Digital de Imagens (PDI) no pré-processamento de imagens de pele para futura utilização em análises baseadas em redes neurais convolucionais (CNNs). Conforme demonstrado ao longo do trabalho, os objetivos definidos na introdução foram alcançados com sucesso.

A modelagem do projeto foi bem estruturada, contemplando:

- A correta aplicação das técnicas de pré-processamento de imagem (remoção de ruído, segmentação, realce de contraste e operações morfológicas);
- O desenvolvimento de um modelo CNN simples e funcional para classificação binária das imagens;
- A criação de uma aplicação web que integra de maneira prática o carregamento, processamento e análise das imagens.

Os exemplos apresentados no relatório, como o fluxo de pré-processamento e os resultados de classificação da CNN, corroboram a efetividade da abordagem utilizada. O pipeline de pré-processamento demonstrou potencial ao permitir que a rede alcançasse um **recall de 93,22%**, o que é particularmente relevante nesse tipo de aplicação, onde a sensibilidade do modelo (capacidade de identificar corretamente os casos positivos) é crítica para evitar falsos negativos.

Apesar da acurácia global de 72,03% e da precisão de 65,48%, o F1-score de 76,92% mostra um bom equilíbrio entre precisão e recall. Esses resultados sugerem que o modelo está mais inclinado a identificar corretamente lesões suspeitas, mesmo que cometa alguns falsos positivos — um trade-off aceitável em cenários clínicos, onde o custo de uma falha em detectar um caso real pode ser alto.

Assim, o pipeline proposto mostra-se promissor para aplicações que priorizam alta sensibilidade na análise de imagens dermatológicas.

**Pontos Positivos**

- Integração completa entre pré-processamento de imagem, treinamento de modelo e interface web;
- Aplicação prática dos conceitos de PDI, reforçando o aprendizado teórico com implementação concreta;
- Resultados quantitativos satisfatórios, mesmo com um modelo CNN relativamente simples;
- Facilidade de uso da aplicação web, permitindo a interação intuitiva com as funcionalidades desenvolvidas.

**Pontos Negativos**

- Volume limitado de dados para treinamento e teste, o que pode ter impactado a generalização do modelo;
- Simplicidade do modelo CNN: a rede utilizada tinha apenas duas camadas convolucionais; redes mais profundas poderiam melhorar ainda mais o desempenho;
- Falta de validação cruzada: apenas uma divisão simples entre treino e teste foi realizada, o que poderia ser aprimorado para maior robustez dos resultados;
- Funcionalidade de classificação ainda inicial: o sistema identifica padrões, mas não realiza uma classificação clínica ou diagnóstica definitiva, o que seria necessário em aplicações reais de apoio médico.

Em síntese, a implementação proposta foi bem-sucedida em atingir os objetivos acadêmicos, demonstrando a viabilidade da combinação de técnicas de pré-processamento de imagens com aprendizado profundo em um contexto de análise de imagens médicas. O projeto também estabelece bases sólidas para futuras extensões, como a utilização de redes mais complexas, ampliação da base de dados e melhorias na avaliação do modelo.

REFERÊNCIAS BIBLIOGRÁFICAS

Guandalini, C. C. V., Silva, L. S. B., Ribeiro, A. C. M., Franceschini, C., Silva, J. P. F. da, Prata, M. C., … Machado, F. L. C. (2024). INTELIGÊNCIA ARTIFICIAL NA DETECÇÃO DE CÂNCER DE PELE: BENEFÍCIOS E DESAFIOS PARA A PRÁTICA DERMATOLÓGICA. Revista Ibero-Americana De Humanidades, Ciências E Educação, 10(12), 14–25. https://doi.org/10.51891/rease.v10i12.17209

AGÊNCIA BRASIL. Brasil tem 546 mil médicos; proporção é de 2,56 por mil habitantes. 2023. Disponível em: https://agenciabrasil.ebc.com.br/saude/noticia/2023-02/brasil-tem-546-mil-medicos-proporcao-e-de-256-por-mil-habitantes. Acesso em: 9 Mar. 2025.

GOVERNO FEDERAL. Acessar a plataforma móvel de serviços digitais do Ministério da Saúde. 2023. Disponível em: https://www.gov.br/pt-br/servicos/acessar-a-plataforma-movel-de-servicos-digitais-do-ministerio-da-saude. Acesso em: 10 Mar. 2025.

PFIZER. Diagnóstico precoce do câncer. 2023. Disponível em: https://www.pfizer.com.br/noticias/ultimas-noticias/diagnostico-precoce-do-cancer. Acesso em: 10 Mar. 2025.

WORLD BANK. Physicians (per 1,000 people). 2023. Disponível em: https://data.worldbank.org/indicator/SH.MED.PHYS.ZS. Acesso em: 10 Mar. 2025.

Bradski, G. (2000). The OpenCV Library. Dr. Dobb's Journal of Software Tools. Site oficial OpenCV: https://opencv.org/ Acesso em: 25 Mar. 2025.

---

### ANEXOS

**ANEXO A - CÓDIGOS**  
Backend-notebook [GitHub]:  
https://github.com/samyhad/skin_cancer_detection  

Aplicação web [GitHub]:  
https://github.com/lorenypsum/medivisao  

---

**ANEXO B - ENTREVISTAS**

As entrevistas foram conduzidas com diversos profissionais da saúde, estudantes e pessoas com experiências pessoais relacionadas ao diagnóstico médico por imagem. As transcrições completas incluem:

- Relatos de técnicos, fonoaudiólogos, estudantes de medicina, enfermeiros, comerciantes e fisioterapeutas;
- Reflexões sobre limitações dos exames de imagem atuais;
- Desejos e sugestões para melhorias usando processamento digital de imagens;
- Experiências pessoais com atrasos em diagnósticos ou diagnósticos incorretos;
- Opiniões sobre como sistemas baseados em IA podem auxiliar no diagnóstico clínico.

Entrevistas completas e formulários estão disponíveis em:
- https://forms.gle/pRwvaDLkLydE2MW5A
- https://forms.gle/mnGGj2gRTx1yFqAEA

As entrevistas reforçam a importância da proposta do projeto, evidenciando sua aplicabilidade e potencial impacto social.

---
