## Lista Circular em Python (Trens e Vagões)

**Abstract.** The objective of this project is to provide a solution for a particular investigation into circular lists in Data Structures 2, using the knowledge acquired in classes and innovative problem-solving techniques. Using the complementary materials offered by professor Juliano Ratusznei, it is possible to understand the essential components of the task, divide it into manageable parts and, finally, reach a coherent resolution that satisfies the problem at hand.

**Resumo.** O objetivo deste projeto é fornecer uma solução para uma investigação particular sobre listas circulares em Estruturas de Dados 2, utilizando os conhecimentos adquiridos nas aulas e técnicas inovadoras de resolução de problemas. Utilizando os materiais complementares oferecidos pelo professor Juliano Ratusznei, é possível compreender os componentes essenciais da tarefa, dividi-la em partes gerenciáveis e, por fim, chegar a uma resolução coerente que satisfaça o problema em questão.

## Descrição do exercício a ser solucionado:
### Implemente uma lista circular com identificador da composição de trens do metrô a qual tenha as seguintes características:
Alocação de memória dinâmica para os vagões inseridos.<br/>
Uma função de busca de vagões por trem.<br/>
Contagem da quantidade de vagões presentes na composição.<br/>
Remoção de vagões.<br/>
Adição de vagões.<br/>
O último vagão deve permitir a acoplagem de máquinas ou vagões.

## Resolução do exercício - Codificação:

```
# Definindo a classe Vagao para representar um vagão individual
class Vagao:
    def __init__(self, numero):
        self.numero = numero
        self.proximo = None
# Definindo a classe ComposicaoTrem para representar a composição de trens
class ComposicaoTrem:
    def __init__(self):
        self.primeiro = None # Ponteiro para o primeiro vagão na composição
        self.ultimo = None # Ponteiro para o último vagão na composição
        self.tamanho = 0 # Armazena a quantidade de vagões na composição

    # Função para adicionar um vagão à composição
    def adicionar_vagao(self, numero):
        novo_vagao = Vagao(numero) # Cria um novo vagão com o número especificado
        if not self.primeiro:
            self.primeiro = novo_vagao
            self.ultimo = novo_vagao
        else:
            self.ultimo.proximo = novo_vagao
            novo_vagao.proximo = self.primeiro # Tornando a lista circular
            self.ultimo = novo_vagao
            self.tamanho += 1 # Incrementando a contagem de vagões

    # Função para remover um vagão da composição
    def remover_vagao(self, numero):
        if not self.primeiro:
            print("A composição está vazia.")
            return
        if self.primeiro.numero == numero:
            if self.primeiro == self.ultimo:
                self.primeiro = None
                self.ultimo = None
            else:
                self.primeiro = self.primeiro.proximo
                self.ultimo.proximo = self.primeiro
            self.tamanho -= 1
            print(f"Vagão {numero} removido com sucesso.")
            return
        
        vagao_anterior = self.primeiro
        vagao_atual = self.primeiro.proximo
    
        while vagao_atual != self.primeiro:
            if vagao_atual.numero == numero:
                vagao_anterior.proximo = vagao_atual.proximo
                self.tamanho -= 1
                print(f"Vagão {numero} removido com sucesso.")
                return
            vagao_anterior = vagao_atual
            vagao_atual = vagao_atual.proximo
        print(f"Vagão {numero} não encontrado na composição.")

    # Função para buscar vagoes por trem
    def buscar_vagoes_por_trem(self, numero_trem):
        if not self.primeiro:
            print("A composição está vazia.")
            return
        
        vagoes_encontrados = []
        vagao_atual = self.primeiro
        while True:
            if vagao_atual.numero // 100 == numero_trem:
                vagoes_encontrados.append(vagao_atual.numero)
                vagao_atual = vagao_atual.proximo
                if vagao_atual == self.primeiro:
                    break

        if not vagoes_encontrados:
            print(f"Nenhum vagão encontrado para o trem {numero_trem}.")
        else:
            print(f"Vagoes do trem {numero_trem}: {', '.join(map(str, vagoes_encontrados))}")
 
    # Função para contar a quantidade de vagões na composição
    def contar_vagoes(self):
        return self.tamanho
 
    # Função para acoplar uma máquina ou vagão (adiciona um vagão ao final da composição)
    def acoplar_maq_vagao(self, numero_maq_vagao):
        self.adicionar_vagao(numero_maq_vagao)
 
    # Representação em string da composição de trens
    def __str__(self):
        if not self.primeiro:
            return "A composição está vazia."
        composicao_str = []
        vagao_atual = self.primeiro
        
        while True:
            composicao_str.append(str(vagao_atual.numero))
            vagao_atual = vagao_atual.proximo
            if vagao_atual == self.primeiro:
                break
 
        return " -> ".join(composicao_str)

# Exemplo de uso interativo com input do usuário:
composicao = ComposicaoTrem()
while True:
    print("\nOpções:")
    print("1. Adicionar vagão")
    print("2. Remover vagão")
    print("3. Buscar vagoes por trem")
    print("4. Contar vagoes")
    print("5. Acoplar máquina/vagão")
    print("6. Exibir composição")
    print("7. Sair")
    escolha = input("Escolha uma opção: ")
    if escolha == '1':
        numero_vagao = int(input("Digite o número do vagão a ser adicionado: "))
        composicao.adicionar_vagao(numero_vagao)
    elif escolha == '2':
        numero_vagao = int(input("Digite o número do vagão a ser removido: "))
        composicao.remover_vagao(numero_vagao)
    elif escolha == '3':
        numero_trem = int(input("Digite o número do trem para buscar vagoes: "))
        composicao.buscar_vagoes_por_trem(numero_trem)
    elif escolha == '4':
        print(f"Quantidade de vagoes na composição: {composicao.contar_vagoes()}")
    elif escolha == '5':
        numero_maq_vagao = int(input("Digite o número da máquina/vagão a ser acoplado: "))
        composicao.acoplar_maq_vagao(numero_maq_vagao)
    elif escolha == '6':
        print("Composição de trens:")
        print(composicao)
    elif escolha == '7':
        break
    else:
        print("Opção inválida. Tente novamente.")
```

## Execução do exercício - Resolução
Figura 1: tela da solução do exercício – adicionando vagões (15, 20 e 30).
<img src="/src/img1.png"><br/><br/>
Figura 2: tela da solução do exercício – removendo vagões (20).
<img src="/src/img2.png"><br/><br/>
Figura 3: tela da solução do exercício – buscando vagões (30 e 15).
<img src="/src/img3.png"><br/><br/>
Figura 4: tela da solução do exercício – contando vagões (2).
<img src="/src/img4.png"><br/><br/>
Figura 5: tela da solução do exercício – acoplando máquinas/vagões à composição (0).
<img src="/src/img5.png"><br/><br/>
Figura 6: tela da solução do exercício – exibindo a composição (15, 30 e 0).
<img src="/src/img7.png"><br/><br/>
