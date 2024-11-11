# SD-PrioridadeThreadsJava

## Descrição da Atividade

Este repositório contém uma atividade prática sobre o uso de threads em Java com diferentes níveis de prioridade. A atividade foi realizada no contexto da disciplina de Sistemas Distribuídos, e o objetivo é observar o comportamento de threads de alta e baixa prioridade durante a execução concorrente.

### Arquivos no Repositório

- **LancadorPrioridade.java**: Arquivo Java que implementa duas threads, uma de alta prioridade e outra de baixa prioridade, e as executa simultaneamente para analisar o comportamento concorrente.

## Instruções para Compilar e Executar

### 1. Clonar o Repositório

Primeiro, clone este repositório localmente:
```bash
git clone https://github.com/Josmarm4/SD-PrioridadeThreadsJava.git
```

### 2. Executar o Programa

Após compilar, execute o programa e redirecione a saída para um arquivo de log com timestamp, para facilitar a análise posterior:

```bash
java LancadorPrioridade > LancadorPrioridade_$(date +%Y%m%d_%H%M%S).log &
```

### Análise da Execução
O programa inicia duas threads:
* Thread de baixa prioridade: Configurada com `Thread.MIN_PRIORITY` (prioridade mínima), esta thread imprime repetidamente a mensagem  `Thread de baixa prioridade executando -> 1`.

* Thread de alta prioridade: Configurada com `Thread.MAX_PRIORITY` (prioridade máxima), esta thread imprime cinco vezes a mensagem `Thread de alta prioridade executando -> 10`, seguida por uma pausa de 10 milissegundos.

### Observações
Na prática, a thread de alta prioridade tende a ser executada mais frequentemente. No entanto, é importante notar que o escalonador de threads do sistema operacional, em conjunto com a JVM, pode tomar decisões diferentes a cada execução. Isso significa que o comportamento exato pode variar entre execuções, e a thread de baixa prioridade ainda pode ser executada ocasionalmente.

### Uso do ShutdownHook
Para garantir que as threads sejam finalizadas corretamente, foi adicionado um `ShutdownHook` ao programa. Esse gancho intercepta o encerramento do programa e interrompe as duas threads de forma controlada. Essa abordagem é especialmente útil em ambientes de concorrência para evitar que as threads continuem rodando indefinidamente após o término da execução principal.

### Exemplo de Saída
Um exemplo de saída será parecido com:
```bash
Thread de baixa prioridade executando -> 1
Thread de alta prioridade executando -> 10
Thread de alta prioridade executando -> 10
Thread de baixa prioridade executando -> 1
```

### Conclusão
Este projeto ajuda a entender como o escalonador de threads em Java lida com prioridades. Embora a definição de prioridade ajude o sistema a determinar a ordem de execução, o comportamento real depende de muitos fatores, como o sistema operacional e a carga atual da CPU.