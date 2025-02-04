# Adicionar Tarefa: O usuário pode inserir uma nova tarefa com uma descrição.
# Listar Tarefas: Exibe todas as tarefas, indicando se estão concluídas ou não.
# Marcar como Concluída: Permite ao usuário marcar uma tarefa como concluída com base no seu número na lista.
# Sair: Finaliza a execução do programa.

# Gerenciador de Tarefas em Java

Este é um simples gerenciador de tarefas implementado em Java. Ele permite adicionar, listar e marcar tarefas como concluídas através do console.

## Código-fonte

```java
package teste1;

import java.util.ArrayList;
import java.util.Scanner;

public class TaskManager {

    // Classe interna para representar uma Tarefa
    static class Task {
        private String description;
        private boolean completed;

        public Task(String description) {
            this.description = description;
            this.completed = false; // Nova tarefa começa como não concluída
        }

        public void markAsCompleted() {
            this.completed = true;
        }

        @Override
        public String toString() {
            return (completed ? "[✔]" : "[ ]") + " " + description;
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<Task> tasks = new ArrayList<>();

        while (true) {
            System.out.println("\n=== Gerenciador de Tarefas ===");
            System.out.println("1. Adicionar Tarefa");
            System.out.println("2. Listar Tarefas");
            System.out.println("3. Marcar Tarefa como Concluída");
            System.out.println("4. Sair");
            System.out.print("Escolha uma opção: ");

            int option = scanner.nextInt();
            scanner.nextLine(); // Limpar o buffer do scanner

            switch (option) {
                case 1:
                    System.out.print("Digite a descrição da tarefa: ");
                    String description = scanner.nextLine();
                    tasks.add(new Task(description));
                    System.out.println("Tarefa adicionada com sucesso!");
                    break;
                case 2:
                    System.out.println("\n=== Lista de Tarefas ===");
                    if (tasks.isEmpty()) {
                        System.out.println("Nenhuma tarefa adicionada ainda.");
                    } else {
                        for (int i = 0; i < tasks.size(); i++) {
                            System.out.println((i + 1) + ". " + tasks.get(i));
                        }
                    }
                    break;
                case 3:
                    System.out.print("Digite o número da tarefa que deseja marcar como concluída: ");
                    int taskNumber = scanner.nextInt();
                    if (taskNumber > 0 && taskNumber <= tasks.size()) {
                        tasks.get(taskNumber - 1).markAsCompleted();
                        System.out.println("Tarefa marcada como concluída!");
                    } else {
                        System.out.println("Número inválido.");
                    }
                    break;
                case 4:
                    System.out.println("Encerrando o Gerenciador de Tarefas. Até mais!");
                    scanner.close();
                    return;
                default:
                    System.out.println("Opção inválida. Tente novamente.");
            }
        }
    }
}
