# DS Java Module 09 – Merged Exercises

This file combines Exercises 16–20 from the repository. Each exercise includes its objective, algorithm, Java implementation, and result.

---

## Ex16 – Check for Balanced Parentheses Using Stack

### Aim
Write a Java program that verifies whether parentheses (`(`, `{`, `[`) in an input string are balanced and correctly ordered.

### Algorithm
1. Read an input expression.
2. Create a stack for opening brackets.
3. Push every opening bracket onto the stack.
4. For each closing bracket, check that the stack is not empty and that its top matches.
5. After processing the expression, the stack must be empty for the expression to be balanced.

### Program

```java
import java.util.Scanner;

public class ParenChecker {
    static class ArrayStack {
        private final char[] data;
        private int top;

        ArrayStack(int capacity) {
            data = new char[Math.max(capacity, 1)];
            top = -1;
        }

        boolean isEmpty() {
            return top == -1;
        }

        void push(char value) {
            data[++top] = value;
        }

        char pop() {
            return data[top--];
        }
    }

    public static boolean isBalanced(String expression) {
        ArrayStack stack = new ArrayStack(expression.length());

        for (char character : expression.toCharArray()) {
            if (character == '(' || character == '{' || character == '[') {
                stack.push(character);
            } else if (character == ')' || character == '}' || character == ']') {
                if (stack.isEmpty()) {
                    return false;
                }

                char opening = stack.pop();
                if ((character == ')' && opening != '(')
                        || (character == '}' && opening != '{')
                        || (character == ']' && opening != '[')) {
                    return false;
                }
            }
        }

        return stack.isEmpty();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String expression = scanner.nextLine();
        System.out.println(isBalanced(expression));
        scanner.close();
    }
}
```

### Result
The program successfully checks whether an input expression contains balanced parentheses using a stack.

---

## Ex17 – Reverse a String Using a Stack

### Aim
Reverse an input string using a stack without using a built-in reverse function.

### Algorithm
1. Read the input string.
2. Push each character onto a stack.
3. Pop the characters one by one and append them to a result.
4. Display the reversed string.

### Program

```java
import java.util.Scanner;
import java.util.Stack;

public class ReverseStringWithStack {
    public static String reverseString(String input) {
        Stack<Character> stack = new Stack<>();

        for (char character : input.toCharArray()) {
            stack.push(character);
        }

        StringBuilder reversed = new StringBuilder();
        while (!stack.isEmpty()) {
            reversed.append(stack.pop());
        }

        return reversed.toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = scanner.nextLine();
        System.out.println(reverseString(input));
        scanner.close();
    }
}
```

### Result
The program successfully reverses the given string using a stack.

---

## Ex18 – Simulate a Ticket Counter Using a Queue

### Aim
Simulate a ticket counter operating on a First-In-First-Out (FIFO) basis using a linked-list queue.

### Algorithm
1. Create an empty linked-list queue.
2. Add customers using `enqueue`.
3. Remove customers using `dequeue` in arrival order.
4. Display the current queue using `display`.
5. Continue processing commands until `exit` is entered.

### Program

```java
import java.util.Scanner;

class Node {
    String customerName;
    Node next;

    Node(String customerName) {
        this.customerName = customerName;
    }
}

class TicketQueue {
    private Node front;
    private Node rear;

    public void enqueue(String customerName) {
        Node newNode = new Node(customerName);
        if (rear == null) {
            front = rear = newNode;
            return;
        }

        rear.next = newNode;
        rear = newNode;
    }

    public void dequeue() {
        if (front == null) {
            System.out.println("Queue is empty. No customer to serve.");
            return;
        }

        System.out.println("Serving customer: " + front.customerName);
        front = front.next;
        if (front == null) {
            rear = null;
        }
    }

    public void displayQueue() {
        if (front == null) {
            System.out.println("Queue is empty.");
            return;
        }

        System.out.print("Queue: ");
        for (Node current = front; current != null; current = current.next) {
            System.out.print(current.customerName);
            if (current.next != null) {
                System.out.print(" -> ");
            }
        }
        System.out.println();
    }
}

public class TicketCounter {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        TicketQueue queue = new TicketQueue();

        while (scanner.hasNextLine()) {
            String command = scanner.nextLine().trim();
            if (command.isEmpty()) {
                continue;
            }

            String[] parts = command.split("\\s+", 2);
            switch (parts[0]) {
                case "enqueue":
                    if (parts.length == 2 && !parts[1].isBlank()) {
                        queue.enqueue(parts[1]);
                    } else {
                        System.out.println("Please provide a customer name.");
                    }
                    break;
                case "dequeue":
                    queue.dequeue();
                    break;
                case "display":
                    queue.displayQueue();
                    break;
                case "exit":
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid command.");
            }
        }

        scanner.close();
    }
}
```

