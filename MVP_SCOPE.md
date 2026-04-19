# Sidereus — Escopo do MVP

## 1) Objetivo do produto
Entregar uma aplicação web com visualização **3D interativa do Sistema Solar** que permita ao usuário:
- navegar pela cena;
- identificar os principais corpos celestes;
- consultar informações básicas de cada corpo;
- alternar modos visuais essenciais para exploração educativa.

O foco do MVP é **experiência de exploração inicial**, e não precisão científica avançada ou simulação orbital completa em tempo real.

---

## 2) Problema que o MVP resolve
Hoje, boa parte dos conteúdos sobre o Sistema Solar é estática (imagens e textos). O MVP do Sidereus propõe uma experiência visual e interativa que facilite:
- entendimento espacial (escala relativa simplificada);
- curiosidade e aprendizado introdutório;
- engajamento por exploração livre.

---

## 3) Público-alvo
- Estudantes (ensino fundamental/médio) em contexto introdutório de astronomia.
- Professores que precisam de recurso visual rápido para aula.
- Entusiastas de espaço que buscam uma experiência exploratória leve no navegador.

---

## 4) Escopo funcional do MVP (IN)

### 4.1 Cena 3D base
- Renderizar Sol + 8 planetas (Mercúrio a Netuno).
- Fundo espacial simples (skybox/estrelas).
- Iluminação básica suficiente para distinguir os corpos.

### 4.2 Interação
- Controle de câmera (orbitar, zoom, pan).
- Seleção de planeta por clique.
- Foco da câmera no corpo selecionado.

### 4.3 Informações contextuais
- Painel lateral/modal com dados básicos do corpo selecionado:
  - nome;
  - tipo (planeta rochoso/gasoso etc.);
  - distância média ao Sol (aproximada);
  - raio/diâmetro aproximado;
  - período orbital aproximado.

### 4.4 Dinâmica visual mínima
- Movimento orbital simplificado (não precisa ser fisicamente preciso).
- Rotação própria simplificada (opcional por corpo, mas desejável para os principais).
- Controle global de velocidade da simulação (pausar/retomar e 2 velocidades).

### 4.5 UI essencial
- Tela inicial com CTA “Iniciar exploração”.
- HUD mínima com:
  - botão play/pause;
  - seletor de velocidade;
  - botão “Reset câmera”.

### 4.6 Qualidade mínima
- Aplicação responsiva para desktop e tablet.
- Performance alvo: 30+ FPS em desktop com configuração mínima de referência (CPU 4 núcleos, 8 GB RAM, GPU integrada equivalente a Intel Iris Xe/AMD Vega 8), em 1920x1080 com configurações visuais padrão.

---

## 5) Fora de escopo do MVP (OUT)
- Luas, asteroides, cometas e cinturões detalhados.
- Missões espaciais, satélites artificiais e trajetórias reais.
- Escalas físicas rigorosas (distâncias/tamanhos 1:1 inviáveis para UX inicial).
- Modo VR/AR.
- Multiplayer.
- Sistema avançado de contas/usuários.
- Internacionalização completa (MVP em um idioma principal).

---

## 6) Requisitos não funcionais
- Stack web moderna com renderização 3D no navegador (ex.: Three.js).
- Carregamento inicial objetivo: < 5s em rede 4G (aprox. 10 Mbps de download, 2 Mbps de upload e ~50 ms de latência), com otimização progressiva.
- Código organizado para permitir evolução posterior (ex.: adicionar luas e missões).
- Telemetria básica opcional para medir uso de interação (sem PII no MVP).

---

## 7) Critérios de aceite do MVP
1. Usuário consegue abrir a aplicação e entrar na cena 3D sem erros críticos.
2. Sol e 8 planetas aparecem e podem ser visualizados com controle de câmera.
3. Clique em planeta abre informações básicas corretas conforme dataset definido.
4. Play/pause e controle de velocidade afetam animação orbital.
5. Reset de câmera funciona consistentemente.
6. Interface permanece utilizável em desktop e tablet.

---

## 8) Métricas iniciais de sucesso
- Taxa de sessão com interação (clique em pelo menos 1 planeta) > 70%.
- Tempo médio de sessão > 2 minutos em testes internos.
- Pelo menos 80% dos testadores relatam clareza visual “boa” ou “muito boa”.

---

## 9) Riscos e mitigação
- **Risco:** performance ruim em dispositivos modestos.
  - **Mitigação:** LOD simples, texturas compactadas, limite de pós-processamento.
