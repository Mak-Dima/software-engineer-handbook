## Custom Executor:
To implement a custom executor, conform a type to the SerialExecutor protocol and integrate it into an actor.    
### Benefits of Custom Executor.

- Thread Affinity: Forces actor execution onto a specific thread or queue. Essential for APIs that demand operations occur on a designated thread (e.g., audio processing threads, database connection limits).

- Legacy Interoperability: Bridges Swift Concurrency with existing C/C++ libraries, custom threading models, or older Grand Central Dispatch (GCD) architectures without rewriting the underlying scheduling logic.

 - Custom Scheduling Logic: Enables strict control over task prioritization, throttling, and execution order, bypassing the default Swift cooperative thread pool mechanics.

- Resource Isolation: Prevents specific intensive operations from exhausting the global concurrent thread pool, reducing the risk of thread starvation for the rest of the application.

```swift
import Foundation

// 1. Define the Custom Executor
final class DispatchSerialExecutor: SerialExecutor {
    private let queue: DispatchQueue

    init(queue: DispatchQueue) {
        self.queue = queue
    }

    // Dispatch the job onto the specific queue
    func enqueue(_ job: UnownedJob) {
        let unownedExecutor = asUnownedSerialExecutor()
        queue.async {
            job.runSynchronously(on: unownedExecutor)
        }
    }

    func asUnownedSerialExecutor() -> UnownedSerialExecutor {
        UnownedSerialExecutor(ordinary: self)
    }
}

// 2. Assign the Executor to an Actor
actor DatabaseActor {
    // Hold a strong reference to the executor
    private let customExecutor: DispatchSerialExecutor

    // Override the default executor requirement
    nonisolated var unownedExecutor: UnownedSerialExecutor {
        customExecutor.asUnownedSerialExecutor()
    }

    init(queue: DispatchQueue) {
        self.customExecutor = DispatchSerialExecutor(queue: queue)
    }

    func performDatabaseOperation() {
        // This executes on the provided DispatchQueue
    }
}
```