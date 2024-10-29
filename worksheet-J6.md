1. The output consists of interleaved messages from two threads: one printing “Good morning!” and the other printing “Good afternoon!”. Each thread starts by announcing it has started, prints its message 10 times, and then announces it is exiting. The output is not consistent across runs. The order varies as thread scheduling is nont-deterministic.

2. With the addition of Thread.sleep(1000); in the run() method of GreetingsThread, the threads now pause for 1 second between printing each message. 

3. In Java, the main method runs on the main thread. When the main method finishes executing, the main thread terminates. However, it does not exit until all threads have completed execution.

4. After adding morningThread.join(5000);, the main thread waits up to 5 seconds for morningThread to finish before proceeding. Here’s how it affects the program:

5. The key difference is the waiting duration: join() waits until completion, while join(10) waits for a specified maximum time.

6. isAlive() checks a thread’s status without affecting thread execution, while join() actively waits for a thread to complete.

7.

On your marks, get set, go!
Tortoise lap 1
Hare lap 1
Cheetah lap 1
Cheetah lap 2
Hare lap 2
Cheetah lap 3
...
CheetahFinished!
HareFinished!
TortoiseFinished!

Cheetah: With a speed of 50, the sleep time per lap is 1000 / 50 = 20 milliseconds.
Hare: With a speed of 20, the sleep time per lap is 1000 / 20 = 50 milliseconds.
Tortoise: With a speed of 5, the sleep time per lap is 1000 / 5 = 200 milliseconds.

The cheetah finishes first because it has the shortest sleep duration (fastest speed), completing laps quickly. The hare finishes second, and the tortoise finishes last due to the longest sleep duration (slowest speed). The threads finish in the order of their speeds because faster animals have shorter sleep times between laps.

8. 
public class AnimalFootRace {
    public static void main(String[] args) {
        Thread tortoiseThread = new AnimalRacerThread("Tortoise", 5);
        Thread hareThread = new AnimalRacerThread("Hare", 20);
        Thread cheetahThread = new AnimalRacerThread("Cheetah", 50);

        System.out.println("On your marks, get set, go!");
        hareThread.start(); // Start hare first

        try {
            Thread.sleep(500); // Wait 500 milliseconds before starting others
        } catch (InterruptedException e) {
            System.out.println("Interrupted while sleeping...");
        }

        tortoiseThread.start();
        cheetahThread.start();
    }
}

9. 
public class AnimalFootRace {
    public static void main(String[] args) {
        Thread tortoiseThread = new AnimalRacerThread("Tortoise", 5);
        Thread hareThread = new AnimalRacerThread("Hare", 20);
        Thread cheetahThread = new AnimalRacerThread("Cheetah", 50);
        Thread aakashThread = new AnimalRacerThread("Aakash", 100); // i am twice as fast as a cheetah

        System.out.println("On your marks, get set, go!");
        tortoiseThread.start();
        hareThread.start();
        cheetahThread.start();
        aakashThread.start(); 
    }
}

Adding myself as an "animal" with an incredible speed of 100 means I take 10 milliseconds per lap

10. Yes, it is possible in the provided Singleton implementation. Since the getInstance() method is not synchronized, if two threads call this method simultaneously when singletonInstance is null, both may pass the if (singletonInstance == null) check before either assigns a new Singleton instance. This can result in both threads creating separate instances, violating the singleton pattern’s intent.

11. Because we added the synchronized keyword, only one thread can exectue this method at a time. Other threads attempting to execute any synchronized method of the same object must wait until the first thread exits the method.

12. 
SimpleThreadOne prints numbers from 1 to 2000. It then sets statusFlag to true and prints a message indicating the change. SimpleThreadTwo may not print any output and appears to hang.

13. Adding the volatile keyword to statusFlag ensures that any read or write to this variable goes directly to main memory, making it immediately visible to all threads.

14. Race conditions may occur if two threads call makeBid simultaneously. Both threads might read the same currentHighestBid and secondHighestBid values before either updates them. This can lead to incorrect updates, such as both threads setting currentHighestBid and secondHighestBid based on outdated information.

public synchronized void makeBid(int amount) {
    if (amount > currentHighestBid) {
        secondHighestBid = currentHighestBid;
        currentHighestBid = amount;
    } else if (amount > secondHighestBid) {
        secondHighestBid = amount;
    }
}