### Result
The program successfully simulates a ticket counter in FIFO order using a linked-list queue.

---

## Ex19 – Check a Palindrome Using a Deque

### Aim
Determine whether a message is a palindrome after removing non-alphanumeric characters and converting the text to lowercase.

### Algorithm
1. Normalize the input by removing non-alphanumeric characters and converting it to lowercase.
2. Insert each character into a deque.
3. Remove and compare characters from the front and rear.
4. If every pair matches, the message is a palindrome.

### Program

```java
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.Scanner;

public class PalindromeChecker {
    public static boolean isPalindrome(String message) {
        String cleaned = message.toLowerCase().replaceAll("[^a-z0-9]", "");
        Deque<Character> deque = new ArrayDeque<>();

        for (char character : cleaned.toCharArray()) {
            deque.addLast(character);
        }

        while (deque.size() > 1) {
            if (!deque.pollFirst().equals(deque.pollLast())) {
                return false;
            }
        }

        return true;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = scanner.nextLine();
        System.out.println(isPalindrome(input) ? "Palindrome" : "Not a palindrome");
        scanner.close();
    }
}
```

### Result
The program successfully checks whether the normalized message is a palindrome by comparing both ends of a deque.

---

## Ex20 – Sort an Array Using Merge Sort

### Aim
Sort an integer array in ascending order without using a built-in sorting function, using the merge sort algorithm with `O(n log n)` time complexity.

### Algorithm
1. Recursively divide the array into two halves until each part contains one element.
2. Merge adjacent sorted parts.
3. Copy the merged values back into the original array.
4. Display the sorted array.

### Program

```java
import java.util.Arrays;
import java.util.Scanner;

public class MergeSort {
    private static void mergeSort(int[] array, int left, int right) {
        if (left >= right) {
            return;
        }

        int middle = left + (right - left) / 2;
        mergeSort(array, left, middle);
        mergeSort(array, middle + 1, right);
        merge(array, left, middle, right);
    }

    private static void merge(int[] array, int left, int middle, int right) {
        int[] temporary = new int[right - left + 1];
        int first = left;
        int second = middle + 1;
        int index = 0;

        while (first <= middle && second <= right) {
            if (array[first] <= array[second]) {
                temporary[index++] = array[first++];
            } else {
                temporary[index++] = array[second++];
            }
        }

        while (first <= middle) {
            temporary[index++] = array[first++];
        }
        while (second <= right) {
            temporary[index++] = array[second++];
        }

        System.arraycopy(temporary, 0, array, left, temporary.length);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int count = scanner.nextInt();
        int[] numbers = new int[count];

        for (int index = 0; index < count; index++) {
            numbers[index] = scanner.nextInt();
        }

        mergeSort(numbers, 0, numbers.length - 1);
        System.out.println("Sorted array:");
        System.out.println(Arrays.toString(numbers));
        scanner.close();
    }
}
```

### Result
The program successfully sorts the array in ascending order using merge sort with `O(n log n)` time complexity.

---

## Summary

| Exercise | Data structure or algorithm |
|---|---|
| Ex16 | Stack – balanced parentheses |
| Ex17 | Stack – string reversal |
| Ex18 | Linked-list queue – ticket counter |
| Ex19 | Deque – palindrome checking |
| Ex20 | Merge sort – array sorting |
