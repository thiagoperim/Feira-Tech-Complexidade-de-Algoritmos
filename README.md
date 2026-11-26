# Desarme a Bomba — Complexidade de Algoritmos

Jogo educacional offline do Grupo 1: Alice, Gustavo, Tiago, Thales H. e Eric.

## Executar

Abra `index.html` diretamente no Chrome ou Edge, inclusive sem internet. No VS Code, abra a pasta do projeto e pressione **F5** para iniciar no Chrome. O Live Server também funciona, mas não é necessário. Não há instalação, servidor ou bibliotecas externas obrigatórios.

## Jogar

Clique em **Começar missão**, leia a mensagem e escolha a estratégia correspondente. As modalidades se alternam a cada rodada:

- **Chute Certeiro — Acesso Direto O(1):** 16 códigos e 20 segundos. Resolva a charada para descobrir a posição. Ela só aparece quando o cronômetro começa.
- **Varredura — Busca Sequencial O(n):** 24 códigos embaralhados e 45 segundos. Uma tentativa incorreta descarta somente o código escolhido.
- **Dividir ao Meio — Busca Binária O(log n):** 32 códigos ordenados e 40 segundos. Uma tentativa informa se a senha é maior ou menor e descarta os códigos impossíveis. A escolha de qualquer código disponível é livre.

Clique em um código e em **Confirmar senha**. **Pedir dica** fornece até três dicas estratégicas por rodada; **Ajuda com controles** explica a interface sem consumir dicas. A senha é definida no início da rodada e permanece fixa.

O modo guiado apresenta um tutorial visual dos controles na primeira missão. O cronômetro permanece parado até o jogador terminar a apresentação da lista. **Pular tutorial** dispensa as explicações; **Rever tutorial** inicia outra rodada com a orientação; **Novo visitante** volta às boas-vindas e restaura o tutorial. **Jogar novamente** alterna a modalidade sem repetir a introdução. O modo desafio pula o tutorial inicial.

- **1** escolhe Chute Certeiro; **2** escolhe Dividir ao Meio; **3** escolhe Varredura. Depois da escolha, essas teclas digitam números normalmente.
- **0–9** digitam a senha; **Backspace** apaga o último dígito; **Enter ou espaço** confirma. Use **Digitar código manualmente** para abrir o teclado virtual.
- **Esc** ou **Reiniciar** iniciam outra rodada; **F11** ou **Tela cheia** ampliam a experiência. O botão de som controla os efeitos da Web Audio API.

## Configuração e conceitos

HTML, CSS e JavaScript estão integrados em um único arquivo. O objeto `CONFIG` no início do JavaScript contém `count` e `seconds` para cada modalidade. Para usar a proposta original, altere os três pares para `count: 16, seconds: 60`. O cronômetro usa `performance.now()` e um prazo absoluto; o reinício não recarrega a página.

No **acesso direto**, o código é acessado por `codes[targetIndex]` em O(1), depois que a posição é conhecida. Resolver a charada é uma etapa separada e seu custo não está incluído nesse acesso. A **busca sequencial** convencional verifica elementos individualmente, em O(n), podendo fazer até 10.000 comparações em uma lista desse tamanho.

Na modalidade de comparação ordenada, o visitante pode escolher qualquer código ativo; a eliminação corresponde à escolha real. Isso não necessariamente é uma busca binária. A **busca binária convencional** compara sempre o centro, em O(log n), e pressupõe dados ordenados; o custo da ordenação não está incluído. Em uma lista não vazia, o máximo é `Math.floor(Math.log2(n)) + 1`: 14 para 10.000 elementos. A tela final compara as tentativas com uma simulação convencional para a mesma senha e não aplica esse limite aos palpites livres.
