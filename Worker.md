public class Main {
    public static void main(String[] args) {
        System.out.println("Домашнее задание к занятию 1.1: " +
                "Лямбда-выражения и функциональные интерфейсы\n" +
                "Задача 2: Работяга\n");

        OnTaskDoneListener listener = System.out::println;
        OnTaskErrorListener listenerE = System.out::println;

        Worker worker = new Worker(listener, listenerE);
        worker.start(33);

    }

}

public class Worker {

    private OnTaskDoneListener callback;
    private OnTaskErrorListener errorCallback;

    public Worker(OnTaskDoneListener callback, OnTaskErrorListener errorCallback) {
        this.callback = callback;
        this.errorCallback = errorCallback;
    }

    public void start(int x) {
        for (int i = 0; i < 100; i++) {
            if (i == x) {
                errorCallback.onError("Task " + i + " is error");
            }
            callback.onDone("Task " + i + " is done");
        }
    }

}


    @FunctionalInterface
    public interface OnTaskDoneListener {

        void onDone(String result);

    }

@FunctionalInterface
public interface OnTaskErrorListener {

    void onError(String result);

}
