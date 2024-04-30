import java.util.ArrayList;

public class Prodcons {
    public static void main(String[] args) {
        ArrayList<Integer> buffer = new ArrayList<Integer>();
        Producer p1 = new Producer(buffer);
        Consumer c1 = new Consumer(buffer);
        
        Thread t1 = new Thread(p1);
        Thread t2 = new Thread(c1);
        t1.start();
        t2.start();
        
    }
}

class Producer implements Runnable {
    private int i = 0;
    int max = 10;
    ArrayList<Integer> buffer;

    public Producer(ArrayList<Integer> buffer) {
        this.buffer = buffer;
    }

    public void run() {
        try {
            while (true) {
                i++;
                produce(i);
            }
        } catch (InterruptedException e) {
            System.out.println("Exception");
        }
    }

    public void produce(int i) throws InterruptedException {
        synchronized (buffer) {
            while (buffer.size() == max) {
                System.out.println("full");
                buffer.wait();
            }
            buffer.add(i);
            synchronized (buffer) {
                buffer.notify();
            }
        }
    }
}
class Consumer implements Runnable {
    private int i = 0;
    int max = 10;
    ArrayList<Integer> buffer;

    public Consumer(ArrayList<Integer> buffer) {
        this.buffer = buffer;
    }

    public void run() {
        try {
            while (true) {
                i--;
                consume(i);
            }
        } catch (InterruptedException e) {
            System.out.println("Exception");
        }
    }

    public void consume(int i) throws InterruptedException {
        synchronized ( buffer) {
            while(buffer.size()==0) {
                System.out.println("Buffer is empty");
                buffer.wait();
            }
            buffer.remove(0);
            synchronized (buffer) {
                buffer.notify();
                
            }
        }
    }
}
