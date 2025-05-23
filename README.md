# Module 10

Hafizh Surya Mustafa Zen 2306256343

## 1.2 Understanding how it works.

### The screenshot

![Program Output](image\timer1.png)

When spawner.spawn(async { ... }) is called, the async task gets added to a queue but doesn’t start right away. Meanwhile, the synchronous line println!("Brian's Komputer: hey hey"); runs immediately, so “hey hey” is printed first—before the executor even starts polling the task. The actual execution begins only after the spawner is dropped and executor.run() is called.

Inside the executor’s loop, the task is polled for the first time, which prints “howdy!” and sets a 2-second timer, then returns Poll::Pending. When the timer completes, it re-schedules the task, and on the second poll, the future finishes and prints “done!”. This explains why you see the output in that specific order: the sync print happens first, followed by the async prints during the task's two-stage execution.