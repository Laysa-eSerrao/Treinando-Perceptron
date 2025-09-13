# Relatório do Perceptron

1. Variação da taxa de aprendizado (learning_rate)
Taxa pequena (ex.: 0.01): O treinamento converge mais devagar, exigindo mais épocas para ajustar os pesos. O perceptron ainda aprende, mas demora mais a alcançar boas previsões.
Taxa maior (ex.: 0.5 ou 1.0): A convergência tende a ser mais rápida, porém pode oscilar bastante e dificultar a estabilização dos pesos, podendo até não convergir em alguns casos.
Conclusão: É preciso um equilíbrio; a taxa de 0.1 usada no exemplo é adequada, pois garante aprendizagem estável sem oscilações excessivas.

2. Variação do número de épocas (epochs)
Poucas épocas (ex.: 10): O treinamento pode parar antes de ajustar os pesos corretamente, resultando em previsões incorretas.
Muitas épocas (ex.: 1000): O modelo converge com segurança, mas há risco de “overfitting” em problemas maiores. No caso das portas lógicas (problemas simples), funciona bem e garante bons resultados.
Conclusão: Para o problema apresentado, entre 100 e 200 épocas já é suficiente para atingir convergência.

3. Teste com a porta AND

Alterando os outputs para a porta lógica AND:

inputs = [[0,0], [0,1], [1,0], [1,1]]
outputs = [[0], [0], [0], [1]]

Resultados esperados:
0 AND 0 = 0
0 AND 1 = 0
1 AND 0 = 0
1 AND 1 = 1

O perceptron consegue aprender a função AND corretamente após treinamento.

4. Extração da função de ativação

O código aplica a função sigmoide diretamente dentro do método. Criando um método separado:

def sigmoid(self, x):
    return 1 / (1 + np.exp(-x))

E no restante do código chamamos self.sigmoid(...). Isso melhora a clareza e facilita futuras trocas de função de ativação.

5. Troca da função de ativação para DEGRAU

Implementação:

def step(self, x):
    return 1 if x > 0 else 0

Impacto: O perceptron continua aprendendo funções linearmente separáveis (como AND e OR).
A diferença é que a saída será exatamente 0 ou 1, sem valores intermediários como na sigmoide.
Para problemas simples como portas lógicas, a função degrau é suficiente e até mais direta.

6. Três entradas (Opcional)

Podemos ampliar 3 entradas adicionando um peso extra (w3) e adaptando inputs e outputs.
Exemplo:
inputs = [[0,0,0], [0,0,1], [0,1,0], [1,0,0], [1,1,1]]

E o cálculo passa a ser:

sigmoid = 1 / (1 + np.exp(-(w1*x1 + w2*x2 + w3*x3 + bias)))

Com isso, o perceptron consegue aprender funções lógicas que dependam de três variáveis.

Conclusões
A taxa de aprendizado e o número de épocas influenciam diretamente na velocidade e estabilidade do treinamento.
O perceptron é capaz de aprender portas lógicas lineares (AND e OR), mas não aprende funções não lineares como XOR.
Alterar a função de ativação (sigmoide → degrau) não afeta a qualidade no caso das portas lógicas, apenas muda a forma da saída.
O código pode ser facilmente estendido para mais entradas.
