# Task-Management-
An extended version of the To-Do-List App class with the methods for adding, viewing, marking as completed, and removing tasks. This example uses a simple text-based menu system to interact with the user.
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.Scanner;

class Task implements Serializable {
    private String title;
    private String description;
    private String dueDate;
    private int priority;
    private boolean completed;
public Task(String title, String description, String dueDate, int priority) {
        this.title = title;
        this.description = description;
        this.dueDate = dueDate;
        this.priority = priority;
        this.completed = false;
    }
  public void setCompleted(boolean completed) {
        this.completed = completed;
    }
}
public class ToDoListApp {
    private List<Task> taskList;
    private Scanner scanner;
    private static final String FILE_PATH = "tasks.dat";
public ToDoListApp() {
        taskList = loadTasksFromFile();
        scanner = new Scanner(System.in);
    }
private List<Task> loadTasksFromFile() {
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream(FILE_PATH))) {
            return (List<Task>) ois.readObject();
        } catch (IOException | ClassNotFoundException e) {
            return new ArrayList<>();
        }
    }
private void saveTasksToFile() {
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(FILE_PATH))) {
            oos.writeObject(taskList);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
private void addTask() {
    }
private void viewTasks() {
    
    }

    private void markTaskAsCompleted() {
    }

    private void removeTask() 
    }

    public static void main(String[] args) {
        ToDoListApp toDoListApp = new ToDoListApp();
        toDoListApp.showMenu();
    }

    public void showMenu() {
        int choice;
        do {
            System.out.println("\n----- ToDo List Menu -----");
            System.out.println("1. Add Task");
            System.out.println("2. View Tasks");
            System.out.println("3. Mark Task as Completed");
            System.out.println("4. Remove Task");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            choice = scanner.nextInt();
            scanner.nextLine(); // Consume the newline character

            switch (choice) {
                case 1:
                    addTask();
                    break;
                case 2:
                    viewTasks();
                    break;
                case 3:
                    markTaskAsCompleted();
                    break;
                case 4:
                    removeTask();
                    break;
                case 5:
                    saveTasksToFile();
                    System.out.println("Exiting ToDo List App. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 5);
    }

    private void addTask() {
        System.out.print("Enter task title: ");
        String title = scanner.nextLine();

        System.out.print("Enter task description: ");
        String description = scanner.nextLine();

        System.out.print("Enter task due date: ");
        String dueDate = scanner.nextLine();

        System.out.print("Enter task priority (1 - Low, 2 - Medium, 3 - High): ");
        int priority = scanner.nextInt();

        Task newTask = new Task(title, description, dueDate, priority);
        taskList.add(newTask);
        System.out.println("Task added successfully!");
    }

    private void viewTasks() {
        if (taskList.isEmpty()) {
            System.out.println("No tasks available.");
            return;
        }

        System.out.println("\n----- Task List -----");
        for (int i = 0; i < taskList.size(); i++) {
            Task task = taskList.get(i);
            System.out.printf("%d. %s - %s (Due: %s, Priority: %d, Completed: %s)%n",
                    i + 1, task.getTitle(), task.getDescription(), task.getDueDate(),
                    task.getPriority(), task.isCompleted() ? "Yes" : "No");
        }
    }

    private void markTaskAsCompleted() {
        viewTasks();

        if (taskList.isEmpty()) {
            return;
        }

        System.out.print("Enter the number of the task to mark as completed: ");
        int taskNumber = scanner.nextInt();
if (taskNumber >= 1 && taskNumber <= taskList.size()) {
            Task selectedTask = taskList.get(taskNumber - 1);
            selectedTask.setCompleted(true);
            System.out.println("Task marked as completed!");
        } else {
            System.out.println("Invalid task number. Please try again.");
        }
    }
    private void removeTask() {
        viewTasks();
if (taskList.isEmpty()) {
            return;
        }
        System.out.print("Enter the number of the task to remove: ");
        int taskNumber = scanner.nextInt();
if (taskNumber >= 1 && taskNumber <= taskList.size()) {
            taskList.remove(taskNumber - 1);
            System.out.println("Task removed successfully!");
        } else {
            System.out.println("Invalid task number. Please try again.");
        }
    }
}
