
# Métodos `join()` e `sleep()` da Classe `Thread` em Java

Este documento aborda os métodos `join()` e `sleep()` da classe `Thread` no Java, explicando seus usos, exemplos práticos e diferenças principais.

---

## O que é a classe `Thread`?

A classe `Thread` faz parte do pacote `java.lang` e é utilizada para criar e controlar threads em aplicações Java. Threads permitem a execução paralela de tarefas, o que é essencial para aplicações que exigem desempenho e eficiência.

---

## Método `join()`

O método `join()` é usado para aguardar a conclusão de uma thread antes de prosseguir com a execução do programa. Ele é especialmente útil para coordenar a execução de múltiplas threads.

### Assinatura:
```java
public final void join() throws InterruptedException
```

### Sobrecargas:
- `join(long millis)`
- `join(long millis, int nanos)`

### Funcionalidade:
- Faz a thread atual aguardar até que a thread chamada termine.
- Evita a execução desordenada de tarefas dependentes.

### Exemplo:
```java
class MinhaThread extends Thread {
    public void run() {
        System.out.println("Thread iniciada.");
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            System.out.println("Thread interrompida.");
        }
        System.out.println("Thread finalizada.");
    }
}

public class ExemploJoin {
    public static void main(String[] args) {
        MinhaThread thread = new MinhaThread();
        thread.start();
        try {
            thread.join();
        } catch (InterruptedException e) {
            System.out.println("Erro: " + e.getMessage());
        }
        System.out.println("Execução principal finalizada.");
    }
}
```

---

## Método `sleep()`

O método `sleep()` é utilizado para pausar a execução de uma thread por um período especificado. Isso é útil para controlar o tempo de execução de tarefas.

### Assinatura:
```java
public static void sleep(long millis) throws InterruptedException
```

### Sobrecarga:
- `sleep(long millis, int nanos)`

### Funcionalidade:
- Pausa a execução da thread atual.
- Não libera os bloqueios adquiridos pela thread.

### Exemplo:
```java
class MinhaThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Contagem: " + i);
            try {
                Thread.sleep(1000); // Pausa de 1 segundo
            } catch (InterruptedException e) {
                System.out.println("Thread interrompida.");
            }
        }
    }
}

public class ExemploSleep {
    public static void main(String[] args) {
        MinhaThread thread = new MinhaThread();
        thread.start();
    }
}
```

---

## Diferenças entre `join()` e `sleep()`

| **Aspecto**          | **`join()`**                                           | **`sleep()`**                       |
|-----------------------|-------------------------------------------------------|--------------------------------------|
| **Propósito**         | Aguarda outra thread terminar antes de continuar      | Pausa a execução da thread atual    |
| **Ação na Thread**    | A thread atual é bloqueada até que outra finalize     | Apenas suspende temporariamente     |
| **Tipo de Método**    | Chamado em uma instância de `Thread`                  | Método estático                     |
| **Exceções**          | Lança `InterruptedException`                         | Lança `InterruptedException`        |

---

## Conclusão

Os métodos `join()` e `sleep()` são fundamentais para o controle de threads no Java. Enquanto `join()` ajuda a sincronizar threads, `sleep()` permite criar pausas controladas na execução. Ambos são ferramentas indispensáveis para o desenvolvimento de programas multithreaded eficientes.

---

## Referências

- Documentação oficial do Java: [Thread](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html)
- Exemplos práticos: [Oracle Java Tutorials](https://docs.oracle.com/javase/tutorial/essential/concurrency/)
- Material da disciplina - [ELC117](https://github.com/andreaInfUFSM/elc117-2024b)

---

**By:** Pedro Henrique Abreu
