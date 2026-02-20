## Async code kata

- [Async code kata](#async-code-kata)
- [Example 1](#example-1)
- [Example 2](#example-2)
- [Exercise](#exercise)
  - [asyncio.Queue](#asyncioqueue)
  - [Problem 1: Communication](#problem-1-communication)
  - [Problem 2: Scale \& Communication](#problem-2-scale--communication)
  - [Problem 3: Results](#problem-3-results)


## Example 1

This a simple async function. It's marked as async by using `async def`

```python
import asyncio

async def hello_world():
    print("Hello World!")

asyncio.run(hello_world())

# output:
# Hello World!
```

## Example 2

This is an example of 2 async tasks that run as a group.
1. `await` signals that the async task will "wait" for a response from another async task.
    - when this happens, execution switches to another async task
    - until it has to await something, at which point execution switches to another
    - and so on...
2. `gather` is a function that runs several async tasks at once and "gathers" their return values (if any)
    - since `gather` is an async function itself, it has to be defined in an async function
    - which can then be run in a non-async context using `asyncio.run`

Notes:

- it is not possible to call async functions directly from non-async code. doing something like `hello_world()` with an async function will simply have no effect - the async code will only run with `await` or `asyncio.run` etc.
- async functions do NOT switch execution to another unless `await` is used.
  - this is in contrast to `threading`, where this switching happens at random points that you have no control over
  - this is the pivotal, main distinction between `async` and `threads`
- if you need to switch control to another async function without actually doing anything, you can use `await asyncio.sleep(0)`
- print debugging/logging is your friend when writing async code. As the number of async tasks grows, so does the complexity of their interactions, and it's not always possible to use unit testing alone in order to ensure expected behaviour and avoid deadlocks

```python
async def hello_world():
    await asyncio.sleep(1)
    return 'Hello World!'

async def testr():
    return 123

async def main():
    return await asyncio.gather(
        asyncio.create_task(hello_world()),
        asyncio.create_task(testr()),
    )

result = asyncio.run(main())
print(f'{result=}')

# output:
# result=['Hello World!', 123]
```

## Exercise

> official docs: https://docs.python.org/3/library/asyncio.html

The above code contains a basic "producer-consumer" example.

- There are 2 functions that are connected by a `Queue`.
- One function puts items on the queue
- And the other function pops items off the queue and does some work on it (in this case it just sleeps)
- You can modify any part of the code you like, except
  - keep the queue as-is (size 50)
  - keep the producer and consumer as the only 2 functions that use the queue
  - keep the sleep times
  - keep the number of items (100)

```python
import asyncio
import time

async def consumer(id: str, queue: asyncio.Queue):
    total = 0
    while True:
        item = await queue.get()
        print(f'-> \x1b[31m{id:<10s}Consumed {item!r}, qsize: {queue.qsize()}\x1b[0m', flush=True)
        total += item
        await asyncio.sleep(0.1) # don't modify this!
        queue.task_done()
    return total

async def producer(id, queue, items):
    for i in items:
        await queue.put(i)
        print(f'+ \x1b[32m{id:<10s}Produced {i}\x1b[0m', flush=True)
        await asyncio.sleep(0.01) # don't modify this!

async def qmain():
    queue = asyncio.Queue(maxsize=50)
    tasks = [
        asyncio.create_task(producer('p1', queue, range(100))),
        asyncio.create_task(consumer('c1', queue)),
    ]
    start = time.time()

    result = await asyncio.gather(*tasks))

    print(f'time taken: {time.time()-start})
    return result

result = asyncio.run(qmain())
print(f'{result=}')

# output:
#  + p1        Produced 0
# -> c1        Consumed 0, qsize: 0
# ...
# -> c1        Consumed 99, qsize: 0
...
```

### asyncio.Queue

The `queue` is a handy class from `asyncio` that supports `put` and `get` (among other things).
- each `put` and `get` is awaitable, meaning that async functions can coordinate without causing bad things to happen (like what happens when you modify a dict with `.pop` as you loop through it).
- giving the queue a `maxsize` means that if the queue already has that many items, a call to `put` will wait until the queue has `< maxsize` items. It can wait indefinitely for this to happen
- calling `get` on a queue with 0 items will wait (indefinitely) until there is an item on the queue.

### Problem 1: Communication

1. Estimate how long the above code should (roughly) take to run. Write down your prediction to check it later
2. Does the code above finish and print the result?
  - If not, can you figure out why?
3. Modify the code so that it finishes, by communicating it via the `queue`
  - check the total time against your prediction. if it's different, can you reason/understand why it took the time that it did?

### Problem 2: Scale & Communication

4. Run 2 more consumers alongside the existing producer & consumer. Tip: Ensure that they have unique IDs
  - Does the code run to completion? If not, can you figure out why and modify the code so that it does?
5. Estimate - what is the lowest possible theoretical time that this could run in?
6. Add more async workers until you reach close to this number (Don't modify any of the sleeps!)

### Problem 3: Results

7. Currently, the consumer functions calculate a sum and return it. Change the consumer code so that it writes each number out to a file, in the format
    ```
    consumer ID | queue item
    ```
8. Ensure that all consumers write their output to the same file