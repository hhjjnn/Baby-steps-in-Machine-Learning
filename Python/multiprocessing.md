﻿﻿﻿﻿﻿﻿﻿﻿﻿﻿﻿

# Multiprocessing in Python

## Process class: start process manually

```python
from multiprocessing import Process
# Process is defined using a task and args
def f(x):
    return x*x
# initialize the process
process = Process(target=f, args=(10,))
# start the process
process.start()
# to make sure the process is terminated after it gets results
process.join()
```

## Pool: create a pool of process and parallel computing

```python
from multiprocessing import Pool
pool = Pool(4)
# apply() is not doing things in parallel. It's doing one by one
pool.apply(func=, args=)
# apply_async() is parallel
pool.apply_async(func=, args=)
```

## Communicate between processes using Manager and Queue

    import multiprocessing as mp

```python
# worker to transform data
def worker(data,q):
    # transform data and put it to queue
    q.put(transform(data))

# process queue
def listener(q):
    # get message from queue
    while True:
        message = q.get()
        # stop listening when killed
        if message == 'kill':
            break
        #write message to file
        with open(path) as file:
            write(message, file)

def main():
    # start a manager to manage multiprocessing
    manager = mp.Manager()
    # start a shared queue as a separate process
    # Manager Queue can be passed around processs generated
    # by Pool while mp.queue may have some problem
    q = manager.Queue()
    # create pool of processes
    pool = mp.Pool(4)

    # start listener
    watcher = pool.apply_async(listener, (q,))

    for data in data_set:
        pool.apply_async(func=worker, args=(data,q))

    # kill listener and close pool
    q.put('kill')
    pool.close()
```

## Apply lock on parallel process

```python

```