- **Risco:** excesso de escopo cedo.
  - **Mitigação:** seguir rigidamente IN/OUT do MVP.
- **Risco:** dados inconsistentes dos planetas.
  - **Mitigação:** dataset versionado e validado antes de integrar UI.

---

## 10) Lista de tarefas (sugestão de Issues)

### Epic 1 — Fundação do projeto
1. **Issue: Setup inicial do projeto 3D web**
   - Definir stack (Vite + Three.js ou equivalente).
   - Configurar lint/format e estrutura de pastas.
   - Critério de pronto: projeto sobe localmente com cena vazia.

2. **Issue: Pipeline de assets e texturas**
   - Estruturar diretório de texturas/modelos.
   - Definir convenção de nomes e compressão.
   - Critério de pronto: assets carregam via loader sem erros.

### Epic 2 — Cena e renderização
3. **Issue: Implementar cena base com Sol + 8 planetas**
   - Criar geometrias/material inicial para cada corpo.
   - Posicionar corpos em escala relativa simplificada.
   - Critério de pronto: todos os planetas visíveis na cena.

4. **Issue: Adicionar skybox/campo de estrelas**
   - Inserir background espacial leve.
   - Critério de pronto: cena com ambientação funcional e desempenho aceitável.

5. **Issue: Iluminação principal da cena**
   - Configurar luz do Sol e iluminação ambiente de suporte.
   - Critério de pronto: contraste visual suficiente dos corpos.

### Epic 3 — Interação
6. **Issue: Controles de câmera (orbit/zoom/pan)**
   - Integrar OrbitControls (ou similar).
   - Definir limites de zoom e ângulos.
   - Critério de pronto: navegação estável sem clipping crítico.

7. **Issue: Seleção de planetas por raycasting**
   - Detectar clique em corpos celestes.
   - Destacar alvo selecionado.
   - Critério de pronto: seleção funciona em todos os planetas.

8. **Issue: Foco automático da câmera no planeta selecionado**
   - Implementar transição suave da câmera.
   - Critério de pronto: foco centraliza planeta e mantém navegação.

### Epic 4 — Dados e UI
9. **Issue: Criar dataset MVP dos planetas (JSON/TS)**
   - Consolidar dados básicos e unidades usadas.
   - Critério de pronto: dataset validado e versionado no repositório.

10. **Issue: Painel de informações do planeta selecionado**
    - Exibir nome, tipo, distância, raio e período orbital.
    - Critério de pronto: painel atualiza corretamente por seleção.

11. **Issue: HUD de controles globais da simulação**
    - Botões play/pause, velocidade e reset câmera.
    - Critério de pronto: controles acionam estado da simulação sem bug visível.

### Epic 5 — Simulação
12. **Issue: Movimento orbital simplificado**
    - Implementar órbitas circulares/elípticas simplificadas por planeta.
    - Critério de pronto: planetas orbitam continuamente com parâmetros distintos.

13. **Issue: Controle de tempo (pausa e velocidade)**
    - Implementar timeScale global.
    - Critério de pronto: animação responde imediatamente aos controles.

### Epic 6 — Qualidade
14. **Issue: Responsividade para desktop e tablet**
    - Ajustar layout do painel e HUD.
    - Critério de pronto: interface sem sobreposição crítica em breakpoints definidos.

15. **Issue: Otimização de performance do MVP**
    - Medir FPS e gargalos principais.
    - Aplicar otimizações básicas de render.
    - Critério de pronto: atingir meta mínima de fluidez em ambiente alvo.

16. **Issue: QA funcional + checklist de aceite do MVP**
    - Executar testes manuais com roteiro.
    - Registrar bugs e validar critérios de aceite.
    - Critério de pronto: checklist de aceite concluído.

---

## 11) Definição de pronto do MVP
O MVP é considerado pronto quando os critérios da seção 7 forem cumpridos e as issues críticas (1, 3, 6, 7, 9, 10, 11, 12, 13, 16) estiverem concluídas.
- **Criticidade (bloqueiam entrega do MVP):** itens que garantem o valor central de exploração 3D funcional com interação mínima completa (cena base, navegação essencial, seleção, dataset, painel, HUD, simulação de tempo/órbita e validação final de aceite).
- **Não críticas para aceite inicial (2, 4, 5, 8, 14, 15):** melhorias de fidelidade visual, profundidade de câmera, trajetórias orbitais, foco automático, responsividade avançada e otimização de performance; agregam qualidade, mas não impedem o objetivo principal do MVP descrito na seção 1.
